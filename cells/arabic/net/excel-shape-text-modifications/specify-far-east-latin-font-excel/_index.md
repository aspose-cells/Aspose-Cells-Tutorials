---
title: تحديد الخط الشرقي واللاتيني في برنامج Excel
linktitle: تحديد الخط الشرقي واللاتيني في برنامج Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تحديد خطوط الشرق الأقصى واللاتينية في Excel باستخدام Aspose.Cells لـ .NET في هذا البرنامج التعليمي الشامل وسهل المتابعة.
weight: 17
url: /ar/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد الخط الشرقي واللاتيني في برنامج Excel

## مقدمة
هل تبحث عن تحسين تقارير Excel أو مستنداتك باستخدام متطلبات خطوط محددة؟ سواء كنت تتعامل مع لغات متعددة أو تسعى ببساطة إلى الحصول على مظهر جمالي فريد في جداول البيانات الخاصة بك، فإن فهم كيفية تحديد الخطوط الشرقية واللاتينية في Excel يعد مهارة بالغة الأهمية. لحسن الحظ، لدينا الحل! في هذا البرنامج التعليمي، نستكشف كيفية استخدام Aspose.Cells لـ .NET لتنفيذ هذه الميزة بسلاسة. دعنا نتعمق!
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة، هناك بعض الأشياء التي ستحتاج إلى إعدادها قبل البدء في استخدام Aspose.Cells:
### .NET Framework أو .NET Core
تأكد من تثبيت .NET Framework أو .NET Core على جهازك. تعمل هذه المكتبة بشكل جيد مع كليهما.
### تثبيت Aspose.Cells
 سوف تحتاج إلى تنزيل مكتبة Aspose.Cells. يمكنك[قم بتحميله من هنا](https://releases.aspose.com/cells/net/) إذا لم تكن على دراية بتثبيت حزم NuGet، فاتبع[هذا الدليل](https://www.nuget.org/).
### بيئة التطوير المتكاملة (IDE)
إن وجود بيئة تطوير متكاملة مثل Visual Studio أو JetBrains Rider يمكن أن يسهل عملية الترميز واستكشاف الأخطاء وإصلاحها وتشغيل مشروعك.
### المعرفة الأساسية بلغة C#
ستكون المعرفة ببرمجة C# مفيدة جدًا لمتابعة هذا البرنامج التعليمي.
## استيراد الحزم
قبل أن نتمكن من العمل مع Aspose.Cells، نحتاج إلى استيراد الحزم اللازمة إلى مشروعنا. إليك كيفية القيام بذلك:
### إنشاء مشروع جديد
1. افتح IDE الخاص بك وقم بإنشاء مشروع تطبيق وحدة تحكم جديد.
2.  أطلق على مشروعك اسمًا وصفيًا، مثل`FontSpecifyingApp`.
### إضافة حزمة Aspose.Cells NuGet
1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2.  يختار`Manage NuGet Packages...`.
3.  بحث عن`Aspose.Cells` وتثبيته.
بحلول نهاية هذه الخطوات، يجب أن يكون كل شيء جاهزًا لبدء الترميز!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
بعد الانتهاء من الإعداد، حان الوقت للبدء في كتابة التعليمات البرمجية. على وجه التحديد، سنقوم بإنشاء مصنف Excel جديد وتحديد الخطوط الخاصة بالشرق الأقصى واللاتينية لمربعات النص. وإليك كيفية القيام بذلك خطوة بخطوة:
## الخطوة 1: إعداد دليل الإخراج
نبدأ بتحديد المكان الذي نريد حفظ ملف Excel فيه. وهذا أمر بالغ الأهمية لأننا نريد التأكد من تخزين ملف الإخراج في مكان يمكن الوصول إليه بسهولة.
```csharp
// دليل الإخراج
string outputDir = "Your Document Directory";
```
## الخطوة 2: إنشاء مصنف فارغ
الآن بعد أن قمنا بإعداد الدليل، فلنبدأ في إنشاء مصنف جديد حيث سنضيف المحتوى. وهذا يشبه البدء بلوحة قماشية جديدة قبل الرسم.
```csharp
// إنشاء مصنف فارغ.
Workbook wb = new Workbook();
```
## الخطوة 3: الوصول إلى ورقة العمل الأولى
بعد ذلك، نريد العمل على ورقة عمل من كتاب العمل الخاص بنا. فكر في ورقة العمل باعتبارها صفحة في كتابك حيث تحدث كل السحر.
```csharp
// الوصول إلى ورقة العمل الأولى.
Worksheet ws = wb.Worksheets[0];
```
## الخطوة 4: إضافة مربع نص
الآن، سنضيف مربع نص إلى ورقة العمل الخاصة بنا. هذا هو المكان الذي سنكتب فيه النص. تخيل أن هذا الأمر يشبه إنشاء مربع نص داخل شريحة من العرض التقديمي.
```csharp
// إضافة مربع نص داخل ورقة العمل.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## الخطوة 5: تعيين نص مربع النص
دعنا نكتب بعض النصوص. في هذا المثال، سنقوم بإدخال الأحرف اليابانية لإظهار خط الشرق الأقصى. الأمر بسيط مثل الكتابة في مربع نص على جهاز الكمبيوتر الخاص بك!
```csharp
// تعيين نص مربع النص.
tb.Text = "こんにちは世界"; //وهذا يعني "مرحبا بالعالم" باللغة اليابانية.
```
## الخطوة 6: تحديد الخطوط
الآن يأتي الجزء المثير! سنقوم بتعيين الخط اللاتيني والخط الشرقي الأقصى للنص. وهذا يشبه اختيار الخط المثالي لدعوة زفاف فاخرة!
```csharp
// حدد اسم الخط الشرقي واللاتيني.
tb.TextOptions.LatinName = "Comic Sans MS"; // هذا هو الخط اللاتيني الذي اخترناه.
tb.TextOptions.FarEastName = "KaiTi"; // هذا هو الخط الذي نرغبه في الشرق الأقصى.
```
## الخطوة 7: احفظ ملف Excel الناتج
أخيرًا، لنبدأ في حفظ مصنف العمل الخاص بنا! هذه الخطوة تنهي مهمتنا وتضمن حفظ كل العمل الشاق الذي قمنا به بشكل صحيح. 
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
والآن، لقد نجحت في تحديد الخطوط الخاصة بالشرق الأقصى واللاتينية في مصنف Excel باستخدام Aspose.Cells for .NET. لا تمنح هذه المهارة مستنداتك لمسة احترافية فحسب، بل إنها تعمل أيضًا على إثراء تجربة القراءة للمستخدمين عبر لغات مختلفة.
لا تتردد في تجربة خطوط وأنماط مختلفة للعثور على مزيج يناسب احتياجاتك المحددة. استمتع بالبرمجة!
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة .NET لإنشاء وإدارة جداول بيانات Excel دون الحاجة إلى تثبيت Microsoft Excel على جهازك. 
### هل يمكنني استخدام Aspose.Cells لتطبيقات الويب؟
نعم! يمكن استخدام Aspose.Cells لكل من تطبيقات سطح المكتب وتطبيقات الويب المبنية باستخدام .NET.
### هل هناك نسخة مجانية من Aspose.Cells؟
 نعم، تقدم Aspose نسخة تجريبية مجانية. يمكنك[تحميله هنا](https://releases.aspose.com/).
### كيف أحصل على الدعم لـ Aspose.Cells؟
 يمكنك طلب الدعم والعثور على موارد قيمة على[منتديات اسبوس](https://forum.aspose.com/c/cells/9).
### أين يمكنني شراء Aspose.Cells؟
 يمكنك شراء Aspose.Cells مباشرة من[موقع اسبوس](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
