---
"description": "استبدل النصوص في مربعات النصوص في جداول بيانات Excel بسهولة باستخدام Aspose.Cells لـ .NET. دليل خطوة بخطوة لأتمتة Excel."
"linktitle": "استبدال العلامة بالنص في مربع النص في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "استبدال العلامة بالنص في مربع النص في Excel"
"url": "/ar/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استبدال العلامة بالنص في مربع النص في Excel

## مقدمة
في هذه المقالة، سنتعمق في مهمة محددة: استبدال العلامات بنصوص داخل مربعات النص في ورقة Excel باستخدام Aspose.Cells. سنرشدك خلال العملية بأكملها خطوة بخطوة، مع ضمان فهمك التام لكل التفاصيل. بنهاية هذا البرنامج التعليمي، لن تُحسّن فهمك لـ Aspose.Cells فحسب، بل ستُبسّط أيضًا مهامك المتعلقة بـ Excel!
## المتطلبات الأساسية
قبل أن تتمكن من البدء، ستحتاج إلى تجهيز بعض الأشياء:
1. Visual Studio: تأكد من تثبيت Visual Studio. إنه بيئة تطوير متكاملة مرنة تُسهّل كتابة البرامج بلغة C#.
2. مكتبة Aspose.Cells: إذا لم تقم بذلك بالفعل، فقم بتنزيل مكتبة Aspose.Cells لـ .NET من [صفحة](https://releases.aspose.com/cells/net/)يمكنك أيضًا الحصول على نسخة تجريبية مجانية للتعرف على ميزاتها.
3. المعرفة الأساسية بلغة C#: إن الفهم الأساسي لبرمجة C# سيساعدك كثيرًا في اتباع هذا الدليل بسهولة.
الآن بعد أن أصبحت كل الأمور جاهزة، دعنا ننتقل إلى الجزء الممتع - كتابة الكود!
## استيراد الحزم
أولاً، لنستورد الحزم اللازمة. هذا أمر بالغ الأهمية، لأنه بدون الاستيراد الصحيح، لن يتعرف الكود على الفئات والأساليب التي سنستخدمها.
## ابدأ مشروعك بلغة C#
افتح Visual Studio وقم بإنشاء مشروع C# جديد، ويفضل أن يكون تطبيق وحدة تحكم، حيث سيسمح لك برؤية الناتج بسهولة.
## إضافة مرجع Aspose.Cells
- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
- حدد "إضافة" > "مرجع".
- انتقل إلى الموقع الذي قمت بتنزيل مكتبة Aspose.Cells منه وأدرجها في مشروعك.
## استيراد مساحات الأسماء الضرورية
بمجرد إضافة المرجع، أضف ما يلي `using` التوجيه في أعلى ملفك الرئيسي:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
يتيح لك هذا الوصول إلى الفئات داخل مساحة اسم Aspose.Cells.
بعد أن أعددنا بيئتنا، لننتقل إلى الجزء الأهم: البرمجة! هدفنا هو العثور على علامات محددة في مربعات النص ضمن ملف Excel واستبدالها بالنص المُعطى.
## الخطوة 1: تحديد دليل المصدر والإخراج
أولاً، نحتاج إلى تحديد مكان وجود ملف Excel المصدر والمكان الذي نريد حفظ النسخة المعدلة فيه.
```csharp
// دليل المصدر والمخرجات
string sourceDir = "Your Document Directory"; // التغيير إلى الدليل الخاص بك
string outputDir = "Your Document Directory"; // التغيير إلى الدليل الخاص بك
```
## الخطوة 2: تحميل المصنف
هنا سنحمّل مصنف إكسل. إذا لم يكن الملف موجودًا، فسيظهر خطأ. لذا، تأكد من صحة مسار الملف!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
هنا، نقوم بتحميل ملف Excel موجود يسمى `sampleReplaceTagWithText.xlsx`.
## الخطوة 3: تحديد العلامات والنص البديل
بعد ذلك، نحتاج إلى تحديد العلامات التي نبحث عنها وما نريد استبدالها به.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
في هذا المثال، يتم تقسيم العلامات باستخدام `$`يمكنك استبدال هذا بأي فاصل تفضله.
## الخطوة 4: تكرار العلامات واستبدالها
سننشئ حلقةً لفحص كل علامة نريد استبدالها. وهنا يأتي السحر!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## الخطوة 5: حفظ المصنف
بعد أن انتهينا من الاستبدالات، حان وقت حفظ المصنف المُعدَّل بالتنسيق المطلوب. إليك كيفية تحويله إلى ملف PDF.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
يمكنك أيضًا حفظه بتنسيقات أخرى مختلفة، بما في ذلك XLSX.
## الخطوة 6: تنفيذ منطق الاستبدال
هذا هو المكان الذي يوجد فيه قلب وظائفنا. `sheetReplace` ستتعامل الطريقة مع الاستبدال الفعلي في أوراق عمل Excel.
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
- نقوم باستبدال العلامة الرئيسية ليس فقط في محتويات الخلية ولكن أيضًا في الرؤوس والتذييلات (إذا كانت موجودة).
- وأخيرًا، نقوم بتحديد كل مربع نص في الورقة واستبدال النص الموجود بداخله، استنادًا إلى العلامة التي نبحث عنها.
## خاتمة
ها قد انتهيت! لقد تعلمت الآن كيفية استبدال العلامات بنصوص في مربعات النص في مستندات Excel باستخدام Aspose.Cells لـ .NET. هذا يوفر عليك الكثير من الوقت، خاصةً عند التعامل مع المهام المتكررة في جداول البيانات.
## الأسئلة الشائعة
### هل يمكنني استبدال العلامات عبر ملفات Excel متعددة مرة واحدة؟
نعم، من خلال التكرار عبر قائمة الملفات، يمكنك تطبيق نفس المنطق على ملفات Excel متعددة.
### هل أحتاج إلى ترخيص مدفوع لاستخدام Aspose.Cells؟
يمكنك البدء بفترة تجريبية مجانية، ولكن للاستفادة الكاملة من الميزات، ستحتاج إلى شراء ترخيص. تحقق من [خيارات الشراء في Aspose](https://purchase.aspose.com/buy).
### هل يمكنني استبدال الصور في مربعات النص باستخدام Aspose.Cells؟
يتعامل Aspose.Cells بشكل أساسي مع النصوص. مع ذلك، يمكنك معالجة الصور بشكل منفصل عند الحاجة.
### ما هي التنسيقات التي يمكنني حفظ ملف Excel المعدل بها؟
يمكنك حفظه بتنسيقات مختلفة بما في ذلك XLSX، PDF، CSV، وما إلى ذلك.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
يمكنك العثور على الدعم وطرح الأسئلة على [منتدى Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}