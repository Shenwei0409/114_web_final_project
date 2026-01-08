
# 114_web_final_project
資管3C 網路程式設計

## 一、專案主題與目標

### 專案主題
本專案為一個前後端分離的活動報名系統，使用者可透過網頁填寫報名資料完成活動報名，管理者可登入後台進行報名名單管理。系統完整實作 CRUD 功能，並整合 MongoDB 作為資料庫，符合課程期末專題之專案主題與技術要求。

### 專案目標
- 建立一個具備前後端整合的完整 Web 應用系統    
- 提供使用者友善的報名介面與即時表單驗證  
- 建立管理者登入機制以保護報名名單資料  
- 使用資料庫儲存並管理所有報名資料  

## 二、技術選擇原因

### 前端技術（React）
- 使用 React 進行元件化開發，提升程式碼可維護性  
- 透過 React Hooks 管理狀態與畫面更新  
- 使用 React Router 實作多頁面切換（報名頁、登入頁、管理頁）  
- 使用 Axios 與後端 API 進行資料串接  

React 為現代主流前端框架，適合開發互動式使用者介面。

### 後端技術（Node.js / Express）
- 使用 Node.js 與 Express 建立 RESTful API  
- 清楚區分 routes 與 models，提升專案結構清晰度  
- 統一 API 回傳格式並搭配 HTTP 狀態碼  
- 實作管理者登入驗證，限制名單管理功能存取  

Express 架構輕量且彈性高，適合 API 伺服器開發。

### 資料庫（MongoDB）
- 使用 MongoDB 作為 NoSQL 資料庫  
- 搭配 Mongoose 定義資料模型與結構  
- 適合儲存活動報名資料，並可彈性擴充欄位  
- 提供快速查詢與資料更新能力  

## 三、系統架構說明

本系統採用前後端分離架構，系統運作流程如下：
- 使用者透過瀏覽器操作前端網頁  
- 前端以 Axios 呼叫後端 RESTful API  
- 後端使用 Express 接收請求並處理商業邏輯  
- 後端透過 Mongoose 與 MongoDB 進行資料存取  
- 後端回傳 JSON 格式資料給前端顯示  

## 四、安裝與執行指引

### 環境需求
- Node.js(v18以上)
- npm
- MongoDB（本機端）

### 啟動 MongoDB
請確認本機 MongoDB 已啟動，並監聽於：mongodb://127.0.0.1:27017

### 後端安裝與啟動
cd 114_web_final_project/backend
npm install
npm run dev
正確顯示:
MongoDB connected 
Server running on http://localhost:5000

### 前端安裝與啟動
cd 114_web_final_project/frontend
npm install react-router-dom
npm install
npm start
完成後於 http://localhost:3000 開啟
管理者密碼:0000