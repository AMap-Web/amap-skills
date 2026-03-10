# JSAPI Skills 用户指南

[🇺🇸 English Documentation](./README.md)

## 产品介绍

**AMap JSAPI Skills** 是一套专为 AI IDE 设计的 AI 编程技能包。它将高德地图 JavaScript API v2.0 的官方文档、最佳实践和代码模板整合成结构化的技能文件，让 Cursor、Claude、Cline 等 AI 编程工具能够：

*   **准确理解** 高德地图 API 的使用方法
    
*   **自动生成** 符合官方规范的地图代码
    
*   **主动规避** 常见开发陷阱和安全问题
    
*   **提供** 经过验证的完整代码示例
    

无论你是初学者还是经验丰富的地图开发者，这套 Skills 都能显著提升你的开发效率。

## 产品特性

### 精准的 API 知识

基于高德 JSAPI v2.0 官方文档构建，覆盖完整 API 能力，确保生成的代码符合最新规范。

### 安全优先

内置安全配置指南，自动提醒开发者配置安全密钥，避免因鉴权问题导致地图白屏。生产环境推荐代理方案，保护密钥安全。

### 模块化设计

文档按功能模块（地图控制、覆盖物、图层、LBS 服务）组织，AI 可按需引用，精准回答你的问题。

### 可验证的代码

所有代码示例均经过验证，AI 会自我校验生成代码的可用性，确保输出可正常运行。

## 能力覆盖

### 地图控制

| **能力** | **说明** |
| --- | --- |
| 地图初始化 | 异步加载、3D/2D 视图、地图样式配置 |
| 视图交互 | 缩放、平移、俯仰、旋转控制 |
| 生命周期管理 | 加载完成回调、资源销毁 |
| 地图控件 | 比例尺、工具栏、鹰眼、图层切换 |

### 覆盖物绘制

| **能力** | **说明** |
| --- | --- |
| Marker | 基础点标记、自定义图标、DOM 内容 |
| LabelMarker | 支持海量点位、文本/图标避让 |
| 矢量图形 | 折线、多边形、圆形、矩形 |
| InfoWindow | 默认信息窗体、自定义内容窗体 |
| Context Menu | 自定义地图/覆盖物右键交互 |

### 图层管理

| **能力** | **说明** |
| --- | --- |
| 标准图层 | 标准地图、卫星图、路网 |
| 3D 图层 | 楼块、室内地图 |
| 自定义数据图层 | Canvas 图层、WMS/WMTS 服务 |

### LBS 服务与插件

| **能力** | **说明** |
| --- | --- |
| 地理编码 | 地址转坐标、坐标转地址 |
| 路径规划 | 驾车、步行、骑行、公交路线 |
| POI 搜索 | 周边搜索、关键字搜索、输入提示 |
| 事件系统 | 点击、拖拽、缩放等交互事件 |

## 快速开始

### 通过 npx skills 安装（推荐）

```bash
# 安装到当前项目
npx skills add AMap-Web/amap-skills

# 或全局安装
npx skills add AMap-Web/amap-skills -g
```

### 方式二：Git Clone

```bash
# 克隆仓库到本地
git clone https://github.com/AMap-Web/amap-skills.git

# 进入目录
cd amap-skills
```

### 方式三：手动配置（Cursor）

Cursor 支持通过 `.cursor/skills/` 目录加载自定义技能。

```bash
# 创建技能目录
mkdir -p .cursor/skills

# 复制或链接技能
cp -r /path/to/amap-skills/skills .cursor/skills/amap-jsapi
```

### 方式四：手动配置（Claude Code）

```bash
# 创建技能目录
mkdir -p .agents/skills

# 复制或链接技能
cp -r /path/to/amap-skills/skills .agents/skills/amap-jsapi
```

### 目录结构

配置完成后，你的项目目录结构应该如下：

```text
your-project/
├── .cursor/                    # 或 .agents/
│   └── skills/
│       └── amap-jsapi/
│           ├── SKILL.md
│           └── references/
│               ├── map-init.md
│               ├── marker.md
│               ├── security.md
│               └── ...
├── src/
├── package.json
└── ...
```

