# AGENTS.md — 道路交通管理處罰條例・實務情境案例庫專案指引

> 本文件（`AGENTS.md`）為本專案之最高開發規範。
> 動手建立或修改任何檔案前，必須先完整閱讀本文件與 `NOTES.md`。
> 每次任務結束前，必須同步更新 `NOTES.md` 的進度與待辦清單。

## 一、專案目標與技術架構
本專案為《道路交通管理處罰條例》實務情境查詢網站，旨在將生硬法條轉化為「條文原文＋構成要件＋互動式路況判定案例」的結構化自學網頁。

- **技術規格**：純靜態網頁（HTML5 + Tailwind CSS CDN + 原生 JavaScript），無需任何建置工具（Zero-build），可直接在瀏覽器與 GitHub Pages 運行。
- **語系規範**：繁體中文，內文一律使用**全形標點符號**（，。、：「」！？）。
- **目錄結構（URL 路徑一律英文小寫與連字號）**：
  ```text
  traffic-law-wiki/
  ├── AGENTS.md                  # 本專案規範文件
  ├── NOTES.md                   # 目前進度白板與待辦清單
  ├── README.md                  # GitHub 專案說明
  ├── .nojekyll                  # 停用 Jekyll 編譯（GitHub Pages 必備）
  ├── index.html                 # 網站首頁（條文索引卡片網格）
  ├── notes/                     # 內容先行區：各條文之定稿文字稿（.md）
  │   └── art-{條號}.md          # 例如：art-55.md、art-44.md
  └── articles/                  # 網頁成品區：每條法規獨立資料夾（Self-Contained）
      └── art-{條號}/            # 例如：art-55/、art-44/
          └── index.html         # 該條文之獨立互動網頁
  ```

---

## 二、視覺設計系統與 UI 隔離規範（Design System & UI Isolation）
全站所有頁面（首頁 `index.html` 與各條文獨立內頁 `articles/art-{條號}/index.html`）必須嚴格鎖定以下交通號誌風格之視覺設計規範與 UI 隔離鐵則，確保未來交由任何 AI 模型擴充新條文時，視覺風格與架構皆完全一致：

1. **字體與框架**：
   - 純靜態 HTML5 + Tailwind CSS CDN + Google Fonts `Noto Sans TC`（字重 400、500、600、700、800，設定於 `tailwind.config` 之 `fontFamily.sans`）。
2. **色彩變數（嚴禁更改）**：
   - **網頁整體底色**：`bg-slate-50`（淺灰白）、**內文主色**：`text-slate-800`。
   - **頂部導覽列、頁尾與條號徽章**：`bg-slate-900`（深岩灰底）、**強調文字與主圖示**：`amber-400`（琥珀警戒黃，如 `text-amber-400`、`bg-amber-400`）。
   - **資訊卡片外觀**：`bg-white rounded-2xl border border-slate-200 shadow-sm`（白底圓角卡片）。
   - **狀態與判定標籤**：
     - **已收錄／合法免罰**：採用 `emerald` 綠系（`bg-emerald-50 text-emerald-700 border-emerald-200`；展開面板結果徽章搭配 `bg-emerald-600 text-white`）。
     - **違規舉發／罰鍰警示**：採用 `rose` 紅系（`bg-rose-50 text-rose-700 border-rose-200`；展開面板結果徽章搭配 `bg-rose-600 text-white`）。
     - **待擴充預告**：採用 `amber` 黃系（`bg-amber-50 text-amber-800 border-amber-200`）。
3. **法條原文卡片視覺層級與字級規範（嚴禁違反）**：
   - **卡片標題列與內文區塊嚴格區分**：深岩灰背景 `bg-slate-900` 僅限用於「法條原文卡片之頂部標題列（Header）」，**嚴禁在卡片內部的任何條文【第X項】區塊使用 `bg-slate-900` 深色背景**，以免造成標題列與內文層級混淆。
   - **條文各【項】淺色系左邊框樣式**：
     - 一般條文項次：`bg-slate-50 border-l-4 border-slate-800 text-slate-800`
     - 一般違規罰則項次：`bg-rose-50 border-l-4 border-rose-600 text-rose-950`
     - 特定對象加重罰則項次：`bg-amber-50 border-l-4 border-amber-500 text-amber-950`
     - 肇事致傷亡等最高級距加重處罰項次：`bg-rose-100 border-l-4 border-rose-700 text-rose-950`
     - 豁免但書項次：`bg-emerald-50 border-l-4 border-emerald-600 text-emerald-950`
   - **統一內文字級與字重標準**：條文各【第X項】內文統一使用標準閱讀字級 `text-base` 與一般字重（`font-normal`），**僅有項次標題（如 `【第一項】`、`【第二項（未停讓一般行人）】`）可使用粗體（`font-bold`）**，禁止將整段條文內文全部加粗。
   - **統一卡片右上角外部連結文字**：所有條文內頁之法條原文卡片右上角外部法規連結文字，一律統一為「`查看完整法條原文 ↗`」。
