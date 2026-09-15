---
category: general
date: 2026-03-18
description: إنشاء مصنف Excel باستخدام C# مع تعليق وحفظ المصنف بصيغة XLSX. تعلم كيفية
  إضافة تعليق، إنشاء تعليق في Excel، وأتمتة ملفات Excel.
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: ar
og_description: إنشاء مصنف Excel باستخدام C# مع تعليق وحفظ المصنف بصيغة XLSX. اتبع
  هذا الدليل خطوة بخطوة لإضافة تعليق في Excel وإنشاء تعليق Excel برمجياً.
og_title: إنشاء مصنف إكسل C# – إضافة تعليق وحفظ كملف XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: إنشاء مصنف إكسل C# – إضافة تعليق وحفظ كملف XLSX
url: /ar/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel باستخدام C# – إضافة تعليق وحفظ كملف XLSX

هل احتجت يوماً إلى **إنشاء مصنف Excel باستخدام C#** وإرفاق ملاحظة داخل خلية، لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—المطورون يسألون باستمرار *كيف يمكن إضافة تعليق* دون فتح Excel يدويًا.  

في هذا الدرس ستحصل على حل كامل وجاهز للتنفيذ يوضح **كيفية إضافة تعليق Excel**، **إنشاء تعليق Excel** باستخدام Smart Marker، و**حفظ المصنف كملف xlsx** في تدفق واحد سلس. لا مراجع معلقة، فقط شفرة صافية يمكنك لصقها في Visual Studio ومشاهدة النتيجة.

## ما ستتعلمه

- تهيئة مصنف Excel من الصفر باستخدام C#.
- إدراج Smart Marker يتحول إلى تعليق Excel.
- تغذية بيانات JSON لتحويل العلامة إلى تعليق حقيقي.
- حفظ الملف كمصنف `.xlsx`.
- طرق اختيارية لإضافة تعليقات دون Smart Markers.

بنهاية الدرس ستحصل على مثال مستقل يمكنك تكييفه للفواتير، تقارير الاختبار، أو أي حالة تحتاج فيها إلى تعليق خلية لإضافة سياق.

### المتطلبات المسبقة

- .NET 6 (أو .NET Framework 4.7+).  
- حزمة **Aspose.Cells for .NET** عبر NuGet – المكتبة التي تدعم ميزة Smart Marker.  
- بيئة تطوير C# أساسية (Visual Studio، VS Code، Rider…).

> **نصيحة احترافية:** إذا كنت بميزانية محدودة، تقدم Aspose نسخة تجريبية مجانية تعمل بالكامل للتطوير والاختبار.

---

## الخطوة 1: إنشاء مصنف Excel C# – إعداد المشروع

أولاً، لننشئ تطبيق console جديد ونضيف حزمة Aspose.Cells.

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

الآن افتح `Program.cs`. أول شيء نفعله هو **إنشاء مصنف جديد**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

لماذا نبدأ بمصنف جديد تمامًا؟ لأنه يضمن لك مساحة عمل نظيفة، يزيل أي تنسيقات مخفية، ويسمح لك بالتحكم في كل شيء من الصفر—مثالي لتوليد التقارير تلقائيًا.

---

## الخطوة 2: كيفية إضافة تعليق – باستخدام Smart Marker

Smart Markers هي نواقل يتم استبدالها بالبيانات في وقت التشغيل بواسطة Aspose. عبر تضمين علامة تتبع النمط **`${Comment:UserComment}`**، نخبر المحرك بتحويل هذه العلامة إلى تعليق فعلي.

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

هل لاحظت البادئة `Comment:`؟ هذه هي الإشارة للمعالج ليتعامل مع القيمة كتعليق وليس كنص عادي. إذا كنت تتساءل *“هل يعمل هذا مع أنواع خلايا أخرى؟”*—نعم، يمكنك تطبيق نفس العلامة على أي خلية، حتى على نطاقات مدمجة.

---

## الخطوة 3: إعداد بيانات JSON – ما سيظهر في التعليق

الخطوة التالية هي مصدر البيانات. هنا نستخدم سلسلة JSON بسيطة، لكن يمكنك أيضًا إمداد DataTable أو List أو كائن مخصص.

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

لا تتردد في استبدال `"Reviewed by QA"` بأي قيمة ديناميكية—ربما طابع زمني، اسم مستخدم، أو رابط إلى نظام تتبع الأخطاء. يجب أن يتطابق اسم المفتاح (`UserComment`) مع معرف العلامة.

---

## الخطوة 4: إنشاء تعليق Excel – معالجة Smart Marker

الآن نمرر JSON إلى معالج Smart Marker. هذه هي اللحظة التي يحدث فيها **إنشاء تعليق Excel** فعليًا.

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

