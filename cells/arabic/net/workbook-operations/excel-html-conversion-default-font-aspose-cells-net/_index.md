---
"date": "2025-04-05"
"description": "تعرف على كيفية تعيين الخط الافتراضي عند تحويل ملفات Excel إلى HTML باستخدام Aspose.Cells لـ .NET، مما يضمن طباعة متسقة وعرضًا احترافيًا."
"title": "تعيين الخط الافتراضي في تحويل Excel إلى HTML باستخدام Aspose.Cells لـ .NET | دليل عمليات المصنف"
"url": "/ar/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إتقان إعداد الخط الافتراضي في تحويل Excel إلى HTML باستخدام Aspose.Cells لـ .NET

## مقدمة

قد يكون تحويل مصنف Excel إلى تنسيق HTML مع الحفاظ على تناسق الطباعة أمرًا صعبًا. يرشدك هذا البرنامج التعليمي إلى كيفية تعيين خط افتراضي باستخدام Aspose.Cells لـ .NET، مما يضمن أن تبدو مستنداتك المحولة أنيقة واحترافية. بإتقان هذه الميزة، ستتغلب على التحديات المتعلقة بالخطوط غير المعروفة أو غير المتوفرة أثناء عملية التحويل.

**ما سوف تتعلمه:**
- كيفية تعيين الخط الافتراضي عند تحويل ملفات Excel إلى HTML.
- دليل خطوة بخطوة حول استخدام Aspose.Cells لـ .NET.
- تقنيات للتعامل مع الخطوط غير المعروفة بسلاسة أثناء العرض.

دعنا نتعمق في إعداد بيئتك ونبدأ في استكشاف هذه الميزة!

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن لديك ما يلي:

- **بيئة .NET**:إصدار متوافق من .NET مثبت (على سبيل المثال، .NET Core أو .NET Framework).
- **مكتبة Aspose.Cells لـ .NET**:قم بتثبيت Aspose.Cells عبر NuGet.
- **المعرفة الأساسية بلغة C#**:ستكون المعرفة بمفاهيم برمجة C# مفيدة.

## إعداد Aspose.Cells لـ .NET

للبدء، قم بإعداد Aspose.Cells في بيئة التطوير الخاصة بك باتباع الخطوات التالية:

**التثبيت عبر CLI:**
```bash
dotnet add package Aspose.Cells
```

**التثبيت عبر مدير الحزم:**
```shell
PM> NuGet\Install-Package Aspose.Cells
```

### الحصول على الترخيص
- **نسخة تجريبية مجانية**:ابدأ بإصدار تجريبي مجاني لاستكشاف الميزات.
- **رخصة مؤقتة**:الحصول على ترخيص مؤقت لأغراض التقييم.
- **شراء**:فكر في شراء ترخيص للاستخدام الإنتاجي.

بمجرد التثبيت، قم بتشغيل مشروعك وإعداده على النحو التالي:
```csharp
using Aspose.Cells;
```

## دليل التنفيذ

### تعيين الخط الافتراضي أثناء العرض

تضمن هذه الميزة عرض مصنف Excel بخط افتراضي محدد عند التحويل إلى HTML. وهي مفيدة بشكل خاص في الحالات التي قد لا تتوفر فيها خطوط معينة على النظام المستهدف.

#### الخطوة 1: إنشاء مصنف والوصول إليه

إنشاء مثيل جديد من `Workbook` والوصول إلى ورقة العمل الأولى الخاصة به:
```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

// إنشاء كائن مصنف والوصول إلى ورقة العمل الأولى.
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];
```

#### الخطوة 2: تعديل نمط الخلية

