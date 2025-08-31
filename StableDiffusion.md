
[喂饭级stable_diffusion_webUI使用教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/617997179)

WebUI 通过浏览器与程序进行交互
	[Web-UI设计，你需要了解的！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/250029144)
	[web端ui是不是就是网页设计？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/35117155)

midjourney 的使用，扁平化素材（小人，icon）的生成
[Midjourney](https://www.midjourney.com/home?callbackUrl=%2Fexplore)

### 其他的模型

**DALL·E 2**[https://openai.com/dall-e-2/](https://link.zhihu.com/?target=https%3A//openai.com/dall-e-2/) _

[设计师的 Midjourney 入门真保姆级教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/617025808)

## Python 环境配置：CUDA & Pytorch 

stable diffusion 是机器学习模型，web-ui 对他进行了封装，于是需要通过 Anaconda 和 python 进行环境管理和启动

python版本至少为3.9，web-ui官方建议使用python3.10或3.11，更高的版本可能不兼容部分插件

Anaconda 的安装和环境配置参考 [[Anaconda]] 和 [[Anaconda#创建虚拟环境]]

通过 conda 安装匹配版本的 PyTorch，同时要注意 CUDA 版本，webui会自动安装PyTorch，可以手动安装确保版本合适

检查 CUDA 版本。在命令行输入
```bash
nvidia-smi
```
输出右上角显示 **CUDA Version: 12.2**，为可以使用的最高 CUDA 版本而不是当前使用的。
参考 PyTorch 官方版本表选择 PyTorch 版本 [Get Started](https://pytorch.org/get-started/locally/) 
不然可能出现 `cuDNN_STATUS_NOT_INITIALIZED` 错误

验证 CUDA 是否可用：
```bash
python -c "import torch; print(torch.cuda.is_available())"
```

```python
import torch

# 检查 PyTorch 版本
print(f"PyTorch 版本: {torch.__version__}")

# 检查 PyTorch 使用的 CUDA 版本
print(f"PyTorch 使用的 CUDA 版本: {torch.version.cuda}")

# 检查 GPU 是否可用
print(f"CUDA 可用: {torch.cuda.is_available()}")

# 获取当前设备信息
if torch.cuda.is_available():
    print(f"当前设备: {torch.cuda.get_device_name(0)}")
    print(f"设备计算能力: {torch.cuda.get_device_capability(0)}")
```

示例,CUDA 11.8 情况下下载 pytorch 
```bash
conda install pytorch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 pytorch-cuda=11.8 -c pytorch -c nvidia
```
如果不太清楚部署的语句，可以问 deepseek
```bash
pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 --index-url https://download.pytorch.org/whl/cu118
pip install torch==2.7.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
```
[完整深度学习环境安装指南 (PyTorch 2.7.1 + CUDA 12.8) - 郭早起 - 博客园](https://www.cnblogs.com/guozaoqi/p/19009347)


cd 命令异常: [windows下命令行模式中cd命令无效的原因-CSDN博客](https://blog.csdn.net/qq_45061258/article/details/113282513)
下载显卡驱动: [Download The Official NVIDIA Drivers | NVIDIA](https://www.nvidia.com/en-us/drivers/)
 CUDA 计算能力 [CUDA GPU Compute Capability | NVIDIA Developer](https://developer.nvidia.com/cuda-gpus)

## Stable Diffusion 模型本地部署

**Stable Diffusion** 官方网站
[https://stability.ai/blog/stabl](https://link.zhihu.com/?target=https%3A//stability.ai/blog/stable-diffusion-public-release)
[Stable Diffusion Online (stablediffusionweb.com)](https://stablediffusionweb.com/#ai-image-generator)
[Stability AI Image Models — Stability AI](https://stability.ai/stable-image)

### WebUI 的下载

webui开源代码地址：[AUTOMATIC1111/stable-diffusion-webui: Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui) ，以此进行 git 部署 stable-diffusion-webui
	在 git bash 中输入 `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui`，即可下载文件夹

这也是一个 webui [Sygil-Dev/sygil-webui: Stable Diffusion web UI](https://github.com/Sygil-Dev/sygil-webui)

推荐使用 ComfyUI：[comfyanonymous/ComfyUI: The most powerful and modular diffusion model GUI, api and backend with a graph/nodes interface.](https://github.com/comfyanonymous/ComfyUI)

项目安装后，在 conda 环境中安装 webui 依赖 （非必要，webui会自动安装依赖）
```bash
pip install -r requirements.txt
or
conda install --yes --file requirements.txt
```
国内需要加速可以使用清华镜像源
```bash
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
或者设置全局镜像源，再安装
```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

### 启动 WebUI
#### stable-diffusion-webui 脚本启动

使用官方提供的脚本 ,在 `webui-user.bat` (git clone 后文件夹中) 中
`set PYTHON=` 写入 `python.exe` 的位置，`set COMMANDLINE_ARGS=` 中写入启动参数,如：

```bash
@echo off

set PYTHON="D:\Python\Python310\python.exe"
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--listen --xformers --medvram

call webui.bat
```
启动 `webui-user.bat`，它会自动用 `set PYTHON ` 的 python 创建 venv 虚拟环境，然后启动 webui

**不使用webui官方脚本启动**
在 conda prompt 或者命令行中使用以下语句启动虚拟环境
```bash
cd /dG:\stable-diffusion-webui
conda activate G:\conda_envs\sd-webui
```
在虚拟环境下启动 WebUI
```bash
python launch.py --listen --xformers
python launch.py --listen
python launch.py --xformers
```
`--listen` 参数启用外部网络连接
`--xformers` 参数可以提升生成速度 `


脚本会自动启动 Web 服务器，并在命令行中显示本地访问链接（通常为 `http://127.0.0.1:7860`，或者使用 `http://localhost:7860`，浏览器输入即可

可以自己编写一键启动的 bat 文件
```bash
@echo off
cd /d "G:\stable-diffusion-webui"
call conda activate "G:\conda_envs\sd-webui"
python launch.py --listen --xformers --medvram
pause
```

若需进一步优化显存或速度，可扩展启动命令：
```bash
python launch.py --listen --xformers --medvram --opt-split-attention --no-half-vae
```

|参数|作用|适用场景|
|---|---|---|
|`--opt-split-attention`|优化注意力计算，降低显存占用|4-6GB显存|
|`--no-half-vae`|禁用VAE半精度，减少色块问题|低端显卡（如GTX 10系列）|
| `--medvram`             | 优化显存，降低一点性能          | 8-10GB显存        |
| `--lowvram`             | 比`--medvram`更彻底，破坏性能 | 6GB以下显存         |


#### stable-diffusion-webui 扩展管理
在 extension 中选择 avaliable 进行操作，但是可能会因为网络问题不成功，出现 `AssertionError: extension access disabled because of command line flags` 。可参考[喂饭级stable_diffusion_webUI使用教程 - 知乎](https://zhuanlan.zhihu.com/p/617997179)
建议用 git 在 extensions 文件夹下 clone

#### ComfyUI 启动

使用 conda 环境来运行 comfyui 项目
在 conda prompt 或者命令行中使用以下语句启动虚拟环境
```bash
cd /dG:\ComfyUI
conda activate G:\conda_envs\comfyui
```
然后使用以下命令启动:
```bash
python main.py
```

浏览器方位 `http://localhost:8188`
#### ComfyUI 插件和模型管理

下载插件和模型：[Git 安装和使用指南 | ComfyUI Wiki](https://comfyui-wiki.com/zh/install/install-comfyui/install-git)
插件位置 `ComfyUI/custom_nodes`；
模型存放位置：
- Checkpoint 模型: `models/checkpoints`
- LoRA 模型: `models/loras`
- VAE 模型: `models/vae`
- Embedding 模型: `models/embeddings`



## models & extensions 模型和插件管理

#### 绘图模型

绘图模型是为了特定风格进行训练的特化模型，不同模型生成不同风格的图片
模型文件放在 `models/Stable-diffusion` 目录下

如果你没有下载任何模型,那么在webui启动前会自动下载一个[v1-5-pruned-emaonly.safetensors](https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors)模型,下载完才启动。这个模型不适合直接使用，但适合训练

有关模型的解释：[终极指南！Stable Diffusion 模型全解析，看这篇就够了_stablediffusion 模型-CSDN博客](https://blog.csdn.net/ice_99/article/details/146556735) 

模型下载站：[Civitai: The Home of Open-Source Generative AI](https://civitai.com/)
SD 1.5 官方基础大模型 [stablediffusiontutorials/stable-diffusion-v1.5 · Hugging Face](https://huggingface.co/stablediffusiontutorials/stable-diffusion-v1.5) 
绘制二次元风格的 MeinaMix : [Meina/MeinaMix · Hugging Face](https://huggingface.co/Meina/MeinaMix) [Meina/MeinaMix at main](https://huggingface.co/Meina/MeinaMix/tree/main) 
写实风格的 majicMIX realistic 麦橘写实  [majicMIX realistic 麦橘写实 - v7 | Stable Diffusion Checkpoint | Civitai](https://civitai.com/models/43331/majicmix-realistic) 
其他常用模型：[超全 Stable Diffusion 常用模型推荐（含网盘下载链接） - 知乎](https://zhuanlan.zhihu.com/p/28932301846) 

#### LoRA 模型微调

具体我也没有用过，似乎需要提示词进行激活？

LoRA 模型存放路径
```bash
stable-diffusion-webui/
└── models/
    └── Lora/  # LoRA文件存放位置
        ├── koreanDollLikeness_v10.safetensors
        └️── detailEnhancer_v20.safetensors
```

#### Controlnet 姿势管理

controlnet 提供了将骨骼文件导入程序，指导 AI 生成特定动作的方法
使用方法参考：[【AI绘画】完美控制画面！告别抽卡时代 人物动作控制/景深/线稿上色 Controlnet安装使用教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Wo4y1i77v/?spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=abb373670a9fcb03baabf3e1d393d6fa)
[【AI绘画】革命性技术突破：ControlNet_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1XA411m7s2/?spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=abb373670a9fcb03baabf3e1d393d6fa)

插件下载：[Mikubill/sd-webui-controlnet: WebUI extension for ControlNet](https://github.com/Mikubill/sd-webui-controlnet) ，同样使用 git，在 `G:\stable-diffusion-webui\extensions` 中管理
模型下载： https://huggingface.co/webui/ControlNet-modules-safetensors/tree/main ，比如 `control_openpose-fp 16.safetensors` ，该模型放在文件夹 `G:\stable-diffusion-webui\extensions\sd-webui-controlnet\models` 下，此文件夹在安装 sb-webui-controlnet 后出现 


#### ADtailer 局部重绘

下载：[Bing-su/adetailer: Auto detecting, masking and inpainting with detection model.](https://github.com/Bing-su/adetailer) 
使用参考：[Stable Diffusion 必装插件之 ADetailer，修脸修手无敌，各种参数详解 - 知乎](https://zhuanlan.zhihu.com/p/678777327) 


## ComfyUI 使用实践


### 碎片

Latent 算法再潜空间进行放大，出图后会与原画风有差别
想要贴近原画风可以选择传统模型放大，如 R-ESRGAN 4x+，但是细节没有 latent 精细

放大修复可以用 title，修脸可以用 facedetail

缩放 latent：按照设定的宽度和高度对图像进行放大
缩放 Latent（比例）：按照设定的具体比例对图像进行放大，小于 2 倍得倍数效果可能不是很明显

K 采样器的“降噪”组好设置在 0.5 以上，经过测试 0.5 是个比较好的数值

菲伦头像
```
(masterpiece), (best quality), (ultra-detailed), illustration, clean lines, sharp details, absurdres, highres, perfect face, beautiful eyes,
Fern (Frieren: Beyond Journey's End), portrait, 1girl, solo, headshot, upper body, purple hair, long hair, purple eyes, human, elegant, gentle expression, determined yet kind look, anime style, line art emphasis, clean white background, wearing wedding dress, smiling
```
菲伦学院风
positive prompt
```
(masterpiece), (best quality), (ultra-detailed), illustration, clean lines, sharp details, absurdres, highres, perfect face, beautiful eyes,8K, (eyes:1.3),(detailed eyes:1.2), 
perfect eyes, sharp eyes, beautiful detailed eyes, shining pupils, full body,((detailed eyes, detailed face, detailed skin))
Fern (Frieren: Beyond Journey's End), full body portrait, 1girl, solo, purple hair, long hair, purple eyes, human, elegant, gentle expression, determined yet kind look, anime style, line art emphasis,
(pure white background:1.1), plain background, no patterns, no borders, no frames, (idol-style sailor uniform, grey blouse, gray pleated skirt, dark red ribbon, black knee-high socks, loafers, decorative ribbon, elaborate bow tie,), school emblem,
holding school bag, casual elegant stance, gentle posture,
```
negative prompt
```
(worst quality), (low quality), (normal quality),(bad anatomy),(bad hands),(extra fingers), (fused fingers), (missing fingers),
(malformed hands),(poorly drawn hands),(disfigured hands),(long fingers),(bad proportions), (extra limbs),(deformed limbs),
(text),(logo),(watermark),(signature),(blurry),(duplicate),(cropped),(error),(mutation),(deformed face),(bad eyes),(bad mouth),(bad face),(extra arms),(extra legs),(ugly),(tiling),(nsfw),
(frame, border, ornate border, decorative frame, background patterns, flowers in background, ornate design in background, watermark, text),
blurry eyes, bad eyes, deformed eyes, extra eyes, (plain design, simple uniform, boring outfit, lack of details)
```