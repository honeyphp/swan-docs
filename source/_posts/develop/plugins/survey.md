---
title: 插件概述
header: develop
nav: plugins
sidebar: survey
---

## 什么是插件 
插件是对一组 js 接口、自定义组件或页面的封装，用于嵌入到小程序中使用，减少小程序的开发量。

插件本身不能独立运行，必须嵌入到其他小程序中才能被用户使用；而第三方小程序在使用插件时，也无法看到插件的代码。因此，插件适合用来封装自己的功能或服务，提供给第三方小程序进行展示和使用。

插件开发者可以像开发小程序一样编写一个插件并上传代码，在插件发布之后，其他小程序方可调用。小程序平台会托管插件代码，其他小程序调用时，上传的插件代码会随小程序一起下载运行。

相对于普通 js 文件或自定义组件，插件拥有更强的独立性，拥有独立的 API 接口、域名列表等，但同时会受到一些限制，如一些 API 无法调用或功能受限，以及部分组件无法在插件中使用。

同时，对于小程序和小程序使用的每个插件会进行数据安全保护，保证它们之间不能窃取其他任何一方的数据（除非数据被主动传递给另一方）。


## 支持插件的swanjs版本
插件的开发和使用自智能小程序swanjs版本 3.90.x 开始支持，低于该版本的基础库不能使用插件功能。

## 其他
在分包中暂时不支持引入插件