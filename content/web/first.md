---
title: "Hugo Setup"
date: 2020-07-16T02:09:44+08:00
draft: false
---
# Hugo Building

## The setup process of Hugo.

### Windows

#### 1.[Hugo releases](https://github.com/gohugoio/hugo/releases)

#### 2.hugo new site ******<!-- myblog name -->

#### 3.cd ******<!-- root -->

#### 4.[Themes:](https://themes.gohugo.io/)

#### 5.hugo server -t themename --buildDrafts

&nbsp;&nbsp;&nbsp;&nbsp;https://localhost:1313

#### 6.hugo new post/blog.md&nbsp;&nbsp;[content]

#### 7 git operation:
$ hugo --theme=casper --baseUrl="http://marginlon.github.io" --buildDrafts

$ cd public

$ git init

$ git add .

$ git commit -m "提交信息"

$ git remote add origin https://github.com/MarginLon/marginlon.github.io

$ git push -u origin master
