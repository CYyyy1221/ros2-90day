# Day2：系统配置与 Linux 命令入门（日期）

## 今日目标
换国内源、系统升级、Linux 基础命令、中文输入法

## 完成情况
✅ 清华软件源更换，系统 356 个包全部升级
✅ Linux 四类命令练习（文件/查看/系统/管道）
✅ 建立学习仓库目录 ~/ros2-90days/（week1-3-notes + README）
✅ fcitx5 拼音输入法安装
✅ VirtualBox Guest Additions 增强功能安装（剪贴板/拖放/显卡驱动）

## 踩坑记录
### 坑1：apt update 全线 404
- 现象：换源后报 ubuntu-ports 路径 404
- 根因：误选了 ARM 架构的 ubuntu-ports 源（x86_64 应用 ubuntu 源）
- 解法：sudo sed -i 's/ubuntu-ports/ubuntu/g' /etc/apt/sources.list

### 坑2：Guest Additions 编译失败（三连）
- 坑A：文件名手敲错（VBoxLiunxAdditions）→ 学会用 Tab 补全
- 坑B：缺编译器 → 装 build-essential dkms linux-headers
- 坑C：仍报 gcc-12 not found → HWE 6.8 内核需要 gcc-12（apt 装 gcc-12 g++-12）
- 验证：lsmod | grep vboxguest 有输出 = 模块加载成功

### 坑3：虚拟机挂机死机
- 根因：Windows 宿主机睡眠把虚拟机一起冻住
- 解法：关闭 Windows 自动睡眠；长时间离开用 sudo shutdown 代替挂机

## 新学到的知识
- Linux 命令"沉默即成功"：执行完没输出 = 正常
- 管道 | 的含义：左边输出喂给右边当输入
- rm 不进回收站，只在练习目录使用
