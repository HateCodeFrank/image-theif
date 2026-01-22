# 🎨 ImageTheif

一个图片配色提取工具，使用 K-means 聚类算法提取图片主色调，并生成渐变背景。

## ✨ 特性

- 🎯 **智能颜色提取**：使用 K-means 聚类算法精准提取图片主色调
- 🌈 **动态渐变背景**：生成类似 Apple Music 的流动渐变效果（拙劣模仿）
- 📊 **颜色占比分析**：自动计算每个颜色的占比
- 🎨 **多种颜色格式**：支持 RGB、HEX、HSL 格式输出
- ⚡ **高性能**：智能采样算法，快速处理大图
- 🎭 **TypeScript**：完整的类型支持
- 📦 **零依赖**：纯 Canvas API 实现

## 🚀 快速开始

### 安装

```bash
npm install image-theif
```

### 基础用法

```typescript
import { ImageTheif } from 'image-theif';

// 创建实例
const theif = new ImageTheif({
  colorCount: 6,      // 提取颜色数量
  quality: 10,        // 采样质量 (1-10)
  el: wrapperElement  // 渐变背景容器（可选）
});

// 提取颜色
const colors = await theif.extract(imageFile);

// 输出格式
[
  {
    rgb: [255, 100, 50],
    hex: '#ff6432',
    hsl: [15, 100, 60],
    percentage: 35
  },
  // ...
]

// 创建渐变背景
theif.createGradientBackground(colors);

// 创建动态渐变背景
theif.createAnimatedGradientBackground(colors);
```

## 🎨 在线演示

[Live Demo](https://your-demo-url.com)

![Demo Screenshot](./screenshots/demo.png)

## 📖 API 文档

### `ImageTheif(options)`

创建提取器实例

**参数：**
- `colorCount?: number` - 提取颜色数量（默认 5）
- `quality?: number` - 采样质量 1-10（默认 10，值越小速度越快）
- `el?: HTMLElement` - 渐变背景容器元素

### `extract(source)`

提取图片主色调

**参数：**
- `source: File | string` - 图片文件或 URL

**返回：**
```typescript
Promise<ColorInfo[]>

interface ColorInfo {
  rgb: [number, number, number];
  hex: string;
  hsl: [number, number, number];
  percentage: number;
}
```

### `createGradientBackground(colors)`

创建静态渐变背景

**参数：**
- `colors: ColorInfo[]` - 颜色数组

**返回：**
- `HTMLCanvasElement`

### `createAnimatedGradientBackground(colors)`

创建动态流动渐变背景（Apple Music 风格）

**参数：**
- `colors: ColorInfo[]` - 颜色数组

**返回：**
- `HTMLCanvasElement`

### `stopAnimation()`

停止渐变动画

### `destroy()`

销毁实例并清理资源

## 🎯 使用场景

- 🎵 音乐播放器背景
- 🖼️ 图片查看器
- 🎨 设计工具配色板
- 📱 移动端主题色提取
- 🌐 网站动态主题

## 🔧 高级配置

```typescript
// 自定义采样和过滤
const theif = new ImageTheif({
  colorCount: 8,
  quality: 5,  // 降低质量提升性能
});

// 根据占比调整渐变强度
const colors = await theif.extract(image);
theif.createGradientBackground(colors);
// 占比高的颜色会更明显
```

## 📊 算法原理

1. **智能采样**：根据 `quality` 参数跳过像素采样
2. **颜色过滤**：过滤透明、过暗、过亮的像素
3. **K-means 聚类**：将相似颜色聚合成主色调
4. **占比计算**：统计每个聚类的像素数量
5. **渐变生成**：根据占比动态调整半径和透明度

## 🛠️ 技术栈

- TypeScript
- Canvas API
- K-means 聚类算法
- requestAnimationFrame

## 📝 开发

```bash
# 安装依赖
npm install

# 开发模式
npm run dev

# 构建
npm run build

# 类型检查
npm run type-check
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 License

MIT License


---

**Star ⭐ 如果这个项目对你有帮助！**
