---
title: إضافة التوقيع الرقمي إلى ملف Excel الموقّع
linktitle: إضافة التوقيع الرقمي إلى ملف Excel الموقّع
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إضافة توقيع رقمي إلى ملف Excel موقّع بالفعل باستخدام Aspose.Cells for .NET في هذا الدليل التفصيلي. قم بتأمين مستنداتك.
weight: 12
url: /ar/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة التوقيع الرقمي إلى ملف Excel الموقّع

## مقدمة
في عالمنا الرقمي اليوم، يعد ضمان صحة وسلامة المستندات أمرًا بالغ الأهمية. تعمل التوقيعات الرقمية كوسيلة قوية للتحقق من عدم تغيير المستند ومن أنه يأتي من مصدر شرعي. إذا كنت تعمل مع ملفات Excel في .NET وتريد إضافة توقيع رقمي إلى ملف موقّع بالفعل، فأنت في المكان المناسب! في هذا الدليل، سنرشدك خلال عملية إضافة توقيع رقمي جديد إلى ملف Excel موقّع موجود باستخدام Aspose.Cells لـ .NET. 
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل، دعنا نتأكد من أن لديك كل ما تحتاجه للبدء:
1.  Aspose.Cells لـ .NET: أولاً وقبل كل شيء، ستحتاج إلى تثبيت Aspose.Cells في بيئة .NET الخاصة بك. يمكنك تنزيله من[صفحة الإصدار](https://releases.aspose.com/cells/net/).
2. .NET Framework: تأكد من تثبيت .NET Framework على جهازك. يفترض هذا الدليل أنك على دراية بمفاهيم برمجة .NET الأساسية.
3. الشهادة الرقمية: ستحتاج إلى شهادة رقمية صالحة (بتنسيق .pfx) لإنشاء توقيع رقمي. إذا لم يكن لديك شهادة رقمية، فيمكنك إنشاء شهادة ذاتية التوقيع لأغراض الاختبار.
4. بيئة التطوير: محرر أكواد أو IDE مثل Visual Studio حيث يمكنك كتابة وتنفيذ كود C# الخاص بك.
5. ملف Excel نموذجي: يجب أن يكون لديك ملف Excel موجود بالفعل وموقع رقميًا. سيكون هذا هو الملف الذي نضيف إليه توقيعًا آخر.
بعد الانتهاء من هذه المتطلبات الأساسية، دعنا ننتقل إلى الكود!
## استيراد الحزم
قبل أن تبدأ في كتابة التعليمات البرمجية، تأكد من استيراد المساحات الأساسية اللازمة. إليك ما تحتاج إلى تضمينه في أعلى ملف C# الخاص بك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
ستتيح لك هذه المساحات الأسماء الوصول إلى الفئات والطرق المطلوبة للتعامل مع ملفات Excel والتعامل مع التوقيعات الرقمية.
الآن، دعنا نقسم العملية إلى خطوات يمكن إدارتها. سنتناول كل خطوة للتأكد من فهمك لكيفية إضافة توقيع رقمي إلى ملف Excel موقّع بالفعل.
## الخطوة 1: قم بتحديد الدلائل الخاصة بك
أولاً، عليك تحديد مكان وجود ملفات المصدر ومكان حفظ ملف الإخراج. هذا الأمر بسيط ولكنه بالغ الأهمية:
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory"; // استبدل بالدليل الفعلي الخاص بك
// دليل الإخراج
string outputDir = "Your Document Directory"; // استبدل بالدليل الفعلي الخاص بك
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي يتم تخزين ملفاتك فيه. وهذا يمهد الطريق لعمليات الملفات الخاصة بك.
## الخطوة 2: تحميل المصنف الموقّع الموجود
بعد ذلك، ستقوم بتحميل مصنف Excel الموجود الذي تم توقيعه بالفعل. وهنا تبدأ السحر:
```csharp
// قم بتحميل المصنف الذي تم توقيعه رقميًا بالفعل لإضافة توقيع رقمي جديد
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
 يقوم هذا الخط بإنشاء خط جديد`Workbook` الكائن بالملف المحدد. تأكد من أن اسم الملف يتطابق مع ملف Excel الموقّع الحالي لديك.
## الخطوة 3: إنشاء مجموعة توقيعات رقمية
لإدارة توقيعاتك الرقمية، تحتاج إلى إنشاء مجموعة. يتيح لك هذا الاحتفاظ بتوقيعات متعددة إذا لزم الأمر:
```csharp
// إنشاء مجموعة التوقيعات الرقمية
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
ستكون هذه المجموعة هي المكان الذي يمكنك من خلاله إضافة توقيعك الرقمي الجديد قبل تطبيقه على المصنف.
## الخطوة 4: تحميل الشهادة الخاصة بك
الآن، حان وقت تحميل الشهادة الرقمية. سيتم استخدام هذه الشهادة لإنشاء التوقيع الجديد:
```csharp
// ملف الشهادة وكلمة المرور الخاصة به
string certFileName = sourceDir + "AsposeDemo.pfx"; // ملف الشهادة الخاص بك
string password = "aspose"; //كلمة مرور الشهادة الخاصة بك
// إنشاء شهادة جديدة
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
 تأكد من الاستبدال`AsposeDemo.pfx` باستخدام اسم ملف الشهادة الخاص بك وقم بتحديث كلمة المرور وفقًا لذلك. هذه الخطوة بالغة الأهمية لأنه بدون الشهادة الصحيحة، لن تتمكن من إنشاء توقيع صالح.
## الخطوة 5: إنشاء توقيع رقمي جديد
بعد تحميل شهادتك، يمكنك الآن إنشاء توقيع رقمي جديد. سيتم إضافة هذا التوقيع إلى مجموعتك:
```csharp
// إنشاء توقيع رقمي جديد وإضافته إلى مجموعة التوقيعات الرقمية
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
هنا، يمكنك تقديم رسالة تصف التوقيع، وهو ما قد يكون مفيدًا لحفظ السجلات. تضمن علامة الوقت أن يكون التوقيع مرتبطًا باللحظة الصحيحة في الوقت.
## الخطوة 6: إضافة مجموعة التوقيعات إلى المصنف
بعد إنشاء التوقيع، حان الوقت لإضافة المجموعة بأكملها إلى المصنف:
```csharp
// إضافة مجموعة التوقيعات الرقمية داخل المصنف
workbook.AddDigitalSignature(dsCollection);
```
تطبق هذه الخطوة بشكل فعال توقيعك الرقمي الجديد على المصنف، مما يميزه بالمصداقية المضافة.
## الخطوة 7: احفظ المصنف
أخيرًا، احفظ المصنف مع التوقيع الرقمي الجديد المضمن فيه. هذه هي اللحظة التي ستؤتي فيها كل جهودك ثمارها:
```csharp
//احفظ المصنف وتخلص منه.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
تأكد من تحديد اسم لملف الإخراج. سيكون هذا هو الإصدار الجديد من ملف Excel الخاص بك، مكتملًا بالتوقيع الرقمي الإضافي.
## الخطوة 8: تأكيد النجاح
ولتلخيص الأمور، من الجيد تقديم تعليقات بمجرد اكتمال العملية بنجاح:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
سيؤدي هذا السطر إلى طباعة رسالة تأكيد على وحدة التحكم، لإعلامك بأن كل شيء سار بسلاسة.
## خاتمة
والآن، لقد نجحت في إضافة توقيع رقمي جديد إلى ملف Excel موقّع بالفعل باستخدام Aspose.Cells for .NET. لا تعمل هذه العملية على تعزيز أمان مستنداتك فحسب، بل تضمن أيضًا أنها جديرة بالثقة ويمكن التحقق منها. 
تُعد التوقيعات الرقمية ضرورية في عالم اليوم الرقمي، وخاصة للشركات والمحترفين الذين يحتاجون إلى الحفاظ على سلامة مستنداتهم. باتباع هذا الدليل، يمكنك بسهولة إدارة التوقيعات الرقمية في ملفات Excel الخاصة بك، مما يضمن بقاء بياناتك آمنة وموثوقة.
## الأسئلة الشائعة
### ما هو التوقيع الرقمي؟
التوقيع الرقمي هو مخطط رياضي للتحقق من صحة وسلامة الرسائل أو المستندات الرقمية. فهو يضمن عدم تغيير المستند ويؤكد هوية المُوقِّع.
### هل أحتاج إلى شهادة خاصة لإنشاء توقيع رقمي؟
نعم، أنت بحاجة إلى شهادة رقمية صادرة عن هيئة تصديق موثوقة (CA) لإنشاء توقيع رقمي صالح.
### هل يمكنني استخدام شهادة موقعة ذاتيًا للاختبار؟
بالتأكيد! يمكنك إنشاء شهادة موقعة ذاتيًا لأغراض التطوير والاختبار، ولكن بالنسبة للإنتاج، من الأفضل استخدام شهادة من جهة اعتماد موثوقة.
### ماذا يحدث إذا حاولت إضافة توقيع إلى مستند غير موقع؟
إذا حاولت إضافة توقيع رقمي إلى مستند غير موقّع بالفعل، فستعمل العملية دون مشاكل، ولكن التوقيع الأصلي لن يكون موجودًا.
### أين يمكنني العثور على مزيد من المعلومات حول Aspose.Cells؟
 يمكنك التحقق من[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) للحصول على أدلة مفصلة ومراجع API.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
