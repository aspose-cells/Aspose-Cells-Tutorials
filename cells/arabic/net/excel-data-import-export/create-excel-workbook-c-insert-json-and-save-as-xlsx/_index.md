---
category: general
date: 2026-03-30
description: إنشاء مصنف إكسل باستخدام C# بسرعة عن طريق إدراج بيانات JSON وحفظ المصنف
  بصيغة XLSX. تعلم كيفية توليد إكسل من JSON، كتابة JSON إلى إكسل، وإدراج JSON في إكسل.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsx
- generate excel from json
- write json to excel
- insert json into excel
language: ar
og_description: إنشاء مصنف إكسل باستخدام C# بسرعة عن طريق إدراج بيانات JSON وحفظ المصنف
  بصيغة XLSX. اتبع هذا الدليل خطوة بخطوة لتوليد إكسل من JSON.
og_title: إنشاء دفتر عمل Excel باستخدام C# – إدراج JSON وحفظه كملف XLSX
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف إكسل C# – إدراج JSON وحفظه كملف XLSX
url: /ar/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel C# – إدراج JSON وحفظه كـ XLSX

هل احتجت يومًا إلى **create Excel workbook C#** وإسقاط بعض JSON مباشرةً في خلية؟ لست الوحيد—غالبًا ما يواجه المطورون نفس اللغز عندما يكون لديهم حمولات API أو ملفات تكوين تحتاج إلى الوصول إلى جدول بيانات للتقارير أو المشاركة.  

الخبر السار هو أنه باستخدام Aspose.Cells يمكنك القيام بذلك في بضع أسطر، **save workbook as XLSX**، والحفاظ على العملية بأكملها آمنة من حيث النوع. في هذا الدرس سنقوم **generate Excel from JSON**، **write JSON to Excel**، ونظهر لك الخطوات الدقيقة لـ **insert JSON into Excel** دون أي عمليات دمج سلاسل معقدة.

## ما يغطيه هذا الدليل

سنستعرض:

1. إعداد مصنف جديد.
2. إضافة Smart Marker يتوقع JSON.
3. تمرير مصفوفة JSON إلى العلامة.
4. تعديل `SmartMarkerOptions` بحيث يبقى JSON في خلية واحدة.
5. حفظ الملف كمصنف XLSX.

بنهاية الدليل ستحصل على ملف `JsonSingleCell.xlsx` جاهز للاستخدام ونمط ثابت يمكنك إعادة استخدامه لأي سيناريو JSON‑to‑Excel. لا خدمات خارجية، فقط C# عادي ومكتبة Aspose.Cells.

**المتطلبات المسبقة**

- .NET 6+ (أو .NET Framework 4.6+).  
- Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.  
- حزمة NuGet `Aspose.Cells` (نسخة تجريبية مجانية أو مرخصة).  

إذا كان لديك ذلك، هيا نبدأ—لا حاجة لإعداد إضافي.

---

## الخطوة 1: إنشاء مصنف جديد في C#

أول شيء تحتاجه هو كائن مصنف فارغ. فكر فيه كملف Excel جديد ينتظر البيانات.

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is your empty Excel file
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

**لماذا هذا مهم:**  
`Workbook` هو نقطة الدخول لجميع عمليات Excel. بإنشائه أولًا، تضمن أن استدعاء **save workbook as xlsx** التالي يمتلك كائنًا ملموسًا لتسلسله.

> **نصيحة احترافية:** إذا كنت تخطط للعمل مع عدة أوراق، يمكنك إضافتها الآن باستخدام `workbook.Worksheets.Add()`.

## الخطوة 2: وضع Smart Marker يتوقع JSON

Smart Markers هي نواقل مكانية تقوم Aspose.Cells باستبدالها أثناء التشغيل. هنا نخبرها بالبحث عن سلسلة JSON باسم `data`.

```csharp
// Put a Smart Marker in cell A1 – {{data:json}} tells Aspose to expect JSON
worksheet.Cells["A1"].PutValue("{{data:json}}");
```

**لماذا هذا مهم:**  
لاحقة `:json` تخبر المحرك أن القيمة الواردة هي JSON، ليست نصًا عاديًا. هذا هو المفتاح لـ **write json to excel** دون تحليل يدوي.

## الخطوة 3: تعريف مصفوفة JSON

الآن نقوم بصنع JSON الذي نريد إدراجه. للعرض سنستخدم قائمة بسيطة من الأشخاص.

```csharp
// Sample JSON array – could come from an API, file, or DB
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";
```

**حالة خاصة:**  
إذا كان JSON الخاص بك يحتوي على علامات اقتباس مزدوجة، تأكد من هروبها (كما هو موضح) أو استخدم سلسلة حرفية (`@"..."`) لتجنب أخطاء التجميع.

## الخطوة 4: ضبط خيارات Smart Marker – الحفاظ على المصفوفة كاملة

