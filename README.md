# 大鱼吃小鱼 - Qwen Version 🐟

一个基于 HTML5 Canvas 的大鱼吃小鱼小游戏。

## 简介

控制你的小鱼，通过吃掉比你小的鱼来长大，同时躲避比你大的鱼！

## 技术栈

- HTML5 Canvas
- JavaScript (原生)
- CSS3

## 目录结构

```
big-fish-small-fish-qwen-version/
├── index.html    # 游戏主文件（单文件应用）
└── README.md     # 项目说明文档
```

## 如何运行

1. 直接用浏览器打开 `index.html` 文件即可
2. 或通过本地服务器访问：
   ```bash
   python3 -m http.server 8000
   ```
   然后访问 `http://localhost:8000`

## 操作方式

- **鼠标控制**: 移动鼠标引导鱼的方向
- **键盘控制**: 使用方向键或 WASD 键移动

## 游戏规则

- 吃掉比你小的鱼可以得分并长大
- 碰到比你大的鱼会被吃掉，游戏结束
- 尽量吃更多的小鱼来获得高分！
