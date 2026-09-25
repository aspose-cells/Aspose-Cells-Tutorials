---
category: general
date: 2026-04-07
description: تعلم كيفية تحديث Pivot، وإدراج صورة في Excel، وحفظ ملف Excel مع عنصر
  نائب للصورة في بضع خطوات فقط.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: ar
og_description: كيفية تحديث Pivot في Excel، وإدراج صورة في Excel، وحفظ مصنف Excel
  باستخدام C# مع عنصر نائب للصورة. مثال على الكود خطوة بخطوة.
og_title: كيفية تحديث الجداول المحورية وإدراج صورة في إكسل – دليل شامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية تحديث الجداول المحورية وإدراج صورة في إكسل – دليل كامل
url: /ar/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحديث Pivot وإدراج صورة في Excel – دليل كامل

هل تساءلت يومًا **كيفية تحديث Pivot** عندما تتغير بيانات المصدر، ثم إدراج مخطط أو صورة جدول جديدة مباشرةً في نفس الورقة؟ لست الوحيد. في العديد من خطوط تقارير البيانات، تكون البيانات مخزنة في قاعدة بيانات، وتقوم جدول Pivot بسحبها، ويحتاج ملف Excel النهائي إلى عرض الأرقام الأخيرة كصورة—حتى لا يتمكن المستخدمون اللاحقون من تعديل المصدر عن طريق الخطأ.

في هذا الدرس سنستعرض ذلك بالضبط: **كيفية تحديث Pivot**، **إدراج صورة في Excel**، وأخيرًا **حفظ مصنف Excel** مع استخدام **عنصر نائب للصورة**. في النهاية ستحصل على برنامج C# واحد قابل للتنفيذ يقوم بكل ذلك، وستفهم لماذا كل سطر مهم.

> **نصيحة احترافية:** الطريقة تعمل مع Aspose.Cells 2024 أو أحدث، مما يعني أنك لا تحتاج إلى تثبيت Excel على الخادم.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (حزمة NuGet `Aspose.Cells`).  
- .NET 6.0 SDK أو أحدث (الكود يتوافق أيضًا مع .NET 8).  
- ملف Excel أساسي (`input.xlsx`) يحتوي بالفعل على جدول Pivot وعنصر نائب للصورة (أول كائن صورة في الورقة).  
- قليل من الفضول حول نماذج كائنات Excel.

لا توجد حاجة إلى COM interop إضافي، ولا تثبيت Office، فقط C# نقي.

---

## كيفية تحديث Pivot والتقاط البيانات الأحدث

أول شيء عليك فعله هو إخبار Excel (أو بالأحرى Aspose.Cells) بأن جدول Pivot يجب أن يعيد حسابه بناءً على أحدث نطاق مصدر. تخطي هذه الخطوة سيتركك بأرقام قديمة، مما يُفقد الغرض الكامل من الأتمتة.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**لماذا هذا مهم:**  
عند استدعاء `Refresh()`، يعيد محرك Pivot تشغيل منطق التجميع. إذا قمت لاحقًا بتصدير Pivot كصورة، ستظهر الصورة *الإجماليات الحالية*، وليس تلك التي كانت موجودة عند آخر حفظ للملف.

---

## إدراج صورة في Excel باستخدام عنصر نائب للصورة

الآن بعد أن تم تحديث Pivot، نحتاج إلى تحويله إلى صورة ثابتة. هذا مفيد عندما تريد تثبيت الشكل للوزع أو تضمينه لاحقًا في شريحة PowerPoint.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

كائن `ImageOrPrintOptions` يتيح لك التحكم في الدقة، الخلفية، والصيغة. PNG غير مضغوط ويعمل بشكل ممتاز لمعظم التقارير التجارية.

---

## إضافة عنصر نائب للصورة إلى ورقة العمل

