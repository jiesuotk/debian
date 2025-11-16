# ---------------------------------------------------------------
# 黄金方案 v3.1（适合手动构建 Alist）
# ---------------------------------------------------------------

# 1. 使用微软的 Alpine DevContainer 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

USER root

# 2. 安装构建依赖
RUN apk add --no-cache \
    bash \
    git \
    wget \
    curl \
    tar \
    gcc \
    musl-dev \
    ca-certificates \
    nodejs \
    npm

# 3. 安装 pnpm
RUN npm install -g npm@11.6.2 && npm install -g pnpm

# 4. 安装 Go 1.22.x（避免 Go 1.23 的日志 bug）
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

ENV PATH="/usr/local/go/bin:${PATH}"

WORKDIR /workspace

USER vscode
