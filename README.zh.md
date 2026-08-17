中文 | [English](README.md)

# Hugo NexT 主題啟動器

這是 [Hugo NexT](https://github.com/hugo-next/hugo-theme-next) 的雙語範例站與起始範本，
包含示範文章、選單、資料及設定；主題本身以 Git submodule 固定版本。

## 環境需求

- Git
- Hugo **Extended 0.146.0 以上**（依目前主題的最低版本要求）

儲存庫記錄的主題 pointer 目前對應 Hugo NexT v4.8.3。

## 連同主題複製

`.gitmodules` 使用 SSH 網址，因此最直接的方式需要已設定 GitHub SSH key：

```bash
git clone --recurse-submodules https://github.com/iankingh/hugo-theme-next-starter.git
cd hugo-theme-next-starter
```

若先前未取得 submodule：

```bash
git submodule update --init --recursive
```

只使用 HTTPS 時，可先在本機覆寫 submodule 網址：

```bash
git config submodule.themes/hugo-theme-next.url https://github.com/hugo-next/hugo-theme-next.git
git submodule update --init --recursive
```

`startup.sh` 會讀取主題的 `VERSION` 檔，因此必須先完成 submodule 初始化。

## 預覽與建置

```bash
# 在 http://localhost:1414/ 預覽
sh startup.sh

# 不顯示啟動畫面的等效指令
hugo server --port 1414

# 正式建置，輸出至 public/
hugo --minify
```

`public/`、Hugo 產生的 resources 與 lock files 已由 Git 忽略。

## 自訂範本

- `config/_default/hugo.yaml`：網址、標題、語言、輸出格式及 Markdown 設定。
- `config/_default/languages.yaml`：中文與英文語言定義。
- `config/_default/menus*.yaml`：各語言的導覽選單。
- `config/_default/params*.yaml`：NexT 外觀與第三方整合設定。
- `content/`：雙語關於、歸檔、友情連結及功能範例文章。
- `data/flinks/`：各語言的友情連結資料。
- `static/`：直接複製的示範圖片、音訊與其他靜態檔案。
- `themes/hugo-theme-next/`：固定版本的上游主題；站點內容不應放入此目錄。

發布前至少要替換範例 `baseURL`、標題、作者資訊、選單、文章，以及所有已啟用的
第三方服務設定。

## 部署與自動化

本儲存庫**沒有網站建置或 GitHub Pages 部署工作流程**。執行
`hugo --minify` 後，可將 `public/` 靜態檔交由自行選擇的託管服務發布。

唯一的工作流程 `.github/workflows/sync-2-gitee.yml` 會在本儲存庫的 `main`
收到 push 時執行，再將寫死的上游 `hugo-next/hugo-theme-next-starter` 來源鏡像
到指定的 Gitee 儲存庫。它需要 `GITEE_RSA_PRIVATE_KEY` secret，且不會建置或
部署範例網站。Fork 若不擁有該鏡像，應檢查或停用此工作流程。

## 更新主題

submodule 設定追蹤上游主題的 `main`：

```bash
git submodule update --remote themes/hugo-theme-next
hugo --minify
git add themes/hugo-theme-next
```

提交新的 pointer 前，請先檢查主題版本說明與建置結果。

## 相關儲存庫

- `hugo-next/hugo-theme-next`：本範本使用的上游主題。
- `iankingh/blog`：使用相同主題、但獨立客製化的實際部落格。
- `iankingh/iankingh.github.io`：導向該部落格的轉址頁。
- `iankingh/iankingh`：GitHub 個人檔案 README，不參與本站建置。

## 授權

請參閱 [LICENSE](LICENSE)。
