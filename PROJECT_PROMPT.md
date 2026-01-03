# 2026 Travel Date Website - Complete Project Prompt

## 專案概述
建立一個美觀、互動的旅遊規劃網站，提供全球旅遊時間表、台灣請假攻略、學校考試行事曆，以及日本與中國假期資訊。

---

## 整體設計風格

### 視覺主題
- **背景**: 真實的藍天漸層（從深藍 #104e8b 到淺藍 #00d2ff）
- **雲朵動畫**: 使用 SVG feTurbulence filter 創建真實的雲朵紋理
  - 雲朵尺寸: 300-700px 寬，高度為寬度的 55%
  - 動畫: 從左至右漂浮 (20-60秒)
  - 透明度: 0.3-0.7 隨機
- **空中生物動畫**: 
  - 飛機圖示 (30% 機率，20-35秒飛過，較高位置)
  - 鳥類圖示 (70% 機率，35-55秒飛過，中低位置)
  - 出現頻率: 每 8.5 秒檢查，70% 機率生成
- **風格**: Glassmorphism（玻璃擬態），帶有模糊背景和半透明效果
- **字體**: 
  - 中文: Noto Sans TC
  - 英文/數字: Poppins, Orbitron

### 色彩系統
- 主色: `#0984e3` (藍色)
- 最佳時間: `#4ecdc4` (青綠色)
- 適合旅遊: `#ffe66d` (黃色)
- 尚可: `#ff6b6b` (紅色)
- 不建議: `#f1f2f6` (淺灰色)
- 文字: `#2d3436` (深灰)

---

## 頁面結構

### 1. index.html - 全球旅遊最佳時間表

#### 功能需求
1. **國家旅遊時間表**
   - 顯示 34 個國家的 12 個月旅遊適宜度
   - 每個國家包含: 日本、韓國、泰國、義大利、法國、英國、西班牙、冰島、瑞士、挪威、瑞典、芬蘭、丹麥、希臘、土耳其、杜拜、埃及、紐西蘭、澳洲、新加坡、馬來西亞、越南、印尼峇里島、美國、加拿大、墨西哥、秘魯、阿根廷、巴西、南非、摩洛哥、肯亞、印度

2. **國旗顯示**
   - 使用 flagcdn.com API
   - 格式: `https://flagcdn.com/w40/{country-code}.png`
   - 圖示大小: 24px，圓角 2px，陰影效果

3. **表格功能**
   - 每個月份欄位顯示:
     - 旅遊季節描述（如：櫻花季、滑雪季）
     - 溫度範圍
   - 月份標題可點擊排序（依該月適宜度排序國家）
   - Hover tooltip 顯示詳細資訊

4. **國家活動 Modal**
   - 點擊任何國家列開啟彈窗
   - 顯示該國 2026 年具體活動與日期
   - 包含:
     - 國旗 (60x40px)
     - 國家名稱
     - 時間軸樣式的活動列表
     - 每個活動包含: 日期（2026 具體日期）、名稱、描述

5. **活動資料範例** (日本)
   ```javascript
   {
     date: '2026/03/25 - 04/10',
     name: '櫻花季 (Sakura)',
     desc: '全國各地的櫻花盛開，東京上野公園、京都哲學之道是賞櫻熱點。東京預計3/25開花，京都約3/28。'
   }
   ```

#### 旅遊資料結構
```javascript
travelData = {
  '日本': {
    months: [1, 1, 3, 3, 3, 2, 1, 1, 2, 3, 3, 2], // 0=不建議 1=尚可 2=適合 3=最佳
    info: ['滑雪季', '賞梅季', '櫻花季', ...],
    temps: ['5-10°C', '5-12°C', ...]
  }
}
```

---

### 2. taiwan_holidays.html - 台灣請假攻略

#### 功能需求
1. **假期請假完整攻略（列表形式，置於頂部）**
   - 顯示所有 2026 台灣法定假期
   - 包含:
     - 假期名稱
     - 日期範圍
     - 原始天數
     - 建議請假日
     - 總連休天數
     - 策略說明
   - 卡片設計，左側彩色邊框（連休超過 9 天用紅色標示）

