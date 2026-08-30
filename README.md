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
/Users/zhanghui/project/石头多多理财小助手/
├── index.html           # 主应用文件（所有 HTML/CSS/JS 都在这一个文件里）
├── shitou.png           # 石头的头像
├── duoduo.png           # 多多的头像
├── xingqiu.png          # 星球图标
├── xiaojiangtie.png     # 小奖贴图标
├── dajiangtie.png       # 大奖贴图标
├── chaodajiangtie.png   # 超大贴图标
└── README.md            # 本说明文档
```

> 本项目采用**单文件应用**架构，所有界面、样式、逻辑都写在 `index.html` 中，方便零基础维护和部署。

## 本地预览（可选）

如果你想在推送前先在电脑上看效果，可以启动本地 HTTP 服务器：

```bash
cd "/Users/zhanghui/project/石头多多理财小助手"
python3 -m http.server 8080
```

然后在浏览器打开：http://localhost:8080

> **更简单的方式**：直接修改后推送到 GitHub，然后访问 https://hvpord.github.io/stone-duoduo-money/ 查看在线效果。
> 
> 注意：直接双击打开 HTML 文件在手机上可能无法正常显示，必须通过 HTTP 服务器或部署到 GitHub Pages 访问。

## 部署到 GitHub Pages

### 首次部署

```bash
cd "/Users/zhanghui/project/石头多多理财小助手"
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
cd "/Users/zhanghui/project/石头多多理财小助手"
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

### 已实现

- [x] 两个孩子余额卡片展示
- [x] 奖励贴图形化显示
- [x] 发奖励（点击奖贴暂存，确认发放）
- [x] 记支出（点击奖贴暂存，确认扣除）
- [x] 孩子间转账（箭头切换方向）
- [x] 家长任务板：新建、编辑、完成和删除任务
- [x] 任务可设置截止时间和可重复完成
- [x] 完成任务二次确认，支持填写额外备注并自动发放奖励
- [x] 完成和删除的任务归档，支持再次编辑发布和永久删除
- [x] 双人任务支持奖励平分
- [x] 记账本显示发奖、扣减和完成任务的原因/备注
- [x] 任务奖励记录使用独立的淡绿色卡片风格
- [x] GitHub Gist 多设备同步与新设备首次同步保护
- [x] 孩子真实头像显示
- [x] 卡通可爱风格

### 待实现

- [x] 数据持久化（localStorage）
- [ ] 计划任务自动执行（每周/每月自动发零花钱）
- [ ] 完整的心愿目标进度追踪
- [x] 交易历史记录
- [x] 云端同步（GitHub Gist）
- [ ] 数据导出/导入
- [ ] 孩子自己发布任务
- [ ] 奖贴合成/兑换动画
- [ ] 家长密码保护

## 数据存储说明

### 当前状态

- 主数据保存在浏览器 `localStorage` 中，刷新页面或重新打开后不会丢失。
- 通过固定 GitHub Gist 中的 `stone-duoduo-data.json` 进行多设备数据同步。
- 没有 Token 的设备只能下载云端数据，不能上传。
- 新设备第一次输入 Token 后同步时只下载云端数据，本次不上传，避免用默认本地数据覆盖 Gist。
- 在强制使用云端数据前，会在当前设备保留一份同步前本地备份。

## 2026-08 任务板与记账优化

- 将原任务列表调整为家长任务板，新增绿色“+”入口和每条任务的完成、编辑、删除按钮。
- 任务增加时限、重复完成、完成次数、完成备注和归档数据。
- 非重复任务完成后移出任务板；重复任务保留并累计完成次数。
- 完成任务后记账本写入“完成任务：任务名。”，并单独显示额外备注。
- 任务板与任务奖励记账卡片统一使用淡绿色视觉风格。
- 从设置页移除“重置数据/清空所有记录”入口及对应函数，防止误操作。

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
