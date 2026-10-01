🚀 NeoTenet Persistent Workspace & Hermes Agent Deployment

محیط ترمینال پرسرعت Ubuntu روی Google Colab همراه با سیستم پشتیبان‌گیری خودکار Google Drive و راهنمای کامل نصب و اجرای Hermes Agent






</div>

🧭 فهرست مطالب

📌 درباره پروژه

⚙️ تنظیمات سخت‌افزاری در Google Colab

⚡ نحوه اجرای پروژه و راه‌اندازی ترمینال

🔄 سیستم بکاپ‌گیری و بازیابی خودکار

🤖 نصب Hermes Agent

🛡️ جلوگیری از قطع شدن Google Colab

📂 ساختار پیشنهادی پروژه

📢 کانال رسمی NeoTenet

📌 درباره پروژه

این پروژه امکان اجرا و داشتن یک سرور مجازی Ubuntu با دسترسی Root روی بستر Google Colab را فراهم می‌کند.

هدف اصلی سیستم، حل مشکل از بین رفتن اطلاعات و پروژه‌ها در Colab است. فایل‌ها و پروژه‌های شما، از جمله Hermes Agent، روی Google Drive ذخیره و پشتیبان‌گیری می‌شوند تا در اجرای بعدی جلسه، اطلاعات قبلی به‌صورت خودکار بازیابی شوند.

✨ قابلیت‌های اصلی

قابلیت

توضیح

🐧 Ubuntu VPS

اجرای محیط Ubuntu با دسترسی Root داخل Google Colab

☁️ Google Drive Backup

ذخیره نسخه پشتیبان پروژه روی Google Drive

🔄 Auto-Restore

بازیابی خودکار اطلاعات در اجرای مجدد

⏱️ Background Backup

تهیه بکاپ خودکار در پس‌زمینه

🌐 Web Terminal

دسترسی به ترمینال Ubuntu از طریق مرورگر

⚡ Cloudflare Tunnel

ایجاد لینک دسترسی با trycloudflare.com

🤖 Hermes Agent

نصب و اجرای Hermes Agent در محیط آماده

نکته: فایل نوت‌بوک پروژه باید با نام NeoTenet_VPS.ipynb در ریپازیتوری قرار داشته باشد تا Badge مربوط به Google Colab به‌درستی کار کند.

⚙️ ۱. تنظیمات سخت‌افزاری در Google Colab

پیش از اجرای نوت‌بوک .ipynb در Google Colab، تنظیمات زیر را اعمال کنید:

وارد فایل NeoTenet_VPS.ipynb در محیط Google Colab شوید.

از منوی بالای صفحه روی Runtime کلیک کرده و Change runtime type را انتخاب کنید.

در بخش Hardware accelerator یکی از گزینه‌های زیر را انتخاب کنید:

نوع استفاده

انتخاب پیشنهادی

🧩 کارهای عمومی و سبک

CPU

🧠 پردازش‌های هوش مصنوعی و سنگین

T4 GPU

روی Save کلیک کنید.

⚡ ۲. نحوه اجرای پروژه و راه‌اندازی ترمینال

نوت‌بوک NeoTenet_VPS.ipynb را اجرا کنید (Shift + Enter).

هنگام درخواست دسترسی، اتصال به Google Drive را تأیید کنید.
این مرحله برای ذخیره‌سازی فایل‌های شما ضروری است.

اسکریپت به‌صورت خودکار بکاپ‌های قبلی را شناسایی و بازیابی می‌کند.

در انتهای خروجی سلول Colab، یک لینک اختصاصی از Cloudflare مانند زیر تولید می‌شود:

https://xxx.trycloudflare.com

لینک را در مرورگر باز کنید تا وارد محیط وب ترمینال Ubuntu شوید.

🖥️ روند کلی اجرا

Google Colab
     │
     ├── اتصال به Google Drive
     │
     ├── بازیابی Backup قبلی
     │
     ├── اجرای Ubuntu + Web Terminal
     │
     └── ایجاد Cloudflare Tunnel
                 │
                 ▼
        Browser → Web Terminal

🔄 ۳. سیستم بکاپ‌گیری و بازیابی خودکار اطلاعات

آیا فایل‌ها پس از اجرای مجدد Colab باقی می‌مانند؟

بله. فرآیند ذخیره و بازیابی به دو بخش اصلی تقسیم می‌شود:

♻️ بازیابی خودکار — Auto-Restore

با هر بار اجرای مجدد نوت‌بوک Google Colab، سیستم به Google Drive متصل می‌شود و فایل پشتیبان:

hermes_backup.tar.gz

را مستقیماً در مسیر اصلی ترمینال بازیابی می‌کند.

🔐 بکاپ خودکار در پس‌زمینه — Background Daemon

تا زمانی که سرور روشن است، یک سرویس پس‌زمینه هر ۵ دقیقه یک‌بار تغییرات پوشه پروژه را فشرده کرده و فایل بکاپ را روی Google Drive جایگزین می‌کند.

