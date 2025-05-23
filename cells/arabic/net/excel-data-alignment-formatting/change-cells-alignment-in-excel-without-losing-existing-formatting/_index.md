---
"description": "تعرّف على كيفية تغيير محاذاة خلايا Excel دون فقدان التنسيق باستخدام Aspose.Cells لـ .NET. اتبع دليلنا الشامل خطوة بخطوة للتحكم السلس."
"linktitle": "تغيير محاذاة خلايا Excel دون فقدان التنسيق"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تغيير محاذاة خلايا Excel دون فقدان التنسيق"
"url": "/ar/net/excel-data-alignment-formatting/change-cells-alignment-in-excel-without-losing-existing-formatting/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تغيير محاذاة خلايا Excel دون فقدان التنسيق

## مقدمة

قد تبدو إدارة ملفات Excel أحيانًا أشبه بخوض متاهة، خاصةً عندما يتعلق الأمر بالحفاظ على التنسيق مع إجراء تعديلات أساسية مثل تغيير محاذاة الخلايا. إذا سبق لك أن حاولت تعديل محاذاة الخلايا في Excel ووجدت أن التنسيق قد اختل، فأنت لست وحدك! في هذا البرنامج التعليمي، سنتعمق في كيفية تغيير محاذاة خلايا Excel دون فقدان أي تنسيق، باستخدام Aspose.Cells لـ .NET. هيا بنا نبدأ!

## المتطلبات الأساسية

قبل الخوض في البرمجة الفعلية، من الضروري التأكد من إعداد كل شيء بشكل صحيح. إليك ما ستحتاجه:

