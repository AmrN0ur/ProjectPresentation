# دليل إضافة عرض تقديمي جديد

هذا الدليل يشرح كيفية إضافة عرض تقديمي جديد إلى منصة DeltaBase ليظهر في الاستضافة على Netlify.

## الخطوات

### 1. إنشاء مجلد العرض الجديد

أنشئ مجلد جديد داخل `presentations/` باسم العرض:

```bash
mkdir presentations/YourProjectName
```

### 2. إنشاء ملفات العرض

داخل المجلد الجديد، أنشئ الملفات التالية:

- `index.html` - الصفحة الرئيسية للعرض التقديمي
- `roadmap.html` (اختياري) - خارطة الطريق/خطة التنفيذ
- `DeltaBase_Logo.png` - شعار المشروع (أو انسخه من مجلد آخر)
- `DeltaBase_Logo.ico` - الأيقونة (أو انسخها)

### 3. تحديث ملف `presentations.json`

أضف العرض الجديد إلى مصفوفة `presentations`:

```json
{
  "presentations": [
    {
      "id": "YourProjectName",
      "title": "عنوان العرض",
      "description": "وصف مختصر للمشروع",
      "thumbnail": "DeltaBase_Logo.png",
      "path": "presentations/YourProjectName/index.html",
      "roadmap": "presentations/YourProjectName/roadmap.html",
      "tags": ["تصنيف1", "تصنيف2", "تصنيف3"],
      "createdAt": "2025-03-30",
      "status": "active"
    }
  ]
}
```

#### شرح الحقول:

| الحقل | الوصف | مثال |
|-------|-------|------|
| `id` | معرف فريد للعرض (يستخدم في الرابط) | `"CanteenSystem"` |
| `title` | العنوان المعروض للمستخدم | `"نظام الكانتين"` |
| `description` | وصف مختصر (1-2 جمل) | `"نظام إدارة..."` |
| `thumbnail` | صورة المصغرة | `"DeltaBase_Logo.png"` |
| `path` | المسار للعرض الرئيسي | `"presentations/.../index.html"` |
| `roadmap` | مسار خارطة الطريق (اختياري) | `"presentations/.../roadmap.html"` أو `null` |
| `tags` | مصفوفة التصنيفات | `["إدارة", "تعليم"]` |
| `createdAt` | تاريخ الإنشاء | `"2025-03-30"` |
| `status` | الحالة: `active` أو `draft` أو `pending` | `"active"` |

## بناء Tailwind CSS للإنتاج

قبل رفع المشروع على Netlify، تأكد من بناء CSS:

```bash
# تثبيت dependencies
npm install

# بناء CSS للإنتاج
npm run build:css
```

هذا سيولد ملف `dist/output.css` المستخدم في الصفحة الرئيسية.

## تحديث `netlify.toml`

أضف قاعدة توجيه للعرض الجديد:

```toml
[[redirects]]
  from = "/YourProjectName"
  to = "/presentations/YourProjectName/index.html"
  status = 200

[[redirects]]
  from = "/YourProjectName/*"
  to = "/presentations/YourProjectName/:splat"
  status = 200
```

**مهم:** أضف هذه القواعد **قبل** قاعدة الـ 404 fallback في نهاية الملف.

### 5. اختبار العرض

بعد رفع الملفات على GitHub ونشرها على Netlify:

1. `/` - يجب أن يظهر العرض في قائمة العروض
2. `/YourProjectName` - يجب أن يذهب مباشرة للعرض
3. روابط "خارطة الطريق" يجب أن تعمل (إذا وجدت)

## هيكل الملفات النهائي

```
ProjectPresentation/
├── index.html                 ← الصفحة الرئيسية
├── presentations.json         ← خريطة العروض
├── netlify.toml              ← توجيهات Netlify
├── presentations/
│   ├── Buildaxis/
│   │   ├── index.html
│   │   └── roadmap.html
│   └── YourProjectName/     ← العرض الجديد
│       ├── index.html
│       ├── roadmap.html
│       ├── DeltaBase_Logo.png
│       └── DeltaBase_Logo.ico
```

## ملاحظات

- رابط العودة للرئيسية في العرض: `href="../../index.html"`
- روابط الصور داخل العرض تكون نسبية: `./DeltaBase_Logo.png`
- لا تضع مسافات في `id`، استخدم CamelCase أو kebab-case
- `status: "draft"` يظهر العرض بشارة "مسودة" صفراء
- `status: "active"` يظهر العرض بشارة "نشط" خضراء
