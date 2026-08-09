# Architectural Decisions

這份文件記錄了 `stablecoin-demo` 專案的重要技術選型與架構決策。

## [2026-08-09] 選擇 ethers.js v6 CDN 引入

### 脈絡 (Context)
專案目標是作為一個極簡的穩定幣功能展示（Demo），需要能快速開啟並在瀏覽器中運行，無需複雜的開發環境設定。

### 決策 (Decision)
我們選擇直接透過 CDN (`https://cdn.jsdelivr.net/npm/ethers@6.10.0/...`) 引入 `ethers.js v6`，而非使用 `npm install`。

### 理由 (Rationale)
1. **零安裝成本**：任何人只要下載 `stableCoin.html` 即可立即執行。
2. **開發效率**：適合用於快速原型設計（Prototyping）。
3. **版本控制**：鎖定在 v6 版本，確保與 ethers.js 最新 API 規範相容。

## [2026-08-09] 實作事件監聽器更新狀態

### 脈絡 (Context)
MetaMask 使用者經常會在擴充功能中切換帳號或網路，若網頁未同步更新會導致顯示過期資訊。

### 決策 (Decision)
在 JavaScript 中明確監聽 `window.ethereum` 的 `accountsChanged` 與 `chainChanged` 事件。

### 理由 (Rationale)
1. **使用者體驗**：提供即時回饋，無需使用者手動重新整理頁面。
2. **健壯性**：確保顯示的餘額與當前選定的錢包帳號一致。
