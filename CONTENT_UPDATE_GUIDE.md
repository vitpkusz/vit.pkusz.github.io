# 网站内容维护说明

这份文档说明后续如何更新 Visual Intelligence Team 网站内容。当前网站基于 Jekyll/al-folio，主要内容分散在 `_pages/`、`_data/`、`_news/`、`_bibliography/` 和 `assets/` 中。

## 常用文件速查

| 想改的内容 | 主要编辑文件 |
| --- | --- |
| 网站名称、描述、favicon、作者高亮 | `_config.yml` |
| 首页标题、logo、轮播入口 | `_pages/main.md` |
| 首页 News | `_news/*.md`，由 `_includes/news.liquid` 读取 |
| 首页 Recent Papers 和 Publications 页面 | `_bibliography/papers.bib`，页面壳在 `_pages/publications.md` |
| Awards 页面 | `_pages/awards.md` |
| Team 页面成员数据 | `_data/team.yml`，页面壳在 `_pages/people2.md` |
| 图片资源 | `assets/img/vit-pkusz/`、`assets/team/`、`assets/teaser/` |

不要编辑 `_site/`。如果本地构建生成了 `_site/`，它只是输出目录，源文件仍然是上表这些文件。

## 1. 更新首页

首页文件是 `_pages/main.md`。

首页保持和原 VAIL 网站相同的信息结构：顶部 logo/title、轮播、News、Recent Papers。Team 和 Awards 不直接写在首页，它们分别在 Team 和 Awards 栏目中维护。

### 修改首页 logo 或标题

在 `_pages/main.md` 中找到：

```html
<img src="{{ '/assets/img/vit-pkusz/logo.png' | relative_url }}" alt="Visual Intelligence Team logo">
<div class="lab-title">Visual Intelligence Team</div>
```

替换图片路径或标题文字即可。图片建议放在 `assets/img/vit-pkusz/`，文件名尽量使用英文小写和短横线，例如 `lab-logo.png`。

### 修改首页轮播

在 `_pages/main.md` 顶部 front matter 中修改 `highlighted_projects`：

```yaml
highlighted_projects:
  - teaser_img: /assets/img/vit-pkusz/dap.png
    caption:
    title: "DAP: Doppler-aware Point Network for Heterogeneous mmWave Action Recognition"
    link: /publications/
```

新增轮播项时复制一段 `- teaser_img...` 即可。图片路径以 `/assets/...` 开头。若使用视频，使用 `teaser_video: /assets/video/example.mp4`。

## 2. 更新 News

每条新闻是 `_news/` 下的一个 Markdown 文件。新增新闻时，新建文件：

```text
_news/2026-07-01-example.md
```

内容模板：

```markdown
---
layout: post
date: 2026-07-01
inline: true
vit_news: true
---

Your news content here.
```

注意事项：

- `date` 决定排序，格式用 `YYYY-MM-DD`。
- 必须保留 `vit_news: true`。当前 `_includes/news.liquid` 只显示带这个标记的新闻，这样旧 VAIL 新闻不会出现在首页。
- `inline: true` 表示新闻直接显示在列表中。如果改成非 inline，需要补充标题和正文页面。
- 新闻内容可以写 Markdown 链接，例如 `[ECCV 2026](https://eccv.ecva.net/)`。

## 3. 更新 Publications 和首页 Recent Papers

论文数据在 `_bibliography/papers.bib`。首页的 Recent Papers 和 `/publications/` 页面都会读取这里。

新增论文时，在 `_bibliography/papers.bib` 中追加一个 BibTeX 条目：

```bibtex
@inproceedings{unique2026key,
  abbr={ECCV},
  title={Paper Title},
  author={Last, First and Last, First},
  year={2026},
  booktitle={European Conference on Computer Vision},
  teaser={paper-teaser.png},
  website={https://example.com/project},
  pdf={https://example.com/paper.pdf},
  tags={Computer Vision, Action Recognition},
  selected={true}
}
```

注意事项：

- `unique2026key` 必须唯一，不要和已有条目重复。
- `selected={true}` 会让论文出现在首页 Recent Papers 中。
- `teaser={paper-teaser.png}` 对应文件应放在 `assets/teaser/paper-teaser.png`。
- 如果没有项目页或 PDF，可以删掉 `website` 或 `pdf` 字段。
- `tags` 用逗号分隔。如果新增了新的 tag，也要同步更新 `_pages/publications.md` 里的筛选按钮。
- `abbr` 是会议/期刊短名，例如 `ECCV`、`CVPR`、`ICCV`、`Arxiv`。

当前 Publications 页的筛选按钮在 `_pages/publications.md`：

```html
<button class="tag-btn" data-tag="Computer Vision">Computer Vision</button>
```

新增标签时，复制一行并修改 `data-tag` 和按钮文字。

