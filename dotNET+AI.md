url : https://devblogs.microsoft.com/dotnet/announcing-dotnet-ai-template-preview2/
2025年4月17日
.NET AI 模板預覽版 2 現已推出
喬丹馬蒂森
喬丹馬蒂森
高級產品經理

目錄
🛠 安裝更新的模板
🚀 .NET AI 聊天範本入門
預覽版 2 中的新增功能
主要功能和配置選項
🔍 在 Visual Studio 中使用模板
💻 使用 Visual Studio Code 和 C# Dev Kit
🚀 新增 .NET Aspire Orchestration
🔮 下一步計畫 – 分享您的回饋
閱讀下文
2025年4月22日
AI Dev Gallery 隆重推出：使用 .NET 進行本地 AI 開發的門戶
喬恩·加洛韋路易斯金塔尼利亞
喬恩，
路易斯
2025年4月22日
使用 SignalR 建立即時 iOS 應用程式：Swift 官方客戶端介紹（公開預覽版）
郭凱文
郭凱文
我們很高興地宣布，.NET AI Chat Web App 模板的預覽版 2 現已推出！此次更新帶來了令人興奮的新功能，包括對 .NET Aspire 的支援以及使用 .NET Aspire 時與 Qdrant 向量資料庫的集成，從而可以更輕鬆地創建雲原生 AI 驅動的聊天應用程式。我們的 .NET AI 範本將繼續成為我們持續努力的一部分，透過在 Visual Studio、Visual Studio Code 和 .NET CLI 中提供鷹架和指導來簡化使用 .NET 進行 AI 開發。

🛠 安裝更新的模板
要開始使用預覽版 2，您需要從終端機安裝 Microsoft.Extensions.AI.Templates。只需運行：


複製
dotnet new install Microsoft.Extensions.AI.Templates
安裝後，範本可在 Visual Studio 和 Visual Studio Code（帶有 C# Dev Kit）中使用，或者您可以透過執行以下命令直接在工作目錄中建立它：


複製
dotnet new aichatweb
在未來的版本中，我們計劃將此範本作為 .NET SDK 的一部分。

🚀 .NET AI 聊天範本入門
.NET AI Chat 範本旨在幫助您快速建立可以與自訂資料互動的 AI 聊天應用程式。此版本繼續使用聊天應用程式常採用的檢索增強生成 (RAG) 模式，並為 .NET Aspire 開發人員引入了新的選項。

預覽版 2 中的新增功能
.NET Aspire 支援：使用 .NET Aspire 擴充您的開發工具包，實現進階 AI 功能和強大的整合選項。

Qdrant 向量資料庫：預覽版 2 包含使用 Qdrant 向量資料庫的範例，進一步增強您使用向量資料製作原型和擴展應用程式的能力。

支援 VS Code 中的配置選項：現在，當使用範本建立具有 C# Dev Kit 擴充功能的新專案時，您可以選擇配置其他選項並選擇模型服務提供者以及向量儲存。

主要功能和配置選項
使用自訂資料聊天：使用 RAG 模式與範例 PDF 或您自己的資料建立基於聊天的 UI 互動。

本地和 Azure 整合：選擇本地向量儲存進行快速原型設計，或選擇 Azure AI 搜尋進行更進階的場景。

可自訂的程式碼：輕鬆調整生成的程式碼以滿足您的專案需求，包括聊天互動、引用追蹤和後續建議。

資料擷取：使用內建程式碼進行擷取、快取和處理，處理各種資料來源和格式。

🔍 在 Visual Studio 中使用模板
從命令列安裝範本後，您可以在 Visual Studio 中的檔案 > 新專案...下找到它，搜尋「AI Chat」或選擇 AI 專案類型來定位範本。

Visual Studio 建立新專案對話框，顯示已選取 AI 專案類型的 AI 聊天 Web 應用程式模板

命名您的項目，選擇其位置，並透過選擇 AI 模型提供者和向量儲存（現在包括使用 Qdrant 向量儲存的選項）來配置您的設定。

AI Chat Web App 範本的專案配置選項顯示模型提供者和向量儲存選擇

您可以從 .NET AI 範本文件中了解每個選項。

💻 使用 Visual Studio Code 和 C# Dev Kit
要在 Visual Studio Code 中使用模板，請先安裝 C# Dev Kit 擴充功能。然後，使用.NET：New Project...指令並選擇AI Chat Web App範本。這將預設使用 GitHub 模型和本地向量儲存來建立一個新項目，其他選項詳見 .NET AI 範本文件。

使用 C# Dev Kit 在 Visual Studio Code 中建立 AI 聊天 Web 應用程式的動畫演示，圖片

🚀 新增 .NET Aspire Orchestration
.NET AI 範本的最新更新引入了 .NET Aspire Orchestration，為本地和基於雲端的 AI 模型提供了強大、靈活的整合。透過選擇“使用 .NET Aspire Orchestration”，範本將建立一個新的 .NET Aspire 解決方案，其中包括一個 .AppHost 項目，該項目配置了與各種 AI 服務和向量儲存提供者合作的整合。

.NET AI 範本配置對話方塊顯示使用 .NET Aspire Orchestration 複選框選項

您可以使用 Ollama 透過 docker.io/ollama/ollama 容器映像託管本機模型，透過 OllamaSharp 存取（由 .NET Aspire Community Toolkit Ollama 整合啟用）。此功能提供了一種在本地部署容器化 AI 模型的無縫方法。

此次更新還包括使用 .NET Aspire Azure OpenAI 整合對 GitHub Models、OpenAI 和 Azure OpenAI 的支持，從而允許透過 Azure 的安全性環境或 OpenAI API 輕鬆連接到高級語言模型。此外，開發人員可以利用支援 Azure AI Search 和 Qdrant 向量儲存的增強語義搜尋功能，為企業和開源解決方案提供高效的向量化資料索引和查詢。

入門很簡單：使用更新的範本命令建立具有 .NET Aspire 啟用配置的專案。無論是利用本地 Ollama 模型、OpenAI 服務還是強大的向量儲存選項，這些工具都為尖端 AI 開發提供了全面的框架。

🔮 下一步計畫 – 分享您的回饋
我們會根據您的回饋不斷努力改進 .NET AI 模板。未來版本將包括控制台和最小 API 模板、對 Azure AI Foundry 的擴展支援以及與語義核心團隊的更深層的整合。我們計劃在 .NET SDK 中預設包含該模板，您的輸入將幫助我們為 .NET 開發人員塑造最佳體驗。

取得.NET AI模板
讓我們知道什麼對您有用以及您希望改進什麼。感謝您試用 .NET AI 範本的預覽版 2，祝您寫程式愉快！
