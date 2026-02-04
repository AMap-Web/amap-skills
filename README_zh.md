# JSAPI  Skills 使用文档

## 产品介绍

**高德地图 JSAPI Skills** 是一套专为 AI  IDE 设计的 AI 编程技能包。它将高德地图 JavaScript API v2.0 的官方文档、最佳实践和代码模板整合为结构化的技能文件，使 Cursor、Claude、Cline  的 AI  Codiing 工具能够：

*   **精准理解**高德地图 API 的使用方法
    
*   **自动生成**符合官方规范的地图代码
    
*   **主动避免**常见的开发陷阱和安全问题
    
*   **提供**经过验证的完整代码示例
    

无论您是地图开发新手还是资深开发者，这套 Skills 都能显著提升您的开发效率。

## 产品特点

### 精准的 API 知识

基于高德地图 JSAPI v2.0 官方文档构建，覆盖完整的 API 能力，确保生成的代码符合最新规范。

### 安全优先

内置安全配置指南，自动提醒开发者配置安全密钥，避免因鉴权问题导致地图白屏。生产环境推荐代理方案，保护您的密钥安全。

### 模块化设计

按功能模块组织文档（地图控制、覆盖物、图层、LBS服务），AI 可按需引用，精准回答您的问题。

### 代码可验证

所有代码示例均经过验证，AI 会自我校验生成代码的可用性，确保输出可以正常运行。

## 能力介绍

### 地图控制

| **能力** | **说明** |
| --- | --- |
| 地图初始化 | 异步加载、3D/2D 视图、地图样式配置 |
| 视图交互 | 缩放、平移、俯仰角、旋转控制 |
| 生命周期管理 | 加载完成回调、资源销毁释放 |
| 地图控件 | 比例尺、工具条、鹰眼、图层切换 |

### 覆盖物绘制

| **能力** | **说明** |
| --- | --- |
| 点标记 (Marker) | 基础标记、自定义图标、DOM 内容 |
| 海量标注 (LabelMarker) | 支持万级点位、文字图标避让 |
| 矢量图形 | 折线、多边形、圆形、矩形 |
| 信息窗体 (InfoWindow) | 默认信息窗、自定义内容窗体 |
| 右键菜单 | 自定义地图/覆盖物右键交互 |

### 图层管理

| **能力** | **说明** |
| --- | --- |
| 标准图层 | 标准地图、卫星图、路网图 |
| 3D 图层 | 建筑楼块、室内地图 |
| 自有数据图层 | Canvas 图层、WMS/WMTS 服务 |

### LBS 服务与插件

| **能力** | **说明** |
| --- | --- |
| 地理编码 | 地址转坐标、坐标转地址 |
| 路径规划 | 驾车、步行、骑行、公交路线 |
| POI 搜索 | 周边搜索、关键词搜索、输入提示 |
| 事件系统 | 点击、拖拽、缩放等交互事件 |

## 快速接入

### 第一步：获取 Skills 文件

#### 方式一：Git Clone（推荐）

```bash
# 克隆仓库到本地
git clone https://github.com/AMap-Web/amap-skills.git

# 进入目录
cd amap-skills

```

#### 方式二：直接下载

