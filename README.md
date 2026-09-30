# HYperRegedit / 3105

هذا هو المشروع الكامل المرسل في أرشيف MediaFire، ويحتوي على مشروع Xcode والشاشات والخدمات والأصول وملفات الـpatch ووحدات العمل الأصلية.

## البنية

- `ThreeOneOSFive/views`: واجهات التطبيق ونظام التصميم.
- `ThreeOneOSFive/helpers`: الخدمات الداخلية مثل إدارة الملفات والمشاريع والتنظيف والتخزين والأرشفة وإدارة التفعيل.
- `ThreeOneOSFive/Assets.xcassets`: الأيقونات والصور.
- `ThreeOneOSFive/Patches`: حزم patch المضمنة.
- `ThreeOneOSFive/exploit` و`ThreeOneOSFive/kexploit`: ملفات الدعم الأصلية كما وردت في المصدر.
- `ThreeOneOSFive.xcodeproj`: مشروع Xcode.
- `build_unsigned.sh`: بناء IPA غير موقع على macOS باستخدام Xcode.

## التفعيل وSDK

يستخدم المشروع الآن M3SB APON SDK v1.1.0 للتحقق من الترخيص عبر Signature v3. تُرسل معلومات dylib إلى API كي يطبق الخادم سياسة الحزمة. لا يمكن تطبيق patch إلا إذا أعاد الخادم `allow_inject: true`؛ وتظل الاستعادة متاحة. لم يعد هناك مفتاح تفعيل محلي ثابت.

لأسباب أمنية، لا تُحفظ بيانات API داخل هذا المستودع. قبل البناء، مرّر `APON_PACKAGE_TOKEN` و`APON_HMAC_SECRET` كمتغيرات بيئة خاصة، أو أضفهما إلى GitHub Actions Secrets. التفاصيل في [API_INTEGRATION.md](API_INTEGRATION.md).

## البناء

يتطلب البناء macOS وXcode. بعد إعداد متغيرات البيئة الخاصة، شغّل:

```bash
./build_unsigned.sh
```

أو استخدم GitHub Actions مع المستودعات السرية المعرفة. يجب توقيع IPA بالطريقة المصرح بها قبل تثبيته.
