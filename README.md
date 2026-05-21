# 🛡 quote-shield

> 報價單發送前，一鍵清理敏感資訊。純瀏覽器執行，資料不離開你的電腦。
>
> Clean sensitive data from quotes before sending. Runs entirely in your browser — files never leave your machine.

---

## 這是什麼？ / What is it?

業務在發報價單前，常常需要手動刪掉成本、利潤、內部備註等不該給客戶看到的資訊——這件事既耗時又容易出錯。

Sales teams often have to manually remove cost, margin, and internal notes from quotes before sending — tedious and error-prone.

**quote-shield** 讓你上傳報價檔案，選好要遮蔽的內容，預覽確認後直接下載乾淨版本，整個流程不超過一分鐘。

**quote-shield** lets you upload a quote file, choose what to redact, preview the result, and download a clean version — all in under a minute.

---

## 功能 / Features

### 格式支援 / File formats
- XLSX · XLS · PDF
- 欄位型（有標準欄位標題）與敘述型（無結構）報價單都能處理
- Handles both structured (named columns) and unstructured (free-text) quote layouts

### 自動遮蔽 / Auto-redaction
| 類型 / Type | 說明 / Description |
|---|---|
| 客戶名稱 / Client Name | 公司名、聯絡人 / Company, contact person |
| 報價金額 / Quote Amount | 單價、總價、折扣 / Unit price, total, discount |
| 成本 / 利潤 / Cost & Margin | 進價、毛利 / Purchase price, gross profit |
| 內部備註 / Internal Notes | 備註、說明欄 / Remarks, description fields |
| 供應商 / Supplier | 供應商名、料號 / Supplier name, part number |
| 業務員 / Sales Rep | 姓名、電話、Email |

### 其他功能 / More
- **四種發送對象預設** — 客戶 / 內部分享 / 合作夥伴 / 自訂
  **4 recipient presets** — Client / Internal / Partner / Custom
- **電話 / Email 自動偵測** — 台灣手機（09xx）、市話、Email 地址
  **Phone / Email auto-detection** — TW mobile, landline, email addresses
- **PDF 手動框選** — 在預覽圖上拖曳滑鼠，手動補塗 Logo、印章等圖片內容
  **PDF manual redact** — drag to paint black boxes over logos, stamps, images
- **OCR 圖片辨識** — 掃描型 PDF 也能自動偵測並遮蔽（Tesseract.js）
  **OCR support** — auto-detect text in scanned / image-based PDFs (Tesseract.js)
- **額外關鍵字** — 手動加入任意文字，全文搜尋遮蔽
  **Custom keywords** — add any text to redact across the whole file
- **三視角預覽** — 遮蔽後 / 原始 / 對照並排
  **3-view preview** — redacted / original / side-by-side compare
- **自訂存檔後綴** — 日期、時間、對象名稱、自訂文字
  **Filename suffix** — date, datetime, recipient name, or custom text
- **設定範本** — 儲存常用遮蔽規則，下次直接載入（localStorage）
  **Saved templates** — store redaction rules locally, reload anytime
- **密碼保護** — PDF AES 真實加密 / XLSX 工作表保護
  **Password protection** — PDF AES encryption / XLSX sheet protection
- **介面雙語** — 自動偵測瀏覽器語言（中文 / English），右上角可手動切換
  **Bilingual UI** — auto-detects browser language (ZH / EN), toggle in top-right

---

## 自動偵測的金額格式 / Detected amount formats

| 格式 / Format | 範例 / Example |
|---|---|
| 貨幣符號 + 數字 / Currency symbol + number | `$2,720,380` · `NT$48,000` · `¥980,000` |
| 千分位數字 / Comma-separated number | `1,234,567` |
| 純數字欄 / Numeric column | 欄位名含金額關鍵字時整欄遮蔽 / Entire column masked when header matches |

---

## 使用方式 / How to use

1. 開啟網頁，上傳報價檔案（`.xlsx` / `.xls` / `.pdf`）
   Open the page, upload your quote file (`.xlsx` / `.xls` / `.pdf`)
2. 選擇發送對象（決定預設遮蔽哪些欄位）
   Choose recipient preset (sets default redaction fields)
3. 細調遮蔽設定，加入額外關鍵字
   Fine-tune settings, add custom keywords
4. 設定存檔後綴與密碼（選填）
   Set filename suffix and password (optional)
5. 預覽確認 → 下載
   Preview & confirm → Download

---

## 隱私 / Privacy

所有處理都在你的瀏覽器本機完成，檔案不會上傳到任何伺服器。

All processing happens locally in your browser. Files are never uploaded anywhere.

- 無後端、無資料庫、無 Cookie、無追蹤 / No backend, no database, no cookies, no tracking
- 離線也能使用（首次開啟需載入函式庫）/ Works offline after first load
- 原始碼完全公開，歡迎自行審查 / Source code fully open, audit freely

---

## 開發路線圖 / Roadmap

| 狀態 / Status | 功能 / Feature |
|---|---|
| ✅ | XLSX / CSV 欄位遮蔽（欄位型 + 敘述型）/ XLSX / CSV field redaction |
| ✅ | 自訂存檔後綴 / Custom filename suffix |
| ✅ | PDF 黑塊遮蔽（文字層）/ PDF text-layer redaction |
| ✅ | PDF AES 加密 / XLSX 密碼保護 / PDF AES encryption & XLSX password |
| ✅ | 電話 / Email 自動偵測 / Phone & Email auto-detection |
| ✅ | 設定範本儲存與載入 / Template save & load |
| ✅ | PDF 手動框選塗黑 / PDF manual drag-to-redact |
| ✅ | OCR 圖片辨識 / OCR image recognition |
| ✅ | 雙語介面 / Bilingual UI |
| ⬜ | 批量處理 / Batch processing |
| ⬜ | DOCX 支援 / DOCX support |

---

## 技術棧 / Tech stack

純前端，單一 HTML 檔案，零框架，依賴三個開源函式庫（CDN 載入）。

Pure frontend, single HTML file, zero framework, three open-source libraries via CDN.

| 函式庫 / Library | 用途 / Purpose |
|---|---|
| [SheetJS](https://sheetjs.com) | XLSX 讀寫 / XLSX read & write |
| [PDF.js](https://mozilla.github.io/pdf.js/) | PDF 預覽與文字層分析 / PDF render & text extraction |
| [@cantoo/pdf-lib](https://github.com/cantoo-scribe/pdf-lib) | PDF 輸出與 AES 加密 / PDF output & AES encryption |
| [Tesseract.js](https://tesseract.projectnaptha.com/) | OCR 圖片文字辨識 / OCR text recognition |

---

## License

MIT
