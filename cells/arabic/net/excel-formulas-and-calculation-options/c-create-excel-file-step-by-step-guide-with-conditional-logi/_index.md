---
category: general
date: 2026-03-25
description: c# إنشاء ملف إكسل وحفظ المصنف كـ xlsx باستخدام تعبير شرطي في إكسل. تعلم
  كتابة قيم الأسعار العليا والدنيا في دقائق.
draft: false
keywords:
- c# create excel file
- save workbook as xlsx
- conditional expression in excel
- write high low price
language: ar
og_description: c# إنشاء ملف إكسل بسرعة. يوضح هذا الدليل كيفية حفظ المصنف كملف xlsx
  واستخدام تعبير شرطي في إكسل لكتابة قيم الأسعار العليا والسفلى.
og_title: c# إنشاء ملف إكسل – دليل كامل مع المنطق الشرطي
tags:
- excel
- csharp
- smartmarkers
- data‑export
title: c# إنشاء ملف إكسل – دليل خطوة بخطوة مع المنطق الشرطي
url: /ar/net/excel-formulas-and-calculation-options/c-create-excel-file-step-by-step-guide-with-conditional-logi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# إنشاء ملف إكسل – دليل كامل مع المنطق الشرطي

هل احتجت يوماً إلى **c# إنشاء ملف إكسل** يقوم تلقائيًا بوضع علامة على الأسعار كـ “High” أو “Low” دون كتابة ماكرو؟ لست وحدك. في العديد من سيناريوهات التقارير لديك قائمة من الأرقام، لكن قاعدة العمل — السعر > 100 → “High”، وإلا “Low” — يجب أن تُدمج مباشرة في جدول البيانات.  

في هذا الدرس سنستعرض مثالًا مختصرًا وقابلًا للتنفيذ بالكامل يقوم **c# إنشاء ملف إكسل**، يحفظ المصنف كملف xlsx، ويستفيد من *تعبير شرطي في إكسل* عبر Aspose.Cells Smart Markers. في النهاية سترى بالضبط كيف يمكنك **كتابة سعر عالي أو منخفض** ببضع أسطر من الشيفرة فقط.

## ما ستتعلمه

- كيفية إنشاء كائن مصنف (Workbook) والحصول على الورقة الأولى.  
- كيفية تضمين Smart Marker يحتوي على تعبير شرطي.  
- تزويد معالج Smart Marker بالبيانات وتوليد الملف النهائي.  
- أين يتم حفظ ملف **حفظ المصنف كـ xlsx** الناتج على القرص وكيف يبدو.  

بدون أي إعدادات خارجية، بدون COM interop، وبدون VBA فوضوي. فقط C# صافية وحزمة NuGet واحدة.

> **المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.7.2+) ومكتبة `Aspose.Cells` المثبتة عبر NuGet (`Install-Package Aspose.Cells`). معرفة أساسية بصياغة C# هي كل ما تحتاجه.

---

## الخطوة 1 – إنشاء مصنف جديد والوصول إلى الورقة الأولى

أول شيء تقوم به عندما **c# إنشاء ملف إكسل** هو إنشاء كائن `Workbook`. هذا الكائن يمثل مستند إكسل بالكامل في الذاكرة.

```csharp
using Aspose.Cells;

...

// Step 1: Initialize a new workbook and get the first worksheet
Workbook workbook = new Workbook();                // In‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];     // First sheet (named Sheet1 by default)
```

*لماذا هذا مهم:* فئة `Workbook` هي نقطة الدخول لجميع عمليات إكسل. من خلال الحصول على `Worksheets[0]` نضمن أننا نعمل على الورقة الافتراضية، مما يبقي المثال منظمًا.

---

## الخطوة 2 – إدراج Smart Marker مع تعبير شرطي

Smart Markers هي أماكن حجز يقوم Aspose.Cells باستبدالها بالبيانات أثناء التشغيل. الصيغة `${field:IF(condition, trueResult, falseResult)}` تسمح لنا بتضمين **تعبير شرطي في إكسل** مباشرة داخل خلية.

```csharp
// Step 2: Put a Smart Marker into cell A1 that evaluates the "price" field
// If price > 100 → "High", else → "Low"
worksheet.Cells["A1"].PutValue("${price:IF(${price}>100,\"High\",\"Low\")}");
```

لاحظ وجود `${price}` مزدوج: الخارجي يخبر المعالج أي حقل يجب تقييمه، بينما الداخلي `${price}` هو القيمة الفعلية المستخدمة في المقارنة.  

*لماذا هذا مهم:* تضمين المنطق داخل العلامة يعني أن ملف إكسل الناتج يكون مستقلاً بذاته—يمكنك فتحه في أي برنامج جدول بيانات ورؤية “High” أو “Low” دون أي شيفرة إضافية.

---

## الخطوة 3 – تزويد معالج Smart Marker بالبيانات

الآن نوفر البيانات الفعلية التي سيستهلكها العلامة. في تطبيق واقعي قد تكون هذه قائمة من الكائنات، DataTable، أو حتى JSON. للتوضيح سنستخدم كائنًا مجهولًا يحتوي على خاصية `price` واحدة.

