家庭生活管理 APP V2.1 年度備註（免修改 Firebase 規則）部署說明

一、此版本只需更新 GitHub 程式檔。
Firebase 專案：family-life-manager-694c7（不需調整）
Firestore Security Rules：維持目前已發布版本，請勿上傳或發布 ZIP 中的 firestore.rules。該檔僅供參考比對。
EHS 專案 esh-v85 不受影響。

二、更新步驟
1. ZIP 解壓縮後，將 index.html、app.js、style.css、sw.js 等程式檔覆蓋 GitHub 儲存庫 family-life-manager-app 的同名檔案。
2. 提交 Commit，至 GitHub Actions 確認 Pages 部署成功。
3. 開啟 https://doublewater0804.github.io/family-life-manager-app/；若顯示舊版，關閉並重新開啟已安裝的 PWA，等待新版 Service Worker 接管。

三、資料儲存
年度備註儲存於 families/home/events/year-note-YYYY；文件帶 id、kind=year-note、scope=shared，因此符合現行 events 寫入規則。
此類紀錄不會列入月份記事清單，卻會納入 data.yearNotes JSON 備份／還原。
不同年份獨立資料，全體有效家庭成員可修改；儲存時會檢查是否被其他人更新。
右下角拖曳高度及展開／收合，維持原功能；高度只保留在本機瀏覽器。

四、驗收順序
1. 登入後在 2026 年輸入備註並儲存，應顯示成功。
2. 重新整理及換家人帳號後仍能看到相同內容。
3. 切到 2027 年應為獨立備註。
4. 月份記事不可出現「年度備註」文件。
5. 匯出 JSON，確認 data.yearNotes 有備註內容。
6. iPhone／iPad 實機確認高度調整可用。

五、注意
如先前版本曾經將備註寫入 yearNotes 專用集合，本版本不會自動讀取或移轉該集合（因目前安全規則禁止讀取）。一般僅部署但尚未使用該版者不受影響。
本版已進行靜態檢查，Firebase 線上驗收仍需上線後執行。
