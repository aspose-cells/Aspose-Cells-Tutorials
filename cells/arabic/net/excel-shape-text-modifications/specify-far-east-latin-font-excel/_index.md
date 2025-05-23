---
"description": "تعرف على كيفية تحديد الخطوط الخاصة بالشرق الأقصى واللاتينية في Excel باستخدام Aspose.Cells لـ .NET في هذا البرنامج التعليمي الشامل وسهل المتابعة."
"linktitle": "تحديد الخط الشرقي واللاتيني في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تحديد الخط الشرقي واللاتيني في Excel"
"url": "/ar/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحديد الخط الشرقي واللاتيني في Excel

## مقدمة
هل ترغب في تحسين تقارير أو مستندات Excel الخاصة بك باستخدام خطوط محددة؟ سواء كنت تتعامل مع لغات متعددة أو تسعى ببساطة إلى تصميم جداول بياناتك بشكل فريد، فإن فهم كيفية تحديد خطوط الشرق الأقصى واللاتينية في Excel مهارة أساسية. لحسن حظك، لدينا الحل! في هذا البرنامج التعليمي، سنستكشف كيفية استخدام Aspose.Cells لـ .NET لتطبيق هذه الميزة بسلاسة. هيا بنا!
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة، هناك بعض الأشياء التي ستحتاج إلى إعدادها قبل البدء في استخدام Aspose.Cells:
### .NET Framework أو .NET Core
تأكد من تثبيت .NET Framework أو .NET Core على جهازك. هذه المكتبة تعمل بكفاءة مع كليهما.
### تثبيت Aspose.Cells
ستحتاج إلى تنزيل مكتبة Aspose.Cells. يمكنك [قم بتحميله من هنا](https://releases.aspose.com/cells/net/)إذا لم تكن على دراية بتثبيت حزم NuGet، فاتبع [هذا الدليل](https://www.nuget.org/).
### بيئة التطوير المتكاملة (IDE)
إن وجود بيئة تطوير متكاملة مثل Visual Studio أو JetBrains Rider يمكن أن يبسط عملية الترميز واستكشاف الأخطاء وإصلاحها وتشغيل مشروعك.
### المعرفة الأساسية بلغة C#
ستكون المعرفة ببرمجة C# مفيدة جدًا لمتابعة هذا البرنامج التعليمي.
## استيراد الحزم
قبل أن نتمكن من العمل مع Aspose.Cells، علينا استيراد الحزم اللازمة إلى مشروعنا. إليك كيفية القيام بذلك:
### إنشاء مشروع جديد
1. افتح IDE الخاص بك وقم بإنشاء مشروع تطبيق وحدة تحكم جديد.
2. قم بتسمية مشروعك بشيء وصفي، مثل `FontSpecifyingApp`.
### إضافة حزمة Aspose.Cells NuGet
1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2. يختار `Manage NuGet Packages...`.
3. بحث عن `Aspose.Cells` وتثبيته.
بحلول نهاية هذه الخطوات، يجب أن يكون كل شيء جاهزًا لبدء الترميز!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
بعد الانتهاء من الإعداد، حان وقت البدء بالبرمجة. على وجه التحديد، سننشئ مصنف Excel جديدًا ونحدد خطوط الشرق الأقصى واللاتينية لمربعات النص. إليك كيفية القيام بذلك خطوة بخطوة:
## الخطوة 1: إعداد دليل الإخراج
نبدأ بتحديد مكان حفظ ملف إكسل. هذا أمر بالغ الأهمية لضمان تخزين ملف الإخراج في مكان يسهل الوصول إليه.
```csharp
// دليل الإخراج
string outputDir = "Your Document Directory";
```
## الخطوة 2: إنشاء مصنف فارغ
بعد إعداد الدليل، لننشئ مصنفًا جديدًا لإضافة المحتوى. هذا يشبه البدء بلوحة قماشية جديدة قبل الرسم.
```csharp
// إنشاء مصنف فارغ.
Workbook wb = new Workbook();
```
## الخطوة 3: الوصول إلى ورقة العمل الأولى
بعد ذلك، سنعمل على ورقة عمل من مصنفنا. تخيّل ورقة العمل كصفحة في كتابك حيث تحدث كل السحر.
```csharp
// الوصول إلى ورقة العمل الأولى.
Worksheet ws = wb.Worksheets[0];
```
## الخطوة 4: إضافة مربع نص
الآن، سنضيف مربع نص إلى ورقة العمل. هنا سنكتب النص. تخيل أن هذا يُنشئ مربع نص ضمن شريحة عرض تقديمي.
```csharp
// أضف مربع نص داخل ورقة العمل.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## الخطوة 5: تعيين نص مربع النص
لنكتب نصًا. في هذا المثال، سنُدخل أحرفًا يابانية لتوضيح خط الشرق الأقصى. الأمر بسيط كالكتابة في مربع نص على جهاز الكمبيوتر!
```csharp
// تعيين نص مربع النص.
tb.Text = "こんにちは世界"; // وهذا يعني "مرحبا بالعالم" باللغة اليابانية.
```
## الخطوة 6: تحديد الخطوط
والآن يأتي الجزء المثير! سنضبط الخطين اللاتيني والشرقي للنص. هذا أشبه باختيار الخط المثالي لدعوة زفاف فاخرة!
```csharp
// حدد اسم الخط باللغة الشرقية واللاتينية.
tb.TextOptions.LatinName = "Comic Sans MS"; // هذا هو الخط اللاتيني الذي اخترناه.
tb.TextOptions.FarEastName = "KaiTi"; // هذا هو الخط الذي نرغب به في الشرق الأقصى.
```
## الخطوة 7: حفظ ملف Excel الناتج
أخيرًا، لنحفظ مصنفنا! بهذه الخطوة، نختتم مهمتنا ونضمن حفظ كل العمل الشاق الذي أنجزناه بشكل صحيح. 
```csharp
// احفظ ملف Excel الناتج.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## الخطوة 8: رسالة التأكيد
لإعلامنا بأن كل شيء تم تنفيذه بنجاح، سنقوم بطباعة رسالة تأكيد على وحدة التحكم:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## خاتمة
وها أنت ذا! لقد نجحت في تحديد خطوط الشرق الأقصى واللاتينية في مصنف Excel باستخدام Aspose.Cells لـ .NET. هذه المهارة لا تضفي على مستنداتك لمسة احترافية فحسب، بل تُثري أيضًا تجربة القراءة للمستخدمين من مختلف اللغات.
لا تتردد في تجربة خطوط وأنماط مختلفة للعثور على ما يناسب احتياجاتك. برمجة ممتعة!
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة .NET لإنشاء وإدارة جداول بيانات Excel دون الحاجة إلى تثبيت Microsoft Excel على جهازك. 
### هل يمكنني استخدام Aspose.Cells لتطبيقات الويب؟
نعم! يُمكن استخدام Aspose.Cells لتطبيقات سطح المكتب وتطبيقات الويب المُصممة باستخدام .NET.
### هل هناك نسخة مجانية من Aspose.Cells؟
نعم، يقدم Aspose نسخة تجريبية مجانية. يمكنك [قم بتحميله هنا](https://releases.aspose.com/).
### كيف أحصل على الدعم لـ Aspose.Cells؟
يمكنك طلب الدعم والعثور على موارد قيمة على [منتديات Aspose](https://forum.aspose.com/c/cells/9).
### أين يمكنني شراء Aspose.Cells؟
يمكنك شراء Aspose.Cells مباشرة من [موقع Aspose](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}