---
category: general
date: 2026-02-14
description: تعلم كيفية حفظ ملف XLSB، إضافة خاصية مخصصة، وفتح ملف XLSB باستخدام C#.
  يوضح المثال الكامل إنشاء وتحديث الخصائص المخصصة في ورقة العمل.
draft: false
keywords:
- how to save xlsb
- add custom property
- open xlsb file
- create custom property
- how to add property
language: ar
og_description: كيفية حفظ ملف XLSB بعد إضافة خاصية مخصصة في C#. يوضح هذا الدليل خطوات
  فتح ملف XLSB، وإنشاء خاصية مخصصة، وحفظ المصنف.
og_title: كيفية حفظ ملف XLSB مع خاصية مخصصة – دليل C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية حفظ ملف XLSB مع خاصية مخصصة – دليل C# خطوة بخطوة
url: /ar/net/document-properties/how-to-save-xlsb-with-a-custom-property-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ XLSB مع خاصية مخصصة – دليل C# كامل

هل تساءلت يومًا **كيف تحفظ ملف XLSB** بعد إرفاق قطعة من البيانات الوصفية بالورقة؟ ربما تقوم بإنشاء لوحة تحكم مالية وتحتاج إلى وضع علامة على كل ورقة عمل بقسمها، أو ربما تريد ببساطة تضمين معلومات إضافية ليست جزءًا من بيانات الخلايا. باختصار، تحتاج إلى **فتح ملف XLSB**، **إنشاء خاصية مخصصة**، ثم **حفظ المصنف** دون كسر التنسيق الثنائي.

هذا بالضبط ما سنقوم به في هذا الدليل. في النهاية، ستحصل على مقتطف قابل للتنفيذ يفتح مصنف *.xlsb* موجود، يضيف (أو يحدث) خاصية مخصصة تسمى *Department*، ويكتب التغييرات إلى ملف جديد. لا حاجة لأي وثائق خارجية—فقط C# عادي ومكتبة Aspose.Cells (أو أي API متوافق تفضله).

## المتطلبات المسبقة

- **.NET 6+** (أو .NET Framework 4.7.2 وما بعده) – الكود يعمل على أي بيئة تشغيل حديثة.  
- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو نسخة مرخصة). إذا كنت تستخدم مكتبة أخرى، قد تختلف أسماء الطرق لكن سير العمل يبقى نفسه.  
- ملف **input.xlsb** موجود في مجلد يمكنك الإشارة إليه، مثال: `C:\Data\input.xlsb`.  
- معرفة أساسية بـ C#—إذا كتبت `Console.WriteLine` من قبل، فأنت جاهز.

> **نصيحة احترافية:** احتفظ بملفات المصنف خارج مجلد *bin* الخاص بالمشروع لتجنب أخطاء “الملف مقفل” أثناء التطوير.

الآن، لنبدأ بالخطوات الفعلية.

## الخطوة 1: فتح مصنف XLSB الموجود

أول شيء يجب القيام به هو تحميل المصنف الثنائي إلى الذاكرة. مع Aspose.Cells هذا سطر واحد، لكن يجدر شرح لماذا نستخدم المُنشئ الذي يأخذ مسار الملف.

```csharp
using Aspose.Cells;

try
{
    // Step 1: Open the existing XLSB workbook
    Workbook workbook = new Workbook(@"C:\Data\input.xlsb");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to open XLSB file: {ex.Message}");
    return;
}
```

**لماذا هذا مهم:**  
- فئة `Workbook` تكتشف تنسيق الملف تلقائيًا من الامتداد، لذا لا تحتاج لتحديد *XLSB* صراحة.  
- تغليف الاستدعاء داخل `try/catch` يحميك من الملفات التالفة أو نقص الأذونات—وهي مشاكل شائعة عند **فتح ملف XLSB** في بيئة الإنتاج.

## الخطوة 2: الحصول على ورقة العمل المستهدفة

معظم السيناريوهات الواقعية تتعامل مع الورقة الأولى فقط، لكن يمكنك تعديل الفهرس (`Worksheets[0]`) لأي ورقة تحتاجها. إليك الكود مع فحص أمان سريع.

```csharp
// Step 2: Get the first worksheet in the workbook
Worksheet worksheet = workbook.Worksheets.Count > 0 ? workbook.Worksheets[0] : null;

if (worksheet == null)
{
    Console.Error.WriteLine("The workbook contains no worksheets.");
    return;
}
```

