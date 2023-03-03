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
* [Installation](#install)
* [Getting Started](#start)
    1. [Edit your starting parameters](#params)
    1. [Getting a model](#model)
    1. [Getting a VAE](#vae)
    1. [Launching and settings](#launch)
    1. [Prompts](#prompts)
    1. [Adding extensions](#extensions)
* Loras
* Upscaling
* ControlNet
* Tips for training character Loras
 
&nbsp;

# Introduction <a name="intro"></a>

Stable Diffusion is a very powerful AI image generation software you can run on your own home computer. It uses "models", which function like the brain of the AI, and can make almost anything given that someone has trained it to do it. The biggest uses are anime art, photorealism, and NSFW content.

The images you create may be used for any purpose, depending on the used model's license. Whether they are "yours" in a legal sense varies by local laws and is often inconclusive. Neither I or any of the people involved in Stable Diffusion or its models are responsible for anything you make, and you are expressively forbidden from creating illegal or harmful content.

&nbsp;

# Installation <a name="install"></a>

* __**Requirements:**__ To run Stable Diffusion on your own computer you'll need at least 16 GB of RAM and 4 GB of VRAM. I will only cover the case where you are running Windows 10/11 and using an NVIDIA graphics card series 16XX, 20XX or 30XX (though 10XX also work). AMD users are out of luck, as it's very inconsistent to get it working. Same with Linux and Mac, though it's possible to do it.

* __**Installer:**__ The easiest way is to download the latest release [HERE](https://github.com/EmpireMediaScience/A1111-Web-UI-Installer/releases). 

* __**Alternative:**__ If you don't meet the hardware requirements, don't worry, you can still use Stable Diffusion for free to its full extent through Google Collab. It borrows Google's computers to use AI, with variable time limitations, usually a few hours every day. To get started, [go here](https://colab.research.google.com/github/TheLastBen/fast-stable-diffusion/blob/main/fast_stable_diffusion_AUTOMATIC1111.ipynb#scrollTo=PjzwxTkPSPHf) and follow the steps.

&nbsp;

# Getting Started <a name="start"></a>

Before generating some images, here are some useful steps you can follow to improve your experience.

1. **Edit your starting parameters:** <a name="params"></a> If you're using the collab, skip this step. If you're using the launcher, turn on **medvram** and **xformers**. Then, set your *Additional Launch Options* to: `--opt-channelslast --no-half-vae`. All of these should offer minor but significant improvements to performance.
    * If your graphics card has more than 8 GB of VRAM, you may turn off medvram to make generations faster. However, medvram still allows you to generate larger images and more images at the same time.
    * If your graphics card has 4 or 6 GB of VRAM, add `--opt-split-attention-v1` as it may lower vram usage even further.
    * If you want to run the program from your computer but want to use it in another device, such as your phone, add `--listen`. Then, use your computer's local IP in the same WiFi network to access the interface.
    * If you're using the original stable-diffusion-webui, you can add these parameters by editing your webui-user.bat, right next to `set COMMANDLINE_ARGS=`
    * Full list of possible parameters [here](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings)

1. **Getting a model:** <a name="model"></a> There are many options, most of which are on [civitai](https://civitai.com). But which to choose? These are my recommendations:
    * For anime, [7th Heaven Mix](https://civitai.com/models/4669/corneos-7th-heaven-mix) has a nice aesthetic similar to anime movies, while [Abyss Orange Mix 3](https://civitai.com/models/9942/abyssorangemix3-aom3) *(__Note:__ scroll down and choose the AOM3 option)* offers more realism, advanced lighting, softer shading, and more lewdness. I remixed the two options above into [Heaven Orange Mix](https://civitai.com/models/14305/heavenorangemix).
    * For creative art go with [DreamShaper](https://civitai.com/models/4384/dreamshaper), there are few options quite like it. An honorable mention goes to [Pastel Mix](https://civitai.com/models/5414/pastel-mix-stylized-anime-model), which has a beautiful and unique aesthetic with the addition of anime.
    * For photorealism go with [Deliberate](https://civitai.com/models/4823/deliberate), it can do almost anything, specially photographs.
    * The [Uber Realistic Porn Merge](https://civitai.com/models/2661/uber-realistic-porn-merge-urpm) is self-explanatory.
     
    *Launcher:* It will let you choose the path to your models folder. Otherwise the models normally go into `stable-diffusion-webui/models/Stable-diffusion`.

    *Collab:* copy the **direct download link to the file** and put it in `MODEL_LINK:`. Turn on `safetensors`, and `Use_temp_storage` if you don't want to save it to your google drive. After the first time you use the collab, you may place more models manually into your Google Drive folder at: `MyDrive/sd/stable-diffusion-webui/models/Stable-diffusion`

1. **Getting a VAE:** <a name="vae"></a> Most models don't come with a VAE built in. The VAE is a small separate model, which "converts your image from AI format into human format". Without it, you'll get faded colors and ugly eyes, among other things.

    There are practically only 3 different VAEs out there worth talking about:
    * [anime vae](https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/VAEs/orangemix.vae.pt), also known as the AnythingV3 vae, also known as the orangemix vae. All anime models use this.
    * [vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/blob/main/vae-ft-mse-840000-ema-pruned.safetensors), the latest from Stable Diffusion itself. Used by photorealism models and such.
    * [kl-f8-anime2](https://huggingface.co/hakurei/waifu-diffusion-v1-4/resolve/main/vae/kl-f8-anime2.ckpt), also known as the waifu diffusion VAE, it is older and produces much brighter results. Used by Pastel Mix.

    *Launcher:* It lets you choose the default VAE, otherwise put them in the `stable-diffusion-webui/models/VAE` folder.
   
    *Collab:* You will have to place it in your Google Drive, in `MyDrive/sd/stable-diffusion-webui/models/VAE`.

1. **Launching and settings:** <a name="launch"></a> It is finally time to launch the WebUI.  
    *Launcher:* Press the button on the launcher and wait patiently for it to start. Then, it will open the interface in your browser. It's like a website, but on your computer.  
    *Collab:* Press the play buttons, **in order, one at a time**. Wait for each one to finish before pressing the next one. **You may skip the ControlNet section this time**. When the final step is finished, it will produce a link you can use to access the interface as a website. This will be open as long as the page stays open.

    The starting page is where you can make your images. But first, we'll go to the Settings tab. There will be sections on the left.
    * In the *Stable Diffusion* section, scroll down and increase **Clip Skip** from 1 to 2. This is said to produce better images, specially for anime. You can also set your VAE from here, but I have a better idea:
    * In the *User Interface* section, scroll down to **Quicksettings list** and change it to `sd_model_checkpoint, sd_vae`.
    * Scroll back up, click the big orange **Apply settings** button, then **Reload UI** next to it. You can now change your model as well as your VAE from the top of the page at any time.

1. **Prompts:** <a name="prompts"></a>

    On the first tab, **txt2img**, you'll be making most of your images. This is where you'll find your *prompt* and *negative prompt*.  
    Stable Diffusion is not like Midjourney or other popular image generation software, you can't just ask it what you want and get a good image. You have to be specific. *Very* specific.  
    I will show you an example of a prompt and negative prompt:
   
    * Anime
        * `2d, masterpiece, best quality, anime, highly detailed face, highly detailed eyes, highly detailed background, perfect lighting`
        * `EasyNegative, worst quality, low quality, 3d, realistic, photorealistic, (loli, child, teen, baby face), zombie, animal, multiple views, text, watermark, signature, artist name, artist logo, censored`
     
    * Photorealism
        * `best quality, 4k, 8k, ultra highres, (realistic, photorealistic, RAW photo:1.4), (hdr, sharp focus:1.2), intricate texture, skin imperfections`
        * `EasyNegative, worst quality, low quality, normal quality, child, painting, drawing, sketch, cartoon, anime, render, 3d, blurry, deformed, disfigured, morbid, mutated, bad anatomy, bad art`

    * **EasyNegative:** The negative prompts above use EasyNegative, which is a *textual inversion embedding* or "magic word" that codifies many bad things to make your images better. Typically one would write a very long, very specific, very redundant, and sometimes silly negative prompt. EasyNegative is as of March 2023 the best choice if you want to avoid that.
        * [Get EasyNegative here](https://huggingface.co/datasets/gsdf/EasyNegative/resolve/main/EasyNegative.safetensors) and put it in your `stable-diffusion-webui/embeddings` folder. Then, go to the bottom of your WebUI page and click *Reload UI*. It will now work when you type the word.

    After a "base prompt" like the above, you may then start typing what you want. For example `young woman in a bikini in the beach, full body shot`. Feel free to add other terms you don't like to your negatives such as `old, ugly, futanari, furry`, etc.
    You can also save your prompts to reuse later with the buttons below Generate. Click **Save style** and give it a name. Later, you can open your *Styles* dropdown to choose, then click *Apply selected styles to the current prompt*.
  
1. **Adding extensions:** <a name="extensions"></a>