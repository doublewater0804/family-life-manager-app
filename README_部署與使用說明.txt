家庭生活管理 APP V2.1 — 繳費基本資料維護版

一、部署
1. 保留現在 Firebase 專案 family-life-manager-694c7，以及 Authentication 帳號。
2. 至 GitHub doublewater0804/family-life-manager-app，將本 ZIP 解壓後所有檔案上傳覆蓋同名檔，確認 Commit changes。
3. 到 GitHub Actions 確認 pages build and deployment 成功。
4. 用 Safari 開啟 https://doublewater0804.github.io/family-life-manager-app/，重開或重新整理取得新版。
5. 不需修改 Firestore 安全規則：本版分類與繳費項目使用現有 families/home/templates 集合，符合目前 templates 讀寫規則。

二、基本資料使用方法
年度首頁 → 設定與繳費基本資料管理 → 繳費基本資料管理。
分成「繳費項目」與「項目分類」兩個頁籤，全部家庭成員均可操作。
繳費項目可建立名稱、分類、週期（預設一次性）、首次到期日、預設金額及啟用狀態。
分類可額外新增、編輯及停用自建分類；預設分類固定保留。
月度新增繳費時，選擇既有名稱，或選「其他（自行輸入新名稱）」；選「其他」存檔後會自動登記為基本資料（一次性）。分類為獨立下拉選單，可按當期情況選擇。
定期項目設定週期和首次到期日期後才會自動產生帳單。歷史月份資料不因基本資料改名而自動變更。
勾選已繳費會寫入當日實際日期，日期可在月份明細直接調整。

三、重要限制與驗收
本次僅完成程式語法和靜態檢查；Firebase 實際連線、iPhone/iPad 操作仍需自行驗收。
先用測試繳費項目確認：新增分類→新增項目→月份挑選→新名稱其他建立→重新整理保留→勾選並改繳費日期→另一帳號可見。
不要在未備份真實資料的情況下刪除 Firestore 集合或管理者會員資料。
本版未自動改寫既有 Firebase 資料，也不會影響工安 EHS 的另一個專案。
