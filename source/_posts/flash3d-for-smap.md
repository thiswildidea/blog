---
title: flash3d for smap
date: 2020-08-04 11:32:43
top: 995
categories:
- smap-plugins-shsmi
tags:
- arcgis
- smap
---
flash3d for smap-shsmi


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
- [FlashPoint3DLayer参数说明](#FlashPoint3DLayer参数说明)
- [FlashPoint3DLayer调用示例](#FlashPoint3DLayer调用示例)
- [FlashPoint3DLayer-click事件](#FlashPoint3DLayer-click事件)

## FlashPoint3DLayer参数说明
```js
    color //颜色
    nring //光圈数量
    spead //闪烁速度
    view //地图试图
    point //数据 由坐标和属性构成
```
## FlashPoint3DLayer调用示例
```js
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
  const samples = [{
        x: 0,
        y: 0,
        attributes: {
          name: '报警点1',
          address: '国际饭店'
        }
      },
      {
        x: 100,
        y: 100,
        attributes: {
          name: '报警点2',
          address: '人民广场附近1'
        }
      },
      {
        x: 150,
        y: 100,
        attributes: {
          name: '报警点3',
          address: '人民广场附近2'
        }
      }
      ]
      const param = {
        color: [255, 0, 0, 1],
        nring: 0.1,
        spead: 1.0,
        view: this.map.view,
        points: samples
      }

      const flashPoint3DLayer = new Plugins.FlashPoint3DLayer(this.map.view)
      flashPoint3DLayer.add(param)
      flashPoint3DLayer.on('click', function(result, geometry) {
        if (geometry) {
          map.view.popup.defaultPopupTemplateEnabled = true
          map.view.popup.autoOpenEnabled = false
          _map.view.popup.open({
            location: geometry,
            title: result.attributes.name,
            content: mapsenceViewPopup.createContentpopup(result.attributes)
          })
        }
      })

    createContentpopup(data) {
    let htmlstring = '';
    htmlstring += "<table>"
    for (let key in data) {
           htmlstring += "<tr>";
           htmlstring += '<td';
           htmlstring += "<span>";
           htmlstring += key;
           htmlstring += " :";
           htmlstring += "</span>";
           htmlstring += "</td>";
           htmlstring += '<td';
           htmlstring += "<span>";
           htmlstring += data[key] != null ? data[key] : "";
           htmlstring += "</span>";
           htmlstring += "</td>";
           htmlstring += "</tr>";
    }
    htmlstring += "</table>"
  }
```
![三维闪烁](https://gitee.com/thiswildidea/images/blob/master/smiapi/ts/4x/3d/flash3d/falsh3d.gif)
![三维闪烁](https://gitee.com/thiswildidea/images/blob/master/smiapi/ts/4x/3d/flash3d/falsh3d-newsymbol.gif)
## FlashPoint3DLayer-click事件
```js
 const flashPoint3DLayer = new Plugins.FlashPoint3DLayer(this.map.view)
  fashPoint3DLayer.on('click', function(result, geometry) {
     // result 返回的属性
     //geometry 返回的点击位置
  })
```

