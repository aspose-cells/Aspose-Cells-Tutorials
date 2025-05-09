---
"description": "تعرّف على كيفية تحديد HTML CrossType في Aspose.Cells لـ .NET. اتبع دليلنا خطوة بخطوة لتحويل ملفات Excel إلى HTML بدقة."
"linktitle": "تحديد HTML CrossType في إخراج HTML برمجيًا في .NET"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تحديد HTML CrossType في إخراج HTML برمجيًا في .NET"
"url": "/ar/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحديد HTML CrossType في إخراج HTML برمجيًا في .NET

## مقدمة
عند تحويل ملفات Excel إلى HTML في تطبيقات .NET، قد تحتاج إلى تحديد كيفية معالجة المراجع التبادلية في المخرجات. توفر فئة HtmlSaveOptions في Aspose.Cells لـ .NET إعدادات متنوعة للتحكم في عملية التحويل، ومن بينها HtmlCrossType. في هذا البرنامج التعليمي، سنشرح كيفية تحديد نوع HTML التبادلي برمجيًا عند تصدير ملفات Excel إلى تنسيق HTML. 
## المتطلبات الأساسية
قبل الغوص في الكود، تأكد من أن لديك ما يلي:
- Aspose.Cells لـ .NET: تأكد من تثبيت مكتبة Aspose.Cells في مشروعك. يمكنك تنزيلها من [موقع Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: تثبيت عمل لبرنامج Visual Studio أو أي بيئة تطوير .NET أخرى.
- المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الأمثلة بشكل أفضل.
- ملف إكسل نموذجي: جهّز ملف إكسل نموذجي للعمل عليه. في هذا المثال، سنستخدم `sampleHtmlCrossStringType.xlsx`.
## استيراد الحزم
للبدء، ستحتاج إلى استيراد مساحات أسماء Aspose.Cells اللازمة. إليك كيفية القيام بذلك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
دعنا نوضح ذلك خطوة بخطوة، مما يجعل من السهل عليك متابعة هذه الوظيفة وتنفيذها في مشاريعك الخاصة.
## الخطوة 1: تحديد دليل المصدر والإخراج
أولاً، عليك تعيين الدلائل لملف Excel المصدر والمكان الذي تريد حفظ ملف HTML الناتج فيه.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
## الخطوة 2: تحميل ملف Excel النموذجي
بعد ذلك، قم بتحميل ملف Excel الخاص بك إلى `Workbook` هذا هو المكان الذي يبدأ فيه كل السحر.
```csharp
// تحميل ملف Excel النموذجي
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
هنا، استبدل `"Your Document Directory"` مع المسار الفعلي لملف Excel. يقرأ هذا السطر ملف Excel في الذاكرة لتتمكن من تعديله.
## الخطوة 3: تحديد خيارات حفظ HTML
الآن، سنقوم بإنشاء مثيل لـ `HtmlSaveOptions`، والذي يسمح لك بتكوين كيفية تحويل ملف Excel إلى HTML.
```csharp
// تحديد نوع HTML المتقاطع
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
في هذه الخطوة، قمنا بتعيين `HtmlCrossStringType` ل `HtmlCrossType.Default`، وهو أحد الخيارات المتاحة للتعامل مع المراجع المتبادلة في HTML الناتج.
## الخطوة 4: تغيير نوع الصليب حسب الحاجة
يمكنك تحديد أنواع مختلفة لـ `HtmlCrossStringType` بناءً على احتياجاتك. إليك الخيارات المتنوعة التي يمكنك استخدامها:
- `HtmlCrossType.Default`:نوع الصليب الافتراضي.
- `HtmlCrossType.MSExport`:يقوم بتصدير HTML بسلوك مشابه لـ MS Excel.
- `HtmlCrossType.Cross`:إنشاء مراجع متقاطعة.
- `HtmlCrossType.FitToCell`:يتناسب مع المراجع المتقاطعة لأبعاد الخلية.
يمكنك تعديل `HtmlCrossStringType` مثله:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpأوt;
// أو 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## الخطوة 5: حفظ ملف HTML الناتج
بعد ضبط خياراتك، حان وقت حفظ ملف HTML المُحوّل. استخدم `Save` الطريقة الخاصة بك `Workbook` هدف:
```csharp
// إخراج HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
هنا، نقوم بتسمية ملف الإخراج بناءً على `HtmlCrossStringType` لقد قمنا بالإعداد. بهذه الطريقة، يمكنك بسهولة تحديد نوع الصليب المستخدم في التحويل.
## الخطوة 6: تأكيد التنفيذ الناجح
وأخيرًا، يُنصح دائمًا بالتأكد من نجاح العملية. يمكنك طباعة رسالة إلى وحدة التحكم:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
سيُعلمك هذا أن العملية قد اكتملت دون أي أخطاء.
## خاتمة
ها قد انتهيت! لقد نجحت في تحديد نوع HTML المتقاطع لتصدير ملف Excel الخاص بك في .NET باستخدام Aspose.Cells. تُعد هذه الوظيفة مفيدة بشكل خاص عند الحاجة إلى الحفاظ على تنسيق أو مراجع محددة في مُخرجات HTML، مما يضمن أن تُلبي مستنداتك المُحوّلة متطلباتك.
## الأسئلة الشائعة
### ما هو HtmlCrossType في Aspose.Cells؟  
يُعرّف HtmlCrossType كيفية التعامل مع المراجع التبادلية في ملف Excel أثناء تحويل HTML. يمكنك اختيار خيارات مثل Default وMSExport وCross وFitToCell.
### هل يمكنني استخدام Aspose.Cells مجانًا؟  
يقدم Aspose.Cells نسخة تجريبية مجانية. يمكنك تنزيلها من موقعهم. [موقع إلكتروني](https://releases.aspose.com/).
### كيف أقوم بتثبيت Aspose.Cells في مشروع .NET الخاص بي؟  
يمكنك تثبيت Aspose.Cells عبر NuGet Package Manager في Visual Studio عن طريق تشغيل الأمر: `Install-Package Aspose.Cells`.
### أين يمكنني العثور على الوثائق الخاصة بـ Aspose.Cells؟  
يمكنك العثور على وثائق شاملة على Aspose.Cells [هنا](https://reference.aspose.com/cells/net/).
### ماذا يجب أن أفعل إذا واجهت خطأ أثناء حفظ ملف HTML؟  
تأكد من صحة مسارات المجلدات وامتلاكك أذونات الكتابة لمجلد الإخراج. إذا استمرت المشكلة، فراجع منتدى دعم Aspose للحصول على المساعدة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}