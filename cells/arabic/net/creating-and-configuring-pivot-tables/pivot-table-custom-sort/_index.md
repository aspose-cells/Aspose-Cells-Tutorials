---
title: فرز جدول محوري مخصص برمجيًا في .NET
linktitle: فرز جدول محوري مخصص برمجيًا في .NET
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية فرز جداول البيانات المحورية برمجيًا في .NET باستخدام Aspose.Cells. دليل خطوة بخطوة يغطي الإعداد والتكوين والفرز وحفظ النتائج كملفات Excel وPDF.
weight: 29
url: /ar/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فرز جدول محوري مخصص برمجيًا في .NET

## مقدمة
عندما يتعلق الأمر بالعمل مع Excel في بيئة .NET، تبرز مكتبة واحدة من بين البقية: Aspose.Cells. الآن، ألا تحب الأمر عندما تسمح لك أداة بالتلاعب بجداول البيانات برمجيًا؟ هذا هو بالضبط ما تفعله Aspose.Cells! في البرنامج التعليمي اليوم، نتعمق في عالم جداول البيانات المحورية ونوضح لك كيفية تنفيذ الفرز المخصص برمجيًا باستخدام هذه المكتبة متعددة الاستخدامات.
## المتطلبات الأساسية
قبل أن نشمر عن أكمامنا ونبدأ في التعامل مع الكود، تأكد من أن لديك بعض الأشياء في مكانها الصحيح:
1. Visual Studio: ستحتاج إلى إصدار صالح للعمل من Visual Studio. إنه الملعب الذي يحدث فيه كل السحر.
2. .NET Framework: تعد المعرفة ببرمجة .NET أمرًا ضروريًا. سواء كنت من المتحمسين لـ .NET Core أو .NET Framework، فأنت على استعداد للبدء.
3.  مكتبة Aspose.Cells: تحتاج إلى تثبيت مكتبة Aspose.Cells. يمكنك الحصول عليها من[رابط التحميل](https://releases.aspose.com/cells/net/) وأضفها إلى مشروعك.
4. الفهم الأساسي لجداول البيانات المحورية: على الرغم من أنك لست بحاجة إلى أن تكون خبيرًا، إلا أن القليل من المعرفة حول كيفية عمل جداول البيانات المحورية سيكون مفيدًا أثناء قيامنا بهذا البرنامج التعليمي.
5.  ملف Excel نموذجي: احصل على ملف Excel نموذجي باسم`SamplePivotSort.xlsx` جاهز في دليل العمل الخاص بك للاختبار.
## استيراد الحزم
بمجرد الانتهاء من ترتيب جميع المتطلبات الأساسية، فإن الخطوة الأولى هي استيراد الحزم اللازمة. للقيام بذلك، قم بتضمين الأسطر التالية في أعلى الكود الخاص بك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
توفر هذه الحزمة كافة الوظائف التي تحتاجها للتعامل مع ملفات Excel باستخدام Aspose.Cells.

حسنًا، لننتقل إلى الجزء الممتع! سنقوم بتقسيم عملية إنشاء جدول محوري وتطبيق الفرز المخصص إلى خطوات يمكن إدارتها.
## الخطوة 1: إعداد المصنف
للبدء، نحتاج إلى إعداد مصنف العمل الخاص بنا. إليك كيفية القيام بذلك:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 في هذه الخطوة، نقوم بتهيئة ملف جديد`Workbook` مثال مع المسار إلى ملف Excel الخاص بنا. يعمل هذا كلوحة حيث ستظهر جدول Pivot الخاص بنا بشكل حي.
## الخطوة 2: الوصول إلى ورقة العمل
بعد ذلك، نحتاج إلى الوصول إلى ورقة العمل التي سنضيف إليها جدولنا المحوري.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 هنا، نأخذ ورقة العمل الأولى في مصنفنا ونستدعي`PivotTableCollection`تتيح لنا هذه المجموعة إدارة كافة جداول البيانات المحورية الموجودة في ورقة العمل هذه.
## الخطوة 3: إنشاء جدولك المحوري الأول
الآن حان الوقت لإنشاء جدولنا المحوري.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
نضيف جدولًا محوريًا جديدًا إلى ورقة العمل الخاصة بنا، مع تحديد نطاق البيانات وموقعه. يشير "E3" إلى المكان الذي نريد أن يبدأ فيه جدولنا المحوري. ثم نشير إلى جدولنا المحوري الجديد باستخدام فهرسه.
## الخطوة 4: تكوين إعدادات جدول المحور
لنبدأ في تكوين جدولنا المحوري! وهذا يعني التحكم في جوانب مثل الإجماليات الكلية وترتيبات الحقول.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
نضمن عدم عرض الإجماليات الكلية للصفوف والأعمدة، مما قد يجعل البيانات أكثر نظافة. ثم نضيف الحقل الأول إلى منطقة الصف، مما يتيح الفرز التلقائي والفرز التصاعدي.
## الخطوة 5: إضافة الأعمدة وحقول البيانات
بمجرد تعيين الصفوف، دعنا نضيف حقول العمود والبيانات.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
نضيف الحقل الثاني كعمود وننسقه كتاريخ. مرة أخرى، نقوم بتمكين الفرز التلقائي والترتيب التصاعدي للحفاظ على تنظيم الأشياء. أخيرًا، نحتاج إلى إضافة الحقل الثالث إلى منطقة البيانات الخاصة بنا:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## الخطوة 6: تحديث جدول البيانات المحوري وحسابه
بعد إضافة جميع الحقول اللازمة، دعنا نتأكد من أن جدول Pivot الخاص بنا جديد وجاهز.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
تعمل هذه الطرق على تحديث البيانات وإعادة حسابها، مما يضمن تحديث كل شيء وعرضه بشكل صحيح في جدولنا المحوري.
## الخطوة 7: الفرز المخصص استنادًا إلى قيم حقل الصف
دعنا نضيف القليل من الأناقة عن طريق فرز جدول البيانات المحوري استنادًا إلى قيم محددة، مثل "المأكولات البحرية".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
نحن نكرر العملية عن طريق إنشاء جدول محوري آخر وإعداده على نحو مماثل للجدول الأول. يمكننا الآن تخصيصه بشكل أكبر:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## الخطوة 8: تخصيص الفرز الإضافي دعنا نجرب طريقة فرز أخرى بناءً على تاريخ محدد:
```csharp
// إضافة جدول محوري آخر للفرز حسب التاريخ
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// كرر إعدادات الصفوف والأعمدة على غرار الخطوات السابقة
```
كل ما عليك فعله هو تكرار نفس العملية، لإنشاء جدول محوري ثالث مع معايير الفرز الخاصة به المصممة خصيصًا لتلبية احتياجاتك.
## الخطوة 9: احفظ المصنف حان الوقت لحفظ كل العمل الشاق الذي بذلناه!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 هنا، يمكنك حفظ المصنف كملف Excel وملف PDF.`PdfSaveOptions` يسمح بتنسيق أفضل، مما يضمن ظهور كل ورقة على صفحة منفصلة عند التحويل.
## الخطوة 10: الإنهاءقم بإنهاء كل شيء من خلال إعلام المستخدم بأن كل شيء على ما يرام.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## خاتمة
بحلول هذا الوقت، تعلمت كيفية الاستفادة من قوة Aspose.Cells لإنشاء جداول محورية وتخصيصها في تطبيقات .NET الخاصة بك. من الإعداد الأولي إلى الفرز المخصص، تتحد كل خطوة لتقديم تجربة سلسة. سواء كنت بحاجة إلى تقديم بيانات المبيعات السنوية أو تتبع إحصائيات المخزون، فإن هذه المهارات ستخدمك جيدًا!
## الأسئلة الشائعة
### ما هو الجدول المحوري؟
الجدول المحوري هو أداة معالجة بيانات في Excel تتيح لك تلخيص البيانات وتحليلها، مما يوفر طريقة مرنة لاستخراج المعلومات بسهولة.
### كيف أقوم بتثبيت Aspose.Cells؟
 يمكنك تثبيته عبر NuGet في Visual Studio أو تنزيله مباشرة من[رابط التحميل](https://releases.aspose.com/cells/net/).
### هل هناك نسخة تجريبية من Aspose.Cells؟
 نعم! يمكنك تجربته مجانًا من خلال زيارة[رابط التجربة المجانية](https://releases.aspose.com/).
### هل يمكنني فرز حقول متعددة في جدول محوري؟
بالتأكيد! يمكنك إضافة وفرز حقول متعددة وفقًا لمتطلباتك.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
 المجتمع نشط للغاية، ويمكنك طرح الأسئلة على المنتدى الخاص بهم[هنا](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
