---
category: general
date: 2026-02-23
description: كيفية إنشاء مصنف باستخدام Aspose.Cells وإضافة علامات باستخدام مصفوفة
  JSON. تعلّم كيفية إضافة العلامات، واستخدام مصفوفة JSON، والعلامات الذكية في Aspose.Cells
  خلال دقائق.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: ar
og_description: كيفية إنشاء دفتر عمل باستخدام Aspose.Cells، إضافة العلامات، واستخدام
  مصفوفة JSON. يوضح لك هذا الدليل خطوة بخطوة كل ما تحتاجه.
og_title: كيفية إنشاء مصنف باستخدام العلامات الذكية – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية إنشاء مصنف باستخدام العلامات الذكية – دليل Aspose.Cells
url: /ar/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء دفتر عمل باستخدام العلامات الذكية – دليل Aspose.Cells

هل تساءلت يومًا **كيفية إنشاء دفتر عمل** يملأ البيانات تلقائيًا من مصدر JSON؟ لست وحدك—المطورون يطرحون باستمرار سؤالًا حول كيفية إضافة علامات تسحب القيم من المصفوفات، خاصةً عند العمل مع Aspose.Cells. الخبر السار؟ الأمر بسيط جدًا بمجرد أن تفهم مفهوم العلامة الذكية. في هذا الدرس سنستعرض إنشاء دفتر عمل، إضافة العلامات، استخدام مصفوفة JSON، وتكوين العلامات الذكية في Aspose.Cells حتى تتمكن من توليد ملفات Excel في الوقت الفعلي.

سنغطي كل ما تحتاج معرفته: تهيئة دفتر العمل، بناء `MarkerCollection`، إمداد مصفوفة JSON، تبديل علم “ArrayAsSingle”، وأخيرًا تطبيق العلامات. في النهاية ستحصل على برنامج C# كامل يعمل على إنتاج ملف Excel يحتوي على القيم **A**، **B**، و**C** مُعبأة تلقائيًا. لا خدمات خارجية، فقط سحر Aspose.Cells النقي.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- حزمة NuGet لـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- فهم أساسي لصياغة C# (إذا كنت مبتدئًا، فإن الشفرات مشروحة بالتفصيل)
- Visual Studio أو أي بيئة تطوير تفضلها

إذا كان لديك كل ذلك، عظيم—لنبدأ.

## الخطوة 1: كيفية إنشاء دفتر عمل (تهيئة ملف Excel)

أول شيء تحتاجه هو كائن دفتر عمل فارغ. فكر فيه كقماش أبيض ستقوم Aspose.Cells برسم البيانات عليه لاحقًا.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **لماذا هذا مهم:** `Workbook` هو نقطة الدخول لكل عملية في Excel. بدونها لا يمكنك إرفاق العلامات الذكية أو حفظ الملف. إنشاء دفتر العمل أولًا يضمن لك بيئة نظيفة للخطوات اللاحقة.

## الخطوة 2: كيفية إضافة العلامات – تهيئة مجموعة العلامات

العلامات الذكية تعيش داخل `MarkerCollection`. هذه المجموعة هي المكان الذي تعرف فيه العناصر النائبة (العلامات) والبيانات التي ستحل محلها.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **نصيحة احترافية:** يمكنك إعادة استخدام نفس `MarkerCollection` لعدة أوراق عمل، لكن الحفاظ على مجموعة واحدة لكل ورقة يسهل عملية تصحيح الأخطاء.

## الخطوة 3: استخدام مصفوفة JSON – إضافة علامة ببيانات JSON

الآن نضيف العلامة فعليًا. العنصر النائب `{SmartMarker}` سيستبدل بمصفوفة JSON التي نوفرها. يجب أن تكون مصفوفة JSON سلسلة نصية، مثل `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **شرح:** طريقة `Add` تأخذ وسيطين: نص العلامة ومصدر البيانات. هنا مصدر البيانات هو مصفوفة JSON، والتي يمكن لـ Aspose.Cells تحليلها تلقائيًا. هذا هو جوهر **استخدام مصفوفة JSON** مع العلامات الذكية.

## الخطوة 4: تكوين العلامة – التعامل مع المصفوفة كقيمة واحدة

بشكل افتراضي، تقوم Aspose.Cells بتوسيع مصفوفة JSON إلى صفوف منفصلة. إذا أردت أن تُعامل المصفوفة بأكملها كقيمة خلية واحدة (مفيد للقوائم المنسدلة أو السلاسل المتصلة)، فعّل علم `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **متى تستخدمه:** إذا كنت تريد أن تظهر المصفوفة في خلية واحدة (مثال: `"A,B,C"`)، فعّل هذا العلم. وإلا، ستكتب Aspose.Cells كل عنصر في صفه الخاص.

