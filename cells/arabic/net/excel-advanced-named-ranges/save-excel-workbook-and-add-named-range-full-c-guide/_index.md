---
category: general
date: 2026-06-27
description: حفظ مصنف Excel في C# مع إضافة نطاق مسمى. تعلّم إنشاء اسم معرف واستخدام
  صيغ الاسم المعرف مع Aspose.Cells.
draft: false
keywords:
- save excel workbook
- add named range
- create defined name
- named range excel
- use defined name formulas
language: ar
og_description: احفظ مصنف Excel باستخدام C# وتعلم كيفية إضافة نطاق مسمى، وإنشاء اسم
  معرف، واستخدام صيغ الأسماء المعرفة مع Aspose.Cells.
og_title: حفظ ملف إكسل وإضافة نطاق مسمى – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel Workbook in C# while adding a named range. Learn to create
    defined name and use defined name formulas with Aspose.Cells.
  headline: Save Excel Workbook and Add Named Range – Full C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel Automation
title: حفظ ملف Excel وإضافة نطاق مسمى – دليل C# الكامل
url: /ar/net/excel-advanced-named-ranges/save-excel-workbook-and-add-named-range-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ دفتر عمل Excel وإضافة نطاق مسمى – دليل C# الكامل

هل احتجت يومًا إلى **حفظ دفتر عمل Excel** بعد إضافة بعض الأسماء المخصصة حول الورقة؟ لست وحدك. في العديد من أدوات التقارير أو التطبيقات المعتمدة على البيانات، ننتهي بإنشاء نطاق مسمى، ثم الإشارة إليه في الصيغ، وأخيرًا حفظ التغييرات على القرص.  

في هذا الدرس سنستعرض ذلك بالضبط: تحميل ملف *.xlsx*، **إضافة نطاق مسمى**، **إنشاء اسم معرف**، استخدام ذلك الاسم داخل صيغة، وأخيرًا **حفظ دفتر عمل Excel** مع التحديثات. لا إطالة—فقط مثال كامل وقابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

> **نصيحة احترافية:** يعمل Aspose.Cells دون الحاجة إلى تثبيت Microsoft Office، مما يجعله مثاليًا لأتمتة الخوادم.

## ما ستحتاجه

- .NET 6 (أو أي بيئة تشغيل .NET حديثة)  
- حزمة NuGet Aspose.Cells لـ .NET (`Install-Package Aspose.Cells`)  
- ملف عينة `input.xlsx` (أي دفتر عمل سيعمل، لكن تأكد من أن Sheet1 يحتوي على بيانات في **A1**)  
- بيئة التطوير المتكاملة المفضلة لديك (Visual Studio, Rider, VS Code…)

هذا كل شيء. إذا كان لديك هذه المتطلبات، يمكننا القفز مباشرة إلى الشيفرة.

## الخطوة 1: إعداد المشروع

أنشئ تطبيقًا من نوع console وأضف Aspose.Cells:

```bash
dotnet new console -n ExcelNamedRangeDemo
cd ExcelNamedRangeDemo
dotnet add package Aspose.Cells
```

افتح `Program.cs`؛ سترى طريقة `Main` الافتراضية. سنستبدل محتواها بسير العمل الكامل في الخطوات التالية.

## الخطوة 2: تحميل دفتر العمل

تحميل دفتر العمل هو أول شيء تقوم به قبل أن تتمكن من **إضافة نطاق مسمى**. فكر فيه كفتح كتاب قبل أن تبدأ بكتابة ملاحظات على الهوامش.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");
```

> **لماذا هذا مهم:** كائن `Workbook` يمثل ملف Excel بالكامل في الذاكرة. بدون هذا الكائن لا يمكنك تعديل الخلايا أو الأسماء أو الصيغ.

## الخطوة 3: إنشاء اسم معرف (إضافة نطاق مسمى)

الآن نقوم فعليًا **بإنشاء اسم معرف** يشير إلى خلية أو نطاق محدد. في واجهة Excel كنت ستذهب إلى *Formulas → Name Manager*؛ هنا نقوم بذلك برمجيًا.

```csharp
        // Step 3: Add a defined name that points to cell A1 on Sheet1
        // This name can be used in formulas throughout the workbook
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");
```

> **شرح:** `wb.Names.Add` يسجل *نطاقًا مسمى* يُدعى **Sales**. السلسلة `=Sheet1!$A$1` هي صيغة الإشارة—تمامًا ما ستكتبه في مربع حوار Name Manager.

## الخطوة 4: استخدام الاسم المعرف في صيغة

وجود اسم مفيد، لكن عادةً ما تريد **استخدام صيغ الاسم المعرف** في مكان ما. لنكتب صيغة بسيطة تضيف 10 إلى القيمة في **Sales** وتضع النتيجة في **B1**.

```csharp
        // Step 4: Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");
