---
title: تنفيذ صيغة الخلية المحلية على غرار صيغة النطاق المحلية
linktitle: تنفيذ صيغة الخلية المحلية على غرار صيغة النطاق المحلية
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: اكتشف كيفية تنفيذ صيغة خلية مشابهة لوظيفة صيغة النطاق المحلية في Aspose.Cells for .NET. تعلم كيفية تخصيص أسماء الوظائف المضمنة في Excel والمزيد.
weight: 13
url: /ar/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ صيغة الخلية المحلية على غرار صيغة النطاق المحلية

## مقدمة
Aspose.Cells for .NET عبارة عن واجهة برمجة تطبيقات قوية ومرنة للتعامل مع جداول البيانات تتيح لك إنشاء ملفات Excel ومعالجتها وتحويلها برمجيًا. إحدى الميزات العديدة التي توفرها Aspose.Cells هي القدرة على تخصيص سلوك وظائف Excel المضمنة، بما في ذلك القدرة على إنشاء أسماء وظائف محلية خاصة بك. في هذا البرنامج التعليمي، سنرشدك خلال الخطوات اللازمة لتنفيذ صيغة خلية مشابهة لوظيفة صيغة النطاق المحلية في Aspose.Cells for .NET.
## المتطلبات الأساسية
قبل أن تبدأ، تأكد من أن لديك ما يلي:
1. تم تثبيت Microsoft Visual Studio 2010 أو إصدار أحدث على نظامك.
2.  أحدث إصدار من مكتبة Aspose.Cells for .NET المثبتة في مشروعك. يمكنك تنزيل المكتبة من[صفحة تنزيل Aspose.Cells لـ .NET](https://releases.aspose.com/cells/net/).
## استيراد الحزم
للبدء، ستحتاج إلى استيراد الحزم اللازمة في مشروع C# الخاص بك. أضف عبارات الاستخدام التالية في أعلى ملف التعليمات البرمجية الخاص بك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## الخطوة 1: إنشاء فئة إعدادات العولمة المخصصة
 الخطوة الأولى هي إنشاء مخصص`GlobalizationSettings`فئة تسمح لك بتجاوز السلوك الافتراضي لوظائف Excel. في هذا المثال، سنقوم بتغيير أسماء`SUM` و`AVERAGE` وظائف ل`UserFormulaLocal_SUM` و`UserFormulaLocal_AVERAGE`، على التوالى.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //قم بتغيير اسم دالة SUM حسب احتياجاتك.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //قم بتغيير اسم الدالة AVERAGE وفقًا لاحتياجاتك.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## الخطوة 2: إنشاء مصنف جديد وتعيين إعدادات العولمة المخصصة
 بعد ذلك، قم بإنشاء مثيل جديد لـ Workbook وقم بتعيينه مخصصًا`GlobalizationSettings` فئة التنفيذ إلى مصنف العمل`Settings.GlobalizationSettings` ملكية.
```csharp
//إنشاء مصنف
Workbook wb = new Workbook();
//تعيين فئة تنفيذ GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## الخطوة 3: الوصول إلى ورقة العمل الأولى والخلية
الآن، دعنا نصل إلى ورقة العمل الأولى في المصنف وخلية محددة داخل تلك ورقة العمل.
```csharp
//الوصول إلى ورقة العمل الأولى
Worksheet ws = wb.Worksheets[0];
//الوصول إلى بعض الخلايا
Cell cell = ws.Cells["C4"];
```
## الخطوة 4: تعيين الصيغ وطباعة الصيغة المحلية
 وأخيرا، دعونا نعين`SUM` و`AVERAGE` الصيغ إلى الخلية وطباعة النتيجة`FormulaLocal` قيم.
```csharp
//تعيين صيغة SUM وطباعة FormulaLocal الخاصة بها
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//تعيين صيغة المتوسط وطباعة صيغتها المحلية
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## خاتمة
في هذا البرنامج التعليمي، تعلمت كيفية تنفيذ صيغة خلية مشابهة لوظيفة صيغة النطاق المحلية في Aspose.Cells لـ .NET. من خلال إنشاء صيغة خلية مخصصة، يمكنك إنشاء جدول بيانات محلي.`GlobalizationSettings` باستخدام الفئة، يمكنك تجاوز السلوك الافتراضي لوظائف Excel وتخصيص أسماء الوظائف المحلية لتناسب احتياجاتك. يمكن أن يكون هذا مفيدًا بشكل خاص عند العمل مع مستندات Excel المترجمة أو الدولية.
## الأسئلة الشائعة
###  ما هو الغرض من ذلك؟`GlobalizationSettings` class in Aspose.Cells?
 ال`GlobalizationSettings` تتيح لك الفئة الموجودة في Aspose.Cells تخصيص سلوك وظائف Excel المضمنة، بما في ذلك القدرة على تغيير أسماء الوظائف المحلية.
###  هل يمكنني تجاوز سلوك الوظائف الأخرى غير`SUM` and `AVERAGE`?
 نعم، يمكنك تجاوز سلوك أي وظيفة مضمنة في Excel عن طريق تعديل`GetLocalFunctionName` الطريقة في عادتك`GlobalizationSettings` فصل.
### هل هناك طريقة لإعادة تعيين أسماء الوظائف إلى قيمها الافتراضية؟
 نعم، يمكنك إعادة تعيين أسماء الوظائف عن طريق إزالة الأسماء المخصصة`GlobalizationSettings` الصف أو عن طريق إرجاع سلسلة فارغة من`GetLocalFunctionName` طريقة.
### هل يمكنني استخدام هذه الميزة لإنشاء وظائف مخصصة في Aspose.Cells؟
 لا، ال`GlobalizationSettings`تم تصميم الفئة لتجاوز سلوك وظائف Excel المضمنة، وليس لإنشاء وظائف مخصصة. إذا كنت بحاجة إلى إنشاء وظائف مخصصة، فيمكنك استخدام`UserDefinedFunction` الفئة في Aspose.Cells.
### هل هذه الميزة متوفرة في جميع إصدارات Aspose.Cells لـ .NET؟
 نعم،`GlobalizationSettings` تتوفر الفئة والقدرة على تخصيص أسماء الوظائف في جميع إصدارات Aspose.Cells لـ .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
