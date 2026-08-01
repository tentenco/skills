# 來源與截圖概念分析

## 兩張 `ref/` 截圖

第一張圖把整個方法濃縮成雙欄分工：左側 Codex 不只是把 prompt 轉貼給右側 ChatGPT Pro，而是擔任專案經理、技術負責人與 QA；右側 Pro 則提供較長時間的推理、設計與候選實作。真正的重點是「Codex 保留最終判斷權」，不是讓兩個模型互相聊天。

第二張圖把同一概念產品化：不再反覆手動上傳 repository ZIP，而是用 `rebel0789/codexpro` 把一個明確 workspace 透過 ChatGPT Developer Mode 的 MCP tools 提供給 Pro。這降低來源過期與人工搬運錯誤，但也把風險從「ZIP 洩密」轉成「公開 connector、工具權限與 workspace 邊界」。

## 微信文章

文章〈目前最强的编程 Agent，不是 Fable 5，而是「用Codex指挥ChatGPT Pro」〉主張的不是模型排行榜，而是一個責任鏈：Codex 先讀 repo、整理安全的上下文與可驗收任務，Pro 做深度工程工作，Codex 再檢查實際檔案、執行測試、把具體失敗送回同一個 Pro 對話修正。文章中特別有價值的原則包括：保留 dirty work、排除 secrets、記錄來源 baseline 與 ZIP SHA-256、不要打斷長推理、不要讓使用者充當兩個 agent 之間的信差，以及沒有明確授權時不得 commit、push、部署或操作 production。

原文：https://mp.weixin.qq.com/s/xspmSmOfa8Ve47VCjmEXLw

## `rebel0789/codexpro`

在本次稽核的 `0.29.0` 版本中，CodexPro 是 repository-scoped MCP server，不是模型代理、額度繞過器或作業系統 sandbox。它提供讀檔、tree、search、write/edit/apply-patch、受限 bash 與 change inspection；`handoff` 模式適合先規劃，workspace write mode 才允許一般程式修改。公開 quick tunnel 必須保留 token、限制 workspace root，並把 connector URL 當密鑰處理。

來源：https://github.com/rebel0789/codexpro

## 上游 `daijro/camoufox`

Camoufox 是經過反指紋修改的 Firefox 發行版，適合作為 ChatGPT Web 的 headed、persistent-profile 瀏覽器層。本 workspace 不啟動 Chromium、Google Chrome for Testing、agent-browser 或獨立 Playwright 腳本。需要透明說明的是：Camoufox 官方 Python API 內部本來就以 Playwright transport 控制它的 patched Firefox；這是上游 Camoufox 的實作依賴，不等於另外啟動一套 Playwright/Chromium automation。

來源：https://github.com/daijro/camoufox

## 合併後的可執行架構

```text
使用者意圖與權限
  -> Codex 讀 repo、寫 acceptance criteria、保管最終判斷
  -> Camoufox 操作使用者已登入的 ChatGPT Pro Web
  -> CodexPro 以含 token 的 HTTPS MCP 暫時暴露單一 workspace
  -> ChatGPT Pro 讀檔並產生候選修改
  -> Codex 本機檢查、測試、瀏覽器 QA
  -> 具體 defect 回到同一 Pro 對話修正
  -> Codex 重驗後才回報完成
```

MCP lane 是首選；無法使用 Developer Mode 時才用經過 secret scan、附 manifest 與 SHA-256 的最小 ZIP fallback。兩條路徑都不能把 Pro 的文字聲明當成完成證據。
