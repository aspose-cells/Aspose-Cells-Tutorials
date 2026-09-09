---
category: general
date: 2026-02-23
description: إنشاء مصنف جديد وتعلم كيفية استيراد ملفات ماركداون إلى إكسل. يوضح هذا
  الدليل كيفية تحميل ملف ماركداون وتحويله إلى إكسل بخطوات سهلة.
draft: false
keywords:
- create new workbook
- how to import markdown
- load markdown file
- how to create workbook
- convert markdown to excel
language: ar
og_description: إنشاء مصنف جديد واستيراد markdown في C#. اتبع هذا الدليل خطوة بخطوة
  لتحميل ملف markdown وتحويل markdown إلى Excel.
og_title: إنشاء مصنف جديد في C# – استيراد Markdown إلى Excel
tags:
- C#
- Excel automation
- Markdown processing
title: إنشاء دفتر عمل جديد في C# – استيراد Markdown إلى Excel
url: /ar/net/conversion-and-rendering/create-new-workbook-in-c-import-markdown-to-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد في C# – استيراد Markdown إلى Excel

هل تساءلت يوماً كيف **تنشئ دفتر عمل جديد** من مصدر Markdown دون أن تفقد أعصابك؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تحويل وثائق نصية بسيطة إلى ورقة Excel منسقة بشكل جميل، خاصةً عندما تكون البيانات موجودة في ملف `.md`.  

في هذا الدرس سنستعرض ذلك خطوة بخطوة: سن **ننشئ دفتر عمل جديد**، نُظهر لك **كيفية استيراد markdown**، وسنحصل في النهاية على ملف Excel يمكنك فتحه في أي برنامج جداول. لا توجد واجهات برمجة تطبيقات غامضة، فقط كود C# واضح، وتفسيرات لأهمية كل سطر، وبعض النصائح الاحترافية لتجنب الأخطاء الشائعة.

بنهاية هذا الدليل ستعرف كيف **تحمّل ملف markdown**، وتفهم **كيفية إنشاء دفتر عمل** برمجياً، وستكون جاهزاً **لتحويل markdown إلى Excel** لأغراض التقارير، تحليل البيانات، أو التوثيق. المتطلب الوحيد هو وجود بيئة تشغيل .NET حديثة ومكتبة تدعم `Workbook.ImportFromMarkdown` (سنستخدم المكتبة المفتوحة المصدر *GemBox.Spreadsheet* في الأمثلة).

---

## ما الذي ستحتاجه

- **.NET 6** أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضاً)  
- حزمة NuGet **GemBox.Spreadsheet** (الإصدار المجاني يكفي لهذا العرض)  
- ملف Markdown (`input.md`) يحتوي على جدول أو قائمة بسيطة تريد تحويلها إلى ورقة Excel  
- أي بيئة تطوير تفضلها—Visual Studio، VS Code، Rider—لا يهم

> **نصيحة احترافية:** إذا كنت تعمل على نظام Linux، فإن الخطوات نفسها تعمل مع سطر أوامر `dotnet`؛ فقط قم بتثبيت حزمة NuGet بشكل عالمي.

---

## الخطوة 1: تثبيت مكتبة الجداول

قبل أن نتمكن من **إنشاء دفتر عمل جديد**، نحتاج إلى فئة تعرف كيفية التعامل مع الجداول. توفر مكتبة GemBox.Spreadsheet نوع `Workbook` مع طريقة `ImportFromMarkdown`، مما يجعل جزء **كيفية استيراد markdown** سهلًا للغاية.

```bash
dotnet add package GemBox.Spreadsheet --version 58.0
```

هذا السطر الواحد يجلب المكتبة وكل تبعياتها. بعد انتهاء الاستعادة، تكون جاهزًا لكتابة الكود.

---

## الخطوة 2: إعداد هيكل المشروع

أنشئ تطبيقًا سطحيًا (Console) جديدًا (أو ضع الكود في مشروع موجود). إليك ملف `Program.cs` بسيط يحتوي على كل ما نحتاجه.

```csharp
using System;
using GemBox.Spreadsheet;   // Namespace for Workbook, etc.

class Program
{
    static void Main()
    {
        // License key for the free version – remove for the paid version.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // Step 2.1: Create a new workbook
        // This is where we actually **create new workbook**.
        var workbook = new Workbook();

        // Step 2.2: Import markdown content
        // The path can be absolute or relative; here we assume the file lives next to the exe.
        string markdownPath = "input.md";

        // Guard against missing files – a common edge case when you **load markdown file**.
        if (!System.IO.File.Exists(markdownPath))
        {
            Console.WriteLine($"Error: '{markdownPath}' not found. Make sure the file exists.");
            return;
        }

        // The ImportFromMarkdown method parses tables and lists into worksheet cells.
        workbook.ImportFromMarkdown(markdownPath);

        // Step 2.3: Save the workbook as an Excel file
        // This completes the **convert markdown to Excel** workflow.
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Success! Workbook created at '{outputPath}'.");
    }
}
```

