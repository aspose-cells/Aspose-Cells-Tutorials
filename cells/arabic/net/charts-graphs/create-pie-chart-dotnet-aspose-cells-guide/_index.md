---
"date": "2025-04-05"
"description": "برنامج تعليمي لبرمجة Aspose.Cells Net"
"title": "إنشاء مخطط دائري في .NET باستخدام Aspose.Cells - دليل كامل"
"url": "/ar/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# كيفية إنشاء مخطط دائري في .NET باستخدام Aspose.Cells: دليل خطوة بخطوة

## مقدمة

يُعد إنشاء تمثيلات بصرية للبيانات مهارة أساسية، خاصةً عند محاولة إيصال معلومات معقدة ببساطة وفعالية. سواء كنت تعمل على تقرير أعمال أو تُحلل إحصاءات ديموغرافية، تُقدم المخططات الدائرية طريقة سهلة لتوضيح أجزاء من الكل. سيرشدك هذا الدليل خلال عملية إنشاء مخطط دائري في .NET باستخدام Aspose.Cells، وهي مكتبة فعّالة تُبسّط العمل مع مستندات Excel برمجيًا.

**ما سوف تتعلمه:**
- كيفية تهيئة وإعداد مصنف Excel.
- ملء البيانات في خلايا ورقة العمل للتوضيح.
- إنشاء مخطط دائري وتكوينه باستخدام Aspose.Cells لـ .NET.
- تخصيص ألوان الشريحة في المخطط الدائري لتحسين المظهر المرئي.
- تركيب الأعمدة تلقائيًا وحفظ المصنف الخاص بك.

دعونا نتعمق في كيفية استخدام Aspose.Cells لإنشاء مخططات دائرية جذابة بسهولة. قبل أن نبدأ، تأكد من استيفائك للمتطلبات الأساسية للمتابعة بسلاسة.

## المتطلبات الأساسية

للبدء بهذا البرنامج التعليمي، تأكد من أن لديك:

- **المكتبات المطلوبة:** ستحتاج إلى مكتبة Aspose.Cells لـ .NET. تأكد من إعداد مشروعك لاستخدامها.
- **متطلبات إعداد البيئة:** بيئة تطوير مناسبة مثل Visual Studio مثبتة على نظامك.
- **المتطلبات المعرفية:** فهم أساسي لبرمجة C# والتعرف على هياكل مستندات Excel.

## إعداد Aspose.Cells لـ .NET

قبل البدء في البرمجة، عليك تثبيت مكتبة Aspose.Cells في مشروعك. إليك الطريقة:

### التثبيت عبر CLI
افتح محطتك أو موجه الأوامر وقم بتشغيل:
```bash
dotnet add package Aspose.Cells
```

### التثبيت عبر مدير الحزم
إذا كنت تستخدم Visual Studio، فافتح وحدة التحكم في إدارة الحزم NuGet وقم بتنفيذ:
```powershell
PM> Install-Package Aspose.Cells
```

#### خطوات الحصول على الترخيص
يمكنك البدء بفترة تجريبية مجانية لتقييم Aspose.Cells. للاستخدام الممتد، يمكنك الحصول على ترخيص مؤقت أو شرائه مباشرةً من موقعهم الإلكتروني.

#### التهيئة والإعداد الأساسي

لتهيئة المكتبة في مشروع C# الخاص بك:
```csharp
using Aspose.Cells;

// إنشاء مثيل لفئة Workbook
Workbook workbook = new Workbook();
```

يتيح لك هذا الإعداد الأساسي البدء في العمل مع ملفات Excel برمجيًا.

## دليل التنفيذ

### الميزة 1: تهيئة المصنف وورقة العمل

**ملخص:** تعمل هذه الميزة على إنشاء مصنف جديد والوصول إلى ورقة العمل الأولى الخاصة به، مما يمهد الطريق لإدخال البيانات وإنشاء المخطط.

#### التهيئة خطوة بخطوة
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // إنشاء كائن مصنف جديد
        Workbook workbook = new Workbook();
        
        // الوصول إلى ورقة العمل الأولى في المصنف
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
هنا، `Workbook` يمثل ملف Excel، والوصول إليه `Worksheets[0]` يعطيك الورقة الأولى.

### الميزة 2: ملء البيانات لمخطط دائري

**ملخص:** يُعدّ ملء البيانات أمرًا بالغ الأهمية، إذ يُشكّل أساس مخططك البياني. تتضمن هذه الخطوة إدخال أسماء الدول ونسب سكانها العالمية المقابلة في خلايا مُحدّدة.

#### تعبئة البيانات خطوة بخطوة
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // أدخل بيانات الدولة في العمود C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // أدخل بيانات النسبة المئوية في العمود D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
تضمن هذه الخطوة أن بياناتك جاهزة للتوضيح.

### الميزة 3: إنشاء مخطط دائري وتكوينه

**ملخص:** تتضمن هذه الميزة إنشاء مخطط دائري، وتعيين بيانات السلسلة الخاصة به، وتكوين خصائص مختلفة مثل العنوان وموضع الأسطورة.

#### إنشاء مخطط دائري خطوة بخطوة
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // إضافة مخطط دائري إلى ورقة العمل
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // تعيين سلسلة البيانات للرسم البياني
        pie.NSeries.Add("D3:D8", true);

        // تحديد بيانات الفئة وتكوين العنوان
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
يقوم هذا الكود بإنشاء مخطط جذاب بصريًا مرتبطًا ببياناتك.

