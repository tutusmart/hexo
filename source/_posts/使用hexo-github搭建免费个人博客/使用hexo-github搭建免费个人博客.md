title: 使用hexo+github搭建免费个人博客
categories:
  - Hexo
date: 2019-10-12 10:43:32
tags:
---
### 1.安装启动
在GitBash 中操作，输入以下命令，等待安装完成。
```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org

```
a.安装 hexo
```shell
cnpm install -g hexo
```
b.初始化 hexo
```shell
hexo init
```
注意，其中有一个_config.xml文件，这个我们叫做站点根目录配置文件，里面的初始内容如下：（附上中文介绍）
c.配置文件
```xml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site 站点主配置
title: Hexo  # 网站标题
subtitle:    # 网站副标题
description:   # 网站描述
keywords:      # 可以不填写保持默认
author: John Doe  # 网站拥有者昵称
language:    # 网站语言设置，一般根据依赖的主题而定
timezone:    # 网站时区设置，一般不填写保持默认

# URL地址链接设置
url: http://yoursite.com   # 网站url设置
root: /                    # 网站根目录链接
permalink: :year/:month/:day/:title/   # 文章链接，默认是按照 /年/月/日/文章标题 设置的链接
permalink_defaults:                    # 默认链接形式

# Directory  网站主要目录，这里一般不做改动
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing  网站文章设置，同样一般不做改动
new_post_name: :title.md  # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:

# Home page setting  主页设置，一般不做改动
index_generator:
  path: ''
  per_page: 10
  order_by: -date  # 首页文章排序，默认是按照文章日期递减

# Category & Tag  分类设置，一般不做改动
default_category: uncategorized
category_map:
tag_map:

# Date / Time format  日期设置，一般不做改动
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination  导航页设置，一般不做改动
per_page: 10   # 设置每页展示多少文章
pagination_dir: page

# Extensions  使用的主题名称，可以在这里切换
theme: next  # 此处切换主题名称

# Deployment  部署，一般选择部署到Github上
deploy:
  type:
```
其实到这里来说，我们的 hexo 博客已经做好了！不信？我们执行下面命令看看：

```shell
//cd到根目录执行
$ hexo g
$ hexo s
```
然后我们打开浏览器，输入http://localhost:4000;
{% asset_img hexo1.png This is an example image %}

d.创建文章

```shell
hexo new "我的第一篇博客"

//或者可以简写为

hexo n "我的第一篇博客"
```
e.创建文件夹
```shell
hexo n [我的第一篇博客] 我的第一篇博客
```
### 2.上传到github
a.配置站点配置文件
1.打开根目录下站点配置文件_config.yml，配置有关deploy的部分：
{% asset_img 20191012104426.png This is an example image %}
b.安装插件
此时，直接使用hexo d部署到github，将出现如下错误：
```shell
$ hexo deploy
ERROR Deployer not found: git
```
这是因为需要安装如下插件
```shell
npm install hexo-deployer-git  --save
```
c.部署到github
```shell
hexo d
```

### 3.关于 标签 分类 归档
1.主题的 _config.yml 文件中的 menu 中进行匹配
```js
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签
  about: /about   //关于                  （添加此行即可）
```
编辑 about 关于页面 md文件 部署就能看到

2：添加 标签页面
使用： hexo new page tags 新建一个 标签 页面。
主题的 _config.yml 文件中的 menu 中进行匹配
底下代码是一篇包含 标签 文章的例子
```js
title: 标签测试
tags:
  - Testing                   （这个就是文章的标签了）
  - Another Tag               （这个就是文章的标签了）
---
```
3：添加 分类页面
使用： hexo new page categories 新建一个 分类 页面。
主题的 _config.yml 文件中的 menu 中进行匹配
```js
title: 分类测试
categories:
- hexo                       （这个就是文章的分类了）
---
```
5：添加 自定义页面
使用： hexo new page "guestbook" 新建一个 自定义 页面。
主题的 _config.yml 文件中的 menu 中进行匹配
```js
menu:
  home: /      //主页
  categories: /categories //分类
  archives: /archives   //归档
  tags: /tags   //标签
  about: /about   //关于
  guestbook: /guestbook    //自定义             （添加此行即可）
```