## الخطوة 5: إرفاق العلامات بالورقة وتطبيقها

أخيرًا، اربط مجموعة العلامات بالورقة وأخبر Aspose.Cells باستبدال العناصر النائبة بالبيانات الفعلية.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **النتيجة:** بعد تشغيل البرنامج، يحتوي الملف `SmartMarkerResult.xlsx` على القيمة **A** (أو المصفوفة كاملة إذا كان `ArrayAsSingle` صحيح) في الخلية `A1`. افتح الملف للتحقق.

### النتيجة المتوقعة

| A |
|---|
| A |   *(إذا كان `ArrayAsSingle` خاطئًا، العنصر الأول يملأ الخلية)*

إذا ضبطت `ArrayAsSingle = true`، ستحتوي الخلية `A1` على السلسلة `["A","B","C"]`.

## الخطوة 6: كيفية إضافة العلامات – سيناريوهات متقدمة (اختياري)

قد تتساءل، *ماذا لو احتجت أكثر من علامة واحدة؟* الجواب بسيط: فقط استدعِ `Add` مرة أخرى.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **لماذا يعمل هذا:** كل علامة تعمل بشكل مستقل، لذا يمكنك خلط “المصفوفة كقيمة واحدة” و“التوسيع إلى صفوف” داخل نفس الورقة. هذه المرونة هي سمة **العلامات الذكية Aspose.Cells**.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| العلامة لم تُستبدل | نص العنصر النائب مفقود أو به خطأ إملائي | تأكد أن الخلية تحتوي على نص العلامة بالضبط (`{SmartMarker}`) |
| JSON لم يُتحلل | صياغة JSON غير صالحة (نقطة اقتباس مفقودة) | استخدم أداة تحقق من JSON أو هروب مزدوج للاقتباسات في سلاسل C# |
| المصفوفة تتوسع بشكل غير متوقع | ترك `ArrayAsSingle` على القيمة الافتراضية `false` | عيّن `["ArrayAsSingle"] = true` للعلامة المحددة |
| دفتر العمل يُحفظ فارغًا | عدم استدعاء `Apply()` قبل `Save()` | احرص دائمًا على استدعاء `worksheet.SmartMarkers.Apply()` قبل الحفظ |

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console. لا تحتاج إلى ملفات إضافية.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

شغّل البرنامج، افتح `SmartMarkerResult.xlsx`، وسترى مصفوفة JSON (أو العنصر الأول منها) موضوعة بدقة في الخلية **A1**.

## الخطوات التالية: توسيع الحل

الآن بعد أن عرفت **كيفية إنشاء دفتر عمل**، **كيفية إضافة العلامات**، و**استخدام مصفوفة JSON** مع Aspose.Cells، فكر في الأفكار التالية:

1. **أوراق عمل متعددة** – كرّر عبر قائمة من الأوراق وأرفق مجموعات علامات مختلفة لكل منها.
2. **JSON ديناميكي** – احصل على JSON من واجهة ويب (`HttpClient`) ومرره مباشرة إلى `smartMarkerCollection.Add`.
3. **تنسيق المخرجات** – بعد تطبيق العلامات، قم بتنسيق الخلايا (خطوط، ألوان) لجعل التقرير أكثر احترافية.
4. **صيغ تصدير** – احفظ دفتر العمل كـ PDF أو CSV أو HTML بتغيير `workbook.Save("file.pdf")`.

كل هذه المواضيع تتضمن **العلامات الذكية Aspose.Cells**، لذا ستستمر في توسيع المفاهيم الأساسية التي تعلمتها للتو.

## الخلاصة

استعرضنا **كيفية إنشاء دفتر عمل** من الصفر، **كيفية إضافة العلامات**، وكيفية **استخدام مصفوفة JSON** مع العلامات الذكية في Aspose.Cells. المثال الكامل القابل للتنفيذ يوضح سير العمل بالكامل، من تهيئة `Workbook` إلى حفظ الملف النهائي. من خلال تبديل علم `ArrayAsSingle` تحصل على تحكم دقيق في طريقة ظهور بيانات JSON في Excel، مما يجعل الحل قابلًا للتكيف مع مجموعة واسعة من سيناريوهات التقارير.

جرّب الكود، عدّل JSON، واختبر علامات إضافية. عندما تتقن هذه اللبنات الأساسية، يصبح إنشاء تقارير Excel متقدمة أمرًا سهلًا. هل لديك أسئلة أو تريد مشاركة حالة استخدام مميزة؟ اترك تعليقًا أدناه—برمجة سعيدة! 

![Diagram showing how to create workbook with smart markers in Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "how to create workbook with Aspose.Cells smart markers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}