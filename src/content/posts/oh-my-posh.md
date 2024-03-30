---
title: "Oh My Posh | Windows Terminal 美化指南"
description: "简洁清爽的 IDE 主题，赏心悦目的代码配色，逼格拉满的 Terminal 终端，极致丝滑的码字体验，总是让人欲罢不能。"
pubDate: "2023-07-15"
categories: ['实用教程']
---

<!-- heroImage: "https://files.sunguoqi.com/images/202311220244903.webp" -->

作为一名"爱码士"，那必然是爱屋及乌，简洁清爽的 IDE 主题，赏心悦目的代码配色，逼格拉满的 Terminal 终端，极致丝滑的码字体验，总是让人欲罢不能。

在 Windows 系统中，我们最常使用的 Shell 工具莫过于 PowerShell 了。虽然它真的很 Power，但纯天然的颜值还是稍显逊色，如何拥有更加 beautiful 的 PowerShell 呢？

<img src="https://files.sunguoqi.com/images/202311250146674.webp">

## Windows Terminal

Windows Terminal 是一个集成了多个命令行环境的终端应用程序。

在 Windows Terminal 下，我们可以同时使用 PowerShell、命令提示符（Command Prompt）和 Windows Subsystem for Linux（WSL）等多种命令行工具。

安装 Windows Terminal 方法也比较简单，我们直接打开 Microsoft Store 下载安装即可。

<img src="https://files.sunguoqi.com/images/202311250147264.webp">

Windows Terminal 提供了许多功能和特性，包括多标签页支持、自定义主题、快速启动、分屏布局、Unicode 字符支持、GPU 加速等。它还支持使用不同的配置文件来定义每个命令行环境的外观和行为。

PowerShell 美化第一步，我们可以直接在 Windows Terminal 中个性化修改它的外观。

<img src="https://files.sunguoqi.com/images/202311250147174.webp">

## Oh My Posh

除了在 Windows Terminal 中个性化修改 PowerShell 的外观，我们还可以使用 [Oh My Posh](https://ohmyposh.dev/)来进一步的美化 PowerShell。

<img src="https://files.sunguoqi.com/images/202311250147163.webp">

#### 什么是 Oh My Posh

Oh My Posh 是一个开源的命令行提示工具，用于美化和定制命令行提示符（prompt）。

Oh My Posh 提供了丰富的主题和配置选项，可以让用户根据自己的喜好和需求来定制命令行提示符的外观和行为。它支持自定义图标、颜色、字体和布局等，使命令行提示符更具个性化和可读性。

使用 Oh My Posh，你可以在命令行提示符中显示有用的信息，如当前路径、Git 分支、Python 虚拟环境、操作系统信息等。它还提供了各种内置的模块和函数，可用于创建自定义的提示符元素和动态内容。

#### 安装 Oh My Posh

安装 Oh My Posh 的方法有多种，在 Windows 中，你可以直接在 Microsoft Store 获取它。

<img src="https://files.sunguoqi.com/images/202311250148937.webp">

#### 使用 Oh My Posh

Oh My Posh 安装成功后，Windows Terminal 并不会默认使用 Oh My Posh 来加载 PowerShell。还需要我们进行以下配置。

在命令行中输入`$profile` 查看 powerShell 的配置文件路径。在该目录下新建`Microsoft.PowerShell_profile.ps1`文件，填入以下内容即可。



```text
oh-my-posh init pwsh | Invoke-Expression
```


#### 安装 Nerd Fonts

Oh 
My Posh 配置成功后，我们重新打开 Windows Terminal 会发现输入提示出现了乱码。

这是因为我们目前终端正在使用的字体不支持图标导致的。我们需要安装 Nerd Fonts 字体。

打开 [Nerd Fonts](https://www.nerdfonts.com/font-downloads) 字体的下载地址，选择我们自己喜欢的字体下载安装即可，这里我选择的字体是`Hack Nerd Font`


<img src="https://files.sunguoqi.com/images/202311250148284.webp">

#### 使用 Nerd Fonts

Nerd 字体安装成功后，我们需要把终端的使用字体配置为我们下载的 Nerd 字体。

打开 Windows Terminal，使用快捷键 `Ctrl+Shift+,` 打开 Windows Terminal 的配置文件。

在 profiles 中加入以下内容即可。

```json
"defaults": {
	"font": {  
		"face": "Hack Nerd Font"  
	}  
}
```


- "face" 对应的键值为你在 Nerd 中下载的字体名称，如 "Hack Nerd Font" 
- 如果你曾经在 Windows Terminal 单独给 PowerShell 设置过字体，你可以将 PowerShell 的字体配置注释掉或直接修改 PowerShell 的字体配置。

>当然你也可以在 Windows Terminal 的图形界面中修改默认字体及 Powershell 的使用字体。

<img src="https://files.sunguoqi.com/images/202311250148578.webp">

配置好字体后重新打开终端，就可以看到我们美化后的效果啦。

<img src="https://files.sunguoqi.com/images/202311250148611.webp">

#### 选择主题

Oh My Posh 官方提供了许多开箱即用的主题供我们选择。

访问下面的链接即可查看主题预览效果。

[https://ohmyposh.dev/docs/themes](https://ohmyposh.dev/docs/themes)

<img src="https://files.sunguoqi.com/images/202311250149788.webp">

#### 使用主题

在命令行中输入`Get-PoshThemes` ，在输出内容的最下面可以查看主题预设文件的路径。

在命令行中输入`notepad $profile` 命令打开 PowerShell 的配置文件，在配置文件中加入主题预设文件路径即可。格式为：

```bash
oh-my-posh init pwsh --config 'C:/Users/Posh/jandedobbeleer.omp.json' | Invoke-Expression
```

## 最终效果

- 在 VSCode 中同样需要配置 Terminal 的字体为 Nerd 字体才可以正常显示图标
- 在 Windows 中使用 neofetch 命令的教程：[点我查看](https://www.makeuseof.com/how-to-install-and-use-neofetch-on-windows/)

<img src="https://files.sunguoqi.com/images/202311250149384.webp">

<img src="https://files.sunguoqi.com/images/202311250149895.webp">










