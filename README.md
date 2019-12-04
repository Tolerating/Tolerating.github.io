> 当前分支用来保存我的博客的源码

下载到本地后执行下列命令:

* `npm install`          安装插件



# 写博客

写好的博客放在`source/_posts/`下

```
---
title: vue.js2.0学习(一)——基础       //文章标题
date: 2013/7/13 20:46:25		   //创建时间
comments: false						//是否可以评论
tags:								//文章标签
- vue2.0
categories:							//文章分类
- 前端开发
---
```



# 生成博客页面

`package.json`文件中定义了`hexo`命令的`npm`方式

`npm run build` 等于 `hexo generate`



生成的博客页面会放在`public`文件夹里面



# 清空public文件夹

`hexo clean`



# 运行在本地服务器上

`hexo server`



# 发布到代码管理平台

`hexo server`

