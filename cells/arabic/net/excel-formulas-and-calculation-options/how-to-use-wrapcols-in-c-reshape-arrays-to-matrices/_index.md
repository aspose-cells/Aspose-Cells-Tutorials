---
category: general
date: 2026-05-23
description: كيفية استخدام WRAPCOLS في C# لإعادة تشكيل مصفوفة أحادية البعد إلى مصفوفة
  ثنائية الأبعاد. تعلّم دالة تغليف الأعمدة، واكتب الصيغة في الخلية، وحوّل 1D إلى 2D
  بسهولة.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: ar
og_description: كيفية استخدام WRAPCOLS في C# يتيح لك إعادة تشكيل مصفوفة أحادية البعد
  إلى مصفوفة ثنائية البعد باستخدام صيغة واحدة. اتبع هذا الدليل لكتابة الصيغة في الخلية
  وإتقان وظيفة تغليف الأعمدة.
og_title: كيفية استخدام WRAPCOLS في C# – إعادة تشكيل المصفوفات إلى مصفوفات
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: كيفية استخدام WRAPCOLS في C# – إعادة تشكيل المصفوفات إلى مصفوفات
url: /ar/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في C# – تحويل المصفوفات إلى مصفوفات ثنائية الأبعاد

هل تساءلت يومًا **كيف تستخدم WRAPCOLS** عندما تحتاج إلى تحويل قائمة مسطحة من الأرقام إلى جدول منظم؟ لست وحدك—الكثير من المطورين يواجهون صعوبة عندما يحاولون تحويل قائمة ذات بعد واحد إلى شبكة ذات بعدين دون كتابة الكثير من حلقات التكرار. الخبر السار؟ دالة WRAPCOLS (المعروفة أحيانًا بدالة تغليف الأعمدة) تقوم بالعمل الشاق في سطر واحد فقط، ويمكنك إدراجها مباشرةً في مصنف Excel من C#.

في هذا الدرس سنستعرض العملية بالكامل: من إنشاء المصنف، إلى **كتابة الصيغة في الخلية**، إلى **تحويل المصفوفة إلى مصفوفة ثنائية الأبعاد**، وأخيرًا إلى **تحويل 1D إلى 2D** باستخدام صيغة WRAPCOLS. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يعمل مع أي مصفوفة رقمية، وستفهم لماذا تُعد دالة تغليف الأعمدة بديلًا أنظف غالبًا لإعادة تشكيل المصفوفات يدويًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+)
* مكتبة **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو نسخة مرخصة) – هي المكوّن الذي يوفّر لنا كائنات `Workbook` و `Worksheet` و `Cell` المستخدمة أدناه.
* فهم أساسي لصياغة C#—لا تحتاج إلى معرفة متقدمة بـ Excel.

هل لديك كل ذلك؟ عظيم—لنبدأ.

