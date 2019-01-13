---
title: 解决Jekyll中NexT主题的localsearch报错问题
description: 昨天部署好了自己的博客后，发现在使用localsearch报错，通过查问题发现是浏览器解析search.xml出现了问题
categories:
 - 环境搭建
tags:
 - Github Pages
 - Jekyll
 - 疑难杂症
 - Jekyll Theme
 - NexT Theme
---

# 问题现象
昨天部署好了自己的博客后，发现在使用localsearch报错，通过查问题发现是浏览器解析search.xml出现了问题。

具体错误如下：
```xml
<parsererror style="display: block; white-space: pre; border: 2px solid #c77; padding: 0 1em 0 1em; margin: 1em; background-color: #fdd; color: black">
    <h3>This page contains the following errors:</h3>
    <div style="font-family:monospace;font-size:12px">
    error on line 32 at column 37: Input is not proper UTF-8, indicate encoding !
    Bytes: 0x08 0x67 0x69 0x74
    </div>
    <h3>Below is a rendering of the page up to the first error.</h3>
</parsererror>
```

# 解决方法

本地打开markdown文件发现，有一些控制字符，导致其解析出错；问题找到了，思路也就出来了，有两种方式：第一个方式是把xml中的控制字符修改掉(修改 ` /search.xml ` 或者修改` /_includes/third_party/search/localsearch.html `)，另一个是把搜索数据源由xml格式改为json格式；详细介绍第二种修改数据源的方式。

## localsearch的数据源由xml改为json
1. 打开 ` /_config.yml ` ，在添加如下配置：
```yaml
search:
  path: search.json
```
2. 在根目录下新建` search.json `, 内容如下:
```json
---
layout: null
sitemap: false
---
[{% for post in site.posts %}
  {
    "title": {{ post.title | smartify | strip_html | jsonify }},
    "url" : {{ post.url | relative_url | jsonify }},
    "content" : {{ post.content | smartify | strip_html | strip_newlines | jsonify }}
  }{%- unless forloop.last -%},{%- endunless -%}
  {% endfor %}
]
```
3. 重启Jekyll，此问题解决