## 使用示例

### 示例 1：基础地图

向 Cursor AI 描述需求：

```text
帮我用 AMap JSAPI 开发一个 POI 搜索与路线规划应用：
0. 地图 API key 在 env.js 文件中，使用这个作为地图密钥
1. 起点搜索：右侧面板顶部搜索框，用户输入地址搜索，选择后在地图标记并跳转查看
2. 分类选择：搜索框下方分类标签（餐饮、娱乐、旅游、医院、超市等），分类数据从 JSON 配置文件读取。点击标签展开二级菜单（如餐饮 - 火锅、烧烤、川菜等）
3. POI 列表：点击二级菜单项，以起点为中心进行周边搜索，结果展示在底部列表
4. POI 预览：点击列表项，地图高亮该 POI 并在左侧显示详情卡片（名称、地址），有"去这里"按钮
5. 路线规划：点击"去这里"，以起点为起点，该 POI 为终点规划路线，默认驾车，支持切换步行/公交/骑行
```

如果 AI 在思考过程中正确使用了 AMap JSAPI 技能文件，并生成了包含安全配置的完整代码，说明 Skill 已成功加载。

## 最佳实践

### 安全配置

```javascript
// 开发环境：直接配置（仅供本地调试）
window._AMapSecurityConfig = {
  securityJsCode: '你的安全密钥',
};

// 生产环境：使用代理转发（推荐）
window._AMapSecurityConfig = {
  serviceHost: 'https://your-domain.com/_AMapService',
};

```

### 资源释放

```javascript
// 组件卸载时务必销毁地图，防止内存泄漏
useEffect(() => {
  // 初始化地图...
  
  return () => {
    map?.destroy();
  };
}, []);

```

### 按需加载插件

```javascript
// 只加载需要的插件，减少首屏资源体积
AMapLoader.load({
  key: '你的 Key',
  version: '2.0',
  plugins: ['AMap.Scale', 'AMap.Geocoder'], // 按需声明
});

```

## 目录结构

```text
amap-skills/
├── skills/                     # 技能目录
│   ├── SKILL.md               # 主技能文件（AI 入口）
│   └── references/            # 详细参考文档
│       ├── map-init.md        # 地图初始化
│       ├── view-control.md    # 视图控制
│       ├── marker.md          # 点标记
│       ├── vector-graphics.md # 矢量图形
│       ├── info-window.md     # 信息窗体
│       ├── context-menu.md    # 右键菜单
│       ├── layers.md          # 基础图层
│       ├── custom-layers.md   # 自定义图层
│       ├── events.md          # 事件系统
│       ├── geocoder.md        # 地理编码
│       ├── routing.md         # 路径规划
│       ├── search.md          # POI 搜索
│       ├── security.md        # 安全配置
│       └── api/               # API 参考文档
└── resource/                  # 图片和资源
```

## 常见问题

### Q: 地图白屏或提示 INVALID\_USER\_KEY 错误

**A:** 请检查：

1.  是否在 `AMapLoader.load` 之前配置了 `window._AMapSecurityConfig`
    
2.  Key 和安全密钥是否匹配
    
3.  Key 是否在控制台启用
    

### Q: Cursor AI 没有使用 Skill 中的知识

**A:** 请确保：

1.  Skill 文件放置在 `.cursor/skills/` 目录下
    
2.  `SKILL.md` 文件存在且格式正确
    
3.  尝试在问题中明确提及"高德地图"
    

### Q: 如何更新 Skill？

如果使用复制方式，需要重新复制最新文件。如果使用 `npx skills add`，可以重新安装获取最新版本。

## 相关链接

*   [高德 JSAPI 官方文档](https://lbs.amap.com/api/jsapi-v2/summary/)
    
*   [高德开放平台控制台](https://console.amap.com/)
    
*   [Cursor 官方文档](https://docs.cursor.com/)
    
*   [JSAPI 示例中心](https://lbs.amap.com/demo/list/jsapi-v2)
    

**让 AI 成为你的地图开发助手，从今天开始！**
