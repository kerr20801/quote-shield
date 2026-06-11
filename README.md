# 🛡 quote-shield

報價單發送前，一鍵清理敏感資訊。純瀏覽器執行，資料不離開你的電腦。

Clean sensitive data from quotes before sending. Runs entirely in your browser — files never leave your machine.

---

## 這是什麼？/ What is it?

業務在發報價單前，常常需要手動刪掉成本、利潤、內部備註等不該給客戶看到的資訊——這件事既耗時又容易出錯。HR 文件往往頁數多、資料密，遮蔽到一半很容易漏掉。

Sales teams often have to manually remove cost, margin, and internal notes from quotes before sending — tedious and error-prone. HR documents are long and dense; partial redaction is a common risk.

quote-shield 讓你上傳報價或 HR 檔案，選好要遮蔽的內容，預覽確認後直接下載乾淨版本，整個流程不超過一分鐘。

quote-shield lets you upload a quote or HR file, choose what to redact, preview the result, and download a clean version — all in under a minute.

---

## 功能 / Features

### 格式支援 / File formats

`XLSX` · `XLS` · `PDF`（含掃描型 / including scanned）

欄位型（有標準欄位標題）與敘述型（無結構）報價單都能處理。PDF 支援完整頁數，不限頁數上限。

Handles both structured (named columns) and unstructured (free-text) layouts. PDF previews all pages with no page cap.

---

### 自動遮蔽 / Auto-redaction

| 類型 / Type | 說明 / Description |
|---|---|
| 客戶名稱 / Client Name | 公司名、聯絡人 / Company, contact person |
| 報價金額 / Quote Amount | 單價、總價、折扣 / Unit price, total, discount |
| 成本 / 利潤 / Cost & Margin | 進價、毛利 / Purchase price, gross profit |
| 內部備註 / Internal Notes | 備註、說明欄 / Remarks, description fields |
| 供應商 / Supplier | 供應商名、料號 / Supplier name, part number |
| 業務員 / Sales Rep | 姓名、電話、Email |

---

### 🧠 本地 ML 語意掃描 / Local ML Semantic Scan（新）

使用 **@xenova/transformers**（HuggingFace）在瀏覽器 WASM 中執行真正的 Transformer 模型，完全離線，資料不外傳。

Uses **@xenova/transformers** (HuggingFace) to run a real Transformer model in-browser via WASM — fully offline, zero data transfer.

- 模型：`paraphrase-multilingual-MiniLM-L12-v2`（支援繁中、簡中、英文、日文）
- Model: `paraphrase-multilingual-MiniLM-L12-v2` (supports ZH-TW, ZH-CN, EN, JA)
- 將欄位名稱與儲存格內容轉為語意向量，與各敏感類型做 cosine similarity 比對
- Converts column headers and cell values to semantic embeddings, compared against sensitive-type anchor vectors via cosine similarity
- 自動啟用建議類別，高風險值可一鍵加入關鍵字清單
- Auto-enables suggested categories; high-risk values can be added to the keyword list in one click
- 首次使用下載約 45MB 模型，之後快取在瀏覽器中，秒速啟動
- First use downloads ~45MB model; cached in browser thereafter for instant startup
- OCR 邊界信心值結果送進 ML 二次確認，減少誤判
- Borderline-confidence OCR words are re-verified by ML to reduce false positives

---

### 📋 強化正則引擎 / Enhanced Regex Engine（12+ 規則）

| 類型 | 範例格式 |
|---|---|
| 台灣手機 / 市話 | `0912-345-678` · `02-2345-6789` |
| 國際電話 | `+886-2-1234-5678` |
| Email | `name@company.com` |
| 台灣身分證 | `A123456789` |
| 統一編號 | `12345678`（8碼） |
| 護照號碼 | `AB1234567` |
| 信用卡號 | `1234-5678-9012-3456` |
| 銀行帳號 | 12–16 碼數字 |
| 台灣地址 | `台北市信義區信義路五段7號` |
| IP 位址 | `192.168.1.1` |
| URL | `https://...` |
| 多幣別金額 | `$` · `NT$` · `USD` · `CNY` · `JPY` · `EUR` · `GBP` · `HKD` · `¥` · `€` |

---

### 🔍 OCR 多語言辨識 / Multi-language OCR（升級）

- 繁中 / 簡中 / 英文 / 日文可自由勾選組合
- Traditional Chinese / Simplified Chinese / English / Japanese selectable
- 信心值門檻滑桿（0–90%）：過濾低品質辨識結果，減少誤遮
- Confidence threshold slider (0–90%): filters out low-quality OCR hits
- 邊界信心值結果由 ML 模型二次驗證
- Borderline results verified by ML model

