---
layout: pos
title: heatmap for smap
date: 2020-08-03 23:10:58
top: 995
categories:
- smap-plugins-shsmi
tags:
- arcgis
- smap
---
heatmap for smap-shsmi

## 引用方式
npm
```js
import SMap from 'smap-shsmi' // 引用SMAP
import Plugins from 'smap-plugins-shsmi' // 引用Plugins
```
普通js
```js
 <script src="http://10.108.3.16/smiapi/smap/SMap.min.js"></script>
 <script src="http://10.108.3.16/smiapi/smap/Plugins.min.js"></script>
```


## 目录
- [热力图调用参数说明](#热力图调用参数说明)
- [添加热力图](#添加热力图)
- [更新热力图](#更新热力图)
- [隐藏热力图](#隐藏热力图)
- [显示热力图](#显示热力图)
- [移除热力图](#移除热力图)

## 热力图调用参数说明
```js
    id            // 热力图对应id  
    h337         // heatmapjs 中
    container    //map div id 
    radius      //半径
    maxOpacity  //最大透明度
    minOpacity  //最小透明度
    blur       //模糊大小
    gradient   // 渐变值
    datas     //数据
```
## 添加热力图
```js
import h337 from 'heatmapjs'  //heatmapjs
import SMap from 'smap-shsmi' // 引用SMAP
import Plugins from 'smap-plugins-shsmi' // 引用Plugins
 const map = new SMap.Map('container', {
        viewMode: '3D',
        center: [0, 0],
        zoom: 4,
        zooms: [0, 12],
        pitch: 60,
        mapStyle: 'smap://styles/dark',
        showBuildingBlock: true
      })
```
```js
const param = {
        id: 'heatmap',
        h337: h337,
        container: 'container',
        radius: 30,
        maxOpacity: 0.8,
        minOpacity: 0,
        blur: 0.7,
        gradient: {
          0: 'rgb(0,0,0)',
          0.3: 'rgb(0,0,255)',
          0.8: 'rgb(0,255,0)',
          0.98: 'rgb(255,255,0)',
          1: 'rgb(255,0,0)'
        },
        datas: [
          [-3020, -5200],
          [-3020, -5200],
          [-3120, -5200],
          [-3120, -5100],
          [-3220, -5200],
          [-3220, -5200],
          [-3220, -5200],
          [-3120, -5200],
          [-3220, -5200]
        ]
      }
      const HeatMap = new Plugins.HeatMap(map.view)
      HeatMap.add(param)
```
![热力图三维](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/heatmap/heatmap.png)
![热力图二维](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/heatmap/heatmap.png)
## 更新热力图
```js
 const updatedatas = [
        [-3020, -6200, 500],
        [-3120, -6200, 500],
        [-3120, -6100, 500],
        [-3220, -6200, 1000]
      ]
    HeatMap.refreshdata(updatedatas)
```
## 隐藏热力图
```js
 HeatMap.hide()
```
## 显示热力图
```js
HeatMap.show()
```
## 移除热力图
```js
HeatMap.remove('heatmap')    
```
