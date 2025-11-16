# -----------------------------------------------------------------
# 黄金方案 Dockerfile
# -----------------------------------------------------------------

# 1. (配方 A)
#    使用 Alpine Linux，它使用 musl 库，专为静态链接而生
FROM alpine:3.19

# 2. (配方 A)
#    安装编译 CGO (musl) 所需的基础工具 + git
RUN apk add --no-cache gcc musl-dev git

# 3. (配方 B)
#    安装 Go 1.22.x (我们使用 Go 1.22.10，这是一个已知安全的版本)
#    我们手动下载，以 100% 确保版本正确
ARG GO_VERSION="1.22.10"
RUN wget https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz
#    将 Go 添加到环境变量
ENV PATH="/usr/local/go/bin:${PATH}"

# 4. (前端需求)
#    安装 Node.js, npm, 和 pnpm
RUN apk add --no-cache nodejs npm
RUN npm i -g pnpm

# 5. 设置一个工作目录 (Codespaces 会自动挂载)
WORKDIR /workspaces

# (可选) 验证安装
RUN go version
RUN node -v
RUN pnpm -v
