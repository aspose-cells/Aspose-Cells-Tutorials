---
category: general
date: 2026-10-26
description: تعلم كيفية استخدام WRAPCOLS في C# لتقسيم نطاق إلى أعمدة، وتطبيق WRAPROWS
  للصفوف، وحفظ المصنف كملف XLSX برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: ar
lastmod: 2026-10-26
og_description: كيفية استخدام WRAPCOLS في C# لتقسيم البيانات إلى أعمدة، واستخدام WRAPROWS
  للصفوف، وحفظ المصنف بصيغة XLSX. اتبع الدليل الكامل خطوة بخطوة.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: كيفية استخدام WRAPCOLS في C# – تقسيم النطاقات وحفظها كملف XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية استخدام WRAPCOLS في C# وحفظ المصنف كملف XLSX
url: /ar/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في C# وحفظ المصنف كملف XLSX

إذا كنت بحاجة إلى **كيفية استخدام WRAPCOLS** لإعادة تنظيم البيانات في ملف Excel، فإن هذا الدليل يوضح لك حلاً كاملاً وقابلاً للتنفيذ. سترى **مثالًا على excel wrapcols**، وتتعلم كيفية **تقسيم النطاق إلى صفوف** باستخدام WRAPROWS، وتختتم بـ **حفظ المصنف كملف XLSX**—كل ذلك يتم **برمجيًا**.

العمل مع Excel من C# يعني غالبًا إنشاء مصنف، تطبيق صيغ، وحفظ الملف. يستخدم الكود أدناه مكتبة **Aspose.Cells**، التي تسمح لك بالتعامل مع ملفات Excel دون الحاجة إلى تثبيت Microsoft Office. بنهاية هذا الشرح ستكون قادرًا على **إنشاء مصنف Excel برمجيًا**، تقسيم البيانات أفقياً وعمودياً، وإنتاج ملف `.xlsx` نظيف جاهز للمعالجة اللاحقة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+)
* إشارة إلى حزمة **Aspose.Cells** عبر NuGet  
  ```bash
  dotnet add package Aspose.Cells
  ```
* إلمام أساسي بـ C# وصيغ Excel

## الخطوة 1: كيفية استخدام WRAPCOLS لتقسيم نطاق إلى أعمدة

دالة **WRAPCOLS** تأخذ نطاقًا أحادي الأبعاد وتوزع قيمه عبر عدد الأعمدة المحدد. في هذا المثال نبدأ بالقيم في `A1:A10` ونطلب من WRAPCOLS إنشاء ثلاثة أعمدة.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **النتيجة:** الخلايا `C1:E4` الآن تحتوي على العناصر العشرة الأصلية مرتبة في ثلاثة أعمدة (العمود الأخير يحتوي على العناصر المتبقية).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## الخطوة 2: تقسيم النطاق إلى صفوف باستخدام WRAPROWS

بينما تعمل **WRAPCOLS** أفقياً، تقوم **WRAPROWS** بالعكس: فهي توزع نطاقًا عبر عدد محدد من الصفوف. هنا نأخذ القيم من `B1:B10` ونرتبها في صفين بدءًا من `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **النتيجة:** الصيغة تملأ الخلايا `F1:K2` بالعشرة قيم موزعة على صفين.

## الخطوة 3: حفظ المصنف كملف XLSX

بعد تطبيق الصيغ، الخطوة الأخيرة هي حفظ الملف. عملية **save workbook as xlsx** تكتب المصنف الموجود في الذاكرة إلى القرص بصيغة OpenXML الحديثة.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### ما يبدو عليه الملف المحفوظ

عند فتح `wrapcols_wraprows_output.xlsx` في Excel سترى:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

و

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

الصيغ تبقى في الخلايا، لذا أي تغييرات لاحقة على النطاقات المصدرية ستنعكس تلقائيًا.

## الخطوة 4: التغييرات الشائعة وحالات الحافة

### تغيير عدد الأعمدة أو الصفوف

* **مزيد من الأعمدة:** زيادة الوسيط الثاني في `WRAPCOLS`.  
  مثال: `=WRAPCOLS(A1:A10,5)` ينشئ خمسة أعمدة، مع ترك خلايا فارغة حيث ينفد البيانات.
* **عدد أعمدة ديناميكي:** استخدم مرجع خلية بدلاً من رقم ثابت.  
  `=WRAPCOLS(A1:A10, G1)` حيث يحتوي `G1` على عدد الأعمدة المطلوب.

### التعامل مع الخلايا الفارغة أو غير الرقمية

تتجاهل WRAPCOLS و WRAPROWS الخلايا الفارغة بشكل افتراضي، لكنها تحافظ على ترتيب القيم غير الفارغة. إذا كنت بحاجة إلى الحفاظ على الفراغات، غلف النطاق المصدر بدوال `IFERROR` أو `TEXT` قبل تطبيق WRAPCOLS.

### الحفظ بصيغ أخرى

بينما يركز هذا الشرح على **save workbook as xlsx**، تدعم Aspose.Cells العديد من الصيغ (`.xls`, `.csv`, `.pdf`, إلخ):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## نصائح احترافية ومخاطر محتملة

* **نصيحة احترافية:** اضبط `Workbook.Settings.CalcEngineEnabled = true` إذا كنت تخطط لتقييم الصيغ فورًا بعد الحفظ.
* **احذر من:** النطاقات المصدرية الكبيرة قد تنتج مناطق تفريغ ضخمة، مما قد يؤثر على الأداء. قلل حجم النطاق أو قسّم العملية إلى أوراق عمل متعددة.
* **سلامة الخيوط:** كائنات Aspose.Cells **غير** آمنة للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة من `Workbook` لكل خيط إذا كنت تعالج الملفات بالتوازي.

## الخلاصة

أنت الآن تعرف **كيفية استخدام WRAPCOLS** لتقسيم نطاق عمودي إلى عدة أعمدة، وكيفية **تقسيم النطاق إلى صفوف** باستخدام WRAPROWS، وكيفية **حفظ المصنف كملف XLSX** بعد إجراء هذه التحويلات. باتباع الخطوات أعلاه يمكنك **إنشاء مصنف Excel برمجيًا**، تطبيق صيغ تفريغ قوية، وإنتاج ملفات Excel جاهزة للمشاركة دون تدخل يدوي.

### ما التالي؟

* استكشف **التنسيق الشرطي** لتسليط الضوء على البيانات المفروزة.
* اجمع بين **WRAPCOLS** و **SORT** أو **FILTER** لإنشاء لوحات معلومات ديناميكية.
* استخدم **API المخططات** في Aspose.Cells لتصوير البيانات المعاد ترتيبها مباشرة من الكود.

برمجة سعيدة، واستمتع بأتمتة عمليات Excel الخاصة بك!


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}