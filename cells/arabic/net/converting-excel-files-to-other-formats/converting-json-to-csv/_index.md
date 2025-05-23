---
"description": "تعرّف على كيفية تحويل JSON إلى CSV برمجيًا في .NET باستخدام Aspose.Cells. اتبع دليلنا خطوة بخطوة لضمان تحويل بيانات سلس."
"linktitle": "تحويل JSON إلى CSV برمجيًا في .NET"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تحويل JSON إلى CSV برمجيًا في .NET"
"url": "/ar/net/converting-excel-files-to-other-formats/converting-json-to-csv/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحويل JSON إلى CSV برمجيًا في .NET

## مقدمة
في عالمنا الرقمي اليوم، أصبح التعامل مع البيانات بتنسيقات متعددة أمرًا شائعًا، ويُعدّ JSON (ترميز كائنات جافا سكريبت) أحد أكثر التنسيقات استخدامًا لتبادل البيانات. ولكن ماذا يحدث عندما تحتاج إلى تحويل JSON إلى تنسيق أسهل للتحليل، مثل CSV (قيم مفصولة بفواصل)؟ سيرشدك هذا البرنامج التعليمي خلال عملية تحويل JSON إلى CSV برمجيًا باستخدام Aspose.Cells لـ .NET، وهي واجهة برمجة تطبيقات سهلة الاستخدام وفعّالة لمعالجة جداول البيانات. 
## المتطلبات الأساسية
قبل التعمق في الكود، من الضروري التأكد من امتلاكك جميع المكونات اللازمة وفهم أساسي للأدوات التي سنستخدمها. لنوضح ما تحتاجه:
- Aspose.Cells لـ .NET: هذه هي المكتبة الأساسية التي سنستخدمها لتحويل JSON إلى CSV. يمكنك [قم بتحميله هنا](https://releases.aspose.com/cells/net/).
- Visual Studio: ستحتاج إلى بيئة تطوير متكاملة (IDE) مثل Visual Studio لكتابة وتنفيذ كود .NET.
- .NET Framework: تأكد من تثبيت .NET Framework. Aspose.Cells متوافق مع كلٍّ من .NET Core و.NET Framework.
- المعرفة الأساسية بلغة C#: على الرغم من أن هذا الدليل سوف يشرح كل جزء من الكود، إلا أنه سيكون مفيدًا إذا كنت على دراية إلى حد ما بلغة C#.
## استيراد الحزم
لاستخدام Aspose.Cells في مشروع .NET الخاص بك، عليك أولاً تثبيت المكتبة. يمكنك القيام بذلك عبر مدير حزم NuGet:
1. افتح Visual Studio.
2. انتقل إلى الأدوات > مدير حزم NuGet > إدارة حزم NuGet للحل.
3. ابحث عن Aspose.Cells وقم بتثبيت الإصدار الأحدث.
بمجرد التثبيت، تأكد من تضمين مساحات الأسماء التالية في الكود الخاص بك:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
الآن بعد إعداد كل شيء، دعنا نقوم بتقسيم الكود خطوة بخطوة حتى تتمكن من رؤية مدى سهولة تحويل ملف JSON إلى CSV باستخدام Aspose.Cells.
## الخطوة 1: قراءة ملف JSON
أول ما علينا فعله هو قراءة بيانات JSON من ملف. سنفترض أن لديك ملف JSON بالفعل (لنسميه `SampleJson.json`) مخزنة في دليل على نظامك.
يمكنك استخدام `File.ReadAllText()` طريقة في C# لقراءة محتويات ملف JSON في سلسلة.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// قراءة ملف JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

هذه الخطوة بالغة الأهمية لأنك تحتاج بيانات JSON الخام لبدء عملية التحويل. بقراءتها كسلسلة نصية، تُجهّزها لمعالجتها بواسطة Aspose.Cells.
## الخطوة 2: إنشاء مصنف فارغ
يعمل Aspose.Cells بشكل أساسي على مصنفات العمل (ملفات Excel). لبدء استيراد بيانات JSON، عليك أولاً إنشاء مصنف عمل فارغ لإدراج هذه البيانات.
```csharp
// إنشاء مصنف فارغ
Workbook workbook = new Workbook();
```
هنا، تقوم بتهيئة مصنف فارغ سيحتوي في النهاية على بيانات بتنسيق CSV. تخيل الأمر كأنك تنشئ جدول بيانات فارغًا في Excel، سيتم ملؤه قريبًا ببيانات JSON.
## الخطوة 3: الوصول إلى الخلايا في المصنف
الآن بعد أن أصبح لدينا مصنف فارغ، نحتاج إلى الوصول إلى خلاياه. `Cells` تمثل المجموعة في Aspose.Cells جميع الخلايا في ورقة العمل، حيث ستضع بيانات JSON الخاصة بك.
```csharp
// الحصول على الخلايا
Cells cells = workbook.Worksheets[0].Cells;
```
يقوم مقتطف التعليمات البرمجية هذا بتحديد ورقة العمل الأولى (ورقة العمل في الفهرس 0) ويحصل على `Cells` المجموعة. هذه الخلايا تشبه شبكة جدول البيانات حيث سيتم إضافة البيانات.
## الخطوة 4: تعيين خيارات JsonLayoutOptions
يوفر Aspose.Cells خيارات تخصيص متعددة لكيفية استيراد بيانات JSON. هنا، نُعرّف `JsonLayoutOptions` لتحديد كيفية تعامل Aspose مع المصفوفات والبيانات الرقمية وعناوين الكائنات.
```csharp
// تعيين خيارات تخطيط Json
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: تحويل قيم السلسلة التي هي قيم رقمية أو تاريخية تلقائيًا.
- ArrayAsTable: التعامل مع المصفوفات في JSON مثل الجداول الموجودة في المصنف.
- IgnoreArrayTitle وIgnoreObjectTitle: تتجاهل هذه الخيارات عناوين المصفوفات والكائنات، مما يضمن استيراد البيانات الخام فقط.
## الخطوة 5: استيراد بيانات JSON
بمجرد تعيين خيارات التخطيط، حان الوقت لإحضار بيانات JSON. `JsonUtility.ImportData()` الطريقة تقوم بالعمل الشاق هنا، حيث تقوم بإدخال بيانات JSON في خلايا المصنف.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
تتطلب هذه الطريقة عدة معلمات:
- `str`:سلسلة JSON التي قرأناها في الخطوة 1.
- `cells`:مجموعة الخلايا التي سيتم وضع البيانات فيها.
- `0, 0`:هذه هي فهرس الصفوف والأعمدة التي تشير إلى المكان الذي يجب أن تبدأ فيه البيانات (أي الزاوية العلوية اليسرى).
- `importOptions`:خيارات التخطيط التي قمنا بتعيينها في الخطوة 4.
## الخطوة 6: حفظ المصنف بتنسيق CSV
الآن وقد أصبحت بيانات JSON في المصنف، يُمكننا بسهولة حفظه كملف CSV. يُعد CSV تنسيقًا بسيطًا وخفيفًا لتخزين البيانات الجدولية، مما يجعله مثاليًا لتحليل البيانات.
```csharp
// دليل الإخراج
string outputDir = "Your Document Directory";
// حفظ المصنف
workbook.Save(outputDir + @"SampleJson_out.csv");
```
في هذه الخطوة، نحفظ المصنف كملف CSV. حدد المسار واسم الملف (`SampleJson_out.csv`) حيث سيتم حفظ ملف CSV.
## الخطوة 7: تأكيد العملية
للتأكد من أن كل شيء يعمل كما هو متوقع، يمكننا طباعة رسالة تأكيد في وحدة التحكم.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
تساعد رسالة النجاح البسيطة في التأكيد على أن العملية تمت بسلاسة.
## خاتمة
تحويل بيانات JSON إلى CSV باستخدام Aspose.Cells لـ .NET عملية سهلة وفعّالة. ببضعة أسطر برمجية فقط، يمكنك تحويل بيانات JSON المعقدة إلى صيغة CSV أسهل استخدامًا. سواء كنت تتعامل مع مصفوفات أو كائنات أو بيانات رقمية، يُسهّل Aspose.Cells ضبط عملية التحويل لتناسب احتياجاتك.
## الأسئلة الشائعة
### هل يمكن لـ Aspose.Cells التعامل مع ملفات JSON كبيرة الحجم؟
نعم، تم تصميم Aspose.Cells للتعامل مع مجموعات البيانات الكبيرة بكفاءة، مما يجعله مناسبًا لمعالجة ملفات JSON الكبيرة دون مشاكل في الأداء.
### كيف يمكنني تخصيص إخراج CSV؟
يمكنك تخصيص إخراج CSV عن طريق ضبط `JsonLayoutOptions` أو معالجة تنسيق المصنف قبل حفظه بتنسيق CSV.
### هل هناك طريقة لاستبعاد بيانات معينة من JSON أثناء التحويل؟
نعم، من خلال تعديل JSON أو استخدام منطق الكود المخصص قبل الاستيراد، يمكنك استبعاد أو تصفية حقول بيانات معينة.
### هل يدعم Aspose.Cells تنسيقات ملفات أخرى إلى جانب CSV؟
بالتأكيد! يدعم Aspose.Cells مجموعة واسعة من التنسيقات، بما في ذلك Excel (XLS، XLSX)، وPDF، وHTML، وغيرها الكثير.
### كيف يمكنني تجربة Aspose.Cells مجانًا؟
أنت تستطيع [قم بتنزيل نسخة تجريبية مجانية هنا](https://releases.aspose.com/) لاختبار كافة الميزات قبل الشراء.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}