2. **行事曆視圖**
   - 顯示 2026 年 1-12 月 + 2027 年 1 月（共 13 個月）
   - 每個月份卡片包含:
     - 月份標題（2027年1月標示「2027年 1月」）
     - 7x6 網格（日一二三四五六）
     - 日期標註:
       - Holiday (紅色): 法定假期
       - Leave (橘色): 建議請假日
       - Weekend (淡藍): 週末
   - Tooltip: Hover 顯示假期名稱或策略說明

3. **2026 台灣假期資料**
   - 元旦: 1/1，請1/2休4天
   - 春節: 2/14-2/22 (9天)，極端策略請2/23-26休16天
   - 228: 2/27-3/1 (3天，2/27補假)
   - 清明兒童節: 4/3-4/6 (4天)
   - 勞動節: 5/1-5/3 (3天)
   - 端午節: 6/19-6/21 (3天)
   - 中秋 & 教師節: 9/25-9/28 (4天)，請9/21-24休10天
   - 國慶 & 光復節: 10/9-11 (3天) + 10/24-26 (3天)
   - 行憲紀念日: 12/25-27 (3天)，請12/21-24休9天
   - 2027元旦: 1/1-1/3，請12/28-31休10天

---

### 3. school_calendar.html - 學校考試行事曆

#### 功能需求
1. **114 下學期 (2026 春季)**
   - 開學日: 2026/02/16 (一)
   - 期中考: 2026/04/21 - 04/22
   - 期末考: 2026/06/23 - 06/24
   - 暑假開始: 2026/07/01 (三)

2. **115 上學期 (2026 秋季)**
   - 開學日: 2026/08/31 (一)
   - 期中考: 2026/11/03 - 11/04
   - 期末考: 2027/01/14 - 01/15
   - 寒假開始: 2027/01/21 (四)