بشكل افتراضي، ستحاول Aspose توسيع المصفوفة عبر الصفوف. نريد أن يبقى سلسلة JSON كاملة داخل خلية واحدة، وهو مثالي لسيناريوهات **insert json into excel** حيث سيقوم المستهلك بتحليل JSON لاحقًا.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Treat the whole array as a single cell value
    ArrayAsSingle = true
};
```

**لماذا هذا مهم:**  
`ArrayAsSingle = true` يمنع توسيع الصفوف، مما يمنحك كتلة JSON نظيفة داخل خلية واحدة. هذا أساسي عندما يكون جدول البيانات صيغة نقل وليس تقريرًا.

## الخطوة 5: معالجة Smart Marker ببيانات JSON

الآن نقوم بربط JSON بالعلامة ونترك Aspose تقوم بالعمل الشاق.

```csharp
// Process the marker – the anonymous object maps "data" to our JSON string
worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);
```

**ما يحدث خلف الكواليس:**  
تقوم Aspose بتقييم النواقل `{{data:json}}`، تسلسل سلسلة `jsonData`، وتكتبها في الخلية A1 مع احترام الخيارات التي حددناها.

## الخطوة 6: حفظ المصنف كملف XLSX

أخيرًا، نكتب المصنف إلى القرص. هنا يأتي دور **save workbook as xlsx**.

```csharp
// Save the workbook – the extension determines the format (XLSX here)
workbook.Save("JsonSingleCell.xlsx");
```

**النتيجة:**  
افتح `JsonSingleCell.xlsx` في Excel، وسترى مصفوفة JSON بالضبط كما عرّفناها، موجودة بشكل منظم في الخلية A1.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق console. يتضمن جميع الخطوات السابقة ويعمل مباشرةً (بافتراض تثبيت حزمة Aspose.Cells عبر NuGet).

```csharp
using System;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add a Smart Marker that expects JSON
            worksheet.Cells["A1"].PutValue("{{data:json}}");

            // 3️⃣ Define the JSON array
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Jane\",\"Age\":28}]";

            // 4️⃣ Configure options – keep array as a single cell value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 5️⃣ Process the marker with the JSON payload
            worksheet.SmartMarkers.Process(new { data = jsonData }, smartMarkerOptions);

            // 6️⃣ Save the workbook as XLSX
            workbook.Save("JsonSingleCell.xlsx");

            Console.WriteLine("Excel file created successfully! Check JsonSingleCell.xlsx.");
        }
    }
}
```

**الناتج المتوقع في Excel**

| A |
|---|
| `[{"Name":"John","Age":30},{"Name":"Jane","Age":28}]` |

تحتوي تلك الخلية الآن على مصفوفة JSON صالحة تمامًا جاهزة للمعالجة اللاحقة.

## أسئلة شائعة وحالات خاصة

### ماذا لو أردت توزيع JSON عبر الصفوف؟

اضبط `ArrayAsSingle = false` (الإعداد الافتراضي). ستقوم Aspose بإنشاء صف لكل عنصر في المصفوفة، وتعيين خصائص الكائن إلى الأعمدة. هذا مفيد عندما تريد عرضًا جدوليًا بدلاً من سلسلة JSON خام.

### هل يمكنني استخدام ملف JSON بدلاً من سلسلة مشفرة صلبة؟

بالطبع. اقرأ الملف إلى سلسلة:

```csharp
string jsonData = File.ReadAllText("people.json");
```

ثم مرر `jsonData` إلى نفس استدعاء `Process`. يبقى باقي خط الأنابيب دون تغيير.

### هل يعمل هذا مع حمولات JSON الكبيرة؟

نعم، لكن راقب استهلاك الذاكرة. بالنسبة للمصفوفات الضخمة، فكر في تدفق البيانات أو الكتابة مباشرةً إلى الصفوف (`ArrayAsSingle = false`) لتجنب خلية واحدة ضخمة قد تواجه Excel صعوبة في التعامل معها.

### هل ملف XLSX المُولد متوافق مع إصدارات Excel القديمة؟

تنسيق `.xlsx` مبني على Office Open XML ويعمل مع Excel 2007 وما بعده. إذا كنت تحتاج إلى تنسيق `.xls` القديم، غيّر استدعاء الحفظ:

```csharp
workbook.Save("JsonSingleCell.xls", SaveFormat.Excel97To2003);
```

## نصائح احترافية للعمل مع JSON وExcel

- **Validate JSON first** – استخدم `System.Text.Json.JsonDocument.Parse(jsonData)` لاكتشاف الإدخال غير الصحيح مبكرًا.  
- **Escape special characters** – إذا كان JSON يحتوي على فواصل أسطر، ستظهر كـ `\n` حرفيًا في الخلية؛ يمكنك استبدالها بـ `Environment.NewLine` قبل المعالجة.  
- **Reuse Smart Markers** – يمكنك وضع عدة علامات في نفس الورقة، كل واحدة تشير إلى خاصية JSON مختلفة.  
- **Combine with formulas** – بمجرد أن يكون JSON في خلية، يمكنك استخدام `FILTERXML` في Excel (في الإصدارات الأحدث) لتحليله مباشرةً.  

## الخلاصة

أنت الآن تعرف كيف **create excel workbook c#**، وتضمين حمولة JSON، و**save workbook as xlsx** باستخدام Aspose.Cells. يتيح لك هذا النمط **generate excel from json**، **write json to excel**، و**insert json into excel** ببضع أسطر من الشيفرة فقط، مما يجعل تبادل البيانات بين الخدمات والمحللين سهلًا.  

هل أنت مستعد للخطوة التالية؟ جرّب تحويل مصفوفة JSON إلى جدول مناسب (اضبط `ArrayAsSingle = false`) أو استكشف تنسيق الورقة بعد الإدراج. نفس النهج يعمل مع CSV، XML، أو حتى كائنات مخصصة—فقط عدل نوع Smart Marker.  

برمجة سعيدة، ولا تتردد في التجربة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو اطلع على الوثائق الرسمية لـ Aspose لمزيد من التفاصيل حول Smart Markers.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}