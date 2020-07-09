---
layout: pos
title: tokenManager for smap
date: 2020-07-08 22:16:39
categories:
- token
tags:
- token
- arcgis
---
上海市测绘院公共服务平台、ArcGIS、Portal 统一token 管理器
## 目录
- [平台token管理器](#平台token管理器)
- [平台token调用方式](#平台token调用方式)
## 平台token管理器
![Image text](https://gitee.com/thiswildidea/images/raw/master/token/tokenManagerUrl.png)
以上tokenManager 界面中 相关参数说明如下：

地图Token 配置名称： 唯一配置名称，不允许重复，通过这个token 配置名称，获取平台token配置信息，调用时候后台会根据token 配置信息生成token.

用户名：平台授权的用户

密码：平台授权的用户的密码

token地址： 平台token获取地址

token 类型： 主要分为三种类型，包括onemap、arcgis和portal，根据具体平台token 类型选择

token 标注：标注token信息，便于识别

## 平台token调用示例
```js
const url =  'http://10.108.3.16:8401/mapconfig/gistoken'
const tokenconfigname ='smiapi_new'  //上步骤中地图Token 配置名称
const requestParamter = {
            tokenconfigname: tokenconfigname,
            domainName: window.location.host //请求前端地址
    }
 axios.post(url, requestParamter).then((r) => {
  const gistoken = JSON.parse(r.data.data).token
 })
```



