MinerU v2.1：Sglang參數透傳/顯存要求降低
https://blog.csdn.net/qq1198768105/article/details/149140536
原創 於 2025-07-05 18:43:35 發佈 · 1.7k 閱讀
今天(2025.7.5)，MinerU 發佈了v2.1.0版本，更新內容如下：
性能優化：
•	大幅提升某些特定解析度（長邊2000圖元左右）文檔的預處理速度
•	大幅提升pipeline後端批量處理大量頁數較少（<10）文檔時的後處理速度
•	pipline後端的layout分析速度提升約20%
體驗優化：
•	內置開箱即用的fastapi服務和gradio webui
•	sglang適配0.4.8版本，大幅降低vlm-sglang後端的顯存要求，最低可在8G顯存(Turing及以後架構)的顯卡上運行
•	對所有命令增加sglang的參數透傳，使得sglang-engine後端可以與sglang-server一致，接收sglang的所有參數
•	支援基於設定檔的功能擴展，包含自訂公式識別字、開啟標題分級功能、自訂本地模型目錄
新特性：
•	pipeline後端更新 PP-OCRv5 多語種文本識別模型，支援法語、西班牙語、葡萄牙語、俄語、韓語等 37 種語言的文字識別，平均精度漲幅超30%。
•	pipeline後端增加對豎排文本的有限支援
MinerU 開源倉庫：https://github.com/opendatalab/MinerU
主要內容解讀
1. vlm-sglang 顯存需求降低
之前的文章測試過，MinerU v2.0 版本的vlm-sglang至少需要 24GB 的顯存，主要原因並不是模型參數量高，而是 sglang 預設分配了較大的靜態記憶體(包含模型權重和 KV Cache 池)，用來提升輸出速度。
在此版本中，MinerU 支援了 sglang 參數的透傳，因此可以控制靜態記憶體分配的比例，從而減小顯存需求。
下面進行具體測試，首先搭建測試環境：
uv venv --python 3.12
初始化並啟動環境：
uv init
source .venv/bin/activate
安裝完整版mineru：
uv add "mineru[all]"
用命令列的方式進行解析調用：
mineru -p shencha.pdf -o result --source modelscope -b vlm-sglang-engine
預設顯存佔用情況如下圖所示，約佔用 36 GB 顯存。
 
下面通過設置參數--mem-fraction-static，讓靜態記憶體的佔用降低，在未設置的情況下，其預設值是0.9。
 	mineru -p shencha.pdf -o result --source modelscope -b vlm-sglang-engine --mem-fraction-static 0.5
顯存佔用顯著減小，約佔用 23 GB。
 
由於 MinerU 本身的模型參數量不高，因此，可以將該值設置得更小，比如設置為0.1，顯存佔用約 6.8 GB。
 
調低靜態顯存分配理論會降低速度，但實測解析速度差距不明顯。
官方文檔提到，對於多卡伺服器，還可以通過張量並行得方式擴充可用顯存--tp 2，也可以通過多卡並行模式來增加輸送量--dp 2。
但實測發現，tp 和 dp 透傳還有點問題，暫未支持。
報錯信息：
TypeError: ServerArgs.__init__() got an unexpected keyword argument 'tp'
文檔還提到，可以用--enable-torch-compile參數去加快推理速度，但實測發現，容易觸發共用記憶體溢出的問題，反而會降低推理速度，報錯資訊：
Runtime error during autotuning: 
[rank0]:E0705 15:48:23.150000 434379 torch/_inductor/select_algorithm.py:2100] [8/6] No valid triton configs. OutOfResources: out of resource: shared memory, Required: 110592, Hardware limit: 101376. Reducing block sizes or `num_stages` may help.. 
2. Fastapi支持
該版本新增了fastapi服務，可直接通過命令列啟動：
mineru-api --host 127.0.0.1 --port 8000
啟動後，會顯示Swagger和ReDoc形式的文檔位址，可在Swagger中，直接進行調用測試。
 
3. Webui支持
該版本新增了基於 gradio 的 webui 介面，可直接通過命令列啟動：
mineru-gradio --server-name 127.0.0.1 --server-port 7860
 
4. 設定檔回歸
在 v2.0 版本中，移除了json的位置檔，在此版本中，可通過設定檔mineru.json進一步進行功能拓展，主要有以下可配置選項：
•	latex-delimiter-config：用於配置 LaTeX 公式的分隔符號，預設為$符號，可根據需要修改為其他符號或字串。
•	llm-aided-config：用於配置 LLM 輔助標題分級的相關參數，相容所有支援openai協定的 LLM 模型，預設使用阿裡雲百練的qwen2.5-32b-instruct模型，可配置 API 金鑰並將enable設置為true來啟用此功能。
•	models-dir：用於指定本地模型存儲目錄，請為pipeline和vlm後端分別指定模型目錄，指定目錄後您可通過配置環境變數export MINERU_MODEL_SOURCE=local來使用本地模型。
檔範本內容如下：
{
    "bucket_info":{
        "bucket-name-1":["ak", "sk", "endpoint"],
        "bucket-name-2":["ak", "sk", "endpoint"]
    },
    "latex-delimiter-config": {
        "display": {
            "left": "$$",
            "right": "$$"
        },
        "inline": {
            "left": "$",
            "right": "$"
        }
    },
    "llm-aided-config": {
        "title_aided": {
            "api_key": "your_api_key",
            "base_url": "https://dashscope.aliyuncs.com/compatible-mode/v1",
            "model": "qwen2.5-32b-instruct",
            "enable": false
        }
    },
    "models-dir": {
        "pipeline": "",
        "vlm": ""
    },
    "config_version": "1.3.0"
}
所謂標題分級，就是借助 llm 的API，根據內容將文本分成一級標題、二級標題、三級標題等結構，使其更結構化，文檔中並未詳細介紹，具體可參考issue#1730：https://github.com/opendatalab/MinerU/issues/1730
