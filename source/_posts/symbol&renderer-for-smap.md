---
title: symbol for smap
date: 2020-08-11 08:52:14
categories:
- smap-shsmi
tags:
- symbol
- smap
---
symbol  for  smap

## 目录
- [MarkSymbol](#MarkSymbol)
    - [SimpleMarkerSymbol](#SimpleMarkerSymbol(2d/3d))
    - [PictureMarkerSymbol](#PictureMarkerSymbol(2d/3d))
    - [IconSymbol3DLayer](#IconSymbol3DLayer(3d))
    - [IconSymbol3DLayer-with-LineCallout3D(3d)](#IconSymbol3DLayer-with-LineCallout3D(3d))
    - [ObjectSymbol3DLayer](#ObjectSymbol3DLayer(3d))
    - [ObjectSymbol3DLayer-with-LineCallout3D(3d)](#ObjectSymbol3DLayer-with-LineCallout3D(3d))
- [LineSymbol](#LineSymbol)
    - [SimpleLineSymbol](#SimpleLineSymbol(2d/3d))
    - [LineSymbol3DLayer](#LineSymbol3DLayer(3d))
    - [PathSymbol3DLayer](#PathSymbol3DLayer(3d))
- [FillSymbol](#FillSymbol)
    - [SimpleFillSymbol](#SimpleFillSymbol(2d/3d))
    - [PictureFillSymbol](#PictureFillSymbol(2d/3d))
    - [MeshSymbol3D(3d)](#MeshSymbol3D(3d))
    - [ExtrudeSymbol3DLayer(3d)](#ExtrudeSymbol3DLayer(3d))
- [TextSymbol](#TextSymbol)
    - [TextSymbol(2/3d)](#TextSymbol(2/3d))
    - [TextSymbol3DLayer](#TextSymbol3DLayer(3d))
- [WaterSymbol3DLayer](#WaterSymbol3DLayer)
- [renderer]](#renderer)
   - [Simplerenderer]](#Simplerenderer)
   - [unique-valuerenderer]](#unique-valuerenderer)
### MarkSymbol
####  SimpleMarkerSymbol(2d/3d)
```js
const symbol = {
  type: "simple-marker",
  style: "square",  //circle  cross	diamond	square	triangle  x
  color: "blue",
  path: '',  //The SVG path of the icon. This property works only in 2D. IE11 is not supported.
  size: "8px",    // 8 or 8px or 8pt
  outline: {  
    color: [ 255, 255, 0 ],
    width: 3
  },
  angle: 0 , // This property is currently not supported in 3D.
  xoffset:0,
  yoffset:0
}
```
#### PictureMarkerSymbol(2d/3d)
```js
const symbol = {
  type: "picture-marker",
  url: "https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png",
  width: "64px",   // 64 or 64px or 64pt
  height: "64px", // 64 or 64px or 64pt
  angle:0,       //  The angle of the marker relative to the screen in degrees.  This property is currently not supported in 3D.
  xoffset,0 ,   //  The offset on the x-axis in points.
  yoffset,0    //The offset on the y-axis in points.
};

Rendering SVG documents and PNG images is not supported in IE11.
SVG documents must include a definition for width and height to load properly in Firefox.
`Animated GIF` and `PNG `images are not supported in 3D SceneView.
The height and width of the symbol is restricted to no more than 200px.
```
#### IconSymbol3DLayer(3d)
```js
const symbol = {
  type: "point-3d", 
  symbolLayers: [{
    type: "icon",
    anchor: "center",   //The positioning of the icon relative to the geometry.  Possible Values:"center"|"left"|"right"|"top"|"bottom"|"top-left"|"top-right"|"bottom-left"|"bottom-right"|"relative"
    anchorPosition : { x: 1.5, y: 1 }  //This property only applies when anchor is set to relative.
    size: 8,    // 14 or 14px or 14pt
    resource: { primitive: "circle" },    //The shape (primitive) or image URL (href) used to visualize the features. If both properties are present, href takes precedence and primitive is ignored.   circle、 square、 cross、 x、 kite、 triangle
    resource: {
      href: "http://10.201.37.225:8080/images/pin_blue.png"
    }
    material: { color: "red" }
    outline:{
         color: "blue",
         size: "0.5px" //0.5 or 0.5px
      }
  }]
};
```
#### IconSymbol3DLayer-with-LineCallout3D(3d)
```js
var symbol = {
  type: "point-3d",  // autocasts as new PointSymbol3D()
  symbolLayers: [{
    type: "icon",  // autocasts as new IconSymbol3DLayer()
    resource: {
      href: "CityHall.svg"
    },
    size: 20
  }],
  verticalOffset: {
    screenLength: 40,
    maxWorldLength: 100,
    minWorldLength: 20
  },
  callout: {
    type: "line", // autocasts as new LineCallout3D()
    size: 1.5,
    color: "white",
    border: {
      color: "black"
    }
  }
})
```
#### ObjectSymbol3DLayer(3d)
```js
const symbol = {
  type: "point-3d",   // autocasts as new PointSymbol3D()
  symbolLayers: [{
    type: "object",  // autocasts as new ObjectSymbol3DLayer()
    anchor: "origin",
    anchorPosition : { x: -0.5, y: -0.5, z: -0.5 }
    castShadows :false
    width: 5,       // diameter of the object from east to west in meters
    height: 20,    // height of the object in meters
    depth: 15,    // diameter of the object from north to south in meters
    resource: { primitive: "cylinder" },
    resource: {
      href: "../3d-assets/model.gltf"
    },
    height: 3,
    material: {
      color: "red"
    }
  }]
}
`anchor`: 
The positioning of the symbol relative to the geometry. The default behavior (origin) depends on the resource:

For sphere, cube and diamond primitives, the origin is at the center.
For cylinder, cone, inverted-cone and tetrahedron primitives, the origin is at the bottom.
For href resources, the origin coincides with the origin of the 3D model.
If anchor is set to relative, the anchor is defined by anchorPosition as a fraction of the symbol's bounding box.

Possible Values:"center"|"top"|"bottom"|"origin"|"relative"

`anchorPosition`： This property only applies when `anchor` is set to relative.

`castShadows` :indicates whether the symbol layer geometry casts shadows in the scene. Setting this property to false will disable shadows for the symbol layer even if direct shadows are enabled in SceneView.environment.
`resource`: The primitive shape (`primitive`) or external 3D model (`href`) used to visualize the points.
```
#### ObjectSymbol3DLayer-with-LineCallout3D(3d)
```js
const symbol = {
  type: "point-3d",   // autocasts as new PointSymbol3D()
  symbolLayers: [{
    type: "object",  // autocasts as new ObjectSymbol3DLayer()
    anchor: "origin",
    anchorPosition : { x: -0.5, y: -0.5, z: -0.5 }
    castShadows :false
    width: 5,       // diameter of the object from east to west in meters
    height: 20,    // height of the object in meters
    depth: 15,    // diameter of the object from north to south in meters
    resource: { primitive: "cylinder" },
    resource: {
      href: "../3d-assets/model.gltf"
    },
    height: 3,
    material: {
      color: "red"
    }
  }],
  verticalOffset: {
    screenLength: 40,
    maxWorldLength: 100,
    minWorldLength: 20
  },
  callout: {
    type: "line", // autocasts as new LineCallout3D()
    size: 1.5,
    color: "white",
    border: {
      color: "black"
    }
  }
}
```
### LineSymbol
#### SimpleLineSymbol(2d/3d)
```js
var symbol = {
  type: "simple-line", 
  color: "lightblue",
  width: "2px",         
  cap:  "square",        //Possible Values:"butt"|"round"|"square"
  join:  "bevel",       //Possible Values:"miter"|"round"|"bevel"
  miterLimit: 2,       //This property is currently not supported in 3D SceneViews.
  style: "short-dot"  //This property is currently not supported in 3D SceneViews.
  marker: {           //This property is currently not supported in 3D SceneViews.
   color: "blue",
   placement: "begin",
   style: "diamond"
};

`style`: Possible Values:"dash"|"dash-dot"|"dot"|"long-dash"|"long-dash-dot"|"long-dash-dot-dot"|"none"|"short-dash"|"short-dash-dot"|"short-dash-dot-dot"|"short-dot"|"solid"
```

#### LineSymbol3DLayer(3d)
```js
const symbol = {
  type: "line-3d",  // autocasts as new LineSymbol3D()
  symbolLayers: [{
    type: "line",  // autocasts as new LineSymbol3DLayer()
    size: 2,  // points
    material: { color: "black" },
    cap: "round",   //Default Value:butt Possible Values:"butt"|"round"|"square"
    join: "round"  //Default Value:miter   Possible Values:"miter"|"round"|"bevel"
  }]
});
```
#### PathSymbol3DLayer(3d)
```js
const stripPath = {
  type: "line-3d",  // autocasts as new LineSymbol3D()
  symbolLayers: [{
    type: "path",  // autocasts as new PathSymbol3DLayer()
    anchor:"center",        //Defines offset of the path cross section relative to the Polyline geometry. Possible Values:"center"|"bottom"|"top"  Default Value:"center"
    profile: "quad",  // creates a rectangular shape
    width: 20,  // path width in meters
    height: 5,  // path height in meters
    material: { color: "#ff7380" },
    cap: "square", //Possible Values:"none"|"butt"|"square"|"round"  Default Value:"butt"
    join: "miter"  //Possible Values:"miter"|"bevel"|"round"  Default Value:"miter"
    castShadows: false, // symbolLayer.castShadows = false;
    profile:"circle"  //Possible Values:"circle"|"quad"   Default Value:"circle"
    profileRotation: "heading"  //Defines how the profile is rotated as it is extruded along the Polyline geometry.  Possible Values:"heading"|"all"  Default Value:"all"
  }]
};
```
### FillSymbol
#### SimpleFillSymbol(2d/3d)
```js
const symbol = {
  type: "simple-fill",  // autocasts as new SimpleFillSymbol()
  color: [ 51,51, 204, 0.9 ],
  style: "solid",   //Possible Values:"backward-diagonal"|"cross"|"diagonal-cross"|"forward-diagonal"|"horizontal"|"none"|"solid"|"vertical" Default Value:solid This property is currently not supported in 3D SceneViews.
  outline: {  // autocasts as new SimpleLineSymbol()
    color: "white",
    width: 1
  }
};
```
#### PictureFillSymbol(2d/3d)
```js
const symbol = {
  type: "picture-fill",  // autocasts as new PictureFillSymbol()
  url: "https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png", //The URL to the image.
  width: "24px",   //The width of the image in points.
  height: "24px",  //The height of the image in points.
  outline: {      // autocasts as new SimpleLineSymbol()
    style: "solid"，
    color: [128, 128, 128, 0.5],
    width: "0.5px"
  },
  xoffset:6 ,  // 6 or 6px or 6pt ,	The offset on the x-axis in points.more details	
  xscale: 1	,   //	The scale factor on the x axis of the symbol.more details
  yoffset: 0,	//	The offset on the y-axis in pixels or points.more details
  yscale:1	,  //1 or 1px or 1pt ,The scale factor on the y axis of the symbol.  
};
```
#### FillSymbol3DLayer(3d)
```js
var symbol = {
  type: "polygon-3d",  // autocasts as new PolygonSymbol3D()
  symbolLayers: [{
    type: "fill",    // autocasts as new FillSymbol3DLayer()
    material: { color: "red" }
  }]
};
```
#### MeshSymbol3D(3d)
```js
const symbol = {
  type: 'mesh-3d',
  symbolLayers: [{
    type: 'fill',
    material: {
      color: [255, 255, 255, 0.6],
      colorMixMode: 'replace'
    },
    edges: {
      type: 'solid',
      color: [0, 0, 0, 0.6],
      size: 1
    }
  }]
}
```
#### ExtrudeSymbol3DLayer(3d)
```js
var symbol = {
  type: "polygon-3d",  // autocasts as new PolygonSymbol3D()
  symbolLayers: [{
    type: "extrude",  // autocasts as new ExtrudeSymbol3DLayer()
    castShadows:false, //Default Value:true
    size: 100000,  // 100,000 meters in height
    material: { color: "red" },
    edges: {
    type: "solid", // autocasts as new SolidEdges3D()
    color: [50, 50, 50, 0.5]
   }
  }]
};
```
### TextSymbol
#### TextSymbol(2/3d)
```js
var textSymbol = {
  type: "text",  // autocasts as new TextSymbol()
  color: "white",
  angle: 0,  //This property is currently not supported in 3D SceneViews.
  haloColor: "black",
  haloSize: "1px",
  text: "You are here",
  xoffset: 3,
  yoffset: 3,
  haloColor:[51, 204, 51, 0.3],
  haloSize: 1,
  horizontalAlignment:'center' //This property is not currently supported in 3D SceneViews
  backgroundColor:[51, 204, 51, 0.3], //the border color of the label's bounding box. This property is only supported for MapImageLayer.
  borderLineColor:[51, 204, 51, 0.3],   //the border color of the label's bounding box. This property is only supported for MapImageLayer.
  borderLineSize: 2,  //the border color of the label's bounding box. This property is only supported for MapImageLayer.
  kerning:true,  //Determines whether to adjust the spacing between characters in the text string.
  lineHeight:1.0,   //This property is currently not supported in 3D SceneViews.
  rotated:1.0,  //this property is currently not supported in 3D SceneViews.
  verticalAlignment:'baseline', // This property is currently not supported in 3D SceneViews. Possible Values:"baseline"|"top"|"middle"|"bottom"
  xoffset:0,   //This property is currently not supported in 3D SceneViews.
  yoffset:0, //This property is currently not supported in 3D SceneViews.
  font: {  // autocasts as new Font()
    size: 12,
    family: "Josefin Slab",
    weight: "bold"
  }
};
```
#### TextSymbol3DLayer(3d)
```js
 const symbol= {
    type: "label-3d",  // autocasts as new LabelSymbol3D()
    symbolLayers: [{
      type: "text",  // autocasts as new TextSymbol3DLayer()
      material: { color: [ 49,163,84 ] },
      size: 12,  // points
      font:16,
      halo : {
           color: [255, 255, 255, 0.8], // autocasts as Color
           size: 2
       }
    }]
```
### WaterSymbol3DLayer
```js
const symbol ={
      type: "polygon-3d",
      symbolLayers: [{
        type: "water",
        waveDirection: 180,
        color: "#5975a3",
        waveStrength: "moderate",
        waterbodySize: "small"
      }]
}
```
### renderer
####  Simplerenderer
 Simplerenderer渲染type为simple, symbol 可按点、线、面二三维场景按需进行符号选择。
 ```js
 //for simple-marker 
 const simplerenderer = {
    type: 'simple',
    symbol: {
     type: "simple-marker",
     style: "square",
     color: "blue",
     path: '',  //The SVG path of the icon. This property works only in 2D. IE11 is not supported.
     size: "8px",    // 8 or 8px or 8pt
     outline: {  
       color: [ 255, 255, 0 ],
       width: 3
     },
     angle: 0 , // This property is currently not supported in 3D.
     xoffset:0,
     yoffset:0
    }
  }
 ```
 ```js
 //for 3d model 
 const simplerenderer = {
    type: 'simple',
    symbol: {
      type: 'mesh-3d',
      symbolLayers: [{
        type: 'fill',
        material: {
          color: [255, 255, 255, 0.6],
          colorMixMode: 'replace'
        },
        edges: {
          type: 'solid',
          color: [0, 0, 0, 0.6],
          size: 1
        }
      }]
    }
  }
 ```
####  unique-valuerenderer
Simplerenderer渲染type为unique-value, symbol可按点、线、面二三维场景按需进行符号选择，可根据字段值分类进行符号定义。
 ```js
  const  renderer={
      type: 'unique-value',
      field: 'ZONE',   //图层字段
      defaultLabel: '',
      defaultSymbol: {
        type: 'polygon-3d',
        symbolLayers: [{
          type: 'extrude',
          size: 10,
          material: {
            color: [51, 51, 204, 0.9]
          }
        }]
      },
      uniqueValueInfos: [{
        label: '罗泾港区',   //value 值标注
        value: '罗泾港区',  //字段值为'罗泾港区'符号
        symbol: {
          type: 'polygon-3d',
          symbolLayers: [{
            type: 'extrude',
            size: 10,
            material: {
              color: [0, 127, 14, 1]
            }
          }] 
        }
      }, {
        label: '黄浦江港区',  //value 值标注
        value: '黄浦江港区', //字段值为'黄浦江港区'符号
        symbol: {
          type: 'polygon-3d',
          symbolLayers: [{
            type: 'extrude',
            size: 10,
            material: {
              color: [255, 106, 0, 1]
            }
          }]
        }
      }, {
        label: '外高桥港区', //value 值标注
        value: '外高桥港区', //字段值为'外高桥港区'符号
        symbol: {
          type: 'polygon-3d',
          symbolLayers: [{
            type: 'extrude',
            size: 10,
            material: {
              color: [130, 56, 242, 1]
            }
          }]
        }
      }, {
        label: '洋山港区',    //value 值标注
        value: '洋山港区', //字段值为'洋山港区'符号
        symbol: {
          type: 'polygon-3d',
          symbolLayers: [{
            type: 'extrude',
            size: 10,
            material: {
              color: [0, 0, 0, 1]
            }
          }]
        }
      }]
    }
 ```