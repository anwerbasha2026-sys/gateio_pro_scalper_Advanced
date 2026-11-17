# Gate.io Pro Scalper — Smart TP & Trailing SL Engine (Kivy Edition)

نسخة **Kivy** الكاملة من تطبيق **Gate.io Pro Scalper** المخصصة للرفع على **GitHub** (لتشغيلها على الكمبيوتر أو تحويلها تلقائياً إلى تطبيق أندرويد **APK** عبر **GitHub Actions + Buildozer**) مع الاحتفاظ الكامل بنسبة 100% بجميع الخيارات والمؤشرات والاستراتيجية وقواعد البيانات، والتحويل الكامل للعمل على واجهة **[Gate.io API v4](https://www.gate.com/docs/developers/apiv4/)**.

## المميزات والاستراتيجية المحفوظة بالكامل
- **إدارة حساب Gate.io API v4**: دعم كامل لوضع التداول التجريبي (`PAPER`) والحقيقي (`LIVE`) عبر توقيع `HMAC-SHA512` القياسي مع حفظ مفاتيح الـ API محلياً.
- **نفس شروط الفلترة والاستراتيجية دون أي تغيير**:
  - فحص أعلى 200 عملة سيولة في سوق Spot المعتمدة عبر [`/api/v4/spot/currency_pairs`](https://github.com/gateio/gateapi-python/blob/master/docs/SpotApi.md) و [`/api/v4/spot/tickers`](https://github.com/gateio/gateapi-python/blob/master/docs/SpotApi.md) واستبعاد العملات المستقرة والأسهم المرمّزة وعملات الرافعة المالية والعملات تحت التقييم (`st_tag`).
  - شرط ترتيب المتوسطات الأسية الصاعد `EMA9 > EMA21 > EMA200` على فريم `5m` وفوق `VWAP`، مع تأكيد الاتجاه الصاعد على الفريمات الأعلى `15m` و `1h` عبر [`/api/v4/spot/candlesticks`](https://github.com/gateio/gateapi-python/blob/master/docs/SpotApi.md).
  - فلتر الفوليوم (`vol_multiplier`) وفلتر التجميع / التغير السعري البسيط (`max_price_change_pct`).
  - فلتر ضغط دفتر الأوامر (`Order Book Pressure`) عبر [`/api/v4/spot/order_book`](https://github.com/gateio/gateapi-python/blob/master/docs/SpotApi.md) لاستبعاد العملة إذا كانت قيمة أوامر البيع أكبر من الشراء.
  - مؤشر القوة النسبية `RSI (14)` مع إمكانية تفعيله/تعطيله وتحديد النطاق الأدنى والأعلى.
  - مؤشر `MACD (12, 26, 9)` مع شرط التقاطع الإيجابي (`MACD > Signal` و `Histogram > 0`).
- **إدارة الصفقة الذكية (Pro TP/SL)**:
  - تأمين الصفقة التلقائي واليدوي على نقطة الدخول (`Break-Even`).
  - الوقف المتحرك لملاحقة الأرباح (`Trailing Stop Loss`).
  - البيع الجزئي بنسبة 50% عند الهدف الأول (`TP1`) ومتابعة الهدف النهائي (`TP2`).
  - الإغلاق الفوري بسعر السوق (`Market IOC`) عبر [`/api/v4/spot/orders`](https://www.fmz.com/syntax-guide/exchanges/cex/gate) أو الإغلاق الإجباري المحلي (`Force Close`) ومسح السجلات والقائمة السوداء.

## محتويات المشروع للرفع على GitHub
- `main.py`: الكود الكامل للتطبيق بواجهة Kivy المتجاوبة (تعمل على الهاتف والكمبيوتر).
- `NotoSansArabic-Regular.ttf`: خط عربي مدمج لضمان ظهور النصوص العربية بشكل سليم على جميع الأنظمة وأندرويد.
- `buildozer.spec`: ملف إعدادات Buildozer لبناء ملف الـ APK (`org.gateioproscalperadvanced`).
- `requirements.txt`: المكتبات المطلوبة للتشغيل المباشر.
- `.github/workflows/build-apk.yml`: ملف البناء التلقائي عبر GitHub Actions لاستخراج ملف الـ APK مباشرة من GitHub.

## طريقة الرفع على GitHub واستخراج الـ APK
1. أنشئ مستودعاً (Repository) جديداً على حسابك في **GitHub**.
2. ارفع جميع ملفات المشروع (`main.py`, `buildozer.spec`, `requirements.txt`, `NotoSansArabic-Regular.ttf`, ومجلد `.github/workflows/build-apk.yml`).
3. انتقل إلى تبويب **Actions** داخل مستودعك على GitHub، وستجد عملية البناء **Build Gateio Pro Scalper Advanced** تعمل تلقائياً (أو اضغط **Run workflow**).
4. بعد انتهاء البناء، قم بتحميل ملف `Gateio-Pro-Scalper-Advanced-ONN-GN3-ARM32` من قسم **Artifacts**.
