# 部署指南 (Deployment Guide)

本指南將協助您將「2026 Travel Date 旅遊規劃網站」部署到各種平台。

## 📋 目錄

- [部署前準備](#部署前準備)
- [GitHub Pages 部署](#github-pages-部署)
- [Netlify 部署](#netlify-部署)
- [Vercel 部署](#vercel-部署)
- [傳統主機部署](#傳統主機部署)
- [本地測試](#本地測試)
- [疑難排解](#疑難排解)

---

## 部署前準備

### ✅ 檢查清單

在部署前，請確認以下項目：

- [ ] 所有 HTML 檔案正常開啟
- [ ] 無 JavaScript 錯誤（開啟瀏覽器 Console 檢查）
- [ ] 圖片與外部資源正常載入
- [ ] 在不同瀏覽器測試（Chrome, Firefox, Safari）
- [ ] 響應式設計在手機上正常顯示

### 📁 必要檔案

確認專案包含以下檔案：

```
2026 Travel Date/
├── index.html
├── taiwan_holidays.html
├── school_calendar.html
├── asia_holidays.html
├── README.md
└── .gitignore (選用)
```

---

## GitHub Pages 部署

### 方法 1: 透過 GitHub 網頁介面

#### 步驟 1: 創建 GitHub Repository

1. 登入 [GitHub](https://github.com)
2. 點擊右上角「+」→「New repository」
3. 設定：
   - Repository name: `2026-travel-date-web`
   - 選擇 Public 或 Private
   - 不勾選 "Add a README file"
4. 點擊「Create repository」

#### 步驟 2: 上傳檔案

1. 在新建的 Repository 頁面，點擊「uploading an existing file」
2. 拖曳所有專案檔案到瀏覽器
3. 輸入 Commit message: `Initial commit`
4. 點擊「Commit changes」

#### 步驟 3: 啟用 GitHub Pages

1. 進入 Repository，點擊「Settings」
2. 左側選單找到「Pages」
3. 在「Source」選擇「Deploy from a branch」
4. Branch 選擇「main」（或 master），資料夾選「/ (root)」
5. 點擊「Save」

#### 步驟 4: 訪問網站

等待 1-2 分鐘後，訪問：
```
https://jason-hey.github.io/2026-travel-date-web/
```

### 方法 2: 透過 Git 指令

```bash
# 1. 初始化 Git
cd "C:\Users\talet\OneDrive\Desktop\Out\[] My Project\2026 Travel Date"
git init

# 2. 添加檔案
git add .
git commit -m "Initial commit"

# 3. 連結遠端 Repository（替換成你的 GitHub URL）
git remote add origin https://github.com/jason-hey/2026-travel-date-web.git

# 4. 推送到 GitHub
git branch -M main
git push -u origin main
```

然後依照「方法 1 - 步驟 3」啟用 GitHub Pages。

---

## Netlify 部署

### 方法 1: 拖放上傳（最簡單）

#### 步驟 1: 準備資料夾

將所有檔案放在同一層資料夾（不要巢狀資料夾）。

#### 步驟 2: 部署

1. 訪問 [Netlify Drop](https://app.netlify.com/drop)
2. 直接拖曳整個專案資料夾到網頁
3. 等待上傳完成
4. Netlify 會自動生成一個 URL，例如：
   ```
   https://random-name-12345.netlify.app
   ```

#### 步驟 3: 自訂網域（選用）

1. 點擊「Domain settings」
2. 點擊「Options」→「Edit site name」
3. 輸入自訂名稱，例如：`2026-travel-date`
4. 新 URL：`https://2026-travel-date.netlify.app`

### 方法 2: 連結 GitHub Repository

#### 步驟 1: 先部署到 GitHub（參考上方 GitHub Pages 步驟）

#### 步驟 2: 連結到 Netlify

1. 登入 [Netlify](https://app.netlify.com)
2. 點擊「Add new site」→「Import an existing project」
3. 選擇「GitHub」
4. 授權 Netlify 存取你的 GitHub
5. 選擇你的 Repository
6. 設定：
   - Build command: 留空
   - Publish directory: `/`（根目錄）
7. 點擊「Deploy site」

#### 優點
- ✅ 每次 `git push` 自動部署
- ✅ 支援 HTTPS
- ✅ 自動 CDN 加速
- ✅ 可設定自訂網域

---

## Vercel 部署

### 方法 1: 透過 GitHub（推薦）

#### 步驟 1: 部署到 GitHub（參考上方）

#### 步驟 2: 連結到 Vercel

1. 訪問 [Vercel](https://vercel.com)
2. 點擊「Add New」→「Project」
3. 選擇「Import Git Repository」
4. 授權 Vercel 存取 GitHub
5. 選擇你的 Repository
6. 設定：
   - Framework Preset: **Other**
   - Build Command: 留空
   - Output Directory: `./`
7. 點擊「Deploy」

#### 步驟 3: 訪問網站

部署完成後，Vercel 會提供：
```
https://2026-travel-date.vercel.app
```

### 方法 2: 使用 Vercel CLI

```bash
# 1. 安裝 Vercel CLI
npm install -g vercel

# 2. 登入
vercel login

# 3. 在專案資料夾執行
cd "C:\Users\talet\OneDrive\Desktop\Out\[] My Project\2026 Travel Date"
vercel

# 4. 按照提示操作
# - Set up and deploy? Yes
# - Which scope? 選擇你的帳號
# - Link to existing project? No
# - Project name? 2026-travel-date
# - In which directory is your code located? ./

# 5. 部署完成，會顯示 URL
```

---

## 傳統主機部署

### 適用於

- cPanel 主機
- FTP 主機
- 虛擬主機
- VPS

### 步驟

#### 1. 連接到主機

使用 FTP 工具（如 FileZilla）：
- Host: 你的主機 FTP 位址
- Username: FTP 使用者名稱
- Password: FTP 密碼
- Port: 21（或 22 for SFTP）

#### 2. 上傳檔案

將所有檔案上傳到：
```
/public_html/
```
或
```
/www/
```
（依主機商而定）

#### 3. 設定首頁

確保 `index.html` 在根目錄，或在主機控制台設定預設首頁為 `index.html`。

#### 4. 訪問網站

```
https://你的網域.com
```

---

## 本地測試

### 方法 1: Python 簡易伺服器

```bash
# Python 3
cd "C:\Users\talet\OneDrive\Desktop\Out\[] My Project\2026 Travel Date"
python -m http.server 8000

# 訪問 http://localhost:8000
```

### 方法 2: Node.js http-server

```bash
# 安裝（僅需一次）
npm install -g http-server

# 啟動
cd "C:\Users\talet\OneDrive\Desktop\Out\[] My Project\2026 Travel Date"
http-server -p 8000

# 訪問 http://localhost:8000
```

### 方法 3: VS Code Live Server

1. 安裝 VS Code 擴充功能：「Live Server」
2. 右鍵點擊 `index.html`
3. 選擇「Open with Live Server」

---

## 疑難排解

### ❌ 問題：國旗圖示無法顯示

**原因**: 使用 `file://` 協定開啟，CORS 限制

**解決方案**:
- 使用上述任一本地伺服器方法
- 或部署到線上平台

---

### ❌ 問題：GitHub Pages 404 錯誤

**檢查項目**:
1. 確認檔名為 `index.html`（小寫）
2. 檢查 Settings → Pages 是否已啟用
3. 確認 Branch 選擇正確（main 或 master）
4. 等待 2-5 分鐘讓 GitHub 建置完成

**強制重新部署**:
```bash
git commit --allow-empty -m "Trigger rebuild"
git push
```

---

### ❌ 問題：Netlify 或 Vercel 部署後空白頁面

**檢查**:
1. 開啟瀏覽器 Console (F12)，查看錯誤訊息
2. 確認所有檔案路徑正確（使用相對路徑，不要用絕對路徑）
3. 檢查檔名大小寫是否一致

---

### ❌ 問題：手機版排版跑掉

**原因**: 瀏覽器快取

**解決方案**:
- 手機瀏覽器強制重新整理
- 清除瀏覽器快取
- 無痕模式測試

---

### ❌ 問題：雲朵或飛行動畫不顯示

**檢查**:
1. 瀏覽器版本是否支援 SVG filter
2. 是否有 JavaScript 錯誤（開啟 Console 檢查）
3. 確認 `<svg>` 標籤完整存在於 HTML 中

---

## 🔧 進階設定

### 自訂網域設定（以 Netlify 為例）

1. 購買網域（如從 GoDaddy, Namecheap）
2. Netlify → Domain settings → Add custom domain
3. 輸入你的網域（如 `www.mytravelsite.com`）
4. 到網域商的 DNS 設定頁面：
   - 類型: `CNAME`
   - 名稱: `www`
   - 值: `你的網站名稱.netlify.app`
   - TTL: `3600`
5. 等待 DNS 生效（可能需要 24-48 小時）

### 啟用 HTTPS

**GitHub Pages**: 自動啟用（Settings → Pages → Enforce HTTPS）

**Netlify**: 自動提供 Let's Encrypt SSL

**Vercel**: 自動提供 SSL

---

## 📊 效能優化建議

### 1. 壓縮檔案

```bash
# 安裝 html-minifier
npm install -g html-minifier

# 壓縮 HTML
html-minifier --collapse-whitespace --remove-comments --minify-css --minify-js index.html -o index.min.html
```

### 2. 使用 CDN

已使用的外部資源會自動透過 CDN 提供：
- Google Fonts
- FlagCDN

### 3. 快取設定

在 Netlify 或 Vercel 的 `netlify.toml` / `vercel.json`：

```toml
# netlify.toml
[[headers]]
  for = "/*.html"
  [headers.values]
    Cache-Control = "public, max-age=0, must-revalidate"

[[headers]]
  for = "/*.jpg"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"
```

---

## 🎯 部署平台比較

| 平台 | 優點 | 缺點 | 推薦度 |
|------|------|------|--------|
| **GitHub Pages** | 免費、與 Git 整合 | 需要 GitHub 帳號 | ⭐⭐⭐⭐ |
| **Netlify** | 超簡單、拖放即可 | 免費版有流量限制 | ⭐⭐⭐⭐⭐ |
| **Vercel** | 速度快、自動優化 | 介面較複雜 | ⭐⭐⭐⭐ |
| **傳統主機** | 完全控制 | 需要維護 | ⭐⭐⭐ |

---

## 📞 需要協助？

- 📖 參考 [README.md](README.md) 了解專案細節
- 📋 查看 [PROJECT_PROMPT.md](PROJECT_PROMPT.md) 了解完整規格
- 🐛 遇到問題請開啟 GitHub Issue

---

**🎉 恭喜！您已成功部署「2026 Travel Date」網站！**

祝您的使用者有美好的旅遊規劃體驗！✈️🌏