```

عند إعادة حساب دفتر العمل، سيظهر `B1` ما يحتويه `A1` زائد عشرة. هذا يوضح قوة *نطاق مسمى في Excel*—يمكنك تغيير الإشارة الأساسية مرة واحدة وتُحدّث جميع الصيغ تلقائيًا.

## الخطوة 5: حفظ دفتر العمل المعدل

أخيرًا نقوم **بحفظ دفتر عمل Excel** إلى ملف جديد لتستمر التغييرات. يمكنك استبدال الأصلي أو الكتابة إلى موقع جديد؛ هنا نحتفظ بكليهما.

```csharp
        // Step 5: Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

تشغيل البرنامج ينتج مخرجات وحدة التحكم مشابهة لـ:

```
Workbook loaded successfully.
Defined name 'Sales' added (named range Excel).
Formula '=Sales + 10' written to B1.
Workbook saved as 'YOUR_DIRECTORY\output.xlsx'.
```

افتح `output.xlsx` وسترى أن **B1** الآن يحتوي على `=Sales + 10`، بينما يظل **A1** دون تغيير. يظهر الاسم **Sales** تحت *Formulas → Name Manager*.

## الحالات الخاصة والأسئلة الشائعة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان اسم الورقة يحتوي على مسافات؟** | ضعه بين علامات اقتباس مفردة: `= 'My Sheet'!$A$1`. |
| **هل يمكنني توجيه الاسم إلى نطاق متعدد الخلايا؟** | بالطبع—استخدم `=Sheet1!$A$1:$A$5` عند استدعاء `wb.Names.Add`. |
| **هل أحتاج إلى إعادة حساب يدويًا؟** | يقوم Aspose.Cells بإعادة الحساب تلقائيًا عند قراءة قيمة خلية. إذا كنت بحاجة إلى تحديث كامل، استدعِ `wb.CalculateFormula()`. |
| **ماذا عن الأسماء الموجودة؟** | `wb.Names.Add` سيُطلق استثناء إذا كان الاسم موجودًا بالفعل. استخدم `wb.Names["Sales"]?.RefersTo = "...";` للتحديث بدلاً من ذلك. |

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بمسار فعلي على جهازك.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");

        // Add a defined name (named range) that points to cell A1 on Sheet1
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");

        // Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");

        // Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

**النتيجة المتوقعة:**  

- `output.xlsx` يحتوي على اسم جديد **Sales** يشير إلى `Sheet1!A1`.  
- الخلية **B1** تعرض قيمة **A1** زائد `10`.  
- الملف متوافق تمامًا مع Excel وGoogle Sheets أو أي مكتبة تفهم النطاقات المسماة.

## الخلاصة

أنت الآن تعرف كيف **تحفظ دفتر عمل Excel**، **تضيف نطاقًا مسمى**، **تنشئ اسمًا معرفًا**، وت **استخدام صيغ الاسم المعرف** باستخدام Aspose.Cells في C#. الخطوات بسيطة: تحميل، تسمية، إشارة، وحفظ.

من هنا يمكنك التوسع إلى:  

- إنشاء نطاقات ديناميكية باستخدام دوال `OFFSET`.  
- تطبيق نفس الاسم عبر عدة أوراق (`Scope = Worksheet`).  
- إنشاء آلاف النطاقات المسماة لنماذج مالية معقدة.

جرّبه، عدّل الإشارة، أو أدخل الاسم في جدول محوري—إمكانات الأتمتة لديك لا حدود لها تقريبًا.

---

![Save Excel Workbook flowchart](excel-workflow.png){: .align-center alt="مخطط تدفق حفظ دفتر عمل Excel"}

*هل أنت مستعد لأتمتة تقارير Excel الخاصة بك؟ اترك تعليقًا، شارك تعديلاتك، أو استنسخ المستودع على GitHub. برمجة سعيدة!*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء وحفظ دفتر عمل Excel Aspose Cells Dotnet](/cells/english/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [كيفية إنشاء وحفظ دفتر عمل Excel كملف ODS باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [إنشاء وحفظ دفتر عمل Excel بصيغة PDF Aspnet Aspose Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}