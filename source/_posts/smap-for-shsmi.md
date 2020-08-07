---
layout: pos
title: smap for shsmi
date: 2020-07-08 14:35:32
top: 1000
categories:
- smap-shsmi
tags:
- arcgis
- smap
---
上海市测绘院地图API加载库,通过该API库实现上海测绘院地图数据加载显示(仅限上海市政务网可用)

## 注意事项
由于`smap-shsmi` 属于新版本api,同时支持二三维一体化，目前功能还不完善，内容同步更新中。


##  示例代码
[![Smap使用示例代码](https://gitee.com/thiswildidea/images/raw/master/others/github.jpg "Smap使用示例代码")](https://github.com/thiswildidea/SMap-shsmi-demo)

## 目录
- [安装](#安装)
- [使用](#使用)
- [以NPM包方式使用](#以NPM包方式使用)
- [以普通JS方式使用](#以普通JS方式使用)
- [示例](#示例)
  - [地图](#地图)
    - [生命周期](#生命周期)
      - [创建二维地图](#创建二维地图)
      - [创建三维地图](#创建三维地图)
    - [地图样式](#地图样式)
      - [地图样式-暗色样式](#地图样式-暗色样式)
      - [地图样式-亮色样式](#地图样式-亮色样式)
      - [地图样式-实景样式](#地图样式-实景样式)
    - [地图属性](#地图属性)
      - [地图缩放级别控制](#地图缩放级别zooms控制)
      - [地图是否可旋转](#地图是否可旋转)
      - [三维建筑地块是否可见](#三维建筑地块是否可见)
        [获取三维地图俯仰角](#[获取三维地图俯仰角)
      - [设置三维地图俯仰角](#设置三维地图俯仰角)
      - [获取地图中心点](#获取地图中心点)
      - [获取地图级别](#获取地图级别)
      - [设置地图中心点](#设置地图中心点)
      - [设置地图级别](#设置地图级别)
      - [设置地图级别和中心点](#设置地图级别和中心点)
      - [获取地图比例尺](#获取地图比例尺)
      - [设置地图旋转角度](#设置地图旋转角度)
      - [获取地图显示范围](#获取地图显示范围)
      - [设置地图显示范围](#设置地图显示范围) 
      - [地图平移-像素平移](#地图平移-像素平移)
      - [地图平移-中心点平移](#地图平移-中心点平移)
      - [地图放大](#地图放大)
      - [地图放大](#地图缩小)
      - [设置地图样式](#设置地图样式)
      - [获取地图样式](#获取地图样式)
      - [开启穿透地表](#开启穿透地表)
      - [恢复地表模式](#恢复地表模式)
      - [添加地图缩放范围限制](#添加地图缩放范围限制)
      - [移除地图缩放范围限制](#移除地图缩放范围限制)
      - [鼠标禁用](#禁用鼠标禁用)
      - [3d模式下二三维视角切换](#3d模式下二三维视角切换)
    - [添加图层](#添加图层)
       - [根据服务url添加图层](#根据服务url添加图层)
       - [设置图层属性](#设置图层属性)
       - [根据图层id删除图层](#根据图层id删除图层)
    - [自定义地图控件主题](#自定义地图控件主题)
       - [自定义地图控件主题-暗色主题](#自定义地图控件主题-暗色主题)
       - [自定义地图控件主题-亮色主题](#自定义地图控件主题-亮色主题)
    - [地图控件](#地图控件)
       - [地图控件-Home](#地图控件-Home)
       - [地图控件-Zoom](#地图控件-Zoom)
       - [地图控件-Compass](#地图控件-Compass)
       - [地图控件-Fullscreen](#地图控件-Fullscreen)
       - [地图控件-LayerListControl](#地图控件-LayerListControl)
       - [地图控件-MeasureLine](#地图控件-MeasureLine)
       - [地图控件-MeasureArea](#地图控件-MeasureArea)
       - [地图控件-BasemapToggle](#地图控件-BasemapToggle)
       - [地图控件-UndergroundSwitch](#地图控件-UndergroundSwitch)
       - [地图控件-BMapGallery](#地图控件-BMapGallery)
       - [地图控件-BMapGalleryExpand](#地图控件-BMapGalleryExpand)
       - [删除地图控件](#删除地图控件)
    - [地图覆盖物](#地图覆盖物)
      - [添加点状覆盖物](#添加点状覆盖物)
      - [更新点状覆盖物](#更新点状覆盖物)
      - [删除点状覆盖物](#删除点状覆盖物)
      - [添加点状覆盖物多个](#添加点状覆盖物多个)
      - [更新点状覆盖物多个](#更新点状覆盖物多个)
      - [删除点状覆盖物多个](#删除点状覆盖物多个)
      - [添加点状覆盖物组](#添加点状覆盖物组)
      - [更新点状覆盖物组](#更新点状覆盖物组)
      - [删除点状覆盖物组](#删除点状覆盖物组)
      - [添加线状覆盖物](#添加线状覆盖物)
      - [更新线状覆盖物](#更新线状覆盖物)
      - [删除线状覆盖物](#删除线状覆盖物)
      - [添加线状覆盖物多个](#添加线状覆盖物多个)
      - [更新线状覆盖物多个](#更新线状覆盖物多个)
      - [删除线状覆盖物多个](#删除线状覆盖物多个)
      - [添加线状覆盖物组](#添加线状覆盖物组)
      - [更新线状覆盖物组](#更新线状覆盖物组)
      - [删除线状覆盖物组](#删除线状覆盖物组)
      - [添加面状覆盖物](#添加面状覆盖物)
      - [更新面状覆盖物](#更新面状覆盖物)
      - [删除面状覆盖物](#删除面状覆盖物)
      - [添加面状覆盖物多个](#添加面状覆盖物多个)
      - [更新面状覆盖物多个](#更新面状覆盖物多个)
      - [删除面状覆盖物多个](#删除面状覆盖物多个)
      - [添加面状覆盖物组](#添加面状覆盖物组)
      - [更新面状覆盖物组](#更新面状覆盖物组)
      - [删除面状覆盖物组](#删除面状覆盖物组)
    - [地图覆盖物More](#地图覆盖物More)
      - [添加点状覆盖物](#添加点状覆盖物addfeature)
      - [更新点状覆盖物](#更新点状覆盖物updatefeature)
      - [删除点状覆盖物](#删除点状覆盖物removefeature)
      - [添加点状覆盖物多个](#添加点状覆盖物多个addfeature)
      - [更新点状覆盖物](#更新点状覆盖物多个updatefeature)
      - [删除点状覆盖物多个](#删除点状覆盖物多个removefeature)
      - [添加点状覆盖物组](#添加点状覆盖物组addfeature)
      - [更新点状覆盖物组](#更新点状覆盖物组updatefeature)
      - [删除点状覆盖物组](#删除点状覆盖物组removefeature)
    - [地图事件](#地图事件)
      - [地图事件列表](#地图事件列表)
      - [地图加载完成事件](#地图加载完成事件)
      - [地图范围变化事件](#地图范围变化事件)
      - [地图中心点变化事件](#地图中心点变化事件)
      - [地图失去焦点事件](#地图失去焦点事件)
      - [地图单击事件](#地图单击事件)
      - [地图双击事件](#地图双击事件)
      - [地图拖拽事件](#地图拖拽事件)
      - [地图聚焦事件](#地图聚焦事件)
      - [地图按住事件](#地图按住事件)
      - [地图键盘键按下事件](#地图键盘键按下事件)
      - [地图键盘键弹起事件](#地图键盘键弹起事件)
      - [地图鼠标和触摸滚动事件](#地图鼠标和触摸滚动事件)
      - [地图鼠标或触摸按下事件](#地图鼠标或触摸按下事件)
      - [地图鼠标进入或触摸开始事件](#地图鼠标进入或触摸开始事件)
      - [地图鼠标离开和触摸结束事件](#地图鼠标离开和触摸结束事件)
      - [地图鼠标移动和触摸操作事件](#地图鼠标移动和触摸操作事件)
      - [地图鼠标释放和触摸结束事件](#地图鼠标释放和触摸结束事件)
      - [地图控件大小变化事件](#地图控件大小变化事件)
      
## 安装
```bash
npm install smap-shsmi --save
```
## 使用
### [以NPM包方式使用]
```js
import SMap from 'smap-shsmi'
  const map = new SMap.Map('container', {
    viewMode: '3D',
    center: [0, 0],
    zoom: 5,
    zooms: [1, 12],
    pitch: 60,
    mapStyle: 'smap://styles/dark', // 'smap://styles/light' 'smap://styles/image'
    showBuildingBlock: true
  })
```
### [以普通JS方式使用]
```js
  <script src="http://10.108.3.16/smiapi/smap/SMap.min.js"/>
        const map = new SMap.Map('mapcontainer', {
           viewMode: '2D',
           center: [0, 0],
           zoom: 5,
           zooms: [1, 12],
           mapStyle: 'smap://styles/dark', // 'smap://styles/light' 'smap://styles/image'
        })
</script>
```
## 示例
### [地图]
#### [生命周期]
##### [创建二维地图]
```js
import SMap from 'smap-shsmi'
const map = new SMap.Map('container', {
  center: [0, 0],
  zoom: 5
})
```
![二维地图](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE/%E5%9C%B0%E5%9B%BE%E5%88%9B%E5%BB%BA/mapcreate.png)

##### [创建三维地图]
```js
import SMap from 'smap-shsmi'
const map = new SMap.Map('container', { 
  viewMode: '3D',
  center: [0, 0],
  zoom: 4,
  pitch:60
})
```
![三维地图](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE/%E5%9C%B0%E5%9B%BE%E5%88%9B%E5%BB%BA/mapcreate.png)

#### [地图样式]
##### [地图样式-暗色样式]
```js
const map = new SMap.Map('container', { 
  viewMode: '2D',
  center: [0, 0],
  zoom: 4,
  mapStyle: 'smap://styles/dark' //未赋值时候，默认为smap://styles/dark
})
```
2D
![二维暗色](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/darktheme.png)
3D
![三维暗色](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/darktheme.png)

##### [地图样式-亮色样式]
```js
const map = new SMap.Map('container', { 
  viewMode: '2D',
  center: [0, 0],
  zoom: 4,
  mapStyle: 'smap://styles/light' 
})
```
2D
![二维亮色](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/lighttheme.png)
3D
![三维亮色](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/lighttheme.png)

##### [地图样式-实景样式]
```js
const map = new SMap.Map('container', { 
  viewMode: '2D',
  center: [0, 0],
  zoom: 4,
  mapStyle: 'smap://styles/image' 
})
```
2D
![二维影像](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/imagetheme.png)
3D
![三维影像](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/imagestheme.png)

#### [地图属性]
##### [地图缩放级别zooms控制]
```js
const map = new SMap.Map('container', {
  center: [0, 0],
  zoom: 5,
  zooms: [1, 9]  //二三维都支持,默认最新小0，最大10 建议二维默认设置最小1，最大9
})
```
##### [地图是否可旋转]
```js
const map = new SMap.Map('container', {
  center: [0, 0],
  zoom: 5,
  zooms: [1, 9] 
  rotateEnable: false //暂二维支持
})
```
##### [三维建筑地块是否可见]
```js
const map = new SMap.Map('container', {
  center: [0, 0],
  zoom: 5,
  zooms: [1, 9] 
  showBuildingBlock: false, //三维地图可用,未赋值时候默认为true
})
```
![暗色建筑](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%BB%BA%E7%AD%91%E7%89%A9%E6%A8%A1%E5%9E%8B/darkthemebuilding.png)
![亮色建筑](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%BB%BA%E7%AD%91%E7%89%A9%E6%A8%A1%E5%9E%8B/lightthemebuilding.png)
![实景建筑]](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%BB%BA%E7%AD%91%E7%89%A9%E6%A8%A1%E5%9E%8B/imagethemebuilding.png)
##### [获取三维地图俯仰角]
```js
const pitch= map.getPitch()
```
##### [设置三维地图俯仰角]
```js
map.setPitch(30)
```
##### [获取地图中心点]
```js
const mapcenter = map.getCenter()
```
##### [获取地图级别]
```js
const zoom = map.getZoom()
```
##### [设置地图中心点]
```js
//2D
 map.setCenter(0，0)
//3D
map.setCenter(0，0, 0)
```
##### [设置地图级别]
```js
 map.setZoom(10)
```
##### [设置地图级别和中心点]
```js
//2D
 map.setZoomAndCenter(10，[0, 0])
//3D
map.setZoomAndCenter(10，[0, 0, 0])
```
##### [获取地图比例尺]
```js
map.getScale()
```
##### [设置地图旋转角度]
```js
map.setRotation(90)
```
##### [获取地图显示范围]
```js
const bounds = map.getBounds()
```
##### [设置地图显示范围]
```js
//2D
const mybounds = new SMap.Bounds([-12244.941157, -6531.252646], [13155.109644,5811.584540]);
map.setBounds(mybounds);
//3D
const mybounds = new SMap.Bounds([-12244.941157, -6531.252646], [13155.109644,5811.584540]);
OR
const mybounds = new SMap.Bounds([-12244.941157, -6531.252646, 0], [13155.109644,5811.584540, 0]);
map.setBounds(mybounds);
```
##### [地图平移-像素平移]
```js
map.panBy(50, 100)
```
##### [地图平移-中心点平移]
```js
//2D
map.panTo(0, 0)
//3D
map.panTo(0, 0, 0) OR map.panTo(0, 0)
```
##### [地图放大]
```js
map.zoomIn()
```
##### [地图缩小]
```js
map.zoomOut()
```
##### [设置地图样式]
```js
map.setMapStyle('smap://styles/light')
```
##### [获取地图样式]
```js
map.getMapStyle()
```
##### [开启穿透地表]
```js
map.enableThroughGround(true)
```
##### [恢复地表模式]
```js
map.enableThroughGround(false)
```
##### [添加地图缩放范围限制]
```js
 this.map.setExtentConstrain([0, 0], [1000, 1000])
```
##### [移除地图缩放范围限制]
```js
map.removeExtentConstrain()
```
##### [鼠标禁用]
```js
map.enableMouseEvent(fasle)
```
##### [3d模式下二三维切换]
```js
map.switchMode('2d')   //map.switchMode('3d')
```
#### [添加图层]
##### [根据服务url添加图层]
```js
layerType         // 图层类型 MapImageLayer SceneLayer FeatureLayer TileLayer GraphicsLayer  SHCTiledMapServiceLayer
layerUrl          // 服务URl
isToken           // 服务isToken
layerTitle        // 服务title
layerId          // 服务layerId
layerOpacity      // 服务opacity
layerVisible      // 服务visible
layerLabelsVisible // 服务labelsVisible 支持FeatureLayer
layerLabelingInfo // 服务labelingInfo 支持FeatureLayer
layerMaxScale     // 服务maxScale
layerMinScale    // 服务minScale
layerdefinitionExpression //服务definitionExpression
layerelevationInfo // elevationInfo  支持FeatureLayer SceneLayer GraphicsLayer
layerPopupEnabled // 服务popupEnabled 支持FeatureLayer SceneLayer GraphicsLayer
layerPopupTemplate// 服务popupTemplate 支持FeatureLayer SceneLayer GraphicsLayer
layerRenderer     // 服务renderer
layerSublayers   // sublayers  支持支持MapImageLayer 
```
```js
const SceneLayerparam = {
              layerType: 'SceneLayer',
              layerUrl: "http://10.201.37.220/server/rest/services/Hosted/LBJZ_ORIGIN/SceneServer",
              layerTitle: "历保建筑原貌",
              layerLayerId: "LBJZ_ORIGIN",
              layerOpacity:1,
              layerVisible:true,
              layerMaxScale:1000,
              layerMinScale:10000000,
              layerPopupEnabled:true,
              elevationInfo: {
                             mode: 'absolute-height',
                            offset: -2.5
                    }
             }
this.map.addLayer(SceneLayerparam)
```
##### [设置图层属性]
```js
layerId          // 服务layerId
layerTitle        // 服务title
layerOpacity      // 服务opacity
layerVisible      // 服务visible
layerLabelsVisible // 服务labelsVisible 支持FeatureLayer
layerLabelingInfo // 服务labelingInfo 支持FeatureLayer
layerMaxScale     // 服务maxScale
layerMinScale    // 服务minScale
layerdefinitionExpression  //服务过滤条件
layerelevationInfo // elevationInfo  支持FeatureLayer SceneLayer GraphicsLayer
layerPopupEnabled // 服务popupEnabled 支持FeatureLayer SceneLayer GraphicsLayer
layerPopupTemplate// 服务popupTemplate 支持FeatureLayer SceneLayer GraphicsLayer
layerRenderer     // 服务renderer
layerSublayers   // sublayers  支持支持MapImageLayer 
```
```js
const Layerpasrams = {
              layerLayerId: "LBJZ_ORIGIN",
              layerVisible:false
             }
this.map.setLayerProperties(Layerpasrams)  //修改图层LBJZ_ORIGIN的可见性为false
```
##### [根据图层id删除图层]
```js
smap.removeLayer('LBJZ_ORIGIN')
```
#### [自定义地图控件主题]
##### [自定义地图控件主题-暗色主题]
```js
 <div id="container"  class="calcite-map  calcite-widgets-dark" />
```
![暗色控件主题](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/maptheme_dark.png)

###### [自定义地图控件主题-亮色主题]
```js
 <div id="container"  class="calcite-map  calcite-widgets-light" />
  
  注意：开发者可以自定义
```
![亮色控件主题](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E4%B8%BB%E9%A2%98/maptheme_light.png)

#### [地图控件]
##### [地图控件-Home]
```js
 const home = new SMap.Home({
   visible: true,
   position: 'top-right'
 })
 map.addControl(home)
```
##### [地图控件-Zoom]
```js
const zoom = new SMap.Zoom({
  visible: true,
  position: 'top-right'
})
map.addControl(zoom)
```
##### [地图控件-Compass]
```js
const compass = new SMap.Compass({
  visible: true,
  position: 'top-right'
})
map.addControl(compass))
```
##### [地图控件-Fullscreen]
```js
const fullscreen = new SMap.Fullscreen({
  visible: true,
  position: 'top-right'
})
map.addControl(fullscreen))
```
##### [地图控件-LayerListControl]
```js
const layerListControl = new SMap.LayerListControl({
  visible: true,
  position: 'top-right'
})
map.addControl(layerListControl)
```
##### [地图控件-MeasureLine]
```js
const measureLine = new SMap.MeasureLine({
  visible: true,
  position: 'top-right'
})
map.addControl(measureLine)
```
##### [地图控件-MeasureLine]
```js
const measureArea = new SMap.MeasureArea({
  visible: true,
  position: 'top-right'
})
map.addControl(measureArea)
```
##### [地图控件-MeasureLine]
```js
const basemapToggle = new SMap.BasemapToggle({
  visible: true,
  position: 'top-right'
})
map.addControl(basemapToggle)
```
##### [地图控件-UndergroundSwitch]
```js
// 仅支持3D地图
const underguroundSwitch = new SMap.UndergroundSwitch({
  visible: true,
  position: 'top-right'
})
map.addControl(underguroundSwitch)
```
##### [地图控件-BMapGallery]
```js
// 支持2/3D地图 （*配合暗色和亮色主题使用）
const bMapGallery = new SMap.BMapGallery({
  visible: true,
  position: 'top-right'
})
map.addControl(bMapGallery)
```
##### [地图控件-BMapGalleryExpand]
```js
// 支持2/3D地图    （*配合暗色和亮色主题使用）
const bMapGalleryexpand = new SMap.BMapGalleryExpand({
  visible: true,
  position: 'top-right'
})
map.addControl(bMapGalleryexpand)
```
![二维地图控件](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E6%8E%A7%E4%BB%B6/mapcontrols.png)
##### [删除地图控件]
```js
map.removeControl(layerListControl) //删除已经添加的layerListControl控件

```
![三维地图控件](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E6%8E%A7%E4%BB%B6/mapcontrol.png)
#### [地图覆盖物]
##### [添加点状覆盖物]
```js
 const  Pointmarker = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(22, 22),
          image: require('../assets/repaireorder_Accepted.gif') //或者用url
        }),
        attributes: {
          'name': '点1',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点1',
          color: 'red',
          visible: true,
          size: 22,
          weight: 'normal',
          angle: 0,
          backgroundColor: 'red',
          borderLineColor: 'blue',
          borderLineSize: 1,
          haloColor: '[51, 204, 51, 0.2]',
          haloSize: 0,
          horizontalAlignment: 'left',
          verticalAlignment: 'top',
          kerning: true,
          lineHeight: 25,
          lineWidth: 200,
          rotated: false,
          xoffset: 10,
          yoffset: 10
        }),
        position: [0, 0]
      })
      map.add(Pointmarker)
```
##### [更新点状覆盖物]
```js
      Pointmarker.label.text = '点1更新'
      Pointmarker.icon.image = require('../assets/blue.gif')
      map.update(Pointmarker)
```
##### [删除点状覆盖物]
```js
map.remove(Pointmarker) //移除上面添加的点状覆盖物
```
##### [添加点状覆盖物多个]
```js
 const  Pointmarker1 = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(22, 22),
          image: require('../assets/repaireorder_Accepted.gif') //或者用url
        }),
        attributes: {
          'name': '点1',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点1',
        }),
        position: [1000, 1000]
      })
 const  Pointmarker2 = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(22, 22),
          image: require('../assets/repaireorder_Accepted.gif') //或者用url
        }),
         attributes: {
          'name': '点2',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点2',
        }),
        position: [1100, 1100]
      })
      map.add([Pointmarker1,Pointmarker2])
```
##### [更新点状覆盖物多个]
```js
      Pointmarker1.label.text = '点1更新'
      Pointmarker1.icon.image = require('../assets/blue.gif')
      
      Pointmarker2.label.text = '点2更新'
      Pointmarker2.icon.image = require('../assets/blue.gif')
      map.update([Pointmarker1, Pointmarker2])
```
##### [删除点状覆盖物多个]
```js
map.remove([Pointmarker1,Pointmarker2]) //移除上面添加的Pointmarker1,Pointmarker2点状覆盖物
```
##### [添加点状覆盖物组]
```js
 const marker1 = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(40, 40),
          image: require('../assets/blue.gif')
        }),
         attributes: {
          'name': '点1',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点1',
          size: 22,
          color: 'yellow',
          xoffset: 0.1,
          yoffset: 0.1,
          // zoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        }),
        position: [500, 500, 100]
      })
      const marker2 = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(40, 40),
          image: require('../assets/blue.gif')
        }),
         attributes: {
          'name': '点2',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点2',
          size: 22,
          color: 'black',
          xoffset: 0.1,
          yoffset: 0.1,
          // zoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        }),
        position: [550, 550, 200]
      })
      const OverlayGroup = new SMap.OverlayGroup([marker1, marker2])
      map.add(OverlayGroup)
```
##### [更新点状盖盖物组]
```js
      OverlayGroup.overlayers[0].icon.image = require('../assets/repaireorder_Accepted.gif')
      OverlayGroup.overlayers[0].label.text = '点5更新'
      OverlayGroup.overlayers[1].icon.image = require('../assets/repaireorder_Accepted.gif')
      OverlayGroup.overlayers[1].label.text = '点6更新'
      map.update(OverlayGroup)

```
##### [删除点状覆盖物组]

```js
    map.remove(OverlayGroup)
```
##### [添加线状覆盖物]
```js
    onePolyline = new SMap.Polyline({
        path: [
          new SMap.LngLat(0, 0),
          new SMap.LngLat(10, 10),
          new SMap.LngLat(50, 50)
        ],
         attributes: {
          'name': '线1',
          'type': '线'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '线一',
          color: 'red',
          visible: true,
          size: 22,
          weight: 'normal',
          angle: 0,
          backgroundColor: 'red',
          borderLineColor: 'blue',
          borderLineSize: 10,
          haloColor: '[51, 204, 51, 0.2]',
          haloSize: 0,
          horizontalAlignment: 'left',
          verticalAlignment: 'top',
          kerning: true,
          lineHeight: 25,
          lineWidth: 200,
          rotated: false,
          xoffset: 10,
          yoffset: 10
        })
      })
     map.add(onePolyline)
```
##### [更新线状覆盖物]
```js
      onePolyline.label.text = '线一更新'
      map.update(onePolyline)
```
##### [删除线状覆盖物]
```js
map.remove(onePolyline) //移除上面添加的线状覆盖物
```
##### [添加线状覆盖物多个]
```js
    const Polyline1 = new SMap.Polyline({
        path: [
          new SMap.LngLat(400, 400),
          new SMap.LngLat(420, 420),
          new SMap.LngLat(450, 450)
        ],
        attributes: {
          'name': '线1',
          'type': '线'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '线一',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      const Polyline2 = new SMap.Polyline({
        path: [
          new SMap.LngLat(600, 600),
          new SMap.LngLat(620, 620),
          new SMap.LngLat(650, 650)
        ],
        attributes: {
          'name': '线1',
          'type': '线'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '线二',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      map.add([Polyline1, Polyline2])
```
##### [更新线状覆盖物多个]
```js
     Polyline1.label.text = '线一更新'
     Polyline2.label.text = '线二更新'
     map.update([Polyline1, Polyline2])
```
##### [删除线状覆盖物多个]
```js
map.remove([Polyline1,Polyline1]) //移除上面添加的Pointmarker1fourPolyline点状覆盖物
```
##### [添加线状覆盖物组]
```js
 const polyline1 = new SMap.Polyline({
        path: [
          new SMap.LngLat(400, 400),
          new SMap.LngLat(420, 420),
          new SMap.LngLat(450, 450)
        ],
      attributes: {
          'name': '线1',
          'type': '线'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '线1',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      const polyline2 = new SMap.Polyline({
        path: [
          new SMap.LngLat(300, 300),
          new SMap.LngLat(320, 320),
          new SMap.LngLat(350, 350)
        ],
        attributes: {
          'name': '线2',
          'type': '线'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '线2',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      OverlayGroup = new SMap.OverlayGroup([polyline1, polyline2])
      map.add(OverlayGroup)
```
##### [更新线状覆盖物组]
```js
     OverlayGroup.overlayers[0].label.text = '线1更新'
     OverlayGroup.overlayers[1].label.text = '线2更新'
     map.update(OverlayGroup)
```
##### [删除线状覆盖物组]

```js
     map.remove(OverlayGroup)
```
##### [添加面状覆盖物]
```js
     onePolygon = new SMap.Polygon({
        paths: [
          new SMap.LngLat(0, 0),
          new SMap.LngLat(20, 0),
          new SMap.LngLat(20, 30),
          new SMap.LngLat(0, 30),
          new SMap.LngLat(0, 0)
        ],
         attributes: {
          'name': '面1',
          'type': '面'
        },
        fillColor: 'red',
        style: 'solid',
        strokeColor: 'yellow',
        strokestyle: 'solid',
        strokeWeight: 1,
        label: new SMap.Label({
          text: '面一',
          color: 'red',
          visible: true,
          size: 22,
          weight: 'normal',
          angle: 0,
          backgroundColor: 'red',
          borderLineColor: 'blue',
          borderLineSize: 10,
          haloColor: '[51, 204, 51, 0.2]',
          haloSize: 0,
          horizontalAlignment: 'left',
          verticalAlignment: 'top',
          kerning: true,
          lineHeight: 25,
          lineWidth: 200,
          rotated: false,
          xoffset: 10,
          yoffset: 10
        })
      })
      map.add(onePolygon)
```
##### [更新面状覆盖物]
```js
      onePolygon.label.text = '面一更新'
      map.update(onePolygon)
```
##### [删除面状覆盖物]
```js
map.remove(onePolygon) //移除上面添加的面状覆盖物
```
##### [添加面状覆盖物多个]
```js
   const Polygon1 = new SMap.Polygon({
        paths: [
          new SMap.LngLat(540, 540),
          new SMap.LngLat(560, 540),
          new SMap.LngLat(560, 560),
          new SMap.LngLat(540, 560),
          new SMap.LngLat(540, 540)
        ],
       attributes: {
          'name': '面1',
          'type': '面'
        },
        fillColor: 'red',
        style: 'solid',
        strokeColor: 'yellow',
        strokestyle: 'solid',
        strokeWeight: 1,
        label: new SMap.Label({
          text: '面1',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
     const Polygon2 = new SMap.Polygon({
        paths: [
          new SMap.LngLat(500, 500),
          new SMap.LngLat(520, 500),
          new SMap.LngLat(520, 550),
          new SMap.LngLat(500, 550),
          new SMap.LngLat(500, 500)
        ],
        attributes: {
          'name': '面2',
          'type': '面'
        },
        fillColor: 'black',
        style: 'solid',
        strokeColor: 'yellow',
        strokestyle: 'solid',
        strokeWeight: 1,
        label: new SMap.Label({
          text: '面2',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      map.add([Polygon1, Polygon2])
```
##### [更新面状覆盖物多个]
```js
     Polygon1.label.text = '面一更新'
     Polygon2.label.text = '面二更新'
     map.update([Polygon1, Polygon2])
```
##### [删除面状覆盖物多个]
```js
map.remove([Polygon1,Polygon2]) //移除上面添加的Polygon1 Polygon2 面状状覆盖物
```
##### [添加面状覆盖物组]
```js
       const polygon1 = new SMap.Polygon({
        paths: [
          new SMap.LngLat(200, 200),
          new SMap.LngLat(220, 200),
          new SMap.LngLat(220, 250),
          new SMap.LngLat(200, 250),
          new SMap.LngLat(200, 200)
        ],
        attributes: {
          'name': '面1',
          'type': '面'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '面1',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      const polygon2 = new SMap.Polygon({
        paths: [
          new SMap.LngLat(240, 240),
          new SMap.LngLat(260, 240),
          new SMap.LngLat(260, 260),
          new SMap.LngLat(240, 260),
          new SMap.LngLat(240, 240)
        ],
        attributes: {
          'name': '面2',
          'type': '面'
        },
        cap: 'square',
        strokeColor: 'red',
        style: 'solid',
        lineJoin: 'round',
        label: new SMap.Label({
          text: '面2',
          size: 22,
          color: 'blue',
          xoffset: 10,
          yoffset: 10,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        })
      })
      OverlayGroup = new SMap.OverlayGroup([polygon1, polygon2])
      map.add(OverlayGroup)
```
##### [更新面状覆盖物组]
```js
     OverlayGroup.overlayers[0].label.text = '面1更新'
     OverlayGroup.overlayers[1].label.text = '面2更新'
     map.update( OverlayGroup)
```
##### [删除面状覆盖物组]

```js
     map.remove(OverlayGroup)
```
#### [地图覆盖物More]
##### [添加点状覆盖物addfeature]
```js
   const onemarker = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(40, 40),
          image: require('../assets/repaireorder_Accepted.gif')
        }),
        attributes: {        //点状覆盖物的属性
          'name': '点1',     //如果需要标注 name 字段必须有，且其字段值为标注内容
          'type': '点'
        },
        label: new SMap.Label({
          color: 'red',                      //标注颜色
          visible: true,                     //标注是否可见
          size: 22,                         // 标注字体大小
          weight: 'normal',                 //仅2d 支持
          angle: 0,                        // 仅2d 支持
          backgroundColor: 'red',          // 仅2d 支持
          borderLineColor: 'blue',         // 仅2d 支持
          borderLineSize: 1,               // 仅2d 支持
          haloColor: '[51, 204, 51, 0.2]', // 标注光圈颜色
          haloSize: 0,                     // 标注光圈大小
          horizontalAlignment: 'left',     // 仅2d 支持
          verticalAlignment: 'top',        // 仅2d 支持
          kerning: true,                    // 仅2d 支持
          lineHeight: 0,                     // 仅2d 支持
          lineWidth: 0,                       // 仅2d 支持
          rotated: true,                       // 仅2d 支持
          xoffset: 0,                         // 仅2d 支持
          yoffset: 0,                          // 仅2d 支持
          placement: 'above-right'，           //标注位置    
          maxScale: 500，                        // 最大可见比例尺
          minScale: 100000                          //最小可见比例尺
        }),
        position: [0, 0, 100]
      })
      map.addfeature(onemarker)
      这种方式自定义性强，资源占用多，不宜多加
```
##### [更新点状覆盖物updatefeature]
```js
   onemarker.attributes['name'] = '点一更新'
   onemarker.icon.image = require('../assets/blue.gif')
   map.updatefeature(onemarker)
```
##### [删除点状覆盖物removefeature]
```js
 map.removefeature(onemarker)
```
##### [添加点状覆盖物多个addfeature]
```js
   const  markone = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(40, 40),
          image: require('../assets/repaireorder_Accepted.gif')
        }),
        attributes: {
          'name': '点1',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点1',
          size: 22,
          xoffset: 0,
          yoffset: 0,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        }),
        position: [1000, 1000, 10]
      })
   const marktwo = new SMap.Marker({
        icon: new SMap.Icon({
          size: new SMap.Size(40, 40),
          image: require('../assets/repaireorder_Accepted.gif')
        }),
        attributes: {
          'name': '点2',
          'type': '点'
        },
        label: new SMap.Label({
          text: '点2',
          size: 22,
          xoffset: 0,
          yoffset: 0,
          horizontalAlignment: 'left',
          verticalAlignment: 'top'
        }),
        position: [1100, 1100, 20]
      })
     map.addfeature([markone, marktwo])
    
    通上面方法一样，自定义性强，资源占用多，不宜多加
```
##### [更新点状覆盖物多个updatefeature]
```js
markone.icon.image = require('../assets/blue.gif')
markone.attributes['name'] = '点一更新'
marktwo.icon.image = require('../assets/blue.gif')
marktwo.attributes['name'] = '点二更新'
map.updatefeature([markone, marktwo])

```
##### [删除点状覆盖物多个removefeature]
```js
 map.removefeature([markone, marktwo])
```
##### [添加点状覆盖物组addfeature]
```js
  const marks = []
      for (let i = 0; i <= 100000; i++) {
        const x = Math.ceil(Math.random() * 1200)
        const y = Math.ceil(Math.random() * 1200)
        const onemarker = new SMap.Marker({
          attributes: {
            'name': '点' + i,                             //name 字段要标注的内容
            'style': Math.ceil(Math.random()).toString() //style 对应样式，对应Style 中style 值
          },
          position: [x, y, 100]
        })
        marks.push(onemarker)
      }
      const label = new SMap.Label({
        size: 22,
        color: 'black',
        xoffset: 0.1,
        yoffset: 0.1,
        horizontalAlignment: 'left',
        verticalAlignment: 'top',
        minScale: 5000,
        maxScale: 1000
      })
      const datafiled = [{        // 覆盖组字段类型
        name: 'name',
        alias: 'name',
        type: 'string'
      }]
      const style = [             // 样式定义，和marks 中mark属性字段style 对应，对应不上没有样式
        {
          style: '0',             //mark 属性字段style 为0时候的样式
          size: new SMap.Size(40, 40),
          url: require('../assets/repaireorder_Accepted.gif')
        }, {
          style: '1',             //mark 属性字段style 为1时候的样式，以此类推可以多加
          size: new SMap.Size(40, 40),
          url: require('../assets/blue.gif')
        }
      ]
    const featureReduction = new SMap.FeatureReduction({
        type: 'cluster',
        clusterRadius: 100
      })
      massmarksgroup = new SMap.OverlayGroup(marks, {
        overlaytype: 'marker',
        datafiled: datafiled,
        style: style,
        label: label,
        frreduction: featureReduction   //聚集样式
      })
      map.addfeature(massmarksgroup)
     
     此方法适合加载大量数据点
```
二维10万个点展示
![二维十万点](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E8%A6%86%E7%9B%96%E7%89%A9/massMarks.png)

二维10万个点聚合展示
![二维十万点聚合](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E5%9C%B0%E5%9B%BE%E8%A6%86%E7%9B%96%E7%89%A9/massMarkscluster.png)

三维10万个点展示
![三维十万点](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E8%A6%86%E7%9B%96%E7%89%A9/massMarkers.png)

三维10万个优化显示
![三维十万点聚合](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E5%9C%B0%E5%9B%BE%E8%A6%86%E7%9B%96%E7%89%A9/massMarkersSelection.png)

##### [更新点状覆盖物组updatefeature]  
```js
  massmarksgroup.overlayers[0].attributes['name'] = '点5更新'
  massmarksgroup.overlayers[0].attributes['style'] = '1'
  massmarksgroup.overlayers[1].attributes['style'] = '0'
  map.updatefeature(massmarksgroup)
```

##### [删除点状覆盖物组removefeature]  
```js
 map.removefeature(massmarksgroup)
```

#### [地图事件]
##### [地图事件列表]
```js
SMap.MapEvent.maploaded or 'maploaded';
SMap.MapEvent.extentchanged or'extentchanged';
SMap.MapEvent.centerchanged or 'centerchanged';
SMap.MapEvent.blur or 'blur';
SMap.MapEvent.click or 'click';
SMap.MapEvent.doubleclick or 'doubleclick';
SMap.MapEvent.drag or 'drag';
SMap.MapEvent.focus or 'focus';
SMap.MapEvent.hold or 'hold';
SMap.MapEvent.keydown or 'key-down';
SMap.MapEvent.keyup or 'key-up';
SMap.MapEvent.mousewheel or 'mouse-wheel';
SMap.MapEvent.pointerdown or 'pointer-down';
SMap.MapEvent.pointerenter or 'pointer-enter';
SMap.MapEvent.pointerleave or 'pointer-leave';
SMap.MapEvent.pointermove or 'pointer-move';
SMap.MapEvent.pointerup or 'pointer-up';
SMap.MapEvent.resize or ' pointer-up';
```
##### [地图加载完成事件]
```js
map.on(SMap.MapEvent.maploaded, function(view) {
     
  })
```
##### [地图范围变化事件]
```js
map.on(SMap.MapEvent.extentchanged, function(excenter) {
     
  })
```
##### [地图中心点变化事件]
```js
map.on(SMap.MapEvent.centerchanged, function(center) {
     
  })
```
##### [地图失去焦点事件]
```js
map.on(SMap.MapEvent.blur, function(view,eventParamter) {
     
  })
```
##### [地图单击事件]
```js
map.on(SMap.MapEvent.click, function(view,eventParamter) {
      view.hitTest(eventParamter).then(async function(response) {
          console.log(response)
        })
  })
```
##### [地图双击事件]
```js
map.on(SMap.MapEvent.doubleclick, function(view,eventParamter) {
     
  })
```
##### [地图拖拽事件]
```js
map.on(SMap.MapEvent.drag, function(view,eventParamter) {
     
  })
```
##### [地图聚焦事件]
```js
map.on(SMap.MapEvent.focus, function(view,eventParamter) {
     
  })
```
##### [地图按住事件]
```js
map.on(SMap.MapEvent.hold, function(view,eventParamter) {
     
  })
```
##### [地图键盘键按下事件]
```js
map.on(SMap.MapEvent.keydown, function(view,eventParamter) {
     
  })
```
##### [地图键盘键弹起事件]
```js
map.on(SMap.MapEvent.keydown, function(view,eventParamter) {
     
  })
```
##### [地图键盘键弹起事件]
```js
map.on(SMap.MapEvent.hold, function(view,eventParamter) {
     
  })
```
##### [地图鼠标和触摸滚动事件]
```js
map.on(SMap.MapEvent.mousewheel, function(view,eventParamter) {
     
  })
```
##### [地图鼠标或触摸按下事件]
```js
map.on(SMap.MapEvent.pointerdown, function(view,eventParamter) {
     
  })
```
##### [地图鼠标进入或触摸开始事件]
```js
map.on(SMap.MapEvent.pointerenter, function(view,eventParamter) {
     
  })
```
##### [地图鼠标离开和触摸结束事件]
```js
map.on(SMap.MapEvent.pointerleave, function(view,eventParamter) {
     
  })
```
##### [地图鼠标移动和触摸操作事件]
```js
map.on(SMap.MapEvent.pointermove, function(view,eventParamter) {
     
  })
```
##### [地图鼠标释放和触摸结束事件]
```js
map.on(SMap.MapEvent.pointerup, function(view,eventParamter) {
     
  })
```
##### [地图控件大小变化事件]
```js
map.on(SMap.MapEvent.resize, function(view,eventParamter) {
     
  })
```


