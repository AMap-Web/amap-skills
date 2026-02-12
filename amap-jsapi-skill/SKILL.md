| 属性 | 值 |
| --- | --- |
| **name** | amap-jsapi-skill |
| **description** | 高德地图 JSAPI v2.0 (WebGL) 开发技能。涵盖地图生命周期管理、强制安全配置、3D 视图控制、覆盖物绘制及 LBS 服务集成。 |
| **license** | MIT |
| **version** | 1.0.0 |

# 高德地图 JSAPI v2.0 开发技能
本指南包含地图初始化、覆盖物、事件、图层等核心模块的 API 说明和代码示例，旨在帮助开发者快速集成高德地图并遵循正确的使用方式。
## 快速开始
### 1. 引入加载器
使用 script 标签加载 loader.js：
```bash
<script src="https://webapi.amap.com/loader.js"></script>
```
### 2. 安全密钥配置 (强制)
**重要**：自 v2.0 起，必须在加载地图前配置安全密钥，否则无法通过鉴权。详情及后端代理示例请参考 [安全策略](references/security.md)。
```javascript
// 在调用 AMapLoader.load 前执行
window._AMapSecurityConfig = {
  securityJsCode: '您的安全密钥', // 开发环境：明文设置
  // serviceHost: 'https://your-proxy-domain/_AMapService', // 生产环境：建议使用代理转发
};
```
### 3. 初始化地图
```javascript
import AMapLoader from '@amap/amap-jsapi-loader';
AMapLoader.load({
    key: '您的Web端开发者Key', // 必填
    version: '2.0',           // 指定版本
    plugins: ['AMap.Scale', 'AMap.ToolBar'] // 预加载插件
}).then((AMap) => {
    const map = new AMap.Map('container', {
        viewMode: '3D',       // 开启3D视图
        zoom: 11,             // 初始缩放级别
        center: [116.39, 39.90] // 初始中心点
    });
    map.addControl(new AMap.Scale());
}).catch(e => console.error(e));
```
## 场景示例
### 地图控制
- **生命周期**：`references/map-init.md` - 掌握 `load`、`Map` 实例创建及 `destroy` 销毁流程。
- **视图交互**：`references/view-control.md` - 控制 `zoom` (缩放)、`center` (平移)、`pitch` (俯仰)、`rotation` (旋转)。
### 覆盖物绘制
- **点标记**：`references/marker.md` - 使用 `Marker` (基础)、`LabelMarker` (海量避让) 标注位置。
- **矢量图形**：`references/vector-graphics.md` - 绘制 `Polyline` (轨迹、线)、`Polygon` (区域、面)、`Circle` (范围、圆)。
- **信息展示**：`references/info-window.md` - 通过 `InfoWindow` 展示详细信息。
- **右键菜单**：`references/context-menu.md` - 自定义地图或覆盖物的右键交互。
### 图层管理
- **基础图层**：`references/layers.md` - 标准、卫星、路网及 3D 楼块图层。
- **自有数据**：`references/custom-layers.md` - 集成 `Canvas`、`WMS/WMTS`, `GLCustomLayer` 地图上叠加 Canvas、WMS图层、 Threejs图层。
### 服务与插件
- **LBS 服务**：
    - `references/geocoder.md` - 地理编码/逆地理编码（地址/坐标互转）。
    - `references/routing.md` - 路径规划（驾车/步行/公交）。
    - `references/search.md` - POI 搜索与输入提示。
- **地图截图**：`references/screenshot.md` - 使用 `@amap/screenshot` [插件](https://github.com/AMap-Web/amap-screenshot) 将当前地图视图导出为 Canvas 或图片（需配合 `WebGLParams.preserveDrawingBuffer`）。
- **事件系统**：`references/events.md` - 响应点击、拖拽、缩放等交互事件。
## 最佳实践
1. **安全第一**：生产环境务必使用代理服务器转发 `serviceHost`，避免 `securityJsCode` 泄露。
2. **按需加载**：仅在 `plugins` 中声明需要的插件，减少首屏资源体积。
3. **资源释放**：组件卸载时务必调用 `map.destroy()`，防止 WebGL 上下文内存泄漏。


## API Reference

JSAPI 文档分为以下几个类别：

### [Foundation Classes](references/api/foundation.md)
LngLat / Bounds / Pixel / Size

### [Information Window](references/api/info-window.md)
InfoWindow

### [Events](references/api/events.md)
Event

### [Map](references/api/map.md)
Map / MapsEvent

### [Official Layers](references/api/layers-official.md)
TileLayer / Traffic / Satellite / RoadNet / Buildings / DistrictLayer / IndoorMap

### [Standard Layers](references/api/layers-standard.md)
WMS / WMTS / MapboxVectorTileLayer

### [Custom Layers](references/api/layers-custom.md)
HeatMap / VectorLayer / LabelsLayer / CustomLayer / Flexible / ImageLayer / CanvasLayer / GLCustomLayer

### [Markers](references/api/marker.md)
Marker / Text / Icon / LabelMarker / ElasticMarker / MarkerCluster / MassMarks / MoveAnimation / AnimationCallback / EasingCallback

### [Context Menu](references/api/context-menu.md)
ContextMenu

### [Vector Graphics](references/api/vector-graphics.md)
Polygon / Polyline / BezierCurve / Circle / CircleMarker / Ellipse / Rectangle / GeoJSON

### [Overlay Groups](references/api/overlay-group.md)
LayerGroup / OverlayGroup

### [Controls](references/api/controls.md)
Control / Scale / ToolBar / ControlBar / MapType / HawkEye

### [Tools](references/api/tools.md)
RangingTool / MouseTool / PolygonEditor / PolylineEditor / CircleEditor / BezierCurveEditor / EllipseEditor / RectangleEditor

### [Services](references/api/services.md)
WebService / WebServiceCallback

### [Search](references/api/search.md)
AutoComplete / AutoCompleteSearchCallback / PlaceSearch / searchCallback / CloudDataSearch / CloudDataSearchCallback

### [Geocoder](references/api/geocoder.md)
Geocoder / GeocoderCallback / ReGeocoderCallback / convertFrom

### [Routing](references/api/routing.md)
Driving / DrivingCallback / DrivingResult / DriveStepBasic / DriveStepDetail / TruckDriving / Walking / WalkingCallback / WalkingResult / Transfer / TransferCallback / TransferResult / Riding / RidingCallback / RidingResult / DragRoute / DragRouteTruck / GraspRoad / GraspRoadCallback

### [Other Services](references/api/services-other.md)
DistrictSearch / Weather / WeatherLiveResult / WeatherForecastResult / StationSearch / LineSearch

### [Screenshot](references/screenshot.md)
Screenshot (toCanvas / toDataURL / download / destroy)

### [Geolocation](references/api/geolocation.md)
Geolocation / GeolocationCallBack / GeolocationResult / CitySearch

### [Common Library](references/api/common.md)
GeometryUtil / DomUtil / Browser / Util

## 使用 skills 必须遵循的铁律
1. **校验生成代码可用性**：自我验证校验代码生成的可用性，一定是可以正常运行的。
## 如何使用
1. 如果有相近的“场景示例”那么去阅读场景示例，再阅读场景示例中的涉及的类的api文档。再结合描述/场景示例/api 去完成任务。
2. 在最终的完成任务前，检查用的api用法是否符合文档。
