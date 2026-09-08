# Day3：Git + GitHub 作品集上线（日期）

## 今日目标
配置 Git，打通 SSH，学习仓库首次 push 到 GitHub

## 完成情况
✅ Git 安装与身份配置（user.name / user.email）
✅ SSH key（ed25519）生成并添加到 GitHub，ssh -T 验证通过
✅ 仓库首次 push 成功：github.com/CYyyy1221/ros2-90day
✅ VirtualBox 共享粘贴板/拖放开启（设置→常规→高级→双向）

## 踩坑记录
### 坑1：git push 报 Repository not found
- 根因：GitHub 仓库名建成了 ros2-90day（少个 s），本地 remote 地址却写的 ros2-90days
- 解法：git remote set-url origin git@github.com:CYyyy1221/ros2-90day.git
- 经验：本地与远端地址必须精确一致，改名用 set-url 不用删库重建

## 新学到的知识
- SSH key 原理：私钥留本机，公钥给 GitHub，免密且安全
- Git 工作流：init → add → commit（本地存档）→ remote add → push（上云）
- 日常三连：git add . && git commit -m "..." && git push
- 此仓库 = 90 天作品集的载体，秋招时供面试官验证学习过程
