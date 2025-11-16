# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v8 - 最终修正版)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用微软官方的 Alpine 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. 切换到 root 用户来安装【所有】工具
USER root

# 3. (关键修复)
#    使用【一个】RUN 命令安装所有必需的工具
#    (这可以 100% 保证可靠性，并避免重复)
RUN apk add --no-cache \
    gcc \
    musl-dev \
    make \
    bash \
    git \
    ca-certificates \
    wget \
    nodejs \
    pnpm

# 4. (配方 B - 必需)
#    安装 Go 1.22.x (解决 "日志失声" bug)
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 5. (必需)
#    将 Go 1.22.x 添加到【系统全局】的环境变量中
ENV PATH="/usr/local/go/bin:${PATH}"

# 6. 切换回安全的非 root 用户
USER vscode
