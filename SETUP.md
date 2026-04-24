# 部署步骤

## 1. 建同名仓库

在 GitHub 上创建新仓库：
- 仓库名：**`erwanjun`**（必须和你用户名完全一致）
- 公开（Public）
- 先别勾选 Add README（我们要推本地的过去）

## 2. 推送代码

在 `/Users/jiaqi/erwanjun` 目录执行：

```bash
cd /Users/jiaqi/erwanjun
git init
git add .
git commit -m "feat: initial profile README"
git branch -M main
git remote add origin https://github.com/erwanjun/erwanjun.git
git push -u origin main
```

## 3. 开启 workflow 写权限（关键一步）

去仓库页面：
**Settings → Actions → General → Workflow permissions**
→ 勾选 **Read and write permissions** → Save

否则贪吃蛇和博客同步的 workflow 会因为没权限写回仓库而失败。

## 4. 手动跑一次贪吃蛇

**Actions 标签页 → Generate Snake → Run workflow**

跑完会新建一个 `output` 分支，里面有生成好的 SVG。README 里的贪吃蛇图就能显示了（可能要等 1-2 分钟 CDN 缓存刷新）。

## 5. 定制化（可选，按需改）

打开 `README.md`，搜索并替换：

| 占位符 | 替换成 |
|---|---|
| `your-blog.com` | 你的博客地址（没有就删掉相关行） |
| `your-email@example.com` | 你的邮箱 |
| `Erwan Jun` | 你想展示的名字 |
| `I'm currently working in China.` | 你的简介 |
| `I'm currently learning Golang, Python...` | 你在学的东西 |
| `.github/assets/cover.gif` | 把你自己的封面图放到 `.github/assets/cover.gif` |

## 6. 博客同步（可选）

如果你有博客：
- 编辑 `.github/workflows/blog-post-workflow.yml`
- 把 `feed_list` 里的 URL 换成你博客的 RSS 地址
- 推送后去 Actions 手动触发一次

如果你没博客：
- 直接删掉 `.github/workflows/blog-post-workflow.yml`
- 同时删掉 `README.md` 里 `Recent Blog` 那一整块

## 7. 验证

打开 `https://github.com/erwanjun`，你应该看到：
- 顶部两栏介绍
- GitHub 统计卡片（数据来自 Vercel，几秒后加载）
- 贪吃蛇吃格子动画（需要 step 4 跑完）
- Streak 连续提交天数
- 技术栈徽章
- 最新博客列表（如果配了 RSS）

## 常见问题

**Q: 贪吃蛇图显示不出来？**
A: 检查 Settings → Actions → General 的 Workflow permissions 是不是 Read and write。然后 Actions 里手动 Run workflow 跑一次 Generate Snake。

**Q: 统计卡片加载慢/挂掉？**
A: 这是 Vercel 公共服务的问题，有时候会抽风，刷新一下就好。

**Q: Streak 连续天数不准？**
A: `streak-stats.demolab.com` 是社区托管的，偶尔会延迟。
