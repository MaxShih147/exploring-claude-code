# Git & GitHub 新手教學（macOS｜student 帳號）

本文件記錄在全新 macOS 使用者帳號（student）中，
從零開始使用 Git，並將本機專案成功推送到 GitHub 的完整流程。
內容以「實際操作成功」為準，適合沒有 Git 經驗的新手照做。

---

## 一、確認目前 Git 狀態（乾淨帳號檢查）

在 Terminal 中檢查 Git 是否已有設定：

`git config --global --list`

如果看到類似以下訊息（找不到設定檔），代表尚未設定過 Git，這是理想的新手狀態：

`fatal: unable to read config file '~/.gitconfig': No such file or directory`

---

## 二、設定 Git 使用者身分（第一次一定要做）

Git 的每一次 commit 都需要作者資訊，請先設定：

`git config --global user.name "你的名字或暱稱"`  
`git config --global user.email "你在 GitHub 使用的 email"`

確認設定是否成功：

`git config --global --get user.name`  
`git config --global --get user.email`

---

## 三、在本機初始化 Git repository

進入你的專案資料夾（例如本教學 repo）：

`cd ~/repos/exploring-claude-code`

初始化 Git：

`git init`

確認目前狀態：

`git status`

---

## 四、第一次加入檔案並 commit

將檔案加入追蹤（stage）：

`git add .`

建立第一次 commit：

`git commit -m "init: first commit"`

確認 commit 是否存在：

`git log --oneline -n 3`

如果能看到 commit 紀錄，代表本機 Git 設定完成。

---

## 五、在 GitHub 建立遠端 repository

1. 登入 GitHub
2. 點擊右上角「＋」→ New repository
3. Repository name 建議與本機資料夾相同（例如 exploring-claude-code）
4. 建立時 **不要勾選**「Add a README」
5. 建立完成後，取得 SSH 位址，例如：  
   `git@github.com:你的帳號/exploring-claude-code.git`

---

## 六、設定 SSH（第一次連線 GitHub 必做）

### 1. 檢查是否已有 SSH key

`ls ~/.ssh`

如果沒有看到 `id_ed25519`，請建立新的 key。

### 2. 產生 SSH key

`ssh-keygen -t ed25519 -C "你在 GitHub 使用的 email"`

一路按 Enter 使用預設設定即可。

### 3. 將公鑰加入 GitHub

顯示公鑰內容：

`cat ~/.ssh/id_ed25519.pub`

複製整段內容，到 GitHub：

Settings → SSH and GPG keys → New SSH key → 貼上並儲存。

### 4. 測試 SSH 連線

`ssh -T git@github.com`

第一次連線時會看到詢問是否信任 GitHub：

`Are you sure you want to continue connecting (yes/no/[fingerprint])?`

請 **手動輸入 `yes`** 並按 Enter。

看到類似以下訊息代表成功：

`Hi <你的帳號>! You've successfully authenticated, but GitHub does not provide shell access.`

---

## 七、設定遠端並推送到 GitHub

在專案資料夾中設定遠端：

`git remote add origin git@github.com:你的帳號/exploring-claude-code.git`

確認遠端設定：

`git remote -v`

推送到 GitHub（第一次）：

`git branch -M main`  
`git push -u origin main`

完成後，重新整理 GitHub 頁面，即可看到專案檔案。

---

## 八、完成檢查清單

- [ ] `git log --oneline` 看得到 commit
- [ ] `git remote -v` 看得到 origin
- [ ] `ssh -T git@github.com` 顯示驗證成功
- [ ] GitHub 網頁看得到檔案

完成以上項目，代表 Git 與 GitHub 已成功設定完成。