# Index <a name="index"></a>

* [معرفی](#intro)
* [نصب روی کامپیوتر شخصی (Windows + Nvidia)](#install)
* [شروع توضیحات](#start)
   1. [مدل ها](#model)
   1. [توضیحات VAE](#vae)
   1. [درخواست ها](#prompt)
   1. [معیارهای تولید تصویر](#gen)
* [افزودنی ها](#extensions)
* [توضیحات Lora](#lora)
   * [توضیحات Lycoris](#lycoris)
* [بزرگ کردن اندازه](#upscale)
* [اسکریپت ها](#imgscripts)
   * [پلات اکس/وای/زی - X/Y/Z Plot](#plot)
   * [ماتریکس درخواست - Prompt Matrix](#matrix)
   * [توضیحات Ultimate Upscaler](#ultimate)
* [کنترل نت](#controlnet)
* [آموزش دادن Lora برای تازه کارها](#train)
* [توضیحات ...vtuberها](#vtubers)
 
&nbsp;

# معرفی <a name="intro"></a>[▲](#index)
استیبل دیفیوژن (که به اختصار به آن SD میگوییم) یک نرم افزار قدرتمند تولید تصویر هوش مصنوعی است که میتوانید آن را بصورت آنلاین و یا بر روی کامپیوتر شخصی نصب و استفاده کنید (فعلا کاملا رایگان است و متن باز). SD از مدل ها "models" که شبیه به مغز هوش مصنوعی عمل میکنند و افرادی آن را آموزش داده اند تا فعالیت های مشخصی انجام دهد استفاده میکند و تقریبا میتواند هر چیزی بسازد. بیشترین استفاده های کاربران فعلا برای انیمه، تصاویر مشابه حقیقی و محتوای NSFW (نا مناسب برای کار/محتوای بزرگسالان/محتوای زننده یا تحریک کننده) است.  

از نگاه قانونی شما مسئول هر نوع تولیدی با آن هستید و افراد سازنده آن مسئولیتی ندارند. 

آخرین تغییرات این راهنما بر اساس نرم افزار آپدیت شده در مارچ 2023 می باشد و با توجه به اینکه یک هفته زمان مثل یک سال در صنعت هوش مصنوعی می ماند، ممکن است در زمان مطالعه این راهنما، تغییراتی در نرم افزار ایجاد شده باشد. 

&nbsp;

# نصب و استفاده آنلاین با استفاده از Google Colab

راهی راحت و برای استفاده از SD بصورت آنلاین و بدون داشتن سخت افزار شخصی استفاده از این سرویس است که از کامپیوترهای گوگل به جای سخت افزار خودتان استفاده میکنید. برای ذخیره تنظیمات و همچنین تصاویر تولید شده از گوگل درایو استفاده میکنیم. 


ابتدا به لینک  [این صفحه](https://colab.research.google.com/drive/1wEa-tS10h4LlDykd87TF5zzpXIIQoCmq) مراجعه کنید

سپس نزدیک به بالای صفحه روی **Copy to Drive** کلیک کنید.منتظر شوید تا صفحه جدید باز شود و صفحه قدیمی را ببندید. حالا داخل صفحه کولب شخصی خود هستید که تنظیمات سفارشی شما را نگه میدارد که از این به بعد باید آن را از داخل گوگل درایوتان باز کنید. اگر برای محتوای اصلی (صفحه قدیمی) آپدیتی ارائه شود شما نیز باید آن را جایگزین کنید تا بتواید از مزایای آن استفاده کنید.  

حال در بخش **Configurations** این تنظیمات را فعال کنید: `output_to_drive, configs_in_drive, no_custom_theme` و در بخش **Models, VAEs, etc** اینها را فعال کنید:`anything_vae`, `wd_vae`, `sd_vae` 

اگر از قبل با SD آشنایی کمی داشته باشید میتوانید با استفاده از باکس متنی `custom_urls` از لینک های منابع مورد نظرتان نیز استفاده کنید که تعدادی از آنها را معرفی کرده ایم. لینکها باید بصورت مستقیم(**direct downloads**) باشند تا هر فایل (ترجیحا از civitai یا huggingface باشند) نصب شود و لینکها می بایست با کاما از هم جدا شوند. 

حال دکمه پلی را در سکشن اول از صفحه که با برچسب **Start 🚀** مشخص شده است را بزنید. چند دقیقه منتظر بمانید تا عملیات ها انجام شوند و لینک عمومی **public link** ایجاد شود که با آن یک تب جدید را میتوانید باز کنید و استفاده از استیبل دیفیوژن را آغاز کنید. **تب مربوط به کولب را باز نگهدارید** (برای موبایل هم به همین صورت تب باز باشد) 

&nbsp;

# نصب روی کامپیوتر شخصی (Windows + Nvidia) <a name="install"></a>[▲](#index)

برای اجرای استیبل دیفیوژن روی کامپیوتر خود حداقل به 16 گیگابایت رم و گرافیکی با حداقل 4 گیگابایت وی رم (8 گیگ توصیه می شود) نیاز دارید. این راهنما بصورت عمومی ویندوز 10 و 11 را با استفاده از کارت گرافیک NVIDIA سری های 16XX, 20XX یا 30XX پشتیبانی می کند. پوزش از کاربران لینوکس، مک و همچنین صاحبین کارت های گرافیک AMD چون این راهنما آنها را در بر نمیگیرد و راه اندازی استیبل دیفیوژن برای آنها پر دردسرتر و پر از ایرادات فنی است. توصیه میشود از همان آموزش کولب که در مرحله قبل ارائه شد استفاده کنید.   

ابتدا آخرین نسخه ریلیز را [از این صفحه](https://github.com/EmpireMediaScience/A1111-Web-UI-Installer/releases) دانلود کنید. 

سپس فایل اینستالر را اجرا کنید و فولدری که میخواهید آنجا نصب شود را مشخص کنید و تا پایان نصب صبر کنید.

حال برنامه را اجرا کنید. گزینه های **medvram** و **xformers** را فعال کنید. اگر وی رم گرافیک شما 12 گیگ یا بیشتر است نیاز به فعال کردن medvram نیست. 
 
تنظیمات اضافی (**Additional Launch Options**) را به این روش میتوانید انجام دهید: `--opt-channelslast --no-half-vae --theme dark` . هر نوع تنظیم دیگری را که مایل باشید میتوانید اضافه کنید و با اسپیس (فضای خالی) آنها را از هم جدا کنید.
   توجه* اگر وی رم کارت گرافیک شما 4تا6 گیگابایت است مقدار `--opt-split-attention-v1` را نیز اضافه کنید چون ممکن است بتوانید از وی رم کمتری استفاده کنید.
   توجه* اگر میخواهید برنامه را روی کامپیوتر خود اجرا کنید ولی از دستگاه دیگری برای کار کردن با برنامه استفاده کنید (مثلا با موبایل)، مقدار `--listen --enable-insecure-extension-access` را نیز اضافه کنید. پس از اجرا، IP لوکال خود را میتوانید از یک وای فای که هردو دستگاه به آن متصل هستند را در مرورگر موبایل باز کنید تا رابط کاربری را مشاهده کنید. همچنین میتوانید روی آن رمز هم بگذارید، فقط کافیست مقداری مثللا مشابه این را نیز اضافه کنید `--gradio-auth name:1234` 
    در صورت تمایل* لیست کامل پارامترهای قابل استفاده را میتوانید [اینجا](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings) بینید. 

اکنون بر روی **Launch** کلیک کنید و منتظر بمانید تا صفحه رابط کاربری آن در مرورگر شما باز شود. برای اولین بار مقداری طول میکشد تا دانلودها انجام شود یا هروقت نیاز به فایلی باشد که بر روی سیستم موجود نیست برنامه اتوماتیک آن را دانلود میکند. 

صفحه حالا باز شده. این یک وبسایت خصوصی متعلق به شماست. صفحه ابتدایی، همان جاییست که میتوانید از طریق وارد کردن متن یک یا چند تصویر ایجاد کنید. اما قبل از شروع به تب تنظیمات(**Settings**) بروید. سکشن تنظیمات در بخش چپ صفحه است.
     در سکشن *Stable Diffusion* به پایین اسکرول کنید و مقدار **Clip Skip** را از 1 به 2 تغییر دهید. این کار برای ایجاد تصاویر بهتر (به خصوص برای انیمه) کمک میکند. 
     در سکشن *User Interface* به پایین اسکرول کنید و **Quicksettings list** را به `sd_model_checkpoint, sd_vae` تغییر دهید
     با اسرول به بالا برگردید و بر روی دکمه نارنجی رنگ بزرگ که برروی آن نوشته **Apply settings** بزنید و بعد **Reload UI** کنار آن را بزنید.
    
حالا میتوانید با داشتن مدل پایه ای که نصب شده است تصاویر را تولید کنید که البته ممکن است زیاد مورد پسند نباشد. من از مدل پایه Runway استفاده میکنم که اگر تمایل داشته باشید میتوانید آن را دانلود و در پوشه مدل ها قرار دهید. حجم این فایل بزرگ است و حدود 8 گیگابایت میباشد: https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/v1-5-pruned.ckpt  و برای فاین تیون نیز مناسب است و همچنین بصورت پیشفرض فیلترهای سنسور و حذف خروجی های بزرگسالان در آن وجود ندارد

 &nbsp;

# شروع توضیحات <a name="start"></a>[▲](#index)

اگر طبق توضیحات قبلی پیش رفته باشید رابط کاربری شما چیزی شبیه به این تصویر است که با هم به تشریح و یادگیری اولیه آن میپردازیم:

![Top](images/top.png)


اینجا میتوانید چک پوینت ها (مدل ها) و VAE را انتخاب کنید. در حالت استفاده از کولب گزینه های اضافه دیگری هم هست که فعلا از آنها چشم پوشی میکنیم تا توضیحات اصلی را بیان کنیم 

**مدل ها (چک پوینت)** <a name="model"></a>[▲](#index)

   همانطور که گفته شد مدل ها را چک پینت نیز می نامند که مغز هوش مصنوعی شما هستند و برای اهداف تولید انواع مختلفی از تصاویر طراحی شده اند. گزینه های بسیار زیاد و متنوعی از آنها وجود دارد (به خصوص در پلتفرم [civitai](https://civitai.com) ) اما کدام را انتخاب کنیم؟ تعدادی پیشنهاد به شما ارائه میدهم: 
   
   مدل [7th Heaven Mix](https://civitai.com/models/4669/corneos-7th-heaven-mix) برای انیمه قابلیت های مشابه تصاویر سینمایی خوبی دارد و مدل [Abyss Orange Mix 3](https://civitai.com/models/9942/abyssorangemix3-aom3) تصاویری واقع گرایانه تر با شیدینگ نرم تر و نورپردازی حرفه ای تر ارائه می دهد. نویسنده این راهنما (نسخه انگلیسی) این دو مدل را با هم مرج کرده و در اختیار شما گذاشته است [Heaven Orange Mix](https://civitai.com/models/14305/heavenorangemix) که ترکیبی از هردو است. 
   
   مدل های معرفی شده برای تصاویر NSFW قدرتمند هستند و رقیب محبوبی نیز به اسم [Grapefruit](https://civitai.com/models/2583/grapefruit-hentai-model) دارند که برای hentai استفاده می شود.
   
   برای آثار هنری بصورت عمومی مدل [DreamShaper](https://civitai.com/models/4384/dreamshaper) گزینه های مناسبی برای خلاقیت ارائه می دهد. همچنین استفاده از [Pastel Mix](https://civitai.com/models/5414/pastel-mix-stylized-anime-model) میتواند آثار هنری زیبا و منحصر به فردی را برایتان فراهم کند. 
   
   برای فوتوریلیسم استفاده از [Deliberate](https://civitai.com/models/4823/deliberate) نتایج بسیار جالبی ارائه میدهد. 
   
   کاربرد مدل [Uber Realistic Porn Merge](https://civitai.com/models/2661/uber-realistic-porn-merge-urpm) نیز که از نام آن مشخص است و نیازی به توضیح ندارد. 
   

   اگر از colab در این راهنما استفاده میکنید **لینک مستقیم فایل مدل** را کپی کنید و در باکس متنی ای که با لیبل `custom_urls` مشخص شده است قرار دهید تا بتوانید نصبشان کنید. همچنین لینک های متعدد را با کاما از هم جدا کنید تا بتوانید همزمان این کار را انجام دهید. &nbsp;
   اگر برنامه را روی کامپیوتر شخصی استفاده می کنید مدل ها را معمولا در پوشه `stable-diffusion-webui/models/Stable-diffusion` قرار میدهند


   چک پوینت ها یا مدل هایی که فایل آنها با پسوند `.safetensors` ارائه شده اند برای استفاده امن هستند. فایل هایی که با پسوند `.ckpt` ارائه میشوند **می توانند/ممکن است** حاوی ویروس باشند پس ابتدا از منبع ارائه دهنده فایل مطمئن شوید. همچنین در زمان انتخاب فایل ها ممکن است گزینه های متعددی مثل fp32، fp16 و pruned را مشاهده کنید، تمام آنها برای تولید تصاویر نتایج تقریبا مشابهی با خطای خیلی کمی ارائه میدهند پس استفاده از فایل های با حجم کمتر (pruned-fp16) نتایج مناسبی دارد و نیاز به استفاده از فایل های حجیم تر نیست. اما اگر میخواهید از فایل ها برای آموزش چک پوینت اختصاصی خود و یا مرج کردن چند مدل با هم استفاده کنید از فایل های حجیم تر استفاده کنید.  

 **توضیحات VAEها** <a name="vae"></a>[▲](#index)

   بیشتر چک پوینت ها با VAE درونی ارائه نمی شوند. VAE یک مدل مجزای کوچک است که "تصاویر را به فرمت انسانی تبدیل میکند". بدون آن شما رنگ های فید شده، چشم های زشت و دیگر چیزهای نامناسب را در خروجی خواهید دید.
   
   ما سه مدل مختلف VAE در حال استفاده داریم:

   مدل [anything vae](https://huggingface.co/WarriorMama777/OrangeMixs/resolve/main/VAEs/orangemix.vae.pt) که با نام اورنج میکس هم شناخته می شود و بیشتر مدل های انیمه از آن استفاده می کنند.

   مدل [vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse-original/blob/main/vae-ft-mse-840000-ema-pruned.safetensors) که توسط خود استیبل دیفیوژن ارائه شده است و توسط بیشتر مدل های فوتوریلیسم و مشابه آن استفاده می شود

   مدل [kl-f8-anime2](https://huggingface.co/hakurei/waifu-diffusion-v1-4/resolve/main/vae/kl-f8-anime2.ckpt) که به وایفو دیفیوژن هم شناخته می شود که قدیمی تر است و بیشتر نتایج اشباع شده ارائه می دهد که توسط Pastel Mix و امثال آن استفاده می شود.
   
   
   فایل های مربوط به VAE ها معمولا در پوشه `stable-diffusion-webui/models/VAE` قرار میگیرند 
   


   **درخواست ها / Prompts** <a name="prompt"></a>[▲](#index)

   در اولین تب **txt2img** شما بیشتر تصاویرتان را می سازید. اینجا جاییست که درخواست *prompt* خود و چیزهایی که نمیخواهید در آن باشد (*negative prompt*/درخواست منفی) را وارد میکنید. استیبل فیوژن مثل میدجرنی () یا دیگر نرم افزارهای مشابه نیست که فقط از آنها درخواستی کلی برای تولید چیزی کنید، باید به طور واضح آن را مشخص کنید، *خیلی* واضح. اغلب مردم یک پرامپت (درخواست) پیدا میکنند که کارشان را راه می اندازد و از آن استفاده میکنند یا از دیگران برای پیشنهادات کمک میک می گیرند. اینجا چند نمونه پرامپت و پرامپت منفی شخصی را نشان میدهم:
   
   * برای انیمه:
      * `2d, masterpiece, best quality, anime, highly detailed face, highly detailed background, perfect lighting`
      * `EasyNegative, worst quality, low quality, 3d, realistic, photorealistic, (loli, child, teen, baby face), zombie, animal, multiple views, text, watermark, signature, artist name, artist logo, censored`
     
   * برای فتورلیسم: 
      * `best quality, 4k, 8k, ultra highres, raw photo in hdr, sharp focus, intricate texture, skin imperfections, photograph of`
      * `EasyNegative, worst quality, low quality, normal quality, child, painting, drawing, sketch, cartoon, anime, render, 3d, blurry, deformed, disfigured, morbid, mutated, bad anatomy, bad art`

   * **توضیح EasyNegative:** <a name="promptneg"></a>
   استفاده از این پرامپت منفی که بصورت *embedding* یا کلمه جادویی "magic word" عمل میکند در واقع شامل تعداد زیادی پرامپت منفی است که به تولید تصاویر بهتر کمک میکند که اگر از آن استفاده نکنیم نیاز به نوشتن تعداد زیادی پرامپ منفی داریم که در پرامپت محدودیت کاراکتر داریم

      برای دانلود این فایل کوچک و نصب آن از [این لینک](https://huggingface.co/datasets/gsdf/EasyNegative/resolve/main/EasyNegative.safetensors) استفاده کنید و آن را در پوشه `stable-diffusion-webui/embeddings` قرار دهید و اگر برنامه در حال اجراست آن را ریلود *Reload UI* کنید. و هروقت آن کلمه را بنویسید (EasyNegative) عمل میکند 


   ![Prompts](images/prompt.png)

   بعد از نوشتن پرامپت ابتدایی یا پایه ای (شبیه پرامپت های بالا که مثال زده شد) خواسته های خود را اضافه میکنیم. مثلا `young woman in a bikini in the beach, full body shot` را اضافه میکنیم. همچنین برا پرامپت منفی نیز چیزهایی که مایل نیستیم در تصویر باشد را اضافه میکنیم...
   
   برای ذخیره کردن پرامپت های خود که بعدا از آنها بخواهید استفاده کنید بر روی دکمه 💾 *Save style* بزنید و برای آن اسمی قرار دهید تا بدانید به چه موضوعی اشاره دارد. بعدا از بخش *Styles* کشوی پایین رونده را باز کنید و آن را انتخاب کنید و علامت 📋 *Apply selected styles to the current prompt* را کلیک کنید تا از آن استفاده کنید. 

   یک تکنیک مهم برای نوشتن پرامپت تاکید (مثبت) و نفی کردن (تاکید منفی) بر کلمات است. وقتی چیزی را داخل پرانتز () میگذاریم برنامه **وزن** بیشتری در نتیجه تولید تصویر برای آن قائل می شود و به هوش مصنوعی میگوید که این قسمت مهمتر است. وزن معمول برای همه چیز برابر با 1 است و هر پرانتز آن را در 1.1 ضرب میکند تا وزن بیشتری بگیرد.(همچنین میتوانید از چندین پرانتر ((())) برای بالا بردن وزن استفاده کنید) 

   همچنین میتوانید وزن کلمات را بصورت مشخص نیز در پرامپت خود وارد کنید، مثل این نمونه: `(full body:1.4)`. و برای کاهش وزن آن میتوانید از براکت ها [] استفاده کنید تا وزن آن را در 0.9 ضرب کند ولی برای کاهش بیشتر هنوز اشاره مستقیم داخل پرانتز نیاز دارید مثل این:  `(this:0.5)`

   موضوع دیگر که باید به خاطر داشته باشید این است که فعلا برای هوش مصنوعی طراحی دست ها و پا مشکل است و این روش ها فقط شانس شما را افزایش میدهند و ممکن است برای کیفیت، دقت، ایده گرفتن و بالا بردن سطح کار به [ControlNet ▼](#controlnet) نیاز داشته باشید تا پیشرفته تر عمل کنید

   
   **معیارهای تولید تصویر/Generation parameters** <a name="gen"></a>[▲](#index)

   دیگر پارامترهای تولید تصویر شبیه به این هستند:
   
   ![Parameters](images/parameters.png)

   * بخش **Sampling method**: این الگوریتم تصویر شما را فرموله میکند و هر کدام نتیجه متفاوتی ایجاد میکنند. پیش فرض `Euler a` معمولا بهترین نتیجه را دارد. همچنین نتایج خوبی را از `DPM++ 2M Karras` و `DPM++ SDE Karras` میتوانید بگیرید
   
   * بخش **Sampling steps**: اینها تعداد "محاسبات" از پیش تعیین شده را مشخص میکنند. نکته اول این است که همیشه تعداد بالاتر استپ ها به معنی جزئیات و نتیجه بهتر نیست. من معمولا از عدد 30 استفاده میکنم و شما ممکن است دوست داشتهباشید از 20 تا 50 را امتحان کنید تا مقدار مناسب خود را پیدا کنید که نتیجه دلخواه را برایتان داشته باشد.
     
   * بخش **Width** و **Height**: ابعاد پیشفرض 512در512 برای طول و عرض تصویر هستند و تقریبا میشود گفت که نباید بالاتر از 768 برای هر کدام از پارامترها بروید چون معمولا باعث خراب شدن تصویر میشود و همچنین سرعت پردازش را کاهش میدهد. برای بدست آوردن تصاویر با سایز بزرگتر به بخش `Hires fix` مراجعه کنید.
     
   * بخش **Batch Count** و **Batch Size**: بچ سایز یعنی کارت گرافیک چه تعداد تصویر را در یک زمان توید کند که محدود به میزان VRAM آن است. بچ کانت هم یعنی چندبار این فعالیت تکرار شود. بچ ها وابسته به سید هستند. توضیحات سید را در بخش `seeds`ببینید.
     
   * بخش **CFG Scale**: مقدار کمتر این پارامتر خلاقیت بیشتری در نتایج ایجاد میکند. شما تقریبا همیشه از 7 استفاده میکنید اما رنج قابل قبول از 4 تا 10 می باشد.
     
   * بخش **Seed**: یک عدد راهنما برای تولید تصاویر است. یک سید با پرامپت مشابه و پارامترهای مشابه معمولا هربار تصویر یکسانی تولید میکند، بجز در مورد بعضی جزئیات کوچک در بعضی شرایط.

   * بخش **Hires fix**: این گزینه به شما امکان تولید تصاویر بزرگتر بدون آسیب رسیدن به مراحل تولید تصویر ابتدایی را میدهد. معمولا برای بزرگ کردن دوبرابری استفاده میشود. وقتی آن را فعال کنید آپشن های بیشتری نمایان می شوند:
      * بخش **Upscaler**: الگوریتمی که بر اساس آن بزرگتر کردن ابعاد را انجام میدهد. الگوریتم `Latent` و متغیرهای آن تصاویر خلاقانه و با جزئیات ایجاد میکنند اما شاید `R-ESRGAN 4x+` را هم دوست داشته باشید، به خصوص ورژن انیمه آن را.
      * بخش **Hires steps**: توصیه میکنم که عددش را حداقل نصف مقدار sampling steps قرار دهید. مقادیر بزرگتر همیشه به معنی نتایج بهتر نیست و همچنین زمان بیشتری را برای تولید نیاز دارد، پس اینجا محافظه کارانه تصمیم بگیرید.
      * بخش **Denoising strength**: یکی از مهم ترین پارامترها است. نزدیک به 0.0 یعنی جزئیاتی به تصویر اضافه نمیشود و نزدیک به 1.0 تصویر بصورت کامل تغییر می کند. توصیه من عددی بین 0.2 و 0.6 است که البته به تصویر شما بستگی دارد که چه مقدار جزئیات به آن اضافه کند بدون اینکه جزئیات تصویر اصلی که دوست دارید از بین برود.
   
   بخش های دیگر:
   * بخش **Restore faces**: ممکن است بتواند تصاویر صورت واقع گرایانه را بهبود دهد. من هیچوقت به آن نیاز نداشته ام چون از مدل ها و پرامپت هایی که در راهنما لیست شده اند استفاده میکنم و همچنین `Hires fix` نیز کار مشابه را انجام میدهد.
   * بخش **Tiling**: برای تولید تکتچرهای تکرار شونده و قرار دادن در grid استفاده می شود.
   * بخش **Script**: به شما اجازه میدهد تا به ویژگی ها و اکستنشن های خوبی همچون [X/Y/Z Plot ▼](#plot) که برای مقایسه تصاویر با پارامترهای متغیر در گرید استفاده می شود، دسترسی داشته باشید. (مهم و قدرتمند) 
   
   
   مقایسه Sampler ها: سمپلر `Euler` یکی از سمپلرهای پایه ای است و سمپلر `DDIM` ورژن سریعتر آن است و سمپلر `DPM++ 2M Karras` ورژن بهبودیافته است. همچنین سمپلر `Euler a` یا `Euler ancestral` را داریم که بیشترین نتایج خلاقانه را تولید میکند و سمپلر `DPM++ 2S a Karras` مشابه آن است. در نهایت سمپلر `DPM++ SDE Karras` را داریم که کندترین و منحصربه فرد ترین است. تعداد زیادی سمپلر دیگر وجود دارد که به آنها نپرداخته ایم ولی کلیات آنها به همین صورت مرتبط هستند. 

&nbsp;
  
# بخش Extensions <a name="extensions"></a>[▲](#index) 

*استیبل دیفیوژن با رابط کاربری وب* یا *Stable Diffusion WebUI* از اضافات *extensions* که کاربردها و کیفیت های بسیار زیادی دارند پشتیبانی می کند. با مراجعه به تب **Extensions** میتوانید آنها را به برنامه اضافه کنید و با قرار دادن لینک آنها در قسمت **Install from URL** و کلیک بر روی دکمه *Install* آنها را به راحتی نصب کنید و پس از پایان نصب به قسمت **Installed** مراجعه کنید و با زدن روی دکمه *Apply and restart UI* از آنها استفاده کنید. 
تعداد محدودی اکستنشن هم هستند که برای فعال سازی نیاز به ری استارت کامل برنامه دارند و معمولا در توضیحات آنها ذکر می شود.
 
![Extensions](images/extensions.png)

معرفی تعدادی از اکستنشن های کاربردی: اگر از کولب این راهنما استفاده میکنید تعداد زیادی از آنها را در حال حاض دارید در غیر اینصورت میتوانید آنها را خودتان اضافه کنید.
   * اکستنشن [Image Browser](https://github.com/AlUlkesh/stable-diffusion-webui-images-browser) - به شما قابلیت مرورتصاویر تولید شده قبلی را بصورت بسیار مفیدی ارائه می دهد و میتوانید مستقیما پرامپت ها و پرارامترهای استفاده شده درتصاویر را به txt2img یا img2img و دیگر بخش های مورد نیاز ارسال کنید.
   * اکستنشن [TagComplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) - اساسی و ضروری برای انیمه آرت که شما تگ های booruی منطبق را در حین تایپ نشان می دهد. انیمه مدل ها با تگ های booru کار میکنند و پرامپت ها معمولا بدون آنها درست کار نمیکنند پس دانستن آنها در حد گادمود است (اطلاعات خداگونه) به خصوص اگر تگ های نایابی باشند.
   * اکستنشن [Locon](https://github.com/KohakuBlueleaf/a1111-sd-webui-locon) به شما اجازه می دهد تا از LoCon ها و LoHa ها استفاده کنید. اطلاعات بیشتر [در ادامه راهنما ▼](#lycoris) موجود است.
   * اکستنشن [ControlNet](https://github.com/Mikubill/sd-webui-controlnet) - اکستنشنی عظیم که نیاز به [راهنمای اختصاصی ▼](#controlnet) خود را دارد. این اکستنشن به شما اجازه می دهد تا آنالیز کنید و از آن برای رفرنس تصویری که میخواهید بسازید استفاده کنید. در عمل میتوانید برای هر نوع ژست/*pose* یا محیطی از آن استفاده کنید.
   * اکستنشن [Ultimate Upscale](https://github.com/Coyote-A/ultimate-upscale-for-automatic1111) - اسکریپتی کاربردی در بخش img2img برای ساخت تصاویر بسیار بزرگ است که وابسته به میزان VRAM کارت گرافیک میتوانید اندازه را بالا ببرید. توضیحات آن را [در ادامه راهنما ▼](#ultimate) میتوانید ببینید


* 
* [Two-shot](https://github.com/opparco/stable-diffusion-webui-two-shot) - Normally you can't create more than one distinct character in the same image without them blending together. This extension lets you divide the image into parts; full, left side, right side; allowing you to make nice 2-character images.
* [Dynamic Prompts](https://github.com/adieyal/sd-dynamic-prompts) - A script to let you generate randomly chosen elements in your image, among other things.
* [Model Converter](https://github.com/Akegarasu/sd-webui-model-converter) - Lets you convert most 7GB/4GB models down to 2GB, by choosing `safetensors`, `fp16`, and `no-ema`. These pruned models work "almost the same" as the full models, which is to say, there is no appreciable difference due to math reasons. Most models come in 2 GB form nowadays regardless.

&nbsp;

# Loras <a name="lora"></a>[▲](#index)

LoRA or *Low-Rank Adaptation* is a form of **Extra Network** and the latest technology that lets you append a sort of smaller model to any of your full models. They are similar to embeddings, one of which you might've seen [earlier ▲](#promptneg), but Loras are larger and often more capable. Technical details omitted.

Loras can represent a character, an artstyle, poses, clothes, or even a human face (though I do not endorse this). Checkpoints are usually capable enough for general work, but when it comes to specific details with little existing examples, you'll need a Lora. They can be downloaded from [civitai](https://civitai.com) or [elsewhere (NSFW)](https://gitgud.io/gayshit/makesomefuckingporn#lora-list) and are 144 MB by default, but they can go as low as 1 MB. Bigger Loras are not always better. They come in `.safetensors` format, same as most checkpoints.

Place your Lora files in the `stable-diffusion-webui/models/Lora` folder, or if you're using the colab in this guide paste the direct download link into the `custom_urls` text box. Then, look for the 🎴 *Show extra networks* button below the big orange Generate button. It will open a new section either directly below or at the very bottom. Click on the Lora tab and press the **Refresh** button to scan for new Loras. When you click a Lora in that menu it will get added to your prompt, looking like this: `<lora:filename:1>`. The start is always the same. The filename will be the exact filename in your system without the `.safetensors` extension. Finally, the number is the weight, like we saw [earlier ▲](#promptweight). Most Loras work between 0.5 and 1 weight, and too high values might "fry" your image, specially if using multiple Loras at the same time.

![Extra Networks](images/extranetworks.png)

An example of a Lora is [Thicker Lines Anime Style](https://civitai.com/models/13910/thicker-lines-anime-style-lora-mix), which is perfect if you want your images to look more like traditional anime.

* Lycoris <a name="lycoris"></a>[▲](#index)

   LyCORIS is a new development that lets LoRAs learn more layers. [Learn about it here](https://github.com/KohakuBlueleaf/Lycoris). You'll need [this extension](https://github.com/KohakuBlueleaf/a1111-sd-webui-locon) to use them.

   As of now there are 2 new LoRA types:
   * **LoCon** - Said to be good with styles
   * **LoHa** - Said to be good with styles that also contain characters
 
   You can make your own in the [trainer further down ▼](#traincolab).

&nbsp;

# Upscaling <a name="upscale"></a>[▲](#index)

As mentioned in [Generation Parameters ▲](#gen), normally you shouldn't go above 768 width or height when generating an image. Instead you should use `Hires fix` with your choice of upscaler and an appropiate denoising level. Hires fix is limited by your VRAM however, so you may be interested in [Ultimate Upscaler ▼](#ultimate) to go even larger.

You can download additional upscalers and put them in your `stable-diffusion-webui/models/ESRGAN` folder. They will then be available in Hires fix, Ultimate Upscaler, and Extras.

The colab in this guide comes with several of them, including **Remacri**, which is a great all-around upscaler for all sorts of images.

* A few notable ones can be [found here](https://huggingface.co/hollowstrawberry/upscalers-backup/tree/main/ESRGAN).
* LDSR is an advanced yet slow upscaler, its model and config can be [found here](https://huggingface.co/hollowstrawberry/upscalers-backup/tree/main/LDSR) and both must be placed in `stable-diffusion-webui/models/LDSR`.
* The [Upscale Wiki](https://upscale.wiki/wiki/Model_Database) contains dozens of historical choices.

Here are some comparisons. All of them were done at 0.4 denoising strength. Note that some of the differences may be completely up to random chance.

<details>
<summary>(Click) Comparison 1: Anime, stylized, fantasy</summary>

![Original](images/upscalers1pre.png)
![Comparison](images/upscalers1.png)
</details>

<details>
<summary>(Click) Comparison 2: Anime, detailed, soft lighting</summary>

![Original](images/upscalers2pre.png)
![Comparison](images/upscalers2.png)
</details>

<details>
<summary>(Click) Comparison 3: Photography, human, nature</summary>
   
![Original](images/upscalers3pre.png)
![Comparison](images/upscalers3.png)
</details>

&nbsp;

# Scripts <a name="imgscripts"></a>[▲](#index)

Scripts can be found at the bottom of your generation parameters in txt2img or img2img.

* **X/Y/Z Plot** <a name="plot"></a>[▲](#index)

   Capable of generating a series of images, usually with the exact same seed, but varying parameters of your choice. Can compare almost anything you want, including different models, parts of your prompt, sampler, upscaler and much more. You can have 1, 2, or 3 variable parameters, hence the X, Y and Z.

   Your parameters in X/Y/Z Plot are separated by commas, but anything else can go inbetween. The most common parameter to compare is **S/R Prompt**, where the first term is a phrase in your prompt and each term afterwards will replace the original. Knowing this, you can compare, say, Lora intensity, like this:

   `<lora:my lora:0.4>, <lora:my lora:0.6>, <lora:my lora:0.8>, <lora:my lora:1>`

   Here I made a comparison between different **models** (columns) and faces of different ethnicities via **S/R Prompt** (rows):

   <details>
   <summary>(Click) X/Y/Z Plot example</summary>
   
   ![X Y Z plot of models and ethnicities](images/XYZplot.png)
   </details>

   **Tip:** It appears possible to do S/R with commas by using quotes like this (note no spaces between the commas and quotes): `"term 1, term 2","term 3, term 4","term 5, term 6"`

* **Prompt Matrix** <a name="matrix"></a>[▲](#index)

   Similar conceptually to S/R from before, but more in-depth. It works by showing each possible combination of terms listed between the `|` symbol in your prompt, for example: `young man|tree|city` will always contain "young man", but we'll see what happens when we add or remove "tree" and "city". You can use commas and spaces just fine between the `|`.

   Inside the script, you will choose either your prompt or your negative prompt to make a matrix of, and whether the variable terms should be put at the start or the end.

   <a name="matrixneg"></a>Here is a comparison using the negative prompts I showed you in [Prompts ▲](#prompt). We can see how EasyNegative affects the image, as well as how the rest of the prompt affects the image, then both together:

   <details>
   <summary>(Click) Prompt matrix examples</summary>
  
   ![Prompt matrix of anime negative prompt sections](images/promptmatrix1.png)
   ![Prompt matrix of photorealistic negative prompt sections](images/promptmatrix2.png)
   </details>

   **Tip:** When using prompt matrix, the Batch Size will let you generate multiple images or the whole grid all at once.

* **Ultimate Upscaler** <a name="ultimate"></a>[▲](#index)

   An improved version of a builtin script, it can be added as an [extension ▲](#extensions) and used from within **img2img**. Its purpose is to resize an image and add more detail way past the normal limits of your VRAM by splitting it into chunks, although slower. Here are the steps:

   1. Generate your image normally up to 768 width and height, you can then apply hires fix if you are able to.

   1. From txt2img or the Image Browser extension send it directly into img2img, carrying its prompt and parameters.

   1. Set the **Denoising** somewhere between 0.1 and 0.4. If you go higher you most likely will experience mutations.

   1. Go down to **Scripts** and choose **Ultimate SD Upscale**. Then, set your parameters like this, with your desired size and upscaler, and the **"Chess" Type**:
   
      ![Ultimate upscale parameters](images/ultimate.png)

      * If you have enough VRAM, you may increase the **Tile width** as well as the **Padding**. For example, doubling both of them. **Tile height** can remain at 0 and it'll match the width.
     
      * It is not necessary to set the **Seams fix** unless you encounter visible seams between regions in the final image.
     
   1. Generate your image and wait. You can watch the squares get sharper if you have image previews enabled.

&nbsp;

# ControlNet <a name="controlnet"></a>[▲](#index)

ControlNet is an extremely powerful recent technology for Stable Diffusion. It lets you analyze information about any previously existing image and use it to guide the generation of your AI images. We'll see what this means in a moment.

If you're using the colab in this guide, you should enable the `all_control_models` option. Otherwise, you should first install the ControlNet [extension ▲](#extensions), then go [here](https://huggingface.co/webui/ControlNet-modules-safetensors/tree/main) to download some models which you'll need to place in `stable-diffusion-webui/extensions/sd-webui-controlnet/models`. I recommend at least Canny, Depth, Openpose and Scribble, which I will show here.

I will demonstrate how ControlNet may be used. For this I chose a popular image online as our "sample image". It's not necessary for you to follow along, but you can download the images and put them in the **PNG Info** tab to view their generation data.

First, you must scroll down in the txt2img page and click on ControlNet to open the menu. Then, click *Enable*, and pick a matching *preprocessor* and *model*. To start with, I chose Canny for both. Finally I upload my sample image. Make sure not to click over the sample image or it will start drawing. We can ignore the other settings.

![Control Net](images/controlnet.png)

* **Canny**

   The Canny method extracts the hard edges of the sample image. It is useful for many different types of images, specially where you want to preserve small details and the general look of an image. Observe:

   <details>
   <summary>(Click) Canny example</summary>
   
   ![Canny preprocessed image](images/canny1.png)
   ![Canny output image](images/canny2.png)
   </details>

* **Depth**

   The Depth method extracts the 3D elements of the sample image. It is best suited for complex environments and general composition. Observe:

   <details>
   <summary>(Click) Depth example</summary>
   
   ![Depth preprocessed image](images/depth1.png)
   ![Depth output image](images/depth2.png)
   </details>

* **Openpose**

   The Openpose method extracts the human poses of the sample image. It helps tremendously to get the desired shot and composition of your generated characters. Observe:

   <details>
   <summary>(Click) Openpose example</summary>
   
   ![Open Pose preprocessed image](images/openpose1.png)
   ![Open Pose output image](images/openpose2.png)
   </details>

* **Scribble**

   Lets you make a simple sketch and convert it into a finished piece with the help of your prompt. This is the only example not using the sample image above.

   <details>
   <summary>(Click) Scribble example</summary>
   
   ![Scribble sample image](images/scribble1.png)
   ![Scribble output image](images/scribble2.png)
   </details>

You will notice that there are 2 results for each method except Scribble. The first is an intermediate step called the *preprocessed image*, which is then used to produce the final image. You can supply the preprocessed image yourself, in which case you should set the preprocessor to *None*. This is extremely powerful with external tools such as Blender and Photoshop.

In the Settings tab there is a ControlNet section where you can enable *multiple controlnets at once*. One particularly good use is when one of them is Openpose, to get a specific character pose in a specific environment, or with specific hand gestures or details. Observe:

<details>
<summary>(Click) Openpose+Canny example</summary>

![Open Pose + Canny](images/openpose_canny.png)
</details>

You can also use ControlNet in img2img, in which the input image and sample image both will have a certain effect on the result. I do not have much experience with this method.

There are also alternative **diff** versions of each ControlNet model, which produce slightly different results. You can [try them](https://civitai.com/models/9868/controlnet-pre-trained-difference-models) if you want, but I personally haven't.

&nbsp;

# Lora Training for beginners <a name="train"></a>[▲](#index)

To train a [Lora ▲](#lora) is regarded as a difficult task. However, my new guide covers everything you need to know to get started for free, thanks to Google Colab:

**[🎴 Read my Lora making guide here](https://civitai.com/models/22530)**

You can also train a Lora on your own computer if you have at least 8 GB of VRAM. For that, I will list a few resources below:

* For training, use [bmaltais' Kohya GUI](https://github.com/bmaltais/kohya_ss). It has all the same settings as my trainer colab and more, so you can follow my guide too. Also there are youtube tutorials available in this link.
* Also, here's an [angry Lora training guide by ao](https://rentry.org/tohoaifaq#opinionated-lora-guide-for-colab)
* To collect your images from Gelbooru like in my guide, install [Grabber](https://github.com/Bionus/imgbrd-grabber/releases).
* To tag your dataset use the [WD1.4 Tagger extension](https://github.com/toriato/stable-diffusion-webui-wd14-tagger) for webui. First add and enable the extension, and restart your entire webui. Then go to the new **Tagger** tab, then **Batch from directory**, and select the folder with your images. Set the output name to `[name].txt` and the threshold at or above 0.35 (this is how closely each tag must match an image to be included). Then **Interrogate** and it will start generating your text files.
* To curate your tags like in my guide use the [Tag Editor extension](https://github.com/toshiaki1729/stable-diffusion-webui-dataset-tag-editor) for webui. It has all the features you need like sorting, pruning, replacing and merging tags. To add an activation tag it's as follows: After adding the extension and restarting your webui, go to the new **Dataset Tag Editor** tab then **Batch Edit Captions**. Turn off "*Show only the tags...*", turn on "*Prepend additional tags*", then add your activation tag inside the **Edit Tags** text box. Then apply your changes, scroll up and save your changes. Only then will it modify your files and add a new tag at the beginning of every text file.

&nbsp;

# ...vtubers? <a name="vtubers"></a>[▲](#index)

That's it, that's the end of this guide for now. I'd be grateful if you want to contribute on missing topics like:
* img2img
* Inpainting
* Controlnet t2i adapters

Thank you for reading!

I have [a separate repo that aggregates vtuber Loras, specially Hololive](https://huggingface.co/hollowstrawberry/holotard). If you're interested in that.

Cheers.

&nbsp;