1. Visual Studio: تأكد من تثبيت Visual Studio (أي إصدار يدعم .NET) على جهاز الكمبيوتر الخاص بك.
2. Aspose.Cells لـ .NET: قم بتنزيل مكتبة Aspose.Cells وتثبيتها من [موقع Aspose](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: سيكون من المفيد أن يكون لديك القليل من المعرفة ببرمجة C# لأننا سنعمل في سياق C#.
4. ملف Excel نموذجي: للتوضيح، قم بإعداد ملف Excel نموذجي (على سبيل المثال، `sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx`) الذي يحتوي على بعض تنسيقات الخلايا الأولية.

## استيراد الحزم

الخطوة الأولى لاستخدام Aspose.Cells لـ .NET هي تضمين مساحات الأسماء اللازمة في مشروعك. إليك الطريقة:

### افتح مشروعك

افتح Visual Studio وقم بإنشاء مشروع C# جديد (سوف يعمل تطبيق وحدة التحكم بشكل جيد).

### إضافة مرجع إلى Aspose.Cells

- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
- اختر "إدارة حزم NuGet".
- بحث عن `Aspose.Cells` وتثبيته.

### استيراد مساحات الأسماء المطلوبة

في أعلى ملف C# الخاص بك، أضف ما يلي باستخدام التوجيهات:

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Tables;
```

سيسمح لك هذا باستخدام الفئات والطرق التي توفرها مكتبة Aspose.Cells بسلاسة.

الآن بعد أن قمنا بترتيب المتطلبات الأساسية واستيراد الحزم، دعنا نقوم بتقسيم عملية تغيير محاذاة الخلايا خطوة بخطوة.

## الخطوة 1: إعداد دليل المصدر والإخراج

للبدء، تحتاج إلى تحديد مكان تخزين ملف Excel والمكان الذي تريد حفظه فيه بعد المعالجة.

```csharp
// دليل المصدر
string sourceDir = "Your Document Directory\\"; // استبدل بالدليل الفعلي الخاص بك

// دليل الإخراج
string outputDir = "Your Document Directory\\"; // استبدل بالدليل الفعلي الخاص بك
```

يُحدد هذا الكود مسارات ملفات الإدخال والإخراج. تأكد من استبدال `"Your Document Directory\\"` مع المسار الفعلي على جهاز الكمبيوتر الخاص بك.

## الخطوة 2: تحميل ملف Excel النموذجي

بعد ذلك، ستحتاج إلى تحميل ملف Excel الخاص بك إلى التطبيق.

```csharp
// قم بتحميل ملف Excel النموذجي الذي يحتوي على خلايا مع التنسيق.
Workbook wb = new Workbook(sourceDir + "sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx");
```

يستخدم هذا السطر من التعليمات البرمجية فئة Workbook لتحميل ملف Excel الحالي الخاص بك حتى نتمكن من معالجة محتوياته.

## الخطوة 3: الوصول إلى ورقة العمل المطلوبة

بعد تحميل المصنف، انتقل إلى ورقة العمل التي تريد تعديلها. يمكن أن تحتوي ملفات Excel على عدة أوراق، لذا تأكد من اختيار الورقة الصحيحة.

```csharp
// الوصول إلى ورقة العمل الأولى.
Worksheet ws = wb.Worksheets[0];
```

هذا المثال يُمكّنك من الوصول إلى ورقة العمل الأولى. إذا كانت بياناتك موجودة في ورقة عمل مختلفة، فاضبط الفهرس وفقًا لذلك.

## الخطوة 4: إنشاء نطاق من الخلايا

حدد الخلايا التي تريد تعديلها بإنشاء نطاق. سيركز هذا التحديد على نطاق محدد، مثل "B2:D7".

```csharp
// إنشاء نطاق الخلايا.
Range rng = ws.Cells.CreateRange("B2:D7");
```

سيسمح لنا هذا النطاق بتطبيق إعدادات المحاذاة الجديدة مباشرة على تلك الخلايا.

## الخطوة 5: إنشاء كائن نمط وتخصيصه

الآن، نحتاج إلى تحديد أنماط المحاذاة التي نرغب في تطبيقها.

```csharp
// إنشاء كائن النمط.
Style st = wb.CreateStyle();

// ضبط المحاذاة الأفقية والرأسية إلى المركز.
st.HorizontalAlignment = TextAlignmentType.Center;
st.VerticalAlignment = TextAlignmentType.Center;
```

هنا، يُنشأ كائن نمط جديد، ونضبط المحاذاة الأفقية والرأسية على المركز. هذا ما يُساعد في محاذاة النص بدقة داخل الخلايا المُختارة.

## الخطوة 6: إعداد علامات الأسلوب

يلعب إعداد علامات الأسلوب دورًا مهمًا في ضمان تطبيق تغييرات الأسلوب الخاصة بك. 

```csharp
// إنشاء كائن علم النمط.
StyleFlag flag = new StyleFlag();

// ضبط محاذاة أعلام الأنماط إلى "صحيح". هذه جملة بالغة الأهمية.
flag.Alignments = true;
```

من خلال ضبط `Alignments` خاصية StyleFlag إلى `true`، فأنت تخبر Aspose.Cells بتطبيق أنماط المحاذاة بشكل صحيح.

## الخطوة 7: تطبيق النمط على نطاق الخلايا

بعد وضع الأنماط والأعلام في مكانها، حان الوقت لتطبيق هذه الأنماط على نطاق الخلايا:

```csharp
// تطبيق النمط على نطاق من الخلايا.
rng.ApplyStyle(st, flag);
```

تؤدي هذه الخطوة إلى تغيير محاذاة جميع الخلايا ضمن هذا النطاق بشكل فعال مع الحفاظ على أي تنسيق موجود.

## الخطوة 8: حفظ المصنف

وأخيرًا، قد ترغب في حفظ التغييرات في ملف جديد حتى تتمكن من الحفاظ على الملف الأصلي سليمًا.

```csharp
// احفظ المصنف بتنسيق XLSX.
wb.Save(outputDir + "outputChangeCellsAlignmentAndKeepExistingFormatting.xlsx", SaveFormat.Xlsx);
```

يحفظ هذا السطر المصنف، مع تغييرات المحاذاة، في دليل الإخراج المحدد مسبقًا.

## الخطوة 9: إعلام النجاح

بعد حفظ الملف، من الجيد تقديم تعليق يفيد بأن كل شيء يعمل كما هو متوقع!

```csharp
Console.WriteLine("ChangeCellsAlignmentAndKeepExistingFormatting executed successfully.");
```

تظهر هذه الرسالة في وحدة التحكم إذا اكتملت العملية دون مشاكل.

## خاتمة

يُعد تغيير محاذاة الخلايا في Excel مع الحفاظ على التنسيق الحالي عمليةً سلسةً مع Aspose.Cells لـ .NET. باتباع هذه الخطوات، يمكنك تبسيط معالجة Excel في تطبيقاتك وتجنب مشكلة فقدان التنسيق القيّم. سواءً كنت تُنتج تقارير أو تُدير موجزات بيانات، فإن إتقان هذه المهارة سيُحدث فرقًا كبيرًا!

## الأسئلة الشائعة

### هل يمكن لـ Aspose.Cells التعامل مع ملفات Excel كبيرة الحجم؟
بالتأكيد! مُحسّن للأداء ويُمكنه معالجة الملفات الكبيرة بكفاءة.

### هل هناك نسخة تجريبية متاحة لـ Aspose.Cells؟
نعم! يمكنك تنزيل نسخة تجريبية مجانية من الموقع [نسخة تجريبية مجانية](https://releases.aspose.com/).

### ما هي لغات البرمجة التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells بشكل أساسي .NET وJava والعديد من اللغات الأخرى من خلال المكتبات الخاصة بها.

### كيف يمكنني الحصول على الدعم لـ Aspose.Cells؟
لأي استفسارات أو مشكلات متعلقة بالدعم، قم بزيارة [منتدى الدعم](https://forum.aspose.com/c/cells/9).

### هل يمكنني تطبيق أنماط متعددة في وقت واحد؟
نعم، يمكنك إنشاء كائنات نمط متعددة وتطبيقها بشكل تسلسلي أو مشروط حسب الحاجة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}