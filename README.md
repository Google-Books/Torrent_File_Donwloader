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
            padding: 20px 0;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            /* سه برابر کردن طول صفحه برای موبایل جهت اسکرول بیشتر */
            min-height: 300vh; 
        }

        /* ========== استایل‌های موبایل (بدون هیچ تغییری طبق درخواست شما) ========== */
        .ad-container {
            margin: 10px 0;
            display: flex;
            justify-content: center;
            width: 100%;
            overflow: hidden;
        }

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
            margin-top: 20px;
            margin-bottom: 20px;
            text-align: center;
            display: inline-block;
            border: none;
            cursor: pointer;
        }

        .download-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #1e7e34, 0 5px 8px rgba(0,0,0,0.6);
        }

        /* ========== استایل‌های دستگاه‌های بزرگتر (تبلت، لپ‌تاپ و کامپیوتر) ========== */
        @media (min-width: 768px) {
            body {
                min-height: 100vh; 
            }
            .ad-container {
                /* نزدیک شدن شدید تبلیغات به یکدیگر (فاصله در حد 2 پیکسل) */
                margin: 2px 0; 
            }
            .download-btn {
                padding: 30px 80px;
                font-size: 32px;
                border-radius: 18px;
                box-shadow: 0 8px 0 #1e7e34, 0 15px 20px rgba(0,0,0,0.7);
                /* چسباندن دکمه به تبلیغ بالایی و تبلیغ پایینی (فاصله مورچه‌ای!) */
                margin-top: 2px; 
                margin-bottom: 2px;
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

    <!-- دکمه دانلود -->
    <a href="https://archive.org/download/22-switchblade.mb/22Switchblade.mb.torrent" class="download-btn" id="downloadButton" target="_blank">
        Download Torrent File
    </a>

    <!-- جایگاه تبلیغ دوم (پایین دکمه 1) -->
    <div class="ad-container" id="ad-bottom-slot-1"></div>
    
    <!-- جایگاه تبلیغ سوم (پایین دکمه 2) -->
    <div class="ad-container" id="ad-bottom-slot-2"></div>

    <script>
        // تابع ایجاد تبلیغ در iframe
        function createIframeAd(containerId, adCode, width, height) {
            const container = document.getElementById(containerId);
            container.innerHTML = ''; 
            
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
            // تزریق کدهای تبلیغات با بک‌گراند مشکی
            doc.write('<html><head><style>body{margin:0;padding:0;background:#000;display:flex;justify-content:center;align-items:center;height:100%;}</style></head><body>' + adCode + '</body></html>');
            doc.close();
        }

        function loadAllAds() {
            const screenWidth = window.innerWidth;
            const isDesktopOrTablet = screenWidth >= 768; 

            const ad300x250 = `<script>atOptions={'key':'fbbc77f2f398f4abc96969e7992e2752','format':'iframe','height':250,'width':300,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/fbbc77f2f398f4abc96969e7992e2752/invoke.js"></scr`+`ipt>`;
            const adNative = `<script async="async" data-cfasync="false" src="https://speedingdeadlyplays.com/d7077547f7a1416ae3fbd97b9d3c1174/invoke.js"></scr`+`ipt><div id="container-d7077547f7a1416ae3fbd97b9d3c1174"></div>`;

            if (isDesktopOrTablet) {
                // دسکتاپ و تبلت: ارتفاع تبلیغ نیتیو 500 در نظر گرفته شده تا کاملا در کنار هم جا شوند
                createIframeAd('ad-top-slot', adNative, "100%", 500); 
                createIframeAd('ad-bottom-slot-1', adNative, "100%", 500);
                createIframeAd('ad-bottom-slot-2', adNative, "100%", 500);
            } else {
                // موبایل (بدون تغییر)
                createIframeAd('ad-top-slot', ad300x250, 300, 250);
                createIframeAd('ad-bottom-slot-1', ad300x250, 300, 250);
                createIframeAd('ad-bottom-slot-2', adNative, "100%", 1000);
            }
        }

        // اجرای اولیه و تنظیم رفرش 10 ثانیه ای
        loadAllAds();
        setInterval(loadAllAds, 10000);
    </script>
</body>
</html>
