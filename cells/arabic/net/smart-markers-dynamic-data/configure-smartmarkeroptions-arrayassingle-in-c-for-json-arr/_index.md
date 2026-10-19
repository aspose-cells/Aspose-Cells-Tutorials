---
category: general
date: 2026-09-21
description: قم بتكوين SmartMarkerOptions ArrayAsSingle في C# لتصدير مصفوفات JSON
  كقيمة خلية واحدة في مصنف Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: ar
lastmod: 2026-09-21
og_description: قم بتكوين SmartMarkerOptions ArrayAsSingle في C# لتصدير مصفوفات JSON
  كقيمة خلية واحدة. تعلّم الحل الكامل خطوة بخطوة.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: تكوين SmartMarkerOptions ArrayAsSingle في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: تكوين SmartMarkerOptions ArrayAsSingle في C# لمصفوفات JSON
url: /ar/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تكوين SmartMarkerOptions ArrayAsSingle في C# لمصفوفات JSON

إذا كنت بحاجة إلى **تكوين SmartMarkerOptions ArrayAsSingle** أثناء إنشاء ملفات Excel باستخدام Aspose.Cells، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. سترى كيف تحتفظ بمصفوفة JSON سليمة في خلية واحدة بدلاً من توزيع عناصرها عبر عدة صفوف.

العمل مع بيانات JSON في جداول البيانات غالبًا ما يعني الاختيار بين عرض مسطح وتمثيل مضغوط. في العديد من سيناريوهات التقارير—مثل تخزين قائمة بالوسوم أو مجموعة من المعرفات—تريد أن يبقى نص JSON بالكامل في خلية واحدة. علامة **ArrayAsSingle** في `SmartMarkerOptions` تجعل ذلك ممكنًا.

في هذا الدرس سوف:

* إنشاء `DataTable` يحتوي على مصفوفة JSON في عمود.
* وضع Smart Markers في ورقة عمل Excel.
* **تكوين SmartMarkerOptions ArrayAsSingle** بحيث يتم التعامل مع مصفوفة JSON كقيمة خلية واحدة.
* معالجة العلامات وحفظ المصنف.
* التحقق من النتيجة.

> **المتطلبات المسبقة** – تحتاج إلى مكتبة Aspose.Cells لـ .NET (الإصدار 23.12 أو أحدث) وبيئة تطوير .NET (يوصى بـ Visual Studio 2022). يُفترض أن لديك معرفة أساسية بـ C# و DataTables.

---

## الخطوة 1: إعداد مصدر البيانات مع مصفوفة JSON

أولاً، أنشئ `DataTable` يحاكي البيانات التي ستحصل عليها من خدمة أو قاعدة بيانات. عمود **Names** يحتوي على سلسلة مشفرة بصيغة JSON تمثل مصفوفة من الأسماء.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*لماذا هذه الخطوة؟*  
تقرأ Smart Markers البيانات مباشرةً من كائنات .NET. بوضع مصفوفة JSON في عمود من نوع سلسلة، تحتفظ بصياغة JSON الدقيقة، والتي يمكن لاحقًا كتابتها إلى خلية دون تغيير.

---

## الخطوة 2: إدراج Smart Markers في مصنف جديد

أنشئ مصنفًا جديدًا، اختر ورقة العمل الأولى، واكتب Smart Markers التي تشير إلى الجدول بأكمله والعمود المحدد **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

المؤشر `&=dataTable.Names` يخبر Aspose.Cells باستبدال الخلية بقيمة عمود **Names** لكل صف في `dataTable`. لأن لدينا صفًا واحدًا فقط، سيتم معالجة المؤشر مرة واحدة.

---

## الخطوة 3: **تكوين SmartMarkerOptions ArrayAsSingle**

بشكل افتراضي، يقوم Aspose.Cells بتوسيع سلسلة تشبه المصفوفة إلى صفوف منفصلة. ضبط `ArrayAsSingle` على `true` يتجاوز هذا السلوك، مما يجبر النص الكامل لـ JSON على البقاء في خلية واحدة.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*لماذا تمكين `ArrayAsSingle`؟*  
عندما تكون `ArrayAsSingle` مساوية لـ `false`، يفسر المحرك `["Alice","Bob"]` كقيمتين منفصلتين ويكتبهما في صفوف متجاورة. ضبطها على `true` يعامل السلسلة كقيمة ذرية، وهو أمر أساسي للحفاظ على تنسيق JSON داخل Excel.

