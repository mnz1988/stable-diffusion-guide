---
license: wtfpl
tags:
- guide
- stable diffusion
- webui
- automatic1111
- stable-diffusion-webui
---

[If you're in the main page, click here to open this document in full width. The index may not work otherwise.](https://huggingface.co/hollowstrawberry/stable-diffusion-guide/blob/main/README.md)

&nbsp;

# Index <a name="sdguide-index"></a>

* [Introduction](#sdguide-intro)
* [Installation](#sdguide-install)
* [Getting Started](#sdguide-start)
    1. [Edit your starting parameters](#sdguide-params)
    1. [Getting a model](#sdguide-model)
    1. [Getting a VAE](#sdguide-vae)
    1. [Launching and settings](#sdguide-launch)
    1. [Prompts](#sdguide-prompt)
    1. [Generation parameters](#sdguide-gen)
* [Extensions](#sdguide-extensions)
* [Loras](#sdguide-lora)
* [Upscalers](#sdguide-upscale)
* ControlNet
* Tips for training character Loras
 
&nbsp;

# Introduction <a name="sdguide-intro"></a>[▲](#sdguide-index)

Stable Diffusion is a very powerful AI image generation software you can run on your own home computer. It uses "models", which function like the brain of the AI, and can make almost anything given that someone has trained it to do it. The biggest uses are anime art, photorealism, and NSFW content.

The images you create may be used for any purpose, depending on the used model's license. Whether they are "yours" in a legal sense varies by local laws and is often inconclusive. Neither I or any of the people involved in Stable Diffusion or its models are responsible for anything you make, and you are expressively forbidden from creating illegal or harmful content.

&nbsp;

# Installation <a name="sdguide-install"></a>[▲](#sdguide-index)

* __**Requirements:**__ To run Stable Diffusion on your own computer you'll need at least 16 GB of RAM and 4 GB of VRAM. I will only cover the case where you are running Windows 10/11 and using an NVIDIA graphics card series 16XX, 20XX or 30XX (though 10XX also work). AMD users are out of luck, as it's very inconsistent to get it working. Same with Linux and Mac, though it's possible to do it.

* __**Installer:**__ The easiest way is to download the latest release [HERE](https://github.com/EmpireMediaScience/A1111-Web-UI-Installer/releases). 

* __**Alternative:**__ If you don't meet the hardware requirements, don't worry, you can still use Stable Diffusion for free to its full extent through Google Collab. It borrows Google's computers to use AI, with variable time limitations, usually a few hours every day. To get started, [go here](https://colab.research.google.com/github/TheLastBen/fast-stable-diffusion/blob/main/fast_stable_diffusion_AUTOMATIC1111.ipynb#scrollTo=PjzwxTkPSPHf) and follow the steps.

&nbsp;

# Getting Started <a name="sdguide-start"></a>[▲](#sdguide-index)

Before generating some images, here are some useful steps you can follow to improve your experience.

1. **Edit your starting parameters** <a name="sdguide-params"></a>[▲](#sdguide-index)

    If you're using the collab, skip this step.

    If you're using the launcher, turn on **medvram** and **xformers**. Then, set your *Additional Launch Options* to: `--opt-channelslast --no-half-vae`. All of these should offer minor but significant improvements to performance.
    * If your graphics card has more than 8 GB of VRAM, you may turn off medvram to make generations faster. However, medvram still allows you to generate larger images and more images at the same time.
    * If your graphics card has 4 or 6 GB of VRAM, add `--opt-split-attention-v1` as it may lower vram usage even further.
    * If you want to run the program from your computer but want to use it in another device, such as your phone, add `--listen`. Then, use your computer's local IP in the same WiFi network to access the interface.
    * If you're using the original stable-diffusion-webui, you can add these parameters by editing your webui-user.bat, right next to `set COMMANDLINE_ARGS=`
    * Full list of possible parameters [here](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings)

1. **Getting a model** <a name="sdguide-model"></a>[▲](#sdguide-index)

    The model is the brain of your AI, designed for the purpose of producing certain types of images. There are many options, most of which are on [civitai](https://civitai.com). But which to choose? These are my recommendations:
    * For anime, [7th Heaven Mix](https://civitai.com/models/4669/corneos-7th-heaven-mix) has a nice aesthetic similar to anime movies, while [Abyss Orange Mix 3](https://civitai.com/models/9942/abyssorangemix3-aom3) *(__Note:__ scroll down and choose the AOM3 option)* offers more realism in the form of advanced lighting and softer shading, as well as more lewdness. I remixed the two options above into [Heaven Orange Mix](https://civitai.com/models/14305/heavenorangemix). While AOM3 is extremely capable for NSFW, the popular [Grapefruit](https://civitai.com/models/2583/grapefruit-hentai-model) hentai model may also fit your needs.
    * For general art go with [DreamShaper](https://civitai.com/models/4384/dreamshaper), there are few options quite like it in terms of raw creativity. An honorable mention goes to [Pastel Mix](https://civitai.com/models/5414/pastel-mix-stylized-anime-model), which has a beautiful and unique aesthetic with the addition of anime.
    * For photorealism go with [Deliberate](https://civitai.com/models/4823/deliberate). It can do almost anything, but specially photographs. Very intricate results.
    * The [Uber Realistic Porn Merge](https://civitai.com/models/2661/uber-realistic-porn-merge-urpm) is self-explanatory.
     
    *Launcher:* It will let you choose the path to your models folder. Otherwise the models normally go into `stable-diffusion-webui/models/Stable-diffusion`.

    *Collab:* copy the **direct download link to the file** and put it in `MODEL_LINK:`. Turn on `safetensors`, and `Use_temp_storage` if you don't want to save it to your google drive. After the first time you use the collab, you may place more models manually into your Google Drive folder at: `MyDrive/sd/stable-diffusion-webui/models/Stable-diffusion`

    Please note that models in the format `.safetensors` are safe to use while `.ckpt` **may** contain viruses. Be careful.

1. **Getting a VAE** <a name="sdguide-vae"></a>[▲](#sdguide-index)

    Most models don't come with a VAE built in. The VAE is a small separate model, which "converts your image from AI format into human format". Without it, you'll get faded colors and ugly eyes, among other things.

    There are practically only 3 different VAEs out there worth talking about:
    * [anime vae](https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/VAEs/orangemix.vae.pt), also known as the AnythingV3 vae, also known as the orangemix vae. All anime models use this.
    * [vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/blob/main/vae-ft-mse-840000-ema-pruned.safetensors), the latest from Stable Diffusion itself. Used by photorealism models and such.
    * [kl-f8-anime2](https://huggingface.co/hakurei/waifu-diffusion-v1-4/resolve/main/vae/kl-f8-anime2.ckpt), also known as the waifu diffusion VAE, it is older and produces much brighter results. Used by Pastel Mix.

    *Launcher:* It lets you choose the default VAE, otherwise put them in the `stable-diffusion-webui/models/VAE` folder.
   
    *Collab:* You will have to place it in your Google Drive, in `MyDrive/sd/stable-diffusion-webui/models/VAE`.

1. **Launching and settings** <a name="sdguide-launch"></a>[▲](#sdguide-index)

    It is finally time to launch the WebUI.  
    *Launcher:* Press the button on the launcher and wait patiently for it to start. Then, it will open the interface in your browser. It's like a website, but on your computer.  
    *Collab:* Press the play buttons, **in order, one at a time**. Wait for each one to finish before pressing the next one. **You may skip the ControlNet section this time**. When the final step is finished, it will produce a link you can use to access the interface as a website. This will be open as long as the page stays open.

    The starting page is where you can make your images. But first, we'll go to the Settings tab. There will be sections on the left.
    * In the *Stable Diffusion* section, scroll down and increase **Clip Skip** from 1 to 2. This is said to produce better images, specially for anime. You can also set your VAE from here, but I have a better idea:
    * In the *User Interface* section, scroll down to **Quicksettings list** and change it to `sd_model_checkpoint, sd_vae`.
    * Scroll back up, click the big orange **Apply settings** button, then **Reload UI** next to it. You can now change your model as well as your VAE from the top of the page at any time.

1. **Prompts** <a name="sdguide-prompt"></a>[▲](#sdguide-index)

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
    You can also save your prompts to reuse later with the buttons below Generate. Click the small 💾 *Save style* and give it a name. Later, you can open your *Styles* dropdown to choose, then click 📋 *Apply selected styles to the current prompt*.

    Note that when you surround something in `(parentheses)`, it will have emphasis or more **weight** in your resulting image, equal to `1.1`. The normal weight is 1, and each parentheses will multiply by an additional 1.1. You can also specify the weight yourself, like this: `(full body:1.4)`. You can also go below 1 to de-emphasize a word: `[brackets]` will multiply by 0.9, but you still use normal parentheses to go lower, like `(this:0.5)`.

1. **Generation parameters** <a name="sdguide-gen"></a>[▲](#sdguide-index)

    * *Sampling method:* These dictate how your image is formulated, and each produce different results. The default of `Euler a` is almost always the best. There are also very good results for `DPM++ 2M Karras` and `DPM++ SDE Karras`.
    * *Sampling steps:* These are "calculated" beforehand, and so more steps doesn't always mean more detail. I always go with 30, you may go from 20-50 and find good results.
    * *Width and Height:* 512x512 is the default, you should almost never go above 768 in either direction as it may distort and deform your image. To produce bigger images see `Hires. fix`
    * *Batch Count and Batch Size:* Batch *size* is how many images your graphics card will create at the same time, which is limited by your graphics card. Batch count is how many repeats of those to produce. Batches have sequential seeds, more on seeds below.
    * *CFG Scale:* "Lower values produce more creative results". You should almost always stick to 7, but 4 to 10 is an acceptable range. It gets strange outside that.
    * *Seed:* A number that guides the creation of your image. The same seed with the same prompt and parameters produces almost exacly the same image every time.
  
    *Hires. fix:* Lets you create larger images without distortion. Usually used at 2x scale. When selected, more options appear:
    * *Upscaler:* The algorithm to upscale with. `Latent` and its variations produce creative results, and you may also like `R-ESRGAN 4x+` and its anime version. Also see [Upscalers](#sdguide-upscale). 
    * *Hires steps:* I recommend at least half as many as your sampling steps. Higher values aren't always better.
    * *Denoising strength:* The most important parameter. Near 0, no detail will be added to the image. Near 1, the image will be changed completely. I recommend something between 0.2 and 0.6 depending on the image.
    
    Others:
    * *Restore faces:* May improve realistic faces. I never need it with the models and prompts listed in this guid as well as hires fix.
    * *Tiling:* Used to produce repeating textures to put on a grid. Not very useful.
    * *Script:* Lets you access useful features and extensions such as `X/Y/Z Plot` which lets you compare images with varying parameters on a grid.

&nbsp;
  
# Extensions <a name="sdguide-extensions"></a>[▲](#sdguide-index)

*Stable Diffusion WebUI* supports extensions to add additional functionality and quality of life. These can be added by going into the **Extensions** tab, then **Install from URL**, and pasting the links found here or elsewhere. Then, click *Install* and wait for it to finish. Then, go to **Installed** and click *Apply and restart UI*.

Here are some useful extensions, I hugely recommend the first 2:
* [Image Browser (fixed fork)](https://github.com/aka7774/sd_images_browser) - This will let you browse your past generated images very efficiently, as well as directly sending their prompts and parameters back to txt2img, img2img, etc.
* [TagComplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) - Absolutely essential for anime art. It will show you the matching booru tags as you type. Anime models work via booru tags, and rarely work at all if you go outside them, so knowing them is godmode. Not all tags will work well in all models though, specially if they're rare.
* [ControlNet](https://github.com/Mikubill/sd-webui-controlnet) - A huge extension deserving of its own guide. It lets you take AI data from any image and use it as an input for your image. Practically speaking, it can create any pose or environment you want. Very powerful if used with external tools succh as Blender.
* [Ultimate Upscale](https://github.com/Coyote-A/ultimate-upscale-for-automatic1111) - A semi-advanced script usable from the img2img section to make really large images, where normally you can only go as high as your VRAM allows.
* [Two-shot](https://github.com/opparco/stable-diffusion-webui-two-shot) - Normally you can't create more than one distinct character in the same image without them blending together. This extension lets you divide the image into parts; full, left side, right side; allowing you to make nice 2-character images.
* [Dynamic Prompts](https://github.com/adieyal/sd-dynamic-prompts) - A script to let you generate randomly chosen elements in your image, among other things.
* [Model Converter](https://github.com/Akegarasu/sd-webui-model-converter) - Lets you convert most 7GB/4GB models down to 2GB, by choosing `safetensors`, `fp16`, and `no-ema`. These pruned models work "almost the same" as the full models, which is to say, there is no appreciable difference due to math reasons. Most models come in 2 GB form nowadays regardless.

&nbsp;

# Loras <a name="sdguide-lora"></a>[▲](#sdguide-index)

LoRA or *Low-Rank Adaptation* is a form of **Extra Network** and the latest technology that lets you append a smaller model to any of your full models. They are similar to embeddings, one of which you might've seen [earlier](#sdguide-prompt), but Loras are larger and often more capable. Technical details omitted.

Loras can represent a character, an artstyle, poses, clothes, or even a human face (though I do not endorse this). Models are usually capable enough for general work, but when it comes to specific details with little existing examples, they fall short. That's where Loras come in. They can be downloaded from [civitai](https://civitai.com) and are 144 MB by default, but they can go as low as 1 MB and sometimes several hundreds of MB. Bigger Loras are not necessarily better. They come in `.safetensor` format, same as models.

Place your lora files in the `stable-diffusion-webui/models/Lora` folder. Then, look for the 🎴 *Show extra networks* button below the big orange Generate button. It will open a new section. Click on the Lora tab and press the **Refresh** button, and your loras should appear. When you click a Lora in that menu it will get added to your prompt. It will look like this: `<lora:filename:1` The start is always the same. The filename will be the exact filename in your system without the `.safetensors` extension. Finally, the number is the weight, like we saw in [Prompts](#sdguide-prompt). Most Loras work between 0.5 and 1 weight, and too high values might "fry" your image.

An example of a Lora is [Thicker Lines Anime Style](https://civitai.com/models/13910/thicker-lines-anime-style-lora-mix), which is perfect if you want your images to look more like traditional anime.

&nbsp;

# Upscalers <a name="sdguide-upscale"></a>[▲](#sdguide-index)

You can download additional upscalers and put them in your `stable-diffusion-webui/models/ESRGAN` folder.

* [Some notable ones here](https://mega.nz/folder/LYdRSK7Y#9_eYXeUDqNbGpQ-FIdYTkg), including Remacri which might be the best one out there, and the files necessary to make 
* [Upscale wiki](https://upscale.wiki/wiki/Model_Database)

Coming soon: How to use ultimate upscaler.