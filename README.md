# JSAPI Skills User Guide

[🇨🇳 中文文档](./README_zh.md)

## Product Introduction

**AMap JSAPI Skills** is a set of AI programming skill packages designed specifically for AI IDEs. It integrates the official documentation, best practices, and code templates of AMap JavaScript API v2.0 into structured skill files, enabling AI coding tools like Cursor, Claude, and Cline to:

*   **Accurately understand** how to use AMap APIs
    
*   **Automatically generate** map code that complies with official specifications
    
*   **Proactively avoid** common development pitfalls and security issues
    
*   **Provide** verified complete code examples
    

Whether you're a beginner or an experienced map developer, this Skills package can significantly improve your development efficiency.

## Quick Start

### Install via npx skills (Recommended)

```bash
# Install the skill to your project
npx skills add AMap-Web/amap-skills

# Or install globally
npx skills add AMap-Web/amap-skills -g
```

### Alternative: Git Clone

```bash
# Clone the repository locally
git clone https://github.com/AMap-Web/amap-skills.git

# Enter the directory
cd amap-skills
```

### Manual Configuration for Cursor

Cursor supports loading custom skills through the `.cursor/skills/` directory.

```bash
# Create skills directory
mkdir -p .cursor/skills

# Copy or link the skill
cp -r /path/to/amap-skills/skills .cursor/skills/amap-jsapi
```

### Manual Configuration for Claude Code

```bash
# Create skills directory
mkdir -p .agents/skills

# Copy or link the skill
cp -r /path/to/amap-skills/skills .agents/skills/amap-jsapi
```

## Directory Structure

```text
amap-skills/
├── skills/                     # Skill directory
│   ├── SKILL.md               # Main skill file (AI entry point)
│   └── references/            # Detailed reference documentation
│       ├── map-init.md        # Map initialization
│       ├── view-control.md    # View control
│       ├── marker.md          # Markers
│       ├── vector-graphics.md # Vector graphics
│       ├── info-window.md     # Info window
│       ├── context-menu.md    # Context menu
│       ├── layers.md          # Base layers
│       ├── custom-layers.md   # Custom layers
│       ├── events.md          # Event system
│       ├── geocoder.md        # Geocoding
│       ├── routing.md         # Route planning
│       ├── search.md          # POI search
│       ├── security.md        # Security configuration
│       └── api/               # API reference documentation
└── resource/                  # Images and resources
```

## Usage Examples

### Example 1: Basic Map

Describe your requirements to Cursor AI:

```text
Create a React component that displays an AMap, centered on Shanghai Bund, zoom level 15, using the dark phantom theme style

```

### Example 2: Add Markers

```text
Add 3 markers on the map, marking Beijing, Shanghai, and Guangzhou respectively. When clicking a marker, display an info window with the city name

```

### Example 3: Route Planning

```text
Implement driving route planning from Beijing to Shanghai, draw the route on the map, and display estimated driving time and distance

```

### Example 4: POI Search

```text
Add a search box. After user enters keywords, search for restaurants within 5 kilometers on the map and display the search results

```

## Best Practices

### Security Configuration

```javascript
// Development environment: Direct configuration (for local debugging only)
window._AMapSecurityConfig = {
  securityJsCode: 'Your security key',
};

// Production environment: Use proxy forwarding (Recommended)
window._AMapSecurityConfig = {
  serviceHost: 'https://your-domain.com/_AMapService',
};

```

### Resource Cleanup

```javascript
// Always destroy the map when component unmounts to prevent memory leaks
useEffect(() => {
  // Initialize map...
  
  return () => {
    map?.destroy();
  };
}, []);

```

### Load Plugins On Demand

```javascript
// Only load required plugins to reduce initial resource size
AMapLoader.load({
  key: 'Your Key',
  version: '2.0',
  plugins: ['AMap.Scale', 'AMap.Geocoder'], // Declare as needed
});

```

## FAQ

### Q: Map shows white screen or INVALID\_USER\_KEY error

**A:** Please check:

1.  Whether `window._AMapSecurityConfig` is configured before `AMapLoader.load`
    
2.  Whether Key and security key match
    
3.  Whether Key is enabled in AMap console
    

### Q: Cursor AI doesn't use knowledge from Skill

**A:** Please ensure:

1.  Skill files are placed in the `.cursor/skills/` directory
    
2.  `SKILL.md` file exists and is correctly formatted
    
3.  Try explicitly mentioning "AMap" in your questions
    

### Q: How to update Skill?

If using the copy method, you need to re-copy the latest files. If using `npx skills add`, you can reinstall to get the latest version.

## Related Links

*   [AMap JSAPI Official Documentation](https://lbs.amap.com/api/jsapi-v2/summary/)
    
*   [AMap Open Platform Console](https://console.amap.com/)
    
*   [Cursor Official Documentation](https://docs.cursor.com/)
    
*   [JSAPI Demo Center](https://lbs.amap.com/demo/list/jsapi-v2)
    

**Let AI become your map development assistant, starting today!**