## 4. 更新 Awards

Awards 页面文件是 `_pages/awards.md`。

直接编辑 Markdown 列表即可：

```markdown
- Student Name: Award Name, 2026
```

注意保留文件顶部的 front matter：

```yaml
---
layout: page
permalink: /awards/
title: Awards
nav: true
nav_order: 3
_styles: >
  .post-header { display: none; }
---
```

不要删除这段，否则页面路径、导航或样式会受影响。

## 5. 更新 Team

Team 页面显示逻辑在 `_pages/people2.md`，一般不需要改。成员数据在 `_data/team.yml`。

新增成员模板：

```yaml
- name: "Student Name"
  role: "M.S. Students"
  image: "../assets/team/example.jpg"
  link: false
  affiliation: "PKU Shenzhen"
```

常用 `role`：

- `Principal Investigator`
- `Postdoctoral Researchers`
- `Ph.D. Students`
- `M.S. Students`
- `Visiting Students and Scholars`
- `Alumni`

注意事项：

- 同一个 `role` 的成员会自动分到同一个栏目。
- 当前学生照片暂时复用 `assets/team/` 中原 VAIL 照片。后续替换真实照片时，把图片放到 `assets/team/`，再改对应成员的 `image`。
- `image` 路径保持 `../assets/...` 这种写法，因为 Team 页面在 `/team/`。
- 如果没有个人主页，保持 `link: false`。如果有主页，写完整 URL。
- Alumni 通常不需要 `image`，可以写：

```yaml
- name: "Alumni Name"
  role: "Alumni"
  link: false
  year: "2026"
  affiliation: "PKU Shenzhen"
```

## 6. 更新导航栏目

导航栏来自 `_pages/*.md` 的 front matter。常见字段：

```yaml
nav: true
nav_order: 3
title: Awards
permalink: /awards/
```

注意事项：

- `nav: true` 表示显示在导航栏。
- `nav_order` 越小越靠前。当前顺序是 Lab、Publications、Awards、Team。
- 首页 `_pages/main.md` 的 `permalink: /` 对应导航中的 Lab。
- 改 `permalink` 会改变页面 URL，除非确实需要，不建议改。

## 7. 更新图片和资源

建议按用途放置：

- 实验室 logo、主页通用图片：`assets/img/vit-pkusz/`
- Team 人像：`assets/team/`
- 论文缩略图：`assets/teaser/`
- 视频：`assets/video/`

注意事项：

- 文件名尽量使用英文、小写、短横线，例如 `dap-teaser.png`。
- 避免在正式资源文件名里使用空格或中文，减少路径兼容问题。
- 替换图片后，如果浏览器仍显示旧图，可能是缓存问题，强制刷新页面即可。
- 图片尽量压缩后再提交，避免页面加载过慢。

## 8. `_config.yml` 中常见可改项

`_config.yml` 是全站配置。常见字段：

```yaml
title: Visual Intelligence Team
description: >
  Visual Intelligence Team, HRI Lab, Peking University Shenzhen
icon: vit-pkusz/logo.png
baseurl: /vit.pkusz.github.io
```

注意事项：

- `title` 影响浏览器标题和站点元信息。
- `description` 影响站点描述。
- `icon` 对应 `assets/img/` 下的路径，不要写 `/assets/img/` 前缀。
- `baseurl` 和 GitHub Pages 部署路径有关，不确定时不要改。
- `scholar.first_name` 和 `scholar.last_name` 用于论文作者高亮；当前是 Mengyuan Liu。

## 9. 本地检查和预览

如果本机装好了 Ruby/Jekyll，可以运行：

```bash
bundle exec jekyll build
bundle exec jekyll serve
```

常见检查：

```bash
git status --short
```

如果构建失败，优先检查：

- YAML front matter 是否完整，文件顶部和结尾是否有 `---`。
- YAML 缩进是否使用空格，不要用 Tab。
- `_data/team.yml` 每个成员字段是否缩进一致。
- BibTeX 条目是否缺少逗号或右花括号。
- 图片路径是否存在，大小写是否一致。

当前 Codex 环境中没有 `ruby`、`bundle`、`jekyll`，因此无法在这里直接启动 Jekyll 预览；在本机或部署环境有 Ruby 工具链时再运行上面的命令。

## 10. 推荐更新流程

1. 先确定内容类型：News、Publication、Award、Team、Homepage。
2. 按上面的表格找到对应文件。
3. 复制已有条目作为模板，只改必要字段。
4. 新增图片时先放到合适的 `assets/` 子目录，再更新引用路径。
5. 运行 `git status --short` 看改了哪些文件。
6. 如果有 Ruby/Jekyll 环境，运行 `bundle exec jekyll build`。
7. 打开本地预览或部署后的页面，重点检查导航、图片、日期排序和链接。
