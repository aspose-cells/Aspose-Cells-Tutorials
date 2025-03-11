---
title: تصدير خصائص المصنف وورقة العمل في المستند بتنسيق HTML
linktitle: تصدير خصائص المصنف وورقة العمل في المستند بتنسيق HTML
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تصدير خصائص مستندات Excel ودفاتر العمل وأوراق العمل إلى HTML باستخدام Aspose.Cells for .NET. يتضمن دليلًا سهلًا خطوة بخطوة.
weight: 11
url: /ar/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير خصائص المصنف وورقة العمل في المستند بتنسيق HTML

## مقدمة

عندما يتعلق الأمر بالتعامل مع جداول البيانات، غالبًا ما نجد أنفسنا في حاجة إلى تحويل ملفات Excel إلى تنسيقات مختلفة للمشاركة أو الحفظ أو العرض. إحدى المهام الشائعة هي تصدير خصائص المصنف وورقة العمل إلى تنسيق HTML. في هذه المقالة، سنوضح لك كيفية إنجاز ذلك باستخدام Aspose.Cells لـ .NET. لا تقلق إذا كنت جديدًا على الترميز أو مكتبة Aspose؛ فسنقوم بتقسيمها خطوة بخطوة لتسهيل اتباعها!

## المتطلبات الأساسية

قبل أن نتعمق في الكود، دعنا نتأكد من أن لديك كل ما تحتاجه للبدء:

1. .NET Framework: تأكد من إعداد بيئة التطوير لديك باستخدام .NET Framework. Aspose.Cells متوافق مع إصدارات .NET Framework حتى 4.8.
   
