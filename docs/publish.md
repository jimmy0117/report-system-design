# 發布到 GitHub Pages

## 第一次發布

1. 確認 repo 為公開
2. 把雛型的 HTML 檔案命名為 `index.html`，透過「Add file → Upload files」上傳到 repo 根目錄，覆蓋範本的預設頁面
3. 進入 repo 的「Settings → Pages」，Source 選「Deploy from a branch」，分支選 `main`，資料夾選 `/ (root)`，按 Save
4. 等待數分鐘，Pages 設定頁上方會出現網址
5. 打開網址確認雛型可以正常操作，再把網址貼到課程共用頻道

之後每次上傳新版本，網站都會自動更新。可以在 repo 的 Actions 分頁看到發布進度。

## 常見問題

| 症狀 | 可能原因 | 解法 |
| --- | --- | --- |
| 網址顯示 404 | 發布尚未完成、首頁檔名不是 index.html | 等幾分鐘，檢查檔名與 Pages 設定 |
| 網頁還是舊版本 | 瀏覽器快取，或發布尚未完成 | 強制重新整理（Windows 按 Ctrl+Shift+R，Mac 按 Cmd+Shift+R），到 Actions 分頁查看發布狀態 |
| 雛型在 Claude 中正常，上傳後一片空白 | 雛型是 React 元件，或引用了無法在一般網頁載入的資源 | 請AI改寫成單一、可獨立執行的 HTML 檔案 |
| 影像示意圖沒有顯示 | 圖片路徑錯誤，或圖片沒有一起上傳 | 確認路徑寫成 `images/檔名`，大小寫一致 |
| 中文變成亂碼 | 檔案沒有指定編碼 | 請AI在 HTML 的 head 加上 `<meta charset="utf-8">` |
