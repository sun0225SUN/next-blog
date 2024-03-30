---
title: "快速上手，教你如何将 ChatGPT 接入到微信公众号"
description: "使用 OpenAI API 和 WeRobot 搭建一个简单的机器人"
pubDate: "2023-1-29"
categories: ['实用教程']
---

<!-- heroImage: "https://files.sunguoqi.com/images/202311220232967.webp" -->

## 成果演示

### 基础问答

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250121850.webp"/>
{% endfolding %}

### 代码解读

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250122187.webp"/>
{% endfolding %}

### 代码转换

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250122303.webp"/>
{% endfolding %}

### 错误修正

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250122231.webp"/>
{% endfolding %}

### 情感分析

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250123269.webp"/>
{% endfolding %}

### 项目分类

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250123372.webp"/>
{% endfolding %}


### 名字生成器

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250123039.webp"/>
{% endfolding %}


### 时间复杂度计算

{% folding, 查看详情 %}
<img src="https://files.sunguoqi.com/images/202311250124645.webp"/>
{% endfolding %}

## 友情提示

本教程假定您已经拥有以下资源

- 一个微信公众号
- 一个 OpenAI 账号
- 一台可访问外网的服务器
- 一个域名 (最好有，没有也可以)

您最好已经掌握以下技能

- Python 编程基础
- 一定的 Web 开发及服务端运维经验

## OpenAI API

在本节，您将学会如何使用 Python 来调用 OpenAI API。

### 新建一个 Python 项目

使用 PyCharm 或其他集成开发环境创建一个 Python 项目。

<img src="https://files.sunguoqi.com/images/202311250132445.webp"/>

### 新建一个 API key

