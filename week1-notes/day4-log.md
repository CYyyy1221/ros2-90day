# Day4：ROS2 安装与 DDS 排障（2026-09-08）

## 今日目标
安装 ROS2 Humble，跑通 talker/listener 双终端通信

## 最终结果
✅ ROS2 Humble 桌面版安装完成（清华源 + 官方密钥）
✅ 双终端消息互通
✅ RViz2 图形环境正常

## 踩坑记录（重点）
### 坑1：fishros 一键脚本段错误
- 现象：wget 下载成功，bash 执行报"段错误(核心已转储)"
- 排查：head -20 fishros 发现内容是 HTML 网页不是脚本
- 根因：fishros 网站入口变更，返回的是网页
- 解法：放弃一键脚本，改用官方 apt 源手动安装

### 坑2：GitHub 直连失败
- 现象：curl 下载 deb 包 90 秒后报 SSL_read 错误
- 解法：换清华 ros2 镜像源（mirrors.tuna.tsinghua.edu.cn/ros2/ubuntu）

### 坑3：密钥下载 404
- 现象：apt update 报 NO_PUBKEY，密钥文件只有 153 字节
- 排查：cat 发现下载到的是 404 错误页
- 解法：从 keyserver.ubuntu.com 直接取公钥，gpg --dearmor 转格式

### 坑4：依赖关系死锁
- 现象：安装 ros-humble-desktop 报 libpulse 等版本冲突，apt upgrade 后依旧
- 根因：sources.list 缺 jammy-updates 分支，安全库和更新库的包版本错位
- 解法：补一行 jammy-updates 源 + apt full-upgrade

### 坑5：talker/listener 互相发现失败
- 现象：talker 正常发布，listener/echo 收不到任何话题
- 根因：VirtualBox 虚拟网卡组播支持差，Fast DDS 发现机制失效
- 解法：ROS_LOCALHOST_ONLY=1 + 切换 CycloneDDS

## 新学到的知识
- apt 装软件的完整链路：加源 → 加签名密钥 → update → install
- ROS2 的 DDS 中间件可切换（Fast DDS / CycloneDDS）
- 常用命令：ros2 topic list / echo、ros2 daemon stop
