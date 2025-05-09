---
"description": "حدّث عناصر صيغ Power Query بسهولة في Excel باستخدام Aspose.Cells لـ .NET. دليل خطوة بخطوة لتبسيط عمليات معالجة البيانات."
"linktitle": "تحديث عنصر صيغة Power Query"
"second_title": "مرجع واجهة برمجة التطبيقات Aspose.Cells لـ .NET"
"title": "تحديث عنصر صيغة Power Query"
"url": "/ar/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحديث عنصر صيغة Power Query

## مقدمة

إذا سبق لك العمل مع Excel، فأنت تعلم مدى فعاليته، خاصةً عند البدء في استخدام Power Query. إنها الوسيلة السحرية التي تُمكّنك من تحويل بياناتك وتنظيفها وتحليلها بسهولة. إحدى الطرق الرائعة للتعامل مع صيغ Power Query في Excel هي استخدام Aspose.Cells لـ .NET. اليوم، سنرشدك خلال تحديث عناصر صيغ Power Query خطوة بخطوة. هيا، هيا بنا نبدأ!

## المتطلبات الأساسية

قبل أن تتعمق في الكود، هناك بعض الأشياء التي قد ترغب في إعدادها:

1. Visual Studio: ستحتاج إلى بيئة تطوير متكاملة (IDE) لكتابة وتشغيل أكواد .NET. Visual Studio هو الخيار الأمثل.
2. مكتبة Aspose.Cells: تأكد من توفر مكتبة Aspose.Cells في مشروعك. يمكنك تنزيلها من [موقع](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: بينما سنتناول هذا الأمر معًا، فإن الحصول على بعض الفهم الأساسي للغة C# سيساعدك بالتأكيد، خاصة عند التنقل عبر فئات وطرق مختلفة.
4. ملفات إكسل نموذجية: ستحتاج إلى ملفات إكسل المذكورة في مقتطف الكود. تأكد من توفر ما يلي:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: تأكد من أن مشروعك يستهدف إصدارًا متوافقًا من .NET Framework.

الآن بعد أن أصبحت معداتنا جاهزة، يمكننا الانتقال إلى الجزء الممتع: كتابة التعليمات البرمجية!

## استيراد الحزم

أولاً، ستحتاج إلى استيراد مساحات الأسماء اللازمة. إليك كيفية القيام بذلك:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

بإضافة هذه المساحات، تُعلم المُجمِّع بأنك تنوي استخدام الفئات والأساليب من مكتبة Aspose.Cells. هذه الخطوة بالغة الأهمية لأنها تُمهِّد الطريق للكود الذي يليه.

لنبدأ بشرح مقتطف الشفرة الذي قدمته. سيشرح لك هذا البرنامج التعليمي كل جزء، ويضمن فهمك لما يحدث.

## الخطوة 1: إعداد أدلة العمل

في هذه الخطوة، سنحدد مكان ملفات المصدر والإخراج. هذا يضمن أن يعرف Aspose مكان البحث عن ملفات Excel.

```csharp
// أدلة العمل
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## الخطوة 2: تحميل المصنف

الآن، دعنا نحمل ملف Excel الذي يوجد به Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
ال `Workbook` الفئة هي نقطة دخولك إلى ملف Excel. بتمرير مسار ملف المصدر، ننشئ مثيلًا يسمح لنا بالتعامل معه. يمكنك تخيل الأمر كفتح كتاب - تستعد لقراءة (أو تحرير) محتوياته.

## الخطوة 3: الوصول إلى مجموعة البيانات

بعد ذلك، سنتمكن من الوصول إلى صيغ Power Query المخزنة في Data Mashup الخاص بالمصنف.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
ال `DataMashup` تحتوي الفئة على جميع صيغ Power Query المرتبطة بمصنف عملك. هنا سنبدأ العمل الشاق، تمامًا كما لو كنت تفتح صندوق أدوات للإصلاحات.

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

- نحن نمر عبر كل `PowerQueryFormula` في `mashupData`.
- في هذه الحلقة، نغوص في كل منها `PowerQueryFormulaItem`.
- نتحقق من تطابق اسم العنصر مع "المصدر". إذا كان الأمر كذلك، نقوم بتحديث قيمته للارتباط بملف المصدر الجديد.

وهذا يشبه العثور على الصفحة الصحيحة في دليل ثم إجراء التحديثات اللازمة - إنها عملية مباشرة ودقيقة.

## الخطوة 5: حفظ المصنف المحدث

بعد إجراء التحديثات، حان الوقت لحفظ التغييرات.

```csharp
// احفظ المصنف الناتج.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
ال `Save` تكتب هذه الطريقة المصنف المُحدّث إلى دليل الإخراج المُحدد. يشبه الأمر حفظ تعديلاتك في نسخة جديدة من الدليل، جاهزة للاستخدام من قِبل الآخرين!

## خاتمة

تهانينا! لقد نجحت في تحديث عنصر صيغة Power Query باستخدام Aspose.Cells لـ .NET. بهذه الطريقة، يمكنك أتمتة تعديل صيغ Power Query في ملفات Excel، مما يوفر عليك وقتًا وجهدًا كبيرين.

## الأسئلة الشائعة

### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة قوية للتعامل مع ملفات Excel في تطبيقات .NET دون الحاجة إلى تثبيت Microsoft Excel.

### هل أحتاج إلى Microsoft Excel لتشغيل Aspose.Cells؟
لا، يتيح لك Aspose.Cells إنشاء ملفات Excel وتحريرها برمجيًا دون الحاجة إلى Excel على الخادم أو جهاز التطوير الخاص بك.

### ما هي أنواع ملفات Excel التي يمكنني العمل عليها باستخدام Aspose.Cells؟
يمكنك العمل مع .xlsx، و.xls، و.xlsm، والعديد من تنسيقات Excel الأخرى باستخدام Aspose.Cells.

### هل هناك نسخة تجريبية متاحة لـ Aspose.Cells؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية من [صفحة إصدار Aspose Cells](https://releases.aspose.com/).

### كيف يمكنني الحصول على الدعم لـ Aspose.Cells؟
يمكنك الوصول إلى الدعم من خلال [منتدى Aspose](https://forum.aspose.com/c/cells/9)، حيث يمكنك طرح الأسئلة والعثور على إجابات من المجتمع وفريق Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}