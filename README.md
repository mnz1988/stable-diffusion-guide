---
license: wtfpl
tags:
- guide
- stable diffusion
- webui
- automatic1111
- stable-diffusion-webui
language:
- en
---

**[CLICK HERE TO OPEN THIS DOCUMENT IN FULL WIDTH](README.md#index)**

&nbsp;

# Index <a name="index"></a>

* [Introduction](#intro)
* [Google Collab](#collab)
* [Local Installation (Windows + Nvidia)](#install)
* [Getting Started](#start)
   1. [Models](#model)
   1. [VAEs](#vae)
   1. [Prompts](#prompt)
   1. [Generation parameters](#gen)
* [Extensions](#extensions)
* [Loras](#lora)
* [Upscaling](#upscale)
* [Scripts](#scripts)
   * [X/Y/Z Plot](#plot)
   * [Prompt Matrix](#matrix)
   * [Ultimate Upscaler](#ultimate)
* [ControlNet](#controlnet)
* [Lora Training](#train)
    * [Tips for training character Loras](#trainchars)
 
&nbsp;

# Introduction <a name="intro"></a>[▲](#index)

Stable Diffusion is a very powerful AI image generation software you can run on your own home computer. It uses "models", which function like the brain of the AI, and can make almost anything, given that someone has trained it to do it. The biggest uses are anime art, photorealism, and NSFW content.

The images you create may be used for any purpose, depending on the used model's license. Whether they are "yours" in a legal sense varies by local laws and is often inconclusive. Neither I or any of the people involved in Stable Diffusion or its models are responsible for anything you make, and you are expressively forbidden from creating illegal or harmful content.

This guide is up to date with the best practices as of March 2023. One week is like a year in AI time, so this guide may be outdated by the time you read it. Hopefully it is still useful.

&nbsp;

# Google Collab <a name="collab"></a>[▲](#index)

The easiest way to use Stable Diffusion is through Google Collab. It borrows Google's computers to use AI, with variable time limitations, usually a few hours every day. You will need a Google account (or several, wink wink) and we will be using Google Drive for ease of access.

If you instead want to run it on your own computer, [scroll down ▼](#install).

1. Open [this page](https://colab.research.google.com/drive/1wEa-tS10h4LlDykd87TF5zzpXIIQoCmq).

1. Near the top, click **Copy to Drive**. Wait for the new window to open and close the old one. This is now your personalized collab which will save your settings, and you should open it from your Google Drive from now on. Check the original for updates as frequently as you like.

1. Turn on the following options under **Configurations**: `output_to_drive, configs_in_drive, no_custom_theme`. Then, turn on the following options under **Models, etc**: `anything_vae`, `wd_vae`, `sd_vae`.

1. If you're already familiar with Stable Diffusion, you may paste links to your desired resources in the `custom_urls` text box. We will add some links later in this guide. Links must be **direct downloads** to each file (ideally from civitai or huggingface), and must be separated by commas.

1. You can save the file now if you want, and whenever you change something in this page later.

1. Press the play button to the left, anywhere in the first section of the page labeled **Start 🚀**. Wait a few minutes for it to finish, while a few progress messages appear near the bottom. Then, a **public link** will be created, which you can open in a new tab to start using Stable Diffusion. **Keep the collab tab open!** (It may be difficult to keep both tabs open on mobile)

1. You can now make some decent anime images thanks to the default **Anything 4.5** model. But we can go further. Also, what are all of these options? [Scroll down ▼](#start) to get started.

&nbsp;

# Local Installation (Windows + Nvidia) <a name="install"></a>[▲](#index)

To run Stable Diffusion on your own computer you'll need at least 16 GB of RAM and 4 GB of VRAM (preferably 8). I will only cover the case where you are running Windows 10/11 and using an NVIDIA graphics card series 16XX, 20XX or 30XX (though 10XX also work). My apologies to AMD, Linux, and Mac users, but their cases are harder to cover. If you don't meet the hardware requirements, you can just proceed with the Google Collab method [above](#collab).

1. Get the latest release from [this page](https://github.com/EmpireMediaScience/A1111-Web-UI-Installer/releases). 

1. Run the installer, choose a simple location to install to, and wait for it to finish.

1. Run the program. You will see a few options. First, turn on **medvram** and **xformers**. You may skip medvram if you have 12 or more GB of VRAM.

1. Set your *Additional Launch Options* to: `--opt-channelslast --no-half-vae --theme dark` . Any extra options should be separated by spaces.
    * If your graphics card has less than 8 GB of VRAM, add `--opt-split-attention-v1` as it may lower vram usage even further.
    * If you want to run the program from your computer but want to use it in another device, such as your phone, add `--listen`. After launching, use your computer's local IP in the same WiFi network to access the interface.
    * Full list of possible parameters [here](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings)

1. Click **Launch** and wait for a browser window to open with the interface. It may take a while the first time.

1. The page is now open. It's your own private website. The starting page is where you can make your images. But first, we'll go to the **Settings** tab. There will be sections of settings on the left.
    * In the *Stable Diffusion* section, scroll down and increase **Clip Skip** from 1 to 2. This is said to produce better images, specially for anime.
    * In the *User Interface* section, scroll down to **Quicksettings list** and change it to `sd_model_checkpoint, sd_vae`
    * Scroll back up, click the big orange **Apply settings** button, then **Reload UI** next to it.

1. You are more than ready to generate some images, but you only have the basic model available. It's not great, at most it can make some paintings. Also, what are all of these options? See [below ▼](#start) to get started.

&nbsp;

# Getting Started <a name="start"></a>[▲](#index)

Before or after generating your first few images, you will want to take a look at the information below to improve your experience and results.  
The top of your page should look similar to this:

![Top](images/top.png)

Here you can select your model and VAE. We will go over what these are and how you can get more of them. The collab has additional settings here too, you should ignore them for now.


1. **Models** <a name="model"></a>[▲](#index)

   The **model**, also called **checkpoint**, is the brain of your AI, designed for the purpose of producing certain types of images. There are many options, most of which are on [civitai](https://civitai.com). But which to choose? These are my recommendations:
   * For anime, [7th Heaven Mix](https://civitai.com/models/4669/corneos-7th-heaven-mix) has a nice aesthetic similar to anime movies, while [Abyss Orange Mix 3](https://civitai.com/models/9942/abyssorangemix3-aom3) *(__Note:__ scroll down and choose the AOM3 option)* offers more realism in the form of advanced lighting and softer shading, as well as more lewdness. I remixed the two options above into [Heaven Orange Mix](https://civitai.com/models/14305/heavenorangemix).
   * While AOM3 is extremely capable for NSFW, the popular [Grapefruit](https://civitai.com/models/2583/grapefruit-hentai-model) hentai model may also fit your needs.
   * For general art go with [DreamShaper](https://civitai.com/models/4384/dreamshaper), there are few options quite like it in terms of raw creativity. An honorable mention goes to [Pastel Mix](https://civitai.com/models/5414/pastel-mix-stylized-anime-model), which has a beautiful and unique aesthetic with the addition of anime.
   * For photorealism go with [Deliberate](https://civitai.com/models/4823/deliberate). It can do almost anything, but specially photographs. Very intricate results.
   * The [Uber Realistic Porn Merge](https://civitai.com/models/2661/uber-realistic-porn-merge-urpm) is self-explanatory.
     
   *Launcher:* It will let you choose the path to your models folder. Otherwise the models normally go into `stable-diffusion-webui/models/Stable-diffusion`.

   *Collab:* Copy the **direct download link to the file** and paste it in the text box labeled `custom_urls`. Multiple links are separated by commas.
    
   Please note that checkpoints in the format `.safetensors` are safe to use while `.ckpt` **may** contain viruses, so be careful. Additionally, when choosing models you may have a choice between fp32, fp16 and pruned. They all produce the same images within a tiny margin of error, so just go with the smallest file (fp16-pruned). If you want to use them for training or merging, go with the biggest one instead.

1. **VAEs** <a name="vae"></a>[▲](#index)

   Most models don't come with a VAE built in. The VAE is a small separate model, which "converts your image from AI format into human format". Without it, you'll get faded colors and ugly eyes, among other things.

   If you're using the collab in this guide, you should already have the below VAEs, as I told you to select them before running.

   There are practically only 3 different VAEs out there worth talking about:
   * [anything vae](https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/VAEs/orangemix.vae.pt), also known as the orangemix vae. All anime models use this.
   * [vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/blob/main/vae-ft-mse-840000-ema-pruned.safetensors), the latest from Stable Diffusion itself. Used by photorealism models and such.
   * [kl-f8-anime2](https://huggingface.co/hakurei/waifu-diffusion-v1-4/resolve/main/vae/kl-f8-anime2.ckpt), also known as the Waifu Diffusion VAE, it is older and produces more saturated results. Used by Pastel Mix.

   *Launcher:* It lets you choose the default VAE, otherwise put them in the `stable-diffusion-webui/models/VAE` folder.
   
   If you did not follow this guide up to this point, you will have to go into the **Settings** tab, then the **Stable Difussion** section, to select your VAE.

   Whenever you place a new file you can either restart the UI at the bottom of the page or press the small 🔃 buttons next to a dropdown.

1. **Prompts** <a name="prompt"></a>[▲](#index)

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
      * [Get EasyNegative here](https://huggingface.co/datasets/gsdf/EasyNegative/resolve/main/EasyNegative.safetensors). For collab, paste the link into the `custom_urls` text box. For Windows, put it in your `stable-diffusion-webui/embeddings` folder. Then, go to the bottom of your WebUI page and click *Reload UI*. It will now work when you type the word.
   
   ![Prompts](images/prompt.png)

   After a "base prompt" like the above, you may then start typing what you want. For example `young woman in a bikini in the beach, full body shot`. Feel free to add other terms you don't like to your negatives such as `old, ugly, futanari, furry`, etc.  
   You can also save your prompts to reuse later with the buttons below Generate. Click the small 💾 *Save style* button and give it a name. Later, you can open your *Styles* dropdown to choose, then click 📋 *Apply selected styles to the current prompt*.

   Note that when you surround something in `(parentheses)`, it will have more emphasis or **weight** in your resulting image, equal to `1.1`. The normal weight is 1, and each parentheses will multiply by an additional 1.1. You can also specify the weight yourself, like this: `(full body:1.4)`. You can also go below 1 to de-emphasize a word: `[brackets]` will multiply by 0.9, but you must still use normal parentheses to go lower, like `(this:0.5)`.

   Also note that hands and feet are famously difficult for AI to generate. These methods improve your chances, but you may need to do img2img inpainting, photoshopping, or advanced techniques with [ControlNet ▼](#controlnet) to get it right.

1. **Generation parameters** <a name="gen"></a>[▲](#index)

   The rest of the parameters in the starting page will look something like this:
   
   ![Parameters](images/parameters.png)

   * **Sampling method:** These dictate how your image is formulated, and each produce different results. The default of `Euler a` is almost always the best. There are also very good results for `DPM++ 2M Karras` and `DPM++ SDE Karras`.
   * **Sampling steps:** These are "calculated" beforehand, and so more steps doesn't always mean more detail. I always go with 30, you may go from 20-50 and find good results.
   * **Width and Height:** 512x512 is the default, and you should almost never go above 768 in either direction as it may distort and deform your image. To produce bigger images see `Hires. fix`
   * **Batch Count and Batch Size:** Batch *size* is how many images your graphics card will generate at the same time, which is limited by its VRAM. Batch *count* is how many repetitions of those to produce. Batches have sequential seeds, more on seeds below.
   * **CFG Scale:** "Lower values produce more creative results". You should almost always stick to 7, but 4 to 10 is an acceptable range. It may get strange outside that.
   * **Seed:** A number that guides the creation of your image. The same seed with the same prompt and parameters produces almost exacly the same image every time.
  
   **Hires. fix:** Lets you create larger images without distortion. Often used at 2x scale. When selected, more options appear:
   * **Upscaler:** The algorithm to upscale with. `Latent` and its variations produce creative results, and you may also like `R-ESRGAN 4x+` and its anime version. I recommend the Remacri upscaler, see [Upscalers ▼](#upscale). 
   * **Hires steps:** I recommend at least half as many as your sampling steps. Higher values aren't always better, and they take a long time, so be conservative here.
   * **Denoising strength:** The most important parameter. Near 0.0, no detail will be added to the image. Near 1.0, the image will be changed completely. I recommend something between 0.2 and 0.6 depending on the image, to add enough detail as the image gets larger, without *destroying* any original details you like.
    
   Others:
   * **Restore faces:** May improve realistic faces. I never need it with the models and prompts listed in this guide as well as hires fix.
   * **Tiling:** Used to produce repeating textures to put on a grid. Not very useful.
   * **Script:** Lets you access useful features and extensions, such as [X/Y/Z Plot ▼](#plot) which lets you compare images with varying parameters on a grid. Very powerful.

&nbsp;
  
# Extensions <a name="extensions"></a>[▲](#index)

*Stable Diffusion WebUI* supports extensions to add additional functionality and quality of life. These can be added by going into the **Extensions** tab, then **Install from URL**, and pasting the links found here or elsewhere. Then, click *Install* and wait for it to finish. Then, go to **Installed** and click *Apply and restart UI*.  
![Extensions](images/extensions.png)

Here are some useful extensions. Most of these come installed in the collab, and I hugely recommend you manually add the first 2 if you're running locally:
* [Image Browser (fixed fork)](https://github.com/aka7774/sd_images_browser) - This will let you browse your past generated images very efficiently, as well as directly sending their prompts and parameters back to txt2img, img2img, etc.
* [TagComplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) - Absolutely essential for anime art. It will show you the matching booru tags as you type. Anime models work via booru tags, and rarely work at all if you go outside them, so knowing them is godmode. Not all tags will work well in all models though, specially if they're rare.
* [ControlNet](https://github.com/Mikubill/sd-webui-controlnet) - A huge extension deserving of [its own guide ▼](#controlnet). It lets you take AI data from any image and use it as an input for your image. Practically speaking, it can create any pose or environment you want. Very powerful if used with external tools succh as Blender.
* [Ultimate Upscale](https://github.com/Coyote-A/ultimate-upscale-for-automatic1111) - A semi-advanced script usable from the img2img section to make really large images, where normally you can only go as high as your VRAM allows. See [Ultimate Upscaler ▼](#ultimate).
* [Two-shot](https://github.com/opparco/stable-diffusion-webui-two-shot) - Normally you can't create more than one distinct character in the same image without them blending together. This extension lets you divide the image into parts; full, left side, right side; allowing you to make nice 2-character images. It is an optional launch setting in the collab.
* [Dynamic Prompts](https://github.com/adieyal/sd-dynamic-prompts) - A script to let you generate randomly chosen elements in your image, among other things.
* [Model Converter](https://github.com/Akegarasu/sd-webui-model-converter) - Lets you convert most 7GB/4GB models down to 2GB, by choosing `safetensors`, `fp16`, and `no-ema`. These pruned models work "almost the same" as the full models, which is to say, there is no appreciable difference due to math reasons. Most models come in 2 GB form nowadays regardless.

&nbsp;

# Loras <a name="lora"></a>[▲](#index)

LoRA or *Low-Rank Adaptation* is a form of **Extra Network** and the latest technology that lets you append a smaller model to any of your full models. They are similar to embeddings, one of which you might've seen [earlier ▲](#prompt), but Loras are larger and often more capable. Technical details omitted.

Loras can represent a character, an artstyle, poses, clothes, or even a human face (though I do not endorse this). Checkpoints are usually capable enough for general work, but when it comes to specific details with little existing examples, they fall short. That's where Loras come in. They can be downloaded from [civitai](https://civitai.com) or [elsewhere (NSFW)](https://gitgud.io/gayshit/makesomefuckingporn#lora-list) and are 144 MB by default, but they can go as low as 1 MB. Bigger Loras are not always better. They come in `.safetensors` format, same as most checkpoints.

Place your lora files in the `stable-diffusion-webui/models/Lora` folder, or paste the direct download link into the `custom_urls` text box in collab. Then, look for the 🎴 *Show extra networks* button below the big orange Generate button. It will open a new section. Click on the Lora tab and press the **Refresh** button, and your loras should appear. When you click a Lora in that menu it will get added to your prompt, looking like this: `<lora:filename:1>`. The start is always the same. The filename will be the exact filename in your system without the `.safetensors` extension. Finally, the number is the weight, like we saw in [Prompts ▲](#prompt). Most Loras work between 0.5 and 1 weight, and too high values might "fry" your image, specially if using multiple Loras at the same time.

![Extra Networks](images/extranetworks.png)

An example of a Lora is [Thicker Lines Anime Style](https://civitai.com/models/13910/thicker-lines-anime-style-lora-mix), which is perfect if you want your images to look more like traditional anime.

&nbsp;

# Upscaling <a name="upscale"></a>[▲](#index)

As mentioned in [Generation Parameters ▲](#parameters), normally you shouldn't go above 768 width or height when generating an image. Instead you should use `Hires. fix` with your choice of upscaler and an appropiate denoising level. Hires fix is limited by your VRAM however, so you may be interested in [Ultimate Upscaler ▼](#ultimate) to go even larger.

You can download additional upscalers and put them in your `stable-diffusion-webui/models/ESRGAN` folder. They will then be available in Hires fix, Ultimate Upscaler, and Extras.

The collab comes with several of them, including Remacri, which is one of the best for all sorts of images.

* A few notable ones can be [downloaded here](https://huggingface.co/hollowstrawberry/upscalers-backup/tree/main/ESRGAN).
* LDSR is an advanced yet slow upscaler, its model and config can be [found here](https://huggingface.co/hollowstrawberry/upscalers-backup/tree/main/LDSR) and both must be placed in `stable-diffusion-webui/models/LDSR`.
* The [Upscale Wiki](https://upscale.wiki/wiki/Model_Database) contains dozens of historical choices.

In the future I may present examples for each upscaler.

&nbsp;

# Scripts <a name="scripts"></a>[▲](#index)

Scripts can be found at the bottom of your generation parameters in txt2img or img2img.

* **X/Y/Z Plot** <a name="plot"></a>[▲](#index)

   Capable of generating a series of images, usually with the exact same seed, but varying parameters of your choice. Can compare almost anything you want, including different models, parts of your prompt, sampler, upscaler and much more. You can have 1, 2, or 3 variable parameters, hence the X, Y and Z.

   Your parameters in X/Y/Z Plot are separated by commas, but anything else can go inbetween. The most common parameter to compare is **S/R Prompt**, where the first term is a phrase in your prompt and each term afterwards will replace the original. Knowing this, you can compare, say, Lora intensity, like this:

   `<lora:my lora:0.4>, <lora:my lora:0.6>, <lora:my lora:0.8>, <lora:my lora:1>`

   Here I made a comparison between different **models** (columns) and faces of different ethnicities via **S/R Prompt** (rows):

   ![X Y Z plot of models and ethnicities](images/XYZplot.png)

* **Prompt Matrix** <a name="matrix"></a>[▲](#index)

   Similar conceptually to S/R from before, but more in-depth. It works by showing each possible combination of terms listed between the `|` symbol in your prompt, for example: `young man|tree|city` will always contain "young man", but we'll see what happens when we add or remove "tree" and "city". Unlike S/R it also lets you use commas.

   Inside the script, you will choose either your prompt or your negative prompt to make a matrix of, and whether the variable terms should be put at the start or the end.

   Here is a comparison using the negative prompts I showed you [much earlier ▲](#prompt) in this guide. We can see how EasyNegative affects the image, as well as how the rest of the prompt affects the image, then both together:

   ![Prompt matrix of anime negative prompt sections](images/promptmatrix1.png)
   ![Prompt matrix of photorealistic negative prompt sections](images/promptmatrix2.png)

&nbsp;

# ControlNet <a name="controlnet"></a>[▲](#index)

ControlNet is an extremely powerful recent technology for Stable Diffusion. It lets you analyze information about any previously existing image and use it to guide the generation of your AI images. We'll see what this means in a moment.

If you're on collab, you should enable the `all_control_models` option. On Windows, you should first install the ControlNet [extension ▲](#extensions), then go [here](https://civitai.com/models/9251/controlnet-pre-trained-models) to download some models which you'll need to place in `stable-diffusion-webui/extensions/sd-webui-controlnet/models`. I recommend at least Canny, Depth, Openpose and Scribble, which I will show here.

I will demonstrate how ControlNet may be used. For this I chose a popular image online as our "sample image". It's not necessary for you to follow along, but you can download the images and put them in the **PNG Info** tab to view their generation data.

First, you must scroll down in the txt2img page and click on ControlNet to open the menu. Then, click *Enable*, and pick a matching *preprocessor* and *model*. To start with, I chose Canny for both. Finally I upload my sample image. Make sure not to click over the uploaded image or it will start drawing. We can ignore the other settings.

![Control Net](images/controlnet.png)

* **Canny**

   The Canny method extracts the hard edges of the sample image. It is useful for many different types of images, specially where you want to preserve small details and the general look of an image. Observe:

   <details>
   <summary>Canny example, click to open</summary>
   
   ![Canny preprocessed image](images/canny1.png)
   ![Canny output image](images/canny2.png)
   </details>

* **Depth**

   The Depth method extracts the 3D elements of the sample image. It is best suited for complex environments and general composition. Observe:

   <details>
   <summary>Depth example, click to open</summary>
   
   ![Depth preprocessed image](images/depth1.png)
   ![Depth output image](images/depth2.png)
   </details>

* **Openpose**

   The Openpose method extracts the human poses of the sample image. It helps tremendously to get the desired shot and composition of your generated characters. Observe:

   <details>
   <summary>Openpose example, click to open</summary>
   
   ![Open Pose preprocessed image](images/openpose1.png)
   ![Open Pose output image](images/openpose2.png)
   </details>

* **Scribble**

   Lets you make a simple sketch and convert it into a finished piece with the help of your prompt. For this one I asked a friend:

   <details>
   <summary>Scribble example, click to open</summary>
   
   ![Scribble sample image](images/scribble1.png)
   ![Scribble output image](images/scribble2.png)
   </details>

You will notice that there are 2 results for each method. The first is an intermediate step called the *preprocessed image*, which is then used to produce the final image. You can supply the preprocessed image yourself, in which case you should set the preprocessor to *None*. This is extremely powerful with external tools such as Blender.

In the Settings tab there is a ControlNet section where you can enable *multiple controlnets at once*. One particularly good use is when one of them is Openpose, to get a specific character pose in a specific environment, or with specific hand gestures or details. Observe:

![Open Pose + Canny](images/openpose_canny.png)

You can also use ControlNet in img2img, in which the input image and sample image both will have a certain effect on the result. I do not have much experience with this method.

There are also alternative **diff** versions of each ControlNet model, which produce slightly different results. You can [try them](https://civitai.com/models/9868/controlnet-pre-trained-difference-models) if you want, but I personally haven't.

&nbsp;

# Lora Training <a name="train"></a>[▲](#index)

   * **Character Loras** <a name="trainchars"></a>[▲](#index)

   Coming soon.