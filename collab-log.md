# 协作开发日志 - 大鱼吃小鱼 Qwen Version

## 项目概览

**项目名称**: 大鱼吃小鱼 - Qwen Version  
**技术栈**: HTML5 Canvas + 原生 JavaScript（单文件应用）  
**开发模式**: 5 轮迭代协作开发（collab-game-dev skill）  
**最终代码量**: ~1500 行（index.html）  
**PR 总数**: 6 个（5 轮开发 + 1 个文档 PR）

---

## 开发轮次记录

### 第 1 轮：初始版本 → Review 修复
**目标**: 构建可玩的基础游戏

**Generator 初始实现** (~638 行):
- 玩家鱼控制（鼠标/键盘）
- AI 鱼生成和基础 AI（逃跑/追击）
- 碰撞检测和吃鱼成长机制
- 基础 UI（分数、吃掉数量）

**Reviewer 反馈**（模糊化）:
> "游戏能动了，但是帧率变化时鱼的速度会不一样快，还有一些数字直接写在代码里不太好改，手机上玩不了，最高分也存不下来..."

**Round 1 Fixes** (PR #1):
- ✅ 帧率无关运动（dt 乘以速度）
- ✅ CONFIG 对象集中配置
- ✅ P 键暂停功能
- ✅ 触控支持（touchstart/touchmove）
- ✅ localStorage 最高分保存
- ✅ 大小指示器（绿色=可吃，红色=危险）

---

### 第 2 轮：代码质量优化
**目标**: 重构代码结构，提升可维护性

**Reviewer 反馈**（模糊化）:
> "代码看起来有点乱，drawFish 函数太长了，有些变量名字看不懂，还有背景绘制每帧都重复画浪费性能..."

**Round 2 Fixes** (PR #2):
- ✅ drawFish 拆分为 drawBody/drawTail/drawFin/drawEye 子函数
- ✅ 变量命名规范化
- ✅ 背景离屏 canvas 缓存（bgCanvas/bgCtx）
- ✅ 海藻和光线静态绘制
- ✅ 气泡系统独立函数

---

### 第 3 轮：用户体验优化
**目标**: 增强视觉反馈和游戏感受

**Reviewer 反馈**（模糊化）:
> "吃鱼的时候没什么感觉，不知道吃了多少分，游戏开始太突然了，被吃掉的时候也不知道发生了什么..."

**Round 3 Fixes** (PR #3):
- ✅ 分数弹出动画（+10, +20 飘起来消失）
- ✅ Combo 连击系统（2秒内连吃获得倍率加分）
- ✅ 3-2-1-GO 倒计时
- ✅ CSS 震动动画（游戏结束 shake）
- ✅ 鱼身花纹（大鱼有斑点和条纹）
- ✅ 吃鱼粒子特效（8 个彩色粒子爆炸）

---

### 第 4 轮：功能增强
**目标**: 增加游戏深度和可玩性

**Reviewer 反馈**（模糊化）:
> "我觉得游戏还可以更有意思一点！能不能加一些特殊的东西飘在海里？比如一个护盾吃了可以保护自己一段时间，或者有个加速的道具？还有如果有些特别的鱼，比如金色的分数很高但跑得很快，或者炸弹鱼碰到就死，会刺激很多！难度也应该随时间变难..."

**Round 4 Features** (PR #4):
- ✅ Web Audio 音效系统（oscillator 合成，无需音频文件）
  - eat / golden / bomb / powerup / combo / gameover / countdown / go
- ✅ 金鱼（⭐ 5倍分数，金色光效，游得更快，更难捕捉）
- ✅ 炸弹鱼（💣 碰到即死，主动追击玩家，护盾可挡，20粒子爆炸）
- ✅ 道具系统：
  - 🛡️ 护盾：无敌 5 秒，可以挡住炸弹和敌鱼
  - ⚡ 加速：速度翻倍 4 秒
  - 🧲 磁铁：自动吸取小鱼 6 秒
- ✅ 难度递进：每 30 秒提升难度等级
  - 鱼速度增加
  - 大鱼生成概率增加
  - 炸弹鱼概率增加
- ✅ 成长阶段 UI：小鱼🐟 → 中鱼🐠 → 大鱼🐡 → 巨型鱼🦈
- ✅ 鱼群行为：30% 概率生成 4 条鱼的小群
- ✅ 护盾视觉效果：旋转虚线圈

**代码增长**: +675 行（从 ~800 行增长到 ~1480 行）

---

### 第 5 轮：Bug 修复
**目标**: 修复边界情况和潜在 bug

**Reviewer 反馈**（模糊化）:
> "游戏玩起来偶尔会有一些奇怪的问题，比如快速点击重新开始会卡顿，有时候游戏结束了还有东西在动，护盾消失了边框颜色还在。还有一些代码看起来多余，希望能清理一下..."

**Round 5 Fixes** (PR #5):
- ✅ 道具立即生成 bug：`powerupSpawnTimer` 初始化为 0 导致第一个道具立即出现
- ✅ 倒计时重入 bug：快速点击"再来一次"会创建多个 setInterval
- ✅ Game over 双重触发：同一帧可能触发两次游戏结束
- ✅ comboTimeout 未清理：Game over 时定时器仍会触发
- ✅ Shield CSS 残留：护盾消失或游戏结束时 `shield-border` 类未移除
- ✅ 删除未使用的 `canEat` 变量
- ✅ 统一清理动画帧和定时器

---

### 文档 PR
**PR #6**: 添加 `docs/deployment.md` 部署指南

---

## 最终状态

### 游戏特性一览

| 类别 | 功能 |
|------|------|
| **控制** | 鼠标/触屏/键盘（方向键+WASD） |
| **视觉** | 离屏canvas背景、鱼花纹、粒子特效、震动动画 |
| **音效** | Web Audio 合成（8种音效） |
| **玩法** | Combo连击、道具系统、难度递进、成长阶段 |
| **特殊鱼** | 金鱼（5x分数）、炸弹鱼（即死） |
| **道具** | 护盾、加速、磁铁 |
| **AI** | 逃跑/追击、鱼群行为、炸弹主动追击 |
| **持久化** | localStorage 最高分 |
| **兼容** | 桌面+移动端，帧率无关运动 |

### 文件清单

```
big-fish-small-fish-qwen-version/
├── index.html              # 游戏主文件（~1500 行）
├── README.md               # 项目说明
├── collab-log.md           # 本日志
└── docs/
    └── deployment.md       # 部署指南
```

### Git 历史

```
e42cfdc Merge pull request #6 - docs: 添加部署指南
2e1401a Merge pull request #5 - round5: fix - 修复多个 bug
c85fba1 Merge pull request #4 - round4: feat - 功能增强
903b685 Merge pull request #3 - round3: 用户体验优化
a353b32 Merge pull request #2 - round2: 代码质量优化
ef88666 Merge pull request #1 - round1: review fixes
```

### 仓库地址

**GitHub**: https://github.com/TD-ding/big-fish-small-fish-qwen-version

---

## 开发流程说明

本项目使用 **collab-game-dev** skill 的简化单 agent 模式：

1. **Generator**: 根据需求生成代码
2. **Reviewer**: 审查代码并提出改进建议
3. **Fuzzification**: 将技术反馈转化为自然语言（模拟"新手用户"口吻）
4. **Generator**: 根据模糊化反馈进行修改
5. 每轮生成一个 PR，合并到 main

每轮都遵循：
- 生成/修改代码 → git add → git commit → git push → gh pr create → gh pr merge
- 从 main 拉取最新代码创建新的 agent/dev 分支

---

## 技术亮点

1. **单文件架构**: 整个游戏在一个 HTML 文件中，包含 HTML/CSS/JS
2. **帧率无关运动**: 所有运动乘以 dt（时间增量），确保不同帧率下体验一致
3. **离屏 Canvas**: 背景静态元素预渲染，减少每帧绘制开销
4. **Web Audio 合成**: 使用 OscillatorNode 生成音效，无需外部音频文件
5. **CONFIG 集中化**: 所有魔法数字集中在 CONFIG 对象中，易于调整
6. **dt 帧率补偿**: 使用 `Math.min(elapsed / TARGET_FRAME_MS, 3)` 防止卡顿时的大跳跃

---

*开发完成时间: 2026-06-09*  
*开发模式: Claude Code Agent (Qwen-powered review simulation)*
