---
category: general
date: 2026-02-28
description: تعلم كيفية إضافة خاصية مخصصة إلى مصنف Excel باستخدام C# وكتابة مخرجات
  الكونسول بسرعة. يتضمن تحميل مصنف Excel بـ C# والوصول إلى الخصائص المخصصة بـ C#.
draft: false
keywords:
- how to add custom property
- load excel workbook c#
- write console output c#
- access custom properties c#
- get first worksheet c#
language: ar
og_description: كيفية إضافة خاصية مخصصة في Excel باستخدام C# مع شرح مفصل. تحميل المصنف،
  الوصول إلى الخصائص المخصصة، وكتابة مخرجات الكونسول.
og_title: كيفية إضافة خاصية مخصصة في إكسل باستخدام C# – دليل كامل
tags:
- C#
- Excel
- Aspose.Cells
- CustomProperties
title: كيفية إضافة خاصية مخصصة في إكسل باستخدام C# – دليل خطوة بخطوة
url: /ar/net/document-properties/how-to-add-custom-property-in-excel-with-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة خاصية مخصصة في Excel باستخدام C# – دليل خطوة‑بخطوة

هل تساءلت يومًا **كيفية إضافة خاصية مخصصة** إلى ملف Excel باستخدام C#؟ في هذا الدرس سنستعرض تحميل دفتر عمل Excel، الوصول إلى الخصائص المخصصة، وطباعة النتيجة إلى وحدة التحكم. هذا سيناريو شائع عندما تحتاج إلى وضع علامة على ورقة ببيانات وصفية مثل “Department” أو “Budget” دون تعديل البيانات الظاهرة.

ما ستحصل عليه من هذا الدليل هو حل كامل جاهز للنسخ‑واللصق يُظهر لك كيفية **load excel workbook c#**، استرجاع **first worksheet c#**، إضافة وقراءة **custom properties c#**، وأخيرًا **write console output c#**. لا مراجع غامضة للوثائق الخارجية—كل ما تحتاجه موجود هنا، بالإضافة إلى بعض النصائح الاحترافية لتجنب المشكلات الشائعة.

---

## المتطلبات المسبقة

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+).  
- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو مرخصة). إذا كنت تفضّل بديلًا مفتوح المصدر، فإن EPPlus يعمل بصورة مماثلة؛ فقط استبدل مساحة الاسم وأسماء الفئات.  
- بيئة تطوير C# أساسية (Visual Studio، VS Code، Rider—أي منها يناسبك).  
- ملف Excel اسمه `input.xlsx` موجود في مجلد يمكنك الإشارة إليه، مثال: `C:\Data\input.xlsx`.

> **نصيحة احترافية:** عند تثبيت Aspose.Cells عبر NuGet، الحزمة تضيف تلقائيًا توجيه `using Aspose.Cells;` الضروري، لذا لن تحتاج إلى البحث عن ملفات DLL يدويًا.

## الخطوة 1 – تحميل دفتر عمل Excel C# (نقطة البداية)

قبل أن تتمكن من التعامل مع الخصائص المخصصة، تحتاج إلى كائن دفتر العمل في الذاكرة.

```csharp
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

// Define the path to your Excel file
string workbookPath = @"C:\Data\input.xlsx";

// Load the workbook – this is the classic way to load excel workbook c#
Workbook wb = new Workbook(workbookPath);
```

**لماذا هذا مهم:** تحميل دفتر العمل ينشئ كائن `Workbook` كامل المميزات يمنحك الوصول إلى الأوراق، الخلايا، ومجموعة `CustomProperties` المخفية. تخطي هذه الخطوة أو استخدام مسار غير صحيح سيتسبب في رمي استثناء `FileNotFoundException`، لذلك نحدد المسار صراحةً في البداية.

## الخطوة 2 – الحصول على الورقة الأولى C# (حيث يحدث السحر)

معظم جداول البيانات تحتوي على ورقة افتراضية تريد العمل معها. Aspose.Cells يخزن الأوراق في مجموعة ذات فهرس يبدأ من الصفر، لذا الأولى هي الفهرس `0`.

```csharp
// Retrieve the first worksheet – get first worksheet c# is as simple as this
Worksheet worksheet = wb.Worksheets[0];
```

