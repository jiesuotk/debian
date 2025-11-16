# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v2 - 修正版)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用【微软官方的】Alpine 基础镜像。
#    它已经内置了 sudo、bash、git 和一个非 root 用户 (vscode)
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. (配方 A)
#    安装 CGO (musl) 编译所需的工具
#    我们必须切换到 root 用户来安装
USER root

RUN apk add --no-cache gcc musl-dev

# 3. (配方 B)
#    安装 Go 1.22.x (我们使用 1.22.10，一个已知安全的版本)
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 4. (关键)
#    将 Go 1.22.x 添加到【系统全局】的环境变量中
#    这样所有用户 (包括 vscode) 都能访问它
ENV PATH="/usr/local/go/bin:${PATH}"

# 5. 切换回安全的非 root 用户
USER vscode
