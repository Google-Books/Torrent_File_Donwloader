<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Download Torrent</title>
    <style>
        body {
            background-color: #000000; /* بک‌گراند کاملا سیاه */
            margin: 0;
            padding: 20px 0 50px 0;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 200vh; /* برای اطمینان از قابلیت اسکرول صفحه */
        }

        /* کانتینر تبلیغات */
        .ad-container {
            margin: 15px 0;
            display: flex;
            justify-content: center;
            width: 100%;
            overflow: hidden;
        }

        /* استایل پایه دکمه برای موبایل (بزرگتر از قبل) */
        .download-btn {
            background-color: #28a745;
            color: #ffffff;
            padding: 20px 50px;
            font-size: 22px;
            font-weight: bold;
            border-radius: 12px;
            text-decoration: none;
            box-shadow: 0 6px 0 #1e7e34, 0 10px 15px rgba(0,0,0,0.6);
            transition: all 0.1s;
            margin-top: 25px;
            margin-bottom: 25px;
            text-align: center;
            display: inline-block;
            border: none;
            cursor: pointer;
        }

        .download-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #1e7e34, 0 5px 8px rgba(0,0,0,0.6);
        }

        /* استایل دکمه برای دستگاه‌های بزرگتر (تبلت، لپ‌تاپ و کامپیوتر) */
        @media (min-width: 768px) {
            .download-btn {
                padding: 35px 90px;
                font-size: 32px;
                border-radius: 18px;
                box-shadow: 0 8px 0 #1e7e34, 0 15px 20px rgba(0,0,0,0.7);
                margin-top: 40px;
                margin-bottom: 40px;
            }
            .download-btn:active {
                transform: translateY(6px);
                box-shadow: 0 2px 0 #1e7e34, 0 8px 12px rgba(0,0,0,0.7);
            }
        }
    </style>
</head>
<body>

    <!-- جایگاه تبلیغ اول (بالای دکمه) -->
    <div class="ad-container" id="ad-top-slot"></div>

    <!-- 
    ====== قسمت تغییر لینک و اسم دکمه ======
    برای تغییر اسم دکمه، متن بین تگ‌ها رو تغییر بده.
    برای تغییر لینک دانلود، آدرس داخل ویژگی href رو عوض کن.
    -->
    <a href="https://archive.org/download/22-switchblade.mb/22Switchblade.mb.torrent" class="download-btn" id="downloadButton" target="_blank">
        Download Torrent File
    </a>
    <!-- ==================================== -->

    <!-- جایگاه تبلیغ دوم (پایین دکمه 1) -->
    <div class="ad-container" id="ad-bottom-slot-1"></div>
    
    <!-- جایگاه تبلیغ سوم (پایین دکمه 2) -->
    <div class="ad-container" id="ad-bottom-slot-2"></div>

    <script>
        // تابع ایجاد تبلیغ در یک iframe ایزوله برای جلوگیری از تداخل کدها
        function createIframeAd(containerId, adCode, width, height) {
            const container = document.getElementById(containerId);
            container.innerHTML = ''; // پاکسازی کانتینر قبل از لود مجدد
            
            const iframe = document.createElement('iframe');
            iframe.width = width;
            iframe.height = height;
            iframe.frameBorder = "0";
            iframe.scrolling = "no";
            iframe.style.border = "none";
            iframe.style.overflow = "hidden";
            container.appendChild(iframe);

            const doc = iframe.contentWindow.document;
            doc.open();
            // تزریق کد با بک‌گراند مشکی تا با صفحه هماهنگ باشد
            doc.write('<html><head><style>body{margin:0;padding:0;background:#000;display:flex;justify-content:center;align-items:center;height:100vh;}</style></head><body>' + adCode + '</body></html>');
            doc.close();
        }

        // تابع اصلی بررسی دستگاه و لود تبلیغات متناسب
        function loadAllAds() {
            const screenWidth = window.innerWidth;
            const isDesktopOrTablet = screenWidth >= 768; // 768 پیکسل به بالا به عنوان تبلت و کامپیوتر در نظر گرفته می‌شود

            // کدهای تبلیغاتی
            const ad300x250 = `<script>atOptions={'key':'fbbc77f2f398f4abc96969e7992e2752','format':'iframe','height':250,'width':300,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/fbbc77f2f398f4abc96969e7992e2752/invoke.js"></scr`+`ipt>`;
            const adNative = `<script async="async" data-cfasync="false" src="https://speedingdeadlyplays.com/d7077547f7a1416ae3fbd97b9d3c1174/invoke.js"></scr`+`ipt><div id="container-d7077547f7a1416ae3fbd97b9d3c1174"></div>`;

            if (isDesktopOrTablet) {
                // *** قانون برای تبلت، لپ‌تاپ و کامپیوتر ***
                // فقط تبلیغ نیتیو نمایش داده شود (بالا 1 بار، پایین 2 بار)
                createIframeAd('ad-top-slot', adNative, "100%", 400); // عرض کامل، ارتفاع 400 برای نیتیو
                createIframeAd('ad-bottom-slot-1', adNative, "100%", 400);
                createIframeAd('ad-bottom-slot-2', adNative, "100%", 400);
            } else {
                // *** قانون برای موبایل (دستگاه‌های کوچکتر) ***
                // بالا: تبلیغ بزرگ 300 در 250 (جایگزین بنر کوچک قبلی)
                createIframeAd('ad-top-slot', ad300x250, 300, 250);
                // پایین 1: تبلیغ 300 در 250
                createIframeAd('ad-bottom-slot-1', ad300x250, 300, 250);
                // پایین 2: تبلیغ نیتیو
                createIframeAd('ad-bottom-slot-2', adNative, "100%", 400);
            }
        }

        // 1. لود اولیه تبلیغات هنگام باز شدن صفحه
        loadAllAds();

        // 2. تنظیم رفرش (ریلود) خودکار تمامی تبلیغات دقیقاً هر 10 ثانیه یکبار
        setInterval(loadAllAds, 10000); // 10000 میلی‌ثانیه = 10 ثانیه
    </script>
</body>
</html>
