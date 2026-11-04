---
name: report-design-system
description: 影像報告撰寫系統的設計系統。產生或修改報告系統的畫面、雛型或元件（工作清單、打報告畫面、放射師介面）時使用，確保顏色、字級、狀態標籤與按鈕一致。
---

# 影像報告撰寫系統設計系統

產生或修改畫面時，依照以下規則。數值一律來自文件最後的「tokens.css」區塊：請把整段 CSS 放進產生頁面的 `<style>`（或存成 `tokens.css` 以 `<link>` 引用）。這份檔案可以單獨使用，不需要其他檔案。

## 必須遵守

- 顏色、字級、間距、圓角一律使用 `tokens.css` 中的變數，不自行加入新顏色或新數值
- 報告狀態一律用狀態標籤呈現：顏色加上圖示與文字，不只靠顏色
- 每個畫面只有一個主要按鈕（主色實心）：打報告畫面是「儲存」，清單中待打的列是「打報告」
- 打報告畫面的操作列固定在底部，順序為：上一筆、下一筆｜（右側）儲存、認證
- 儲存或認證後自動跳到下一筆未完成的報告；沒有下一筆時回到工作清單
- 停用的按鈕要在畫面上說明原因（例如橫幅「尚未指派報告醫師」）
- 所有可操作元件都要有 3px `--color-focus` 的鍵盤焦點外框
- 不使用瀏覽器的 alert／confirm 對話框；需要確認的動作改用畫面上的確認區

## 視覺風格：霧面玻璃

- `body` 背景用 `var(--page-gradient), var(--color-surface)`
- 卡片與面板：`--glass-bg`、1px `--glass-border`、`--radius-lg`、`--shadow-soft`、`backdrop-filter: blur(var(--glass-blur))`
- 文字多的區塊（表格、報告表單、頂欄、底部操作列）改用 `--glass-bg-strong`
- 主要按鈕用 `--gradient-primary` 與 `--shadow-button`；篩選膠囊為全圓角，選取時用漸層
- 面板標題用 `--font-size-xs`、`--letter-spacing-label`、`--color-text-muted`，前面加主色的 ✦
- 風格只改外觀：狀態色、焦點外框、錯誤色不可為了風格調淡

## 手機版（700px 以下）

- 工作清單表格改成卡片：每筆一張卡，兩欄「欄位名稱＋值」，報告狀態與操作按鈕佔滿整列，保留狀態淡底色與左側色條
- 打報告畫面單欄；底部操作列兩排、按鈕平分寬度
- 控制項最小高度 44px（`--control-height` 已在 tokens.css 中處理）

## 報告狀態

主要狀態（每筆只有一個，放在同一個標籤位置）：

| 狀態 | 變數 | 標示 |
| --- | --- | --- |
| 等待影像 | `--status-waiting` | `⧗ 等待影像`，虛線外框、白底 |
| 待指派 | `--status-waiting` | `⇢ 待指派`，虛線外框、白底 |
| 未完成 | `--status-pending` | `○ 未完成`，淡底 |
| 已完成 | `--status-done` | `◐ 已完成`，淡底 |
| 已認證 | `--status-certified` | `✔ 已認證`，淡底 |

修飾標籤（與主要狀態並排，不取代主要狀態）：

| 標籤 | 變數 | 標示 |
| --- | --- | --- |
| 醫令已 DC | `--status-dc` | `⊘ 醫令已DC`，清單整列灰底、單號刪除線；不計入未完成數量 |
| 取消認證・待重打 | `--status-recall` | `↺ 取消認證・待重打` |
| 已逾時 | `--deadline-overdue` / `--deadline-overdue-bg` | `⏰ 已逾時`，紅底白字 |
| 即將到期 | `--deadline-soon` | `⏳ 剩 N 小時`，12 小時內到期才顯示 |

清單列：依主要狀態套用淡底色與左側 4px 色條；「等待影像／待指派」用白底與虛線色條。

## 元件

### 按鈕
- 主要：`--color-primary` 實心、白字。每個畫面最重要的一個動作
- 次要：白底、主色框線與文字（例如「認證」）。一般輔助動作用白底灰框
- 危險：白底、`--color-danger` 框線與文字（例如「取消認證」）
- 最小高度 `--control-height`（36px），表格內小按鈕 28px

### 表格列
- 一般：依狀態的淡底色＋左側色條
- 滑過：底色 `#dde8f5`，游標變手指
- 選取（鍵盤焦點）：3px `--color-focus` 外框，按 Enter 開啟
- 整列可點擊，同時保留最右欄的明確按鈕

### 狀態標籤
圓角膠囊：`圖示＋文字`，文字色與框線色相同，底色為對應淡底色；圖示標 `aria-hidden`，文字一定存在。

### 表單欄位
- 一般：白底、`--color-border` 框線；標籤旁註明「必填／選填」
- 聚焦：框線與 3px 外框改為 `--color-focus`
- 錯誤：框線改 `--color-danger`、底色 `--color-danger-bg`，欄位下方說明原因與解決方法
- 片語按鈕放在欄位正下方，標示「片語帶入：」，按下後附加到欄位結尾

