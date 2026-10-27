# 💬 Streamlit × Groq API AI 聊天室

使用 **Streamlit** 建立的 AI 聊天網頁，透過 **Groq API** 呼叫 `openai/gpt-oss-120b` 模型。可以在本機執行，也能部署到 **Streamlit Community Cloud**，分享網頁連結給其他人使用。

## ✨ 專案功能

- 💬 聊天式介面：直接輸入問題並查看 AI 回答。
- 🧠 多輪對話：將目前工作階段的對話紀錄傳給模型，支援上下文互動。
- 🔄 新聊天按鈕：清除目前工作階段的聊天紀錄。
- 🔐 安全管理 API Key：透過環境變數或 Streamlit Cloud Secrets 設定，不需公開金鑰。
- ☁️ 雲端部署：支援 Streamlit Community Cloud。

> **模型說明**：此專案使用 `openai/gpt-oss-120b`，並非 Llama 模型。請確認你的 Groq 帳號可以存取該模型。

## 🗂️ 專案結構

```text
streamlit-groq-chat/
├── app.py             # Streamlit 應用程式入口
├── requirements.txt   # Python 套件清單
├── README.md          # 專案說明文件
└── .gitignore         # 避免提交機密與暫存檔
```

## 🛠️ 使用技術

- Python 3
- [Streamlit](https://streamlit.io/)
- [Groq Python SDK](https://github.com/groq/groq-python)
- Groq 模型：`openai/gpt-oss-120b`

## 🚀 本機執行

### 1. 下載專案並安裝依賴

```bash
git clone https://github.com/<你的GitHub帳號>/<你的儲存庫名稱>.git
cd <你的儲存庫名稱>
pip install -r requirements.txt
```

如果還沒建立 GitHub 儲存庫，也可以直接把這些檔案放在同一個資料夾中。

### 2. 取得 Groq API Key

前往 [Groq Console — API Keys](https://console.groq.com/keys)，建立並複製新的 API Key。

**不要把 API Key 寫死在 `app.py`，也不要將金鑰推送到 GitHub。**

### 3. 設定本機環境變數

macOS / Linux：

```bash
export GROQ_API_KEY="你的_GROQ_API_KEY"
```

Windows PowerShell：

```powershell
$env:GROQ_API_KEY="你的_GROQ_API_KEY"
```

### 4. 啟動 Streamlit

```bash
streamlit run app.py
```

依照終端機顯示的網址開啟網頁（通常是 `http://localhost:8501`）。

## ☁️ 部署到 Streamlit Community Cloud

1. 在 [GitHub](https://github.com/) 建立一個儲存庫，並上傳 `app.py`、`requirements.txt`、`README.md` 和 `.gitignore`。
2. 前往 [Streamlit Community Cloud](https://share.streamlit.io/) 登入，建立新的 App。
3. 選擇 GitHub 儲存庫與分支，**Main file path** 設為 `app.py`。
4. 在部署設定或 App 管理介面的 **Secrets** 中新增以下 TOML 設定（貼上你自己的金鑰）：

   ```toml
   GROQ_API_KEY = "你的_GROQ_API_KEY"
   ```

5. 儲存 Secrets 並部署或重新啟動 App。成功後即可取得可分享的 Streamlit 網址。

> Streamlit Cloud 會將 Secrets 提供給應用程式。本專案透過 `os.environ.get("GROQ_API_KEY")` 讀取金鑰。**不要把 Secrets 的實際內容放進 GitHub 儲存庫**。

## ⚙️ 模型參數

在 `app.py` 中可以調整：

| 參數 | 預設值 | 說明 |
| --- | --- | --- |
| `MODEL` | `openai/gpt-oss-120b` | 使用的 Groq 模型 |
| `temperature` | `0` | 輸出隨機程度 |
| `max_completion_tokens` | `1024` | 單次回應的最大完成 token 數 |
| `top_p` | `0.5` | 核心取樣參數 |
| `stream` | `False` | 等待完整回覆後顯示 |

## ❓ 常見問題

**`The api_key client option must be set`**  
尚未正確設定 `GROQ_API_KEY`。請檢查本機環境變數或 Cloud Secrets。

**`AuthenticationError`**  
金鑰可能無效或已撤銷。請確認 Groq Console 中的 API Key 是否有效。

**模型無法使用**  
確認模型 ID 正確且帳號有權使用；必要時參考 [Groq 模型文件](https://console.groq.com/docs/models) 更換模型。

**為什麼部署後別人也能聊天？**  
公開部署的 App 使用你設定的 Groq API Key 發送請求，可能產生使用量或費用。請留意使用額度和流量，避免將私有服務無限制公開。

## 📝 注意事項

- 聊天紀錄儲存在 Streamlit 的 `st.session_state` 中，重設工作階段後不會永久保留。
- 這是教學與展示用途的基本版本，尚未包含登入、持久化儲存或個別使用者額度管理。
- API 使用受 Groq 服務條款、模型可用性與帳號限制約束。
# groq
