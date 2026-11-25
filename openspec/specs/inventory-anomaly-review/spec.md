# 庫存異常判定

## Purpose

定義原型如何對照本機測試庫的單據歷史和庫存，形成供人工覆核的異常判定。

## Requirements

### Requirement: 偵測精確重複單號

原型 SHALL 使用擷取出的單號查詢歷史。當歷史中有相同單號時，原型 SHALL 標記重複，且測試資料庫 SHALL 阻擋寫入相同單號。

#### Scenario: 重複提交已確認的單據

- **WHEN** 再次分析一張已確認寫入的單據
- **THEN** 原型回傳 `DUPLICATE_DOCUMENT`，而測試庫會拒絕相同單號的第二次寫入

### Requirement: 檢查出貨量是否超過可用庫存

原型 SHALL 依倉別及 SKU 找出對應庫存列，以現有量減去保留量計算可用量，並對超量的出貨品項標記庫存不足。

#### Scenario: 申請出貨量大於可用量

- **WHEN** 單據申請出貨 95 件，對應庫存有 100 件且已保留 10 件
- **THEN** 原型標記 `INSUFFICIENT_STOCK` 並要求人工覆核

### Requirement: 要求補正必要欄位

單號、日期、倉別或品項明細缺漏時，原型 SHALL 要求使用者補正單據。

#### Scenario: 單據只有棧板類型

- **WHEN** 輸入只提供棧板類型
- **THEN** 原型回傳 `REQUEST_CORRECTION`