معظم قوالب Excel تحتوي بالفعل على شكل أو صورة تعمل كـ “فتحة” للرسومات الديناميكية. إذا لم يكن لديك واحدة، فقط أدخل صورة فارغة في Excel واحفظ القالب—ستظهر في Aspose.Cells كـ `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**ماذا لو كان لديك عدة عناصر نائب؟**  
فقط غيّر الفهرس (`Pictures[1]`, `Pictures[2]`, …) أو قم بالتكرار عبر `worksheet.Pictures` للعثور على واحدة بالاسم.

---

## حفظ مصنف Excel بعد التعديلات

أخيرًا، نقوم بحفظ التغييرات. الآن يحتوي المصنف على Pivot محدث، PNG تم إنشاؤه حديثًا، وعنصر نائب الصورة تم تحديثه بهذه الصورة.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

عند فتح `output.xlsx` ستلاحظ أن فتحة الصورة امتلأت بأحدث لقطة من Pivot. لا حاجة لأي خطوات يدوية.

---

## مثال كامل يعمل (جميع الخطوات معًا)

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. يتضمن بيانات `using` الضرورية، معالجة الأخطاء، وتعليقات توضح كل سطر غير واضح.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**النتيجة المتوقعة:**  
افتح `output.xlsx`. الآن يظهر أول كائن صورة PNG لجدول Pivot المحدث. إذا غيرت بيانات المصدر في `input.xlsx` وشغلت البرنامج مرة أخرى، ستُحدَّث الصورة تلقائيًا—دون الحاجة إلى نسخ‑لصق يدوي.

---

## الاختلافات الشائعة وحالات الحافة

| الحالة | ما الذي يجب تغييره |
|-----------|----------------|
| **جداول Pivot متعددة** | قم بالتكرار عبر `sheet.PivotTables` وقم بتحديث كل منها، ثم اختر الجدول الذي تحتاجه للصورة. |
| **تنسيق صورة مختلف** | اضبط `ImageFormat = ImageFormat.Jpeg` (أو `Bmp`) في `ImageOrPrintOptions`. |
| **اختيار عنصر نائب ديناميكي** | استخدم `sheet.Pictures["MyPlaceholderName"]` بدلاً من الفهرس. |
| **مصنفات كبيرة** | زد `Workbook.Settings.CalculateFormulaEngine` إلى `EngineType.Fast` للحصول على تحديث أسرع. |
| **التشغيل على خادم بدون واجهة** | Aspose.Cells يعمل بالكامل بدون واجهة مستخدم، لذا لا تحتاج إلى أي إعدادات إضافية. |

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع المصنفات المفعَّلة بالماكرو (`.xlsm`)?**  
ج: نعم. Aspose.Cells يتعامل معها كأي مصنف آخر؛ تُحفظ الماكروهات لكن لا تُنفّذ أثناء التحديث.

**س: ماذا لو كان Pivot يستخدم مصدر بيانات خارجي؟**  
ج: يجب التأكد من صحة سلسلة الاتصال على الجهاز الذي يشغّل الكود. استدعِ `pivotTable.CacheDefinition.ConnectionInfo` لتعديلها برمجيًا.

**س: هل يمكنني وضع الصورة في نطاق خلايا محدد بدلاً من عنصر نائب؟**  
ج: بالتأكيد. استخدم `sheet.Pictures.Add(row, column, pivotImg)` حيث `row` و `column` هما مؤشرات صفرية.

---

## الخلاصة

غطّينا **كيفية تحديث Pivot**، **إدراج صورة في Excel**، **إضافة عنصر نائب للصورة**، وأخيرًا **حفظ مصنف Excel**—كل ذلك في مقتطف C# منظم. من خلال تحديث Pivot أولاً، تضمن أن الصورة تعكس الأرقام الأخيرة، وباستخدام عنصر نائب تحافظ على قوالبك نظيفة وقابلة لإعادة الاستخدام.

بعد ذلك قد ترغب في استكشاف:

- تصدير نفس الصورة إلى تقرير PDF (`PdfSaveOptions`).  
- أتمتة دفعة من الملفات ببيانات مصدر مختلفة.  
- استخدام Aspose.Slides للصق PNG مباشرةً في شريحة PowerPoint.

لا تتردد في التجربة—استبدل PNG بـ JPEG، غيّر DPI، أو أضف صورًا متعددة. الفكرة الأساسية تبقى نفسها: حافظ على البيانات محدثة، التقطها كصورة، وأدرجها حيث تحتاجها.

برمجة سعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}