**شرح:**  
- `workbook.Worksheets.Count` يضمن عدم محاولة الوصول إلى فهرس غير موجود، مما سيتسبب في رفع استثناء `ArgumentOutOfRangeException`.  
- في المشاريع الكبيرة قد تسترجع ورقة بالاسم (`Worksheets["Report"]`)—يمكنك استبدال ذلك إذا كنت *تنشئ خاصية مخصصة* على تبويب محدد.

## الخطوة 3: إضافة أو تحديث خاصية مخصصة على ورقة العمل

الخصائص المخصصة هي أزواج مفتاح/قيمة تُخزن جنبًا إلى جنب مع ورقة العمل. إنها مثالية للبيانات الوصفية مثل “Department”، “Author”، أو “Revision”. الـ API يتعامل مع مجموعة `CustomProperties` كقائمة قاموس.

```csharp
// Step 3: Add or update a custom property on the worksheet
// "Department" is the property name; "Finance" is the value.
worksheet.CustomProperties["Department"] = "Finance";
```

**ما الذي يحدث خلف الكواليس؟**  
- إذا كانت الخاصية **موجودة بالفعل**، فإن الفهرس يستبدل قيمتها—هذا هو الجزء المتعلق بـ “كيفية إضافة خاصية” الذي يسأل عنه الكثير من المطورين.  
- إذا لم تكن موجودة، فإن المجموعة تنشئها تلقائيًا. لا حاجة لاستدعاء `Add` إضافي، مما يبقي الكود مختصرًا.

### الحالات الخاصة والبدائل

| الحالة | النهج الموصى به |
|-----------|----------------------|
| **خصائص متعددة** | كرر عبر قاموس من أزواج المفتاح/القيمة وعيّن كل واحدة. |
| **قيم غير نصية** | استخدم `CustomProperties.Add(string name, object value)` لتخزين أرقام أو تواريخ أو قيم منطقية. |
| **الخاصية موجودة وتحتاج للحفاظ على القيمة القديمة** | اقرأ القيمة الحالية أولًا: `var old = worksheet.CustomProperties["Department"];` ثم قرر ما إذا كنت ستستبدلها. |
| **مصنفات كبيرة** | فكر في استدعاء `workbook.BeginUpdate();` قبل التعديلات و`workbook.EndUpdate();` بعد ذلك لتحسين الأداء. |

## الخطوة 4: حفظ المصنف المعدل إلى ملف جديد

الآن بعد أن أصبحت الخاصية موجودة، ستحتاج إلى **حفظ XLSB** دون فقد أي صيغ أو مخططات أو كود VBA موجود. طريقة `Save` تأخذ مسار الهدف و`SaveFormat` اختياريًا.

```csharp
// Step 4: Save the modified workbook to a new file
string outputPath = @"C:\Data\output.xlsb";
workbook.Save(outputPath, SaveFormat.Xlsb);

Console.WriteLine($"Workbook saved successfully to {outputPath}");
```

**لماذا نستخدم `SaveFormat.Xlsb` صراحةً؟**  
- يضمن التنسيق الثنائي حتى لو كان امتداد الملف مكتوبًا بشكل خاطئ.  
- بعض الـ APIs تستنتج التنسيق من الامتداد، لكن الصراحة تجنب الأخطاء الدقيقة عندما تقوم بإعادة تسمية الملف لاحقًا.

### التحقق من النتيجة

بعد التنفيذ، افتح `output.xlsb` في Excel واتبع الخطوات:

1. انقر بزر الفأرة الأيمن على تبويب الورقة → **View Code** → **Properties** (أو استخدم *File → Info → Show All Properties*).  
2. ابحث عن “Department = Finance”.

إذا رأيت ذلك، فقد نجحت في **إضافة خاصية مخصصة** و**حفظ XLSB**.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى مشروع Console، عدل مسارات الملفات، واضغط **F5**.