从 [Releases](https://github.com/AMap-Web/amap-skills/releases) 页面下载最新版本的压缩包并解压。

### 第二步：在 Cursor 中配置 Skill

Cursor 支持通过 `.cursor/skills/` 目录加载自定义技能。

#### 2.1 创建 Skills 目录

在您的项目根目录下创建 `.cursor/skills/` 文件夹：

```bash
mkdir -p .cursor/skills

```

#### 2.2 链接或复制 Skill 文件

**方式一：软链接（推荐，方便更新）**

```bash
# macOS / Linux
ln -s /path/to/amap-skills/amap-jsapi-skill .cursor/skills/amap-jsapi-skill

# Windows (以管理员身份运行 CMD)
mklink /D .cursor\skills\amap-jsapi-skill C:\path\to\amap-skills\amap-jsapi-skill

```

**方式二：直接复制**

```bash
cp -r /path/to/amap-skills/amap-jsapi-skill .cursor/skills/

```

#### 2.3 项目目录结构

配置完成后，您的项目目录结构应该类似：

![image.png](./resource/contents.png)

```text
your-project/
├── .cursor/
│   └── skills/
│       └── amap-jsapi-skill/
│           ├── SKILL.md
|           └── api
|               |——map.md
|               |——layers.md
│           └── references/
│               ├── map-init.md
│               ├── marker.md
│               ├── security.md
│               └── ...
├── src/
├── package.json
└── ...

```

![image.png](./resource/cursor_skills.png)

### 第三步：验证配置

1.  打开 Cursor IDE
    
2.  打开您的项目
    
3.  按 `Cmd/Ctrl + L` 打开 AI Chat
    
4.  输入测试问题：
    

```text
帮使用高德 JSAPI  开发一个 POI 搜索与路径规划应用：
0. 地图ak在env.js文件中，使用这个作为地图ak
1. 起点搜索：右侧面板顶部搜索框，用户输入地址搜索，选择后在地图打点并跳转视角
2. 分类选择：搜索框下方显示分类 Tab（美食、娱乐、旅游、医院、超市等），分类数据从 JSON 配置文件读取。点击 Tab
展开二级菜单（如美食-火锅、烧烤、川菜等）
3. POI 列表：点击二级菜单项，以起点为中心进行周边搜索，结果显示在底部列表
4. POI 预览：点击列表项，地图高亮该 POI 并在左侧展示一个详情卡片，显示详情（名称、地址），提供"去这里"按钮
5. 路径规划：点击"去这里"，以起点和该 POI 为终点进行路径规划，默认驾车，支持切换步行/公交/骑行我创建一个高德地图，显示北京天安门的位置，并添加一个标记点

```

![image.png](./resource/demo_chat.png)

如果 AI 在思考过程能够正确使用 高德地图JSAPI的 skill 文件如上图过程并生成包含安全配置、的完整代码，说明 Skill 已成功加载，您可以正确配置JSAPI key 浏览页面。

![image.png](./resource/demo.png)

### 第四步：申请高德开发者 Key

如果您还没有高德地图开发者账号，请按以下步骤申请：

1.  访问 [高德开放平台控制台](https://console.amap.com/)
    
2.  注册并登录账号
    
3.  进入「应用管理」→「我的应用」
    
4.  点击「创建新应用」
    
5.  添加 Key，选择「Web端(JS API)」服务
    
6.  获取 **Key** 和 **安全密钥**
    

> **重要**：自 2021 年 12 月起，高德地图 JSAPI v2.0 强制要求配置安全密钥，否则地图将无法加载。

## 使用示例

### 示例 1：基础地图

向 Cursor AI 描述您的需求：

```text
创建一个 React 组件，显示高德地图，中心点在上海外滩，缩放级别 15，使用幻影黑主题样式

```

### 示例 2：添加标记点

```text
在地图上添加 3 个标记点，分别标注北京、上海、广州，点击标记时显示城市名称的信息窗体

```

### 示例 3：路径规划

```text
实现从北京到上海的驾车路径规划功能，在地图上绘制路线，并显示预计行驶时间和距离

```

### 示例 4：POI 搜索

```text
添加一个搜索框，用户输入关键词后在地图上搜索周边 5 公里范围内的餐厅，并显示搜索结果

```

## 最佳实践

### 安全配置

```javascript
// 开发环境：直接配置（仅用于本地调试）
window._AMapSecurityConfig = {
  securityJsCode: '您的安全密钥',
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
  key: '您的Key',
  version: '2.0',
  plugins: ['AMap.Scale', 'AMap.Geocoder'], // 按需声明
});

```

## 目录结构

```text
amap-jsapi-skill/
├── SKILL.md                    # 技能主文件（AI 入口）
└── references/                 # 详细参考文档
    ├── map-init.md             # 地图初始化
    ├── view-control.md         # 视图控制
    ├── marker.md               # 点标记
    ├── vector-graphics.md      # 矢量图形
    ├── info-window.md          # 信息窗体
    ├── context-menu.md         # 右键菜单
    ├── layers.md               # 基础图层
    ├── custom-layers.md        # 自定义图层
    ├── events.md               # 事件系统
    ├── geocoder.md             # 地理编码
    ├── routing.md              # 路径规划
    ├── search.md               # POI 搜索
    └── security.md             # 安全配置

```

## 常见问题

### Q: 地图显示白屏或报错 INVALID\_USER\_KEY

**A:** 请检查：

1.  是否在 `AMapLoader.load` 之前配置了 `window._AMapSecurityConfig`
    
2.  Key 和安全密钥是否匹配
    
3.  Key 是否已在高德控制台启用
    

### Q: Cursor AI 没有使用 Skill 中的知识

**A:** 请确保：

1.  Skill 文件放置在 `.cursor/skills/` 目录下
    
2.  `SKILL.md` 文件存在且格式正确
    
3.  尝试在提问时明确提及"高德地图"或"AMap"
    

### Q: 如何更新 Skill？

如果使用复制方式，需要重新复制最新文件。

## 相关链接

*   [高德地图 JSAPI 官方文档](https://lbs.amap.com/api/jsapi-v2/summary/)
    
*   [高德开放平台控制台](https://console.amap.com/)
    
*   [Cursor 官方文档](https://docs.cursor.com/)
    
*   [JSAPI 示例中心](https://lbs.amap.com/demo/list/jsapi-v2)
    

**让 AI 成为您的地图开发助手，从今天开始！**
