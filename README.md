# xiaohongshu-mcp-plus

中文 | English

这是一个已经打包好的 `xiaohongshu-mcp-plus` Docker 发布包。  
This is a ready-to-use Docker release bundle for `xiaohongshu-mcp-plus`.

它的目标很简单：  
The goal is simple:

- 让你在新机器上更快恢复服务
- 让你更容易迁移当前运行环境
- 让 OpenClaw 或其他 MCP 客户端可以继续连接这套服务

- Restore the service on a new machine quickly
- Move the current runtime more easily
- Keep OpenClaw or other MCP clients connected to this service

## 📦 包含什么 | What Is Included

- `xiaohongshu-mcp-plus-image.tar.gz`
  中文：Docker 镜像包  
  English: Docker image archive

- `xiaohongshu-mcp-plus-data.tar.gz`
  中文：运行数据包，包含 `plus-data` 和 `plus-images`  
  English: Runtime data archive, including `plus-data` and `plus-images`

- `xiaohongshu-mcp-plus-compose.yml`
  中文：Docker Compose 启动模板  
  English: Docker Compose startup template

- `CHECKSUMS.txt`
  中文：发布包校验值  
  English: checksums for the release files

## ⬇️ 下载方式 | How To Download

大文件不会直接放在仓库源码里。  
Large archives are not stored directly in the Git repository source tree.

请到 GitHub Releases 页面下载下面两个文件：  
Please download the following files from the GitHub Releases page:

- `xiaohongshu-mcp-plus-image.tar.gz`
- `xiaohongshu-mcp-plus-data.tar.gz`

如果你只是想先看说明文档，直接浏览仓库首页即可。  
If you only want the instructions first, just read the repository homepage.

## 👥 适合谁 | Who This Is For

如果你是非技术用户，也可以照下面做。你主要只需要会这几件事：

- 安装 Docker
- 复制文件
- 打开终端粘贴命令

If you are not technical, you can still follow this guide.  
You mainly need to know how to:

- install Docker
- copy files
- paste commands into Terminal

## 🚀 快速开始 | Quick Start

### 1️⃣ 第一步：导入镜像 | Step 1: Load The Docker Image

```bash
docker load -i xiaohongshu-mcp-plus-image.tar.gz
```

检查镜像是否导入成功：  
Check whether the image was loaded successfully:

```bash
docker images | grep xiaohongshu-mcp-plus
```

当前镜像名：  
Current image name:

```text
docker-xiaohongshu-mcp-plus
```

### 2️⃣ 第二步：恢复数据 | Step 2: Restore Runtime Data

```bash
mkdir -p ~/xhs-plus-runtime
tar -xzf xiaohongshu-mcp-plus-data.tar.gz -C ~/xhs-plus-runtime
```

解压后你会看到：  
After extraction you should have:

- `~/xhs-plus-runtime/plus-data`
- `~/xhs-plus-runtime/plus-images`

### 3️⃣ 第三步：启动服务 | Step 3: Start The Service

最直接的方式：  
The most direct way:

```bash
docker run -d \
  --name xiaohongshu-mcp-plus \
  -p 18068:18060 \
  -e TZ=Asia/Shanghai \
  -e ROD_BROWSER_BIN=/usr/bin/google-chrome \
  -e COOKIES_PATH=/app/data/cookies.json \
  -v ~/xhs-plus-runtime/plus-data:/app/data \
  -v ~/xhs-plus-runtime/plus-images:/app/images \
  docker-xiaohongshu-mcp-plus
```

### 🧩 或者：使用 Compose | Or: Use Docker Compose

先修改 `xiaohongshu-mcp-plus-compose.yml` 里的本机路径，再运行：  
First update the host paths in `xiaohongshu-mcp-plus-compose.yml`, then run:

```bash
docker compose -f xiaohongshu-mcp-plus-compose.yml up -d
```

## ✅ 检查是否成功 | Check If It Works

```bash
curl http://127.0.0.1:18068/health
```

如果返回 `success: true`，说明服务已经起来了。  
If it returns `success: true`, the service is running.

## 🔌 MCP 地址 | MCP Endpoint

```text
http://127.0.0.1:18068/mcp
```

这个地址可以给：

- OpenClaw
- mcporter
- 其他支持 MCP 的客户端

This endpoint can be used by:

- OpenClaw
- mcporter
- other MCP-compatible clients

## 🦞 OpenClaw 接入示例 | OpenClaw Example

```bash
npx mcporter config add xiaohongshu-plus http://127.0.0.1:18068/mcp
```

查看工具列表：  
List available tools:

```bash
npx mcporter list xiaohongshu-plus
```

## 🗂️ 文件夹说明 | Folder Notes

- `/app/data`
  中文：cookies 和运行数据  
  English: cookies and runtime data

- `/app/images`
  中文：图片素材目录  
  English: image assets directory

## 🙋 非技术用户注意事项 | Notes For Non-Technical Users

1. `xiaohongshu-mcp-plus-data.tar.gz` 可能带有登录态。  
   `xiaohongshu-mcp-plus-data.tar.gz` may contain login state.

2. 如果你只是想分享程序，不想分享账号状态，只发镜像包，不发数据包。  
   If you only want to share the program and not the account state, share the image archive only, not the data archive.

3. 如果新机器上打不开，请优先检查 Docker 是否正常安装。  
   If it does not start on a new machine, first check whether Docker is installed correctly.

4. 如果你不懂路径，先照着示例命令原样执行，再根据需要改。  
   If you are not comfortable with file paths, start with the example commands first.

## ❤️ 原作者说明 | Original Author Attribution

这个发布包不是从零写的新项目，它基于原始项目整理而来。  
This release bundle is not a brand-new project from scratch. It is packaged from an original upstream project.

原作者与原项目：  
Original author and upstream project:

- 作者 / Author: `xpzouying`
- 项目 / Project: `xiaohongshu-mcp`
- GitHub: [https://github.com/xpzouying/xiaohongshu-mcp](https://github.com/xpzouying/xiaohongshu-mcp)

本仓库主要提供：

- Docker 镜像分发
- 数据恢复方式
- 更容易理解的使用说明

This repository mainly provides:

- Docker image distribution
- runtime data restore instructions
- easier-to-understand setup guidance
