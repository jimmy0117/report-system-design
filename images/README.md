# 影像示意圖

課程中不連接 PACS，打報告畫面的影像區以這些示意圖代替。

| 檢查類別 | 檢查名稱 | 示意圖 |
| --- | --- | --- |
| 健檢胸部X光 | 胸部X光數位攝影 | `chest-xray.svg` |
| 門診放射 | 胸部X光（正面） | `chest-xray.svg` |
| 門診放射 | 腹部X光 | `abdomen-xray.svg` |
| 健檢乳攝 | 2D+3D乳房攝影 | `mammography.svg` |
| 心臟超音波 | 心臟超音波 | `echocardiography.svg` |
| 頸動脈超音波 | 頸動脈超音波 | `carotid-ultrasound.svg` |

在雛型中引用時，路徑寫成 `images/chest-xray.svg`，大小寫要一致。尚未照影像的檢查（`image_taken` 為 false）不顯示示意圖，請設計「尚無影像」時的畫面。
