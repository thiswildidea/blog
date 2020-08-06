---
layout: pos
title: smap-geotask-shsmi
date: 2020-07-31 16:58:44
top: 998
categories:
- smap-geotask-shsmi
tags:
- arcgis
- smap
---
# smap-geotask-shsmi
上海市测绘院smap jsapi geotask 扩展模块

## 注意事项
由于smap-geotask-shsmi 属于smap-shsmi或者smap-shsmi-aa扩展模块,再使用过程中需要先引用smap-shsmi或者smap-shsmi-aa。

## 引用方式
npm
```js
import SMap from 'smap-shsmi' // 引用SMAP
import Plugins from 'smap-geotask-shsmi' // 引用Plugins
```
普通js
```js
 <script src="http://10.108.3.16/smiapi/smap/SMap.min.js"></script>
 <script src="http://10.108.3.16/smiapi/smap/GeoTask.min.js"></script>
```

## 目录
- [图层查询](#图层查询)
   - [featureLayer](#featureLayer)
      - [图层查询(featureLayer)调用](#图层查询(featureLayer)调用)
      - [(featureLayer)查询结果地图地图移除](#(featureLayer)查询结果地图地图移除)
      - [(featureLayer)查询结果地图地图隐藏](#(featureLayer)查询结果地图地图隐藏)
      - [(featureLayer)查询结果地图地图显示](#(featureLayer)查询结果地图地图显示)
      - [图层查询(featureLayer)参数说明](#图层查询(featureLayer)参数说明)
   - [mapImageLayer](#mapImageLayer)
      - [图层查询(mapImageLayer调用)](#图层查询(mapImageLayer)调用)
      - [(mapImageLayer)查询结果地图地图移除](#(featureLayer)查询结果地图地图移除)
      - [(mapImageLayer)查询结果地图地图隐藏](#(featureLayer)查询结果地图地图隐藏)
      - [(mapImageLayer)查询结果地图地图显示](#(mapImageLayer)查询结果地图地图显示)
      - [图层查询(mapImageLayer)参数说明](#图层查询(mapImageLayer)参数说明)
   - [identify](#identify)
      - [图层identify调用](#图层查询identify调用)
      - [图层identify调用结果地图隐藏](#图层identify调用结果地图隐藏)
      - [图层identify调用结果地图显示](#图层identify调用结果地图显示)
      - [图层identify调用结果地图移除](#图层identify调用结果地图移除)
      - [图层identify调用参数说明](#图层identify调用参数说明)
## 图层查询
### featureLayer
#### 图层查询(featurelayer)调用
```js
import SMap from 'smap-shsmi' // 引用SMAP
import GeoTask from 'smap-geotask-shsmi' // 引用GeoTask
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
      layerUniqueId: 'qx_boundary',             //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
       url:'http://10.108.3.16/arcgis/rest/services/boundary/sh_qx_boundary/FeatureServer',
      queryDefinition: "name like '%黄浦%'",   // qxcode like '%01%    //查询条件类似sql语句
      displayed: false,                        //查询结果是否在地图上显示
      outFields: ['*'],                       //查询属性字段定义* 为所有字段
      type: 'polygon',                       //查询图层类型可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
      symbol: {                             // 地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
        type: 'simple-fill',
        color: [255, 255, 255, 0],
        outline: {
          color: [255, 255, 0, 1],
          width: '5px'
        }
      }
    }
    const  flayerqueryTask = new GeoTask.Query(this.map.view)
    const flayerqueryTask.featurelayer(param).then((result) => {
        console.log(result)
  })
```
#### (featureLayer)查询结果地图地图移除
```js
flayerqueryTask.remove() //移除已查询绘制在地图上的显示结果
```
#### (featureLayer)查询结果地图地图隐藏
```js
flayerqueryTask.hide()  //隐藏已查询绘制在地图上的显示结果
```
#### (featureLayer)查询结果地图地图显示
```js
flayerqueryTask.show() //显示已查询绘制在地图上的显示结果
```
#### 图层查询(featurelayer)参数说明
```js
 layerUniqueId        //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
  url                   //查询的图层url地址，如果图层加载到地图中，传入图层layerUniqueId 即可，若地图没有加载该图层到地图，可传入该图层服务Url地址
 type                 //查询要素类型 分 polygon、polyline、point 三种类型
 queryDefinition     //查询条件类似sql语句
 displayed          //查询结果是否在地图上显示
 symbol           //地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
 outFields       // 要返回的属性字段，*为所有字段，可按实际图层字段定义  
```
### mapImageLayer
#### 图层查询(mapImageLayer)调用
```js
import SMap from 'smap-shsmi' // 引用SMAP
import GeoTask from 'smap-geotask-shsmi' // 引用GeoTask
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
      layerUniqueId: 'qx_boundary',         //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
      url:'http://10.108.3.16/arcgis/rest/services/boundary/sh_jd_boundary/MapServer',  //要查的图层url 若地图没有加载该图层可以根据url传入可访问查询图层ur
      layerId:0，                          //服务图层中要被查的id
      queryDefinition: "name like '%黄浦%'", // qxcode like '%01%    //查询条件类似sql语句
      displayed: false,                    //查询结果是否在地图上显示
      outFields: ['*'],                   //要返回的属性字段，*为所有字段，可按实际图层字段定义
      type: 'polygon',                  ///查询要素类型 分 polygon、polyline、point 三种类型
      symbol: {                        // 地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
        type: 'simple-fill',
        color: [255, 255, 255, 0],
        outline: {
          color: [255, 255, 0, 1],
          width: '5px'
        }
      }
    }
    const  mlayerqueryTask = new GeoTask.Query(this.map.view)
    const mlayerqueryTask.mapImageLayer(param).then((result) => {
        console.log(result)
  })
```
#### (mapImageLayer)查询结果地图地图移除
```js
mlayerqueryTask.remove()  //移除已查询绘制在地图上的显示结果
```
#### (mapImageLayer)查询结果地图地图隐藏
```js
mlayerqueryTask.hide()  //隐藏已查询绘制在地图上的显示结果
```
#### (mapImageLayer)查询结果地图地图显示
```js
mlayerqueryTask.show()  //显示已查询绘制在地图上的显示结果
```
#### 图层查询(mapImageLayer)参数说明
```js
 layerUniqueId           //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
 url                   //查询的图层url 地址，如果图层加载到地图中，传入layerUniqueId 即可，若地图没有加载该图层到地图，可传入该图层服务Url地址
 layerId                //要查的图层类型为MapImageLayer的子图层id
 type                  //查询要素类型 分 polygon、polyline、point 三种类型
 queryDefinition      //查询条件类似sql语句
 displayed           //查询结果是否在地图上显示
 symbol             //地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
 outFields       // 要返回的属性字段，*为所有字段都返回，可按实际图层字段定义

```
### identify
#### 图层查询identify调用
```js
import SMap from 'smap-shsmi' // 引用SMAP
import GeoTask from 'smap-geotask-shsmi' // 引用GeoTask
 const map = new SMap.Map('container', {
        viewMode: '3D',
        center: [0, 0],
        zoom: 4,
        zooms: [0, 12],
        pitch: 60,
        mapStyle: 'smap://styles/dark',
        showBuildingBlock: true
      })
    let identifytask=null
      smap.on(SMap.MapEvent.maploaded, function(view, eventParamter) {
         identifytask = new GeoTask.Identify(smap.view)
         identifytask.on('click', function(result, geometry) {  // identify结果地图点击显示
            console.log(result,geometry)  
         })
    })
```
```js
//点击地图查询指定图层内容
 smap.on(SMap.MapEvent.click, function(view, eventParamter) {
     const param = {
         layerUniqueId:'XH_JD_V2',
         url:"http://10.201.37.222/arcgis/rest/services/XH_JD_V2/MapServer",
         displayed: true, //查询接口是否在地图上显示
         layerIds:[0],
         tolerance:1,
         geometry:eventParamter.mapPoint
     }
     identifytask.MapService(param).then((result) => {
       console.log(result)
     })
 })
```
#### 图层identify调用结果地图隐藏
```js
identifytask.hide()
```
#### 图层identify调用结果地图显示
```js
identifytask.show()
```
#### 图层identify调用结果地图移除
```js
identifytask.remove()
```
#### 图层identify调用参数说明
```js
  layerUniqueId   // 服务id,当服务已经加载到地图了，使用id
  url         // 服务url,当地图没有加载到地图中，使用要identify的url
  layerIds   // 服务子图层id, 指定layerIds，identify智慧识别对应图层信息
  geometry   //点击位置
  displayed  //点击识别内容是否在地图上显示
  tolerance  // 容差，值越大越容易识别
```