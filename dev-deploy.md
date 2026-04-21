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



# 查看运行状态
docker exec -it trendradar python manage.py status

# 手动执行一次爬虫
docker exec -it trendradar python manage.py run

# 查看实时日志
docker exec -it trendradar python manage.py logs

# 显示当前配置
docker exec -it trendradar python manage.py config

# 显示输出文件
docker exec -it trendradar python manage.py files

# Web 服务器管理（用于浏览器访问生成的报告）
docker exec -it trendradar python manage.py start_webserver   # 启动 Web 服务器
docker exec -it trendradar python manage.py stop_webserver    # 停止 Web 服务器
docker exec -it trendradar python manage.py webserver_status  # 查看 Web 服务器状态

# 查看帮助信息
docker exec -it trendradar python manage.py help

# 重启容器
docker restart trendradar

# 停止容器
docker stop trendradar

# 删除容器（保留数据）
docker rm trendradar