# 快速開始：建立 GitHub Pages 網站

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
=="python"
'''
# 1. 先 cd 到你想放專案的資料夾
cd C:\Users\tsungnan\Projects

# 2. 複製指定的 repo
git clone https://github.com/TNKuo/EBOOK_test.git

# 3. 進入專案資料夾
cd EBOOK_test

3. 修改檔案後上傳，輸入:
      # 1. 查看哪些檔案有改動
    git status

    # 2. 加入所有改動的檔案
    git add .

    # 3. 建立存檔點（寫下你改了什麼）
    git commit -m "新增首頁內容"

    # 4. 上傳到 GitHub
    git push

'''


## 步驟五：設定 GitHub Actions 自動部署

在 `.github/workflows/` 建立部署檔案，推送後 GitHub 會自動編譯並發布。

## 步驟六：啟用 GitHub Pages

1. 到你的 repo → **Settings** → **Pages**
2. Source 選擇 **GitHub Actions**
3. 推送程式碼到 `main` 分支
4. 等待 Actions 完成，網站就上線了！

!!! success "完成！"
    你的網站會在 `https://<username>.github.io/<repo>/` 上線。