[Account API Keys - OpenAI API](https://beta.openai.com/account/api-keys)

点击上方链接创建一个密钥，保存此密钥以便后续使用。

<img src="https://files.sunguoqi.com/images/202311250133137.webp"/>

### 安装 openai 依赖

在 Pycharm 中打开本地终端并输入以下命令安装 openai 依赖包。

```bash
pip install openai
```

#### 安装失败

请确保您的电脑可以正常访问境外网络，否则可能会安装失败。

<img src="https://files.sunguoqi.com/images/202311250133200.webp"/>

#### 安装成功

<img src="https://files.sunguoqi.com/images/202311250133044.webp"/>

在终端中输入以下命令查看**openai**依赖包是否已经安装成功。

```bash
pip list
```

终端输出如下（示例）。

```txt
aiohttp            3.8.3
aiosignal          1.3.1
async-timeout      4.0.2
attrs              22.2.0
certifi            2022.12.7
charset-normalizer 2.1.1
colorama           0.4.6
frozenlist         1.3.3
idna               3.4
multidict          6.0.4
openai             0.26.4
pip                22.3.1
requests           2.28.2
setuptools         65.5.1
tqdm               4.64.1
urllib3            1.26.14
wheel              0.38.4
yarl               1.8.2
```


### 查看示例应用

[Examples - OpenAI API](https://beta.openai.com/examples)

打开上方链接，查看 OpenAI 官网所列出的示例应用，此页面包含了 ChatGPT 的主要应用场景。

<img src="https://files.sunguoqi.com/images/202311250134339.webp"/>

以最简单的问答应用为例，点击**Q&A**后弹出如下界面，之后点击**Open in Playground**按钮。

<img src="https://files.sunguoqi.com/images/202311250134892.webp"/>

点击**View code**查看本应用的示例代码。

<img src="https://files.sunguoqi.com/images/202311250134886.webp"/>

复制此代码并粘贴至项目文件**main.py**中。

<img src="https://files.sunguoqi.com/images/202311250135412.webp"/>

### 本地调试

基于示例，修改后的代码如下，记得修改**api_key**的值。

```python
import os  
import openai  
  
# openai.api_key = os.getenv("OPENAI_API_KEY")  
openai.api_key = "sk-6mWGxEw**************NqKWDXWRRaLxXAPxfEmO"  
  
response = openai.Completion.create(  
    model="text-davinci-003",  
    prompt="Python 是这个世界上最好的语言吗？",  
    temperature=0,  
    max_tokens=1000,  
    top_p=1,  
    frequency_penalty=0,  
    presence_penalty=0,  
    # 此参数定义了您的问题终止符 
    # stop=["\n"]   
)  
  
print(response)
```

运行该程序，控制台输出如下。

```txt
{
  "choices": [
    {
      "finish_reason": "length",
      "index": 0,
      "logprobs": null,
      "text": "\n\n\u4e0d\u662f{此处省略部分字符}\u3002Python\u662"
    }
  ],
  "created": 1674910885,
  "id": "cmpl-6df7dn3shXPJwGmpeTQotLwBW9cPw",
  "model": "text-davinci-003",
  "object": "text_completion",
  "usage": {
    "completion_tokens": 99,
    "prompt_tokens": 26,
    "total_tokens": 125
  }
}

进程已结束，退出代码 0
```

`text`即为我们问题的答案，在**main.py**加入下面这行代码。

```python
print(response.choices[0].text)
```

重新运行此脚本，程序运行结果最终如下。

<img src="https://files.sunguoqi.com/images/202311250140641.webp"/>

### 代码解读

各参数的含义请查阅官方文档：[API Reference - OpenAI API](https://beta.openai.com/docs/api-reference/completions/create)

本程序的代码逻辑比较简单，请读者自行理解。


## WeRoBot

WeRoBot 项目地址：[WeRoBot 是一个微信公众号开发框架](https://github.com/offu/WeRoBot)

在本节，您将使用**WeRoBot**框架创建一个**Hello World**程序。

当您的公众号后台收到用户发来的消息时，程序会自动调用并发送**Hello World**，如下图所示。

<img src="https://files.sunguoqi.com/images/202311250139832.webp"/>

### 安装 werobot 依赖

使用**ssh**工具打开服务器终端并输入以下命令。

```bash
pip install werobot
```

### 新建 Python 脚本

```bash
touch hello.py
```

使用**Vim**打开**hello.py**文件，复制以下内容后保存。

```python
import werobot

robot = werobot.WeRoBot(token='tokenhere')

@robot.handler
def hello(message):
    return 'Hello World!'

# 让服务器监听在 0.0.0.0:520
robot.config['HOST'] = '0.0.0.0'
robot.config['PORT'] = 520
robot.run()
```

### 运行该脚本

运行该脚本之前，请确保您服务器的`520`端口已开放。

输入以下命令运行此脚本。

```bash
python3 ./hello.py 
```

终端输出如下。

```bash
Bottle v0.12.23 server starting up (using AutoServer())...
Listening on http://0.0.0.0:520/
Hit Ctrl-C to quit.
```

### 服务测试

在浏览器中输入**http://{您服务器的公网ip}:{端口号}**访问此服务。

如果您看到如下界面，说明本服务已部署成功。

<img src="https://files.sunguoqi.com/images/202311250139445.webp"/>

### 反向代理

由于微信公众号的后台接口只支持**80**和**443**端口，故需要配置**Nginx 反向代理**。

<img src="https://files.sunguoqi.com/images/202311250139593.webp"/>

您可以使用**宝塔面板**或**Nginx Proxy Manager**配置反向代理，此处不做过多讲解。

当然，如果您服务器的**80**或**443**端口没有被占用的话，您可以直接将**werobot**运行在该端口下。

您只需要修改**hello.py**文件中该行代码**robot.config['PORT'] = 80/443**即可。

### 公众号配置

打开微信公众平台，[点我](https://mp.weixin.qq.com/)

在**设置与开发**选项卡中点击**基本配置**，输入您反向代理后的**域名**，设置您的**令牌**，消息加密点击**自动生成**，加密方式设置成**明文**。

请注意：这里的令牌必须和**hello.py**中的**token**保持一致。

```python
robot = werobot.WeRoBot(token='tokenhere')
```

<img src="https://files.sunguoqi.com/images/202311250138792.webp"/>

输入好配置后我们点击**提交**，然后**启用**该配置即可。

### Hello World !

不出意外的话，当用户在您的后台发送任何消息时，后台便会自动发送**Hello world`

### 数据转发原理

<img src="https://files.sunguoqi.com/images/202311250138991.webp"/>

如上图所示，当在微信公众号后台发送消息时，数据首先会发送到微信服务器上，如果公众号后台配置了接口信息，那么**微信服务器**便会将数据转发到**开发者服务器**。由**开发者服务器**做出响应，再经过**微信服务器**发送到微信公众号客户端。

## ChatGPT & WeRoBot

首先，恭喜您已经完成了上面两个小节的内容。

在本节，我们将会把 ChatGPT 和 WeRoBot  融合成一个脚本，当用户输入信息时，后台响应的不再是**Hello World`，而是经过 ChatGPT 处理后的结果。

### 编写代码

在服务器中新建**chatgpt.py**文件，并将以下代码复制到该文件中。

```python
import werobot
import openai

robot = werobot.WeRoBot(token='你的 Token')

openai.api_key = "你的 api_key"

def generate_response(prompt):
    response = openai.Completion.create(
        model = "text-davinci-003",
        prompt = prompt,
        max_tokens = 1000,
        temperature = 0.5,
        top_p = 1,
        frequency_penalty = 0.0,
        presence_penalty = 0.0,
    )
    message = response.choices[0].text
    return message.strip()


@robot.handler
def hello(message):
    return generate_response(message.content)

# 本程序将在 520 端口运行
robot.config['HOST'] = '0.0.0.0' 
robot.config['PORT'] = 520
robot.run()

```

### 进程管理

当我们关掉**ssh 会话**连接时，我们在此会话中运行的进程便会被杀死，如何解决这个问题呢？

这里推荐大家使用**Screen**对进程进行管理，常用命令如下。

```bash
安装：
	#CentOS系统安装命令
	yum install screen
 
	#Debian/Ubuntu安装命令
	apt-get install screen

创建：
	# 新建 screen
	screen -S your_screen_name

查看：
	# 查看 screen 列表
	screen -ls

进入：
	# 进入 screen
	screen -r xxx

删除：
	# 在当前screen下，输入Ctrl+D，删除该screen
	Ctrl+D

退出：
	# 在当前screen下，输入先后Ctrl+A，Ctrl+D，退出该screen
	Ctrl+A，Ctrl+D

杀死：
	# 删除指定screen, your_screen_name为待删除的screen name
	screen -S your_screen_name -X quit
```

### 运行服务

确保您服务器的**520**端口 (端口号以实际开发为准) 已开放，且没被占用。

在终端中输入以下命令，创建一个`screen`。

```bash
screen -S chatgpt
```

进入`screen`后，输入以下命令运行`chatgpt.py`即可。

```bash
python3 ./chatgpt.py
```


## 注意事项

### 科学上网

由于敏感原因，请确保您的电脑和服务器都可以正常访问境外网络。

### 账号注册

OpenAI 账号注册可参考此教程 [OpenAI ChatGPT 注册保姆级攻略，绝对有效 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/589642999)

### 微信公众号自定义菜单及关键词回复失效

由于我们使用了自定义的接口，便无法再使用官方提供的**自定义菜单**及**关键词回复**等功能。

二者功能实现可参考**WeRoBot**文档自行开发。

<img src="https://files.sunguoqi.com/images/202311250137197.webp"/>

<img src="https://files.sunguoqi.com/images/202311250137084.webp"/>


### 该公众号提供的服务出现故障，请稍后再试！

微信官方为了优化用户体验，对接口制定了如下规则：

> 微信服务器在五秒内如果收不到开发者服务器的响应便会主动断掉连接，并且重新发起请求，总共重试三次。

此规则会对本程序带来一定的限制，如果用户输入的文本较为复杂或者 ChatGPT 较难处理的话，服务器的响应时间通常会超过 5s，客户端便会收到**该公众号提供的服务出现故障，请稍后再试**的消息。

未认证的公众号暂时无法突破此限制（已认证的公众号可以采取被动模式接收消息，待程序处理完成后使用主动模式进行发送消息的方法突破此限制）。

对于用户而言，建议您采用**英语**进行提问，并且**精炼**您的语言，以避免 ChatGPT 处理复杂文本而超时。