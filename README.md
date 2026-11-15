# 道路交通管理處罰條例・實務情境案例庫（Traffic Law Wiki）

本專案為[《道路交通管理處罰條例》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040012)實務情境自學查詢網站，旨在將生硬的交通法規條文轉化為「**條文原文＋構成要件＋互動式路況判定案例**」的結構化互動網頁，協助駕駛人與用路人透過真實道路情境快速釐清違規構成要件與合法免罰界線。

---

## 一、專案目的與核心特色

1. **法條結構化拆解**：完整對照法務部全國法規資料庫之[《道路交通管理處罰條例》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040012)、[《道路交通安全規則》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040013)與[《違反道路交通管理事件統一裁罰基準及處理細則》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=D0080029)，將條文拆解為直觀的構成要件與裁罰基準。
2. **內容先行原則與四步驟擴充 SOP**：所有條文均嚴格遵循 `AGENTS.md` 規範，先於 `notes/` 目錄撰寫結構化 Markdown 定稿（包含法條原文、三大構成要件與 3 則實務案例），再轉化為 `articles/` 下之獨立互動網頁（Self-Contained HTML），最後掛載至首頁並更新 `NOTES.md`。
3. **統一視覺設計系統**：全站鎖定深岩灰（`slate-900`）、琥珀黃（`amber-400`）與淺灰底（`slate-50`）之 Tailwind CSS 視覺識別，搭配玫瑰紅（違規舉發）與翡翠綠（合法免罰）語意化判定狀態色。
4. **零建置成本（Zero-Build）**：採用純靜態 HTML5、Tailwind CSS CDN 與原生 JavaScript（Vanilla JS）開發，無須安裝任何編譯工具即可直接於瀏覽器或 GitHub Pages 運行。

---

## 二、目錄結構

本專案嚴格遵守 `AGENTS.md` 規範，所有路徑均採用英文小寫與連字號（kebab-case）：

```text
traffic-law-wiki/
├── AGENTS.md                  # 專案最高開發規範文件（含視覺設計系統與四步驟擴充 SOP）
├── NOTES.md                   # 目前進度白板與待辦清單
├── README.md                  # GitHub 專案說明文件
├── .nojekyll                  # 停用 Jekyll 編譯（GitHub Pages 必備）
├── index.html                 # 網站首頁（條文索引卡片網格）
├── notes/                     # 內容先行區：各條文之定稿文字稿（.md）
│   ├── art-55.md              # 第 55 條（違規臨時停車）定稿文字稿
│   └── art-44.md              # 第 44 條（行近行人穿越道減速與停讓義務）定稿文字稿
└── articles/                  # 網頁成品區：每條法規獨立資料夾（Self-Contained）
    ├── art-55/                # 第 55 條獨立網頁資料夾
    │   └── index.html         # 第 55 條互動式路況判定網頁
    └── art-44/                # 第 44 條獨立網頁資料夾
        └── index.html         # 第 44 條互動式路況判定網頁
```

---

## 三、已收錄與待擴充條文清單

| 條號 | 條文主題 | 文字稿路徑 | 互動網頁路徑 | 狀態 |
| :--- | :--- | :--- | :--- | :--- |
| [第 55 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=55) | 違規臨時停車之處罰與豁免要件 | `notes/art-55.md` | `articles/art-55/index.html` | 已完成 |
| [第 44 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=44) | 行近行人穿越道之減速慢行與停讓行人義務 | `notes/art-44.md` | `articles/art-44/index.html` | 已完成 |
| [第 56 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=56) | 違規停車與併排停車之處罰及移置保管 | `notes/art-56.md` | `articles/art-56/index.html` | 待擴充 |

---

## 四、本地端與 GitHub Pages 瀏覽方式

### 1. 本地端直接瀏覽
由於本專案採用 Zero-build 純靜態架構，無須安裝 Node.js 或任何打包工具：
- 直接以瀏覽器開啟根目錄下的 `index.html` 即可瀏覽首頁，並點擊卡片進入各條文互動頁面（例如 `articles/art-55/index.html` 或 `articles/art-44/index.html`）。
- 或使用 VS Code Live Server、Python 內建伺服器啟動本地預覽：
  ```bash
  python3 -m http.server 8000
  ```
  接著於瀏覽器開啟 `http://localhost:8000` 即可。

### 2. GitHub Pages 部署與瀏覽
1. 將本專案完整推送至 GitHub 儲存庫（例如 `traffic-law-wiki`）。
2. 專案根目錄已內建 `.nojekyll` 空檔案，可確保 GitHub Pages 不會啟動 Jekyll 編譯，直接發布所有靜態資源。
3. 前往 GitHub 儲存庫的 **Settings** ＞ **Pages**，於 **Build and deployment** 選擇 **Deploy from a branch**，分支選擇 `main`（或 `master`）及 `/ (root)` 目錄並儲存。
4. 部署完成後，即可透過 `https://<您的GitHub帳號>.github.io/traffic-law-wiki/` 線上瀏覽首頁，或透過 `https://<您的GitHub帳號>.github.io/traffic-law-wiki/articles/art-44/` 直接存取單一條文頁面。

---

## 五、法規資料來源
- 法務部全國法規資料庫：[《道路交通管理處罰條例》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040012)
- 法務部全國法規資料庫：[《違反道路交通管理事件統一裁罰基準及處理細則》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=D0080029)
- 法務部全國法規資料庫：[《道路交通安全規則》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040013)
