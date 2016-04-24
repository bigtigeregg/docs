# 云引擎快速入门

该文档帮助你快速的了解如何创建一个云引擎项目，本地开发调试，以及如何部署到云端。

## 创建项目

### 使用命令行创建项目

在本地创建项目需要使用 LeanCloud 官方命令行工具，请根据 [云引擎命令行工具使用详解-安装](https://leancloud.cn/docs/leanengine_cli.html#安装) 部分安装该工具，并确保你已经在本地机器上可以成功运行命令行工具：

```
$ lean -h
```
如果一切正常，你应该看到命令行工具的帮助信息。

使用命令行工具创建的项目模板是一个空项目：

```
$ lean new
```
然后根据提示输入相关信息即可。

### 从项目模板创建

从 Github 迁出示例项目，该项目可以作为一个你应用的基础：

```
$ git clone https://github.com/leancloud/node-js-getting-started.git
$ cd node-js-getting-started
```

然后添加应用 appId 等信息到该项目：

```
$ lean app add <appName> <appId>
```

以上两种方式创建的项目结构如下：


```
.
├── README.md
├── app.js
├── cloud.js
├── package.json
├── public
│   └── stylesheets
│       └── style.css
├── routes
│   └── todos.js
├── server.js
└── views
    ├── error.ejs
    ├── index.ejs
    └── todos.ejs
```


## 本地运行

首先在当前项目的目录下安装必要的依赖，执行如下命令行：

```
$ npm install
```

然后启动应用：

```
$ lean up
```


**提示**：命令行窗口可能会提示输入 Master Key，该信息可以在 [控制台 / 设置 / 应用 Key](/app.html?appid=#/key) 中找到。

<div class="callout callout-info">复制粘贴 Master Key 后，窗口不会有任何显示，直接按回车键确认即可。</div>

应用即可启动运行。

## 访问站点

打开浏览器访问 <http://localhost:3000> 会显示如下内容：

```
LeanEngine

这是 LeanEngine 的示例应用

当前时间：Mon Feb 01 2016 18:23:36 GMT+0800 (CST)

一个简单的「TODO 列表」示例
```

访问的页面在代码 `./app.js` 中定义：

```js
...
app.get('/', function(req, res) {
  res.render('index', { currentTime: new Date() });
});
...
```

### 新建一个 Todo

用浏览器打开 <http://localhost:3000/todos> ，然后在输入框输入 「点个外卖」并点击 「新增」，可以看到 Todo 列表新增加了一行。

打开控制台选择对应的应用，可以看到在 Todo 表中会有一个新的记录，它的 `content` 列的值就是刚才输入的「点个外卖」。

详细的实现细节请阅读源代码，里面有完整的代码以及注释帮助开发者理解如何在 LeanEngine 上编写符合自己项目需求的代码。

## 部署到云端

部署到预备环境：

```
$ lean deploy
```

如果你设置了 [二级域名](leanengine_webhosting_guide-node.html#设置域名)，即可通过 `http://stg-${your_app_domain}.leanapp.cn` 访问你应用的预备环境。

部署到生产环境：

```
$ lean publish
```

如果你设置了 [二级域名](leanengine_webhosting_guide-node.html#设置域名)，即可通过 `http://${your_app_domain}.leanapp.cn` 访问你应用的生产环境。

