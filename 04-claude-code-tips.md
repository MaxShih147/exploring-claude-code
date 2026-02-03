# Claude Code 實用 Tips

（斜線指令 × CLAUDE.md × 記憶系統 × Git 整合）

這份文件整理的是 **Claude Code 中最容易被忽略、但一旦知道就回不去的功能**。
不是照順序學，而是「用到再回來查」。

---

## 一、什麼是斜線指令（Slash Commands）？

在 Claude Code 中，只要輸入 `/`，就會看到一整排指令。

斜線指令的本質是：

- 一個指令 = 一整段工作流程
- 用來取代冗長的自然語言描述
- 可以整合工具、檔案、參數與記憶

👉 可以把它想成「AI 版快捷鍵」。

---

## 二、常見內建斜線指令（重點版）

| 指令                 | 功能說明                |
| ------------------ | ------------------- |
| `/init`            | 初始化專案，建立 CLAUDE.md  |
| `/help`            | 顯示所有可用指令            |
| `/review`          | 程式碼審查               |
| `/security-review` | 安全性檢查               |
| `/pr_comments`     | 查看 Pull Request 評論  |
| `/clear`           | 清除目前對話              |
| `/compact`         | 壓縮對話、保留重點           |
| `/permissions`     | 管理 Claude 可用工具權限    |
| `/cost`            | 顯示 token 使用量        |
| `/doctor`          | 檢查 Claude Code 安裝狀態 |
| `/config`          | 開啟設定介面              |
| `/model`           | 切換 AI 模型            |
| `/status`          | 顯示系統狀態              |

> 注意：指令會隨 Claude Code 版本調整，請以實際顯示為準。

---

## 三、最重要的一個指令：/init

如果只記得一個指令，**就是 /init**。

/init 會做的事情：

- 掃描整個專案結構
- 分析語言、框架與入口點
- 自動產生 CLAUDE.md
- 建立 Claude 對這個專案的「長期記憶」

沒有 /init，Claude 只是聊天工具
有了 /init，Claude 才是專案助理

---

## 四、CLAUDE.md 是什麼？

CLAUDE.md 是 Claude Code 的「專案記憶檔」。

你可以把它想成：

- 專案背景說明
- 技術與工具使用約定
- 不希望 Claude 做的事
- 團隊共識與規範

---

## 五、CLAUDE.md 的三個層級 (細節待補...)

### 1）專案層級

- 放在專案目錄
- 會進 Git
- 團隊共用

### 2）本地個人層級

- 僅影響自己
- Git 會忽略
- 適合放個人習慣

### 3）全域層級

- 放在 ~/.claude
- 影響所有專案
- 適合放通用偏好

---

## 六、用 # 指令直接寫入記憶

你可以直接對 Claude 說：

    # 專案一律使用 uv 建立 Python 環境，不要使用 pip

Claude 會詢問要存在哪一層，確認後寫入對應的 CLAUDE.md。

👉 這是「教 Claude 習慣」的核心技巧。

---

## 七、精準指定檔案（@filename）

你可以直接說：

    請分析 @src/components/Header.js

效果是：

- Claude 只會專注該檔案
- 不會掃整個專案
- 非常適合大型 repo

---

## 八、Shell 指令整合（進階）

斜線指令可以被允許執行特定 shell 指令，例如 git。

常見用途：

- 查看 git 狀態
- 整理 commit
- 產生變更摘要

👉 本質上是「可控的 AI 終端助理」。

---

## 九、自訂斜線指令（最強功能）

斜線指令其實就是一個 Markdown 檔案。

放置位置：

    ~/.claude/commands/        （全域）
    <project>/.claude/commands/（專案限定）

一個檔案 = 一個指令。

---

## 十、最小自訂指令範例：/commit

檔名：commit.md
內容只要一句話即可：

    分析目前的程式碼變更，產生有意義的 git commit 訊息，並執行 git commit。

重開 Claude Code 後即可使用：

    /commit

---

## 十一、指令參數（$ARGUMENTS）

指令可以接受參數，例如：

    請執行 $ARGUMENTS 的測試，並產生測試報告。

使用時：

    /test user authentication
    /test database migration

---

## 十二、控制 Claude 的節奏（很重要）

- Esc：立即中斷 Claude
- /clear：清掉對話重新開始
- /compact：保留重點、減少雜訊

---

## 十三、什麼時候該寫成斜線指令？

如果你常對 Claude 說：

- 幫我整理 commit
- 幫我檢查 PR
- 幫我寫文件
- 幫我跑固定流程

👉 就該把它寫成斜線指令。

---

## 結語

你不是在「用 AI 寫程式」，
而是在 **把自己的工作流程變成工具，交給 AI 執行**。

從一個指令開始就好。

---

## 下一步（建議）

- 把最常用的一句話，做成第一個自訂指令
- 每卡一次，就想：這能不能變成指令？
