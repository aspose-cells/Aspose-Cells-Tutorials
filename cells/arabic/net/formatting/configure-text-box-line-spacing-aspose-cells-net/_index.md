---
"date": "2025-04-05"
"description": "تعرّف على كيفية ضبط تباعد الأسطر في مربعات النص في Excel باستخدام Aspose.Cells .NET. يتناول هذا الدليل إعداد النص وتنسيقه وحفظ التغييرات."
"title": "تكوين تباعد أسطر مربع النص في Excel باستخدام Aspose.Cells .NET - دليل خطوة بخطوة"
"url": "/ar/net/formatting/configure-text-box-line-spacing-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# تكوين تباعد أسطر مربع النص باستخدام Aspose.Cells .NET: دليل خطوة بخطوة

## مقدمة
عند العمل مع جداول بيانات Excel برمجيًا، يعد تحسين قابلية القراءة من خلال تنسيق النص المخصص أمرًا بالغ الأهمية. **Aspose.Cells لـ .NET** يتيح للمطورين إنشاء ملفات Excel ومعالجتها بسهولة. يرشدك هذا البرنامج التعليمي إلى كيفية ضبط تباعد الأسطر في مربع نص ضمن ورقة عمل Excel باستخدام Aspose.Cells لـ .NET. سواءً كنت تُنشئ تقارير أو تُؤتمت إنشاء المستندات، فإن هذه التقنيات تُحسّن بشكل كبير من جمالية جدول بياناتك.

**ما سوف تتعلمه:**
- إنشاء مصنف جديد والوصول إلى أوراق العمل الخاصة به.
- إضافة شكل مربع نص إلى ورقة العمل.
- تعيين وتنسيق النص داخل الشكل، بما في ذلك تعديلات المسافة بين الأسطر.
- حفظ التعديلات بتنسيق Excel.

## المتطلبات الأساسية

### المكتبات المطلوبة
تأكد من تثبيت Aspose.Cells لـ .NET. ستحتاج أيضًا إلى بيئة تطوير مناسبة لتشغيل أكواد C#.

### إعداد البيئة
- **بيئة التطوير**:Visual Studio أو أي IDE مفضل يدعم .NET.
- **إصدار Aspose.Cells**:تأكد من حصولك على أحدث إصدار من Aspose.Cells لـ .NET.

### متطلبات المعرفة
الإلمام بأساسيات برمجة C# وعمليات Excel مفيد، ولكنه ليس إلزاميًا. يرشد هذا البرنامج التعليمي المبتدئين خلال كل خطوة.

## إعداد Aspose.Cells لـ .NET
لبدء استخدام Aspose.Cells، قم بتثبيته في مشروعك على النحو التالي:

### خيارات التثبيت

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**مدير الحزم**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### الحصول على الترخيص
ابدأ بـ **رخصة تجريبية مجانية** لاستكشاف كامل إمكانيات Aspose.Cells لـ .NET. للاستخدام طويل الأمد، يُنصح بشراء ترخيص أو الحصول على ترخيص مؤقت.

#### التهيئة والإعداد الأساسي
بمجرد التثبيت، قم بتهيئة المصنف الخاص بك والوصول إلى مكوناته كما هو موضح في مقتطفات التعليمات البرمجية الموجودة في هذا البرنامج التعليمي.

## دليل التنفيذ
دعونا نقسم التنفيذ إلى أقسام واضحة استنادًا إلى الوظيفة.

### إنشاء مصنف والوصول إليه
**ملخص**ابدأ بإنشاء مصنف Excel والوصول إلى ورقة العمل الأولى فيه. ستكون هذه الورقة بمثابة لوحة عمل لعملياتنا اللاحقة.

#### الخطوة 1: تهيئة المصنف
```csharp
using Aspose.Cells;

string SourceDir = "YOUR_SOURCE_DIRECTORY";

Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];
```
هنا، نقوم بتهيئة `Workbook` الكائن والوصول إلى ورقة العمل الأولى الخاصة به باستخدام `ws = wb.Worksheets[0]`.

### إضافة مربع نص إلى ورقة العمل
**ملخص**:قم بتعزيز ورقة العمل الخاصة بك عن طريق إضافة شكل مربع نص.

#### الخطوة 2: إضافة شكل مربع النص
```csharp
using Aspose.Cells.Drawing;

Shape shape = ws.Shapes.AddTextBox(2, 0, 2, 0, 100, 200);
```
نضيف `TextBox` إلى ورقة العمل عند الأبعاد المحددة (x، y، العرض، الارتفاع).

### تعيين النص في الشكل
**ملخص**:قم بملء مربع النص الخاص بك بالمحتوى والوصول إلى الفقرات للتنسيق.

