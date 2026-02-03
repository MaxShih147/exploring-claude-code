# Exploring Claude Code｜必要工具安裝（macOS）

本流程假設在全新 macOS 使用者帳號（student）中，電腦尚未安裝任何開發工具，目標是用最少步驟完成 Claude Code 的可用環境，新手只要照做即可。

## 安裝 Visual Studio Code（VS Code）

1. 打開瀏覽器  
2. 搜尋「Visual Studio Code download」  
3. 下載 macOS 版本並完成安裝  
4. 安裝完成後，打開 VS Code 一次即可  

VS Code 將作為後續編輯文件與程式的主要工具。

## 安裝 Git（假設尚未安裝）

1. 打開 Terminal  
2. 輸入 `git --version`  

如果系統跳出 Command Line Tools 的安裝提示視窗，請點選 Install 並等待完成，這個過程會同時安裝 Git；如果直接顯示 Git 的版本號，代表 Git 已經存在，不需要再安裝。安裝完成後可再次輸入 `git --version` 確認。

## 安裝 Claude Code（官方建議方式）

在 Terminal 輸入 `curl -fsSL https://claude.ai/install.sh | bash`，此指令會使用官方安裝腳本自動完成所有必要設定。安裝完成後，Claude Code 會被放在 `~/.local/bin/claude`。

## 設定 PATH（必要步驟）

若安裝完成後出現提示表示 `~/.local/bin` 尚未加入 PATH，請在 Terminal 直接執行 `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc`，此設定會立即生效，不需要重新啟動電腦或 Terminal。

## 確認安裝完成

請依序輸入 `git --version` 與 `claude --version`，只要兩者皆能顯示版本號，即代表必要工具已安裝完成，可以開始使用 Claude Code。

## 補充說明

本流程不需要事先安裝 Node.js 或 npm，官方安裝腳本會自動處理所有必要環境，新手只需確認能正常執行 `claude` 指令即可。
