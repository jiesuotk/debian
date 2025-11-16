# 基础镜像使用 Debian 11
FROM debian:11

# 设置环境变量
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV PATH=/usr/local/go/bin:$PATH

# 安装基础工具和依赖
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    build-essential \
    ca-certificates \
    unzip \
    sudo \
    gnupg \
    lsb-release \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# 安装 Go 1.21.5
RUN wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz \
    && rm -rf /usr/local/go \
    && tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz \
    && rm go1.21.5.linux-amd64.tar.gz

# 安装 Node.js 22.x 和 pnpm
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g pnpm

# 验证安装
RUN go version && node -v && npm -v && pnpm -v

# 设置工作目录
WORKDIR /workspaces/${GITHUB_REPOSITORY}

# 默认命令
CMD [ "bash" ]
