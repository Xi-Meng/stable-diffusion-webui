# 基于stable diffusion models的面向多维变化的模特穿衣
## 实验环境搭建
- 使用A100机器
- docker镜像及其启动
```
docker pull nvidia/cuda:12.2.2-cudnn8-devel-ubuntu22.04
docker run --gpus all -v ~/:/workspace --name xmy_nvidia_workspace -u root -itd --device=/dev/dri --security-opt seccomp=unconfined --group-add video nvidia/cuda:12.2.2-cudnn8-devel-ubuntu22.04
```
- 进入docker：
```
docker exec -it xmy_nvidia_workspace /bin/bash
```
- 配置网络代理并搭建基本环境
```
apt-get update
apt install git software-properties-common -y
add-apt-repository ppa:deadsnakes/ppa -y
apt install python3.10-venv -y
```

- 创建新用户user，并赋予相应权限，同时切换到新用户user。（./webui.sh的运行不能以root用户运行，因此要创建新用户。）
```
adduser user
chown -R user:user ./stable-diffusion-webui
su - user
```
- 搭建环境的所有命令如下：
```
git clone https://github.com/Xi-Meng/stable-diffusion-webui && cd stable-diffusion-webui
python3.10 -m venv venv
./webui.sh
```
- 可以先提前拉取实验中所有需要用到的模型，也可以等报错之后再拉取。（由于Huggingface被墙因此一定会报错）
```
wget https://hf-mirror.com/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors
```
```
mkdir openai
cd openai
git clone https://gitee.com/hf-models/clip-vit-large-patch14.git
```
- 关闭网络代理，然后再运行启动命令`./webui.sh`。（如果不关闭网络代理，会遇到localhost is not accessible的问题。）。此时页面既可以进行正常展示并且进行使用

## 实验结果
见实验报告中。

## 相关网站
- 可以在以下网站中找到相关的prompt和所有的可用模型。
https://civitai.com/models/43331/majicmix-realistic?modelVersionId=176425
