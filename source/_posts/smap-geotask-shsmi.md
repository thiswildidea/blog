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

## 目录
- [图层查询](#图层查询)
   - [featureLayer](#featureLayer)
      - [图层查询(featureLayer)调用](#图层查询(featureLayer)调用)
      - [图层查询(featureLayer)参数说明](#图层查询(featureLayer)参数说明)
    - [mapImageLayer](#mapImageLayer)
       - [图层查询(mapImageLayer调用)](#图层查询(mapImageLayer)调用)
       - [图层查询(mapImageLayer)参数说明](#图层查询(mapImageLayer)参数说明)
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
    const  queryTask = new GeoTask.Query(this.map.view)
    const queryTask.featurelayer(param).then((result) => {
        console.log(result)
  })
```
#### 图层查询(featurelayer)参数说明
```js
 layerUniqueId        //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
 type                 //查询要素类型 分 polygon、polyline、point 三种类型
 queryDefinition     //查询条件类似sql语句
 displayed          //查询结果是否在地图上显示
 symbol           //地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
 outFields       // 要返回的属性字段，*为所有字段，可按实际图层字段定义
 queryUrl       //查询的图层url地址，如果图层加载到地图中，传入图层layerUniqueId 即可，若地图没有加载该图层到地图，可传入该图层服务Url地址
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
    const  queryTask = new GeoTask.Query(this.map.view)
    const queryTask.featurelayer(param).then((result) => {
        console.log(result)
  })
```
#### 图层查询(mapImageLayer)参数说明
```js
 layerUniqueId           //要查的图层ID 若地图没有加载该图层可以根据queryUrl 传入可访问查询图层ur
 layerId                //要查的图层类型为MapImageLayer的子图层id
 type                  //查询要素类型 分 polygon、polyline、point 三种类型
 queryDefinition      //查询条件类似sql语句
 displayed           //查询结果是否在地图上显示
 symbol             //地图上显示的渲染符号，可根据type类型，设置polygon、polyline、point 三种类型样式及扩展类型样式
 outFields       // 要返回的属性字段，*为所有字段都返回，可按实际图层字段定义
 queryUrl        //查询的图层url 地址，如果图层加载到地图中，传入layerUniqueId 即可，若地图没有加载该图层到地图，可传入该图层服务Url地址
```
