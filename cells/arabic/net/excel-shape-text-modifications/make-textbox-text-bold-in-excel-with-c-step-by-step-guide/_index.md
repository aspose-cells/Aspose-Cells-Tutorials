---
category: general
date: 2026-02-21
description: تعلم كيفية جعل نص TextBox غامقًا، وتغيير حجم خط TextBox، وتحميل دفتر
  عمل Excel باستخدام C# و Aspose.Cells في مثال كامل قابل للتنفيذ.
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: ar
og_description: اجعل نص TextBox غامقًا في ملف Excel باستخدام C#. يوضح هذا الدرس أيضًا
  كيفية تغيير حجم خط TextBox وتحميل دفتر عمل Excel باستخدام C# مع Aspose.Cells.
og_title: اجعل نص مربع النص غامقًا في Excel باستخدام C# – دليل كامل
tags:
- C#
- Aspose.Cells
- Excel automation
title: اجعل نص مربع النص غامقًا في إكسل باستخدام C# – دليل خطوة بخطوة
url: /ar/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

final Arabic version.

Be careful with markdown headings.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# جعل نص الـ TextBox غامق في Excel باستخدام C# – دليل خطوة بخطوة

هل تحتاج إلى **جعل نص الـ TextBox غامق** في ملف Excel باستخدام C#؟ في هذا الدرس سنوضح لك بالضبط كيفية *تحميل دفتر عمل Excel*، **تغيير حجم خط الـ TextBox**، وتنسيق نص الشكل باستخدام Aspose.Cells.  
إذا سبق لك أن نظرت إلى جدول بيانات ممل وفكرت “يجب أن يبرز الـ TextBox الخاص بي”، فأنت في المكان الصحيح.

سنستعرض كل سطر من الشيفرة، نشرح لماذا كل استدعاء مهم، وحتى نتناول ما يجب فعله عندما لا يحتوي ورقة العمل على أي TextBox على الإطلاق. في النهاية ستحصل على مقطع شفرة قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET—دون الحاجة إلى روابط “انظر الوثائق” الغامضة.

## ما ستحتاجه

- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو نسخة مرخصة) – الـ API الذي نستخدمه للتعامل مع أشكال Excel.  
- .NET 6 أو أحدث (الشيفرة تعمل أيضاً مع .NET Framework 4.7+).  
- ملف Excel بسيط (`input.xlsx`) يحتوي بالفعل على صندوق نص واحد على الأقل في الورقة الأولى.  

هذا كل ما تحتاجه. لا حزم NuGet إضافية، لا تفاعل COM، فقط C# صافية.

## جعل نص الـ TextBox غامق – تحميل دفتر العمل والوصول إلى الشكل

الخطوة الأولى هي فتح دفتر العمل والحصول على الـ TextBox الذي نريد تحريره.  
نقوم أيضاً بإجراء فحص أمان سريع حتى لا تتعطل الشيفرة إذا كانت الورقة فارغة.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**لماذا هذا مهم:**  
*تحميل دفتر العمل* يمنحنا كائن `Workbook` يمثل الملف بالكامل في الذاكرة. الوصول إلى `Worksheets[0]` آمن لأن كل ملف Excel يحتوي على ورقة واحدة على الأقل. شرط الحماية (`if (worksheet.TextBoxes.Count == 0)`) يمنع حدوث `IndexOutOfRangeException`—وهو خطأ شائع عند أتمتة الملفات الموجودة.

## تغيير حجم خط الـ TextBox

قبل أن نجعل النص غامقاً، دعنا نتأكد من أن الحجم هو بالضبط ما تحتاجه.  
تغيير الحجم بسيط كضبط خاصية `Font.Size`.

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**نصيحة احترافية:**  
إذا كنت تحتاج إلى حجم ديناميكي يعتمد على إدخال المستخدم، استبدل `12` بمتغير. كائن `Font` مشترك عبر الشكل بأكمله، لذا فإن تغيير الحجم يؤثر فوراً على كل حرف داخل الـ TextBox.

## جعل نص الـ TextBox غامق – الإجراء الأساسي

