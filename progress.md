# 家庭工具箱 · 專案進度

記錄 family-tools 這個小專案目前有哪些工具、用了什麼技術、還有哪些待辦事項，方便之後回來查閱或繼續開發。

線上首頁：https://linmayin.github.io/family-tools/

---

## 工具清單

### 1. 寢具清洗提醒（bedding_wash_tracker.html）
- 記錄每件棉被、被單的上次清洗日期
- 自動計算「建議下次清洗」日期（目前設定為 **6 週**後）
- 已清洗過的項目會自動依日期排到最上方，日期越早（越快到期）排越前面；尚未清洗的項目維持在下方，可手動拖曳排序
- 可自行新增／刪除／改名項目
- 儲存方式：**自動偵測環境**——在 Claude Artifact 裡用 `window.storage`，在 GitHub Pages 或本機瀏覽器則自動改用 `localStorage`，兩邊都能正常存資料

### 2. 資金紀錄（finance_tracker.html）
- 追蹤薪資、投資、專用帳戶三個帳戶的收支與轉帳紀錄
- 月度／年度預算檢視、餘額總覽、類別管理
- 新增「📤 匯入 JSON」功能，搭配原有的「📥 匯出 JSON」，可以把舊版（本機下載使用）的資料搬到新的線上版本
- 儲存方式：`localStorage`（在 GitHub Pages 或本機瀏覽器開都沒問題）

### 3. 暑期自主學習闖關（transit_challenge.html，原檔名「捷運大挑戰_全線版_.html」）
- 每日任務清單、30 分鐘專注計時（含分心偵測）
- 星星／蘋果獎勵機制，搭配高雄捷運紅／橘線與輕軌路網作為進度視覺化
- 家長管理區有密碼保護
- 儲存方式：`localStorage`

### 4. 肩頸舒緩動作教學計時器（shoulder_neck_timer.html）
- 教學動作搭配計時器，舒緩久坐久站的肩頸痠痛
- 儲存方式：`localStorage`

---

## 技術筆記

- **`window.storage` vs `localStorage`**：`window.storage` 是 Claude Artifact 專屬的儲存方式，只有在 Claude 對話的 Artifact 預覽視窗裡才存在；放到 GitHub Pages 這種一般網站環境後，`window.storage` 並不存在，資料會存不進去。目前只有寢具清洗提醒做了「自動偵測、兩邊都能用」的處理；其他三個工具目前都是用 `localStorage`，在 GitHub 上沒問題，但如果之後想在 Claude Artifact 裡使用並記錄資料，需要比照寢具清洗提醒的做法補上偵測邏輯。
- **GitHub 部署方式**：透過 GitHub API（`GET` 現有檔案 SHA → base64 編碼 → `PUT` 更新）部署，Python 的 `urllib.request` 優先於 shell curl，尤其是處理中文內容或大檔案時。
- **Repo 與 GitHub Pages**：`linmayin/family-tools`，Pages 來源為 `main` 分支根目錄。

---

## 更新紀錄

- 建立 family-tools repo，整合四個工具並建立 index 首頁
- 寢具清洗提醒：清洗週期由 2 個月調整為 6 週
- 寢具清洗提醒：已清洗項目改為依日期自動排序，鎖定其拖曳把手；未清洗項目仍可手動拖曳排序
- 資金紀錄：新增「匯入 JSON」功能，解決舊版資料搬移問題
- 寢具清洗提醒：修正儲存機制的環境相容性問題（`window.storage` 在 GitHub Pages 上失效的問題）

---

## 待辦事項

- [ ] 視需要為資金紀錄、暑期自主學習闖關、肩頸舒緩動作教學計時器補上「自動偵測環境」的儲存邏輯，讓它們在 Claude Artifact 裡也能可靠存資料
- [ ] 首頁圖示目前為線條 SVG，之後可考慮換成自訂圖示（比照 teacher-tools 的做法）
