---
title: 使用Hexo搭建个人博客
date: 2019-10-20 17:30:34
tags: Hexo
---
### 准备环境：

1. node.js
2. git

### 安装步骤

1. 安装hexo-cli
	```
    $ npm install -g hexo-cli
    ```

2. 建立一个新的文件夹来作为博客的目录
    ```
    $ mkdir blog
    ```

3. 初始化博客
    ```
    $ sudo hexo init
    # windows下直接使用 hexo init
    ```

3. 启动博客
    ```
    hexo server
    # 可简写：hexo s
    ```

> 至此，一个博客就搭建完成了

### 新建文章

1. 新建文章
    ```
    hexo new '文章名'
    # 可简写： hexo n '文件名'
    ```

2. 清理
    ```
    hexo clean
    ```

3. 重新生成静态文件
    ```
    hexo generate
    # 可简写: hexo g
    ```

### 部署到服务器(或github等代码托管平台)

#### 将博客部署到github上

1. 在github上创建自己的主页(项目名与自己用户名一致)

2. 安装git部署插件
    ```
        $ npm install --save hexo-deployer-git
    ```

3. 设置博客目录内 _config.yml文件
    修改最下面内容
    ```
    deploy: 
      type: git
      repo: 仓库地址
      branch: master
    ```

4. 部署到远端
    ```
    $ hexo d
    ```

### 设置主题

1. 找到心仪的主题 , 例：[https://github.com/litten/hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)

2. 将主题拷贝到主题目录
    ```
    git clone 主题地址 themes/主题名
    ```

3. 修改配置文件 _config.yml(大概第87行) 
    ```
    theme: 主题名(默认是landscape)
    ```
4. 重新清理，创建，部署

### 参考
b站程序羊：[手把手教你从0开始搭建自己的个人博客 |无坑版视频教程| hexo](https://www.bilibili.com/video/av44544186)