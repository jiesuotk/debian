# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v3 - 修正版)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用微软官方的 Alpine 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. 切换到 root 用户来安装所有工具
USER root

# 3. (配方 A)
#    安装 CGO (musl) 编译工具 (gcc, musl-dev)
#    (新) 并且安装 Node.js 和 npm
RUN apk add --no-cache gcc musl-dev nodejs npm

# 4. (新) 
#    使用 npm 来安装 pnpm
RUN npm i -g pnpm

# 5. (配方 B)
#    安装 Go 1.22.x (一个已知安全的版本)
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 6. (关键)
#    将 Go 1.22.x 添加到【系统全局】的环境变量中
ENV PATH="/usr/local/go/bin:${PATH}"

# 7. 切换回安全的非 root 用户
USER vscode
