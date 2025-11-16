# ---------------------------------------------------------------
# 黄金方案 Dockerfile (v3 - 稳定版，支持前端 + 后端构建)
# ---------------------------------------------------------------

# 使用微软官方 Alpine（musl）基础环境
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 升级到 root 以安装构建工具
USER root

# 安装构建后端 Go 所需的工具链（musl 必备）
RUN apk add --no-cache \
    gcc \
    musl-dev \
    make \
    bash \
    wget \
    git \
    ca-certificates \
    nodejs \
    npm

# 安装 pnpm（前端构建用）
RUN npm i -g pnpm

# 安装 Go（推荐稳定且兼容的版本）
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 设置 Go 到系统 PATH
ENV PATH="/usr/local/go/bin:${PATH}"

# 切回 vscode 用户
USER vscode
