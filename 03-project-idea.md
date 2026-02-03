# 03-project-idea.md

本章目標：先把「第二個開發 repo 要做什麼」講清楚，並列出最小可行版本（MVP）需要的東西。這個 repo 會用來做一個好玩的 App：使用者在 UI 輸入一句人話，系統把它變成「可執行的操作計畫」，再自動呼叫 Claude Code 去真的把事情做完（建檔、改檔、跑指令、commit）。

## 專案概念（一句話）
用一個簡單 UI，把「人話 prompt」轉成「可執行的 Claude 行動計畫」，並自動執行，不需要真人複製貼上。

## 使用者體驗（MVP）
1. 使用者在網頁輸入一句話（例如：建立一個 React 專案並在首頁顯示 Hello）
2. 按下 Run
3. UI 顯示系統產生的計畫（可先 dry-run）
4. 按下 Confirm 後開始執行
5. UI 顯示執行進度與結果（成功 / 失敗 + log）
6. 最後產出一個真正被修改過的資料夾（或專案），並可選擇自動 commit

## 系統角色分工（很重要）
- ChatGPT：把人話翻譯成「結構化計畫」（只輸出 JSON，不直接執行）
- Python（Orchestrator）：驗證計畫、逐步執行、呼叫 Claude Code、回報進度
- Claude Code：在指定 repo / 資料夾內真正動手做事（看檔案、改檔案、跑指令）
- React UI：輸入 prompt、顯示 plan / log、提供 Run / Confirm 的操作

## 需要的東西（Checklist）

### A) 必要軟體／環境
- Node.js（用來跑 React 前端；如果只做後端也可以先不裝，但做 UI 就需要）
- Python 3（建議 3.10+）
- Claude Code（已完成安裝）
- Git（已完成安裝）
- VS Code（已完成安裝）

### B) 需要的帳號與金鑰
- OpenAI API Key（給 Python 呼叫 ChatGPT 產生「計畫 JSON」）
- Claude / Anthropic 相關登入或 Token（依 Claude Code 目前使用方式；至少要能在終端機正常執行 claude 指令）
- GitHub（可選：若要自動 push 或建立 repo）

### C) 需要的專案架構（最小版）
- `frontend/`：React UI（輸入 prompt、顯示 plan、顯示 log）
- `backend/`：Python API（FastAPI）
- `workspace/`：執行區（所有 Claude Code 的操作限制在這裡，避免亂動系統）
- `schemas/`：計畫格式（JSON schema 或型別定義）

### D) 需要定義的資料格式（超重要）
一個「計畫 JSON」格式，至少包含：
- `goal`：一句話目標
- `workspace`：要在哪個資料夾執行（例如 workspace/demo-app）
- `actions[]`：一連串步驟（白名單）
  - shell：允許的指令（需白名單）
  - file_write：寫入檔案（路徑限制在 workspace）
  - file_edit：修改檔案（可先由 Claude Code 代勞）
- `mode`：dry-run 或 run

### E) 最小安全設計（MVP 也要有）
- 只允許在 `workspace/` 底下操作（禁止跑到 ~/ 或 /）
- `shell` action 只允許白名單（例如：mkdir、cd、npm create vite、pip install…）
- 預設先 dry-run，讓使用者看到計畫再 confirm
- 所有輸出（stdout/stderr）要回傳到 UI 顯示（方便 debug）
- 每次執行建立獨立資料夾（例如 workspace/job-0001）

## MVP 里程碑（建議順序）
1. 後端 CLI 版跑通：Python 接 prompt → 呼叫 ChatGPT 產 plan → 逐步執行（不做 UI）
2. 加上 dry-run：先顯示 plan，不執行
3. 加上 run：確認後執行並回報 log
4. 加上 React UI：輸入 prompt / 顯示 plan / 顯示 log
5. 加上「可選 commit」：執行完成後自動 git add/commit（先不 push）

## 下一步（你可以選一個先做）
- 先建立第二個開發 repo（建議命名：prompt-to-claude 或 command-bridge）
- 先定義 plan JSON 格式 v0.1（最小 action 白名單）
- 先用 Python 做一個最小 FastAPI：/plan（產 plan）、/run（執行）