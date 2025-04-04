---
title: تغيير بيانات المصدر لجدول محوري برمجيًا في .NET
linktitle: تغيير بيانات المصدر لجدول محوري برمجيًا في .NET
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تغيير بيانات مصدر جدول المحور برمجيًا باستخدام Aspose.Cells لـ .NET من خلال البرنامج التعليمي الشامل الخاص بنا خطوة بخطوة.
weight: 10
url: /ar/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير بيانات المصدر لجدول محوري برمجيًا في .NET

## مقدمة
في عالم تحليل البيانات، لا تتألق سوى أدوات قليلة مثل Microsoft Excel. يعتمد عدد لا يحصى من المستخدمين على Excel لإدارة وتحليل البيانات يوميًا، ولكن وراء الكواليس، يكون الأمر أكثر تعقيدًا من مجرد النقر والسحب. إذا كنت ترغب في معالجة ملفات Excel برمجيًا - على وجه التحديد، لتغيير بيانات المصدر لجدول محوري - فأنت في المكان المناسب! في هذا الدليل، سنستكشف كيف يمكنك تحقيق ذلك باستخدام Aspose.Cells for .NET. سواء كنت مطورًا متمرسًا أو تغوص للتو في بحر البرمجة، فستجد هذا البرنامج التعليمي مليئًا بالمعلومات القيمة التي يسهل اتباعها.
## المتطلبات الأساسية
قبل أن نبدأ رحلتنا لتغيير بيانات المصدر لجدول محوري، دعنا نتأكد من إعداد كل شيء وتجهيزه:
1. Visual Studio: تأكد من أن لديك نسخة من Microsoft Visual Studio مثبتة، حيث سنقوم بكتابة الكود الخاص بنا هنا.
2. مكتبة Aspose.Cells: ستحتاج إلى تنزيل مكتبة Aspose.Cells والإشارة إليها في مشروعك. يمكنك تنزيلها[هنا](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: على الرغم من أن هذا البرنامج التعليمي مبسط، إلا أن فهم لغة C# سيساعدك على فهم الكود بشكل أفضل.
4. ملف Excel: يجب أن يكون لديك ملف Excel نموذجي (مثل "Book1.xlsx") يحتوي على جدول محوري يمكننا التعامل معه.
حسنًا، مع التحقق من هذه المتطلبات الأساسية، يمكننا المضي قدمًا في استيراد الحزم اللازمة والحصول على الترميز!
## استيراد الحزم
أولاً وقبل كل شيء، دعنا نستورد الحزم التي سنحتاجها. افتح مشروع C# الخاص بك في Visual Studio وأضف التعليمات التالية في أعلى ملف التعليمات البرمجية الخاص بك:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
ستتيح لك هذه المساحات الاسمية الوصول إلى الفئات الأساسية اللازمة للعمل مع ملفات Excel ومعالجة محتوياتها باستخدام Aspose.Cells.

الآن، دعنا نقسم العملية إلى خطوات يمكن إدارتها. سنشرح كيفية فتح ملف Excel وتعديل ورقة العمل وتغيير مصدر بيانات الجدول المحوري وحفظ النتائج.
## الخطوة 1: قم بتحديد دليل المستندات الخاص بك
 أولاً، عليك تحديد مكان ملف Excel الخاص بك. قم بتعديل`dataDir` متغير للإشارة إلى المجلد الذي يحتوي على "Book1.xlsx".
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
```
يقوم هذا السطر بإعداد الدليل الذي سيتم تخزين ملف Excel فيه، مما يجعل الوصول إليه لاحقًا أسهل.
## الخطوة 2: تحديد مسار الإدخال
بعد ذلك، دعنا ننشئ سلسلة لتحديد المسار الكامل لملف Excel المدخل الخاص بك:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
يساعد هذا في تبسيط الوصول إلى الملف الخاص بك؛ فلن تضطر إلى الاستمرار في كتابة نفس المسار عدة مرات في جميع أنحاء الكود الخاص بك.
## الخطوة 3: إنشاء تدفق ملف
 الآن حان الوقت لفتح ملف Excel. سنقوم بإنشاء`FileStream` الذي يسمح لك بقراءة محتوى ملف Excel:
```csharp
// إنشاء مجرى ملف يحتوي على ملف Excel الذي سيتم فتحه
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
يفتح هذا السطر الملف في وضع القراءة، مما يسمح لنا بالوصول إلى بياناته.
## الخطوة 4: تحميل المصنف
مع وجود مجرى الملف في مكانه، فإن الخطوة التالية هي تحميل المصنف:
```csharp
// فتح ملف Excel من خلال مجرى الملف
Workbook workbook = new Workbook(fstream);
```
 يقوم هذا الأمر بأخذ ملف Excel الخاص بك وتحميله في`Workbook` بمجرد تحميل الملف، يمكنك التعامل معه حسب الحاجة.
## الخطوة 5: الوصول إلى ورقة العمل
حان الوقت للتعمق في التفاصيل. سننتقل إلى ورقة العمل الأولى في المصنف:
```csharp
// الوصول إلى ورقة العمل الأولى في ملف Excel
Worksheet worksheet = workbook.Worksheets[0];
```
يتيح لك هذا الوصول المباشر إلى البيانات الموجودة في ورقة العمل الأولى، مما يسهل تعديلها.
## الخطوة 6: ملء البيانات الجديدة
بعد ذلك، نريد إدراج بيانات جديدة في الخلايا. في هذا المثال، سنضيف بعض البيانات النموذجية:
```csharp
// ملء البيانات الجديدة في خلايا ورقة العمل
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 هنا، نضع القيم "Golf" و"Qtr4" و`7000` في خلايا محددة. يمكنك تغيير هذه القيم إلى ما يناسب احتياجاتك.
## الخطوة 7: تغيير النطاق المسمى
الآن، سنقوم بتغيير النطاق المسمى الذي يشير إليه جدول البيانات المحوري. يتضمن هذا إنشاء نطاق أو تحديثه:
```csharp
// تغيير النطاق المسمى "مصدر البيانات"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
من خلال تحديد نطاق جديد، نضمن أن الجدول المحوري يستخدم هذه البيانات الجديدة عند تحديثه.
## الخطوة 8: احفظ ملف Excel المعدّل
بعد كل التغييرات، من المهم حفظ عملك! دعنا نحفظ المصنف المعدل:
```csharp
// حفظ ملف Excel المعدل
workbook.Save(dataDir + "output.xls");
```
يؤدي هذا الأمر إلى حفظ المصنف في ملف جديد، حتى لا تتمكن من الكتابة فوق الملف الأصلي إلا إذا كنت ترغب في ذلك!
## الخطوة 9: إغلاق مجرى الملف
أخيرًا، من الضروري إغلاق مجرى الملف لتحرير أي موارد تستخدمها:
```csharp
// إغلاق مجرى الملف لتحرير كافة الموارد
fstream.Close();
```
تضمن هذه الخطوة عدم تسرب الذاكرة في تطبيقك وبقاءه فعالاً.
## خاتمة
تهانينا! لقد نجحت للتو في تغيير بيانات المصدر لجدول محوري برمجيًا في .NET باستخدام Aspose.Cells. تفتح هذه الوظيفة العديد من الاحتمالات لأتمتة مهام Excel وتحسين سير العمل لديك. سواء كنت تقوم بتحديث التقارير المالية أو تتبع بيانات المبيعات أو حتى مجرد اللعب بمجموعات البيانات، فإن القدرة على القيام بذلك برمجيًا يمكن أن توفر لك الكثير من الوقت وتقلل من خطر الأخطاء.

## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة .NET قوية للعمل مع ملفات Excel، مما يسمح للمستخدمين بإنشاء مستندات Excel وتعديلها ومعالجتها برمجيًا.
### هل يمكنني تغيير بيانات المصدر لجداول المحور الموجودة باستخدام هذه الطريقة؟
بالتأكيد! تتيح لك هذه الطريقة تحديث مصدر البيانات لجداول البيانات المحورية الموجودة ضمن مصنف Excel الخاص بك.
### هل أحتاج إلى تثبيت Office لاستخدام Aspose.Cells؟
لا! Aspose.Cells عبارة عن مكتبة مستقلة، مما يعني أنك لا تحتاج إلى تثبيت Microsoft Office للعمل مع ملفات Excel.
### هل استخدام Aspose.Cells مجاني؟
يقدم Aspose.Cells إصدارًا تجريبيًا مجانيًا، ولكن للحصول على الوظائف الكاملة، سيتعين عليك شراء ترخيص. يمكنك العثور على التفاصيل[هنا](https://purchase.aspose.com/buy).
### أين يمكنني العثور على المزيد من الأمثلة والدعم؟
 لمزيد من الأمثلة والدعم، راجع[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) ومنتدى مجتمعهم[هنا](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
