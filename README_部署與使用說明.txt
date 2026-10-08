家庭生活管理 APP V2.0｜Spark 免費版｜部署說明

一、專案確認
Firebase 專案：family-life-manager-694c7（與 EHS 的 esh-v85 分開）
資料庫：(default)；Authentication 已啟用 Email/Password。
初始管理者文件：families/home/members/0nObHXjQkxfw8plQAu1wfCkK73n1
管理者文件必要欄位：uid=文件ID, name=管理者, role=admin, active=true。

二、Firestore 安全規則
本包 firestore.rules 配合先前已發布規則。若線上規則仍是前一步提供並發布的版本，不必重新發布；只要確認兩者規則與功能一致。其他規則版本應先備份並比對。

三、GitHub Pages 部署
1. 建立獨立 GitHub 儲存庫（例如 family-life-manager-app）。
2. 上傳本包根目錄所有前端檔案：index.html、app.js、style.css、firebase-config.js、manifest.webmanifest、sw.js、icon-192.png、icon-512.png。
3. GitHub 儲存庫 Settings → Pages → Deploy from a branch → main、/(root) → Save。
4. 等候網址 https://你的帳號.github.io/儲存庫名稱/ 啟用。
5. Firebase Console → Authentication → Settings → Authorized domains，新增「你的帳號.github.io」（僅填網域，不含 https 或路徑），若已存在就不需重複新增。
6. Safari 開啟 GitHub Pages HTTPS 網址 → 分享 → 加入主畫面。

四、帳號管理（Spark 免費版）
新增家人：
A. Firebase Console → Authentication → 使用者 → 新增使用者，填寫家人 Email 與初始密碼（勿將密碼給本工具）。
B. 複製新成員的 UID。
C. Firestore → families → home → members → 新增文件，文件 ID = 新成員 UID；新增 uid（string, 等於 UID）、name（string）、email（string）、role（string, member）、active（boolean, true）。
D. 家人可用 Email／密碼登入。第一次登入後請更改密碼。
停用家人：先於 Firestore 將對應 members 文件的 active 設為 false，再到 Authentication 停用其帳號；已開啟的頁面可能仍殘留先前顯示的資料，敏感資訊不得依賴用戶端清除。
不要將家庭成員設定 role=admin，除非要授予管理權限。
管理介面已改為「成員列表＋控制台操作說明」；無 Cloud Functions，也沒有 APP 內建立／停用帳號按鈕。

五、使用與限制
首頁、繳費、月曆、年度、設定、管理（僅管理者）保留。
家人可建立／修改家庭共用紀錄；共用資料點刪除會軟刪除到回收區；管理者可還原。
JSON 備份限定目前選擇範圍；匯入可合併或覆蓋。覆蓋共用資料只允許管理者；覆蓋前會下載一份備份，請確認已保存。
覆蓋共用資料採軟刪除原紀錄；大型備份分筆操作中斷可能有部分完成，若遇失敗可用備份重試。建議先用少量測試資料驗證匯出／還原。
裝置離線時 Firebase 登入與同步仍有條件限制，離線操作需先有成功登入、快取及權限驗證；不要將未同步資料視作已完成雲端備份。
固定繳費在 APP 開啟且登入成功後產生近期項目，不是伺服器定時排程。

六、驗收
先測：管理者登入 → 建立家庭共用繳費 → 建立私人記事 → 匯出 JSON → 另台裝置登入確認同步。
再建立測試家庭成員，檢查：能修改共用資料、不能讀取管理者私人資料、不能修改 member 文件。
最後測：共用資料刪除／還原、年度統計、重複固定繳費、資料匯入。

七、費用
使用 GitHub Pages + Firebase Authentication Email/Password + Firestore，通常可在 Spark 免費額度內進行小規模家庭使用，超過免費額度可能受限制。未使用 Storage/Functions，無需本包升級 Blaze。