**ما الفائدة؟** باستهداف الورقة الأولى مباشرة، تتجنب التكرار عبر المجموعة عندما تحتاج إلى ورقة واحدة فقط. إذا كان ملفك يحتوي على عدة أوراق وتحتاج إلى ورقة مختلفة، فقط غيّر الفهرس أو استخدم `Worksheets["SheetName"]`.

## الخطوة 3 – إضافة خاصية مخصصة (جوهر كيفية إضافة خاصية مخصصة)

الآن نجيب أخيرًا على السؤال الأساسي: **كيفية إضافة خاصية مخصصة** إلى ورقة عمل.

```csharp
// Add a custom property named "Department" with value "Finance"
worksheet.CustomProperties.Add("Department", "Finance");

// Add a numeric custom property named "Budget" with value 1,250,000
worksheet.CustomProperties.Add("Budget", 1250000);
```

### خلف الكواليس

- `CustomProperties` هي مجموعة تتواجد على كائن `Worksheet`، وليس على دفتر العمل.  
- طريقة `Add` تقبل مفتاحًا من نوع string وقيمة من نوع object، لذا يمكنك تخزين نصوص، أرقام، تواريخ، أو حتى علامات منطقية.  
- Aspose.Cells يحفظ هذه الخصائص تلقائيًا داخل ملف Excel الأساسي عند حفظه لاحقًا.

> **احذر:** إذا حاولت إضافة خاصية باسم مكرر، سيُطلق Aspose استثناء `ArgumentException`. لتحديث خاصية موجودة، استخدم `worksheet.CustomProperties["Budget"].Value = newValue;`.

## الخطوة 4 – استرجاع واستخدام الخاصية المخصصة (Access Custom Properties C#)

قراءة الخاصية مرة أخرى سهلة مثل كتابتها. تُظهر هذه الخطوة **access custom properties c#** وتوضح أيضًا كيفية **write console output c#**.

```csharp
// Retrieve the "Budget" value from the custom properties collection
var budget = worksheet.CustomProperties["Budget"].Value;

// Optional: Cast to the expected type if you need numeric operations
decimal budgetAmount = Convert.ToDecimal(budget);
```

**لماذا التحويل؟** خاصية `Value` تُعيد كائنًا من النوع `object`. تحويله إلى نوع رقمي يتيح لك إجراء حسابات—مثل إضافة الضريبة أو مقارنة الميزانيات—دون تكلفة إضافية للـ boxing/unboxing.

## الخطوة 5 – كتابة ناتج وحدة التحكم C# (رؤية النتيجة)

أخيرًا، نعرض الميزانية المسترجعة في وحدة التحكم. هذا يلبي متطلب **write console output c#**.

```csharp
// Display the budget amount in the console
Console.WriteLine($"Budget: {budgetAmount:C0}");
```

محدد التنسيق `:C0` يطبع الرقم كعملة دون أرقام عشرية، مثال: `Budget: $1,250,000`. يمكنك تعديل سلسلة التنسيق لتتناسب مع إعدادات اللغة لديك.

## الخطوة 6 – حفظ دفتر العمل (حفظ التغييرات)

إذا رغبت في بقاء الخصائص المخصصة بعد انتهاء الجلسة الحالية، يجب حفظ دفتر العمل.

```csharp
// Save the workbook to a new file so you don't overwrite the original
string outputPath = @"C:\Data\output_with_properties.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

**ملاحظة:** رغم أن الخصائص المخصصة مرتبطة بالورقة، إلا أنها تُخزن داخل حزمة `.xlsx`، لذا يزداد حجم الملف بشكل طفيف فقط.

## مثال كامل جاهز للتنفيذ (Copy‑Paste Ready)

فيما يلي البرنامج الكامل الذي يربط جميع الخطوات معًا. الصقه في مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook – how to add custom property starts here
            string workbookPath = @"C:\Data\input.xlsx";
            Workbook wb = new Workbook(workbookPath);

            // 2️⃣ Get the first worksheet – get first worksheet c#
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Add custom properties – this is the core of how to add custom property
            worksheet.CustomProperties.Add("Department", "Finance");
            worksheet.CustomProperties.Add("Budget", 1250000);

            // 4️⃣ Retrieve the budget – access custom properties c#
            var budget = worksheet.CustomProperties["Budget"].Value;
            decimal budgetAmount = Convert.ToDecimal(budget);

            // 5️⃣ Write console output – write console output c#
            Console.WriteLine($"Budget: {budgetAmount:C0}");

            // 6️⃣ Save the workbook so the properties persist
            string outputPath = @"C:\Data\output_with_properties.xlsx";
            wb.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");

            // Keep console window open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Budget: $1,250,000
Workbook saved to C:\Data\output_with_properties.xlsx
Press any key to exit...
```

