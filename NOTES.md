# NOTES.md — 專案進度白板與待辦清單

> 本文件記錄《道路交通管理處罰條例・實務情境案例庫》之目前開發進度、已收錄條文狀態與後續擴充待辦事項。
> 依據 `AGENTS.md` 規範，每次任務開始前須先檢視本文件，並於任務完成前同步更新本文件。

---

## 一、專案整體狀態

- **專案名稱**：道路交通管理處罰條例・實務情境案例庫（`traffic-law-wiki`）
- **目前狀態**：已完成全站外部法規超連結 100% 統一（法源網域全面鎖定 `law.moj.gov.tw` 並加上 `target="_blank" rel="noopener noreferrer"`），同步更新 `AGENTS.md`、第 55 條與第 44 條頁面並完成專案打包。
- **最後更新日期**：2026-11-16
- **架構與規範檢核**：
  - [x] 建立並強化專案最高規範文件 `AGENTS.md`（含色票規範、「法條原文卡片層級與字級規範」、「外部法規超連結來源與格式規範」、「UI 隔離鐵則」、「內容先行原則」與「四步驟擴充 SOP」）
  - [x] 建立 GitHub Pages 必備之 `.nojekyll` 空檔案與 `README.md`
  - [x] 完成第 55 條：`notes/art-55.md` ＋ `articles/art-55/index.html` ＋ 首頁卡片
  - [x] 完成第 44 條：`notes/art-44.md` ＋ `articles/art-44/index.html` ＋ 首頁卡片（插入於 `<!-- INSERT_NEW_CARD_HERE -->` 上方）
  - [x] 完成全站外部法規超連結掃描與統一：`index.html`、`articles/art-55/index.html`、`articles/art-44/index.html` 所有外部連結均已 100% 統一為 `law.moj.gov.tw`（單條採用 `LawSingle.aspx?pcode=K0040012&flno={條號}`，全文與細則採用 `LawAll.aspx`），且全部具備 `target="_blank" rel="noopener noreferrer"`。

---

## 二、目前已收錄條文

### 1. [《道路交通管理處罰條例》第 55 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=55)（違規臨時停車之處罰與豁免要件）
- **收錄狀態**：已完成（文字稿與互動網頁均已上線，通過 UI 隔離、法條層級、色票及全國法規資料庫連結統一檢核）
- **對應檔案**：
  - 內容文字稿：`notes/art-55.md`
  - 互動式網頁：`articles/art-55/index.html`
- **收錄重點**：
  - 完整收錄[第 55 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=55)第一項五款禁止臨時停車處所與方式（處新臺幣三百元以上六百元以下罰鍰），以及第二項接送未滿七歲兒童或行動不便者上、下車不受三分鐘限制之豁免但書。
  - 結合[第 3 條第 10 款](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=3)與[第 7-1 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=7-1)，拆解三大構成要件與 3 則實務路況判定案例。

### 2. [《道路交通管理處罰條例》第 44 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=44)（行近行人穿越道之減速慢行與停讓行人義務）
- **收錄狀態**：已完成（依 `AGENTS.md` 四步驟擴充 SOP 建置完畢，通過 UI 隔離、法條層級、色票及全國法規資料庫連結統一檢核）
- **對應檔案**：
  - 內容文字稿：`notes/art-44.md`
  - 互動式網頁：`articles/art-44/index.html`
- **收錄重點**：
  - 完整收錄[第 44 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=44)第一項七款減速慢行義務、第二項未暫停讓一般行人先行通過、第三項未暫停讓攜帶白手杖或導盲犬之視覺功能障礙者，以及第四項因而肇事致人受傷或重傷死亡之加重處罰規定。
  - 結合[《道路交通安全規則》](https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=K0040013)第 103 條與第 134 條第 2 款，拆解三大構成要件與 3 則實務路況判定案例。

---

## 三、待擴充項目（Backlog & To-Do List）

- [ ] **擴充[《道路交通管理處罰條例》第 56 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=56)（違規停車與併排停車之處罰及移置保管）**
  - **預定步驟 1**：撰寫 `notes/art-56.md`（收錄第 56 條第一項十款違規停車態樣、第二項併排停車處新臺幣 2,400 元罰鍰、三大構成要件與 3 則實務案例）。
  - **預定步驟 2**：依視覺設計系統、外部連結規範與 UI 隔離鐵則生成 `articles/art-56/index.html`。
  - **預定步驟 3**：於 `index.html` 之 `<!-- INSERT_NEW_CARD_HERE -->` 上方插入第 56 條索引卡片。
  - **預定步驟 4**：同步更新 `NOTES.md` 與 `README.md`。
- [ ] **擴充[《道路交通管理處罰條例》第 48 條](https://law.moj.gov.tw/LawClass/LawSingle.aspx?pcode=K0040012&flno=48)（轉彎或變換車道不依標誌、標線、號誌指示）**
