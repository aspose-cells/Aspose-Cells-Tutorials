---
"description": "تعرّف على كيفية إضافة توقيع رقمي إلى ملف Excel مُوقّع مسبقًا باستخدام Aspose.Cells لـ .NET في هذا الدليل المُفصّل. حمِّل مستنداتك بأمان."
"linktitle": "إضافة التوقيع الرقمي إلى ملف Excel الموقّع"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إضافة التوقيع الرقمي إلى ملف Excel الموقّع"
"url": "/ar/net/workbook-operations/add-digital-signature-to-signed-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة التوقيع الرقمي إلى ملف Excel الموقّع

## مقدمة
في عالمنا الرقمي اليوم، يُعدّ ضمان صحة وسلامة المستندات أمرًا بالغ الأهمية. تُعدّ التوقيعات الرقمية وسيلةً فعّالة للتحقق من عدم تعديل المستند ومن أنه صادر من مصدر شرعي. إذا كنت تعمل على ملفات Excel في .NET وترغب في إضافة توقيع رقمي إلى ملف مُوقّع مسبقًا، فأنت في المكان المناسب! في هذا الدليل، سنشرح لك عملية إضافة توقيع رقمي جديد إلى ملف Excel مُوقّع موجود باستخدام Aspose.Cells لـ .NET. 
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل، دعنا نتأكد من أن لديك كل ما تحتاجه للبدء:
1. Aspose.Cells لـ .NET: أولًا وقبل كل شيء، ستحتاج إلى تثبيت Aspose.Cells في بيئة .NET لديك. يمكنك تنزيله من [صفحة الإصدار](https://releases.aspose.com/cells/net/).
2. إطار عمل .NET: تأكد من تثبيت إطار عمل .NET على جهازك. يفترض هذا الدليل أنك مُلِمٌّ بمفاهيم برمجة .NET الأساسية.
3. الشهادة الرقمية: ستحتاج إلى شهادة رقمية صالحة (بتنسيق .pfx) لإنشاء توقيع رقمي. إذا لم تكن لديك واحدة، يمكنك إنشاء شهادة ذاتية التوقيع لأغراض الاختبار.
4. بيئة التطوير: محرر أكواد أو IDE مثل Visual Studio حيث يمكنك كتابة وتنفيذ كود C# الخاص بك.
5. ملف إكسل نموذجي: يجب أن يكون لديك ملف إكسل مُوقّع رقميًا. هذا هو الملف الذي سنضيف إليه توقيعًا جديدًا.
بعد الانتهاء من هذه المتطلبات الأساسية، دعنا ننتقل إلى الكود!
## استيراد الحزم
قبل البدء بالبرمجة، تأكد من استيراد مساحات الأسماء اللازمة. إليك ما يجب تضمينه في أعلى ملف C#:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
ستتيح لك هذه المساحات الوصول إلى الفئات والطرق المطلوبة للتعامل مع ملفات Excel والتعامل مع التوقيعات الرقمية.
الآن، لنُقسّم العملية إلى خطوات سهلة. سنشرح كل خطوة للتأكد من فهمك لكيفية إضافة توقيع رقمي إلى ملف Excel مُوقّع مسبقًا.
## الخطوة 1: تحديد الدلائل الخاصة بك
أولاً، عليك تحديد مكان ملفات المصدر ومكان حفظ ملف الإخراج. هذا بسيط ولكنه بالغ الأهمية:
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory"; // استبدل بالدليل الفعلي الخاص بك
// دليل الإخراج
string outputDir = "Your Document Directory"; // استبدل بالدليل الفعلي الخاص بك
```
يستبدل `"Your Document Directory"` مع المسار الفعلي لتخزين ملفاتك. هذا يُهيئ الظروف لعمليات ملفاتك.
## الخطوة 2: تحميل المصنف الموقّع الموجود
بعد ذلك، ستحمّل مصنف Excel الحالي المُوقّع. وهنا تبدأ العملية:
```csharp
// قم بتحميل المصنف الذي تم توقيعه رقميًا بالفعل لإضافة توقيع رقمي جديد
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
يقوم هذا الخط بتهيئة سطر جديد `Workbook` الكائن بالملف المحدد. تأكد من أن اسم الملف يطابق ملف Excel المُوقّع الحالي لديك.
## الخطوة 3: إنشاء مجموعة توقيعات رقمية
لإدارة توقيعاتك الرقمية، عليك إنشاء مجموعة. يتيح لك هذا حفظ توقيعات متعددة عند الحاجة:
```csharp
// إنشاء مجموعة التوقيعات الرقمية
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
ستكون هذه المجموعة هي المكان الذي يمكنك من خلاله إضافة توقيعك الرقمي الجديد قبل تطبيقه على المصنف.
## الخطوة 4: تحميل الشهادة الخاصة بك
الآن، حان وقت تحميل شهادتك الرقمية. ستُستخدم هذه الشهادة لإنشاء التوقيع الجديد:
```csharp
// ملف الشهادة وكلمة المرور الخاصة به
string certFileName = sourceDir + "AsposeDemo.pfx"; // ملف الشهادة الخاص بك
string password = "aspose"; // كلمة مرور الشهادة الخاصة بك
// إنشاء شهادة جديدة
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
تأكد من الاستبدال `AsposeDemo.pfx` أدخل اسم ملف الشهادة، ثم حدِّث كلمة المرور وفقًا لذلك. هذه الخطوة بالغة الأهمية، لأنه بدون الشهادة الصحيحة، لن تتمكن من إنشاء توقيع صالح.
## الخطوة 5: إنشاء توقيع رقمي جديد
بعد تحميل شهادتك، يمكنك الآن إنشاء توقيع رقمي جديد. سيُضاف هذا التوقيع إلى مجموعتك.
```csharp
// إنشاء توقيع رقمي جديد وإضافته إلى مجموعة التوقيعات الرقمية
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
هنا، تُقدّم رسالة تصف التوقيع، مما يُساعد في حفظ السجلات. يضمن الطابع الزمني ارتباط التوقيع بالوقت الصحيح.
## الخطوة 6: إضافة مجموعة التوقيعات إلى المصنف
بعد إنشاء التوقيع، حان الوقت لإضافة المجموعة بأكملها إلى المصنف:
```csharp
// إضافة مجموعة التوقيعات الرقمية داخل المصنف
workbook.AddDigitalSignature(dsCollection);
```
تطبق هذه الخطوة توقيعك الرقمي الجديد على المصنف بشكل فعال، مما يمنحه مزيدًا من الأصالة.
## الخطوة 7: حفظ المصنف
أخيرًا، احفظ مصنف العمل مع التوقيع الرقمي الجديد. هذه هي اللحظة التي تُثمر فيها جهودك:
```csharp
// احفظ المصنف وتخلص منه.
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
تأكد من تحديد اسم لملف الإخراج. سيكون هذا هو الإصدار الجديد من ملف Excel، مكتملًا بالتوقيع الرقمي الإضافي.
## الخطوة 8: تأكيد النجاح
ولإنهاء الأمور، من الجيد تقديم تعليقات بمجرد اكتمال العملية بنجاح:
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
سيؤدي هذا السطر إلى طباعة رسالة تأكيد في وحدة التحكم، لإعلامك بأن كل شيء سار بسلاسة.
## خاتمة
وها أنت ذا! لقد نجحت في إضافة توقيع رقمي جديد إلى ملف Excel مُوقّع مسبقًا باستخدام Aspose.Cells لـ .NET. هذه العملية لا تُحسّن أمان مستنداتك فحسب، بل تضمن أيضًا موثوقيتها وقابليتها للتحقق. 
تُعد التوقيعات الرقمية ضرورية في عالمنا الرقمي اليوم، خاصةً للشركات والمحترفين الذين يحتاجون إلى الحفاظ على سلامة مستنداتهم. باتباع هذا الدليل، يمكنك بسهولة إدارة التوقيعات الرقمية في ملفات Excel، مما يضمن بقاء بياناتك آمنة وموثقة.
## الأسئلة الشائعة
### ما هو التوقيع الرقمي؟
التوقيع الرقمي هو نظام رياضي للتحقق من صحة وسلامة الرسائل أو المستندات الرقمية. فهو يضمن عدم تعديل المستند، ويؤكد هوية المُوقّع.
### هل أحتاج إلى شهادة خاصة لإنشاء توقيع رقمي؟
نعم، أنت بحاجة إلى شهادة رقمية صادرة عن هيئة إصدار شهادات موثوقة (CA) لإنشاء توقيع رقمي صالح.
### هل يمكنني استخدام شهادة موقعة ذاتيًا للاختبار؟
بالتأكيد! يمكنك إنشاء شهادة موقعة ذاتيًا لأغراض التطوير والاختبار، ولكن للإنتاج، يُفضل استخدام شهادة من جهة اعتماد موثوقة.
### ماذا يحدث إذا حاولت إضافة توقيع إلى مستند غير موقع؟
إذا حاولت إضافة توقيع رقمي إلى مستند غير موقّع بالفعل، فستعمل العملية دون مشاكل، ولكن التوقيع الأصلي لن يكون موجودًا.
### أين يمكنني العثور على مزيد من المعلومات حول Aspose.Cells؟
يمكنك التحقق من [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) للحصول على إرشادات مفصلة ومراجع API.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}