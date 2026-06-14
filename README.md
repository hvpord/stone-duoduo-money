# 石头多多理财小助手

一个专为两个孩子（石头、多多）设计的零花钱/理财管理网页应用，可以在 iPhone 上像 App 一样使用。

## 项目目标

帮助孩子理解金钱概念，培养理财习惯：
- 通过完成任务获得奖励贴
- 学习储蓄、支出、转账
- 记录心愿目标并逐步实现

## 开发环境

**无需安装任何开发工具**，只需要：
- 一个文本编辑器（如 VS Code、Cursor、系统自带文本编辑器）
- 一个现代浏览器（Safari、Chrome 等）
- GitHub 账号（用于部署）

## 文件结构

```
/Users/zhanghui/zhanghuihub/家庭/石头多多理财小助手/
├── index.html      # 主应用文件（所有 HTML/CSS/JS 都在这一个文件里）
├── shitou.png      # 石头的头像
├── duoduo.png      # 多多的头像
└── README.md       # 本说明文档
```

> 本项目采用**单文件应用**架构，所有界面、样式、逻辑都写在 `index.html` 中，方便零基础维护和部署。

## 本地预览

进入项目目录，启动一个本地 HTTP 服务器：

```bash
cd "/Users/zhanghui/zhanghuihub/家庭/石头多多理财小助手"
python3 -m http.server 8080
```

然后在浏览器打开：http://localhost:8080

> 注意：直接双击打开 HTML 文件在手机上可能无法正常显示，必须通过 HTTP 服务器或部署到 GitHub Pages 访问。

## 部署到 GitHub Pages

### 首次部署

```bash
cd "/Users/zhanghui/zhanghuihub/家庭/石头多多理财小助手"
git init
git add index.html shitou.png duoduo.png README.md
git commit -m "初始版本"
git remote add origin https://github.com/hvpord/stone-duoduo-money.git
# 在 GitHub 上创建 stone-duoduo-money 公开仓库后：
git push -u origin main
```

然后在 GitHub 仓库设置中开启 Pages：
- Settings → Pages → Source 选择 "Deploy from a branch"
- Branch 选择 `main`，路径选择 `/(root)`

访问地址：https://hvpord.github.io/stone-duoduo-money/

### 后续更新

每次修改后，执行：

```bash
cd "/Users/zhanghui/zhanghuihub/家庭/石头多多理财小助手"
git add index.html shitou.png duoduo.png README.md
git commit -m "更新说明"
git push
```

等待 1-3 分钟，手机上刷新页面即可看到更新。

## 货币系统：奖励贴

本项目使用"奖励贴"代替人民币，让孩子更直观理解：

| 奖贴 | 图标 | 价值 |
|------|------|------|
| 星球 | 🪐 | 1000 元 |
| 超大贴 | 🎫 | 50 元 |
| 大奖贴 | 🥇 | 5 元 |
| 小奖贴 | 🥈 | 2.5 元 |

例如：1505 元 = 1 个星球 + 10 个超大贴 + 1 个大奖贴

## 功能清单

### 已实现（草稿版）

- [x] 两个孩子余额卡片展示
- [x] 奖励贴图形化显示
- [x] 发奖励（点击奖贴暂存，确认发放）
- [x] 记支出（点击奖贴暂存，确认扣除）
- [x] 孩子间转账（箭头切换方向）
- [x] 任务/心愿/挑战列表
- [x] 点击头像领取和完成任务
- [x] 双人任务支持奖励平分
- [x] 孩子真实头像显示
- [x] 卡通可爱风格

### 待实现

- [ ] 数据持久化（localStorage）
- [ ] 计划任务自动执行（每周/每月自动发零花钱）
- [ ] 完整的心愿目标进度追踪
- [ ] 交易历史记录
- [ ] 云端同步（GitHub Gist）
- [ ] 数据导出/导入
- [ ] 孩子自己发布任务
- [ ] 奖贴合成/兑换动画
- [ ] 家长密码保护

## 数据存储说明

### 当前状态

目前是**纯演示草稿**，刷新页面后数据会恢复为示例数据。

### 后续规划

1. **本地存储**：使用浏览器 localStorage 保存数据，离线可用
2. **云端同步**：可选配置 GitHub Gist Token，多设备同步
3. **导出备份**：支持导出 JSON 文件备份

## 头像替换方法

准备两张正方形的孩子照片，建议：
- 尺寸：200×200 像素以上
- 格式：PNG（支持透明背景最佳）
- 文件名保持为 `shitou.png` 和 `duoduo.png`

替换项目目录中的同名文件，然后重新部署即可。

## 开发约定

- 所有代码尽量保持在 `index.html` 一个文件中
- 使用 emoji 和明亮色彩保持卡通风格
- 头像始终彩色显示，不使用灰色/黑白头像
- 重要操作尽量用图形化交互，减少数字输入

## 在线访问

https://hvpord.github.io/stone-duoduo-money/

家人可以直接通过这个链接访问，不需要 GitHub 账号。

## 提示

如果手机上打开后没有看到最新更新，可以尝试：
1. Safari 顶部下拉刷新页面
2. 关闭 Safari 标签页重新打开
3. 删除主屏幕图标，重新"添加到主屏幕"
