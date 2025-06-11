---
"date": "2025-04-05"
"description": "تعلّم كيفية إنشاء مخططات دائرية ديناميكية بخطوط إرشادية باستخدام Aspose.Cells لـ .NET. اتبع هذا الدليل لتحسين مهاراتك في تصور البيانات."
"title": "إنشاء مخططات دائرية بخطوط إرشادية في Aspose.Cells .NET - دليل شامل"
"url": "/ar/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إنشاء مخططات دائرية بخطوط إرشادية باستخدام Aspose.Cells .NET

## مقدمة
حسّن تصور بياناتك بإنشاء مخططات دائرية أكثر إفادة باستخدام Aspose.Cells لـ .NET. يوضح لك هذا الدليل التفصيلي كيفية إضافة خطوط إرشادية إلى أجزاء المخطط الدائري، مما يُسهّل عليك تحديد فئات البيانات المقابلة بسرعة. باتباع هذا البرنامج التعليمي، ستكون تصوراتك جذابة بصريًا وفعّالة للغاية.

**ما سوف تتعلمه:**
- إعداد Aspose.Cells لـ .NET في بيئتك
- إنشاء مخططات دائرية مخصصة لخطوط القيادة باستخدام C#
- حفظ الرسم البياني كصورة أو داخل مصنف Excel

تأكد من أن كل شيء جاهز لديك لتتمكن من المتابعة بفعالية.

## المتطلبات الأساسية
قبل البدء، تأكد من استيفاء المتطلبات الأساسية التالية:

- **المكتبات والإصدارات**ثبّت Aspose.Cells لـ .NET. تأكد من تثبيت أحدث إصدار من مشروعك.
- **إعداد البيئة**:يفترض هذا الدليل وجود بيئة .NET متوافقة مع Aspose.Cells.
- **متطلبات المعرفة**:إن المعرفة الأساسية ببرمجة C# وعمليات Excel مفيدة.

## إعداد Aspose.Cells لـ .NET
للبدء، قم بتثبيت Aspose.Cells في مشروعك عبر:

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**مدير الحزم**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

احصل على ترخيص للوظائف الكاملة من خلال الاختيار من الخيارات التالية:
- **نسخة تجريبية مجانية**:ابدأ تجربتك المجانية على [صفحة تنزيل Aspose](https://releases.aspose.com/cells/net/).
- **رخصة مؤقتة**:الحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).
- **شراء**:للحصول على الميزات الكاملة، قم بشراء ترخيص [هنا](https://purchase.aspose.com/buy).

قم بتهيئة Aspose.Cells في مشروعك عن طريق إنشاء مثيل لـ `Workbook` فصل.

## دليل التنفيذ

### إنشاء المصنف وورقة العمل
1. **تهيئة المصنف**
   إنشاء مصنف جديد بتنسيق XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **الوصول إلى ورقة العمل الأولى**
   استخدم ورقة العمل الأولى لإدخال البيانات:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **إضافة البيانات إلى مخطط دائري**
   املأ ورقة العمل الخاصة بك بالفئات والقيم:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // أضف أسماء الفئات المتبقية...
   worksheet.Cells["B1"].PutValue(10.4);
   // أضف القيم المقابلة...
   ```

### إضافة مخطط دائري إلى ورقة العمل
1. **إنشاء مخطط دائري**
   إنشاء مخطط دائري وإضافته إلى مجموعة المخططات الموجودة في ورقة العمل الخاصة بك:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **تكوين بيانات السلسلة والفئات**
   ربط البيانات الخاصة بالسلسلة والفئات:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **تخصيص تسميات البيانات**
   قم بإيقاف تشغيل عرض الأسطورة، وتعيين تسميات البيانات لإظهار أسماء الفئات والنسب المئوية:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### تنفيذ خطوط القائد
1. **تشغيل خطوط القائد**
   تمكين خطوط القائد للحصول على اتصالات بصرية أكثر وضوحًا:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **ضبط موضع تسميات البيانات**
   ضمان الرؤية عن طريق تعديل مواضع الملصقات:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### حفظ الرسم البياني والمصنف
1. **حفظ كصورة**
   تحويل الرسم البياني إلى ملف صورة:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **حفظ المصنف**
   احفظ المصنف لعرض الرسم البياني داخل Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## التطبيقات العملية
- **التقارير المالية**:تمثل تخصيصات الميزانية بشكل واضح.
- **تحليلات التسويق**:تصور بيانات حصة السوق بشكل فعال في العروض التقديمية أو التقارير.
- **تحليل المبيعات**:عرض توزيع المبيعات بين المناطق/المنتجات المختلفة بسهولة.

تتضمن إمكانيات التكامل تصدير هذه التصورات إلى تطبيقات الويب أو تضمينها داخل أدوات إعداد التقارير الآلية.

## اعتبارات الأداء
عند استخدام Aspose.Cells، ضع ما يلي في الاعتبار للحصول على الأداء الأمثل:
- تقليل مجموعات البيانات الكبيرة المحملة في الذاكرة مرة واحدة.
- استخدم حلقات فعالة وتجنب الحسابات غير الضرورية داخل الحلقات.
- قم بتنظيف الموارد مثل كائنات مصنف العمل بشكل منتظم لمنع تسرب الذاكرة.

## خاتمة
لقد تعلمتَ كيفية إنشاء مخططات دائرية بخطوط إرشادية باستخدام Aspose.Cells لـ .NET. تُحسّن هذه الوظيفة وضوح عروض البيانات المرئية، مما يجعلها أكثر سهولة في الوصول إليها وأكثر تأثيرًا. 

**الخطوات التالية:**
استكشف المزيد من التخصيصات في مظهر المخطط أو جرب أنواع المخططات الأخرى المتوفرة في Aspose.Cells.

## قسم الأسئلة الشائعة
1. **ما هو الخط الرئيسي في مخطط دائري؟**
   تربط الخطوط الرئيسية تسميات البيانات بأجزائها الخاصة، مما يحسن قابلية القراءة.

2. **هل يمكنني استخدام Aspose.Cells مجانًا؟**
   نعم، يمكنك البدء بإصدار تجريبي مجاني، ولكن الميزات الكاملة تتطلب ترخيصًا.

3. **هل من الممكن تصدير المخططات كصور؟**
   بالتأكيد! استخدم `ImageOrPrintOptions` لحفظ الرسم البياني الخاص بك بتنسيقات الصور مثل PNG أو JPEG.

4. **كيف يمكنني تعديل مواضع علامات البيانات يدويًا؟**
   تعديل إحداثيات X وY لملصقات البيانات ضمن حلقة نقاط السلسلة.

5. **هل يمكن لـ Aspose.Cells التكامل مع أنظمة أخرى؟**
   نعم، يمكن استخدامه مع قواعد البيانات وخدمات الويب والمزيد للحصول على حلول إعداد التقارير الآلية.

## موارد
- [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/)
- [تنزيل Aspose.Cells](https://releases.aspose.com/cells/net/)
- [شراء الترخيص](https://purchase.aspose.com/buy)
- [نسخة تجريبية مجانية](https://releases.aspose.com/cells/net/)
- [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/)
- [منتدى الدعم](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}