```csharp
// Step 3: Process the Smart Marker with a data source
var data = new { price = 120 };   // Change this value to test different outcomes
worksheet.SmartMarkerProcessor.Process(data);
```

إذا غيرت `price` إلى `80`، ستظهر الخلية “Low”. هذا يوضح قدرة **كتابة سعر عالي أو منخفض** في سطر واحد فقط.

---

## الخطوة 4 – حفظ المصنف كملف XLSX

أخيرًا، نقوم بحفظ المصنف الموجود في الذاكرة إلى القرص. هنا يأتي دور **حفظ المصنف كـ xlsx**.

```csharp
// Step 4: Write the workbook to a .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);
```

بعد تشغيل البرنامج، افتح `output.xlsx` وستجد الخلية **A1** تحتوي إما على “High” أو “Low” بناءً على السعر الذي قمت بتحديده.

![Excel screenshot showing "High" in cell A1](/images/excel-high-low.png "Result of c# create excel file with conditional expression")

*نصيحة احترافية:* استخدم `Path.Combine` لتجنب كتابة المسارات يدويًا؛ فهو يعمل على Windows وLinux وmacOS على حد سواء.

---

## مثال كامل يعمل – انسخ، الصق، شغّل

فيما يلي التطبيق الكامل للكونسول. الصقه في مشروع .NET جديد واضغط **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelConditionalDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & get first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert Smart Marker with conditional expression
            worksheet.Cells["A1"].PutValue("${price:IF(${price}>100,\"High\",\"Low\")}");

            // 3️⃣ Supply data (change the price to see different results)
            var data = new { price = 120 };
            worksheet.SmartMarkerProcessor.Process(data);

            // 4️⃣ Save as .xlsx (this is the save workbook as xlsx step)
            string outputFile = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputFile, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to: {outputFile}");
            Console.WriteLine("Open the file and check cell A1 – it should read 'High' or 'Low'.");
        }
    }
}
```

### النتيجة المتوقعة

- يطبع الكونسول المسار الكامل إلى `output.xlsx`.  
- عند فتح ملف إكسل يظهر **A1 = High** (لأننا عيّننا `price = 120`).  
- غيّر قيمة `price` إلى `80` وأعد التشغيل؛ **A1 = Low**.  

هذا هو دورة الحياة الكاملة لـ **c# إنشاء ملف إكسل**، من الإنشاء في الذاكرة إلى المنطق الشرطي وأخيرًا حفظ النتيجة.

---

## الأسئلة المتكررة والحالات الخاصة

### هل يمكنني معالجة قائمة من الأسعار بدلاً من قيمة واحدة؟

بالطبع. استبدل الكائن المجهول بمجموعة وعدّل العلامة لتغطي نطاقًا (مثال: `${price[i]:IF(${price[i]}>100,"High","Low")}`). سيعيد المعالج تكرار الصف لكل عنصر.

### ماذا لو احتجت إلى شروط أكثر تعقيدًا؟

يمكنك تداخل عبارات `IF` أو استخدام وظائف أخرى مثل `AND`، `OR`، وحتى صيغ مخصصة. مثال:

```csharp
worksheet.Cells["B1"].PutValue(
    "${price:IF(AND(${price}>100, ${price}<200),\"Medium\",\"Other\")}"
);
```

### هل يعمل هذا مع إصدارات إكسل القديمة؟

الحفظ باستخدام `SaveFormat.Xlsx` ينتج تنسيق Office Open XML الحديث، المدعوم من Excel 2007 وما بعده. إذا كنت بحاجة إلى الصيغة القديمة `.xls`، غيّر قيمة تعداد `SaveFormat` وفقًا لذلك، لكن بعض الدوال الحديثة قد لا تكون متاحة.

### هل Aspose.Cells مجاني؟

Aspose يقدم نسخة تقييم مجانية مع علامة مائية. للاستخدام الإنتاجي ستحتاج إلى ترخيص، لكن واجهة البرمجة (API) تبقى نفسها.

---

## الخلاصة

لقد غطينا للتو كيفية **c# إنشاء ملف إكسل**، **حفظ المصنف كـ xlsx**، وتضمين **تعبير شرطي في إكسل** يتيح لك **كتابة سعر عالي أو منخفض** دون أي معالجة يدوية لاحقة. النهج قابل للتوسع—استبدل الكائن المجهول باستعلام قاعدة بيانات، أو حلقة عبر الصفوف، أو حتى توليد تقارير متعددة الأوراق.

الخطوات التالية قد تشمل:

- تصدير جدول بيانات كامل مع أعمدة شرطية متعددة.  
- تنسيق الخلايا بناءً على نفس المنطق (مثلاً تعبئة حمراء لـ “Low”).  
- دمج Smart Markers مع الرسوم البيانية لإنشاء لوحات معلومات أغنى.

جرّبه، عدّل الشروط، وشاهد كيف يمكنك بسرعة تحويل الأرقام الخام إلى تقرير إكسل مصقول. إذا واجهت أي صعوبات، اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}