#### الخطوة 3: تحديد محتوى النص
```csharp
shape.Text = "Sign up for your free phone number.\nCall and text online for free.";
TextParagraph p = shape.TextBody.TextParagraphs[1];
```
تحدد هذه القطعة النصية النص في الشكل وتحدد فقرة لمزيد من التخصيص.

### تكوين تباعد أسطر الفقرات
**ملخص**:اضبط مسافة السطور والمسافة قبل وبعد مربع النص الخاص بك لتحسين قابلية القراءة.

#### الخطوة 4: تعيين تباعد الأسطر
```csharp
using Aspose.Cells.Drawing.Texts;

p.LineSpaceSizeType = LineSpaceSizeType.Points; // استخدم النقاط للتحكم الدقيق
p.LineSpace = 20; // مسافة السطور 20 نقطة

// تكوين المسافة بعد الفقرة
p.SpaceAfterSizeType = LineSpaceSizeType.Points;
p.SpaceAfter = 10;

// تكوين المسافة قبل الفقرة
p.SpaceBeforeSizeType = LineSpaceSizeType.Points;
p.SpaceBefore = 10;
```
تعمل هذه الإعدادات على ضبط مظهر النص الخاص بك، مما يعزز قابلية قراءته.

### حفظ المصنف
**ملخص**:بمجرد تكوينه، احفظ المصنف الخاص بك للحفاظ على التغييرات.

#### الخطوة 5: حفظ التغييرات
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY";
wb.Save(outputDir + "/outputSetTextboxOrShapeParagraphLineSpacing.xlsx", SaveFormat.Xlsx);
```
يكتب هذا الأمر المصنف المعدل مرة أخرى إلى ملف Excel بتنسيق XLSX.

## التطبيقات العملية
- **إنشاء التقارير تلقائيًا**:تخصيص عروض مربع النص للتقارير الديناميكية.
- **إنشاء القالب**:قم بتطوير قوالب ذات أنماط وتنسيقات محددة مسبقًا باستخدام Aspose.Cells.
- **تحسين عرض البيانات**:تحسين قابلية قراءة البيانات عن طريق تنسيق مربعات النص داخل لوحات المعلومات أو الملخصات.

تتضمن إمكانيات التكامل الجمع بين Aspose.Cells وأنظمة CRM لأتمتة إنشاء المستندات استنادًا إلى تفاعلات العملاء.

## اعتبارات الأداء
- **تحسين استخدام الموارد**:تقليل حجم الذاكرة عن طريق إدارة كائنات المصنف بكفاءة.
- **المعالجة غير المتزامنة**:تنفيذ عمليات غير متزامنة للتعامل مع مجموعات البيانات الكبيرة دون حظر الخيط الرئيسي.
- **أفضل الممارسات**:قم بتحديث المكتبات بانتظام واتبع أفضل ممارسات .NET لضمان الأداء الأمثل مع Aspose.Cells.

## خاتمة
باتباع هذا الدليل، ستتعلم كيفية التعامل مع ملفات Excel باستخدام Aspose.Cells لـ .NET بكفاءة. يمكنك الآن إنشاء مصنفات، وإضافة مربعات نص منسقة، وضبط تباعد الأسطر، وحفظ مستنداتك بتنسيق احترافي. لمزيد من التطوير، استكشف المزيد من ميزات مكتبة Aspose.Cells وجرّب إعدادات مختلفة.

يمكن أن تشمل الخطوات التالية دمج هذه التقنيات في سير عمل معالجة البيانات الأكبر أو استكشاف مكتبات Aspose الأخرى للحصول على حلول شاملة لإدارة المستندات.

## قسم الأسئلة الشائعة
1. **كيف أقوم بتثبيت Aspose.Cells؟**
   - استخدم NuGet Package Manager أو .NET CLI كما هو موضح في قسم الإعداد.
   
2. **هل يمكنني استخدام نسخة تجريبية مجانية من Aspose.Cells؟**
   - نعم، يمكنك البدء بفترة تجريبية مجانية لتقييم إمكانياته.

3. **ما هي أنواع المستندات التي يمكنني التعامل معها باستخدام Aspose.Cells؟**
   - ملفات Excel في المقام الأول (.xlsx)، لكنها تدعم تنسيقات متعددة للتحويل والمعالجة.

4. **هل هناك دعم لـ .NET Core أو .NET Framework؟**
   - يعد Aspose.Cells متوافقًا مع مشاريع .NET Core و.NET Framework.

5. **كيف أقوم بتنسيق النص داخل الشكل؟**
   - الوصول إلى `TextBody` خاصية الشكل لتعديل خصائص النص مثل تباعد الأسطر، كما هو موضح في هذا البرنامج التعليمي.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}