### 橫幅
畫面上方的說明區，顏色跟著它說明的狀態（DC 灰、等待影像橘、取消認證紫、逾時紅），一律有圖示與文字。

## 需要新增狀態或元件時

先說明要新增什麼、為什麼，等我確認後再加入設計系統（`design-system.md` 的變更紀錄與 `tokens.css`），不要直接在畫面上加新的樣式。

## tokens.css

以下是設計系統的全部變數，與 repo 根目錄的 `tokens.css` 相同。修改設計系統時，兩邊要一起更新。

```css
/* 影像報告撰寫系統 — 迷你設計系統
   每個變數的用途與使用規則見 design-system.md。
   修改或新增變數時，先更新 design-system.md 的「變更紀錄」，再改畫面。
   v3（2026-11-04）：視覺風格改為「霧面玻璃」（參考使用者提供的 Pinterest 範例），
   報告狀態色維持原本的數值，確保在淡色底上的對比度。 */

:root {
  /* 色彩：基本 */
  --color-primary: #3f5fe0;          /* 冰藍紫，白底對比 5.3:1 */
  --color-primary-hover: #3350c8;
  --color-primary-2: #6366e8;        /* 漸層終點，白字對比 4.6:1 */
  --gradient-primary: linear-gradient(135deg, var(--color-primary) 0%, var(--color-primary-2) 100%);
  --color-on-primary: #ffffff;
  --color-bg: #ffffff;               /* 輸入框、實心底 */
  --color-surface: #eef3fb;          /* 頁面底色（漸層的基底）、表頭 */
  --color-text: #1e2a44;
  --color-text-muted: #56627c;
  --color-border: #d3ddef;
  --color-focus: #2b50d6;
  --color-danger: #b42318;
  --color-danger-bg: #fdecea;

  /* 霧面玻璃 */
  --page-gradient: radial-gradient(1200px 600px at 85% -10%, #dfe6fb 0%, transparent 60%),
                   radial-gradient(900px 500px at -10% 30%, #e6eefb 0%, transparent 60%),
                   linear-gradient(180deg, #f3f6fc 0%, #e8eef9 100%);
  --glass-bg: rgba(255, 255, 255, 0.62);
  --glass-bg-strong: rgba(255, 255, 255, 0.82);  /* 文字較多的區塊（表格、表單） */
  --glass-border: rgba(255, 255, 255, 0.9);
  --glass-blur: 14px;
  --shadow-soft: 0 8px 28px rgba(63, 95, 224, 0.10), 0 1px 2px rgba(30, 42, 68, 0.06);
  --shadow-button: 0 6px 16px rgba(63, 95, 224, 0.28);

  /* 色彩：報告狀態（每種狀態：文字/邊框色 + 淡底色；一律搭配圖示與文字，不單靠顏色）
     選用方案 A「橘／藍／綠／灰」，與其他方案的比較見 design-system.md */
  --status-pending: #a64b00;        /* 未完成：橘棕 */
  --status-pending-bg: #fff4e5;
  --status-done: #1f5fa8;           /* 已完成：藍 */
  --status-done-bg: #e8f1fb;
  --status-certified: #17653f;      /* 已認證：綠 */
  --status-certified-bg: #e6f4ec;
  --status-dc: #5f6b7a;             /* 醫令已 DC：灰（另加刪除線） */
  --status-dc-bg: #eceff3;

  /* v2 新增：流程上「還不能打」的狀態（虛線外框區分） */
  --status-waiting: #5f6b7a;        /* 等待影像、待指派：灰、虛線框、白底 */
  --status-waiting-bg: #ffffff;
  /* v2 新增：修飾標籤（與主要狀態並排，不取代主要狀態） */
  --status-recall: #6b3fa0;         /* 取消認證・待重打：紫 */
  --status-recall-bg: #f3edfa;
  --deadline-overdue: #ffffff;      /* 已逾時：紅底白字（實心，最強烈） */
  --deadline-overdue-bg: #b42318;
  --deadline-soon: #b42318;         /* 即將到期：紅字、淡紅底 */
  --deadline-soon-bg: #fdecea;

  /* 字級 */
  --font-family: "Noto Sans TC", "Microsoft JhengHei", "PingFang TC", sans-serif;
  --font-size-xs: 12px;        /* v3：區塊標籤（大寫、加寬字距） */
  --font-size-sm: 13px;
  --font-size-md: 15px;
  --font-size-lg: 18px;
  --font-size-xl: 22px;
  --font-size-display: 36px;   /* 未完成數量專用 */
  --letter-spacing-label: 0.12em;

  /* 間距 */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-6: 24px;

  /* 圓角 */
  --radius: 10px;              /* 按鈕、輸入框 */
  --radius-lg: 18px;           /* 卡片、面板 */

  /* 控制項最小高度（點擊範圍；手機上加大） */
  --control-height: 36px;
}

@media (max-width: 700px) {
  :root { --control-height: 44px; }
}
```
