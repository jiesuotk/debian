# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v9 - 修复了 pnpm)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用微软官方的 Alpine 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. 切换到 root 用户来安装【所有】工具
USER root

# 3. (关键修复 - 步骤 1)
#    安装所有【能】用 apk 安装的工具
#    (我们安装 nodejs，它会自动带来 npm)
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

# 4. (关键修复 - 步骤 2)
#    现在我们有了 npm，用 npm 来安装 pnpm
RUN npm i -g pnpm

# 5. (配方 B - 必需)
#    安装 Go 1.22.x (解决 "日志失声" bug)
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 6. (必需)
#    将 Go 1.22.x 添加到【系统全局】的环境变量中
ENV PATH="/usr/local/go/bin:${PATH}"

# 7. 切换回安全的非 root 用户
USER vscode
