# 起点阅读书籍分享

## 项目简介

    
    该模块可以让用户分享自己已经订阅的章节。
    原理很简单，把订阅的章节上传到服务器，可以让你在没有订阅该章节的情况下，通过其他用户分享的订阅章节来免费观看的订阅内容，和订阅后的体验一致。

## 使用指南

 * 无需任何设置，激活即用

 * 进入后根据提示先进入我的界面，然后正常观看和订阅。

 * 如果有分享其他用户分享过的章节会自动展示，不需要再次订阅

 * 如果上传失败又想马上重新上传就在起点 **清除缓存** 页面 “长按” **已下载书籍缓存** 可删除模块数据库

 * **我的** 页面 “长按” 左上角 **设置** 图标查看公告

## 模块目前问题

 * 首次观看新书可能会卡住，退出起点重进就会恢复

 * 服务器较差，经常连接超时是正常情况，如需重新上传参考 [使用指南-4](#使用指南)

 * 有问题提ISSUES

## 模块规则

* 上传

    - 在书籍详情、目录、下载、正文皆会触发上传

    - 正文规则是如果本地没有记录、本地记录上传时间大于2天会触发上传

    - 上传成功会提示 **XX章节 OK**

* 下载

    - 同IP最多2个用户、10秒内最多只能请求5次

    - 每个用户都能无限制观看其他用户的章节，前提是你在两天之内上传过订阅章节

    - 优先网络查询，网络查不到或者失败会本地数据库查询，都查不到就提示 **内容不存在**

    - 下载成功无提示，如遇到未授权注意上述下载规则

## 项目目标

    
    模块已经完成了基本的功能，但是还有很多可以改进和优化的地方。

    目前由个人出资垫付了服务器和中转费用，但是只能大概垫付两三个月，我需要大约 100 元/月 的资金来购买和维护服务器。

    如果模块你们用起来很舒服，并且不想项目暴死，请援助我们。

    如果你对我的模块感兴趣，或者想要支持我的创意，你可以选择多多宣传本项目或者以下几种方式来参与我的众筹项目


## 捐赠

* BTC：35hAgA3GnfbX12opqqxuauxbcEMQZnonaa

* USDT(仅支持TRX/TRC20)：TCR9MAoxA84AxdQCL6uohhXcH6cPnBNSrw

* 以太坊：0xe33CE05e26e9e95C6B6689F5d3751CaF5A1C5702

---

## 预览

![preview1](previews/preview1.png)

![preview2](previews/preview2.png)

![preview](previews/preview.gif)