الآن إلى الميزة الأساسية: جعل النص غامقاً.  
علامة `IsBold` تغير وزن الخط دون تعديل أي تنسيق آخر.

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**ما الذي يحدث في الخلفية؟**  
Aspose.Cells يخزن تنسيق النص في كائن `Font` مرتبط بالشكل. ضبط `IsBold = true` يحدث الـ XML الأساسي (`<b>1</b>`) الذي تقرأه Excel عند عرض الورقة. هذه عملية **غير مدمرة**—إذا عُدت وضعت `IsBold = false`، يعود النص إلى الوزن الطبيعي.

## حفظ دفتر العمل المعدل

بعد إكمال التنسيق، نكتب التغييرات إلى القرص.  
يمكنك استبدال الملف الأصلي أو، كما هو موضح هنا، إنشاء ملف جديد للحفاظ على المصدر دون تعديل.

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**النتيجة المتوقعة:**  
افتح `output.xlsx` في Excel. يجب أن يعرض الـ TextBox الأول في الورقة الأولى نصه بخط **Calibri 12 pt، غامق**. لا تتأثر الأشكال الأخرى.

## تنسيق نص شكل Excel – خيارات تنسيق إضافية (اختياري)

بينما الهدف الأساسي هو **جعل نص الـ TextBox غامق**، قد ترغب أيضاً في:

| الخيار | مقتطف الشيفرة | متى يُستخدم |
|--------|--------------|-------------|
| مائل | `textBox.Font.IsItalic = true;` | لتأكيد عنوان فرعي |
| لون النص | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | ألوان العلامة التجارية |
| المحاذاة | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | عناوين مركزية |
| عدة TextBoxes | حلقة عبر `worksheet.TextBoxes` | تنسيق دفعة |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

هذه التعديلات الإضافية توضح كيف يمكن توسيع *format excel shape text* لتتجاوز مجرد جعل النص غامقاً.

## الحالات الحدية والمشكلات الشائعة

1. **عدم وجود TextBoxes في الورقة** – شرط الحماية الذي أضفناه (`if (worksheet.TextBoxes.Count == 0)`) يخرج البرنامج بأمان ويُعلم المستخدم.  
2. **الأوراق المخفية** – الأوراق المخفية لا تزال قابلة للوصول عبر مجموعة `Worksheets`؛ فقط تأكد من الإشارة إلى الفهرس الصحيح.  
3. **الملفات الكبيرة** – تحميل دفتر عمل ضخم قد يستهلك الذاكرة. فكر في استخدام `Workbook.LoadOptions` لتحميل الأجزاء المطلوبة فقط.  
4. **إصدارات Excel المختلفة** – Aspose.Cells يدعم `.xls`، `.xlsx`، وحتى `.xlsb`. الشيفرة نفسها تعمل عبر جميع الإصدارات، لكن إصدارات Excel القديمة قد تتجاهل بعض ميزات الخط الحديثة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

شغّل البرنامج، افتح `output.xlsx` الناتج، وسترى النص داخل الـ TextBox غامقاً، بخط Calibri 12‑pt. بسيط، أليس كذلك؟

## الخلاصة

الآن تعرف **كيفية جعل نص الـ TextBox غامق** في دفتر عمل Excel باستخدام C#، وكيفية **تغيير حجم خط الـ TextBox**، وأساسيات **تحميل دفتر عمل Excel بـ C#** باستخدام Aspose.Cells. المثال الكامل أعلاه جاهز للإدراج في أي مشروع، وقد رأيت أيضاً طرق **تنسيق نص شكل Excel** للحصول على تنسيقات أغنى.

ما الخطوة التالية؟ جرّب حلقة عبر كل ورقة عمل لجعل جميع الـ TextBoxes غامقة، أو اجمع ذلك مع توليد محتوى مدفوع بالبيانات—مثلاً ملء الـ TextBox بقيم من قاعدة بيانات. المبادئ نفسها تنطبق، والشيفرة تظل نظيفة.

هل لديك تعديل ترغب بمشاركته، أو واجهت خطأ غير متوقع؟ اترك تعليقاً، ولنستمر في النقاش. برمجة سعيدة!

![make textbox text bold in Excel using C#](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}