### الميزة 4: تخصيص ألوان الشريحة في المخطط الدائري

**ملخص:** يُحسّن تخصيص مظهر كل شريحة سهولة القراءة والجمال. تتضمن هذه الخطوة تخصيص ألوان فريدة لكل شريحة.

#### تخصيص الألوان خطوة بخطوة
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // تعيين ألوان مخصصة لكل شريحة
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
تضيف هذه الخطوة لمسة حيوية إلى الرسم البياني الخاص بك.

### الميزة 5: ملاءمة الأعمدة تلقائيًا وحفظ المصنف

**ملخص:** تتضمن الخطوات النهائية ضبط عرض الأعمدة لتحسين رؤية البيانات وحفظ المصنف بتنسيق Excel.

#### ضبط العمود وحفظه خطوة بخطوة
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // ضبط الأعمدة تلقائيًا لتناسب المحتوى
        worksheet.AutoFitColumns();

        // حفظ المصنف كملف Excel
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
ويضمن هذا أن تكون وثيقتك النهائية مصقولة وجاهزة للعرض.

## التطبيقات العملية

- **التقارير التجارية:** استخدم المخططات الدائرية لتصوير توزيع المبيعات حسب المنطقة.
- **الدراسات الديموغرافية:** تصور بيانات السكان عبر بلدان أو مناطق مختلفة.
- **الأدوات التعليمية:** إنشاء وسائل مساعدة بصرية جذابة للطلاب في دورات الإحصاء.
- **تحليل الرعاية الصحية:** عرض توزيعات بيانات المرضى داخل مرافق الرعاية الصحية.

## اعتبارات الأداء

لضمان الأداء الأمثل عند استخدام Aspose.Cells، ضع ما يلي في الاعتبار:

- **التعامل الفعال مع البيانات:** قم بإدارة مجموعات البيانات الكبيرة عن طريق معالجتها في أجزاء إذا لزم الأمر.
- **إدارة الذاكرة:** تخلص من الكائنات بشكل صحيح لتحرير الموارد وتجنب تسرب الذاكرة.
- **تكوينات الرسم البياني المُحسّنة:** قم بتقليل العمليات الحسابية المعقدة أو العرض أثناء إنشاء الرسم البياني للحصول على أداء أسرع.

## خاتمة

لقد تعلمتَ الآن كيفية إنشاء مخطط دائري في .NET باستخدام Aspose.Cells. تُبسّط هذه المكتبة الفعّالة التعامل مع مستندات Excel، مما يتيح لك التركيز على تحليل البيانات بدلاً من تعقيدات معالجة الملفات. جرّب أنواعًا مختلفة من المخططات وخيارات التخصيص المتاحة في Aspose.Cells لتحسين تطبيقاتك بشكل أكبر.

**الخطوات التالية:**
- استكشف أنواعًا أخرى من المخططات مثل المخططات الشريطية أو الخطية.
- دمج وظائف Aspose.Cells في مشاريع .NET الأكبر حجمًا لإعداد التقارير تلقائيًا.

هل أنت مستعد للارتقاء بمهاراتك في تصور البيانات إلى مستوى أعلى؟ تعمق أكثر باستكشاف المزيد من ميزات Aspose.Cells وابدأ بتطبيقها في مشاريعك اليوم!

## قسم الأسئلة الشائعة

1. **ما هو استخدام Aspose.Cells؟**
   - إنها مكتبة لإدارة ملفات Excel برمجيًا، مما يتيح لك إنشاء جداول البيانات وتعديلها وتحليلها.

2. **هل يمكنني استخدام Aspose.Cells بدون ترخيص؟**
   - نعم، ولكن مع قيود. تتيح لك النسخة التجريبية المجانية أو الترخيص المؤقت الوصول الكامل إلى الميزات.

3. **كيف يمكنني تخصيص مظهر مخطط الفطيرة الخاص بي بشكل أكبر؟**
   - استخدم خصائص إضافية مثل `pie.NSeries[0].Area.Formatting` لمزيد من التحكم في الجماليات.

4. **ما هي بعض المشكلات الشائعة عند إنشاء المخططات البيانية في Aspose.Cells؟**
   - تأكد من تحديد نطاقات البيانات بشكل صحيح ومن تكوين جميع خصائص الرسم البياني الضرورية قبل العرض.

5. **كيف يمكنني دمج Aspose.Cells مع مكتبات .NET الأخرى؟**
   - استخدم Aspose.Cells كجزء من حل .NET أكبر، والاستفادة من قدراته جنبًا إلى جنب مع المكتبات الأخرى للتطبيقات الشاملة.

## موارد

- **التوثيق:** [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/)
- **تحميل:** [إصدارات Aspose.Cells](https://releases.aspose.com/cells/net/)
- **شراء:** [شراء Aspose.Cells](https://purchase.aspose.com/buy)
- **نسخة تجريبية مجانية:** [نسخة تجريبية مجانية من Aspose.Cells](https://releases.aspose.com/cells/net/)
- **رخصة مؤقتة:** [احصل على رخصة مؤقتة](https://purchase.aspose.com/temporary-license/)
- **يدعم:** [منتدى أسبوزي](https://forum.aspose.com/c/cells/9)

باتباع هذا الدليل، أصبحتَ الآن جاهزًا لإنشاء مخططات دائرية جذابة بصريًا في تطبيقات .NET باستخدام Aspose.Cells. برمجة ممتعة!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}