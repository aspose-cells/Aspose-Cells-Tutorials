---
category: general
date: 2026-05-23
description: إنشاء ملف Excel من JSON في C# بسرعة. تعلّم كيفية تحميل JSON إلى Excel،
  وإنشاء دفتر عمل Excel برمجيًا، وحفظ دفتر العمل إلى ملف.
draft: false
keywords:
- generate excel from json
- load json into excel
- save workbook to file
- create excel workbook programmatically
language: ar
og_description: إنشاء ملف Excel من JSON باستخدام C#. يوضح هذا الدليل كيفية تحميل JSON
  إلى Excel، وإنشاء دفتر عمل Excel برمجيًا، وحفظ دفتر العمل إلى ملف.
og_title: إنشاء إكسل من JSON باستخدام C# – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Generate Excel from JSON in C# quickly. Learn how to load JSON into
    Excel, create Excel workbook programmatically, and save workbook to file.
  headline: Generate Excel from JSON with C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- JSON
- Excel Automation
title: إنشاء إكسل من JSON باستخدام C# – دليل خطوة بخطوة كامل
url: /ar/net/data-loading-and-parsing/generate-excel-from-json-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# توليد ملف Excel من JSON باستخدام C# – دليل شامل خطوة بخطوة

هل تساءلت يوماً كيف **تولّد ملف Excel من JSON** دون فتح Excel يدوياً؟ لست وحدك. يحتاج العديد من المطورين إلى تحويل استجابات API أو ملفات التكوين أو تفريغ بيانات بسيطة إلى جداول جاهزة للاستخدام — بسرعة، موثوقية، ودون تفاعل المستخدم.  

في هذا الدرس سنستعرض حلاً نظيفاً من البداية إلى النهاية **يقوم بتحميل JSON إلى Excel**، يبني مصنف العمل بالكامل عبر الكود، وأخيراً **يحفظ المصنف إلى ملف**. بنهاية الدرس ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET.

> **نصيحة محترف:** النهج يعمل مع أي بنية JSON يمكن تمثيلها بجدول مسطح. بالنسبة للكائنات المتداخلة سنناقش حلاً سريعاً لاحقاً.

---

## ما الذي ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+).  
- **Aspose.Cells for .NET** – المكتبة التي تشغل محرك Smart Marker الذي سنستخدمه.  
- حمولة JSON (المثال يستخدم قائمة طلبات صغيرة).  
- بيئة التطوير المفضلة لديك (Visual Studio، Rider، أو VS Code).  

لا توجد أدوات طرف ثالث أخرى مطلوبة؛ كل شيء يعمل في الذاكرة.

---

## الخطوة 1 – إنشاء مصنف Excel برمجياً

أول شيء تقوم به أي أتمتة Excel هو إنشاء كائن مصنف. فكر فيه كقماش فارغ يمكنك الرسم عليه.

```csharp
using Aspose.Cells;          // Excel manipulation
using Aspose.Cells.Tables;   // Smart Marker support
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();
```

لماذا ننشئ المصنف عبر الكود؟ لأنه يضمن أن **الملف يُنشأ برمجياً**، يتجنب مشاكل التزامن على نظام الملفات، ويسمح لك بتشغيل كامل الخط الأنابيب على خادم دون واجهة مستخدم.

---

## الخطوة 2 – إدراج عنصر نائب Smart Marker

Smart Markers هي إجابة Aspose على دمج البريد للجدوال. بوضع عنصر نائب واحد مثل `${Orders:ArrayAsSingle}` في خلية، تعرف المكتبة كيفية توسيع مصفوفة JSON إلى صفوف تلقائياً.

```csharp
        // Step 2: Put a Smart Marker into cell A1 (first worksheet, first cell)
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");
```

إذا كنت جديداً على Smart Markers، تخيل كتابة `${Orders:ArrayAsSingle}` كعلامة قالب تقول “عند رؤيتك لهذا، ضع كل عنصر من مجموعة *Orders* كصف منفصل”.

---

## الخطوة 3 – ربط SmartMarkerProcessor

المعالج هو المحرك الذي يقرأ العنصر النائب، يحلل JSON، ويملأ الورقة.

```csharp
        // Step 3: Initialise the processor with the workbook we just prepared
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

لماذا لا نستدعي `Workbook.Save` مباشرةً؟ لأن البيانات لم تُضاف بعد. المعالج يجسر الفجوة بين JSON الخام وتخطيط Excel.

---

## الخطوة 4 – تعريف بيانات JSON للتحميل

إليك مصفوفة JSON صغيرة تمثل طلبين. في سيناريو واقعي قد تجلبها من API REST، تقرأها من ملف، أو تبنيها في الوقت الفعلي.

```csharp
        // Step 4: JSON that will populate the Smart Marker
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";
```

لاحظ أننا حافظنا على JSON **مسطح** — كل كائن يحتوي فقط على حقول بدائية. هذا يتطابق مع نمط “تحميل JSON إلى Excel” بأكثر صورة نظيفة. إذا كان لديك كائنات متداخلة، ستحتاج إلى تسطيحها أولاً (انظر *النصيحة المتقدمة* في النهاية).

---

## الخطوة 5 – تطبيق JSON على المصنف

الآن يحدث السحر. المعالج يقرأ JSON، يوسع Smart Marker، ويكتب صفوفاً لكل كائن.

```csharp
        // Step 5: Apply JSON – the Smart Marker expands automatically
        processor.ApplyJson(jsonData);
