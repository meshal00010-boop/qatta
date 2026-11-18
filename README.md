# القطّة: نسخة الموقع المستقل

## وش في المجلد
- `index.html`: التطبيق كامل.
- `config.js`: إعدادات Firebase، تنعبى وقت النشر.
- `firestore.rules`: قواعد الحماية لقاعدة البيانات.
- `manifest.json` و`icon-*.png`: اسم التطبيق وأيقونته في الشاشة الرئيسية.

إذا ما تعبّت `config.js`، يشتغل الموقع كنسخة تجربة محفوظة على الجهاز بس.

## خطوات النشر (حوالي نص ساعة، مرة وحدة بس)

### 1) Firebase: قاعدة البيانات وتسجيل الدخول
1. ادخل https://console.firebase.google.com بحساب قوقل، واضغط **Create a project** وسمّه `qatta`. خدمة Google Analytics مو لازمة.
2. من القائمة: **Build → Authentication → Get started**، وشغّل **Anonymous**.
3. من القائمة: **Build → Firestore Database → Create database**، واختر أقرب منطقة (مثلاً `europe-west` أو `me-central`)، وابدأ بـ **production mode**.
4. في Firestore افتح تبويب **Rules**، والصق محتوى `firestore.rules`، واضغط **Publish**.
5. من ⚙️ **Project settings → General → Your apps** اضغط أيقونة الويب `</>`، وسجّل تطبيق باسم `qatta`. خدمة Hosting مو لازمة.
6. انسخ القيم `apiKey` و`authDomain` و`projectId` و`appId` وحطها في `config.js`.

### 2) الاستضافة: رفع الموقع
1. ادخل https://app.netlify.com/drop وسجّل دخولك.
2. اسحب مجلد الموقع كامل للصفحة، ويعطيك رابط مثل `https://qatta-xxxx.netlify.app`.
3. من **Site configuration → Change site name** تقدر تغيّر الاسم لشي أسهل.
4. ارجع لـ Firebase: **Authentication → Settings → Authorized domains**، وأضف رابط الموقع.

### 3) على الآيفون
افتح الرابط في سفاري، واضغط زر المشاركة، واختر **إضافة إلى الشاشة الرئيسية**. يطلع بأيقونة القطّة واسمه، ويفتح بملء الشاشة.

## ملاحظات
- كل شخص يُعرَّف بجهازه: يكتب اسمه مرة وحدة. وإذا مسح بيانات سفاري أو غيّر جواله، يرجع يدخل القطّات من الرابط، بس القطّات اللي سواها من الجهاز القديم ما تبقى باسمه.
- الخريطة من OpenStreetMap، والبحث عن الأماكن من Nominatim، وكلها مجانية.
- الخطة المجانية في Firebase تكفي للربع وزيادة.
