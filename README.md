# Kohya_ss SDXL训练包

支持一键下载模型，一键启动训练webui
内置内网穿透（需自行配置）和gohttpserver实用工具
欢迎加群 https://r.t4wefan.pub/s/913 反馈问题

# 开始训练前推荐先更新`start.ipynb`

复制粘贴下面一行命令到终端执行
或者在启动展示的ipynb文件中执行(v4及之后的版本已内置此代码块)

```bash
rm -rf /root/start.ipynb && wget https://drive.t4wefan.pub/d/autodl/sdxl/latest/start.ipynb
```

# 注意，多卡首次使用需要配置accelerate

## 单卡默认已配置，如有报错跟随下面的指引配置

## 步骤 1：输入accelerate config

首先，在命令行中输入以下命令：

Copy

```
accelerate config
```

## 步骤 2：选取本机并选择GPU

接下来，您将被提示选择加速库的安装方式。请按照以下步骤进行操作：

1. 选择 "this machine" 选项，以便安装加速库到本机。
2. 选择 "GPU" 选项，以便在GPU上运行模型。

## 步骤 3：按回车键继续

现在，您将被要求回答一些问题以配置加速库。在这些问题中，我们将使用默认选项，因此只需按回车键继续即可。

## 步骤 4：选择精度

最后，您将被要求选择模型精度。您可以选择使用fp16或bf16。这取决于您的应用程序和硬件。在这里，我们将选择使用fp16，因为它可以提供比较好的性能和准确度。

完成以上步骤后，您的环境就已经配置好了。现在可以开始使用加速库来加速您的模型了。

## 基本环境

框架及版本 pytorch2.0.1
CUDA版本 117 or 118

## 构建过程

详见

```
https://drive.t4wefan.pub/d/code/kohya/Kohya_ss.md
```

### 代码Clone

已经写入ipynb文档，启动即可

### 依赖安装

默认已安装，ipynb文档中有安装命令，下面有完整的部署文档

## 以下是我手写的部署文档的原文

# Kohya ss py3.11

## Run

**start webui (also avaiable for autodl if you have frp or port forwarding)**

```
./gui.sh --server_port 28000 --listen 0.0.0.0 --headless
```

**start webui for autodl**

```
./gui.sh --server_port 6006 --listen 0.0.0.0 --headless
```

**start auto111 sd-webui for test**

```
conda activate webui && cd /root && ./sd.sh
```

## Deploy

**multi gpu fix**

```
export MKL_SERVICE_FORCE_INTEL=1
export MKL_THREADING_LAYER=GNU
```

**clone repo**

```
git clone -b sdxl-dev https://github.com/bmaltais/kohya_ss.git
```

**install torch**

```
#cu117
conda install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia

#cu118
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

**install requirements**

```
pip install -r requirements.txt

# if you are using linux
pip install xformers==0.0.20 bitsandbytes==0.35.0 tensorboard==2.12.3 tensorflow==2.12.0
```

**install without file**

```
pip install accelerate==0.19.0 albumentations==1.3.0 altair==4.2.2 dadaptation==3.1 diffusers[torch]==0.18.2 easygui==0.98.3 einops==0.6.0 fairscale==0.4.13 ftfy==6.1.1 gradio==3.36.1 huggingface-hub==0.15.1 lion-pytorch==0.0.6 lycoris_lora==1.8.0 invisible-watermark==0.2.0 open-clip-torch==2.20.0 opencv-python==4.7.0.68 prodigyopt==1.0 pytorch-lightning==1.9.0 rich==13.4.1 safetensors==0.3.1 timm==0.6.12 tk==0.1.0 toml==0.10.2 transformers==4.30.2 voluptuous==0.13.1 wandb==0.15.0 xformers==0.0.20 bitsandbytes==0.35.0 tensorboard==2.12.3 tensorflow==2.12.0
```