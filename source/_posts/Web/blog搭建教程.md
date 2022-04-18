---
title: Hexo搭建blog
date: 2021-12-22 18:46:19
author: 奈何
tags: blog
categories: Web
---

<div align='center' ><font size='8'>Hexo搭建blog</font></div>

:smiley: [我的博客主页](https://naihexi.github.io/blog/) :smiley:

# 环境安装

## NodeJs

下载 [nodeJs](https://nodejs.org/en/)【下载12版本的，高版本会伴随一些小问题】

## npm

​	`npm`（ node package manager ）是`Node`的包管理工具，能解决NodeJS代码部署上的很多问题

## cnpm

​	`cnpm的`官方介绍是：cnpm是一个完整 `npmjs.org` 镜像，可以用此代替官方版本(只读)，同步频率目前为 **10分钟** 一次以保证尽量与官方服务同步。

​	由于`npmjs.org`的服务器在国外（即在“墙”外），国（墙）内开发者做项目的时候，很多“包”的下载速度极慢，在这种环境下阿里巴巴为了众多开发者的便捷而出推出了淘宝镜像（即cnpm），它把`npm`官方的“包”全部搬到国内。

### 配置

```bash
# 临时使用
npm --registry https://registry.npm.taobao.org install [依赖的名称]
# 持久使用（慎用）
npm config set registry https://registry.npm.taobao.org
# 检查是否配置成功
npm config get registry
```

**安装cnpm（推荐）**

​	不会影响npm命令，又不用每次都写淘宝地址进行依赖包的安装

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### 使用

```bash
# 安装模块
cnpm install [name]
# 同步模块
cnpm sync connect
# 直接通过 web 方式来同步
open https://npm.taobao.org/sync/connect
# 支持 npm 除了 publish 之外的所有命令
cnpm info connect
```

# Hexo框架

​	[Hexo官网](https://hexo.io/themes/)

​	Hexo是一个基于 nodejs 的快速生成静态博客的开源框架，支持Markdown和大多数Octopress插件，一个命令即可部署到GitHub页面、Giteee、Heroku等，强大的API，可无限扩展，拥有数百个主题和插件。

## 安装

电脑中需要已安装Git、Node.js(6.9以上)

```bash
npm install hexo-cli -g
# 安装依赖包
npm i --save packageName
npm i --save-dev packageName
# 安装指定版本的包，版本号用@符号连接
npm i webpack@1.2.1
```

## 建站

```bash
# 初始化博客项目（最新版本已经可以在这一步安装依赖）
hexo init <目录名>
# 安装依赖
npm install hexo -g
# 升级
npm update hexo -g 
```

命令完成后的目录如下：

![img](https://naihexi.gitee.io/picgo/blog/init.png)

文件夹说明：

```
|-- demo//项目跟目录名
    |-- .gitignore//git时忽略的文件或目录
    |-- package-lock.json
    |-- package.json//应用程序的信息
    |-- _config.yml//网站的配置信息
    |-- scaffolds//模板文件夹，Hexo的模板是指在新建的markdown文件中默认填充的内容。
    |   |-- draft.md
    |   |-- page.md
    |   |-- post.md//博文模板
    |-- source//资源文件夹，存放用户资源
    |   |-- _posts//博文目录
    |       |-- hello-world.md//博文
    |-- themes//主题文件夹，Hexo 会根据主题来生成静态页面
        |-- landscape.//默认主题
            ...
```

此时`package.json`中内容如下：

[npm中package.json详解](https://www.cnblogs.com/zourong/p/5943224.html)

```json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.8.0",
    "hexo-generator-archive": "^0.1.5",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.1",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-renderer-marked": "^0.3.2",
    "hexo-server": "^0.3.3"
  }
}
```

### 修改配置

url：网站地址，必须修改，此处博文是托管在github上，故此使用[http://youname.github.io](https://links.jianshu.com/go?to=http%3A%2F%2Fyouname.github.io) 格式作为网站名字

language：语言，设置中文，根据需要修改，中文为`zh-CN`
 注意：配置值与配置名需要隔一个空格，否则会编译报错。

repo：部署服务器仓库地址，https://gitee.com/RainNG/blog.git

```bash
# Site
title: 夜色微凉
subtitle: ''
description: '原谅我这一生放纵不羁爱自由'
keywords:
author: 夜色微凉
#language: en
language: zh-CN
timezone: ''

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
#url: http://example.com
url: https://rainng.gitee.io/blog
root: /blog
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: https://gitee.com/RainNG/blog.git
  branch: master
```

### 修改post

修改 **scaffolds/post** 文件，追加一行【为了我们创建博客的时候可以给文章添加分类】

```bash
title: {{ title }}
date: {{ date }}
tags:
# 追加内容
categories:
```

## 常用指令

### 启动服务

```bash
# 1、Hexo 会监视文件变动并自动更新，除修改站点配置文件外,无须重启服务器,直接刷新网页即可生效。
hexo s
hexo server
# 2、以静态模式启动
hexo server -s
# 3、更改访问端口 (默认端口为4000，'ctrl + c'关闭server)
hexo server -p 5000
# 4、自定义 IP
hexo server -i IP地址
```

### 新建文章

```bash
# 1、新建一篇文章
hexo n "我的第一篇文章"
hexo new "我的第一篇文章" 
# 2、新建一篇文章,文章名称和标题分别为bbb.md 和 bbb. 文章采用aaa布局, 此时会在站点根目录下：source/_posts/，生成bbb.md文件,如下：
	#	---
	#	layout : aaa（post）
	#	title:
	#	date:
	# 	---
# 使用---分割的区域叫做“Front-matter”，用于指定这篇博文的变量，可手动修改
hexo new aaa "bbb"
```

手动修改`Front-matter`：

```bash
---
layout:
title: my first blog
date: 2019-05-11 16:20:56
updated:
comments:
tags:
- introduction
- hexo
categories:
- Diary
---
```

文章头配置选项：

| 配置选项   | 默认值                         | 描述                                                         |
| :--------- | :----------------------------- | :----------------------------------------------------------- |
| title      | `Markdown` 的文件标题          | 文章标题                                                     |
| date       | 文件创建时的日期时间           | 发布时间，应保证全局唯一                                     |
| author     | 根 `_config.yml` 中的 `author` | 文章作者                                                     |
| img        | `featureImages` 中的某个值     | 文章特征图                                                   |
| top        | `true`                         | 文章是否置顶，值为 `true`，则会作为首页推荐文章              |
| cover      | `false`                        | 是否需要加入到首页轮播封面中                                 |
| coverImg   | 无                             | 该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片 |
| password   | 无                             | 文章阅读密码，该值必须是用 `SHA256` 加密后的密码，防止被他人识破。 |
| toc        | `true`                         | 是否开启 TOC，可以针对某篇文章单独关闭 TOC 的功能。          |
| mathjax    | `false`                        | 是否开启数学公式支持                                         |
| summary    | 无                             | 文章卡片摘要显示的文字，如果无值程序会自动截取文章的部分内容作为摘要 |
| categories | 无                             | 文章分类，建议一篇文章一个分类                               |
| tags       | 无                             | 文章标签，一篇文章可以多个标签                               |

### 生成静态文件

```bash
# 生成静态网页 (执行 $ hexo g后会在站点根目录下生成public文件夹, hexo会将"/blog/source/" 下面的.md后缀的文件编译为.html后缀的文件,存放在"/blog/public/ " 路径下)
hexo g
hexo generate
# 文件生成后立即部署网站
hexo generate -d
hexo generate --deploy
# 监视文件变动
hexo g -w
```

### 部署网站

#### 安装部署插件deployer

```bash
npm install hexo-deployer-git --save
# or
cnpm install --save hexo-deployer-git
```

#### 修改配置

```bash
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy: 
  type: git
  repo: https://gitee.com/RainNG/blog.git
  branch: master
  message: publish blog
```

#### 部署指令

```bash
# 将本地数据部署到远端服务器(如github)
hexo d
hexo deploy
# 部署之前先生成静态文件
hexo deploy -g
hexo deploy --generate
```

#### 部署问题

1.  本地与部署pages服务页面不一致

​	本地使用静态文件，发布用的是cdn，浏览器保存了之前的数据，需清除浏览器缓存后再强制刷新：

​	如FireFox 重新载入（忽略缓存）： Ctrl + F5



### 发表草稿

```bash
hexo p
hexo publish
# 通过 publish 命令将草稿移动到 source/_posts 文件夹,草稿默认是不会显示在页面中的，可在执行时加上 --draft 参数，或是把 render_drafts 参数设为 true来预览草稿。
hexo publish [layout] <title> 
```

### 清除缓存

```bash
# 清除缓存 ,网页正常情况下可以忽略此条命令,执行该指令后,会删掉站点根目录下的public文件夹和 db.json
hexo clean
```

### 查看

```bash
node-v #查看node.js版本号
npm -v #查看npm版本号
hexo -v #查看hexo版本号
hexo list	#列出网站资料
```

## 主题配置

​	如果不想使用默认的主题，也可以下载一个新的主题，放在themes目录下，并修改 _config.yml 内的 theme 设定，即可切换主题。

Hexo 官网主题页：[themes](https://hexo.io/themes/)

Github 官网搜索`hexo-theme`，选择`All GitHub`

### 安装主题渲染插件

​	在hexo站点目录(非主题目录)下安装 **hexo-renderer-sass** 和 hexo-renderer-scss：

**注意**：不安装这两个插件，更换主题打开页面时，图片等布局可能异常。

```bash
# 1、将.scss样式文件渲染成最后的style.css文件
cnpm install hexo-renderer-sass --save
cnpm install hexo-renderer-scss --save
# or 推荐
npm install -g yarn	# 安装
yarn add hexo-renderer-sass
yarn add hexo-renderer-scss
# 2、
cnpm install hexo-generator-json-content --save
```

### 下载主题

以next主题为例：[next使用教程](https://links.jianshu.com/go?to=http%3A%2F%2Ftheme-next.iissnan.com%2Fgetting-started.html)

1.  在themes目录下克隆next主题

```bash
# snippet 主题，安利
git clone git://github.com/shenliyang/hexo-theme-snippet.git themes/hexo-theme-snippet
# gal 主题
git clone https://github.com/ZEROKISEKI/hexo-theme-gal.git themes/gal
# next 主题
git clone https://github.com/theme-next/hexo-theme-next themes/next
# Butterfly 主题
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/Butterfly
```

### 更换主题

 修改配置文件 _config.yml ：

```bash
## Themes: https://hexo.io/themes/
theme: gal

# 末尾追加
jsonContent:
  dateFormat: MM-DD
  pages:
    title: true
    text: true
    path: true
    date: true
    excerpt: true
    preview: true
  posts:
    title: true
    text: true
    path: true
    date: true
    excerpt: true
    tags: [{
      name: tag.name,
      slug: tag.slug,
      permalink: tag.permalink
    }]
    preview: true
```

### 开启页面功能

```bash
# 开启页面功能
hexo new page "search"	# 开启搜索功能
hexo new page "404"		# 配置错误页面
hexo new page "tags"
hexo new page "categories"
hexo new page "about"
```

重新hexo clean,hexo g，hexo s，就可以更新主题。

## 常用主题插件

### GitHub使用Gitalk

[网站配置Gittalk](https://blog.csdn.net/wyounger/article/details/111356242)

[gitalk授权时403处理](https://blog.csdn.net/deep_learn/article/details/123843774)

# Markdown

​	Hexo 默认是使用 Markdown 格式的文件的，所以在写新博客之前，要先了解一下 Markdown 语法 。

## Typora

​	Typora 是一款支持实时预览的 Markdown 文本编辑器，所见即所得，好用免费（推荐）。

​	下载地址：[Typora中文网](https://www.typora.net/)

​	Markdown 使用请参考下面这篇文章。

# 辅助工具

## PicGo

​	`偏好设置 -> 图像 -> 上传服务设定`，配置PicGo。

​	PicGo 是一位中国开发者基于 electron-vue 开发的用于快速上传图片并获取图片 URL 链接的开源工具，GitHub主页：[PicGo](https://github.com/Molunerfinn/PicGo)

​	PicGo 本体支持七牛云、腾讯云、又拍云、阿里云、SM、Imgur、GitHub等图床，Gitee图床需安装插件（PicGo 插件设置中直接搜索Gitee，然后选择一个安装即可）。

​	**图床**，即提供外链访问的图片存储服务器。可以在GitHub或Gitee中创建一个仓库作为图床。	

​	Typora 配合可以实现在文章中插入图片时自动上传并替换为链接内容，已Gitee为例：

1.  获取 repo tokens

​	这个 token 主要用于让 PicGo 有权限往Git服务器仓库 push 代码(图片)。

​	点击 头像 -> 设置 -> 私人令牌

​	新建令牌，编辑描述（用于PicGo上传图片），生成，复制保存（此字符串只会出现一次，点击其他页面后就无法再查看了，需要重新创建）。

2.  配置PicGo：

​	打开 PicGo ,选择`图床设置`，选择`Gitee图床`（已安装Gitee图床插件），填写参数：

-   **repo**，填写格式为用户名/仓库名（如 https://gitee.com/RainNG/picgo.git 填写 RainNG/picgo）
-   **branch**，填写默认分支master或者main
-   **Token**，填写上一步获取的 token 值
-   **path**，选填，可以自定义名称，比如用年月来分类，不填图片会上传在仓库根目录。
-   **customPath**，这个会在上一个参数的基础上再创建一层子文件夹用于按年、年月或年季来分类保存。
-   **customUrl**，用于修改返回的 url 前缀，不填则返回原始 url。解决`文件大于1M，登录后可见`的问题需要更改此项。

 3.    解决"文件大于1M，登录后可见"问题

       ​	如果上传的图片大于 1M ，不管是在 Typora 中还是在浏览器网页中，是无法加载出图片的。

       ​	博客仓库打开 Gitee Pages 功能，其他人就可以访问博客仓库里的博客了，图床仓库也一样，打开它的 Gitee Pages 功能，无需登陆就可以访问里面的图片了。打开图片仓库的Pages功能，然后复制 url 到 customUrl 即可解决。

       

>   ​	对于`GitHub图床`，`图床设置`与Gitee基本相同，只是自定义域名配置需求不同：
>
>   ​	`设定自定义域名`，用于修改返回的 url 前缀，不填则返回原始 url。配置CDN加速需要更改此项。
>
>   **CDN 加速(jsDelivr)**
>
>   ​	CDN的全称是(Content Delivery  Network)，即内容分发网络。其目的是通过在现有的Internet中增加一层新的CACHE(缓存)层，将网站的内容发布到最接近用户的网络”边缘“的节点，使用户可以就近取得所需的内容，提高用户访问网站的响应速度。
>
>   ​	[jsDelivr CDN 官网](https://www.jsdelivr.com/)， jsDelivr 支持 npm、GitHub、WordPress三个站点的加速。
>
>   ​	原始图片地址格式：`https://raw.githubusercontent.com/用户名/仓库名/分支名/目录/图片名.png`
>
>   ​	更改后的图片地址格式：`https://cdn.jsdelivr.net/gh/用户名/仓库名@分支名/目录/图片名.png`
>
>   ​	即修改GitHub图床设置的自定义域名为`https://cdn.jsdelivr.net/gh/用户名/仓库名@master`。

# 参考

​	感谢各位大大的文章，如有侵权，请联系删除。

1.  [从零开始搭建自己的个人博客](https://blog.csdn.net/qijing19991210/article/details/121733409?utm_medium=distribute.pc_feed_v2.none-task-blog-hot_rank_bottoming-13.pc_personrecdepth_1-utm_source=distribute.pc_feed_v2.none-task-blog-hot_rank_bottoming-13.pc_personrec)
2.  [从零开始免费搭建自己的博客](https://blog.csdn.net/yushuaigee/article/details/111465155?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-3.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-3.nonecase)