4. **外部法規超連結來源與格式規範（100% 統一，嚴禁混用其他網站）**：
   - 全站所有 HTML 檔案（`index.html` 與各 `articles/art-{條號}/index.html`）之所有外部超連結，法源網域必須 **100% 統一為「法務部全國法規資料庫（`law.moj.gov.tw`）」**，嚴禁連結至其他第三方網站、部落格或地方政府鏡像系統：
     - 《道路交通管理處罰條例》單一條文（如第 3、7-1、44、55、56 條）：一律使用 `https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno={條號}`
     - 《道路交通管理處罰條例》全文總覽：一律使用 `https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040012`
     - 《道路交通安全規則》全文總覽：一律使用 `https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040013`
     - 《違反道路交通管理事件統一裁罰基準及處理細則》：一律使用 `https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=D0080029`
   - 所有外部連結之 `<a>` 標籤皆須統一加上 `target="_blank" rel="noopener noreferrer"`。
5. **UI 隔離鐵則（嚴格執行）**：
   - 網頁前端畫面僅呈現給一般民眾閱讀的法規與案例資訊，**嚴禁在 UI 畫面上直接印出 `AGENTS.md`、`NOTES.md`、檔案路徑（如 `notes/art-*.md`、`articles/art-*/index.html`）或 HTML 註解標籤（如 `<!-- INSERT_NEW_CARD_HERE -->`）等內部開發指令**。
   - 內部擴充定位標記（如 `<!-- INSERT_NEW_CARD_HERE -->`）僅能存在於 HTML 原始碼註解中，絕不可渲染於使用者可見畫面上。
6. **內頁版型結構一致性**：
   - 每篇條文內頁（`articles/art-{條號}/index.html`）頂部導覽列之返回首頁連結，必須統一指向 `../../index.html`。
   - 內頁主體統一包含四大區塊（搭配 `bg-slate-900 text-amber-400` 之 `壹`、`貳`、`參`、`肆` 區塊徽章）：
     - **壹、法條原文與法定用詞定義**
     - **貳、三大構成要件深度解析**（三欄網格 `grid-cols-1 md:grid-cols-3`）
     - **參、互動式實務路況判定案例**（共 3 則，提供原生 JS 單筆展開／收合 `toggleCase` 與全部展開／收合 `toggleAllCases` 功能）
     - **肆、實務延伸對照表**

---

## 三、內容先行原則（Content-First Principle）
為避免直接在 HTML 標籤中編寫法條造成內容疏漏或法理錯誤，本專案嚴格執行「**內容先行原則**」：

1. **禁止跳過文字稿直接寫網頁**：新增或修改任何法條時，**絕對禁止**直接撰寫 `articles/art-{條號}/index.html`。必須先在 `notes/art-{條號}.md` 完成結構化 Markdown 定稿。
2. **文字稿必備結構**：每篇 `notes/art-{條號}.md` 必須完整包含：
   - **法規來源與條文定位**：附上法務部全國法規資料庫（`law.moj.gov.tw`）連結。
   - **一、法條原文**：逐項、逐款完整收錄該條文全文，並附上關聯定義或執行條文（如《道路交通安全規則》對應條文）。
   - **二、三大構成要件解析**：拆解實務執法與行政救濟之三大核心判定要件，並說明民眾檢舉規定（第 7-1 條）或裁罰基準。
   - **三、實務路況判定案例（3 則）**：每則案例皆須包含「路況情境描述」、「判定結果（違規舉發／合法免罰）」與「法理依據與實務解析」。

---

## 四、四步驟擴充標準作業程序（4-Step Expansion SOP）
當需要為網站新增一條法規時，必須嚴格依序執行以下四個步驟，不得跳步或遺漏：

1. **步驟一：撰寫內容先行文字稿（`notes/art-{條號}.md`）**
   - 檢索最新法條原文與實務見解，依「內容先行原則」建立 `notes/art-{條號}.md`，確保法條文字、罰鍰金額、構成要件與 3 則實務路況案例完整無誤，且全面使用繁體中文與全形標點符號。
2. **步驟二：生成獨立互動網頁（`articles/art-{條號}/index.html`）**
   - 嚴格依據 `notes/art-{條號}.md` 的定稿內容，套用「視覺設計系統與 UI 隔離規範」（`bg-slate-50`、`text-slate-800`、`bg-slate-900`、`amber-400`），建立 `articles/art-{條號}/index.html`。
   - 確認頂部返回首頁連結指向 `../../index.html`，法條原文卡片右上角連結統一為「`查看完整法條原文 ↗`」，所有外部法規連結 100% 採用 `law.moj.gov.tw` 並加上 `target="_blank" rel="noopener noreferrer"`，各【項】區塊均採用淺色背景且內文為 `text-base` 一般字重（僅標題加粗），實作原生 JavaScript 互動函式（`toggleCase` 與 `toggleAllCases`），且畫面上絕不外露任何內部開發指令或檔案路徑。
3. **步驟三：掛載首頁索引卡片（更新 `index.html`）**
   - 開啟根目錄 `index.html`，在原始碼中之 `<!-- INSERT_NEW_CARD_HERE -->` 註解標記**正上方**插入新條文的索引卡片（保留 `<!-- INSERT_NEW_CARD_HERE -->` 註解標記與最後一張面向一般民眾之虛線預留卡）。
   - 同步更新首頁橫幅之「已收錄條文」與「待擴充項目」狀態徽章，並確保首頁畫面上無任何開發者指令字眼。
4. **步驟四：更新專案進度白板（更新 `NOTES.md` 與 `README.md`）**
   - 於 `NOTES.md` 將該條文自「待擴充項目」移入「目前已收錄條文」，詳細記錄收錄重點，並規劃下一階段待擴充條文（同步更新 `README.md` 之收錄清單表格）。
