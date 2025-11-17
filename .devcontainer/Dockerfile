# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v10 - 最终版)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用微软官方的 Alpine 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. 切换到 root 用户来安装【所有】工具
USER root

# 3. (关键) 安装所有必需的工具
#    gcc, musl-dev: 解决 "CGO 卡死" (配方 A)
#    nodejs, npm, pnpm: 解决 "前端编译"
RUN apk add --no-cache \
    gcc \
    musl-dev \
    make \
    bash \
    git \
    ca-certificates \
    wget \
    nodejs \
    npm

# 4. (关键) 用 npm 安装 pnpm
RUN npm i -g pnpm

# 5. (配方 B - 已修正)
#    安装 Go 1.23.4 (解决 "依赖库编译失败")
ARG GO_VERSION="1.23.4"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 6. (必需)
#    将 Go 1.23.4 添加到【系统全局】的环境变量中
ENV PATH="/usr/local/go/bin:${PATH}"

# 7. 切换回安全的非 root 用户
USER vscode