### لماذا هذا مهم

- **`SpreadsheetInfo.SetLicense`** – حتى النسخة المجانية تحتاج إلى مفتاح placeholder؛ وإلا ستواجه استثناءً وقت التشغيل.  
- **`new Workbook()`** – هذا السطر **ينشئ دفتر عمل جديد** في الذاكرة. فكر فيه كقماش فارغ سيحمل لاحقًا البيانات المستخرجة من Markdown.  
- **`ImportFromMarkdown`** – هذا هو جوهر **كيفية استيراد markdown**. الطريقة تقرأ الجداول (`| Header |`) والقوائم النقطية، وتحول كل خلية إلى خلية في الجدول.  
- **التحقق من وجود الملف** – تخطي هذا الفحص قد يسبب استثناء `FileNotFoundException`، وهو مصدر شائع للإحباط عند **تحميل ملف markdown** من مسار نسبي.  
- **`Save`** – أخيرًا نقوم **بتحويل markdown إلى Excel** عن طريق حفظ دفتر العمل الموجود في الذاكرة إلى `output.xlsx`.

---

## الخطوة 3: إعداد ملف Markdown تجريبي

لرؤية العملية تعمل، أنشئ ملف `input.md` في نفس المجلد الذي يحتوي على الملف التنفيذي المترجم. إليك مثالًا بسيطًا يتضمن جدولًا وقائمة نقطية:

```markdown
# Sales Report Q1

| Product | Units Sold | Revenue |
|---------|------------|---------|
| Widget A | 120 | $1,200 |
| Widget B | 85  | $850   |
| Widget C | 60  | $600   |

- Note: All figures are in USD.
- Data collected from the internal CRM.
```

عند تشغيل البرنامج، سيقوم GemBox بترجمة الجدول إلى ورقة عمل ويضع النقاط النقطية أسفله، مع الحفاظ على التسلسل الهرمي للنص.

---

## الخطوة 4: تشغيل التطبيق والتحقق من النتيجة

قم بترجمة البرنامج وتنفيذه:

```bash
dotnet run
```

يجب أن ترى:

```
Success! Workbook created at 'output.xlsx'.
```

افتح `output.xlsx` في Excel أو Google Sheets أو LibreOffice Calc. ستجد:

| المنتج   | الوحدات المباعة | الإيرادات |
|----------|----------------|-----------|
| Widget A | 120            | $1,200    |
| Widget B | 85             | $850      |
| Widget C | 60             | $600      |

أسفل الجدول، تظهر النقطتان في العمود الأول، مما يمنحك تمثيلًا دقيقًا للـ Markdown الأصلي.

---

## الخطوة 5: خيارات متقدمة وحالات حافة

### 5.1 استيراد ملفات Markdown متعددة

إذا كنت بحاجة إلى **تحميل ملفات markdown** من مجلد ودمجها في دفتر عمل واحد، ما عليك سوى التكرار عبر الملفات:

```csharp
foreach (var mdFile in System.IO.Directory.GetFiles("MarkdownFolder", "*.md"))
{
    var ws = workbook.Worksheets.Add(System.IO.Path.GetFileNameWithoutExtension(mdFile));
    ws.ImportFromMarkdown(mdFile);
}
```

كل ملف يحصل على ورقة عمل خاصة به، مما يجعل عملية **تحويل markdown إلى Excel** قابلة للتوسع.

### 5.2 تخصيص أسماء أوراق العمل

بشكل افتراضي تُنشئ `ImportFromMarkdown` ورقة باسم “Sheet1”. يمكنك إعادة تسميتها لتوضيح المحتوى:

```csharp
workbook.Worksheets[0].Name = "Q1 Sales";
```

### 5.3 التعامل مع الملفات الكبيرة

عند التعامل مع مستندات Markdown ضخمة، فكر في تدفق الملف بدلاً من تحميله بالكامل مرة واحدة. حاليًا تتوقع GemBox مسار ملف، لكن يمكنك معالجة الـ markdown إلى أجزاء أصغر واستيراد كل جزء إلى ورقة عمل منفصلة.

### 5.4 تنسيق الخلايا بعد الاستيراد

