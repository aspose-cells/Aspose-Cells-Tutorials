---
"date": "2025-04-05"
"description": "تعرّف على كيفية إضافة العلامات المائية وتخصيصها في جداول بيانات Excel باستخدام Aspose.Cells لـ .NET. يغطي هذا الدليل ميزات الإعداد والتنفيذ والأمان."
"title": "كيفية إضافة علامات مائية في Excel باستخدام Aspose.Cells .NET - دليل شامل"
"url": "/ar/net/headers-footers/excel-watermark-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# كيفية إضافة علامات مائية في Excel باستخدام Aspose.Cells .NET

في عالمنا الرقمي اليوم، تُعدّ حماية بياناتك الحساسة أمرًا بالغ الأهمية عند مشاركة مستندات مثل جداول البيانات. إضافة العلامات المائية - وهي إشارة بصرية خفية لكنها قوية - قد تُشير إلى السرية أو الملكية. يُرشدك هذا الدليل الشامل إلى كيفية استخدام Aspose.Cells لـ .NET لإضافة تأثيرات نص العلامة المائية وتخصيصها في جداول بيانات Excel.

## ما سوف تتعلمه
- إعداد Aspose.Cells لـ .NET في بيئة التطوير الخاصة بك.
- إضافة علامة مائية إلى ورقة Excel باستخدام C#.
- تخصيص مظهر العلامات المائية، بما في ذلك إعدادات اللون والشفافية.
- قفل الأشكال داخل Excel لمنع التعديلات غير المصرح بها.
- تطبيقات عملية لتعزيز أمن الوثائق.

دعونا نستكشف كيفية تنفيذ هذه الوظائف في مشاريعك.

## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك:
- **فيجوال ستوديو** تم تثبيته على جهازك (أي إصدار من عام 2017 فصاعدًا).
- المعرفة الأساسية بتطوير C# و.NET.
- فهم عام للتعامل مع ملفات Excel باستخدام واجهات برمجة التطبيقات.

بالإضافة إلى ذلك، قم بتثبيت Aspose.Cells لـ .NET عبر وحدة تحكم إدارة الحزم NuGet أو .NET CLI:

**مدير الحزم NuGet**
```bash
PM> Install-Package Aspose.Cells
```

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

