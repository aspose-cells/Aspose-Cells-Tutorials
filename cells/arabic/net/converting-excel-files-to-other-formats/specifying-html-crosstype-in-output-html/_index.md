---
title: تحديد HTML CrossType في إخراج HTML برمجيًا في .NET
linktitle: تحديد HTML CrossType في إخراج HTML برمجيًا في .NET
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تحديد HTML CrossType في Aspose.Cells لـ .NET. اتبع البرنامج التعليمي خطوة بخطوة لتحويل ملفات Excel إلى HTML بدقة.
weight: 17
url: /ar/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد HTML CrossType في إخراج HTML برمجيًا في .NET

## مقدمة
عندما يتعلق الأمر بتحويل ملفات Excel إلى HTML في تطبيقات .NET، فقد تجد نفسك في حاجة إلى تحديد كيفية التعامل مع المراجع المتقاطعة في المخرجات. توفر فئة HtmlSaveOptions في Aspose.Cells لـ .NET إعدادات مختلفة للتحكم في عملية التحويل، وأحد هذه الخيارات هو HtmlCrossType. في هذا البرنامج التعليمي، سنشرح كيفية تحديد النوع المتقاطع لـ HTML برمجيًا عند تصدير ملفات Excel إلى تنسيق HTML. 
## المتطلبات الأساسية
قبل الغوص في الكود، تأكد من أن لديك ما يلي:
-  Aspose.Cells لـ .NET: تأكد من تثبيت مكتبة Aspose.Cells في مشروعك. يمكنك تنزيلها من[موقع اسبوس](https://releases.aspose.com/cells/net/).
- Visual Studio: تثبيت عملي لبرنامج Visual Studio أو أي بيئة تطوير .NET أخرى.
- المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الأمثلة بشكل أفضل.
-  ملف Excel نموذجي: احرص على أن يكون لديك ملف Excel نموذجي جاهز للعمل به. في هذا المثال، سنستخدم`sampleHtmlCrossStringType.xlsx`.
## استيراد الحزم
للبدء، ستحتاج إلى استيراد مساحات الأسماء Aspose.Cells اللازمة. إليك كيفية القيام بذلك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
دعنا نوضح ذلك خطوة بخطوة، حتى يسهل عليك متابعة هذه الوظيفة وتنفيذها في مشاريعك الخاصة.
## الخطوة 1: قم بتحديد أدلة المصدر والإخراج
أولاً، يتعين عليك تحديد الدلائل لملف Excel المصدر والمكان الذي تريد حفظ ملف HTML الناتج فيه.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
## الخطوة 2: تحميل ملف Excel النموذجي
 بعد ذلك، قم بتحميل ملف Excel الخاص بك إلى`Workbook` هذا هو المكان الذي يبدأ فيه كل السحر.
```csharp
// تحميل ملف Excel النموذجي
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 هنا، استبدل`"Your Document Directory"` مع المسار الفعلي الذي يوجد به ملف Excel الخاص بك. يقرأ هذا السطر ملف Excel في الذاكرة حتى تتمكن من التعامل معه.
## الخطوة 3: تحديد خيارات حفظ HTML
 الآن، سنقوم بإنشاء مثيل لـ`HtmlSaveOptions`، الذي يسمح لك بتكوين كيفية تحويل ملف Excel إلى HTML.
```csharp
// تحديد نوع HTML Cross
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 في هذه الخطوة، قمنا بتعيين`HtmlCrossStringType` ل`HtmlCrossType.Default`، وهو أحد الخيارات المتاحة للتعامل مع المراجع المتبادلة في HTML الناتج.
## الخطوة 4: قم بتغيير نوع الصليب حسب الحاجة
 يمكنك تحديد أنواع مختلفة لـ`HtmlCrossStringType` بناءً على متطلباتك. فيما يلي الخيارات المختلفة التي يمكنك استخدامها:
- `HtmlCrossType.Default`:نوع الصليب الافتراضي.
- `HtmlCrossType.MSExport`:يقوم بتصدير HTML بسلوك مشابه لسلوك MS Excel.
- `HtmlCrossType.Cross`:إنشاء مراجع متقاطعة.
- `HtmlCrossType.FitToCell`:يتناسب مع المراجع المتقاطعة لأبعاد الخلية.
 يمكنك تعديل`HtmlCrossStringType` مثله:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// أو
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// أو
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## الخطوة 5: احفظ ملف HTML الناتج
 بمجرد تكوين خياراتك، حان الوقت لحفظ ملف HTML المُحوَّل. استخدم`Save` الطريقة الخاصة بك`Workbook` هدف:
```csharp
// إخراج HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 هنا، نقوم بتسمية ملف الإخراج بناءً على`HtmlCrossStringType` لقد قمنا بالإعداد. بهذه الطريقة، يمكنك بسهولة تحديد نوع الصليب الذي تم استخدامه في التحويل.
## الخطوة 6: تأكيد التنفيذ الناجح
أخيرًا، من الأفضل دائمًا التأكد من نجاح العملية. يمكنك طباعة رسالة على وحدة التحكم:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
سيُعلمك هذا أن العملية قد اكتملت دون أي أخطاء.
## خاتمة
والآن، لقد نجحت في تحديد النوع المتقاطع لملفات HTML المصدرة في Excel في .NET باستخدام Aspose.Cells. وهذه الوظيفة مفيدة بشكل خاص عندما تحتاج إلى الحفاظ على تنسيق أو مراجع معينة في مخرجات HTML، مما يضمن أن المستندات المحولة تلبي متطلباتك.
## الأسئلة الشائعة
### ما هو HtmlCrossType في Aspose.Cells؟  
يحدد HtmlCrossType كيفية التعامل مع المراجع المتقاطعة في ملف Excel أثناء تحويل HTML. يمكنك اختيار خيارات مثل Default وMSExport وCross وFitToCell.
### هل يمكنني استخدام Aspose.Cells مجانًا؟  
 يقدم Aspose.Cells إصدارًا تجريبيًا مجانيًا. يمكنك تنزيله من موقعه[موقع إلكتروني](https://releases.aspose.com/).
### كيف أقوم بتثبيت Aspose.Cells في مشروع .NET الخاص بي؟  
 يمكنك تثبيت Aspose.Cells عبر NuGet Package Manager في Visual Studio عن طريق تشغيل الأمر:`Install-Package Aspose.Cells`.
### أين يمكنني العثور على الوثائق الخاصة بـ Aspose.Cells؟  
 يمكنك العثور على وثائق شاملة على Aspose.Cells[هنا](https://reference.aspose.com/cells/net/).
### ماذا يجب أن أفعل إذا واجهت خطأ أثناء حفظ ملف HTML؟  
تأكد من صحة مسارات الدليل وأن لديك أذونات الكتابة للدليل الناتج. إذا استمرت المشكلة، فتحقق من منتدى دعم Aspose للحصول على المساعدة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
