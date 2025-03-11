---
title: استبدال العلامة بالنص في مربع النص في Excel
linktitle: استبدال العلامة بالنص في مربع النص في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: استبدل النص في مربعات النص في جداول بيانات Excel بسهولة باستخدام Aspose.Cells for .NET. دليل خطوة بخطوة لأتمتة Excel.
weight: 11
url: /ar/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استبدال العلامة بالنص في مربع النص في Excel

## مقدمة
في هذه المقالة، سنتعمق في مهمة محددة: استبدال العلامات بالنص داخل مربعات النص في ورقة Excel باستخدام Aspose.Cells. وسنرشدك خلال العملية بأكملها خطوة بخطوة، مع التأكد من فهمك لكل التفاصيل. وبحلول نهاية هذا البرنامج التعليمي، لن تعزز فهمك لـ Aspose.Cells فحسب، بل ستعمل أيضًا على تبسيط المهام المرتبطة بـ Excel!
## المتطلبات الأساسية
قبل أن تتمكن من البدء، ستحتاج إلى إعداد بعض الأشياء:
1. Visual Studio: تأكد من تثبيت Visual Studio. فهو عبارة عن بيئة تطوير متكاملة مرنة تجعل كتابة التعليمات البرمجية بلغة C# أمرًا سهلاً.
2.  مكتبة Aspose.Cells: إذا لم تقم بذلك بالفعل، فقم بتنزيل مكتبة Aspose.Cells لـ .NET من[صفحة](https://releases.aspose.com/cells/net/)يمكنك أيضًا الحصول على نسخة تجريبية مجانية للتعرف على ميزاتها.
3. المعرفة الأساسية بلغة C#: إن الفهم الأساسي لبرمجة C# سيساعدك كثيرًا في اتباع هذا الدليل بسهولة.
الآن بعد أن أصبح كل شيء جاهزًا، دعنا ننتقل إلى الجزء الممتع - كتابة الكود!
## استيراد الحزم
أولاً وقبل كل شيء، دعنا نستورد الحزم الضرورية. هذا أمر بالغ الأهمية لأنه بدون الاستيراد الصحيح، لن يتعرف الكود الخاص بك على الفئات والطرق التي سنستخدمها.
## ابدأ مشروعك بلغة C#
افتح Visual Studio وقم بإنشاء مشروع C# جديد، ويفضل أن يكون تطبيق وحدة تحكم، حيث سيسمح لك برؤية الناتج بسهولة.
## إضافة مرجع Aspose.Cells
- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
- حدد "إضافة" > "مرجع".
- انتقل إلى الموقع الذي قمت بتنزيل مكتبة Aspose.Cells منه وقم بتضمينها في مشروعك.
## استيراد المساحات الاسمية الضرورية
 بمجرد إضافة المرجع، أضف ما يلي`using` التوجيه في الجزء العلوي من ملفك الرئيسي:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
يتيح لك هذا الوصول إلى الفئات داخل مساحة اسم Aspose.Cells.
الآن بعد أن قمنا بإعداد بيئتنا، فلننتقل إلى الجزء الأكثر أهمية وهو البرمجة! هدفنا هو العثور على علامات محددة في مربعات النص داخل ملف Excel واستبدالها بالنص المقدم.
## الخطوة 1: تحديد دليل المصدر والإخراج
أولاً، نحتاج إلى تحديد مكان وجود ملف Excel المصدر والمكان الذي نريد حفظ النسخة المعدلة فيه.
```csharp
// دليل المصدر والمخرج
string sourceDir = "Your Document Directory"; // التغيير إلى الدليل الخاص بك
string outputDir = "Your Document Directory"; // التغيير إلى الدليل الخاص بك
```
## الخطوة 2: تحميل المصنف
هذا هو المكان الذي سنقوم فيه بتحميل مصنف Excel الخاص بنا. إذا لم يكن الملف موجودًا، فسيؤدي ذلك إلى ظهور خطأ. لذا، تأكد من صحة مسار الملف!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 هنا، نقوم بتحميل ملف Excel موجود يسمى`sampleReplaceTagWithText.xlsx`.
## الخطوة 3: تحديد العلامات والنص البديل
بعد ذلك، نحتاج إلى تحديد العلامات التي نبحث عنها وما نريد استبدالها به.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 في هذا المثال، يتم تقسيم العلامات باستخدام`$`يمكنك استبدال هذا بأي فاصل تفضله.
## الخطوة 4: تكرار العلامات واستبدالها
سننشئ حلقة لفحص كل علامة نريد استبدالها. وهنا يحدث السحر!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## الخطوة 5: احفظ المصنف
الآن بعد أن قمنا بإجراء عمليات الاستبدال، حان الوقت لحفظ المصنف المعدّل بالتنسيق المطلوب. وإليك كيفية تحويله إلى ملف PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
ويمكنك أيضًا حفظه بتنسيقات أخرى مختلفة، بما في ذلك XLSX.
## الخطوة 6: تنفيذ منطق الاستبدال
 هذا هو المكان الذي يوجد فيه قلب وظائفنا.`sheetReplace` ستتعامل الطريقة مع الاستبدال الفعلي في أوراق عمل Excel.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- أولاً، نقوم بالمرور على كل ورقة عمل في المصنف.
- نقوم باستبدال العلامة الرئيسية ليس فقط في محتويات الخلية ولكن أيضًا في الرؤوس والتذييلات (إن وجدت).
- وأخيرًا، نقوم بتحديد كل مربع نص في الورقة واستبدال النص الموجود بداخله، استنادًا إلى العلامة التي نبحث عنها.
## خاتمة
والآن، لقد تعلمت كيفية استبدال العلامات بالنص في مربعات النص في مستندات Excel باستخدام Aspose.Cells for .NET. ويمكن أن يوفر لك هذا الكثير من الوقت، خاصة عند التعامل مع المهام المتكررة في جداول البيانات.
## الأسئلة الشائعة
### هل يمكنني استبدال العلامات عبر ملفات Excel المتعددة مرة واحدة؟
نعم، من خلال التنقل عبر قائمة الملفات، يمكنك تطبيق نفس المنطق على ملفات Excel المتعددة.
### هل أحتاج إلى ترخيص مدفوع لاستخدام Aspose.Cells؟
 يمكنك البدء بإصدار تجريبي مجاني، ولكن للحصول على الوظائف الكاملة، ستحتاج إلى شراء ترخيص. تحقق من[خيارات الشراء في Aspose](https://purchase.aspose.com/buy).
### هل يمكنني استبدال الصور في مربعات النص باستخدام Aspose.Cells؟
يتعامل Aspose.Cells بشكل أساسي مع النصوص. ومع ذلك، يمكنك معالجة الصور بشكل منفصل إذا لزم الأمر.
### ما هي التنسيقات التي يمكنني حفظ ملف Excel المعدل بها؟
يمكنك حفظه بتنسيقات مختلفة بما في ذلك XLSX، PDF، CSV، وما إلى ذلك.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
 يمكنك العثور على الدعم وطرح الأسئلة على[منتدى اسبوس](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
