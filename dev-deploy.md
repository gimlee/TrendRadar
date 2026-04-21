如果需要自定义修改代码或构建自己的镜像：

# 克隆项目
git clone https://github.com/sansan0/TrendRadar.git
cd TrendRadar

# 修改配置文件
vim config/config.yaml
vim config/frequency_words.txt

# 使用构建版本的 docker compose
cd docker
cp docker-compose-build.yml docker-compose.yml

# 关闭BUILDKIT
DOCKER_BUILDKIT=0 docker compose build
docker compose build --no-cache --build-arg http_proxy=http://${hostip}:10808 --build-arg https_proxy=http://${hostip}:10808

构建并启动服务：

# 选项 A：构建并启动所有服务
docker compose build
docker compose up -d

# 选项 B：仅构建并启动新闻推送服务
docker compose build trendradar
docker compose up -d trendradar

# 选项 C：仅构建并启动 MCP AI 分析服务
docker compose build trendradar-mcp
docker compose up -d trendradar-mcp


如果你改的是 config/config.yaml，推荐直接执行这一条，让主程序立刻重新跑一遍：
docker exec trendradar python -m trendradar
然后看日志，等出现这类字样再刷新页面：
docker logs -f trendradar