شغّل البرنامج، افتح `output_with_properties.xlsx` في Excel، ثم انتقل إلى **File → Info → Properties → Advanced Properties → Custom**. ستظهر لك “Department” = “Finance” و “Budget” = 1250000 هناك.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان دفتر العمل محميًا بكلمة مرور؟

Aspose.Cells يتيح لك فتح ملف محمي بتمرير كائن `LoadOptions` يحتوي على كلمة المرور:

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx) { Password = "mySecret" };
Workbook wb = new Workbook(workbookPath, loadOptions);
```

### هل يمكنني إضافة خصائص مخصصة إلى دفتر العمل نفسه بدلاً من ورقة واحدة؟

نعم—استخدم `wb.CustomProperties` بدلاً من `worksheet.CustomProperties`. الـ API هو نفسه، لكن النطاق يتغير من ورقة إلى الملف بأكمله.

### هل يعمل هذا مع ملفات .xls (Excel 97‑2003)؟

بالطبع. Aspose.Cells يُجرد التنسيق، لذا يعمل نفس الكود مع `.xls`، `.xlsx`، `.xlsm`، إلخ. فقط تأكد أن امتداد الملف يتطابق مع التنسيق الفعلي.

### كيف أحذف خاصية مخصصة؟

```csharp
worksheet.CustomProperties.Remove("Department");
```

إزالة الخاصية آمنة؛ إذا لم يكن المفتاح موجودًا، لا يحدث شيء.

## نصائح احترافية ومخاطر

- **تجنب كتابة المسارات صراحةً** في الكود الإنتاجي. استخدم `Path.Combine` وملفات الإعدادات لجعل الأمور أكثر مرونة.  
- **قم بتحرير دفتر العمل** إذا كنت تعالج العديد من الملفات في حلقة. ضعها داخل كتلة `using` أو استدعِ `wb.Dispose()` يدويًا.  
- **احذر من تنسيقات الأرقام الخاصة بالثقافة** عند تحويل قيمة `object`. `Convert.ToDecimal` يراعي ثقافة الخيط الحالي، لذا اضبط `CultureInfo.InvariantCulture` إذا كنت تحتاج إلى تحليل ثابت.  
- **إضافة خصائص دفعة واحدة**: إذا كان لديك عشرات من عناصر البيانات الوصفية، فكر في التكرار عبر قاموس للحفاظ على الكود DRY.

## الخاتمة

لقد غطينا الآن **كيفية إضافة خاصية مخصصة** إلى ورقة Excel باستخدام C#. من تحميل دفتر العمل، الحصول على الورقة الأولى، إضافة وقراءة الخصائص المخصصة، إلى كتابة النتيجة في وحدة التحكم وحفظ الملف—أصبح لديك حل كامل جاهز للنسخ.  

بعد ذلك، قد تستكشف **access custom properties c#** على مستوى دفتر العمل، أو تجرب أنواع بيانات أكثر تعقيدًا مثل التواريخ والبووليات. إذا كنت مهتمًا بأتمتة إنشاء التقارير، اطلع على دليلنا حول **write console output c#** لتسجيل مجموعات بيانات كبيرة، أو غص في سلسلة **load excel workbook c#** لتعامل متقدم مع الأوراق.

لا تتردد في تعديل أسماء الخصائص، إضافة بياناتك الوصفية الخاصة، ودمج هذا النمط في خطوط معالجة بيانات أكبر. برمجة سعيدة، ولتظل جداولك مُعَلَّمَةً بثراء!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}