3. **卡片設計**
   - 顏色標示:
     - 期中考: 橘色邊框 (#f39c12)
     - 期末考: 紅色邊框 (#e74c3c)
     - 假期: 綠色邊框 (#2ecc71)
   - 每個卡片包含:
     - 考試類型標籤
     - 考試/假期名稱
     - 日期
     - 說明文字
   - 右上角大型透明數字裝飾 (Start/Mid/Final/Fun)

---

### 4. asia_holidays.html - 日本 & 中國假期

#### 功能需求
1. **雙欄布局**
   - 左欄: 日本 2026 假期
   - 右欄: 中國 2026 假期
   - 響應式: 小螢幕改為單欄

2. **日本假期資料**
   - 元日: 1/1 (四)
   - 成人の日: 1/12 (一) 三連休
   - 建國紀念之日: 2/11 (三)
   - 天皇誕生日: 2/23 (一) 三連休
   - 春分の日: 3/20 (五) 三連休
   - 昭和の日: 4/29 (三)
   - 黃金週: 5/3 - 5/6 (憲法紀念日、綠之日、兒童節、補假)
   - 海の日: 7/20 (一) 三連休
   - 山の日: 8/11 (二)
   - 敬老の日: 9/21 (一) 三連休
   - 秋分の日: 9/23 (三)
   - スポーツの日: 10/12 (一) 三連休
   - 文化の日: 11/3 (二)
   - 勤勞感謝の日: 11/23 (一) 三連休

3. **中國假期資料**
   - 元旦: 1/1 - 1/3 (3天)
   - 春節: 2/16 - 2/22 (7天黃金週)
   - 清明節: 4/4 - 4/6 (3天)
   - 勞動節: 5/1 - 5/5 (5天)
   - 端午節: 6/19 - 6/21 (3天)
   - 中秋節: 9/25 - 9/27 (3天)
   - 國慶節: 10/1 - 10/7 (7天黃金週)

4. **卡片設計**
   - 左側彩色邊框標示
   - 日本: 紅色 (#ef3340)
   - 中國: 紅色 (#de2910)，淡黃漸層背景
   - 標籤顯示假期長度 (三連休/小長假/7天長假等)

---

## 導航列設計

### 結構
所有頁面包含統一的導航列，包含 4 個連結:
1. 🌍 全球最佳時間 (index.html)
2. 🇹🇼 台灣請假攻略 (taiwan_holidays.html)
3. 📅 學校考試行事曆 (school_calendar.html)
4. 🇯🇵🇨🇳 亞洲假期 (asia_holidays.html)

### 樣式
- 當前頁面: 白色背景 + 深藍文字
- 其他頁面: 半透明白底 + 白色文字，帶邊框
- Hover: 上移 2px + 背景變深
- 圓角膠囊形狀 (border-radius: 50px)
- Backdrop blur 效果

---

## 技術實現細節

### SVG Cloud Filter
```html
<svg width="0" height="0" style="position:absolute;">
  <filter id="cloud-real">
    <feTurbulence type="fractalNoise" baseFrequency="0.012" numOctaves="5" seed="0" result="noise" />
    <feDisplacementMap in="SourceGraphic" in2="noise" scale="150" />
  </filter>
</svg>
```

### 雲朵動畫 (JavaScript)
```javascript
const cloudsContainer = document.getElementById('clouds');
for (let i = 0; i < 12; i++) {
  const cloud = document.createElement('div');
  cloud.className = 'cloud';
  const width = Math.random() * 400 + 300;
  cloud.style.width = width + 'px';
  cloud.style.height = (width * 0.55) + 'px';
  cloud.style.top = Math.random() * 100 + '%';
  cloud.style.animationDuration = (Math.random() * 40 + 20) + 's';
  cloud.style.animationDelay = (Math.random() * -60) + 's';
  cloudsContainer.appendChild(cloud);
}
```

### 飛行物動畫
```javascript
function spawnFlyingObject() {
  const el = document.createElement('div');
  el.className = 'flying-obj';
  const isPlane = Math.random() > 0.7;
  
  if (isPlane) {
    // 飛機 SVG: 較大、較快、較高
    el.innerHTML = `<svg width="32" height="32">...</svg>`;
    el.style.animation = `fly-across ${20 + Math.random() * 15}s linear forwards`;
    el.style.top = (5 + Math.random() * 40) + '%';
  } else {
    // 鳥類 SVG: 較小、較慢、中低位置
    el.innerHTML = `<svg width="24" height="24">...</svg>`;
    el.style.animation = `fly-across ${35 + Math.random() * 20}s linear forwards`;
    el.style.top = (20 + Math.random() * 50) + '%';
  }
  
  container.appendChild(el);
  setTimeout(() => el.remove(), 60000);
}

// 70% 機率每 8.5 秒生成
setInterval(() => {
  if (Math.random() > 0.3) spawnFlyingObject();
}, 8500);
```

---

## 響應式設計

### 斷點
- 桌面: > 900px
- 平板: 601px - 900px
- 手機: ≤ 600px

### 適配策略
1. **導航列**: flex-wrap，小螢幕換行
2. **表格**: 水平滾動 (overflow-x: auto)
3. **卡片網格**: 
   - 桌面: 3-4 欄
   - 平板: 2 欄
   - 手機: 1 欄
4. **Modal**: 寬度 90%，最大 600px

---

## 檔案結構
```
2026 Travel Date/
├── index.html              (全球旅遊時間表)
├── taiwan_holidays.html    (台灣請假攻略)
├── school_calendar.html    (學校考試行事曆)
├── asia_holidays.html      (日本中國假期)
└── PROJECT_PROMPT.md       (本文件)
```

---

## 部署說明
所有頁面為純靜態 HTML/CSS/JavaScript，可直接部署至:
- GitHub Pages
- Netlify
- Vercel
- 任何靜態網站託管服務

無需後端或資料庫，所有資料硬編碼於 JavaScript 中。

---

## 瀏覽器相容性
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- 使用現代 CSS (backdrop-filter, grid, flexbox)
- JavaScript ES6+

---

## 未來擴充建議
1. 加入更多國家到旅遊時間表
2. 支援多語言 (英文/日文)
3. 整合天氣 API 顯示即時天氣
4. 提供 PDF 下載功能
5. 加入使用者評分與評論系統
6. 整合航班/飯店搜尋 API

---

**最後更新**: 2026-01-03
**版本**: 1.0
**作者**: AI Assistant
