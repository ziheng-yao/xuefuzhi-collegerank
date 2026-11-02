# 学府志 · 站点部署说明

这是「学府志」的静态站点包（**定版**）。**无构建步骤、无外部依赖**，`index.html` 打开即可运行。

## 目录

| 文件 | 说明 |
|---|---|
| `index.html` | 首页（已定版：B 版档案卡视觉 + 「按你的标准，给大学排名」叙事 + 权重演示模块 + 响应式） |
| `ranking.html` | 排名页（四维权重、子权重、预设、筛选、分页、显示数据不足） |
| `method.html` | 关于页（数据来源、算法、覆盖统计） |
| `data/schools.js` | 前端数据包（`window.__SCHOOLS__`，1412 所本科院校，约 860 KB） |
| `data/schools.json` | 同内容 JSON |
| `favicon.svg` | 站点图标（砖红方块 + 楷体「学」） |
| `og.png` | 分享图（1200×630） |

> 三页导航统一为「首页 / 排名 / 关于」，链接均为站点相对路径。部署时**上传整个 `site/` 目录的内容**，不要只上传单个文件。

## 本地预览

直接双击 `index.html`；或在 `site/` 目录下起一个静态服务器：

```bash
python -m http.server 8080
# 打开 http://127.0.0.1:8080
```

## 部署 · GitHub Pages（推荐，免费）

1. 在 GitHub 新建仓库，例如 `xuefuzhi-site`（公开仓库）
2. 把 `site/` **里面的内容**上传到仓库根目录（网页上传即可，不需要命令行）
3. 仓库 **Settings → Pages**：Source 选 *Deploy from a branch*，Branch 选 `main` / `(root)`，Save
4. 等 1–2 分钟，访问 `https://<你的用户名>.github.io/xuefuzhi-site/`

命令行方式（需先安装 git）：

```bash
cd site
git init
git add .
git commit -m "学府志 定版"
git branch -M main
git remote add origin https://github.com/<用户名>/xuefuzhi-site.git
git push -u origin main
```

## 部署 · Netlify / Vercel

- Netlify：登录后把 `site/` 目录直接拖进「Deploy manually」区域
- Vercel：New Project → 选择仓库（或拖拽上传）→ Framework 选 *Other* → 不需要 Build Command → Deploy

## 部署后要改的一处

1. **`og:image` 改成绝对地址**：目前三页 meta 里是相对路径 `og.png`。微信/微博/Twitter 等平台抓取分享卡时通常需要完整 URL，部署后请改成 `https://你的域名/og.png`

## 说明

- 站点是单文件 HTML（内联 CSS/JS），部署时不需要 npm、不需要构建
- 字体使用系统字体栈（宋体 / 苹方 / 微软雅黑 / 楷体 / Bahnschrift），不依赖网络字体
- 数据为真实数据（1412 所本科院校，525 所四维齐全参与排名），已内联在 `data/schools.js`
