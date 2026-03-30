# DeltaBase Presentation Platform

منصة DeltaBase لعرض المشاريع البرمجية - منصة استضافة العروض التقديمية للعملاء.

## الاستضافة

المنصة مستضافة على Netlify ومتاحة مباشرة عبر:
- الصفحة الرئيسية: `/`
- العروض المباشرة: `/Buildaxis`, `/CanteenSystem`

## هيكل الملفات

```
ProjectPresentation/
├── index.html              ← الصفحة الرئيسية (Hub)
├── presentations.json      ← خريطة العروض
├── netlify.toml           ← إعدادات توجيه Netlify
├── dist/
│   └── output.css         ← Tailwind CSS المبني (Production)
├── presentations/
│   ├── Buildaxis/
│   │   ├── index.html     ← العرض التقديمي
│   │   └── roadmap.html   ← خارطة الطريق
│   └── CanteenSystem/
│       └── index.html     ← العرض التقديمي
├── DeltaBase_Logo.png     ← الشعار
├── DeltaBase_Logo.ico     ← الأيقونة
└── ADDING_PRESENTATION.md ← دليل إضافة عرض جديد
```

## التقنيات المستخدمة

- HTML5, CSS3, JavaScript (Vanilla)
- Tailwind CSS (مبني للإنتاج)
- Lucide Icons (CDN)
- Google Fonts (Tajawal)

## إعادة بناء CSS (للمطورين)

إذا احتجت تعديل التصميم:

```bash
npm install
npm run build:css
```

## إضافة عرض جديد

راجع `ADDING_PRESENTATION.md` للتفاصيل الكاملة.

---

© 2026 DeltaBase Software
