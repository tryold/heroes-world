# عالم الأبطال - نسخة الويب (HTML/CSS/JS)

## 📁 هيكل الملفات
```
WebApp/
├── index.html          # التطبيق (SPA - Single Page Application)
├── video_list.js       # قائمة الفيديوهات (تُحدّث تلقائياً)
├── README_WEB.md       # هذا الملف
├── Images/             # 34 صورة (حيوانات/فواكه/خضروات)
├── Sounds/             # 70 ملف صوت (b_/f_ + animals + letters + quran + numbers)
└── video/              # 8 ملفات فيديو (mp4)
```

## 🚀 cách chạy (كيفية التشغيل)

### 1. محلياً (على جهازك)
1. انسخ `WebApp\` إلى مجلد
2. افتح `index.html` في متصفح (Chrome/Edge/Safari)
3. يعمل بدون خادم (server) — كل شيء client-side

### 2. على iPad / iPhone
1. ارفع `WebApp\` إلى Dropbox / Google Drive / GitHub Pages
2. افتح الرابط في Safari
3. **إضافة إلى الشاشة الرئيسية**: Safari → Share → Add to Home Screen
4. سيعمل كتطبيق (PWA-like) بدون شريط عنوان

### 3. استضافة (Hosting)
- **GitHub Pages**: مجاني، سهل
- **Netlify**: مجاني، drag & drop
- **Vercel**: مجاني
- **Dropbox**: public link (محدود)

## 📂 ربط الملفات (Dropbox)

### صور الحيوانات
- رابط Dropbox: `https://www.dropbox.com/s/XXXX/lion.png?dl=1`
- في `index.html`: `'Images/' + c.image` → استبدل بـ Dropbox link

### أصوات
- رابط Dropbox: `https://www.dropbox.com/s/XXXX/b_Animals.wav?dl=1`
- في `index.html`: `'Sounds/Animals/' + ...` → استبدل بـ Dropbox link

### فيديوهات
- رابط Dropbox: `https://www.dropbox.com/s/XXXX/video.mp4?dl=1`
- في `index.html`: `'video/' + name + '.mp4'` → استبدل بـ Dropbox link

## 🎯 ميزات
- ✅ متعدد الشاشات (SPA) — لا إعادة تحميل
- ✅ RTL (عربي) — `dir="rtl"`
- ✅ Responsive (iPad-friendly)
- ✅ localStorage (حفظ التقدم)
- ✅ Leaderboard (لوحة النجوم)
- ✅ TTS (Web Speech API) — ينطق العربية
- ✅ Confetti animation
- ✅ جميع الألعاب: حروف، حيوانات، قرآن، أرقام، ألوان، ذاكرة، ربط، فيديو

## 📱 iPad Tips
- استخدم Safari (أفضل دعم لـ Web Speech API)
- أضف إلى Home Screen (يعمل كتطبيق)
- تأكد من اتصال إنترنت (لتحميل الصور/الأصوات)

## 🔧 تخصيص
- **Media URLs**: استبدل `'Images/'`, `'Sounds/'`, `'video/'` بـ Dropbox links
- **Colors**: عدّل CSS variables في `:root`
- **Content**: عدّل arrays (letters, animals, surahs, etc.) في `<script>`
- **Videos**: عدّل `video_list.js` (تُحدّث تلقائياً عند إضافة videos)

## 📊 الإحصائيات (Leaderboard)
- محفوظة في `localStorage` (محلية)
- للـ global leaderboard: استخدم Firebase / Supabase (backend)

## ⚠️ ملاحظات
- Web Speech API (TTS) يتطلب اتصال إنترنت (أو voice pack محلي)
- Dropbox links: استخدم `?dl=1` للتحميل المباشر
- الصور/الأصوات: CORS قد يسبب مشاكل — استخدم Dropbox direct links
- الفيديوهات: WebBrowser/HTML5 video player

## 📝 إضافة فيديوهات جديدة
1. ضع ملف `*.mp4` في `video\`
2. أعد توليد `video_list.js`:
   ```powershell
   $base = "C:\path\to\WebApp"
   $names = [System.IO.Directory]::GetFiles("$base\video", "*.mp4") | ForEach-Object { [System.IO.Path]::GetFileNameWithoutExtension($_) }
   $js = "const videos = [`n"
   foreach ($n in $names) { $js += "    '" + $n + "',`n" }
   $js += "];"
   $js | Out-File "$base\video_list.js" -Encoding UTF8
   ```
3. أو عدّل `video_list.js` يدوياً