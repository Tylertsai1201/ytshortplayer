# ytshortplayer：YouTube Shorts 連續播放器

貼上 YouTube 播放清單（公開或「不公開」都可以），就能連續播放、隨機播放，並記住上次看到哪裡。不用登入、不用 API 金鑰、不扣任何人的點數。

播放器本身不記錄任何特定清單：清單 ID 只出現在使用者自己的連結裡。

## 用法

- 首頁貼上連結：https://tylertsai1201.github.io/ytshortplayer/
- 指定清單：`https://tylertsai1201.github.io/ytshortplayer/?list=<播放清單ID>`
- 直接把 YouTube 連結接在後面也可以：`https://tylertsai1201.github.io/ytshortplayer/https://www.youtube.com/playlist?list=<ID>`（由 `404.html` 取出 `list=` 後轉址）
- 自訂大標題與副標（選用）：`?list=<ID>&title=<大標題>&sub=<副標>`；沒帶的話用 YouTube 上的清單名稱與頻道名

## 運作方式（全部在看的人的瀏覽器裡完成）

| 項目 | 做法 |
|---|---|
| 讀清單有哪些影片 | 背景開一個看不見的 YouTube 播放器，用播放清單模式載入（不播放），向它要影片 ID。最多 200 部 |
| 讀標題 | YouTube 公開的 oEmbed 查詢，一部問一次，存在瀏覽器裡，下次不用再問 |
| 排序 | 八成以上標題開頭有編號（如 001）就依編號排，否則照 YouTube 清單順序 |
| 播放 | 一次只載入單一影片（手機上用播放清單模式播 Shorts 會出現錯誤代碼 2） |
| 播完接下一部 | 手機的 Shorts 播放器會自動重播、不發出播完訊號，所以每 0.25 秒檢查一次，偵測到「從片尾跳回片頭」就算播完 |
| 進度條 | 只在手機等觸控裝置顯示自製進度條；電腦版 YouTube 播放器本身就有 |
| 記憶 | 存在各自瀏覽器的 localStorage（瀏覽器本機儲存），換裝置會從頭開始 |

## 本機預覽

```powershell
cd "C:\Users\AIXAI\OneDrive\Desktop\Tyler's OBS\002.Projects\ytshortplayer"
python -m http.server 8767
```

打開 http://127.0.0.1:8767/