---

### 🧠 NER 命名實體辨識 / Named Entity Recognition

使用 **compromise.js** 偵測英文人名、組織名、地點，自動加入遮蔽關鍵字清單。

Uses **compromise.js** to detect English person names, organizations, and places, automatically added to the redaction keyword list.

---

### 其他功能 / More

- **四種發送對象預設** — 客戶 / 內部分享 / 合作夥伴 / 自訂 · 4 recipient presets — Client / Internal / Partner / Custom
- **PDF 手動框選** — 在預覽圖上拖曳滑鼠，手動補塗 Logo、印章等 · PDF manual redact — drag to paint black boxes over logos, stamps
- **額外關鍵字** — 手動加入任意文字，全文搜尋遮蔽 · Custom keywords — add any text for full-document search & redact
- **三視角預覽** — 遮蔽後 / 原始 / 對照並排 · 3-view preview — redacted / original / side-by-side compare
- **自訂存檔後綴** — 日期、時間、對象名稱、自訂文字 · Filename suffix — date, datetime, recipient, or custom
- **設定範本** — 儲存常用遮蔽規則（localStorage）· Saved templates — store redaction rules locally
- **密碼保護** — PDF AES 真實加密 / XLSX 工作表保護 · Password protection — PDF AES encryption / XLSX sheet lock
- **介面雙語** — 自動偵測瀏覽器語言，右上角可手動切換 · Bilingual UI — auto-detects browser language (ZH / EN)

---

## 使用方式 / How to use

1. 開啟網頁，上傳報價或 HR 檔案（`.xlsx` / `.xls` / `.pdf`）
   Open the page, upload your file
2. 選擇發送對象（決定預設遮蔽哪些欄位）
   Choose recipient preset
3. 細調遮蔽設定，加入額外關鍵字；需要時按「🧠 ML 掃描」讓模型自動分析
   Fine-tune settings; click **ML Scan** to let the model analyze automatically
4. 設定存檔後綴與密碼（選填）
   Set filename suffix and password (optional)
5. 預覽確認 → 下載
   Preview & confirm → Download

---

## 隱私 / Privacy

所有處理都在你的瀏覽器本機完成，檔案不會上傳到任何伺服器。ML 模型也是下載到本機後在本機執行。

All processing — including ML inference — happens locally in your browser. Files and model outputs are never uploaded anywhere.

- 無後端、無資料庫、無 Cookie、無追蹤 / No backend, no database, no cookies, no tracking
- 離線也能使用（首次開啟需載入函式庫與模型）/ Works offline after first load
- 原始碼完全公開，歡迎自行審查 / Source code fully open, audit freely

---

## 開發路線圖 / Roadmap

| 狀態 | 功能 / Feature |
|---|---|
| ✅ | XLSX / CSV 欄位遮蔽 / Field redaction |
| ✅ | PDF 黑塊遮蔽（文字層）/ PDF text-layer redaction |
| ✅ | PDF AES 加密 / XLSX 密碼保護 / Encryption |
| ✅ | 電話 / Email 自動偵測 / Phone & Email detection |
| ✅ | 身分證 / 統編 / 護照 / 銀行帳號 / 信用卡 / 地址偵測 |
| ✅ | PDF 手動框選塗黑 / PDF manual drag-to-redact |
| ✅ | OCR 多語言（繁中 / 簡中 / 英 / 日）+ 信心值門檻 |
| ✅ | 🧠 本地 ML 語意掃描（Transformer，完全離線）|
| ✅ | NER 命名實體辨識（人名 / 組織 / 地點）|
| ✅ | OCR × ML 雙層驗證 / OCR + ML dual-layer verification |
| ✅ | 設定範本儲存與載入 / Template save & load |
| ✅ | 雙語介面 / Bilingual UI |
| ✅ | PDF 完整頁數預覽（移除頁數上限）|
| ⬜ | 批量處理 / Batch processing |
| ⬜ | DOCX 支援 / DOCX support |

---

## 技術棧 / Tech stack

純前端，單一 HTML 檔案，零框架。

Pure frontend, single HTML file, zero framework.

| 函式庫 / Library | 用途 / Purpose |
|---|---|
| SheetJS | XLSX 讀寫 / XLSX read & write |
| PDF.js | PDF 預覽與文字層分析 / PDF render & text extraction |
| @cantoo/pdf-lib | PDF 輸出與 AES 加密 / PDF output & AES encryption |
| Tesseract.js | OCR 圖片文字辨識 / OCR text recognition |
| @xenova/transformers | 瀏覽器端 Transformer 語意模型 / In-browser Transformer ML |
| compromise.js | 英文 NER 命名實體辨識 / English NER |

---

## License

MIT