📦 مسیر Backup

/content/drive/MyDrive/Hermes_Project/hermes_backup.tar.gz

✋ پشتیبان‌گیری دستی

برای بکاپ فوری، بدون منتظر ماندن برای چرخه‌ی ۵ دقیقه‌ای، داخل Web Terminal دستور زیر را اجرا کنید:

tar -czvf /content/drive/MyDrive/Hermes_Project/hermes_backup.tar.gz /root/hermes-agent

💡 پیشنهاد: قبل از پایان دادن به جلسه Colab یا انجام تغییرات مهم، یک Backup دستی ایجاد کنید.

🤖 ۴. آموزش کامل نصب Hermes Agent (در ترمینال)

پس از ورود به Web Terminal از طریق لینک Cloudflare، دستورات زیر را به‌ترتیب کپی و اجرا کنید.

1️⃣ آپدیت مخازن و نصب پیش‌نیازها

apt update && apt upgrade -y
apt install python3 python3-pip git -y

2️⃣ نصب مدیریت پکیج UV

pip install uv --break-system-packages

3️⃣ دریافت سورس Hermes از GitHub

git clone https://github.com/nousresearch/hermes-agent.git
cd hermes-agent

4️⃣ همگام‌سازی و تست اولیه

uv sync
uv run hermes --help

5️⃣ اجرای نهایی Hermes

hermes

🧩 همه دستورات در یک‌جا

apt update && apt upgrade -y
apt install python3 python3-pip git -y

pip install uv --break-system-packages

git clone https://github.com/nousresearch/hermes-agent.git
cd hermes-agent

uv sync
uv run hermes --help

hermes

🔗 سورس Hermes Agent:
https://github.com/nousresearch/hermes-agent

🛡️ ۵. جلوگیری از قطع شدن گوگل کولب (Anti-Idle Script)

برای جلوگیری از بسته شدن اتوماتیک جلسه Google Colab در اثر عدم فعالیت:

در صفحه Google Colab کلیدهای Ctrl + Shift + I (یا F12) را فشار دهید.

وارد تب Console شوید.

کد JavaScript زیر را Paste کرده و Enter بزنید:

function KeepAlive() {
    console.log("Keeping Colab Session Active...");
    document.querySelector("colab-connect-button")?.click();
}

setInterval(KeepAlive, 60000);

⚠️ این اسکریپت را مسئولانه استفاده کنید و محدودیت‌ها و قوانین سرویس Google Colab را در نظر بگیرید.

📂 ساختار پیشنهادی پروژه

برای مرتب نگه داشتن ریپازیتوری، ساختار پیشنهادی به شکل زیر است:

.
├── NeoTenet_VPS.ipynb
├── README.md
├── LICENSE
└── screenshots/

🧱 فایل‌های مهم

فایل / مسیر

کاربرد

NeoTenet_VPS.ipynb

نوت‌بوک اصلی اجرای محیط

README.md

مستندات و راهنمای نصب

LICENSE

مجوز پروژه

screenshots/

تصاویر و پیش‌نمایش‌های پروژه

✅ چک‌لیست راه‌اندازی

[ ] ساخت / باز کردن NeoTenet_VPS.ipynb
[ ] انتخاب CPU یا T4 GPU
[ ] اتصال Google Drive
[ ] اجرای کامل Notebook
[ ] دریافت Cloudflare URL
[ ] ورود به Web Terminal
[ ] نصب Hermes Agent
[ ] بررسی اجرای `hermes`
[ ] ایجاد Backup دستی در صورت نیاز

🧠 نکات مهم

سیستم برای اجرای محیط Ubuntu در Google Colab طراحی شده است.

اطلاعات پروژه در Google Drive پشتیبان‌گیری می‌شوند تا در اجرای مجدد قابل بازیابی باشند.

بکاپ پس‌زمینه در حالت عادی هر ۵ دقیقه اجرا می‌شود.

برای Backup فوری می‌توانید دستور tar ارائه‌شده در بالا را اجرا کنید.

لینک دسترسی ترمینال از طریق Cloudflare تولید می‌شود.

برای استفاده از Hermes Agent، دستورات نصب را به‌ترتیب اجرا کنید.

Google Drive را بدون تأیید دسترسی رها نکنید؛ اتصال به Drive بخش مهم فرآیند ذخیره‌سازی و بازیابی است.

📢 کانال رسمی NeoTenet

<div align="center">

توسعه داده شده توسط تیم NeoTenet 🚀

برای دریافت آخرین آپدیت‌ها، کدهای جدید، ابزارها و پروژه‌های بیشتر به کانال تلگرام ما بپیوندید:



<br>

© NeoTenet — All Rights Reserved

</div>

⭐ حمایت از پروژه

اگر این پروژه برای شما مفید بود، با یک ⭐ به ریپازیتوری GitHub انگیزه‌ی توسعه‌ی نسخه‌های بعدی را بیشتر کنید.

<div align="center">

Made with ❤️ by NeoTenet

</div>