# MkDocs 教學：建立 GitHub Pages 網站

## 步驟一：建立檔案結構

你的專案需要以下結構：

```
my-repo/
├── mkdocs.yml          # 網站設定檔
├── docs/
│   ├── index.md        # 首頁
│   ├── page1.md        # 其他頁面
│   └── images/         # 圖片資料夾
└── .github/
    └── workflows/
        └── deploy.yml  # 自動部署設定
```
!!! note "注意事項"

    為什麼 publish*.yml 檔案到 GitHub 需要再創建一個 `.github/workflows` 資料夾然後裡面再放一個 `*.yml` 檔案？

    Ans:

    1. 原因很簡單：這是 GitHub 的平台規則，那個 yml 不是「要被發佈到 GitHub Pages 的內容」，而是「叫 GitHub 幫你自動做事的設定檔」，是 GitHub Actions 的約定路徑。GitHub 只會到固定位置找這種設定，所以必須放在 `.github/workflows/` 底下。

    2. 資料夾位置不能亂放。GitHub Actions 只會辨識 `.github/workflows/` 裡面的 `.yml` 或 `.yaml`。如果你放在專案根目錄、docs 或寫成 `.github/workflow/`（單數），GitHub 都不會把它當成 workflow。

    3. 可以把它理解成：

        - 網站內容：放在 `docs/` 或 build 後的 `site/`
        - GitHub Actions：放在 `.github/workflows/`

        GitHub 只會去固定的地方找自動化腳本。


## 步驟二：撰寫 Markdown

每個 `.md` 檔案就是一個網頁。使用標準 Markdown 語法：

```markdown

# 標題

這是一段文字，支援 **粗體**、*斜體*、`程式碼`。

## 小標題

- 列表項目 1
- 列表項目 2

| 欄位 A | 欄位 B |
|--------|--------|
| 值 1   | 值 2   |
```
!!! note "注意事項"
    關於Markdown語法，可以參考 [Markdown入門語法](<https://vocus.cc/article/68efa7c1fd89780001a99c46>)

## 步驟三：設定 `mkdocs.yml`

這是網站的核心設定檔：

```yaml
site_name: 我的網站名稱
site_url: https://<username>.github.io/<repo>/

theme:
  name: material        # 使用 Material 主題
  language: zh-TW       # 中文介面

nav:                    # 導覽列
  - 首頁: index.md
  - 關於: about.md
```
## 步驟四：連接 GitHub 並上傳檔案

1. 到 VS Code 的終端機
2. 輸入指令

```bash
# 1. 先 cd 到你想放專案的資料夾
cd C:\Users\tsungnan\Projects

# 2. 複製指定的 repo
git clone https://github.com/TNKuo/EBOOK_test.git

# 3. 進入專案資料夾
cd EBOOK_test

```

3. 修改檔案後上傳，輸入：


```bash
    # 1. 查看哪些檔案有改動
    git status

    # 2. 加入所有改動的檔案 (「把目前資料夾內所有我要提交的變更，先放到待出貨區（Staging Area）。」)(其中 .代表目前資料夾的意思。)
    git add .

    # 3. 建立存檔點（寫下你改了什麼）(其中 -m 是 message（提交訊息） 的意思。)
    git commit -m "新增首頁內容"

    # 4. 上傳到 GitHub
    git push
```
或是
```bash
    # 1.把目前所有變更加入暫存區（包含新增、修改、刪除檔案）。你剛剛選「全部一起推（包含刪除與 site）」，所以用 -A 最符合。
    git add -A

    # 2.建立一個提交（commit），把剛才暫存的內容打包成一個版本。
    -m 後面是這次變更的說明文字。
    git commit -m "..."
    
    # 3.把本地 main 分支的最新 commit 推到遠端 origin（GitHub）。
    git push origin main
```
    
!!! note "Git 會自己辨認上傳的repositories嗎?"
    重點是這三層：

    你目前在哪個 git 專案資料夾
    Git 先看當前路徑（或其上層）有沒有 .git，這決定是「哪個本地 repository」。

    你 push 的 remote 名稱
    例如 git push origin main 裡的 origin，會對應到一個遠端 URL。

    分支對應（tracking）
    如果你只打 git push，Git 會用目前分支追蹤的遠端分支（若已設定）。

    可以用這幾個指令確認，不會推錯：
    ```bash
    git rev-parse --show-toplevel
    git remote -v
    git branch -vv
    ```

## 步驟五：設定 GitHub Actions 自動部署

在 `.github/workflows/` 建立部署檔案，推送後 GitHub 會自動編譯並發布。

## 步驟六：啟用 GitHub Pages

1. 到你的 repo → **Settings** → **Pages**
2. Source 選擇 **GitHub Actions**
3. 推送程式碼到 `main` 分支
4. 等待 Actions 完成，網站就上線了！

!!! success "完成！"
    你的網站會在 `https://<username>.github.io/<repo>/` 上線。


## 步驟七：更新 GitHub Pages

1. 修改內容後，可以用下面指令預覽網頁。
```yaml
mkdocs serve
```
2. 修改完後，至修改後的資料夾，例如:D:\VScode\EBook_Markdown
3. 鍵入下面程式碼：
```bash
# 1. 加入所有改動的檔案
git add .

# 2. 建立存檔點（寫下你改了什麼）
git commit -m "新增首頁內容"

# 3. 上傳到 GitHub
git push
```
3. 至Github 的Repository選擇分支再合併入Main。

!!! Note:
    ```
    mkdocs gh-deploy --clean
    ```
    這個指令會改動並推送 gh-pages 分支，不是你目前開發分支。
    常見使用時機：
    你改了 getting-started.md 或 mkdocs.yml 後要上線。
    線上看到舊內容，想強制用乾淨產物重發一次。
    標準流程：
    ```
    git add -A
    git commit -m "update docs"
    git push origin tsungnan-snps-github-pages-setup
    mkdocs gh-deploy --clean
    ```
