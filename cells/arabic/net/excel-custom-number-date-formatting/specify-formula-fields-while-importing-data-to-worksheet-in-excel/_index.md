---
"description": "تعرف على كيفية استيراد البيانات إلى جداول Excel باستخدام حقول الصيغة المحددة باستخدام Aspose.Cells لـ .NET في هذا البرنامج التعليمي المفصل."
"linktitle": "تحديد حقول الصيغة عند استيراد البيانات إلى ورقة Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تحديد حقول الصيغة عند استيراد البيانات إلى ورقة Excel"
"url": "/ar/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحديد حقول الصيغة عند استيراد البيانات إلى ورقة Excel

## مقدمة

عندما يتعلق الأمر بمعالجة ملفات Excel برمجيًا، يُعد Aspose.Cells for .NET أداةً قيّمةً للغاية. فهو يوفر وظائف فعّالة لإنشاء جداول بيانات Excel وتعديلها ومعالجتها بسهولة. ومن ميزاته الرائعة إمكانية تحديد حقول الصيغ أثناء استيراد البيانات إلى جدول بيانات Excel. تخيّل أنك تعمل على تقرير مالي وتحتاج إلى حساب الإجماليات تلقائيًا بناءً على مدخلات المستخدم. سيرشدك هذا البرنامج التعليمي خطوة بخطوة لتحقيق ذلك بأسلوب واضح ومباشر.

## المتطلبات الأساسية

قبل الغوص في الكود، دعنا نتأكد من أن لديك كل ما تحتاجه. 

