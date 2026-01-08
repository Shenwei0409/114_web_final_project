## Base URL
http://localhost:5000/api

## 一、建立活動報名

路由  
POST /registrations

說明  
建立一筆新的活動報名資料。

參數（Request Body）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| name | String | 是 | 報名者姓名 |
| email | String | 是 | 電子信箱（不可重複） |
| phone | String | 是 | 電話號碼（不可重複） |
| agreed | Boolean | 是 | 是否同意服務條款 |

Request 範例
{
  "name": "王小明",
  "email": "test@gmail.com",
  "phone": "0912345678",
  "agreed": true
}

成功回應  
HTTP Status：201 Created

{
  "success": true,
  "data": {
    "_id": "65f123456789abcd",
    "name": "王小明",
    "email": "test@gmail.com",
    "phone": "0912345678",
    "agreed": true,
    "checkedIn": false,
    "createdAt": "2026-01-05T21:23:16.823Z"
  },
  "message": "Registration created"
}

失敗回應（重複報名）  
HTTP Status：409 Conflict

{
  "success": false,
  "message": "email already registered"
}

## 二、取得所有報名名單（管理者）

路由  
GET /registrations

說明  
取得所有活動報名資料，僅限管理者存取。

參數（Request Header）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| x-admin-token | String | 是 | 管理者登入後取得的驗證 token |

成功回應  
HTTP Status：200 OK

{
  "success": true,
  "data": [
    {
      "_id": "65f123456789abcd",
      "name": "王小明",
      "email": "test@gmail.com",
      "phone": "0912345678",
      "agreed": true,
      "checkedIn": true,
      "createdAt": "2026-01-05T21:23:16.823Z"
    }
  ],
  "message": "Registrations fetched"
}

失敗回應（未授權）  
HTTP Status：401 Unauthorized

{
  "success": false,
  "message": "admin unauthorized"
}

## 三、切換簽到狀態（管理者）

路由  
PUT /registrations/:id/checkin

說明  
切換指定報名者的簽到或取消簽到狀態。

參數（URL Path）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| id | String | 是 | 報名資料的唯一識別碼 |

參數（Request Header）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| x-admin-token | String | 是 | 管理者驗證 token |

成功回應  
HTTP Status：200 OK

{
  "success": true,
  "data": {
    "_id": "65f123456789abcd",
    "checkedIn": true
  },
  "message": "Registration updated"
}

## 四、刪除報名資料（管理者）

路由  
DELETE /registrations/:id

說明  
刪除指定的活動報名資料。

參數（URL Path）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| id | String | 是 | 報名資料的唯一識別碼 |

參數（Request Header）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| x-admin-token | String | 是 | 管理者驗證 token |

成功回應  
HTTP Status：200 OK

{
  "success": true,
  "data": {
    "id": "65f123456789abcd"
  },
  "message": "Registration deleted"
}

## 五、管理者登入

路由  
POST /admin/login

說明  
管理者登入並取得後台管理用的驗證 token。

參數（Request Body）

| 參數名稱 | 型別 | 必填 | 說明 |
|--------|------|------|------|
| password | String | 是 | 管理者登入密碼 |

Request 範例
{
  "password": "admin_password"
}

成功回應  
HTTP Status：200 OK

{
  "success": true,
  "data": {
    "token": "admin_token_string"
  },
  "message": "login success"
}

失敗回應（密碼錯誤）  
HTTP Status：401 Unauthorized

{
  "success": false,
  "message": "password incorrect"
}

---

備註  
- 所有管理者相關 API 皆需在 Request Header 中帶入 x-admin-token  
- API 回應格式皆統一為 JSON  
- 所有資料皆實際儲存於 MongoDB


