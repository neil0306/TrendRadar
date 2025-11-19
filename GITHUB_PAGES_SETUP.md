# GitHub Pages 自动更新设置指南

## 问题说明

如果你发现 GitHub Pages 不会自动更新，这是因为缺少了自动部署步骤。现在已经添加了自动部署功能。

## 设置步骤

### 1. 启用 GitHub Pages

1. 进入你的 GitHub 仓库
2. 点击 **Settings**（设置）
3. 在左侧菜单中找到 **Pages**（页面）
4. 在 **Source**（源）部分：
   - 选择 **GitHub Actions** 作为部署源
   - 不要选择分支部署（如 `gh-pages` 分支或 `master` 分支的 `/docs` 目录）

### 2. 验证工作流

工作流文件 `.github/workflows/crawler.yml` 已经包含了自动部署步骤：

- ✅ 爬虫运行并生成 `index.html`
- ✅ 自动提交更改到仓库
- ✅ 自动部署到 GitHub Pages

### 3. 检查部署状态

1. 进入 **Actions** 标签页
2. 查看 **Hot News Crawler** 工作流
3. 确认有两个作业：
   - `crawl`：运行爬虫并生成 HTML
   - `deploy`：部署到 GitHub Pages

### 4. 访问你的页面

部署完成后，你的 GitHub Pages 地址通常是：
- `https://你的用户名.github.io/TrendRadar/`

## 注意事项

1. **首次部署**：第一次部署可能需要几分钟时间
2. **自动更新**：每次爬虫运行后，如果生成了新的 `index.html`，会自动部署
3. **部署频率**：部署频率取决于你的爬虫运行频率（默认每 30 分钟）
4. **权限要求**：确保工作流有 `pages: write` 和 `id-token: write` 权限（已在工作流中配置）

## 故障排查

如果部署失败：

1. **检查 Actions 日志**：
   - 进入 Actions 标签页
   - 查看失败的工作流运行
   - 检查错误信息

2. **确认 Pages 设置**：
   - Settings → Pages
   - 确保选择了 **GitHub Actions** 作为源

3. **检查权限**：
   - Settings → Actions → General
   - 确保 "Workflow permissions" 设置为 "Read and write permissions"

4. **手动触发**：
   - 进入 Actions 标签页
   - 选择 "Hot News Crawler" 工作流
   - 点击 "Run workflow" 手动触发

## 技术说明

工作流使用以下步骤：

1. **crawl 作业**：
   - 运行 Python 爬虫生成 `index.html`
   - 提交更改到仓库
   - 上传 Pages artifact

2. **deploy 作业**：
   - 等待 crawl 作业完成
   - 从 artifact 部署到 GitHub Pages

这样确保了每次爬虫运行后，GitHub Pages 都会自动更新。

