<div align="center">

<h1>Mangio-RVC-Fork (Retrieval-based-Voice-Conversion) 💻 </h1>
A fork of an easy-to-use SVC framework based on VITS with top1 retrieval 💯. <br><br>
<b> 

> 💓 Please support the original [RVC repository](https://www.bilibili.com/video/BV1pm4y1z7Gm/). Without it, obviously this fork wouldn't have been possible. The Mangio-RVC-Fork aims to essentially enhance the features that the original RVC repo has in my own way. Please note that this fork is NOT STABLE and was forked with the intention of experimentation. Do not use this Fork thinking it is a "better" version of the original repo. Think of it more like another "version" of the original repo. Please note that this doesn't have a google colab. If you want to use google colab, go to the original repository. This fork is intended to be used with paperspace and local machines for now.
</b>

## Add me on discord: Funky Town#2048
I am able to communicate with you here and there.

[![madewithlove](https://forthebadge.com/images/badges/built-with-love.svg)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI)
  
[![Licence](https://img.shields.io/github/license/liujing04/Retrieval-based-Voice-Conversion-WebUI?style=for-the-badge)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI/blob/main/%E4%BD%BF%E7%94%A8%E9%9C%80%E9%81%B5%E5%AE%88%E7%9A%84%E5%8D%8F%E8%AE%AE-LICENSE.txt)
[![Huggingface](https://img.shields.io/badge/🤗%20-Spaces-yellow.svg?style=for-the-badge)](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

<img src="https://33.media.tumblr.com/2344c05b16d25e60771d315604f90258/tumblr_nmy9cc0Zm71syljkjo1_1280.gif" /><br>
  
</div>

------

> The original RVC [Demo Video](https://www.bilibili.com/video/BV1pm4y1z7Gm/) here!

> Realtime Voice Conversion Software using RVC : [w-okada/voice-changer](https://github.com/w-okada/voice-changer)

> The dataset for the pre-training model uses nearly 50 hours of high quality VCTK open source dataset.

> High quality licensed song datasets will be added to training-set one after another for your use, without worrying about copyright infringement.
# Summary 📘
## Features that this fork (Mangio-RVC-Fork) has that the original repo doesn't ☑️
+ Local inference with the conv2d 'Half' exception fix. apply the argument --use_gfloat to infer-web.py to use this fix.
+ f0 Inference algorithm overhaul: 🌟
  + Added pyworld dio f0 method.
  + Added torchcrepe crepe f0 method. (Increases pitch accuracy and stability ALOT)
  + Modifiable crepe_hop_length for the crepe algorithm via the web_gui
+ f0 Crepe Pitch Extraction for training. 🌟 (EXPERIMENTAL) Works on paperspace machines but not local mac/windows machines. Potential memory leak. Watch out.
+ Paperspace integration 🌟
  + Paperspace argument on infer-web.py (--paperspace) that shares a gradio link
  + Make file for paperspace users
+ Tensorboard access via Makefile (make tensorboard)
+ Total epoch slider for the training now limited to 10,000 not just 1000.

## This repository has the following features too:
+ Reduce tone leakage by replacing source feature to training-set feature using top1 retrieval;
+ Easy and fast training, even on relatively poor graphics cards;
+ Training with a small amount of data also obtains relatively good results (>=10min low noise speech recommended);
+ Supporting model fusion to change timbres (using ckpt processing tab->ckpt merge);
+ Easy-to-use Webui interface;
+ Use the UVR5 model to quickly separate vocals and instruments.

## Features planned to be added during the fork's development ▶️
+ Improved GUI (More convenience).
+ Google colab notebook for this fork.
+ Automatic removal of old generations to save space.
+ Potentially a pyin f0 method or a hybrid f0 crepe method.

# About this fork's crepe training: 
Crepe training is still incredibly instable and there's been report of a memory leak. This will be fixed in the future, however it works quite well on paperspace machines. Please note that crepe training adds a little bit of difference against a harvest trained model. Crepe sounds clearer on some parts, but sounds more robotic on some parts too. Both I would say are equally good to train with, but I still think crepe on INFERENCE is not only quicker, but more pitch stable (especially with vocal layers). Right now, its quite stable to train with a harvest model and infer it with crepe. If you are training with crepe however (f0 feature extraction), please make sure your datasets are as dry as possible to reduce artifacts and unwanted harmonics as I assume the crepe pitch estimation latches on to reverb more.

# Installing the Dependencies 🖥️
Using pip (python3.9.8 is stable with this fork)

## Paperspace Users:
```bash
cd Mangio-RVC-Fork
make install # Do this everytime you start your paperspace machine
```

## Windows/MacOS
**Notice**: `faiss 1.7.2` will raise Segmentation Fault: 11 under `MacOS`, please use `pip install faiss-cpu==1.7.0` if you use pip to install it manually.

```bash
pip install -r requirements.txt
```

# Preparation of other Pre-models ⬇️
## Paperspace Users:
```bash
cd Mangio-RVC-Fork
make base # Do only once after cloning this fork (No need to do it again unless pre-models change on hugging face)
```

## Local Users
RVC requires other pre-models to infer and train.
You need to download them from our [Huggingface space](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/).

Here's a list of Pre-models and other files that RVC needs:
```bash
hubert_base.pt

./pretrained 

./uvr5_weights

#If you are using Windows, you may also need this dictionary, skip if FFmpeg is installed
ffmpeg.exe
```
# Running the Web GUI to Infer & Train 💪

## For paperspace users:
```bash
cd Mangio-RVC-Fork
make run
```
Then click the gradio link it provides.

# Running the Tensorboard 📉
```bash
cd Mangio-RVC-Fork
make tensorboard
```
Then click the tensorboard link it provides and refresh the data.

# Other 

If you are using Windows, you can download and extract `RVC-beta.7z` to use RVC directly and use `go-web.bat` to start Webui.

There's also a tutorial on RVC in Chinese and you can check it out if needed.

## Credits
+ [ContentVec](https://github.com/auspicious3000/contentvec/)
+ [VITS](https://github.com/jaywalnut310/vits)
+ [HIFIGAN](https://github.com/jik876/hifi-gan)
+ [Gradio](https://github.com/gradio-app/gradio)
+ [FFmpeg](https://github.com/FFmpeg/FFmpeg)
+ [Ultimate Vocal Remover](https://github.com/Anjok07/ultimatevocalremovergui)
+ [audio-slicer](https://github.com/openvpi/audio-slicer)
## Thanks to all contributors for their efforts

<a href="https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI/graphs/contributors" target="_blank">
  <img src="https://contrib.rocks/image?repo=liujing04/Retrieval-based-Voice-Conversion-WebUI" />
</a>

