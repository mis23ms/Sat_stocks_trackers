# Sat_stocks_trackers
Sat_stocks_trackers
```md
# Sat_stocks_trackers

整合三個 GitHub Actions 追蹤器的「總覽 dashboard」，在同一頁看到：
- 今日重點（從各 repo 的 `index.md` 解析出最新連結）
- 最新更新（用 GitHub repo 的 `pushed_at` 當更新時間）

收錄來源：
- TW Stock News Tracker（台股新聞追蹤）：https://github.com/mis23ms/TW_Stock_News_Tracker
- SEC Filing Tracker：https://github.com/mis23ms/US_ETF_Stocks
- tw-keyword-research：https://github.com/mis23ms/tw-keyword-research

---

## Dashboard

GitHub Pages：
https://mis23ms.github.io/Sat_stocks_trackers/

---

## Repo 結構

```

Sat_stocks_trackers/
├─ index.html
└─ README.md

```

---

## 資料怎麼抓

### 今日重點
- 讀取每個來源 repo 的 `index.md`（raw）
- 解析 Markdown 裡的連結 `[title](url)`
- 如果是相對路徑（例如 `reports/2026-02-11.md`），會自動補成該 repo 的 GitHub Pages URL

### 最新更新
- 讀取每個來源 repo 的 GitHub API
- 以 `pushed_at` 顯示更新時間

---

## 來源設定

`index.html` 內有 `SOURCES` 設定，三個來源都包含：

- `pagesBase`：該 repo 的 GitHub Pages 首頁
- `indexRaw`：該 repo 的 `index.md` raw 連結
- `repoApi`：該 repo 的 GitHub API 連結

只要這三個欄位正確，dashboard 會自動運作。

---

## GitHub Pages 設定

Settings → Pages
- Source：Deploy from a branch
- Branch：`main`
- Folder：`/(root)`

確保 repo 根目錄有 `index.html`。

---

## 常見問題

### 點進去 404
通常是 `index.md` 內的相對連結沒有被正確補成 Pages URL。
請檢查 `SOURCES[i].pagesBase` 是否是該 repo 真正的 Pages 首頁（大小寫也要一致）。

### 今日重點數量太少/太多
`index.html` 內 `parseIndexHighlights(indexMd, 12)` 的 12 是顯示上限。
```
