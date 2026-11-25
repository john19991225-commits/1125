# 單據輸入與欄位擷取

## Purpose

定義倉儲原型如何從電子單據取得文字、結構化欄位與來源證據。

## Requirements

### Requirement: 支援電子單據與合成測試資料

原型 SHALL 支援從有文字層的 PDF 擷取文字，並在已安裝及設定 Tesseract 時辨識圖片。原型 SHALL 提供可讀取 UTF-8 合成文字的測試模式。

#### Scenario: 處理有效的合成單據

- **WHEN** 原型以合成模式分析含單號、倉別與品項的測試單據
- **THEN** 原型回傳結構化欄位，並在可配對的文字行保留來源識別碼

### Requirement: 回報無法處理的輸入

當上傳內容為空或文字擷取失敗時，原型 SHALL 回報失敗並標示需要人工注意。

#### Scenario: 上傳空檔

- **WHEN** 上傳內容為空
- **THEN** 原型回傳 `FAILED` 與 `EMPTY_FILE`，並標示需要人工注意