### الحصول على الترخيص
لاستخدام Aspose.Cells لـ .NET، يمكنك البدء برخصة تجريبية مجانية لاستكشاف إمكانياتها:
1. **نسخة تجريبية مجانية:** قم بزيارة [صفحة ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/) وطلب ترخيص مؤقت.
2. **شراء:** للاستخدام طويل الأمد، قم بشراء ترخيص من خلال [صفحة شراء Aspose](https://purchase.aspose.com/buy).

### الإعداد الأساسي
بمجرد حصولك على Aspose.Cells عبر NuGet أو CLI، قم بتهيئته في مشروع C# الخاص بك:
```csharp
using Aspose.Cells;
```

## إعداد Aspose.Cells لـ .NET
فيما يلي نظرة عامة موجزة حول إعداد Aspose.Cells وتكوينه:
1. **ثَبَّتَ** Aspose.Cells باستخدام Package Manager Console أو .NET CLI كما هو موضح أعلاه.
2. **تهيئة:** ابدأ بإنشاء `Workbook` كائن يمثل ملف Excel.

```csharp
Workbook workbook = new Workbook();
```
3. **تطبيق الترخيص:** إذا كان لديك ترخيص، قم بتطبيقه لفتح الميزات الكاملة.

## دليل التنفيذ

### الميزة 1: إضافة علامة مائية إلى ورقة Excel
#### ملخص
تتضمن إضافة العلامة المائية إنشاء تأثيرات نصية تتراكب على بياناتك بشكل دقيق، مما يشير إلى حالة المستند مثل "سري".

#### التنفيذ خطوة بخطوة
##### إنشاء مصنف وورقة عمل
```csharp
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

##### إضافة تأثير النص كعلامة مائية
قم بإنشاء شكل تأثير النص باستخدام سمات محددة مثل نمط الخط والحجم والموضع والمظهر.

```csharp
Shape wordart = sheet.Shapes.AddTextEffect(
    MsoPresetTextEffect.TextEffect1,
    "CONFIDENTIAL", 
    "Arial Black",
    50,   // حجم الخط
    false, // هل هو مائل؟
    true, // جريئة
    18,   // الوضع الأيسر
    8,    // المركز الأول
    1,    // عرض
    1,    // ارتفاع
    130,  // زاوية الدوران
    800   // عامل المقياس
);
```

##### تخصيص المظهر
اضبط لون التدرج والشفافية للحصول على مظهر أنيق.
```csharp
FillFormat wordArtFormat = wordart.Fill;
wordArtFormat.SetOneColorGradient(Color.Red, 0.2, GradientStyleType.Horizontal, 2); 
wordArtFormat.Transparency = 0.9; // اجعلها شفافة قليلا

wordart.HasLine = false; // قم بإزالة خط الحدود للحصول على مظهر أنظف
```

##### احفظ مصنفك
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

### الميزة 2: قفل جوانب الشكل في ورقة Excel
#### ملخص
يمنع قفل الأشكال المستخدمين غير المصرح لهم من تغيير العلامة المائية أو الأشكال الأخرى، مما يضمن سلامة المستند.

#### التنفيذ خطوة بخطوة
##### قفل خصائص مختلفة للعلامة المائية
قم بتأمين العلامة المائية الخاصة بك عن طريق قفل جوانبها.
```csharp
wordart.IsLocked = true;
wordart.SetLockedProperty(ShapeLockType.Selection, true);
wordart.SetLockedProperty(ShapeLockType.ShapeType, true);
wordart.SetLockedProperty(ShapeLockType.Move, true);
wordart.SetLockedProperty(ShapeLockType.Resize, true);
wordart.SetLockedProperty(ShapeLockType.Text, true);
```

##### حفظ التغييرات
تأكد من حفظ التغييرات في المصنف الخاص بك.
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

## التطبيقات العملية
1. **التقارير السرية:** استخدم العلامات المائية للتقارير الداخلية التي تحتوي على معلومات حساسة.
2. **إشعارات حقوق النشر:** تضمين إشعارات حقوق الطبع والنشر في القوالب الموزعة على العملاء.
3. **التحكم في الإصدار:** قم بالإشارة إلى المسودة أو الإصدارات النهائية للمستندات باستخدام نص العلامة المائية ذي الصلة.

## اعتبارات الأداء
- **تحسين الموارد:** قم بتقليل استخدام الموارد عن طريق تحميل أوراق العمل والأشكال الضرورية فقط.
- **إدارة الذاكرة:** التخلص من الأشياء بطريقة سليمة باستخدام `Dispose()` الأساليب حيثما ينطبق ذلك، لضمان إدارة فعالة للذاكرة في تطبيقات .NET.

## خاتمة
بإتقان استخدام Aspose.Cells لـ .NET لإضافة علامات مائية وقفل الأشكال في جداول بيانات Excel، ستعزز أمان مستنداتك وتنقل المعلومات المهمة بسرعة. يزودك هذا الدليل بالمهارات اللازمة لتطبيق هذه الميزات بفعالية.

### الخطوات التالية
استكشف المزيد من خيارات التخصيص في [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) أو حاول دمج هذه الوظائف في أنظمة أكبر تتطلب إدارة مستندات قوية.

## قسم الأسئلة الشائعة
1. **كيف يمكنني تغيير نص العلامة المائية؟**
   - تعديل المعلمة الثانية لـ `AddTextEffect()` الطريقة مع النص المطلوب.
2. **هل يمكنني استخدام خطوط مختلفة للعلامة المائية الخاصة بي؟**
   - نعم، قم بتحديد أي خط عن طريق تغيير المعلمة الثالثة في `AddTextEffect()`.
3. **ماذا لو كان ملف Excel الخاص بي كبيرًا وكان التحميل بطيئًا؟**
   - فكر في تحسين الكود الخاص بك لتحميل الأجزاء الضرورية فقط من المصنف أو استخدام خيارات ضبط الأداء المتوفرة في Aspose.Cells.
4. **هل من الممكن إزالة العلامة المائية لاحقًا؟**
   - نعم، يمكنك حذف الأشكال من مجموعة أوراق العمل التي توجد بها.
5. **كيف يمكنني تطبيق هذا الحل في المعالجة الدفعية؟**
   - كرر العمل على عدة مصنفات، مع تطبيق منطق مماثل داخل الحلقات أو المهام غير المتزامنة لتحقيق الكفاءة.

## موارد
- [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/)
- [تنزيل Aspose.Cells](https://releases.aspose.com/cells/net/)
- [شراء ترخيص](https://purchase.aspose.com/buy)
- [احصل على نسخة تجريبية مجانية](https://releases.aspose.com/cells/net/)
- [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)

الآن بعد أن أصبحت لديك المعرفة، فقد حان الوقت لتطبيق هذه التقنيات عمليًا وتأمين مستندات Excel الخاصة بك بشكل فعال!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}