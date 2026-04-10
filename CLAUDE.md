# CLAUDE.md — cubxxw GitHub Profile Repo

## 关键规则：不要直接修改 README.md

**`README.md` 是由 GitHub Actions 自动生成的，每次 workflow 运行都会被覆盖。**

直接修改 `README.md` 的改动会在下次 Actions 触发后丢失。

**正确的修改方式：**
- 修改 `templates/README.md.tpl` — 这是 markscribe 模板源文件，Actions 读取它渲染生成 `README.md`
- 修改 `.github/workflows/` 下的 workflow 文件来调整 Actions 行为

## 项目结构

```
cubxxw/
├── templates/
│   └── README.md.tpl      # ← 主页内容在这里改，markscribe 模板
├── .github/workflows/
│   ├── update-readme.yml  # markscribe 渲染 tpl → README.md
│   ├── metrics.yml        # 生成 github-metrics.svg
│   ├── snake.yml          # 生成贡献蛇形动画（output 分支）
│   └── waka-readme.yml    # WakaTime 数据同步
├── README.md              # ← 自动生成，不要手动改
└── github-metrics.svg     # ← 自动生成，不要手动改
```

## markscribe 模板语法

`.tpl` 文件中可用的 Go 模板函数（由 markscribe 提供）：

```
{{range recentContributions 5}} ... {{- end}}   # 最近贡献的仓库
{{range recentRepos 5}} ... {{- end}}            # 最近创建的项目
{{range recentStars 5}} ... {{- end}}            # 最近 star 的仓库
{{range followers 5}} ... {{- end}}              # 最近的 followers
{{range recentPullRequests 5}} ... {{- end}}     # 最近的 PR
{{range rss "URL" 6}} ... {{- end}}              # RSS 博客文章
{{humanize .OccurredAt}}                         # 相对时间格式化
```

## metrics.yml 已关闭的插件

以下插件已删除（有问题或信息冗余）：
- `plugin_tweets` — Twitter API 401 报错
- `plugin_habits` — "uses spaces for indentation" 无意义内容
- `plugin_rss` — 知乎中文 RSS，与主页风格不符
- `plugin_gists` — 0 Gists，无内容
- `plugin_calendar` / `plugin_isocalendar` — 与 Activity Graph 重复
- `plugin_repositories` — 与 README 里 Featured Projects 重复
- `plugin_people` — followers/following 头像网格，冗余
