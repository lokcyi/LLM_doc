# 網頁操作及自動測試程式開發利器 - Playwright for .NET 筆記  
  
之前在用 C# 呼叫 Chrome 批次產生網頁快照的簡便做法 讀者 Rong 留言提到 Playwright。最近計劃寫一些機器人程式將複雜網頁操作自動化，\
機緣成熟，這回就不用 PuppeteerSharp 了，想試試很多人推的 Playwright。  
  
Playwright 是微軟 2019 推出的網頁自動測試框架，同時支援 Chromium、Firefox 及 WebKit (Safari 採用的核心)，涵蓋所有主流瀏覽器，並能跨平台執行。  
  
對我來說，Playwright 與 Selenium、PuppeteerSharp 都能實現機器人操作及自動測試，Playwright 最大優勢在於它的微軟血統。撇開保證 100% 原生支援 .NET 這點不談，  
API 介面「非常微軟」是最讓我心動的點，這有些難以言喻，但寫起來非常有感。  
  
過去每每使用移植自其他語言的程式庫，例如：NPOI、NLog... 即便是 .NET 物件、參數、方法，但凡從命名、參數傳遞方式、呼叫步驟到設定檔寫法，總能嗅出濃濃的「異國風情」，  
好比明明是中文也聽得懂，但「現在我有冰淇淋」怎麼聽就是不對勁。用 .NET 寫了幾段 Playwright 小程式，確定 Playwright for .NET 是個「Native Speaker」無誤，  
字正腔圓，流暢清晰，令人心曠神怡，舒服到心坎裡。
  
Playwright for .NET 官方文件的說明很完整，是絕佳的入門教材。我聚焦在如何用 Playwright 操作及整合瀏覽器，整理術語及重點如下：  
