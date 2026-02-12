# 地图截图 (Screenshot)

`@amap/screenshot` 插件可将当前地图视图导出为 Canvas 或图片。使用前必须在初始化地图时传入 `WebGLParams.preserveDrawingBuffer: true`，否则导出结果会为空或黑屏。

## 1. 必备配置

**Critical**: Add `WebGLParams` when creating the map:

```javascript
const map = new AMap.Map('container', {
    center: [116.39, 39.90],
    zoom: 10,
    viewMode: '3D',
    pitch: 35,
    WebGLParams: {
        preserveDrawingBuffer: true  // Required for screenshot
    }
});
```

## 2. 加载插件

### CDN

Load AMap JS first, then the screenshot plugin:

```html
<script src="https://webapi.amap.com/maps?v=2.0&key=YOUR_KEY"></script>
<script src="https://cdn.jsdelivr.net/npm/@amap/screenshot/dist/index.js"></script>
```

### npm

```bash
npm install @amap/screenshot
```

```javascript
import { Screenshot } from '@amap/screenshot';
```

## 3. 基础用法

### CDN

```javascript
const screenshot = new AMap.Screenshot(map);
```

### npm

```javascript
const screenshot = new Screenshot(map);
```

## 4. API 方法

| Method | Parameters | Returns | Description |
|--------|------------|---------|-------------|
| `toCanvas()` | none | `Promise<HTMLCanvasElement>` | Returns the generated canvas element |
| `toDataURL(imageType?)` | `imageType`: `'image/png'` \| `'image/jpeg'`, default `'image/png'` | `Promise<string>` | Returns base64 data URL |
| `download(options)` | `{ filename: string, type?: imageType }` | `Promise<boolean>` | Downloads the image file |
| `destroy()` | none | void | Releases internal cached memory |

## 5. 完整示例

### 预览到 img 元素

```javascript
const screenshot = new AMap.Screenshot(map);

function captureMap() {
    screenshot.toDataURL().then(url => {
        document.getElementById('preview').setAttribute('src', url);
    });
}
```

### 下载 PNG

```javascript
screenshot.download({ filename: 'map-screenshot.png' }).then(success => {
    if (success) console.log('Download started');
});
```

### 下载 JPEG

```javascript
screenshot.download({
    filename: 'map-screenshot.jpg',
    type: 'image/jpeg'
}).then(success => {
    if (success) console.log('Download started');
});
```

### 获取 Canvas 进一步处理

```javascript
screenshot.toCanvas().then(canvas => {
    // Use canvas for cropping, filters, etc.
    const ctx = canvas.getContext('2d');
    // ...
});
```

### 资源释放

当不再需要截图实例时调用 `destroy()`：

```javascript
screenshot.destroy();
```

## 6. 注意事项

1. **WebGLParams**：未设置 `preserveDrawingBuffer: true` 时，缓冲区每帧会被清空，导出结果将为空或黑屏。
2. **内存释放**：组件卸载时调用 `destroy()` 释放缓存。
3. **3D 视图**：支持 2D 和 3D（`viewMode: '3D'`）地图视图。
