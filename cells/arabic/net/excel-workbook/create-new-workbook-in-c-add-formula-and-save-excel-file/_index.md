---
category: general
date: 2026-02-23
description: إنشاء مصنف جديد برمجيًا بلغة C# وإضافة صيغة إلى خلية. تعلم كيفية استخدام
  EXPAND، ثم احفظ مصنف Excel بسهولة.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: ar
og_description: إنشاء مصنف جديد برمجيًا باستخدام C#. إضافة صيغة إلى خلية، تعلم كيفية
  استخدام EXPAND، وحفظ مصنف Excel في ثوانٍ.
og_title: إنشاء مصنف جديد في C# – إضافة صيغة وحفظ ملف Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: إنشاء مصنف جديد في C# – إضافة صيغة وحفظ ملف Excel
url: /ar/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد في C# – إضافة صيغة وحفظ ملف Excel

هل تساءلت يومًا كيف يمكنك **إنشاء مصنف جديد** من الشيفرة دون فتح Excel مطلقًا؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى إنشاء جدول بيانات سريعًا — ربما لتقرير، أو تصدير، أو تفريغ بيانات سريع.  

الأخبار السارة؟ في هذا الدليل ستتعرف بالضبط على كيفية **إنشاء مصنف جديد**، وإضافة **صيغة إلى خلية**، ثم **حفظ مصنف Excel** ببضع أسطر فقط من C#. سنستعرض أيضًا **كيفية استخدام EXPAND** لتوليد مصفوفات ديناميكية دون النسخ اليدوي. في النهاية، ستتمكن من **إنشاء ملف Excel برمجيًا** وإرساله إلى المستخدمين أو الخدمات المت downstream.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (أي بيئة تشغيل .NET حديثة تعمل)
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو مرخصة) – هذه المكتبة تزودنا بفئات `Workbook` و `Worksheet` المستخدمة أدناه.
- فهم أساسي لصياغة C# — لا حاجة لمعرفة عميقة بـ Excel.

إذا كان لديك هذه بالفعل، رائع! إذا لا، احصل على Aspose.Cells من NuGet (`Install-Package Aspose.Cells`) وستكون جاهزًا للبدء.

---

## الخطوة 1: إنشاء مصنف جديد – الأساس

للبدء، نحتاج إلى إنشاء كائن مصنف جديد. فكر فيه كفتح ملف Excel جديد تمامًا وخالٍ من أي محتوى.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **لماذا هذا مهم:** فئة `Workbook` هي نقطة الدخول لأي تعديل على Excel. بإنشاء نسخة جديدة، نخصص الذاكرة للأوراق، الأنماط، والصيغ — كل ذلك دون التفاعل مع نظام الملفات.

---

## الخطوة 2: الوصول إلى الورقة الأولى

كل مصنف جديد يأتي بورقة عمل افتراضية (تسمى *Sheet1*). سنستخرجها لنتمكن من وضع البيانات والصيغ.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **نصيحة احترافية:** إذا كنت بحاجة إلى عدة أوراق، ما عليك سوى استدعاء `workbook.Worksheets.Add("MySheet")` وابدأ العمل مع كائن `Worksheet` المعاد.

---

## الخطوة 3: إضافة صيغة إلى خلية – باستخدام EXPAND

الآن للجزء الممتع: إدراج صيغة. دالة `EXPAND` مثالية عندما تريد تحويل مصفوفة ثابتة إلى نطاق أكبر يتم تعبئته تلقائيًا.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### كيف تعمل صيغة EXPAND

| المعامل | المعنى |
|----------|---------|
| `{1,2,3}` | المصفوفة المصدر (قائمة أفقية من ثلاثة أرقام) |
| `5`       | عدد الصفوف المطلوب في النتيجة |
| `1`       | عدد الأعمدة المطلوب (احتفظ بـ 1 لتبقى عمودية) |

عند تقييم Excel لهذا، ينتج قائمة **عمودية**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **لماذا نستخدم EXPAND؟** إنها تلغي الحاجة إلى النسخ اليدوي أو حلقات VBA. الدالة تعيد تشكيل البيانات ديناميكيًا، مما يجعل جداولك أكثر قوة وأسهل صيانة.

---

## الخطوة 4: حفظ مصنف Excel – حفظ النتيجة

مع وجود الصيغة، الخطوة الأخيرة هي كتابة المصنف إلى القرص. يمكنك اختيار أي مجلد لديك صلاحية كتابة فيه.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **ما ستراه:** افتح `ExpandFormula.xlsx` في Excel، وستظهر المصفوفة الموسعة في الخلية `A1`. الصيغة نفسها تبقى في الخلية، لذا إذا عدلت المصفوفة المصدر، يتم تحديث النتيجة تلقائيًا.

---

## اختياري: التحقق من النتيجة برمجيًا

إذا كنت تفضل عدم فتح Excel يدويًا، يمكنك قراءة القيم مرة أخرى للتأكد من مطابقتها للتوقعات.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

تشغيل الكود أعلاه سيطبع:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## أسئلة شائعة وحالات خاصة

| السؤال | الإجابة |
|----------|--------|
| **هل يمكنني استخدام EXPAND مع مصفوفة مصدر أكبر؟** | بالتأكيد. فقط غير `{1,2,3}` إلى أي ثابت أو نطاق خلايا، مثل `EXPAND(A1:C1,10,1)`. |
| **ماذا لو احتجت إلى نتيجة أفقية؟** | بدل معاملات الصف/العمود: `EXPAND({1,2,3},1,5)` سيولد نطاقًا من صف واحد وخمس أعمدة. |
| **هل سيعمل هذا على إصدارات Excel القديمة؟** | `EXPAND` متاح بدءًا من Excel 365/2021. بالنسبة للإصدارات القديمة، سيتعين عليك محاكاة المصفوفة باستخدام `INDEX`/`SEQUENCE`. |
| **هل أحتاج إلى استدعاء `workbook.CalculateFormula()`؟** | لا. Aspose.Cells يقوم تلقائيًا بتقييم الصيغ عند الحفظ، لذا تظهر القيم فورًا. |
| **كيف أضيف أكثر من ورقة قبل الحفظ؟** | استدعِ `workbook.Worksheets.Add("SecondSheet")` وكرر خطوات تعديل الخلايا على الورقة الجديدة. |

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه والصقه في تطبيق Console، عدل مسار الإخراج، واضغط **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

افتح الملف المُولد وسترى نفس الأرقام مملوءة في العمود **A**.

---

## ملخص بصري

![مثال إنشاء مصنف جديد](create-new-workbook.png "لقطة شاشة تُظهر مصنفًا جديدًا تم إنشاؤه باستخدام إنشاء مصنف جديد في C#")

*الصورة توضح المصنف المُنشأ حديثًا مع نتيجة EXPAND.*

---

## الخلاصة

أنت الآن تعرف كيف **تنشئ مصنفًا جديدًا**، **تضيف صيغة إلى خلية**، و**تحفظ مصنف Excel** باستخدام C#. من خلال إتقان **كيفية استخدام EXPAND**، يمكنك توليد مصفوفات ديناميكية دون جهد يدوي، وتتيح لك العملية بأكملها **إنشاء ملف Excel برمجيًا** لأي سيناريو أتمتة.

ما التالي؟ جرّب استبدال المصفوفة الثابتة بمرجع نطاق، واختبر أبعاد `EXPAND` المختلفة، أو ربط صيغ متعددة عبر الأوراق. النمط نفسه يعمل مع المخططات، التنسيق، وحتى جداول Pivot — لذا استمر في الاستكشاف.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بقوة Excel البرمجية!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}