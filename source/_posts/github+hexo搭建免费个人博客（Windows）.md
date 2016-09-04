---
title: github+hexo搭建免费个人博客（Windows）
date: 2016-09-01 21:14:34
tags:
- hexo
categories: 
- 博客搭建
---

![](http://ww1.sinaimg.cn/large/a8fc9690gw1f7hdxrjygjj20zk0npwlx.jpg)


>出于工作、兴趣、分享等各种原因，很多人想搭建自己的一个博客，本文将介绍如何利用github+hexo搭建免费的个人博客。

<!-- more -->

## 主要步骤


1.安装node.js，用于生成静态页面（node-v4.4.4-x64.msi）[node.js中文网](http://nodejs.cn/)，确认版本用node -v
2.安装git，将本地hexo内容提交到github上去（msysgit为windows版本，Git-2.5.1-64-bit.exe）
3.申请github账号，作为博客的远程仓库，免费挂在网上提供访问的，配置好SSH Keys之后提交不需再手动输入账号密码，检查是否有ssh keys（cd ~/.ssh若提示No such file or directory则要生成）
设置用户信息命令，新建远程仓库karl2000.github.io(命名要求"用户名.github.io")
git config --global user.name "karl2000"//用户名
git config --global user.name "karl2000@qq.com"//邮箱
4.安装hexo（npm install hexo-cli -g）（npm install hexo --save），确认版本用hexo -v
5.初始化文件夹（hexo init）
6.运行命令npm install hexo-deployer-git --save
避免出现如下错误提示
ERROR Deployer not found : github
7.清除缓存文件 (db.json) 和已生成的静态文件 (public)。（hexo clean，本机调试时可不用）
8.生成静态页面（hexo generate或者hexo g）
9.本地启动（hexo server或者hexo s）
10.部署（hexo deploy或者hexo d）
打开站点_config.yml，修改deploy指向
```
deploy:
  type: git
  repo: git@github.com:karl2000/karl2000.github.io.git #此处复制github仓库地址后再加上“.git”
  branch: master
  ```
11.新建博客（hexo new 标题或者hexo n 标题）
12.新建页面（hexo new page "tags"新建标签页面）
步骤1-4只配置一次即可，以后操作只需后面的步骤。


理解：网页github上的master分支是自动维护的，由hexo d进行部署，不要手动git对其操作

更改主题，
可到https://hexo.io/themes/搜索合适的主题
复制下载主题git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
安装渲染器（==）
    npm install hexo-renderer-jade --save
    npm install hexo-renderer-sass --save
hexo使用参考官方教程https://hexo.io/zh-cn/



思路：安装node.js->安装git->安装hexo

经验：
1. 如果修改_config.yml过程中出现一堆乱码，很有可能在冒号后面没有加空格引起
2. 公益404网页无法显示解决办法：使用独立域名
3. hexo d -g命令不报错但是网页打不开，请尝试hexo clean
4. 出现如下错误，原因是对package.json进行了修改（可能由于git merge或者git pull产生），利用`git checkout -- package.json`撤销对工作区的修改，或者打开文件直接修改
```
Administrator@FVJOP6VIOYE3H4W MINGW64 /e/CODE/git/BLOG/karl2000githubio (master)
$ hexo
FATAL Cannot read property 'code' of undefined
TypeError: Cannot read property 'code' of undefined
    at C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\lib\find_pkg.js:23:25
    at tryCatcher (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\util.js:16:23)
    at Promise._settlePromiseFromHandler (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\promise.js:510:31)
    at Promise._settlePromise (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\promise.js:567:18)
    at Promise._settlePromise0 (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\promise.js:612:10)
    at Promise._settlePromises (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\promise.js:687:18)
    at Async._drainQueue (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\async.js:138:16)
    at Async._drainQueues (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\async.js:148:10)
    at Immediate.Async.drainQueues [as _onImmediate] (C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli\node_modules\bluebird\js\release\async.js:17:14)
    at processImmediate [as _immediateCallback] (timers.js:383:17)

```
5. 出现如下错误，输入`npm install hexo-server --save`
```
Administrator@FVJOP6VIOYE3H4W MINGW64 /d/karl2000.github.io (hexo)
$ hexo s
Usage: hexo <command>

Commands:
  clean     Removed generated files and cache.
  config    Get or set configurations.
  deploy    Deploy your website.
  generate  Generate static files.
  help      Get help on a command.
  init      Create a new Hexo folder.
  list      List the information of the site
  migrate   Migrate your site from other system to Hexo.
  new       Create a new post.
  publish   Moves a draft post from _drafts to _posts folder.
  render    Render files with renderer plugins.
  version   Display version information.

Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/
```
思维导图