2.  Aspose.Cells لـ .NET: ستحتاج إلى تثبيت Aspose.Cells. يمكنك تنزيل المكتبة من[صفحة التنزيلات](https://releases.aspose.com/cells/net/). 

3. IDE: بيئة التطوير المتكاملة (IDE) المناسبة مثل Visual Studio سوف تعمل على تبسيط تجربة الترميز الخاصة بك.

4.  ملف Excel النموذجي: لأغراض الاختبار، تأكد من أن لديك ملف Excel باسم`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` في دليل العمل الخاص بك.

## استيراد الحزم

الآن بعد أن قمنا بتغطية المتطلبات الأساسية، فلنبدأ باستيراد الحزم اللازمة في مشروع C# الخاص بنا. إليك كيفية القيام بذلك:

### إنشاء مشروع جديد

- افتح بيئة التطوير المتكاملة الخاصة بك وقم بإنشاء مشروع C# جديد. يمكنك اختيار تطبيق وحدة تحكم، وهو مثالي لتشغيل هذا النوع من المهام.

### أضف حزمة Aspose.Cells NuGet

لإضافة حزمة Aspose.Cells، اتبع الخطوات التالية:

- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد "إدارة حزم NuGet".
- في مدير الحزم NuGet، ابحث عن "Aspose.Cells" وقم بتثبيته.
- ستوفر هذه الحزمة الفئات والطرق اللازمة للعمل مع ملفات Excel.

### استيراد المساحات الاسمية

في الجزء العلوي من ملف البرنامج الرئيسي، تأكد من تضمين مساحات الأسماء التالية:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

 هذا سوف يعطينا القدرة على الوصول إلى`Workbook` و`HtmlSaveOptions` الفئات التي سنستخدمها في مثالنا.

الآن بعد أن قمت بإعداد كل شيء، دعنا نقوم بتقسيم العملية إلى خطوات بسيطة.

## الخطوة 1: إعداد أدلة الملفات الخاصة بك

أولاً، نحتاج إلى تحديد مكان وضع ملفات الإدخال والإخراج. في الكود الخاص بك، قم بتهيئة الدلائل على النحو التالي:

```csharp
// دليل المصدر
string sourceDir = "Your Document Directory/";  // تحديث بالمسار الفعلي الخاص بك

// دليل الإخراج
string outputDir = "Your Document Directory/";  // تحديث بالمسار الفعلي الخاص بك
```

- دليل المصدر: هذا هو المكان الذي يوجد فيه ملف Excel المدخل الخاص بك (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) يتم تخزينها.
- دليل الإخراج: هذا هو المسار الذي تريد حفظ ملف HTML الناتج فيه.

## الخطوة 2: تحميل ملف Excel الخاص بك

 الآن نحتاج إلى تحميل ملف Excel باستخدام`Workbook` فصل:

```csharp
// تحميل ملف Excel النموذجي
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

-  مثال المصنف:`Workbook` يقوم المنشئ بأخذ مسار الملف إلى ملف Excel الخاص بك ويقوم بإنشاء مثيل جديد يمكنك التعامل معه.

## الخطوة 3: إعداد خيارات حفظ HTML

بعد ذلك، نحدد كيفية رغبتنا في حفظ بيانات Excel إلى HTML:

```csharp
// تحديد خيارات حفظ HTML
HtmlSaveOptions options = new HtmlSaveOptions();

// منع تصدير خصائص المستندات والمصنفات وورقة العمل
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: تساعد هذه الفئة في إدارة كيفية تحويل ملف Excel إلى HTML.
-  لقد وضعنا عدة خيارات لـ`false`لأننا لا نريد تضمين خصائص المصنف وورقة العمل في مخرجات HTML الخاصة بنا.

## الخطوة 4: تصدير كل شيء إلى HTML

نحن الآن جاهزون لحفظ المصنف الخاص بنا بتنسيق HTML:

```csharp
// تصدير ملف Excel إلى HTML باستخدام خيارات حفظ HTML
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

-  ال`Save` تتطلب الطريقة معلمتين: مسار الملف لملف HTML الناتج والخيارات التي قمنا بإعدادها. سيؤدي تشغيل هذه الطريقة إلى إنشاء ملف HTML الخاص بك في دليل الإخراج المحدد.

## الخطوة 5: ملاحظات وحدة التحكم

أخيرًا، دعنا نقدم بعض الملاحظات في وحدة التحكم لنعرف أن العملية اكتملت بنجاح:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## خاتمة

وهكذا، تكون قد نجحت في تصدير خصائص المصنف وورقة العمل إلى HTML باستخدام Aspose.Cells لـ .NET! لقد اتبعت عملية واضحة، من إعداد البيئة الخاصة بك إلى تصدير بيانات Excel الخاصة بك. تكمن روعة استخدام المكتبات مثل Aspose.Cells في أنها تبسط المهام المعقدة، مما يجعل الحياة أسهل للمطورين. الآن، يمكنك مشاركة جداول البيانات الخاصة بك على نطاق أوسع باستخدام HTML، تمامًا مثل السماح للعالم بإلقاء نظرة على مصنفاتك دون منحهم الكتاب بالكامل.

## الأسئلة الشائعة

### كيف أقوم بتثبيت Aspose.Cells لـ .NET؟  
بإمكانك تثبيت مكتبة Aspose.Cells عبر NuGet في مشروع Visual Studio الخاص بك من خلال NuGet Package Manager.

### هل يمكنني تخصيص مخرجات HTML؟  
 نعم، يوفر Aspose.Cells خيارات متنوعة في`HtmlSaveOptions` لتخصيص كيفية تحويل ملف Excel إلى HTML.

### هل هناك طريقة لتضمين خصائص المستند في تصدير HTML؟  
 يمكنك ضبط`ExportDocumentProperties`, `ExportWorkbookProperties` ، و`ExportWorksheetProperties` ل`true` في`HtmlSaveOptions` إذا كنت ترغب في تضمينها.

### ما هي التنسيقات التي يمكنني تصدير ملف Excel إليها بخلاف HTML؟  
يدعم Aspose.Cells تنسيقات مختلفة بما في ذلك PDF وCSV وXML وغيرها.

### هل هناك نسخة تجريبية متاحة؟  
 نعم، يمكنك الحصول على نسخة تجريبية مجانية من Aspose.Cells من[موقع إلكتروني](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