```

خلف الكواليس، تقوم Aspose بإنشاء جدول بيانات مؤقت، تربط كل خاصية (`Id`, `Total`) بعمود، وتدرج الصفوف مباشرةً أسفل العنصر النائب. لا حلقات، لا عنونة خلايا يدوية — مجرد تحويل إعلاني.

---

## الخطوة 6 – حفظ المصنف إلى ملف

أخيراً، نقوم بحفظ المصنف المملوء إلى القرص.

```csharp
        // Step 6: Save the populated workbook to a physical file
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

خطوة **حفظ المصنف إلى ملف** هي القطعة الأخيرة من اللغز. تقوم Aspose بكتابة ملف `.xlsx` النهائي باستخدام Open XML تحت الغطاء، لذا يكون الملف متوافقاً تماماً مع Excel، Google Sheets، وLibreOffice.

---

## مثال عملي كامل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه وتشغيله. تأكد من تثبيت حزمة NuGet الخاصة بـ Aspose.Cells (`dotnet add package Aspose.Cells`).

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Insert Smart Marker placeholder in cell A1
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");

        // 3️⃣ Initialise SmartMarkerProcessor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 4️⃣ JSON data (could come from a file, API, etc.)
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";

        // 5️⃣ Apply JSON – Smart Marker expands automatically
        processor.ApplyJson(jsonData);

        // 6️⃣ Save the workbook to disk
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### النتيجة المتوقعة

عند فتح `OrdersReport.xlsx` سترى:

| Id | Total |
|----|-------|
| 1  | 99.9  |
| 2  | 45.0  |

عناوين الأعمدة تُنشأ تلقائياً من أسماء خصائص JSON، وكل عنصر في المصفوفة يصبح صفاً جديداً. لا حاجة لعناوين خلايا يدوية.

---

## نصيحة متقدمة – التعامل مع JSON كبير أو متداخل

إذا كان JSON الخاص بك يحتوي على **كائنات متداخلة** (مثلاً `Order` يحتوي على كائن فرعي `Customer`)، لا يزال بإمكان Smart Markers المساعدة لكن سيتعين عليك تسطيح البنية أولاً:

```csharp
// Example flattening using Newtonsoft.Json.Linq
var jArray = JArray.Parse(jsonData);
var flatList = jArray.Select(item => new {
    Id = (int)item["Id"],
    Total = (decimal)item["Total"],
    CustomerName = (string)item["Customer"]["Name"]
}).ToList();
string flatJson = JsonConvert.SerializeObject(flatList);
processor.ApplyJson(flatJson);
```

هذا النهج يحافظ على سلاسة تدفق **تحميل JSON إلى Excel** حتى مع البيانات المعقدة.

---

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|-------|------------|------|
| **غياب رخصة Aspose.Cells** | النسخة التجريبية تضيف علامة مائية. | احصل على ملف رخصة وسجّله عبر `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |
| **خطأ إملائي في العنصر النائب** | علامات Smart Marker حساسة لحالة الأحرف. | تحقق من تهجئة `${Orders:ArrayAsSingle}` والأقواس. |
| **JSON كبير يسبب ضغطاً على الذاكرة** | يتم تحميل كامل JSON إلى RAM. | قم ببث JSON أو معالجته على دفعات، ثم دمج الأوراق. |
| **عدم توافق تنسيق التاريخ** | تواريخ JSON تظهر كقيمة ticks خام. | استخدم `JsonSerializerSettings` لتنسيق التواريخ، أو أضف تنسيق عمود مخصص بعد المعالجة. |

---

## لماذا هذه الطريقة تتفوق على التكرار اليدوي

- **إعلاني**: تصف *ما* تريد (جدول) بدلاً من *كيف* تكرّر الصفوف.  
- **الأداء**: Smart Markers تستخدم مخازن داخلية محسّنة، غالباً أسرع من حلقات `for` البسيطة.  
- **قابلية الصيانة**: تغيير مصدر البيانات (CSV، قاعدة بيانات، API) يتطلب فقط استبدال سلسلة JSON — لا تغييرات في منطق Excel.  
- **القابلية للتوسع**: يمكن إعادة استخدام القالب نفسه لعشرات التقارير بأشكال بيانات مختلفة.

---

## الخلاصة

لقد استعرضنا كيف **نولد Excel من JSON** في C# عبر **تحميل JSON إلى Excel**، **إنشاء مصنف Excel برمجياً**، وأخيراً **حفظ المصنف إلى ملف**. يعمل الخط الأنابيب بالكامل في الذاكرة، يحتاج إلى بضع أسطر من الكود فقط، وينتج جدولاً نظيفاً جاهزاً للمشاركة.

هل تريد التعمق أكثر؟ جرّب إضافة تنسيق شرطي، إدراج مخططات، أو تصدير مباشرة إلى PDF — كل ذلك ممكن باستخدام كائن `Workbook` نفسه. الفكرة الأساسية: Smart Markers تحول JSON إلى جداول Excel مع تقريباً لا وجود للشفرة المتكررة.

هل لديك أسئلة حول معالجة بنى JSON معينة أو تعديل تنسيق الإخراج؟ اترك تعليقاً أو اطرح سؤالك في المناقشة أدناه. برمجة سعيدة!

---

![توليد Excel من JSON باستخدام C# – لقطة شاشة لملف OrdersReport.xlsx](/images/generate-excel-from-json.png "توليد excel من json")

*نص بديل للصورة:* توليد excel من json – النتيجة البصرية للدرس.

## دروس ذات صلة

- [كيفية إنشاء وحفظ مصنف Excel كملف ODS باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [إنشاء وحفظ مصنف Excel كملف PDF في ASP.NET باستخدام Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [استيراد بيانات JSON إلى Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}