# -----------------------------------------------------------------
# 黄金方案 Dockerfile (v4 - 最终修正版)
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用微软官方的 Alpine 基础镜像
FROM mcr.microsoft.com/devcontainers/base:alpine-3.19

# 2. 切换到 root 用户来安装所有工具
USER root

# 3. (配方 A & 前端需求)
#    安装 CGO (musl) 工具 (gcc, musl-dev)
#    以及 nvm/pnpm 所需的工具 (curl, bash)
RUN apk add --no-cache gcc musl-dev curl bash

# 4. (配方 B - Go)
#    安装 Go 1.22.x (一个已知安全的版本)
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# 5. (前端需求 - Node.js)
#    手动安装 nvm (Node Version Manager)
ENV NVM_DIR="/usr/local/share/nvm"
ENV NODE_VERSION="lts" 
RUN mkdir -p $NVM_DIR && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | NVM_DIR="$NVM_DIR" bash

# 6. (前端需求 - pnpm)
#    使用 nvm 安装 Node.js (LTS) 和 pnpm
#    这必须在 bash subshell 中运行才能加载 nvm
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    nvm use default && \
    npm i -g pnpm"

# 7. (关键) 设置所有环境变量，以便 vscode 用户能找到它们
ENV PATH="/usr/local/go/bin:${PATH}"
#    将 nvm 的路径添加到 shell 配置文件，以便新终端能加载
RUN echo "export NVM_DIR=\"$NVM_DIR\"" >> /etc/profile.d/nvm.sh
RUN echo "[ -s \"$NVM_DIR/nvm.sh\" ] && \. \"$NVM_DIR/nvm.sh\"" >> /etc/profile.d/nvm.sh

# 8. 切换回安全的非 root 用户
USER vscode

# 9. (关键) 告诉 vscode 用户的 shell (bash) 如何加载 nvm
ENV BASH_ENV="/etc/profile"
ENV SHELL="/bin/bash"

# 10. (可选) 验证安装
RUN go version
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && node -v && pnpm -v"
