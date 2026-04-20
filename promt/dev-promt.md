提示词

# P1
我在config/config.yaml中之前配置了MiniMax-M2.7，后面又改回了deepseek,然后执行了
docker restart trendradar
docker exec -it trendradar python manage.py start_webserver
执行后，在http://localhost:8080/#tab-0上最后显然的内容包含如下内容：
 AI 分析失败: AI 分析失败 (BadRequestError): litellm.BadRequestError: LLM Provider NOT provided. Pass in the LLM provider you are trying to call. You passed model=MiniMax-M2.7 Pass model as E.g. For 'Huggingface' inference endpoints pass in `co...
请解决。
这个项目中.env和config.yaml到底是什么关系，帮助文档怎么又说.env会覆盖config.yaml？