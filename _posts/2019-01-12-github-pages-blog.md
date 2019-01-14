---
title: 搭建基于github pages的博客
description: 搭建基于github pages的博客， github上新建用户仓库  1.申请github账号（忽略）2.新建 “你的账号.github.io”仓库
categories:
 - 环境搭建
tags:
 - Github Pages
 - Jekyll
---


# github上新建用户仓库
1. 申请github账号（忽略）
2. 新建 “你的账号.github.io”仓库

# 安装 Jekyll(非必须)

## 安装ruby

```shell
xcode-select --install
gem install --user-install bundler jekyll
```

## 设置环境变量

把 ` export PATH="$HOME/.gem/ruby/2.3.0/bin:$PATH" ` 添加到 ` ~/.bash_profile ` 文件最后一行，然后执行 ` ~/.bash_profile ` 以便生效

```shell
source ~/.bash_profile
```

 详细步骤  参考 [https://jekyllrb.com/docs/installation/macos/](https://jekyllrb.com/docs/installation/macos/)

#   运行 HelloWord

## 克隆github上的 仓库到本地
```shell
git clone https://github.com/你的账号/你的账号.github.io.git
```

## 初始化jekyll工作目录

切换到刚刚检出的github仓库目录下，  执行：
```shell
jekyll new myblog
mv myblog/* ./ 
rm -rf myblog
```

## 启动jekyll本地服务

```shell
bundle exec jekyll serve
```
此时可以使用浏览器访问 [http://localhost:4000](http://localhost:4000)

# 编写博客内容

自己博客内容都放在 `_posts` 文件夹中，可以是markdown也可以是html文件，可以试着修改一个试试。

# 使用第三方主题

 可以根据自己的喜好去找个主题样式，让博客更加漂亮，随便搜到几个，仅 供参考。
- [https://github.com/topics/jekyll-theme](https://github.com/topics/jekyll-theme)
- [http://jekyllthemes.org](http://jekyllthemes.org)