1. Visual Studio أو أي بيئة تطوير متكاملة (IDE) لـ .NET: تأكد من أن لديك بيئة تطوير متكاملة مناسبة لكتابة وتشغيل كود C# الخاص بك.
2. Aspose.Cells لـ .NET: ستحتاج إلى تنزيل مكتبة Aspose.Cells والرجوع إليها في مشروعك. يمكنك تنزيلها من [إصدارات Aspose](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة بلغة C# ومفاهيم البرمجة الموجهة للكائنات على فهم الأمثلة بشكل أفضل.
4. .NET Framework: يفترض هذا البرنامج التعليمي أنك تستخدم .NET Framework 4.5 أو أعلى.

بمجرد الانتهاء من المتطلبات الأساسية، دعنا ننتقل إلى استيراد بعض البيانات إلى ورقة Excel مع حقول الصيغة المحددة.

## استيراد الحزم

قبل البدء بكتابة الكود، ستحتاج إلى استيراد مساحة اسم Aspose.Cells اللازمة. عادةً ما يتم ذلك في أعلى ملف C#:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

يتيح لك هذا استخدام الفئات والطرق التي توفرها مكتبة Aspose.Cells دون الحاجة إلى إضافة البادئة الخاصة بمساحة الأسماء إليها في كل مرة.

دعونا نقسم العملية بأكملها إلى خطوات قابلة للإدارة:

## الخطوة 1: تحديد دليل الإخراج

أولاً، عليك تحديد مكان حفظ ملف Excel. إليك الطريقة:

```csharp
static string outputDir = "Your Document Directory"; // حدد دليل المستندات الخاص بك هنا
```

يستبدل `"Your Document Directory"` مع مسار ملفك الفعلي. هذا هو المكان الذي سيتم فيه حفظ ملف Excel المُنشأ.

## الخطوة 2: إنشاء فئة محددة من قبل المستخدم لعناصر البيانات

بعد ذلك، سنقوم بتعريف فئة لتنظيم البيانات التي نخطط لاستيرادها.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

هذا `DataItems` ستحتوي الفئة على الأعداد الصحيحة الخام والصيغ التي سنكتبها في ورقة Excel. 

## الخطوة 3: تهيئة قائمة لاحتواء عناصر البيانات

سنستخدم قائمة لحفظ مثيلات متعددة من `DataItems` فصل.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## الخطوة 4: إضافة عناصر البيانات إلى القائمة

الآن، لنُضِف بعض المُدخلات إلى قائمتنا. سيحتوي كل مُدخل على رقمين وصيغتين.

```csharp
// قم بتعريف كل عنصر بيانات وإضافته
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\"،\"موقع Aspose\")";
dis.Add(di);

// كرر ذلك لعناصر البيانات الإضافية
```

تأكد من تخصيص كل منها `DataItems` مثال بقيم وصيغ فريدة.

## الخطوة 5: إنشاء مصنف وورقة عمل Access

بعد ذلك، قم بإنشاء المصنف والوصول إلى ورقة العمل الأولى التي سنقوم في النهاية باستيراد البيانات منها.

```csharp
Workbook wb = new Workbook(); // إنشاء مصنف جديد
Worksheet ws = wb.Worksheets[0]; // الوصول إلى ورقة العمل الأولى
```

## الخطوة 6: تحديد خيارات استيراد الجدول

هنا يكمن السر. عليك تحديد الحقول في بياناتك التي تتوافق مع الصيغ. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

في هذا المثال، يحتوي الحقلان الأخيران على صيغ، وهو ما يشار إليه بـ `true`، في حين تم تعيين الحقلين الأولين على `false`.

## الخطوة 7: استيراد الكائنات المخصصة

الآن بعد إعداد كل شيء، دعنا نستورد قائمة عناصر البيانات إلى ورقة العمل.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

يقوم هذا الخط باستيراد البيانات فعليًا بدءًا من الخلية A1.

## الخطوة 8: حساب الصيغ

نظرًا لأننا قمنا باستيراد بعض الصيغ، فمن الضروري حسابها.

```csharp
wb.CalculateFormula();
```

تضمن هذه الطريقة أن يتم تقييم الصيغ الخاصة بك بناءً على تبعياتها.

## الخطوة 9: ملاءمة الأعمدة تلقائيًا

لتتأكد من أن بياناتك قابلة للعرض، يمكنك ضبط الأعمدة تلقائيًا استنادًا إلى المحتوى.

```csharp
ws.AutoFitColumns();
```

تعمل هذه الخطوة على تحسين تخطيط ملف Excel. 

## الخطوة 10: احفظ ملف Excel الخاص بك

وأخيرًا، حان الوقت لحفظ ملف Excel الذي قمت بإنشائه حديثًا. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

تأكد من أن اسم ملف الإخراج الخاص بك ذو صلة ووصفي!

## الخطوة 11: التحقق من التنفيذ

كطريقة بسيطة للتأكد من أن كل شيء يسير بشكل صحيح، قد ترغب في طباعة رسالة.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

وهذا يمنحك ردود فعل فورية بأن الكود يعمل دون أي مشاكل.

## خاتمة

ها قد انتهيت! لقد نجحت في استيراد البيانات إلى ورقة Excel باستخدام Aspose.Cells لـ .NET وحقول الصيغ المحددة. باتباع هذه الخطوات، يمكنك تطبيق تقنيات مشابهة لأتمتة مهام معالجة البيانات المصممة خصيصًا لاحتياجاتك. سواء كنت تُجري تحليلات للتقارير أو تُحافظ على البيانات، فإن إتقان فن التعامل مع Excel باستخدام Aspose مهارة تستحق العناء.

## الأسئلة الشائعة

### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة .NET مصممة لإنشاء ملفات Excel ومعالجتها وتحويلها برمجيًا.

### كيف أقوم بتثبيت Aspose.Cells لـ .NET؟
يمكنك تنزيله من [إصدارات Aspose](https://releases.aspose.com/cells/net/) وأشير إليه في مشروعك.

### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم، تقدم Aspose نسخة تجريبية مجانية متاحة على [هذا الرابط](https://releases.aspose.com/).

### أين يمكنني العثور على المزيد من الأمثلة؟
يمكن العثور على أمثلة ووثائق إضافية في [صفحة توثيق Aspose](https://reference.aspose.com/cells/net/).

### ماذا لو واجهت مشاكل أثناء استخدام Aspose؟
يمكنك طلب المساعدة من منتدى دعم Aspose [هنا](https://forum.aspose.com/c/cells/9).
 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}