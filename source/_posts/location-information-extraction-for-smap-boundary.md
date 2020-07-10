---
title: location information extraction for smap boundary
date: 2020-07-10 10:39:45
categories:
- soe
tags:
- smap
- soe
---
基于SOE位置坐标提取所在区县、街道、居委会等信息

## 目录
- [SOE扩展服务开发](#SOE扩展服务开发)
- [SOE扩展服务部署](#SOE扩展服务部署)
- [SOE开发示例代码](#SOE开发示例代码)
- [SOE扩展服务页面测试](#SOE扩展服务页面测试)
- [SOE扩展服务PostMan测试](#SOE扩展服务PostMan测试)
- [SOE扩展服务代码调用示例](#SOE扩展服务代码调用示例)

## SOE扩展服务开发
![开发代码](https://gitee.com/thiswildidea/images/raw/master/SOE/SOE%E5%BC%80%E5%8F%91.png)

## SOE扩展服务部署
![服务部署](https://gitee.com/thiswildidea/images/raw/master/SOE/soedepoly.png)


##  SOE开发示例代码
[![SOE示例代码](https://gitee.com/thiswildidea/images/raw/master/SOE/soe.png "GitHub-SOE开发示例代码")](https://github.com/thiswildidea/soe_sample.git)

## SOE扩展服务页面测试
![页面调试](https://gitee.com/thiswildidea/images/raw/master/SOE/htmlrequest.png)
```js
{
   "xq": {
       "x": "926.2958984375",
       "y": "-3862.19219970703",
       "name": "黄浦区",
       "qxcode": "01",
       "area": 20288024.285772,
       "Shape_Length": 19974.927168038354,
       "Shape_Area": 20288024.254232578
   },
       "jd": {
       "qx_name": "黄浦区",
       "x": "130.582702636719",
       "y": "-131.352294921875",
       "name": "南京东路街道",
       "jd_code": "0102",
       "jd_code_old": null,
       "mark": " ",
       "bm_code": null,
       "area": 2394111.005086,
       "Shape_Length": 7121.459256870845,
       "Shape_Area": 2394111.036476193
   },
      "jwh": {
      "codx": "72.8416137695313",
      "cody": "197.221313476563",
      "jdname": "南京东路街道",
      "name": "定兴居委会",
      "qxname": "黄浦区",
      "jwhcode": "010222",
      "jdcode": "0102",
      "gnqcode": null,
      "gnqname": null,
      "jwh_code_old": null,
      "gnq_code_old": null,
      "gnq_name_old": null,
      "jd_code_old": null,
      "mark": " ",
      "jd_code_1": null,
      "jwh_code_1": null,
      "area": 139785.476893,
      "Shape_Length": 1527.7262899206362,
      "Shape_Area": 139785.46658027975
   }
}
```
## SOE扩展服务PostMan测试
![PostMan测试](https://gitee.com/thiswildidea/images/raw/master/SOE/postman.png)

## SOE扩展服务代码调用示例
```js
   const url = 'http://10.108.3.16/arcgis/rest/services/soe/sh_boundary_service/MapServer/exts/ShsmiSOEServiceBus/findqxjdjwhinformationbylocation'
   const requestParamter = 'location={"x":"0","y":"0"}&f=pjson'
   axios.post(url, requestParamter).then((r) => {
     if (r.status === 200) {
       console.log(r.data)
     }
   })
 ```