```csharp
// FullExample.cs
using System;
using Aspose.Cells;

namespace XlsbCustomPropertyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputPath = @"C:\Data\input.xlsb";
            string outputPath = @"C:\Data\output.xlsb";

            // 1️⃣ Open the existing XLSB workbook
            Workbook workbook;
            try
            {
                workbook = new Workbook(inputPath);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Unable to open file: {ex.Message}");
                return;
            }

            // 2️⃣ Get the first worksheet (or change the index/name as needed)
            if (workbook.Worksheets.Count == 0)
            {
                Console.Error.WriteLine("❌ No worksheets found in the workbook.");
                return;
            }
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Add or update the custom property "Department"
            //    This demonstrates how to add property if missing or update it if present.
            sheet.CustomProperties["Department"] = "Finance";

            // 4️⃣ Save the workbook as a new XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Save failed: {ex.Message}");
            }
        }
    }
}
```

**مخرجات وحدة التحكم المتوقعة**

```
✅ Workbook saved to C:\Data\output.xlsb
```

افتح الملف الناتج في Excel وسترى خاصية *Department* المخصصة مرفقة بالورقة الأولى.

---

## أسئلة شائعة وإجابات

**س: هل يعمل هذا مع إصدارات Excel القديمة (2007‑2010)؟**  
ج: بالتأكيد. تم تقديم تنسيق XLSB في Excel 2007، وتحتفظ Aspose.Cells بالتوافق مع الإصدارات السابقة. فقط تأكد من أن الجهاز المستهدف يحتوي على البيئة اللازمة (مكتبة .NET تتعامل مع التنسيق داخليًا).

**س: ماذا لو أردت إضافة خاصية إلى *المصنف* بدلاً من ورقة واحدة؟**  
ج: استخدم `workbook.CustomProperties["Project"] = "Alpha";`. نفس منطق الفهرس ينطبق، لكن النطاق يتغير من ورقة عمل إلى المصنف بأكمله.

**س: هل يمكنني تخزين تاريخ كخاصية مخصصة؟**  
ج: نعم. مرّر كائن `DateTime`: `worksheet.CustomProperties["ReviewDate"] = DateTime.Today;`. سيعرض Excel التاريخ بصيغة ISO.

**س: كيف أقرأ خاصية مخصصة لاحقًا؟**  
ج: استرجعها بنفس الطريقة: `var dept = worksheet.CustomProperties["Department"];`.

---

## نصائح لكتابة كود جاهز للإنتاج

- **تحرير الموارد**: ضع `Workbook` داخل كتلة `using` إذا كنت تستخدم .NET 5+ لتحرير الموارد الأصلية بسرعة.  
- **تحديثات مجمعة**: استدعِ `workbook.BeginUpdate();` قبل حلقة إضافة العديد من الخصائص، ثم `workbook.EndUpdate();` بعد ذلك—هذا يقلل من استهلاك الذاكرة.  
- **تسجيل الأخطاء**: بدلاً من `Console.Error`، استخدم إطار تسجيل (Serilog, NLog) لتشخيص أفضل.  
- **التحقق من المدخلات**: تأكد من أن اسم الخاصية غير فارغ ولا يحتوي على أحرف غير مسموح بها (`/ \ ? *`).  
- **سلامة الخيوط**: كائنات Aspose.Cells غير آمنة للاستخدام المتعدد الخيوط؛ تجنّب مشاركة نسخة `Workbook` بين الخيوط.

---

## الخلاصة

أنت الآن تعرف **كيفية حفظ XLSB** بعد **إضافة خاصية مخصصة** إلى ورقة عمل، ورأيت سير العمل الكامل في C#—من **فتح ملف XLSB** إلى **إنشاء خاصية مخصصة** وأخيرًا **حفظ** المستند المحدث. هذا النمط قابل لإعادة الاستخدام لتوسيم التقارير، تضمين سجلات تدقيق، أو ببساطة إغناء ملفات Excel بسياق إضافي.

هل أنت مستعد للتحدي التالي؟ جرّب تعداد جميع الخصائص المخصصة الموجودة، أو صدّرها إلى ملف JSON للمعالجة اللاحقة. يمكنك أيضًا استكشاف **كيفية إضافة خاصية** إلى كائنات المخططات أو جداول المحور—هذه خطوات قليلة فقط.

إذا وجدت هذا الدرس مفيدًا، اضغط إعجاب، شاركه مع زملائك، أو اترك تعليقًا أدناه بحالتك الخاصة. برمجة سعيدة، ولتظل جداول البيانات لديك دائمًا موثقة جيدًا!  

![Diagram showing the flow of opening an XLSB file, adding a custom property, and saving the workbook – how to save xlsb](https://example.com/images/save-xlsb-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}