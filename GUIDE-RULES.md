# Game Guide Site — 建立新內容前必讀

## 檔案結構
```
game-name/
  index.html              # landing page（CollectionPage schema）
  articles/
    article-slug.html     # 攻略文章（Article schema）
```

## 每個新 HTML 檔案必須包含

### `<head>` 必要元素
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="120–160 字 SEO 描述">
<meta name="keywords" content="逗號, 分隔, 關鍵字">
<meta name="author" content="GameGuide.tw">
<meta name="google-adsense-account" content="ca-pub-4900630860092971">
<meta name="robots" content="index, follow">
<meta property="og:title" content="頁面標題 — 攻略站">
<meta property="og:description" content="與 description 相同">
<meta property="og:type" content="website（專區）或 article（文章）">
<title>頁面標題 — 攻略站</title>
```

### ld+json Schema
- **專區 landing page**: `CollectionPage` + `ItemList`
- **文章**: `Article` + `datePublished` + `dateModified` + `author`
- 鳴潮範例有 `itemListElement` 陣列

### 其他 `<head>`
```html
<link rel="canonical" href="https://game.cubedhub.com/完整路徑.html">
<script src='https://cdn.tailwindcss.com'></script>
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-4900630860092971" crossorigin="anonymous"></script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="../css/style.css（依目錄層級調整 ../ 數量）">
<script>tailwind.config = { theme: { extend: { fontFamily: { sans: ['Noto Sans TC', 'system-ui', 'sans-serif'] } } } }</script>
```

## 文章內容結構
1. Breadcrumb: `遊戲名 / 分類`
2. `<h1>` + 日期 `2026-07-30` + `約 X 分鐘閱讀`
3. Intro callout box（`bg-${color}-500/10 border`）
4. 編號章節 `一、...` 二、...（`<h2>`）
5. 表格：`bg-[#1a1d2e]` thead + `divide-[#2a2d3e]`
6. FAQ 章節：Q&A 卡片格式（`bg-[#1a1d2e] rounded-xl p-6`）
7. Footer + `© 2026 攻略站 GameGuide.tw`
8. `<script src="../../js/main.js">`（依層級調整）

## Navbar 規則
- Desktop: `hidden md:flex items-center gap-1`
- Mobile: `mobile-menu fixed top-0 right-0 w-72`
- Active 頁: `class="nav-link active"`
- Logo 連結指向上一層 `../index.html`

## 數據準確性
- 所有攻略數據（等級、數值、機制、日期）必須真實，不可編造
- 引用來源時附上連結（官方公告、巴哈姆特、媒體報導）
- 版本更新後需審查既有文章是否過時

## 遊戲圖片必備
- **首頁卡片**：每款在首頁顯示的遊戲，其 `.card-image` 必須有 `background-image: url('../images/遊戲名.jpg')` 指向真實遊戲截圖/Key Art
- **遊戲 landing page 卡片**：每個文章卡片也必須有 `background-image` 搭配遊戲圖片
- **遊戲專區 Hero**：可使用遊戲主視覺圖作為背景
- 圖片優先使用官方 Key Art、Steam header、Press Kit 素材
- 不允許只用純漸層背景而無遊戲圖片
- 圖片加上 `background-size:cover;background-position:center;` 確保正確顯示

## 新遊戲上線流程（Checklist）
- [ ] Navbar（桌面 + 手機）加入連結
- [ ] 首頁「熱門攻略遊戲」horizontal scroll 加入卡片
- [ ] 首頁「新上線攻略專區」加入卡片（如有 3 款以上新遊戲）
- [ ] 首頁「遊戲分類」grid 加入卡片
- [ ] 首頁「最新攻略文章」加入至少 1 篇文章
- [ ] 首頁 Footer「遊戲專區」加入連結
- [ ] 首頁快速入口 pills 加入連結（新遊戲標註 NEW）
- [ ] 遊戲圖片已放入 `images/` 目錄並引用
- [ ] 文章頁面卡片也使用遊戲圖片

## 絕對禁止
- `console.log`、`TODO`、`FIXME`、`debugger`
- `href="#"` 佔位連結
- 用 `<div>` 代替 `<a>` 包裹卡片
- 副檔名省略 `.html`（目錄 index.html 除外）
- 路徑 `../../` 層級錯誤（文章: `../../css/style.css`）
- 日期懶惰複製（每篇文章獨立維護日期）
- 新遊戲上線後只加 navbar 而忽略首頁其他區塊

## 顏色對應
| 遊戲 | 主色 | 漸層 |
|------|------|------|
| 瑪奇Mobile | indigo | `from-indigo-900/60 to-purple-900/60` |
| 新楓之谷經典版 | red | `from-red-900/60 to-orange-900/60` |
| 蔚藍檔案 | blue | `from-blue-900/60 to-cyan-900/60` |
| 鳴潮 | cyan | `from-cyan-900/60 to-teal-900/60` |
| 幻獸帕魯 | emerald | `from-emerald-900/60 to-teal-900/60` |
| 黑神話悟空 | amber | `from-amber-900/60 to-orange-900/60` |

## 部署
- push `master` 分支即自動部署
- 根目錄必須包含: `CNAME`、`ads.txt`、`robots.txt`、`sitemap.xml`
