<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Download Torrent</title>
    <style>
        body {
            background-color: #000000; /* بک گراند کاملا سیاه */
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 200vh; /* قابلیت اسکرول صفحه */
            padding-top: 110px; /* فاصله برای بنر چسبان بالا */
        }

        /* بنر چسبان بالای صفحه */
        .top-banner {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background-color: #000000;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            margin: 0;
            padding: 0;
        }

        /* دکمه سه بعدی، سبز و گوشه گرد */
        .download-btn {
            background-color: #28a745;
            color: #ffffff;
            padding: 15px 40px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 12px;
            text-decoration: none;
            box-shadow: 0 6px 0 #1e7e34, 0 10px 15px rgba(0,0,0,0.5);
            transition: all 0.1s;
            margin-top: 30px;
            margin-bottom: 10px;
            text-align: center;
            display: inline-block;
        }

        .download-btn:active {
            transform: translateY(4px);
            box-shadow: 0 2px 0 #1e7e34, 0 5px 8px rgba(0,0,0,0.5);
        }

        /* فاصله کم برای تبلیغات پایین */
        .ad-container {
            margin: 10px 0;
            display: flex;
            justify-content: center;
            width: 100%;
        }
    </style>
</head>
<body>

    <!-- کانتینر تبلیغ چسبان بالا -->
    <div class="top-banner" id="top-ad"></div>

    <!-- 
    ====== قسمت تغییر لینک و اسم دکمه ======
    لینک (href) و اسم دکمه رو میتونی از خط پایین تغییر بدی 
    -->
    <a href="https://archive.org/download/22-switchblade.mb/22Switchblade.mb.torrent" class="download-btn" target="_blank">
        Download Torrent File
    </a>
    <!-- ==================================== -->

    <!-- کانتینر تبلیغ زیر دکمه -->
    <div class="ad-container" id="bottom-ad"></div>
    
    <!-- کانتینر تبلیغ نیتیو -->
    <div class="ad-container" id="native-ad"></div>

    <script>
        // تابع ساخت iframe برای دور زدن محدودیت‌های لود تبلیغات
        function createIframeAd(containerId, adCode, width, height) {
            const container = document.getElementById(containerId);
            container.innerHTML = ''; // پاک کردن تبلیغ قبلی
            
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
            // تزریق کدهای تبلیغاتی به داخل iframe با پس زمینه مشکی
            doc.write('<html><head><style>body{margin:0;padding:0;background:#000;display:flex;justify-content:center;}</style></head><body>' + adCode + '</body></html>');
            doc.close();
        }

        // تابع اصلی لود و ریلود تبلیغات
        function loadAllAds() {
            const screenWidth = window.innerWidth;
            
            // 1. منطق نمایش تبلیغ بالا بر اساس سایز دستگاه کاربر
            let topAdCode = '';
            let topW = 320, topH = 50;

            if (screenWidth >= 768) { // سایز بزرگ (دسکتاپ/تبلت بزرگ)
                topAdCode = `<script>atOptions={'key':'f149a587920745dc076b1f8fe3e2a0a0','format':'iframe','height':90,'width':728,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/f149a587920745dc076b1f8fe3e2a0a0/invoke.js"></scr`+`ipt>`;
                topW = 728; topH = 90;
            } else if (screenWidth >= 480) { // سایز میانه (تبلت)
                topAdCode = `<script>atOptions={'key':'90a8d37acfa9e879fd26c5bcd919d8a1','format':'iframe','height':60,'width':468,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/90a8d37acfa9e879fd26c5bcd919d8a1/invoke.js"></scr`+`ipt>`;
                topW = 468; topH = 60;
            } else { // سایز کوچک (موبایل)
                topAdCode = `<script>atOptions={'key':'2fe12843aa95d044d4fef22456b0668a','format':'iframe','height':50,'width':320,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/2fe12843aa95d044d4fef22456b0668a/invoke.js"></scr`+`ipt>`;
                topW = 320; topH = 50;
            }
            createIframeAd('top-ad', topAdCode, topW, topH);

            // 2. تبلیغ 300x250 با فاصله کم زیر دکمه
            const bottomAdCode = `<script>atOptions={'key':'fbbc77f2f398f4abc96969e7992e2752','format':'iframe','height':250,'width':300,'params':{}};</scr`+`ipt><script src="https://speedingdeadlyplays.com/fbbc77f2f398f4abc96969e7992e2752/invoke.js"></scr`+`ipt>`;
            createIframeAd('bottom-ad', bottomAdCode, 300, 250);

            // 3. تبلیغ نیتیو در پایین‌ترین قسمت
            const nativeAdCode = `<script async="async" data-cfasync="false" src="https://speedingdeadlyplays.com/d7077547f7a1416ae3fbd97b9d3c1174/invoke.js"></scr`+`ipt><div id="container-d7077547f7a1416ae3fbd97b9d3c1174"></div>`;
            createIframeAd('native-ad', nativeAdCode, "100%", 400); // ارتفاع 400 برای جا دادن نیتیو
        }

        // اجرای تبلیغات در لحظه باز شدن صفحه
        loadAllAds();

        // رفرش شدن تمام تبلیغ‌ها دقیقا هر 10 ثانیه (10000 میلی‌ثانیه)
        setInterval(loadAllAds, 10000);
    </script>
</body>
</html>
