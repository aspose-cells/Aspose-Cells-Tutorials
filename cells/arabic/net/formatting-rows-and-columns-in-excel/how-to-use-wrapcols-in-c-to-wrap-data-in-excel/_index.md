---
category: general
date: 2026-11-19
description: كيفية استخدام wrapcols في C# لتغليف البيانات في Excel وحساب صيغ Excel
  بسرعة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: ar
lastmod: 2026-11-19
og_description: كيفية استخدام wrapcols في C# لتغليف البيانات في Excel. تعلم حساب صيغ
  Excel وحفظ المصنف برمجياً.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: كيفية استخدام wrapcols في C# – تغليف البيانات في Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: كيفية استخدام wrapcols في C# لتغليف البيانات في Excel
url: /ar/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام wrapcols في C# لتغليف البيانات في Excel

إذا كنت بحاجة إلى **how to use wrapcols** لإعادة تنظيم قائمة عمودية إلى أعمدة متعددة، يوضح لك هذا الدليل الخطوات الدقيقة. ستتعلم أيضًا كيفية **calculate Excel formulas** بحيث يتم تخزين النتيجة في الملف الذي تحفظه.

العمل مع Excel من C# غالبًا ما يبدأ بتحميل مصنف، تطبيق الصيغ، وأخيرًا حفظ التغييرات. يغطي هذا البرنامج التعليمي جميع هذه المراحل مع الحفاظ على سهولة نسخ‑لصق الكود في مشروعك الخاص.

## ما ستحققه

