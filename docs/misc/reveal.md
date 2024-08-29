# reveal-md 编写 Slides

!!! info
    本篇文章适用于不想使用Powerpoint但是拥有展示需求的人。

## 为什么我放弃了PPT而选择了reveal-md

> [再见PPT，你好“文档演示模式”](https://www.yuque.com/yuque/blog/nxe6vv?view=doc_embed)

在大一的这段时间里，我一度因为PPT中各种繁琐的功能而浪费了大把时间。换句话说，PPT有太多太多展示需求之外的功能，页面不够简介，使用太过繁琐。此外，PPT对于接受者的设备也有要求：

- 接受者的电脑里必须有Powerpoint软件，否则预览时会出现各种问题
- 双方的Powerpoint版本要求基本一致，否则会不兼容
- 上台展示时需要用U盘拷贝或者在展示用电脑上登录自己的微信等等，不方便

而reveal-md没有这些缺点。我们只需要写一个md文档，make一下，最后上传到github上就完成了。在展示用电脑上输入`<...>.github.io/site/index.html（示例）`就可以展示了。

## 原始reveal-md安装

我并没有研究如何裸使用reveal-md，想了解的可以移步isshikih修的笔记：
> [isshikih修的笔记](https://note.isshikih.top/others/reveal-md2Slides/#%E5%AE%89%E8%A3%85%E4%B8%8E%E6%BC%94%E7%A4%BA)

## Tonycrane的模板

xg的模板让这个slides的美工直接顶到了天花板。

!!! notice
    首先确保你能使用npm！

在终端中输入如下命令：
```shell
npm install -g reveal-md
```
这样你就下载了reveal-md。

接下来可以使用他的模板了。这里贴出他的示例以及项目网址：

>[预览](https://slides.tonycrane.cc/RevealmdTemplate)

>[xg的slides模板](https://github.com/TonyCrane/slide-template)

## 生成网页链接

创建一个github仓库，将文件打包进去，开启github-pages部署就可以啦！这样你就可以访问(github-pages的网址)/site/index.md来演示了！

### 自定义域名
如果你有自己的域名，可以将github-pages的网址解析到你自己的域名。先在代理商那里创建一个CNAME条目到github-pages的网址。然后在仓库的根目录创建一个CNAME文件，写入你的域名，在pages里面设置下就好了。

如果你想省略后面的/site/index.md，可以在根目录下创建一个index.html，放入以下代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta http-equiv="refresh" content="0;url=site/index.html">
    <title>Redirecting...</title>
</head>
<body>
    <p>If you are not redirected automatically, follow this <a href="site/index.html">link to site/index.html</a>.</p>
</body>
</html>
```
这样就可以跳转到/site/index.md了。