---
"date": "2025-04-05"
"description": "تعرّف على كيفية إضافة الأشكال البيضاوية وتخصيصها في Excel باستخدام Aspose.Cells لـ .NET. حسّن عروض بياناتك بسهولة."
"title": "إضافة أشكال بيضاوية إلى Excel باستخدام Aspose.Cells لـ .NET | دليل خطوة بخطوة"
"url": "/ar/net/images-shapes/add-oval-shapes-excel-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# كيفية إضافة أشكال بيضاوية إلى أوراق عمل Excel باستخدام Aspose.Cells لـ .NET

## مقدمة

في عالم عرض البيانات، يُمكن أن يُعزز مظهر جداول بيانات Excel الجذابة فهمَ البيانات وتفاعلَها بشكل كبير. إضافة أشكال مُخصصة، مثل الأشكال البيضاوية، ليست سهلةً دائمًا مع وظائف Excel الأساسية. **Aspose.Cells لـ .NET** يوفر طريقة فعّالة لإدراج الأشكال البيضاوية وتخصيصها برمجيًا في أوراق العمل. سيوضح لك هذا الدليل التفصيلي كيفية الاستفادة من Aspose.Cells لإضافة أشكال بيضاوية إلى ملفات Excel بكفاءة.

### ما سوف تتعلمه:
- كيفية إعداد Aspose.Cells في مشروع .NET الخاص بك
- عملية إضافة الأشكال البيضاوية وتكوينها في ورقة عمل Excel
- خيارات التخصيص الرئيسية للأشكال البيضاوية
- أفضل الممارسات لدمج هذه الميزات في المشاريع الأكبر

دعونا نتعمق في المتطلبات الأساسية قبل أن نبدأ في الترميز!

## المتطلبات الأساسية

قبل أن تتمكن من البدء في إضافة الأشكال البيضاوية إلى أوراق العمل الخاصة بك، تأكد من توفر ما يلي:

- **Aspose.Cells لـ .NET**:مكتبة قوية تسمح بالتعامل على نطاق واسع مع ملفات Excel.
  - للتثبيت، استخدم أحد الأمرين:
    - **.NET CLI**:
      ```bash
إضافة حزمة Dotnet Aspose.Cells
```
    - **Package Manager**:
      ```powershell
PM> NuGet\Install-Package Aspose.Cells
```
- **بيئة التطوير**:تأكد من إعداد بيئة تطوير .NET المناسبة، مثل Visual Studio أو VS Code مع .NET SDK.
- **المعرفة الأساسية بـ C# وإطارات عمل .NET**:ستكون المعرفة بمفاهيم البرمجة الموجهة للكائنات في C# مفيدة.

## إعداد Aspose.Cells لـ .NET

إعداد Aspose.Cells سهل للغاية. اتبع الخطوات التالية للبدء:

1. **تثبيت الحزمة**:
   استخدم الأوامر المقدمة أعلاه لتثبيت حزمة Aspose.Cells في مشروعك.
   