---

## الخطوة 4: معالجة Smart Markers باستخدام الخيارات المكوَّنة

الآن شغّل محرك Smart Marker، مع تمرير كائن الخيارات الذي قمت بتكوينه للتو.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

أثناء المعالجة، يقرأ Aspose.Cells الـ `dataTable`، يطبق العلامات، ويحترم علامة `ArrayAsSingle`، مما يترك مصفوفة JSON دون تعديل.

---

## الخطوة 5: حفظ المصنف والتحقق من النتيجة

أخيرًا، احفظ المصنف على القرص. افتح الملف المُنشأ في Excel أو أي عارض جداول بيانات لتأكيد أن الخلية **A2** تحتوي على نص JSON الدقيق.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### النتيجة المتوقعة

| A   |
|-----|
| **["Alice","Bob"]** |

الخلية **A2** تُظهر مصفوفة JSON كقيمة نصية واحدة، تمامًا كما هي مخزنة في `DataTable`. لا يتم إنشاء صفوف إضافية.

---

## التحويرات الشائعة ومعالجة الحالات الطرفية

| Situation | How to adapt |
|-----------|--------------|
| **عدة صفوف مع مصفوفات JSON** | إعداد `ArrayAsSingle` نفسه يعمل؛ كل مصفوفة JSON في الصف تبقى في خلية خاصة بها. |
| **هياكل JSON مختلفة (كائنات، مصفوفات متداخلة)** | طالما أن JSON هو سلسلة نصية، سيحافظ `ArrayAsSingle` عليها دون تعديل. بالنسبة للكائنات المعقدة قد تحتاج إلى هروب علامات الاقتباس. |
| **استخدام مصدر بيانات مختلف (مثل List\<T\>)** | استبدل `DataTable` بأي مجموعة قابلة للتعداد؛ يبقى تركيب العلامة (`&=myList.Property`) كما هو. |
| **التصدير إلى CSV بدلاً من XLSX** | `ArrayAsSingle` لا يزال ساريًا، لكن تذكر أن CSV لا يحافظ على تنسيق الخلايا؛ قد تحتاج إلى وضع JSON بين علامات اقتباس. |

**نصيحة احترافية:** دائمًا قم بتعيين `ArrayAsSingle` *قبل* استدعاء `ProcessSmartMarkers`. تغيير العلامة بعد المعالجة لا يؤثر على الخلايا التي تم إنشاؤها بالفعل.

---

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق وحدة تحكم. يتضمن جميع توجيهات `using` والتعليقات للتوضيح.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

شغّل البرنامج، افتح `SmartMarkerJson.xlsx`، وسترى مصفوفة JSON محفوظة في الخلية **A2**.

---

## الخلاصة

أنت الآن تعرف كيف **تكوين SmartMarkerOptions ArrayAsSingle** في C# للحفاظ على مصفوفة JSON كقيمة خلية واحدة عند استخدام علامات Aspose.Cells الذكية. الخطوات — إعداد `DataTable`، إدراج العلامات، ضبط علامة `ArrayAsSingle`، المعالجة، والحفظ — تشكل نمطًا قابلًا للتكرار يمكنك تطبيقه على أي سيناريو يتطلب تمثيل JSON مضغوط داخل Excel.

بعد ذلك، قد تستكشف:

* **Aspose.Cells smart markers** للتكرار على المجموعات.
* تصدير **كائنات JSON المتداخلة** عن طريق تخصيص تنسيق الخلايا.
* دمج **التنسيق الشرطي** مع العلامات الذكية للحصول على تقارير أغنى.

لا تتردد في تجربة هياكل بيانات مختلفة ومشاركة ما توصلت إليه. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف Excel من JSON – دليل Aspose.Cells الكامل](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [إنشاء وتكوين مصنف Excel Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [إنشاء وتكوين مصنف Excel Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}