المكتبة تستورد النص الخام؛ إذا أردت تنسيقات أرقام صحيحة أو عناوين غامقة، يمكنك إجراء معالجة لاحقة:

```csharp
var ws = workbook.Worksheets[0];
ws.Rows[0].Style.Font.Weight = ExcelFont.BoldWeight; // Header row bold
ws.Columns[1].Style.NumberFormat = "0";               // Units Sold as integer
ws.Columns[2].Style.NumberFormat = "$#,##0";         // Revenue as currency
```

هذه التعديلات تجعل ملف Excel النهائي يبدو مصقولًا، وهو ما يُطلب غالبًا في التقارير الموجهة للعملاء.

---

## الخطوة 6: الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|---------|-------|------|
| **ملف Markdown مفقود** | تختلف المسارات النسبية عند التشغيل من IDE مقابل سطر الأوامر. | استخدم `Path.GetFullPath` أو ضع الملف في نفس دليل الملف التنفيذي. |
| **صيغة جدول غير صحيحة** | تحتاج جداول Markdown إلى فواصل `|` وسطر فاصل رأس (`---`). | تحقق من الـ markdown باستخدام عارض على الإنترنت قبل الاستيراد. |
| **خطأ في تفسير نوع البيانات** | قد تُقرأ الأرقام كسلاسل نصية، خاصةً عند وجود فواصل. | بعد الاستيراد، عدل `NumberFormat` للعمود كما هو موضح في الخطوة 5.3. |
| **عدم تعيين مفتاح الترخيص** | يرمي GemBox استثناءً إذا لم يتم تكوين الترخيص. | احرص على استدعاء `SpreadsheetInfo.SetLicense` في بداية البرنامج. |

---

## الخطوة 7: مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج الكامل الذي يمكنك وضعه في مشروع Console جديد. يتضمن جميع الخطوات، معالجة الأخطاء، وروتين بسيط لمعالجة ما بعد الاستيراد يجعل صف العنوان غامقًا.

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Free license – replace with your key for unlimited rows/columns.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Create a new workbook
        var workbook = new Workbook();

        // 2️⃣ Define the markdown file path
        string markdownPath = "input.md";

        // 3️⃣ Verify the file exists (prevents a crash when you load markdown file)
        if (!File.Exists(markdownPath))
        {
            Console.WriteLine($"Error: Markdown file '{markdownPath}' not found.");
            return;
        }

        // 4️⃣ Import the markdown content – this is the core of how to import markdown
        workbook.ImportFromMarkdown(markdownPath);

        // 5️⃣ Optional: make the header row bold
        var sheet = workbook.Worksheets[0];
        sheet.Rows[0].Style.Font.Weight = ExcelFont.BoldWeight;

        // 6️⃣ Save as Excel – final step of convert markdown to Excel
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook created successfully at '{outputPath}'.");
    }
}
```

شغّله، افتح `output.xlsx`، وسترى جدولًا منسقًا بالكامل مستخرجًا من مصدر Markdown الخاص بك.

---

## الخلاصة

لقد أظهرنا لك الآن كيفية **إنشاء دفتر عمل جديد** في C# واستيراد محتوى **ملف markdown** إليه بسلاسة، أي **تحويل markdown إلى Excel**. العملية تختصر في ثلاث خطوات بسيطة: إنشاء كائن `Workbook`، استدعاء `ImportFromMarkdown`، ثم `Save` للنتيجة.  

إذا كنت تتساءل **كيف تستورد markdown** لهياكل أكثر تعقيدًا—مثل القوائم المتداخلة أو كتل الشيفرة—جرّب خيارات `ImportOptions` المتاحة في النسخة المدفوعة أو قم بمعالجة الـ Markdown يدويًا قبل تمريره إلى دفتر العمل.  

الخطوات التالية التي قد تستكشفها:

- **كيفية إنشاء دفتر عمل** يحتوي على أوراق عمل متعددة للمعالجة الدفعة  
- أتمتة سير العمل باستخدام خط أنابيب CI/CD لتوليد التقارير مع كل دفع (push)  
- استخدام صيغ أخرى (CSV، JSON) جنبًا إلى جنب مع Markdown لاستراتيجية استيعاب بيانات موحدة  

جرّب ذلك، عدّل التنسيقات، ودع أتمتة الجداول تقوم بالعمل الشاق نيابةً عنك. هل لديك أسئلة أو ملف Markdown غريب يرفض الاستيراد؟ اترك تعليقًا أدناه—برمجة سعيدة!  

![Diagram illustrating the flow from Markdown file to Excel workbook

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}