2. **الحصول على الترخيص**:
   - يمكنك البدء بـ [نسخة تجريبية مجانية](https://releases.aspose.com/cells/net/) لاختبار الوظائف.
   - للحصول على ميزات موسعة، فكر في الحصول على ترخيص مؤقت أو شراء ترخيص من خلال [صفحة شراء Aspose](https://purchase.aspose.com/buy).

3. **التهيئة**:
   بمجرد التثبيت والترخيص، يمكنك تهيئة Aspose.Cells في تطبيقك:
   
   ```csharp
باستخدام Aspose.Cells؛
```

With the environment set up, let's move on to implementing oval shapes.

## Implementation Guide

### Adding an Oval Shape

This feature guides you through adding a basic oval shape to an Excel worksheet.

#### Overview
Adding ovals can enhance the visual appeal of your data presentation. In this section, we'll add and configure an oval in the first worksheet of our Excel file using Aspose.Cells.

#### Steps:

##### Step 1: Define Directory for Output

First, define where you want to save your output files:

```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";
string dataDir = Path.Combine(outputDir, "OvalShapeExample");

if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### الخطوة 2: إنشاء مصنف

إنشاء مثيل لـ `Workbook` الصف لبدء العمل مع ملفات Excel:

```csharp
Workbook excelbook = new Workbook();
```

##### الخطوة 3: إضافة الشكل البيضاوي

استخدم `AddOval` طريقة وضع الشكل البيضاوي في ورقة العمل:

```csharp
// أضف شكلًا بيضاويًا عند الإحداثيات والحجم المحددين
Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```

##### الخطوة 4: تكوين الموضع

تعيين نوع التنسيب إلى `FreeFloating` لمزيد من التحكم في المواضع:

```csharp
oval1.Placement = PlacementType.FreeFloating;
```

##### الخطوة 5: تعيين خصائص الخط

قم بتخصيص مظهر مخطط الشكل البيضاوي عن طريق ضبط سمك الخط ونمط الشرطة:

```csharp
// تعيين وزن الخط ونمط الشرطة
oval1.Line.Weight = 1;
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### الخطوة 6: حفظ المصنف

وأخيرًا، احفظ المصنف الخاص بك في ملف في الدليل المحدد:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExample.xls"));
```

#### نصائح استكشاف الأخطاء وإصلاحها:
- تأكد من تعيين جميع مسارات الدليل بشكل صحيح لمنع أخطاء عدم العثور على الملف.
- تأكد من أن Aspose.Cells مرخص بشكل صحيح إذا كنت تستخدم ميزات تتجاوز حدود الإصدار التجريبي.

### إضافة شكل بيضاوي آخر (دائرة)

الآن دعونا نضيف شكل بيضاوي آخر، مصمم على شكل دائرة، مع خصائص مختلفة.

#### ملخص
إضافة أشكال متعددة تُساعد في إنشاء تصورات أكثر تعقيدًا. سنشرح هنا كيفية إضافة شكل بيضاوي دائري إلى ورقة العمل.

#### خطوات:

##### الخطوة 1: التأكد من وجود الدليل

هذه الخطوة مشابهة للقسم السابق؛ تأكد من إعداد الدليل بشكل صحيح.

```csharp
if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### الخطوة 2: إنشاء مصنف

إنشاء جديد `Workbook` مثال على إضافة هذا الشكل:

```csharp
Workbook excelbook = new Workbook();
```

##### الخطوة 3: إضافة شكل الدائرة

أضف شكلًا بيضاويًا آخر بأبعاد تجعله يبدو كدائرة:

```csharp
// أضف شكلًا دائريًا بإحداثيات وأحجام مختلفة
Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```

##### الخطوة 4: تكوين الموضع

تعيين نوع الموضع للشكل الجديد:

```csharp
oval2.Placement = PlacementType.FreeFloating;
```

##### الخطوة 5: تعيين خصائص الخط

قم بتحديد وزن الخط ونمط الشرطة للتخصيص:

```csharp
// تخصيص خصائص الخط
oval2.Line.Weight = 1;
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### الخطوة 6: حفظ المصنف بالشكل الجديد

احفظ المصنف مرة أخرى، هذه المرة قم بتضمين كلا الشكلين:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExampleWithCircle.xls"));
```

## التطبيقات العملية

يتيح Aspose.Cells مجموعة واسعة من التطبيقات العملية لإضافة الأشكال البيضاوية إلى أوراق عمل Excel:

1. **تصور البيانات**:قم بتعزيز مخططات البيانات باستخدام التعليقات التوضيحية المصممة خصيصًا.
2. **تصميم لوحة القيادة**:استخدم الأشكال البيضاوية لتسليط الضوء على المقاييس أو الأقسام الرئيسية في لوحات المعلومات المالية.
3. **إنشاء القالب**:إنشاء قوالب قابلة لإعادة الاستخدام للتقارير التي تتطلب عناصر مرئية متسقة.

تُظهر حالات الاستخدام هذه مدى تنوع Aspose.Cells في البيئات المهنية والتجارية.

## اعتبارات الأداء

عند العمل مع مجموعات بيانات كبيرة أو أوراق عمل معقدة، يعد تحسين الأداء أمرًا بالغ الأهمية:

- **إدارة الذاكرة بكفاءة**:تأكد من التخلص السليم من الكائنات لتحرير الذاكرة.
- **عمليات الدفعات**:قم بإجراء العمليات على دفعات عندما يكون ذلك ممكنًا لتقليل وقت المعالجة.
- **استخدام الموارد**:راقب استخدام الموارد وقم بتحسين مسارات التعليمات البرمجية التي تتطلب تكاليف حسابية باهظة.

يمكن أن تساعدك اتباع أفضل الممارسات هذه في الحفاظ على أداء سلس عند استخدام Aspose.Cells لإجراء عمليات معالجة مكثفة في Excel.

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية إضافة وتكوين أشكال بيضاوية في جداول بيانات Excel باستخدام Aspose.Cells لـ .NET. باتباع الخطوات الموضحة، يمكنك تحسين عروض بياناتك التقديمية باستخدام عناصر مرئية مخصصة بسهولة. لمزيد من الاستكشاف، فكّر في التعمق في ميزات Aspose.Cells الأكثر تقدمًا أو دمج هذه التقنيات في مشاريع أكبر.

## قسم الأسئلة الشائعة

1. **هل يمكنني استخدام Aspose.Cells بدون ترخيص؟**
   - نعم، ولكن مع بعض القيود. تتوفر نسخة تجريبية لأغراض الاختبار.
2. **كيف يمكنني تغيير لون الشكل البيضاوي؟**
   - استخدم `FillFormat` خاصية لتخصيص لون التعبئة والنمط.
3. **هل من الممكن إضافة نص داخل الشكل البيضاوي؟**
   - نعم، يمكنك إدراج أشكال نصية داخل الأشكال البيضاوية باستخدام واجهة برمجة التطبيقات Aspose.Cells.
4. **هل يمكنني أتمتة هذه العملية لملفات متعددة؟**
   - بالتأكيد، قم بالمرور على مجموعة الملفات الخاصة بك وتطبيق هذه الأساليب برمجيًا.
5. **ما هي متطلبات النظام لتشغيل Aspose.Cells؟**
   - إنه يدعم .NET Framework 2.0 والإصدارات الأحدث، بما في ذلك .NET Core و.NET 5/6.

## موارد
- [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/)
- [تنزيل Aspose.Cells لـ .NET](https://releases.aspose.com/cells/net/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}