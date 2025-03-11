---
title: تحديث عنصر صيغة Power Query
linktitle: تحديث عنصر صيغة Power Query
second_title: مرجع واجهة برمجة التطبيقات Aspose.Cells لـ .NET
description: يمكنك بسهولة تحديث عناصر صيغة Power Query في Excel باستخدام Aspose.Cells for .NET. دليل خطوة بخطوة لتبسيط عمليات معالجة البيانات.
weight: 160
url: /ar/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديث عنصر صيغة Power Query

## مقدمة

إذا سبق لك العمل باستخدام Excel، فأنت تعلم مدى قوته، وخاصةً عندما تبدأ في استخدام Power Query. فهي الصلصة السرية التي تسمح لك بتحويل بياناتك وتنظيفها وتحليلها دون عناء. إحدى الطرق الرائعة للتعامل مع صيغ Power Query في Excel هي من خلال Aspose.Cells for .NET. اليوم، سنرشدك خلال تحديث عناصر صيغ Power Query خطوة بخطوة. لذا، استعد للبدء!

## المتطلبات الأساسية

قبل أن تتعمق في الكود، هناك بعض الأشياء التي قد ترغب في إعدادها:

1. Visual Studio: ستحتاج إلى بيئة تطوير متكاملة (IDE) لكتابة وتشغيل كود .NET الخاص بك. Visual Studio هو الخيار الأمثل.
2.  مكتبة Aspose.Cells: تأكد من توفر مكتبة Aspose.Cells ضمن مشروعك. يمكنك تنزيلها من[موقع](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: بينما سنتناول هذا الأمر معًا، فإن الحصول على بعض الفهم الأساسي للغة C# سيساعدك بالتأكيد، خاصة عند التنقل عبر فئات وطرق مختلفة.
4. ملفات Excel النموذجية: ستحتاج إلى ملفات Excel المذكورة في مقتطف التعليمات البرمجية. تأكد من توفر ما يلي:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: تأكد من أن مشروعك يستهدف إصدارًا متوافقًا من .NET Framework.

الآن بعد أن أصبحت معداتنا جاهزة، يمكننا الانتقال إلى الجزء الممتع: كتابة التعليمات البرمجية!

## استيراد الحزم

أولاً وقبل كل شيء، ستحتاج إلى استيراد مساحات الأسماء الضرورية. وإليك كيفية القيام بذلك:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

من خلال إضافة هذه المساحات الاسمية، فأنت بذلك تخبر المترجم بأنك تنوي استخدام الفئات والطرق من مكتبة Aspose.Cells. هذه الخطوة بالغة الأهمية لأنها تضع الأساس للكود الذي يليها.

دعنا نستعرض مقتطف التعليمات البرمجية الذي قدمته. سيرشدك هذا البرنامج التعليمي إلى كل جزء، مما يضمن فهمك لما يحدث.

## الخطوة 1: إعداد أدلة العمل

في هذه الخطوة، سنحدد مكان وجود ملفات المصدر والإخراج. وهذا يضمن أن Aspose يعرف المكان الذي يبحث فيه عن ملفات Excel الخاصة بك.

```csharp
// أدلة العمل
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## الخطوة 2: تحميل المصنف

الآن، لنقم بتحميل ملف Excel الذي يوجد فيه Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 ال`Workbook` تعتبر الفئة نقطة دخولك إلى ملف Excel. من خلال تمرير مسار ملف المصدر الخاص بنا، نقوم بإنشاء مثيل يسمح لنا بالتعامل معه. يمكنك تخيل الأمر مثل فتح كتاب - فأنت تستعد لقراءة (أو تحرير) محتوياته.

## الخطوة 3: الوصول إلى مجموعة البيانات

بعد ذلك، سنتمكن من الوصول إلى صيغ Power Query المخزنة في Data Mashup الخاص بالمصنف.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 ال`DataMashup` تحتوي الفئة على جميع صيغ Power Query المرتبطة بمصنف العمل الخاص بك. هذا هو المكان الذي سنقوم فيه بالعمل الشاق، تمامًا كما هو الحال عندما تفتح صندوق أدوات للإصلاحات.

## الخطوة 4: تكرار صيغ Power Query

الآن يأتي الجزء الذي نكرر فيه صيغ Power Query للعثور على الصيغة المحددة التي نريد تحديثها.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  نحن نمر عبر كل منها`PowerQueryFormula` في`mashupData`.
- في هذه الحلقة، نغوص في كل منها`PowerQueryFormulaItem`.
- نتحقق مما إذا كان اسم العنصر يتطابق مع "المصدر". إذا كان الأمر كذلك، نقوم بتحديث قيمته للارتباط بملف المصدر الجديد.

وهذا يشبه العثور على الصفحة الصحيحة في دليل ثم إجراء التحديثات اللازمة - إنها عملية مباشرة ودقيقة.

## الخطوة 5: احفظ المصنف المحدث

بعد إجراء التحديثات، حان الوقت لحفظ التغييرات.

```csharp
// احفظ المصنف الناتج.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 ال`Save` تكتب الطريقة المصنف المحدث إلى دليل الإخراج المحدد. الأمر أشبه بختم تعديلاتك في إصدار جديد من الدليل، جاهزًا لاستخدام الآخرين!

## خاتمة

مبروك! لقد نجحت في تحديث عنصر صيغة Power Query باستخدام Aspose.Cells for .NET. باستخدام هذه الطريقة، يمكنك أتمتة تعديل صيغ Power Query في ملفات Excel، مما يوفر لك الوقت والجهد الثمينين.

## الأسئلة الشائعة

### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة فعالة للتعامل مع ملفات Excel في تطبيقات .NET دون الحاجة إلى تثبيت Microsoft Excel.

### هل أحتاج إلى Microsoft Excel لتشغيل Aspose.Cells؟
لا، يتيح لك Aspose.Cells إنشاء ملفات Excel وتحريرها برمجيًا دون الحاجة إلى Excel على الخادم أو جهاز التطوير الخاص بك.

### ما هي أنواع ملفات Excel التي يمكنني العمل عليها باستخدام Aspose.Cells؟
بإمكانك العمل مع .xlsx، و.xls، و.xlsm، والعديد من تنسيقات Excel الأخرى باستخدام Aspose.Cells.

### هل هناك نسخة تجريبية متاحة لـ Aspose.Cells؟
 نعم، يمكنك تنزيل نسخة تجريبية مجانية من[صفحة إصدار Aspose Cells](https://releases.aspose.com/).

### كيف يمكنني الحصول على الدعم لـ Aspose.Cells؟
 يمكنك الوصول إلى الدعم من خلال[منتدى اسبوس](https://forum.aspose.com/c/cells/9)حيث يمكنك طرح الأسئلة والعثور على إجابات من المجتمع وفريق Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
