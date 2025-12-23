# 圣诞树 - 交互式粒子体验

使用 Three.js (WebGL)、GLSL 着色器逻辑和 Google MediaPipe 计算机视觉集成的交互式圣诞树项目。

## 功能特性

- 🎨 **视觉设计**：香槟金/奶油白配色方案，渐变文字，磨砂玻璃UI
- ✨ **粒子系统**：4000个粒子（1500主体+2500尘埃），多种几何形状
- 🖐️ **手势控制**：MediaPipe 手部追踪，捏合/握拳/张开手势识别
- 📸 **照片墙**：上传照片到3D场景，金色相框
- 🎄 **糖果手杖**：程序化生成红白斜纹纹理的3D糖果手杖
- 🔄 **三种模式**：树形螺旋、散落球体、照片聚焦
- 💡 **后期处理**：辉光特效（UnrealBloomPass），高反射环境

## 快速开始

### 使用 npm 运行

```bash
# 安装依赖
npm install

# 方法1：使用 http-server（推荐）
npm start
# 打开 http://localhost:8080

# 方法2：使用 serve
npm run dev
# 打开 http://localhost:3000

# 方法3：使用 Express 服务器
npm run server
# 打开 http://localhost:3000

# 方法4：直接打开文件（某些功能可能需要本地服务器）
npm run open
```

### 直接运行
1. 双击 `圣诞树.html` 文件
2. 或使用支持 ES 模块的现代浏览器打开

## 系统要求

- **浏览器**：Chrome 90+ / Edge 90+ / Firefox 88+（支持 ES 模块和 WebGL2）
- **摄像头**：用于手势识别（可选，但推荐）
- **网络**：需要加载 CDN 资源（Three.js, MediaPipe）

## 操作指南

### 基本控制
- **H 键**：隐藏/显示 UI 控件
- **上传照片**：点击 "ADD MEMORIES" 按钮
- **手势控制**：
  - **捏合** 👌：聚焦模式（放大随机照片）
  - **握拳** ✊：树形模式（粒子排列成圣诞树）
  - **张开手** 🖐️：散落模式（粒子随机分布）
  - **移动手掌**：旋转 3D 场景

### 手势识别说明
1. 允许浏览器访问摄像头
2. 将手放在摄像头前（右下角有不可见预览）
3. 手势识别距离：建议 30-100cm

## 技术架构

### 核心依赖
```html
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/",
    "@mediapipe/tasks-vision": "https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.3/+esm"
  }
}
</script>
```

### 文件结构
```
圣诞树.html          # 单文件 HTML 应用（850 行）
package.json         # npm 配置和脚本
server.js           # Express 服务器
README.md           # 本文档
```

## 故障排除

### 常见问题

1. **模块导入错误**
   - 确保使用现代浏览器（Chrome/Edge）
   - 检查网络连接，CDN 资源需要访问
   - 如果遇到 CORS 问题，使用本地服务器（npm start）

2. **摄像头无法访问**
   - 检查浏览器权限设置
   - 确保没有其他应用占用摄像头
   - 尝试刷新页面重新请求权限

3. **手势识别不准确**
   - 确保良好的光照条件
   - 手部距离摄像头 30-100cm
   - 背景不要太复杂

4. **性能问题**
   - 关闭其他标签页释放 GPU 资源
   - 降低浏览器硬件加速设置
   - 减少浏览器扩展程序

### 错误修复
如果遇到 `PMREMGenerator` 导入错误，已修复：
```javascript
// 错误（已修复）
import { PMREMGenerator } from 'three/src/extras/PMREMGenerator.js';

// 正确
import { PMREMGenerator } from 'three';
```

## 开发说明

### 代码结构
- **单文件设计**：HTML + CSS + JavaScript 在一个文件中
- **ES6+ 模块**：使用 import/export，类结构
- **状态机模式**：TREE/SCATTER/FOCUS 三种状态
- **粒子系统**：基于用户数据（userData）管理状态

### 扩展可能性
1. 添加更多粒子类型（星形、雪花）
2. 实现音频可视化同步
3. 添加更多手势（滑动、旋转）
4. 集成 WebXR 支持（VR/AR）

## 许可证

MIT 许可证 - 详见项目文件

## 致谢

- [Three.js](https://threejs.org/) - 3D 图形库
- [Google MediaPipe](https://mediapipe.dev/) - 计算机视觉
- [jsDelivr](https://www.jsdelivr.com/) - CDN 服务
- [Google Fonts](https://fonts.google.com/) - 字体服务