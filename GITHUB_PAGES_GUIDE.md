# دليل النشر على GitHub Pages + Firebase
## نظام زيارات إدارة المخاطر

---

## ✅ ما تم تعديله في index.html

تعديل واحد فقط — إضافة إعدادات Firebase مباشرة في الكود:

```javascript
const HARDCODED_FB_CFG = {
  apiKey: "AIzaSyAQRFyfayXYCDFSaJ23HUQsXrOW8cVuTJ4",
  authDomain: "cash-makhater2-data.firebaseapp.com",
  projectId: "cash-makhater2-data",
  appId: "1:431443769425:web:1481dd22155f73f2a7e070"
};
```

**النتيجة:** الموقع يتصل بـ Firebase تلقائياً على أي جهاز فور فتحه، بدون أي إعداد يدوي.

---

## الجزء الأول: إنشاء Repository على GitHub

### الخطوة 1 — إنشاء حساب أو الدخول
1. افتح **https://github.com**
2. إذا ليس لديك حساب: اضغط **Sign up** وسجّل
3. إذا لديك حساب: اضغط **Sign in**

### الخطوة 2 — إنشاء Repository جديد
1. بعد الدخول، اضغط الزر **+** في أعلى اليمين
2. اختر **"New repository"**
3. أمام **Repository name**: اكتب `risk-management-system`
4. اترك **Public** محددة (مطلوبة لـ GitHub Pages المجانية)
5. **ضع علامة** على **"Add a README file"**
6. اضغط **"Create repository"**

### الخطوة 3 — رفع ملف index.html
1. داخل الـ Repository الجديد، اضغط **"Add file"** → **"Upload files"**
2. اسحب ملف `index.html` إلى منطقة الرفع، أو اضغط **"choose your files"**
3. في خانة **"Commit changes"** اكتب: `Add main site file`
4. اضغط **"Commit changes"** (الزر الأخضر)
5. تحقق: يجب أن ترى `index.html` في الصفحة الرئيسية للـ Repository

---

## الجزء الثاني: تفعيل GitHub Pages

### الخطوة 4 — فتح Settings
1. في صفحة الـ Repository، اضغط **"Settings"** (آخر تبويب في القائمة العلوية)
2. في القائمة الجانبية اليسرى، اضغط **"Pages"**

### الخطوة 5 — إعداد المصدر
في قسم **"Build and deployment"**:

1. تحت **"Source"**: اختر **"Deploy from a branch"**
2. تحت **"Branch"**: اختر **"main"**
3. تحت **"Folder"**: اختر **"/ (root)"**
4. اضغط **"Save"**

### الخطوة 6 — انتظر الرابط
1. الصفحة ستعيد تحميل نفسها
2. انتظر **2-5 دقائق**
3. ارجع إلى **Settings → Pages**
4. سترى رسالة: **"Your site is live at https://USERNAME.github.io/risk-management-system/"**
5. انسخ هذا الرابط — هذا رابط موقعك النهائي

---

## الجزء الثالث: إعداد Firebase (ضروري للمزامنة)

### الخطوة 7 — إضافة دومين GitHub Pages في Firebase
⚠️ هذه الخطوة الأهم — بدونها Firebase سيرفض الاتصال

1. افتح **https://console.firebase.google.com**
2. اختر مشروع: **cash-makhater2-data**
3. من القائمة الجانبية: **Build → Authentication**
4. اضغط تبويب **"Settings"**
5. قسم **"Authorized domains"** → اضغط **"Add domain"**
6. أضف: `USERNAME.github.io` (استبدل USERNAME باسم حسابك)
7. اضغط **"Add"**

### الخطوة 8 — التحقق من Firestore Rules
1. من القائمة: **Build → Firestore Database**
2. اضغط تبويب **"Rules"**
3. تأكد أن القواعد هكذا:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
4. إذا كانت مختلفة، انسخ الكود أعلاه والصقه، ثم اضغط **"Publish"**

### الخطوة 9 — التحقق من Firestore Database
1. من القائمة: **Build → Firestore Database**
2. تأكد أن الحالة **"Active"** (وليس "Suspended")
3. إذا كانت "Suspended"، ابحث عن زر تفعيل أو راجع خطة Firebase المجانية

---

## الجزء الرابع: الاختبار والتحقق

### الخطوة 10 — اختبار الموقع
افتح الرابط: `https://USERNAME.github.io/risk-management-system/`

| الاختبار | ما يجب أن يحدث |
|----------|----------------|
| فتح الرابط | تظهر شاشة تسجيل الدخول |
| أدخل: `Fadicash@2026` | تدخل للموقع |
| الشريط أعلاه | يظهر "Firebase متصل — مزامنة فورية نشطة" |
| البيانات | تظهر 251+ سجل في الجدول |
| البحث | اكتب اسم عميل → تظهر نتائج فورية |

### الخطوة 11 — اختبار المزامنة بين جهازين
1. افتح الموقع على جهازك (كمبيوتر)
2. افتح الموقع على هاتفك (نفس الرابط)
3. على الكمبيوتر: ادخل لوحة التحكم وارفع Excel جديد
4. على الهاتف: يجب أن تظهر السجلات الجديدة خلال 5 ثوانٍ تلقائياً بدون refresh

---

## الجزء الخامس: تحديث الموقع مستقبلاً

### إذا أردت تحديث ملف index.html:
1. افتح الـ Repository على GitHub
2. اضغط على ملف `index.html`
3. اضغط أيقونة القلم (Edit) في أعلى اليمين
4. أو: اضغط **"Add file"** → **"Upload files"** وارفع الملف الجديد
5. اضغط **"Commit changes"**
6. انتظر 1-2 دقيقة → الموقع يتحدث تلقائياً

---

## استكشاف المشاكل

### مشكلة: "Firebase لم يتصل" أو الشريط أحمر
**الحل:** تأكد أنك أضفت `USERNAME.github.io` في Authorized domains (الخطوة 7)

### مشكلة: الصفحة تفتح لكن البيانات فارغة
**الحل:** افتح Console في المتصفح (F12) وانظر للأخطاء. غالباً مشكلة في Firestore Rules.

### مشكلة: 404 عند فتح الرابط
**الحل:** انتظر 5 دقائق إضافية. GitHub Pages يحتاج وقتاً أحياناً.

### مشكلة: "Your site is published" لكن يفتح صفحة README فارغة
**الحل:** تأكد أن `index.html` موجود في الـ root (ليس في مجلد فرعي)

---

## ملخص الروابط المهمة

| الخدمة | الرابط |
|--------|--------|
| Repository | `https://github.com/USERNAME/risk-management-system` |
| الموقع | `https://USERNAME.github.io/risk-management-system/` |
| Firebase Console | `https://console.firebase.google.com/project/cash-makhater2-data` |
| Firestore Data | `https://console.firebase.google.com/project/cash-makhater2-data/firestore` |

---

## ملاحظة حول GitHub Pages و HTTPS

GitHub Pages يوفر HTTPS تلقائياً ومجاناً — لا تحتاج أي إعداد إضافي.
هذا مهم لأن `type="module"` و Firebase يتطلبان HTTPS.

