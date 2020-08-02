---
layout: pos
title: light ring for smap new
date: 2020-08-02 23:09:31
categories:
- smap-plugins-shsmi
tags:
- plugins
- smap
---

根据筛选条件及相关设置参数为指定上海区县、街道、居委设置渐变光圈
## 目录
- [调用参数说明](#调用参数说明)
- [二维区县光圈](#二维区县光圈)
- [二维街道光圈](#二维街道光圈)
- [二维居委会光圈](#二维居委会光圈)
- [二维自定义范围光圈](#二维自定义范围光圈)
- [三维区县光圈](#三维区县光圈)
- [三维街道光圈](#三维街道光圈)
- [三维居委会光圈](#三维居委会光圈)
- [三维自定义范围光圈](#三维自定义范围光圈)
- [三维自定义光圈高度](#三维自定义光圈高度)
- [自定光圈宽度](#自定光圈宽度)
- [自定义光圈和遮盖层颜色](#自定义光圈和遮盖层颜色)
- [光圈和遮盖层隐藏](#光圈和遮盖层隐藏)
- [光圈和遮盖层显示](#光圈和遮盖层显示)
- [光圈和遮盖层移除](#光圈和遮盖层移除)
### 调用参数说明
```js
    boundaryType: 'qx_boundary',  // 光圈类型，目前支持上海市区县（qx）、街道(jd)、居委会(jwh)三个层次范围光圈
    boundaryDefinition: "name like '%黄浦%'", // 查询条件定义，支持按类型名称或者按照对应区县、街道、居委会编码查询，区县编码：qxcode like '%01% 。街道编码：jd_code like '%3509%。 居委会编码：jwhcode like '%072128%'
    boundarydistance: 150, //光圈宽度（单位米）
    bounarycount: 5, //光圈渐变个数
    inputgeometry：[[0, 0], [10000, 0], [10000, 10000],[0, 10000], [0, 0]], //范围坐标点集合，首尾坐标闭合
    boundaryColor: 'blue', //光圈渐变主色
    maskColor: [0, 17, 33, 0.9], //遮罩层颜色
    symbol: { size: 20 }  //光圈高度，仅三维中支持
```
[![区县属性数据](https://gitee.com/thiswildidea/images/raw/master/others/Datatable.png "区县属性数据")](https://gitee.com/thiswildidea/images/blob/master/resouces/boundary/qx_boundary.xlsx)
[![街道属性数据](https://gitee.com/thiswildidea/images/raw/master/others/Datatable.png "街道属性数据")](https://gitee.com/thiswildidea/images/blob/master/resouces/boundary/jd_boundary.xlsx)
[![居委会属性数据](https://gitee.com/thiswildidea/images/raw/master/others/Datatable.png "居委会属性数据")](https://gitee.com/thiswildidea/images/blob/master/resouces/boundary/jwh_boundary.xlsx)
### 二维区县光圈
```js
import SMap from 'smap-shsmi'
import Plugins from 'smap-plugins-shsmi'
  const map = new SMap.Map('container', {
    viewMode: '2D',
    center: [0, 0],
    zoom: 5,
    zooms: [1, 12],
    mapStyle: 'smap://styles/dark'
  })
```
```js
  const lightringParamter = {
    boundaryType: 'qx_boundary',
    boundaryDefinition: "name like '%黄浦%'", // qxcode like '%01%
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9]
  }
 const xqmaskBoundary = new Plugins.MaskBoundary(map.view)
 xqmaskBoundary.add(lightringParamter)
```
![二维区县光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%85%89%E5%9C%88/%E5%8C%BA%E5%8E%BF%E5%85%89%E5%9C%88.png)
### 二维街道光圈
```js
  const lightringParamter = {
    boundaryType: 'jd_boundary',
    boundaryDefinition: "name like '%上钢新村街道%'", // jd_code  like '%3509%
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9]
  }
  const jdmaskBoundary = new Plugins.MaskBoundary(smap.view)
  jdmaskBoundary.add(lightringParamter)
```
![二维街道光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%85%89%E5%9C%88/%E8%A1%97%E9%81%93%E5%85%89%E5%9C%88.png)
### 二维居委会光圈
```js
  const lightringParamter = {
    boundaryType: 'jwh_boundary',
    boundaryDefinition: "jwhcode like '%072128%'", // name like '%曹杨新苑%
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9]
  }
 const  jwhmaskBoundary = new Plugins.MaskBoundary(smap.view)
   jwhmaskBoundary.add(lightringParamter)
```
![二维居委会光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%85%89%E5%9C%88/%E5%B1%85%E5%A7%94%E4%BC%9A%E5%85%89%E5%9C%88.png)
### 二维自定义范围光圈
```js
  const lightringParamter = {
        boundarydistance: 1000,
        bounarycount: 5,
        boundaryColor: 'blue',
        maskColor: [0, 17, 33, 0.9],
        inputgeometry: [[0, 0], [10000, 0], [10000, 10000],[0, 10000], [0, 0]]
  }
   const  custommaskBoundary = new Plugins.MaskBoundary(smap.view)
   custommaskBoundary.add(lightringParamter)
```
![二维自定义范围光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%85%89%E5%9C%88/%E8%87%AA%E5%AE%9A%E4%B9%89%E5%85%89%E5%9C%88.png)
### 三维区县光圈
```js
import SMap from 'smap-shsmi'
  const map = new SMap.Map('container', {
    viewMode: '3D',
    center: [0, 0],
    zoom: 5,
    zooms: [1, 12],
    mapStyle: 'smap://styles/dark'
  })
```
```js
  const lightringParamter = {
    boundaryType: 'qx_boundary',
    boundaryDefinition: "name like '%黄浦%'", // qxcode like '%01%
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    symbol: {
      size: 20
    }
  }
  const xqmaskBoundary = new Plugins.MaskBoundary(map.view)
   xqmaskBoundary.add(lightringParamter)
```
![三维区县光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E5%8C%BA%E5%8E%BF%E5%85%89%E5%9C%88.png)
### 三维街道光圈
```js
  const lightringParamter = {
    boundaryType: 'jd_boundary',
    boundaryDefinition: "name like '%上钢新村街道%'", // jd_code  like '%3509%
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    symbol: {
      size: 20
    }
  }
  const jdmaskBoundary = new Plugins.MaskBoundary(map.view)
  jdmaskBoundary.add(lightringParamter)
```
![三维街道光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E8%A1%97%E9%81%93%E5%85%89%E5%9C%88.png)
### 三维居委会光圈
```js
  const lightringParamter = {
    boundaryType: 'jwh_boundary',
    boundaryDefinition: "name like '%曹杨新苑%' ",  // "jwhcode like '%072128%'"
    boundarydistance: 150,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    symbol: {
      size: 20
    }
  }
  const  jwhmaskBoundary = new Plugins.MaskBoundary(map.view)
   jwhmaskBoundary.add(lightringParamter)
```
![三维居委会光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E5%B1%85%E5%A7%94%E4%BC%9A%E5%85%89%E5%9C%88.png)
### 三维自定义范围光圈
```js
  const lightringParamter = {
    boundarydistance: 1000,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    inputgeometry: [[0, 0], [10000, 0], [10000, 10000],[0, 10000], [0, 0]]
    symbol: {
      size: 20
    }
  }
  const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
   custommaskBoundary.add(lightringParamter)
```
![三维自定义范围光圈](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8C%83%E5%9B%B4%E5%85%89%E5%9C%88.png)
### 三维自定义光圈高度
```js
  const lightringParamter = {
    boundarydistance: 1000,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    inputgeometry: [[0, 0], [10000, 0], [10000, 10000],[0, 10000], [0, 0]]
    symbol: {
      size: 1000
    }
  }
   const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
   custommaskBoundary.add(lightringParamter)
```
![三维自定义光圈高度](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E5%85%89%E5%9C%88%E9%AB%98%E5%BA%A6.png)
### 自定光圈宽度
```js
  const lightringParamter = {
    boundaryType: 'jwh_boundary',
    boundaryDefinition: "name like '%曹杨新苑%' ",  // "jwhcode like '%072128%'"
    boundarydistance: 550,
    bounarycount: 5,
    boundaryColor: 'blue',
    maskColor: [0, 17, 33, 0.9],
    symbol: {
      size: 20
    }
  }
   const  jwhmaskBoundary = new Plugins.MaskBoundary(map.view)
   jwhmaskBoundary.add(lightringParamter)
```
![自定光圈宽度](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E5%85%89%E5%9C%88%E5%AE%BD%E5%BA%A6.png)
### 自定义光圈和遮盖层颜色
```js
  const lightringParamter = {
    boundarydistance: 1000,
    bounarycount: 5,
    boundaryColor: 'red',
    maskColor: [112, 117, 233, 0.9],
    inputgeometry: [[0, 0], [10000, 0], [10000, 10000],[0, 10000], [0, 0]]
    symbol: {
      size: 10
    }
  }
  const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
   custommaskBoundary.add(lightringParamter)
```
![Image text](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%85%89%E5%9C%88/%E5%85%89%E5%9C%88%E5%92%8C%E9%81%AE%E7%BD%A9%E5%B1%82%E9%A2%9C%E8%89%B2%E8%87%AA%E5%AE%9A%E4%B9%89.png)
### 光圈和遮盖层隐藏
```js
 const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
 custommaskBoundary.hide()
 ```
### 光圈和遮盖层显示
```js
 const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
 custommaskBoundary.show()
 ```
### 光圈和遮盖层移除
```js
 const  custommaskBoundary = new Plugins.MaskBoundary(map.view)
 custommaskBoundary.remove()
 ```