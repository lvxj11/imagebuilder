# OpenWrt/ImmortalWrt 镜像构建项目

## 项目简介

这是一个用于构建 OpenWrt/ImmortalWrt 自定义镜像的项目，基于 24.10 版本，包含多种配置选项和自定义脚本。

## 项目结构

```
├── bin/                  # 构建输出目录
├── files-bypass/         # 基本配置文件
│   └── etc/uci-defaults/ # UCI 默认配置
├── files-full/           # 完整配置文件
│   ├── etc/custom-scripts/ # 自定义脚本
│   └── etc/uci-defaults/   # UCI 默认配置
├── build.sh              # 基本构建脚本
├── build-bypass.sh       # 包含代理应用的构建脚本
├── docker-build-bypass.sh # Docker 构建脚本（bypass 版本）
├── docker-build-full.sh  # Docker 构建脚本（full 版本）
└── LICENSE               # 许可证文件
```

## 主要功能

### 构建脚本

1. **build.sh** - 基本构建脚本，包含以下功能：
   - 禁用不需要的文件系统和镜像格式
   - 安装基本软件包：curl、openssh-sftp-server
   - 安装 Luci 界面和中文语言包
   - 安装推荐软件包：ttyd
   - 安装推荐主题：argon

2. **build-bypass.sh** - 增强版构建脚本，在基本脚本的基础上增加：
   - 更换为镜像源（解决官方源掉线问题）
   - 安装代理应用：passwall
   - 配置并安装 nikki 应用

### 自定义脚本

在 `files-full/etc/custom-scripts/` 目录下包含以下脚本：

- **dhcp** - DHCP 相关脚本
- **log.sh** - 日志管理脚本
- **update-ipset.sh** - IPset 更新脚本
- **update-ipv6-for-qbittorrent-ipset.sh** - 为 qBittorrent 更新 IPv6 IPset
- **update-ipv6-for-webserver-ipset.sh** - 为 Web 服务器更新 IPv6 IPset

### UCI 默认配置

在 `files-bypass/etc/uci-defaults/` 和 `files-full/etc/uci-defaults/` 目录下包含以下配置：

- **lvxj00-public.sh** - 公共配置
- **lvxj01-dhcp.sh** - DHCP 配置
- **lvxj02-ipv6.sh** - IPv6 配置
- **lvxj50-private.sh** - 私有配置
- **lvxj51-webserver.sh** - Web 服务器配置
- **lvxj52-qbittorrent.sh** - qBittorrent 配置

## 使用方法

### 基本构建

```bash
./build.sh
```

### 包含代理应用的构建

```bash
./build-bypass.sh
```

### Docker 构建

```bash
./docker-build-bypass.sh  # 构建包含代理应用的镜像
./docker-build-full.sh    # 构建完整配置的镜像
```

## 构建配置

- **ROOTFS_PARTSIZE** - 根文件系统分区大小，默认 800MB
- **FILES** - 配置文件目录，默认 "files"
- **PACKAGES** - 要安装的软件包列表

## 注意事项

1. 构建前请确保已安装必要的依赖
2. 构建过程可能需要较长时间，具体取决于网络速度和系统性能
3. 构建完成后，镜像文件将位于 `bin` 目录

## 许可证

本项目使用 MIT 许可证，详见 LICENSE 文件。