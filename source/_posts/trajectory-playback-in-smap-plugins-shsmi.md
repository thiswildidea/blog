---
layout: pos
title: trajectory  playback  in  smap-plugins-shsmi
date: 2020-07-16 21:43:13
categories:
- smap-plugins-shsmi
tags:
- smap
- plugins
---
二三维轨迹路径播放
## 目录
- [调用示例](#调用示例)
    [三维轨迹播放](#三维轨迹播放)
    [二维轨迹播放](#二维轨迹播放)
- [参数说明](#参数说明)

## 调用示例
### 三维轨迹播放
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
      const routedata = [
        {
          x: 358.5185,
          y: -77.2235
        },
        {
          x: 267.4522,
          y: 99.1188
        },
        {
          x: 234.90484,
          y: 212.834811
        },
        {
          x: 181.7233,
          y: 381.1000
        },
        {
          x: 138.1169,
          y: 527.79151
        },
        {
          x: 88.0071,
          y: 647.4898
        },
        {
          x: 63.1774,
          y: 692.2989
        },
        {
          x: 94.5310,
          y: 706.0872
        },
        {
          x: 143.59157,
          y: 595.3354
        },
        {
          x: 182.1127,
          y: 481.7369
        },
        {
          x: 223.4553,
          y: 323.6532
        },
        {
          x: 248.4933,
          y: 203.5321
        },
        {
          x: 325.065,
          y: 31.37497
        },
        {
          x: 546.1844,
          y: -355.09700
        }
      ]
      const trajectory = new Plugins.Trajectory(map.map)
      trajectory.playback({
        coords: routedata,
        showtrail: true,
        trailsymbol: {
          type: 'simple-line',
          color: [255, 255, 255, 0.5],
          width: '10px',
          style: 'solid'
        },
        mobilesymbol: {
          type: 'point-3d',
          symbolLayers: [{
            type: 'icon',
            size: '50px',
            resource: {
              href: require('@/assets/car.png')
            }
          }],
          verticalOffset: {
            screenLength: 50,
            maxWorldLength: 2000,
            minWorldLength: 20
          },
          callout: {
            type: 'line',
            color: [0, 0, 0],
            size: 2,
            border: {
              color: [255, 255, 255]
            }
          }
          }
        })
```
![三维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectoryplayback.png)
![三维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectoryplayback1.png)
![三维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/3d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectory.gif)
### 二维轨迹播放
```js
import SMap from 'smap-shsmi' // 引用SMAP
import Plugins from 'smap-plugins-shsmi' // 引用Plugins
 const map = new SMap.Map('container', {
        viewMode: '2D',
        center: [0, 0],
        zoom: 4,
        zooms: [0, 12],
        mapStyle: 'smap://styles/dark'
      })
```
```js
      const routedata = [
        {
          x: 358.5185,
          y: -77.2235
        },
        {
          x: 267.4522,
          y: 99.1188
        },
        {
          x: 234.90484,
          y: 212.834811
        },
        {
          x: 181.7233,
          y: 381.1000
        },
        {
          x: 138.1169,
          y: 527.79151
        },
        {
          x: 88.0071,
          y: 647.4898
        },
        {
          x: 63.1774,
          y: 692.2989
        },
        {
          x: 94.5310,
          y: 706.0872
        },
        {
          x: 143.59157,
          y: 595.3354
        },
        {
          x: 182.1127,
          y: 481.7369
        },
        {
          x: 223.4553,
          y: 323.6532
        },
        {
          x: 248.4933,
          y: 203.5321
        },
        {
          x: 325.065,
          y: 31.37497
        },
        {
          x: 546.1844,
          y: -355.09700
        }
      ]
      const trajectory = new Plugins.Trajectory(map.map)
      trajectory.playback({
        coords: routedata,
        showtrail: true,
        trailsymbol: {
          type: 'simple-line',
          color: [255, 255, 255, 0.5],
          width: '10px',
          style: 'solid'
        },
        mobilesymbol: {
          type: 'picture-marker',
          url: require('@/assets/car.png'),
          width: '64px',
          height: '64px'
          }
        })
```
![二维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectoryplayback.png)
![二维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectoryplayback1.png)
![二维轨迹播放](https://gitee.com/thiswildidea/images/raw/master/smiapi/ts/4x/2d/%E8%BD%A8%E8%BF%B9%E6%92%AD%E6%94%BE/trajectoryplayback.gif)
## 参数说明
```js
coords：轨迹坐标（上海坐标系统）
showtrail: 是否显示轨迹
trailsymbol： 轨迹符号   //二三维模式下自行定义 参考以上示例
mobilesymbol：移动符号 //二三维模式下自行定义  参考以上示例
```