خلف الكواليس، تقوم Aspose بتحليل JSON، العثور على الحقل `UserComment`، وإدراجه كتعليق مرتبط بالخلية **B2**. تظل القيمة الظاهرة في الخلية هي النص الأصلي للعلامة، لكن Excel سيظهر التعليق عند التحويم فوقها.

---

## الخطوة 5: حفظ المصنف كملف XLSX – تخزين النتيجة

أخيرًا، نكتب المصنف إلى القرص. هذا يحقق مطلب **حفظ المصنف كملف xlsx**.

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

افتح `output.xlsx` في Excel، وحوم فوق الخلية **B2**، وسترى التعليق *“Reviewed by QA”* يظهر. هذا كل شيء—بدون خطوات يدوية، بدون COM interop، فقط C# صافية.

---

## بديل: كيفية إضافة تعليق دون Smart Markers

إذا كنت تفضّل نهجًا أكثر مباشرة، يمكنك إنشاء كائن تعليق بنفسك:

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

هذه الطريقة مفيدة عندما يكون نص التعليق معروفًا مسبقًا في وقت التجميع، أو عندما تحتاج لتعيين خصائص إضافية مثل المؤلف، العرض، أو الارتفاع. ومع ذلك، **إنشاء تعليق Excel** عبر Smart Markers يتألق عندما تكون لديك سيناريو يعتمد على البيانات مع العديد من الصفوف والأعمدة.

---

## نصائح احترافية ومخاطر شائعة

| الحالة | ما يجب مراقبته | الحل المقترح |
|-----------|-------------------|-----------------|
| مجموعات بيانات كبيرة (10k+ صف) | معالجة Smart Marker قد تستهلك ذاكرة كبيرة | استخدم overload `SmartMarkerProcessor.Process` الذي يدعم البث، أو قسم المصنف إلى أجزاء |
| الحاجة إلى اسم مؤلف مخصص | المؤلف الافتراضي فارغ | `comment.Author = "MyApp";` بعد إنشاء التعليق |
| رغبة إظهار التعليق افتراضيًا | Excel يخفي التعليقات حتى التحويم | عيّن `comment.Visible = true;` |
| العمل مع إصدارات Excel أقدم | قد لا يدعم `.xlsx` | احفظ كـ `SaveFormat.Xls`، لكن لاحظ أن بعض خصائص التعليق قد تختلف |

---

## النتيجة المتوقعة

- **ملف المصنف:** `output.xlsx` موجود في مجلد `bin` الخاص بالمشروع.  
- **الخلية B2:** تعرض النص `${Comment:UserComment}` (يمكنك إخفاؤه بتغيير لون الخط إلى أبيض).  
- **التعليق المرفق بـ B2:** يظهر “Reviewed by QA” عند التحويم.

![Create Excel workbook C# example showing comment in cell B2](https://example.com/placeholder-image.png "Create Excel workbook C# example showing comment in cell B2")

*نص بديل للصورة:* **مثال إنشاء مصنف Excel باستخدام C# يظهر التعليق في الخلية B2**

---

## ملخص – ما أنجزناه

**أنشأنا مصنف Excel باستخدام C#**، أدرجنا **Smart Marker** تحول إلى **تعليق Excel**، قدمنا JSON لتوليد التعليق، وأخيرًا **حفظنا المصنف كملف xlsx**. كل ذلك تم في بضع عشرات من أسطر الكود النظيف المستقل.

---

## ما التالي؟ توسيع الحل

- **إنشاء تعليقات دفعية:** حلقة تمر عبر DataTable وتطبق Smart Marker على كل صف لإضافة ملاحظات مخصصة.  
- **تنسيق التعليقات:** تعديل حجم الخط، اللون، أو إضافة نص غني باستخدام مجموعة `Comment.RichText`.  
- **التصدير إلى PDF:** استخدم `workbook.Save("output.pdf", SaveFormat.Pdf);` لمشاركة التقارير مع الحفاظ على التعليقات.  

إذا كنت مهتمًا بـ **إضافة تعليق Excel** برمجيًا في سياقات أخرى—مثل استخدام OpenXML SDK أو EPPlus—فهذه المكتبات تدعم أيضًا إنشاء التعليقات، رغم أن واجهة البرمجة تختلف.

---

### ختامًا

إضافة تعليق إلى ملف Excel من خلال C# لا يجب أن تكون مهمة شاقة. باستخدام محرك Smart Marker في Aspose.Cells تحصل على طريقة مختصرة، مدفوعة بالبيانات لـ **إضافة تعليق Excel**، **إنشاء تعليق Excel**، و**حفظ المصنف كملف xlsx** بأقل قدر من الشيفرة المتكررة.  

جرّبه، عدّل JSON، وشاهد كيف تتحول البيانات الخام إلى جدول بيانات مصقول غني بالتعليقات. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}