* تحميل ملف `.xlsx` موجود من القرص (**load excel workbook c#**).
* تطبيق دالة `WRAPCOLS` على نطاق، مما يؤدي إلى **wrap data in Excel**.
* إجبار المحرك على تقييم الصيغة (**calculate Excel formulas**).
* حفظ المصنف المعدل (**save Excel file c#**).

المتطلب الوحيد هو وجود إشارة إلى **Aspose.Cells for .NET** (أو أي مكتبة تدعم دالة `WRAPCOLS`). يعمل الكود مع .NET 6+ و Visual Studio 2022، لكن أي بيئة تطوير C# ستفي بالغرض.

## كيفية استخدام wrapcols مع Aspose.Cells

دالة ورقة العمل `WRAPCOLS` تأخذ نطاقًا أحادي البعد وتعيد مصفوفة ثنائية البعد تملأ عدد الأعمدة المحدد. تقوم Aspose.Cells بتقييم الدالة كما يفعل Excel، لذا يمكنك استخدامها مباشرةً في صيغة الخلية.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### لماذا كل سطر مهم

* **Loading the workbook** يمنحك نموذج كائن حي يعكس ملف Excel على القرص.  
* **Assigning the formula** إلى `A1` يخبر Excel (أو Aspose.Cells) بمعاملة النطاق كمصفوفة ديناميكية.  
* `CalculateFormula()` يُطلق محرك الحساب؛ بدونها ستبقى الصيغة غير مُقيمة حتى يتم فتح الملف في Excel.  
* **Saving** يكتب القيم المحسوبة مرة أخرى إلى ملف جديد، مما يجعل البيانات المغلفة مرئية لأي شخص يفتح المصنف.

## حساب صيغ Excel برمجياً

استدعاء `Workbook.CalculateFormula()` هو الطريقة الموصى بها لـ **calculate Excel formulas** عندما تحتاج إلى النتائج فورًا. تحترم الطريقة جميع الدوال المدمجة، الدوال المعرّفة من قبل المستخدم، وأي مراجع خارجية تم حلها بالفعل.

إذا كان لديك عدة أوراق عمل تعتمد على بعضها البعض، يمكنك أيضًا تمرير كائن `CalculationOptions` للتحكم في حدود التكرار أو تمكين الحساب متعدد الخيوط:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

هذه الخطوة الإضافية اختيارية لمثال `WRAPCOLS` البسيط، لكنها تصبح أساسية في المصنفات الكبيرة حيث الأداء مهم.

## حفظ ملف Excel C# بعد تغليف البيانات

النداء إلى `Workbook.Save()` يكتب المصنف بالكامل، بما في ذلك المصفوفة التي تم إنشاؤها حديثًا بواسطة `WRAPCOLS`. يمكنك اختيار أي من الصيغ المدعومة (`.xlsx`, `.xls`, `.csv`, إلخ):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

خطوة **save Excel file c#** تضمن بقاء البيانات المغلفة، لذا في المرة التالية التي يفتح فيها شخص ما الملف سيظهر جدولًا ثابتًا بدلاً من صيغة.

## تحميل مصنف Excel C# وتحضير ورقة العمل

إذا لم يحتوي ملف المصدر الخاص بك بالفعل على البيانات التي تريد تغليفها، يمكنك إنشاؤه مباشرةً:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

يظهر هذا المقتطف **load excel workbook c#** بمعنى أنه يمكنك البدء من مصنف فارغ، ملؤه، ثم تطبيق `WRAPCOLS`. نفس النمط يعمل عندما تحتاج إلى استيراد بيانات من قاعدة بيانات أو ملف CSV قبل التغليف.

## نصيحة احترافية: تحقق من النتيجة دون فتح Excel

بعد الحفظ، يمكنك قراءة المنطقة المغلفة برمجيًا للتأكد من نجاح العملية:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

يجب أن يعرض الطرفية القائمة الأصلية مقسمة عبر ثلاثة أعمدة، مؤكدًا أن **wrap data in excel** عمل كما هو متوقع.

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان النطاق المصدر يحتوي على صفوف أكثر مما يمكن لـ `WRAPCOLS` ملئه؟* | تستمر الدالة في إنشاء صفوف جديدة حسب الحاجة. يبقى عدد الأعمدة ثابتًا. |
| *هل يمكنني تغليف إلى عدد مختلف من الأعمدة؟* | نعم—غيّر الوسيط الثاني، مثلاً `=WRAPCOLS(A2:A10,5)` لخمس أعمدة. |
| *هل أحتاج إلى مسح الصيغة بعد الحساب؟* | ليس إذا استدعيت `CalculateFormula()`. تُعيد الدالة مصفوفة ثابتة، لكن الصيغة تبقى في الخلية. إذا كنت تريد قيمة صافية، انسخ النطاق والصق‑القيم فوقه. |
| *هل سيعمل هذا مع ملفات `.xls` القديمة؟* | `WRAPCOLS` هي دالة مصفوفة ديناميكية تم تقديمها في Excel 365. الصيغ القديمة التي لا تدعم المصفوفات الديناميكية ستخزن الصيغة ولكن قد لا تعرض النتيجة المغلفة بشكل صحيح. استخدم `.xlsx` لسلوك موثوق. |

## الخلاصة

أنت الآن تعرف **how to use wrapcols** في C# لت **wrap data in Excel**، وكيفية **calculate Excel formulas** في الوقت الفعلي، وكيفية **save Excel file C#** بعد التحويل. يوضح المثال الكامل تحميل مصنف، تطبيق دالة `WRAPCOLS`، إجبار الحساب، وحفظ النتيجة.

### الخطوات التالية

* استكشف دوال المصفوفة الديناميكية الأخرى مثل `UNWRAPCOLS` أو `SEQUENCE`.  
* استخدم **Aspose.Cells** لاستيراد البيانات من قاعدة بيانات ثم تغليفها تلقائيًا.  
* اجمع `WRAPCOLS` مع التنسيق الشرطي لتسليط الضوء على صفوف معينة بعد التغليف.

لا تتردد في تجربة نطاقات مصدر مختلفة، عدد الأعمدة، وصيغ الإخراج. إذا واجهت أي مشاكل، فإن مراجعة خطوة **calculate Excel formulas** أو فحص إعدادات حساب المصنف عادةً ما يحلها.

--- 

*صورة: ![لقطة شاشة للبيانات المغلفة في Excel](/images/wrapcols-example.png){.align-center alt="لقطة شاشة تُظهر البيانات المغلفة في ورقة عمل Excel بعد تطبيق WRAPCOLS"}*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام WRAPCOLS في C# لمصفوفات Excel وحفظ المصنف](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [كيفية إنشاء مصنف Excel وتقسيم البيانات باستخدام WRAPCOLS في C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}