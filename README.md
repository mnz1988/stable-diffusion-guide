---
license: wtfpl
tags:
- guide
- stable diffusion
- webui
- automatic1111
- stable-diffusion-webui
---

# Index

* [Introduction](#intro)
* [Installation](#inst)
* [Google Collab](#collab)

# Introduction <a name="intro"></a>

Stable Diffusion is a very powerful AI image generation software you can run on your own home computer. It uses "models", which function like the brain of the AI, and can make almost anything given that someone has trained it to do it. The biggest uses are anime art, photorealism, and NSFW content.

The images you create may be used for any purpose, depending on the used model's license. Whether they are "yours" in a legal sense varies by local laws and is often inconclusive. Neither I or any of the people involved in Stable Diffusion or its models are responsible for anything you make, and you are expressively forbidden from creating illegal or harmful content.

# Installing <a name="inst"></a>

* __**Requirements:**__ To run Stable Diffusion on your own computer you'll need at least 16 GB of RAM and 4 GB of VRAM. I will only cover the case where you are running Windows 10/11 and using an NVIDIA graphics card series 16XX, 20XX or 30XX (though 10XX also work). AMD users are out of luck, as it's very inconsistent to get it working. Same with Linux and Mac, though it's possible to do it.
* __**Alternative:**__ If you don't meet the hardware requirements, don't worry, you can still use Stable Diffusion for free to its full extent through [Google Collab](#collab)
* __**Installer:**__ The easiest way is to download the latest release [HERE](https://github.com/EmpireMediaScience/A1111-Web-UI-Installer/releases). 

# Getting Started <a name="start"></a>

Before generating some images, here are some useful steps you can follow to improve your experience.

1. __**Edit your starting parameters:**__ If you are using the launcher, turn on **medvram** and **xformers**. Then, set your *Additional Launch Options* to: `--opt-channelslast --no-half-vae`. All of these should offer minor but significant improvements to performance.
    * If your graphics card has more than 8 GB of VRAM, you may turn off medvram to make generations faster. However, medvram still allows you to generate larger images and more images at the same time.
    * If your graphics card has 4 or 6 GB of VRAM, add `--opt-split-attention-v1` as it may lower vram usage even further.
    * If you want to run the program from your computer but want to use it in another device, such as your phone, add `--listen`. Then, use your computer's local IP in the same WiFi network to access the interface.
    * If you're not using the launcher but the original stable-diffusion-webui, you can add these parameters by editing your webui-user.bat, right next to `set COMMANDLINE_ARGS=`
    * Full list of possible parameters [here](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings)

2. __**Download a model**__ There are many options, most of which are on [civitai](https://civitai.com). But which to choose? These are my recommendations:
    * For anime, [7th Heaven Mix](https://civitai.com/models/4669/corneos-7th-heaven-mix) has a nice aesthetic similar to anime movies, while [Abyss Orange Mix 3](https://civitai.com/models/9942/abyssorangemix3-aom3) *(__Note:__ scroll down and choose the AOM3 option)* offers more realism, advanced lighting, softer shading, and more lewdness. I remixed the two options above into [Heaven Orange Mix](https://civitai.com/models/14305/heavenorangemix)
    * For creative art go with [DreamShaper](https://civitai.com/models/4384/dreamshaper), there are few options quite like it. An honorable mention goes to [Pastel Mix](https://civitai.com/models/5414/pastel-mix-stylized-anime-model), which has a beautiful and unique aesthetic with the addition of anime.
    * For photorealism go with [Deliberate](https://civitai.com/models/4823/deliberate), it can do almost anything, specially photographs.
    * The [Uber Realistic Porn Merge](https://civitai.com/models/2661/uber-realistic-porn-merge-urpm) is self-explanatory.

3