![Resulting 2x3 matrix after using WRAPCOLS function in C# – how to use WRAPCOLS](https://example.com/images/wrapcols-result.png "كيفية استخدام WRAPCOLS – مصفوفة 2×3 الناتجة")

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

### لماذا هذا مهم

يمكنك محاولة كتابة منطق المصفوفة بنفسك، لكن **دالة تغليف الأعمدة** تتعامل بالفعل مع الحالات الحدية مثل القسمة غير المتساوية والمدخلات الفارغة. إضافة حزمة NuGet الخاصة بـ Aspose.Cells يمنحنا واجهة برمجة تطبيقات نظيفة للتفاعل مع صيغ Excel مباشرةً من C#.

```bash
dotnet add package Aspose.Cells
```

*نصيحة احترافية:* إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → ابحث عن **Aspose.Cells** وقم بتثبيت أحدث نسخة مستقرة.

## الخطوة 2: إنشاء مصنف جديد (أو تحميل مصنف موجود)

الآن بعد أن أصبحت المكتبة جاهزة، يمكننا إنشاء كائن مصنف. هنا ستتم خطوة **كتابة الصيغة في الخلية**.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

في هذا المثال أنشأنا مصنفًا جديدًا تمامًا؛ يمكنك أيضًا تحميل ملف موجود باستخدام `new Workbook("path/to/file.xlsx")` إذا احتجت إلى دمج المصفوفة في قالب مُنسق مسبقًا.

## الخطوة 3: إدراج صيغة WRAPCOLS في خلية

### جوهر “كيفية استخدام WRAPCOLS”

تأخذ دالة **WRAPCOLS** معاملين: مصفوفة (أو نطاق) وعدد الأعمدة التي تريدها لكل صف. في مثالنا سنعيد تشكيل المصفوفة الحرفية `{1,2,3,4,5,6}` إلى **2 صفوف × 3 أعمدة**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

لاحظ كيف تعكس الصيغة ما تكتبه في Excel نفسه. بوضعها في `Cells[0,0]` (الخلية **A1**) نحن **نكتب الصيغة في خلية** دون أي تعقيدات إضافية.

## الخطوة 4: إجبار الحساب حتى تُقيم الصيغة

Aspose.Cells لا يقيم الصيغ تلقائيًا إلا إذا طلبت ذلك. هذه الخطوة تضمن أن المصنف يحتوي فعليًا على المصفوفة المعاد تشكيلها.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

إذا تخطيت هذا السطر، ستظل الخلايا تُظهر نص الصيغة بدلًا من القيم المحسوبة.

## الخطوة 5: قراءة النتيجة (اختياري، لكنه مفيد للتحقق)

قد ترغب في التأكد من أن عملية **تحويل المصفوفة إلى مصفوفة ثنائية الأبعاد** نجحت. إليك حلقة سريعة تطبع الشبكة 2‑by‑3 الناتجة إلى وحدة التحكم.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### النتيجة المتوقعة

```
1   2   3
4   5   6
```

تُظهر وحدة التحكم نفس التخطيط الذي تراه في Excel بعد تشغيل صيغة WRAPCOLS. هذا هو التحول **من 1D إلى 2D** قيد التنفيذ.

## الخطوة 6: معالجة الحالات الحدية – ماذا لو لم يكن طول المصفوفة مضاعفًا لعدد الأعمدة؟

إذا كانت المصفوفة المصدر تحتوي، على سبيل المثال، على 7 عناصر وطلبت 3 أعمدة، فإن WRAPCOLS ستُنشئ الصف الأخير بالعناصر المتبقية وتترك الخلايا المتبقية فارغة. إليك تعديلًا سريعًا لتوضيح ذلك:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

النتيجة:

```
1   2   3
4   5   6
7       
```

دالة **تغليف الأعمدة** تُضيف خلايا فارغة إلى الصف الأخير بشكلٍ أنيق، لذا لا تحتاج إلى كود إضافي للتعامل مع الأحجام غير المتطابقة.

## الخطوة 7: استخدام WRAPCOLS مع بيانات ديناميكية

في المشاريع الحقيقية نادراً ما يتم كتابة المصفوفة يدويًا. بدلاً من ذلك ستُنشئ تمثيلًا نصيًا من مجموعة C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

الآن لقد **حولت 1D إلى 2D** لأي طول، ولا يزال الناتج مصفوفة نظيفة. الصيغة تُبنى في وقت التشغيل، لكن **دالة تغليف الأعمدة** تظل هي نفسها.

## الأخطاء الشائعة ونصائح احترافية

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| نسيان استدعاء `workbook.CalculateFormula()` | Aspose.Cells يترك الصيغ غير مُقيمة | دائمًا استدعِ الطريقة بعد تعيين أي صيغة |
| استخدام مصفوفة حرفية غير رقمية | WRAPCOLS تتوقع أرقامًا أو سلاسل يمكن تحويلها | تأكد من أن الحرفية تحتوي على أرقام فقط (أو سلاسل محاطة بعلامات اقتباس) |
| الكتابة فوق بيانات موجودة عن غير قصد | وضع الصيغة في خلية تحتوي بالفعل على بيانات | اختر خلية جديدة (مثل A1) أو امسح النطاق أولًا |
| عدم الإشارة إلى فهرس الورقة الصحيح | `Worksheets[0]` هي الورقة الأولى، لكن قد تكون أضفت أوراقًا أخرى | تحقق من `worksheet = workbook.Worksheets["SheetName"];` إذا لزم الأمر |

## لماذا WRAPCOLS تتفوق على الحلقات اليدوية

* **قابلية القراءة** – سطر واحد من الصيغة يحل محل عشرات حلقات `for`.  
* **الأداء** – محرك Excel الأصلي مُحسّن بشكل كبير للتعامل مع صيغ المصفوفات.  
* **الصيانة** – يستطيع المطورون المستقبليون فهم النية فورًا: “تغليف هذه القيم في أعمدة”.  
* **القابلية للنقل** – نفس الصيغة تعمل إذا صدّرت المصنف إلى Google Sheets أو LibreOffice—لا تحتاج إلى منطق خاص بـ C#.

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)



## دروس ذات صلة

- [How to Use Aspose.Cells for .NET to Show Cell Ranges as Data Labels in Charts](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}