# Spec Kit 規格驅動開發

## 什麼是規格驅動開發

規格驅動開發（Spec-Driven Development）顛覆了傳統軟體開發流程。 過去幾十年，程式碼一直是主道，規格只是寫完成式的鷹架；規格驅動開發改變了這件事：**規格變成可執行的，直接產生可運作的實作，而不只是指導方向。**

---

## 核心開發理念

Spec Kit 是個開源工具組，讓你專注在產品情境和可預測的結果。它強調幾個核心概念：

- **意圖驅動開發（Intent-driven development）**  
  規格先定義「要做什麼」，再定義「怎麼做」。  
  規格要明確、有防護欄和組織原則。

- **多步驟精煉流程**  
  開發不是從提示詞一次生成程式碼，而是逐步精煉，讓 AI 模型逐層理解規格。

---

## 三種開發階段

Spec Kit 支援三種不同的開發情境：

1. **從零開始開發（0-to-1 Development / Greenfield）**  
  從高階需求開始，產生規格、規劃實作步驟，建構可上線的應用程式。

2. **創意探索（Creative Exploration）**  
  平行實作、探索不同解決方案，支援多種技術堆疊與架構，實驗各種 UX 模式。

3. **迭代增強（Iterative Enhancement / Brownfield）**  
  逐步加入功能、現代化舊系統、調整流程。

---

## 安裝與初始化

安裝 Spec Kit 很簡單，建議先有 **uv 套件管理工具**。uv 套件可由 curl 或 brew 安裝，用自然語言與 Claude Code 溝通他也可協助安裝。

---

### 從 uv 安裝

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
````

已安裝的情況下，如需升級：

```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

---

### 初始化專案

在 repos 層，打開終端機，以下命令可建立新專案：

```bash
specify init <專案名稱>
```

如果專案目錄已存在，或是想對現有專案新增 spec ，可用強制合併指令：

```bash
specify init . --force
# 或
specify init --here --force
```

執行後，Spec Kit 會詢問要使用哪個 AI 工具，選擇 Claude Code。依照個人習慣或作業系統，終端機可選擇 Bash 或 PowerShell。

---

## 指令參考

Spec Kit 提供兩組主要指令：**主要指令**與**斜線指令**。

---

### 主要指令

| 指令      | 說明                                              |
| ------- | ----------------------------------------------- |
| `init`  | 從最新範本初始化新的 Specify 專案                           |
| `check` | 檢查已安裝的工具（git、claude、gemini、code、cursor-agent 等） |

---

### 初始化參數

`specify init` 可使用的參數：

| 參數 / 選項                | 類型 | 說明                                                                                                     |
| ---------------------- | -- | ------------------------------------------------------------------------------------------------------ |
| `<project-name>`       | 參數 | 新專案目錄名稱（使用 `--here` 時可省略）                                                                              |
| `--ai`                 | 選項 | 指定 AI（claude、gemini、copilot、cursor-agent、qwen、opencode、codex、windsurf、kilocode、auggie、roo、codebuddy、q） |
| `--script`             | 選項 | CLI 命令解析器（sh 或 ps）                                                                                     |
| `--ignore-agent-tools` | 旗標 | 跳過 AI 工具檢查                                                                                             |
| `--no-git`             | 旗標 | 不初始化 Git                                                                                               |
| `--here`               | 旗標 | 在目前目錄初始化                                                                                               |
| `--force`              | 旗標 | 覆寫 / 合併現有內容                                                                                            |
| `--skip-tls`           | 旗標 | 跳過 SSL/TLS 驗證（不建議）                                                                                     |
| `--debug`              | 旗標 | 顯示詳細除錯輸出                                                                                               |
| `--github-token`       | 選項 | GitHub token（或使用環境變數）                                                                                  |

---

### 斜線指令

執行 `specify init` 後，可在 Claude Code 使用以下斜線指令。

#### 核心指令（❗必要流程）

| 指令                      | 說明                 |
| ----------------------- | ------------------ |
| `/speckit.constitution` | 建立或更新專案治理原則與開發指南   |
| `/speckit.specify`      | 定義要建構的內容（需求與使用者故事） |
| `/speckit.plan`         | 建立技術實作計畫與技術堆疊選擇    |
| `/speckit.tasks`        | 產生可執行的任務清單         |
| `/speckit.implement`    | 依計畫執行所有任務          |

#### 選用指令（品質與驗證）

| 指令                   | 說明                  |
| -------------------- | ------------------- |
| `/speckit.clarify`   | 釐清不明確規格（建議在 plan 前） |
| `/speckit.analyze`   | 跨檔案一致性與覆蓋率分析        |
| `/speckit.checklist` | 產生品質檢查清單            |

---

## 快速開始

以下為五個步驟的標準流程，每一步對應一個指令。

---

### 步驟一：建立專案原則

```text
/speckit.constitution
```

建立專注於程式碼品質、測試標準、使用者體驗與效能需求的原則。

`🧑‍💻 Max: 我沒用此指令，沒實驗過加不加的效果差異。`


---

### 步驟二：建立規格

```text
/speckit.specify
```

描述「要做什麼」與「為什麼做」，避免直接談技術實作。

`🧑‍💻 Max: 我的作法會是請 chatgpt 產生專案首頁用的 readme.md，其中會包含基礎描述、架構圖、架構選擇、to-do list、參考資料等，不用到太詳盡。然後使用此指令時，請他直接讀取 readme.md。`
```text
/speckit.specify 請以此專案 readme 作為基底
```
`🧑‍💻 Max: 他的產出會是詳盡規格書，並包含 user story。`

---

### 步驟三：建立技術實作計畫

```text
/speckit.plan
```

提供技術堆疊與架構選擇（例如 Vite、HTML/CSS/JS、本地 SQLite）。

`🧑‍💻 Max: 因為這部分的產出會非常龐大，輸出幾十份 md 都有可能，所以只要知道他是在設定 plan 以及撰寫 Claude.md 文件即可，可以想像成設定 Claude 的人設。`


---

### 步驟四：分解成任務

```text
/speckit.tasks
```

從實作計畫建立可執行的任務清單。

---

### 步驟五：執行實作

```text
/speckit.implement
```

依計畫執行所有任務，完成實作。

---
(還沒寫完...)