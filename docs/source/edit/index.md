# Edit GitBook

<hr>

### Global Installation

如果要在本地進行 gitbook 的閱讀或編輯，請使用 `npm` 指令安裝。  
> 請確認是否已安裝 [Nodejs](https://nodejs.org/en/)

```bash
npm install -g gitbook-cli
```

```bash
gitbook install
```

### Run Gitbook

#### View

使用 `dev` 可以在本地 [http://192.168.0.100:8080](http://192.168.0.100:8080) 進行閱讀。
```bash
npm run dev
```

如果要監控檔案的變更即時編譯，請於第一次執行 `dev` 後刪除資料夾 `_book`，後續的變更皆會重新編譯，網頁會自動刷新。
> 此問題來自 [git serve can't restart when file changes #1379](https://github.com/GitbookIO/gitbook/issues/1379)    

#### Image

目前圖片都是放置於 [imgur](https://imgur.com/)，如果要在文中插入圖片，請安裝 [vscode-imgur](https://github.com/MaxfieldWalker/vscode-imgur)，就可以使用快速鍵，在編輯器中貼入圖片並自動上傳。
> 已不需要再額外編寫設定檔案，設定檔已存於 `.vscode` / `settings.json`

> 快速鍵 `Ctrl` + `Alt` + `V`

### Build To HTML

使用 `build` 編譯出靜態檔案，輸出目錄為當前路徑底下的 `docs` 資料夾。
```bash
npm run build
```

### Convert To PDF

使用 `pdf` 將產出 PDF 文件。
```bash
npm run pdf
```
> 如果 OS 為 Windows，請先安裝 [Calibre](https://calibre-ebook.com/download_windows)，並重啟終端機。