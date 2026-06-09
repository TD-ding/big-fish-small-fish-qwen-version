# 部署指南 - 大鱼吃小鱼 Qwen Version

## 项目结构

```
big-fish-small-fish-qwen-version/
├── index.html          # 游戏主文件（单文件应用，约 1500 行）
├── README.md           # 项目说明文档
└── docs/
    └── deployment.md   # 本部署指南
```

## 运行方式

### 方式一：直接打开（推荐快速体验）

直接双击 `index.html` 文件，浏览器即可运行游戏。

### 方式二：本地服务器

```bash
# Python 3
cd big-fish-small-fish-qwen-version
python3 -m http.server 8000

# Node.js (需要安装 http-server)
npx http-server -p 8000
```

然后访问 `http://localhost:8000`。

### 方式三：静态托管

项目是纯静态单文件 HTML，可以部署到任意静态托管服务：

- GitHub Pages
- Netlify
- Vercel
- 任何支持静态文件的 CDN

## 浏览器兼容性

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

需要支持：
- HTML5 Canvas
- Web Audio API（可选，用于音效）
- localStorage（用于最高分保存）
- requestAnimationFrame

## 游戏操作

| 设备 | 操作方式 |
|------|---------|
| 电脑 | 鼠标移动 或 方向键/WASD |
| 移动端 | 触屏滑动 |
| 暂停 | P 键 或 Esc 键 |

## 游戏特色

- 🐟 **成长系统**：小鱼 → 中鱼 → 大鱼 → 巨型鱼
- ⭐ **金鱼**：5 倍分数，跑得更快
- 💣 **炸弹鱼**：碰到即死，会主动追击
- 🛡️⚡🧲 **道具系统**：护盾 / 加速 / 磁铁
- 🔥 **Combo 连击**：2 秒内连吃获得加分
- 📈 **难度递进**：每 30 秒提升难度等级
- 🎵 **Web Audio 音效**：吃鱼、炸弹、道具、Combo 等

## 数据持久化

游戏使用 `localStorage` 保存最高分：

```javascript
localStorage.setItem('bigFishHighScore', highScore);
```

清除浏览器数据或更换浏览器会丢失最高分记录。

## 技术栈

- HTML5 Canvas（渲染）
- 原生 JavaScript（无框架依赖）
- Web Audio API（音效合成）
- CSS3（UI 动画）

## 性能建议

- 游戏以 60 FPS 为基准设计，使用 dt 帧率独立运动
- 低性能设备建议关闭其他占资源的标签页
- 移动端建议使用横屏模式

## 故障排除

**问题：没有声音**
- 需要用户交互后才能播放音效（浏览器安全策略）
- 点击"开始游戏"后音效即可正常工作

**问题：画面卡顿**
- 检查浏览器硬件加速是否开启
- 关闭其他占用资源的程序

**问题：最高分未保存**
- 检查浏览器是否禁用了 localStorage
- 隐私/无痕模式下 localStorage 可能在关闭后清空
