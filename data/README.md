# 模擬資料

所有姓名與身分證字號都是虛構的測試值，只供課程雛型使用。

- `exams.json`：10 筆模擬檢查，內容與案例資料的「檢查清單」一致
- `phrases.json`：片語範例，僅供雛型使用，不是臨床標準用語

## 欄位說明（exams.json）

| 欄位 | 說明 |
| --- | --- |
| exam_no | 單號 |
| exam_at | 檢查日期時間 |
| category | 檢查類別，決定使用哪一種報告範本 |
| exam_name | 檢查名稱 |
| order_dept | 開單單位 |
| order_doctor | 開單醫師 |
| patient_name | 病人姓名（虛構） |
| patient_id | 身分證字號（虛構測試值） |
| sex | 性別 |
| age | 年齡 |
| order_status | 醫令狀態：正常／已DC |
| image_taken | 是否已照影像 |
| report_status | 報告狀態：未完成／已完成／已認證 |
| report_doctor | 報告醫師；null 表示尚未指派 |

## 在 Claude 對話中使用

Claude 對話中產生的雛型讀不到 repo 裡的檔案。請把 `exams.json` 的內容直接貼進對話，請AI寫進雛型程式中。
