---
category: general
date: 2026-02-28
description: كيفية إنشاء مصفوفة في Excel باستخدام C#. تعلم توليد الأرقام، تقييم الصيغة،
  إنشاء مصنف Excel وحفظ ملف Excel في دقائق.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: ar
og_description: كيفية إنشاء مصفوفة في Excel باستخدام C#. يوضح هذا الدرس كيفية توليد
  الأرقام، تقييم صيغة، إنشاء مصنف وحفظ الملف.
og_title: كيفية إنشاء مصفوفة في إكسل باستخدام C# – دليل كامل
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: كيفية إنشاء مصفوفة في إكسل باستخدام C# – دليل خطوة بخطوة
url: /ar/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مصفوفة في Excel باستخدام C# – دليل برمجة كامل

هل تساءلت يومًا **how to create array** في Excel برمجيًا باستخدام C#؟ لست الوحيد—المطورون يطلبون باستمرار طريقة سريعة لإنشاء مجموعة من الأرقام دون كتابة يدوية. في هذا الدليل سنستعرض الخطوات الدقيقة **create excel workbook**، وإدراج صيغة **generates numbers**، **evaluate the formula**، وأخيرًا **save excel file** حتى تتمكن من فتحها في Excel ورؤية النتيجة.

سنستخدم مكتبة Aspose.Cells لأنها تمنحنا تحكمًا كاملاً في الصيغ والحساب دون الحاجة إلى تثبيت Excel. إذا كنت تفضل مكتبة أخرى فإن المفاهيم تبقى نفسها—فقط استبدل استدعاءات الـ API.

## ما يغطيه هذا الدرس

- إعداد مشروع C# مع حزمة NuGet المطلوبة.  
- إنشاء مصنف جديد (هذا هو جزء *create excel workbook*).  
- كتابة صيغة تُنشئ مصفوفة 4‑صف × 3‑عمود باستخدام `SEQUENCE` و `WRAPCOLS`.  
- إجبار المحرك على **evaluate the formula** حتى تتجسد المصفوفة.  
- حفظ المصنف على القرص (**save excel file**) والتحقق من النتيجة.  

بنهاية هذا الشرح ستحصل على برنامج قابل للتنفيذ ينتج ورقة Excel تبدو هكذا:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![كيفية إنشاء مصفوفة في Excel – الورقة الناتجة بعد تشغيل كود C#](image.png)

*(يتضمن نص بديل الصورة الكلمة المفتاحية الأساسية “how to create array” لتحسين محركات البحث.)*

---

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+).  
- Visual Studio 2022 أو أي محرر تفضله.  
- حزمة NuGet **Aspose.Cells** (يتوفر نسخة تجريبية مجانية).  

لا يلزم تثبيت Excel إضافيًا لأن Aspose.Cells يتولى محرك الحساب داخليًا.

---

## الخطوة 1: إعداد المشروع واستيراد Aspose.Cells

للبدء، أنشئ تطبيق console وأضف المكتبة:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

الآن افتح **Program.cs** وأضف مساحة الاسم:

```csharp
using Aspose.Cells;
```

*لماذا هذا مهم*: استيراد `Aspose.Cells` يزودنا بـ `Workbook` و `Worksheet` وفئات الحساب التي سنحتاجها **create excel workbook** والعمل مع الصيغ.

---

## الخطوة 2: إنشاء المصنف والورقة المستهدفة

نحتاج إلى كائن مصنف جديد؛ الورقة الأولى (`Worksheets[0]`) ستستضيف المصفوفة.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*شرح*: فئة `Workbook` تمثل ملف Excel بالكامل. بشكل افتراضي تحتوي على ورقة واحدة، وهو مثالي لعرض توضيحي بسيط. إذا احتجت أوراقًا إضافية يمكنك استدعاء `workbook.Worksheets.Add()` لاحقًا.

---

## الخطوة 3: كتابة صيغة **Generates Numbers** وتشكيل مصفوفة