قم بالوصول إلى خلية محددة، وأضف نصًا، واضبط الخط على خط غير معروف للتوضيح:
```csharp
// قم بالوصول إلى الخلية B4 وأضف بعض النص بداخلها.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// تعيين الخط في الخلية B4 إلى خط غير معروف.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

#### الخطوة 3: تحديد خيارات حفظ HTML

عيّن الخط الافتراضي في مُخرَجات HTML. هنا، سنُوضِّح ذلك بثلاثة خطوط مختلفة:

**ساعي جديد:**
```csharp
// احفظ المصنف بتنسيق HTML مع تعيين الخط الافتراضي إلى Courier New.
HtmlSaveOptions optsCourierNew = new HtmlSaveOptions();
optsCourierNew.DefaultFontName = "Courier New";
wb.Save(outputDir + "/out_courier_new_out.htm", optsCourierNew);
```

**اريال:**
```csharp
// احفظ المصنف بتنسيق HTML مع تعيين الخط الافتراضي إلى Arial.
HtmlSaveOptions optsArial = new HtmlSaveOptions();
optsArial.DefaultFontName = "Arial";
wb.Save(outputDir + "/out_arial_out.htm", optsArial);
```

**تايمز نيو رومان:**
```csharp
// احفظ المصنف بتنسيق HTML مع تعيين الخط الافتراضي إلى Times New Roman.
HtmlSaveOptions optsTimesNewRoman = new HtmlSaveOptions();
optsTimesNewRoman.DefaultFontName = "Times New Roman";
wb.Save(outputDir + "/times_new_roman_out.htm", optsTimesNewRoman);
```

### إنشاء مصنف العمل وتصميم الخلايا

يغطي هذا القسم إنشاء مصنف، والوصول إلى أوراق العمل، والخلايا، وتطبيق الأنماط:

#### الخطوة 1: تهيئة المصنف
إنشاء جديد `Workbook` مثال:
```csharp
// إنشاء كائن مصنف.
Workbook wb = new Workbook();
```

#### الخطوة 2: الوصول إلى ورقة العمل والخلية
انتقل إلى ورقة العمل الأولى والخلية B4 لإضافة نص وتنسيقه:
```csharp
// قم بالوصول إلى ورقة العمل الأولى في المصنف.
Worksheet ws = wb.Worksheets[0];

// قم بالوصول إلى الخلية B4 وأضف بعض النص بداخلها.
Cell cell = ws.Cells["B4"];
cell.PutValue("This text has some unknown or invalid font which does not exist.");

// تعيين الخط في الخلية B4 إلى خط غير معروف.
Style st = cell.GetStyle();
st.Font.Name = "UnknownNotExist";
st.Font.Size = 20;
cell.SetStyle(st);
```

## التطبيقات العملية
- **العلامة التجارية المتسقة**:تأكد من تطبيق خطوط العلامة التجارية بشكل متسق في مستندات HTML المصدرة.
- **قابلية نقل المستندات**:تعامل مع السيناريوهات التي تفتقر فيها البيئات المستهدفة إلى خطوط محددة.
- **التقارير الآلية**:استخدم هذه الميزة لإنشاء تقارير تلقائية ذات طباعة متسقة.

## اعتبارات الأداء
للحصول على الأداء الأمثل:
- إدارة استخدام الذاكرة عن طريق التخلص من الكائنات بشكل مناسب.
- تحسين إعدادات العرض استنادًا إلى احتياجات تطبيقك.
- قم بالتحديث بانتظام إلى أحدث إصدار من Aspose.Cells للحصول على ميزات محسنة وإصلاحات للأخطاء.

## خاتمة

لقد تعلمتَ كيفية تعيين خط افتراضي أثناء تحويل ملفات Excel إلى HTML باستخدام Aspose.Cells لـ .NET. تضمن هذه الميزة تناسق الطباعة، حتى عند عدم توفر بعض الخطوط في النظام المستهدف. لتحسين مهاراتك، استكشف الميزات الإضافية لـ Aspose.Cells وجرّب خيارات عرض مختلفة.

**الخطوات التالية**:حاول تنفيذ هذا الحل في مشاريعك وتخصيصه ليناسب احتياجاتك المحددة.

## قسم الأسئلة الشائعة
1. **ما هو Aspose.Cells لـ .NET؟**
   - مكتبة تسمح بالتعامل مع ملفات Excel وتحويلها داخل تطبيقات .NET.
2. **كيف أقوم بتثبيت Aspose.Cells؟**
   - استخدم NuGet Package Manager أو .NET CLI كما هو موضح أعلاه.
3. **هل يمكنني استخدام هذه الميزة مع الإصدارات الأقدم من .NET؟**
   - تأكد من التوافق عن طريق التحقق من متطلبات نظام المكتبة.
4. **ماذا لو لم يتم دعم الخط الافتراضي الخاص بي على كافة الأنظمة؟**
   - سيتم استخدام الخط الافتراضي المحدد، مما يضمن الاتساق عبر الأنظمة الأساسية.
5. **أين يمكنني العثور على المزيد من الموارد والدعم لـ Aspose.Cells؟**
   - راجع إلى [وثائق Aspose](https://reference.aspose.com/cells/net/) أو ال [منتدى الدعم](https://forum.aspose.com/c/cells/9).

## موارد
- **التوثيق**: [مرجع Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **تحميل**: [صفحة الإصدارات](https://releases.aspose.com/cells/net/)
- **شراء**: [شراء Aspose.Cells](https://purchase.aspose.com/buy)
- **نسخة تجريبية مجانية**: [تنزيل النسخة التجريبية](https://releases.aspose.com/cells/net/)
- **رخصة مؤقتة**: [طلب ترخيص](https://purchase.aspose.com/temporary-license/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}