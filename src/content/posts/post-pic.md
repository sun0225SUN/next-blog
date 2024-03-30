---
title: "使用 Flask 快速构建豆瓣图书/电影海报 WebAPI"
description: "新年新气象，最近一直在折腾新博客，准备好好装修一番"
pubDate: "2023-01-09"
categories: ['实用教程']
---

<!-- heroImage: "https://files.sunguoqi.com/images/202312091441958.webp" -->

新年新气象，最近一直在折腾新博客，准备好好装修一番。

在 [旧站](https://gh.sunguoqi.com/books) 中，有一个**豆瓣图书/电影**的展示页面，感觉还不错。

于是就想在新网站中也加入该元素，另一方面也可以促进自己**多阅读**，**多观影**。<br/>

<img src="https://files.sunguoqi.com/images/202312091442060.webp" />

## 一、初步探索

emmmm，怎么引入呢？直接开发插件？还没学会 halo 的插件如何开发❌

先去 GitHub 上搜搜，看看有没有相关的项目吧？好主意✅

于是便找到了该仓库 [传送门](https://github.com/sadjjk/DoubanPoster)

<img src="https://files.sunguoqi.com/images/202312091442763.webp" />

仓库已经是三年前创建的了，先看看代码可不可以正常跑吧！

果然。。。有 Bug，哈哈哈！

<img src="https://files.sunguoqi.com/images/202312091443113.webp" />

## 二、解决 Bug

打印个状态码，先初步诊断一下，看看 Bug 到底出在哪？

<img src="https://files.sunguoqi.com/images/202312091444281.webp"/>

运行一下！

<img src="https://files.sunguoqi.com/images/202312091445914.webp" />

<strong>418</strong>，还是第一次碰到这个状态码，<strong>Google 一下！</strong>

<img src="https://files.sunguoqi.com/images/202312091445494.webp" />

<img src="https://files.sunguoqi.com/images/202312091445751.webp" />

我是一个茶壶，哈哈哈，IT 技术充满了乐趣。

<img src="https://files.sunguoqi.com/images/202312091446934.webp" />

阿这，不太理解。。。前辈虽然写了`UA列表`，但是在请求的时候竟然不加到`headers`里去，怪不得豆瓣检测出来你是个爬虫，哈哈。

纠正一下吧！

<img src="https://files.sunguoqi.com/images/202312091446486.webp" />

完美运行啦！

<img src="https://files.sunguoqi.com/images/202312091447411.webp" />

<img src="https://files.sunguoqi.com/images/202312091447491.webp" />

但是。。。

## 三、新的需求

每分享一个书籍/电影都要运行此代码生成海报？

那为啥不干脆直接开发个接口，只要像下面这样引入代码就可以直接调用了呢？

```markdown
![](https://douban.sunguoqi.com？params= DOUBANURL)
```

## 四、技术探索

需求存在，开始探索实现方案。

将 Python 脚本做成 API？

只需要创建一个 Web 应用就可以啦。当用户附带正确的参数访问指定路由，就可以触发相应逻辑，最后返回数据。

那用什么技术来编写这个 Web 应用呢？

啊哈，有现成的 Web 框架，比如 Spring Boot，Django，Flask ...

`Spring boot`？

JavaWeb 那一套，对 Java 不熟，还没实际开发过，上手应该有点小困难❌

`Django`？

Django 自学过一段时间，比较容易上手，但 Django **“太健全了”**，内置后台，数据库 ORM 映射，模版机制，表单处理，会话...，用在这个脚本上会不会略显笨拙，感觉有点大材小用了⏱️

`Flask`？

听说 Flask 比较轻量，看看官网，好家伙，五行输出 **hello world**，我看行，就它了✅

<img src="https://files.sunguoqi.com/images/202312091448253.webp" />

## 五、正式开发

### 1、失败尝试

本来想在`Windows`上用`VScode`开发好后再上传到服务器上来着，奈何配置开发环境就配置了好长时间。

一是在写入`Flask_App`到`Windows`系统环境变量时遇到了问题，二是在`VSCode`上运行`Flask`出现了问题。。。

算了，不配了，直接上服务器。

<img src="https://files.sunguoqi.com/images/202312091448864.webp" />

### 2, Hello world

在`Ubuntu`上轻松配置好了环境，然后敲入代码（复制粘贴）

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```
你好，世界！就是这么优雅🎉

<img src="https://files.sunguoqi.com/images/202312091448535.webp" />

### 3、编写路由逻辑

经过一番猛如虎的操作后，我在原代码中加入了如下代码，于是大功告成！

```python
...
import flask
from flask import send_file

def main(url):
    ...
    return api_img_path

@app.route('/',methods=['get'])
def img():
    url = flask.request.args.get('url')
    img = main(url)

    return send_file(img)
```

<img src="https://files.sunguoqi.com/images/202312091449847.webp" />

<img src="https://files.sunguoqi.com/images/202312091449813.webp" />

当然，其实在此期间还经历了一番猛如虎的调试过程🥹

<img src="https://files.sunguoqi.com/images/202312091449225.webp" />

<img src="https://files.sunguoqi.com/images/202312091450044.webp" />

## 六、大功告成

**Github: https://github.com/sun0225SUN/DoubanPoster**

<img src="https://files.sunguoqi.com/images/202312091451842.webp"/>