تسمح لنا دوال المصفوفة الديناميكية في Excel (`SEQUENCE` و `WRAPCOLS`) بإنتاج كتلة من القيم بصيغة واحدة. هذا هو النص الدقيق الذي سنعيّنه:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*لماذا يعمل هذا*:  
- `SEQUENCE(12,1,1,1)` تُعيد قائمة عمودية بالأرقام من 1 إلى 12.  
- `WRAPCOLS(...,3)` تأخذ تلك القائمة وتملأها عبر ثلاثة أعمدة، مع الانسكاب تلقائيًا إلى الصفوف التالية.  

إذا فتحت المصنف في Excel **دون** تقييم الصيغة أولًا، سترى نص الصيغة فقط في `A1`. الخطوة التالية تجبر الحساب.

---

## الخطوة 4: **Evaluate the Formula** حتى تتجسد المصفوفة

Aspose.Cells لا يعيد حساب الصيغ تلقائيًا عند الكتابة، لذا نستدعي محرك الحساب صراحةً:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*ما يحدث*: `Calculate()` يمر على كل خلية تحتوي على صيغة، يحسب نتيجتها، ويكتب القيم مرة أخرى. هذا هو جزء **how to evaluate formula** في دليلنا. بعد هذا الاستدعاء، تحتوي الخلايا A1:C4 على الأرقام من 1 إلى 12، تمامًا كما يحدث في Excel الأصلي.

---

## الخطوة 5: **Save Excel File** والتحقق من النتيجة

أخيرًا نقوم بحفظ المصنف على القرص:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

افتح `output.xlsx` في Excel وسترى المصفوفة 4 × 3 التي أنشأناها. إذا كنت تستخدم نسخة Excel أقدم من 365/2019، لن تُعترف بدوال المصفوفة الديناميكية—ستظل Aspose.Cells تكتب القيم المُحسوبة، لذا يظل الملف قابلًا للاستخدام.

*نصيحة احترافية*: استخدم `SaveFormat.Xlsx` إذا أردت فرض تنسيق معين، مثال: `workbook.Save(outputPath, SaveFormat.Xlsx);`.

---

## مثال كامل جاهز للنسخ (Copy‑Paste Ready)

فيما يلي البرنامج الكامل. الصقه في **Program.cs**، شغّله بـ `dotnet run`، وستحصل على `output.xlsx` في مجلد المشروع.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**المخرجات المتوقعة** (في وحدة التحكم):

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

افتح الملف وسترى الأرقام من 1 إلى 12 مرتبة كما هو موضح أعلاه.

---

## تنويعات وحالات خاصة

### 1. إصدارات Excel القديمة بدون مصفوفات ديناميكية  
إذا كان جمهورك يستخدم Excel 2016 أو أقدم، فإن `SEQUENCE` و `WRAPCOLS` غير موجودين. حل سريع هو توليد الأرقام في C# وكتابتها مباشرة:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

هذه الحلقة اليدوية تُحاكي النتيجة نفسها، وإن كان الكود أطول قليلاً. يبقى مفهوم **how to generate numbers** هو نفسه.

### 2. تغيير حجم المصفوفة  
هل تريد شبكة 5 × 5 بالأرقام من 1 إلى 25؟ فقط عدّل معاملات `SEQUENCE` وعدد الأعمدة في `WRAPCOLS`:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. استخدام النطاقات المسماة لإعادة الاستخدام  
يمكنك تعيين النطاق المنسكب إلى اسم لاستخدامه في صيغ أخرى:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

الآن يمكن لأي ورقة أخرى الإشارة إلى `MyArray` مباشرة.

---

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|---|---|---|
| **Formula not spilling** | تم حذف `Calculate()` أو استدعاؤه قبل تعيين الصيغة. | احرص دائمًا على استدعاء `workbook.Calculate()` **بعد** تعيين الصيغة. |
| **File saved but empty** | تم استخدام `SaveFormat.Csv` عن طريق الخطأ. | استخدم `SaveFormat.Xlsx` أو اترك الصيغة لتحددها Aspose تلقائيًا. |
| **Dynamic 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}