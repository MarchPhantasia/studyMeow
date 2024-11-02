
> [!NOTE] 在开始之前，建议配置 `zsh` 以及 `oh-my-zsh`, 以获得更好的命令行体验

# ollama 安装
## 查看 CPU 信息
``` shell
cpuinfo
```


## 通过 sh 安装

- https://ollama.com/download/linux

``` shell
# 建议在网络环境良好的时候使用
# 对网络质量有较高要求
# 使用HIT WLAN拉取的时候速度极慢
curl -fsSL https://ollama.com/install.sh | sh
```

## Manual Install 手动安装

- [下载地址][https://github.com/ollama/ollama/releases/tag/v0.3.12] 请自行选择合适的版本
- [官方文档][https://github.com/ollama/ollama/blob/main/docs/linux.md]

``` shell
# 不建议 curl 来拉ollama的安装包(目前服务器没有专线)，建议在本地下载好后局域网传输给服务器。
# curl -L https://ollama.com/download/ollama-linux-amd64.tgz -o ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
```

## 确认 CUDA 驱动安装

``` shell
nvidia-smi # 查看输出
```

## Ollama 常用命令

``` shell
ollama pull xxxx(模型名称)
ollama run xxxx # 本地推理
ollama list # 查看本地模型
ollama ps # 查看正在运行的模型
```

## Ollama 微调相关

### Llama_factory 微调工具
垂直领域的法律领域的微调[https://www.bilibili.com/video/BV1URsoefE7w/][https://www.bilibili.com/video/BV1URsoefE7w/]
- 比较需要关注知识库格式。

### Streamlit 流式问答 
较为简单的 ai 问答部署[https://streamlit.io/generative-ai][https://streamlit.io/generative-ai]

