---
title: نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells
linktitle: نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية نسخ VBA Macro User Form Designer بكفاءة في Aspose.Cells for .NET من خلال البرنامج التعليمي الشامل خطوة بخطوة! أطلق العنان لإمكانات Excel.
weight: 11
url: /ar/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells

## مقدمة
مرحبًا بك! إذا كنت تتطلع إلى تحسين تجربتك في Excel باستخدام وحدات الماكرو ونماذج المستخدم في VBA، فأنت في المكان المناسب! في هذا الدليل، نتعمق في كيفية نسخ VBA Macro UserForm Designer بسلاسة من مصنف إلى آخر باستخدام Aspose.Cells for .NET. سواء كنت مطورًا متمرسًا أو مبتدئًا، فسنقوم بإرشادك خلال كل خطوة حاسمة. اعتبر هذا دليلك لإتقان فن التعامل مع ملفات Excel برمجيًا. هل أنت مستعد للبدء؟ هيا بنا!
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة للترميز، دعنا نتأكد من أن لديك كل ما تحتاجه:
1. بيئة تطوير C#: يجب أن يكون لديك بيئة عمل جاهزة لتطوير C#. يوصى بشدة باستخدام Visual Studio.
2.  مكتبة Aspose.Cells لـ .NET: تأكد من دمج مكتبة Aspose.Cells في مشروعك. يمكنك بسهولة[تحميله هنا](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بـ VBA ووحدات الماكرو في Excel: إن الفهم الجيد لـ VBA وكيفية عمل وحدات الماكرو في Excel سيساعدك على التنقل عبر هذا البرنامج التعليمي بسهولة.
4. ملف Excel يحتوي على نموذج مستخدم: للتجربة أو إنشاء أو الحصول على مصنف Excel يحتوي على نموذج مستخدم، ويفضل أن يكون مع تمكين وحدات الماكرو (مثل`.xlsm` الملفات).
## استيراد الحزم
في مشروع C# الخاص بك، ستحتاج إلى استيراد مساحات أسماء معينة في أعلى الملف للاستفادة من وظائف Aspose.Cells. وإليك كيفية القيام بذلك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
يتيح لك تضمين هذه المساحات الأسماءية الوصول إلى جميع الأدوات القوية المضمنة داخل مكتبة Aspose.Cells. 
الآن بعد أن قمنا بتغطية المتطلبات الأساسية والحزم، حان الوقت للانتقال إلى الجزء الممتع: البرمجة! دعنا نوضح ذلك خطوة بخطوة.
## الخطوة 1: قم بتحديد أدلة المصدر والإخراج
أولاً، عليك تحديد مكان وجود ملفاتك:
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
 هنا، استبدل`"Your Document Directory"` مع المسار الفعلي الذي يتم تخزين ملفاتك فيه. هذا هو المكان الذي سيتم فيه الحصول على مصنف العمل المصدر (مع نموذج المستخدم) ومكان حفظ مصنف العمل الجديد.
## الخطوة 2: إنشاء مصنف هدف فارغ
بعد ذلك، دعنا نقوم بإنشاء مصنف الهدف الذي سنقوم فيه بنسخ نموذج المستخدم ووحدات الماكرو الخاصة بنا:
```csharp
// إنشاء مصنف هدف فارغ
Workbook target = new Workbook();
```
يقوم هذا السطر من التعليمات البرمجية بإنشاء مصنف فارغ جديد لنملأه بالبيانات. فكر فيه كلوحة فارغة لتحفتك الفنية!
## الخطوة 3: قم بتحميل مصنف القالب الخاص بك
نحن بحاجة إلى تحميل المصنف الذي يحتوي على نموذج المستخدم ووحدات الماكرو الخاصة بك:
```csharp
// قم بتحميل ملف Excel الذي يحتوي على نموذج مستخدم VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 تأكد من التغيير`"sampleDesignerForm.xlsm"` إلى اسم الملف الفعلي الخاص بك. هذا المصنف يشبه كتاب الوصفات الخاص بك - فهو ما سنستخرج منه مكوناتنا!
## الخطوة 4: نسخ أوراق العمل إلى المصنف المستهدف
الآن، لنبدأ بنسخ أوراق العمل من قالبنا إلى المصنف المستهدف:
```csharp
// نسخ كافة أوراق عمل القالب إلى المصنف المستهدف
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // ضع الرسالة في الخلية A2 من ورقة العمل المستهدفة
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
في هذه الخطوة، نقوم بتكرار كل ورقة عمل في القالب ونسخها إلى المصنف المستهدف. إذا فكرت في الأمر، فستجد أن الأمر أشبه بنقل أفضل وصفاتك من كتاب طبخ إلى آخر!
## الخطوة 5: نسخ وحدات الماكرو VBA من القالب
بعد ذلك، سنقوم بنسخ وحدات ماكرو VBA، بما في ذلك وحدات UserForm Designer، إلى مصنفنا الجديد:
```csharp
// نسخ نموذج مستخدم VBA-Macro Designer من القالب إلى الهدف
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // نسخ كود وحدة ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // نسخ كود وبيانات الوحدات الأخرى
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // احصل على بيانات نموذج المستخدم أي تخزين المصمم
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // إضافة وحدة تخزين المصمم إلى مشروع Vba المستهدف
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
تتولى هذه الكتلة الضخمة من التعليمات البرمجية فحص كل وحدة VBA في ملف القالب. نحن نقوم بنسخ تصميم UserForm والرموز المرتبطة به. الأمر أشبه بضمان حصولك ليس فقط على وصفة فطيرة الجدة الشهيرة ولكن أيضًا على تقنيات الخبز الدقيقة الخاصة بها!
## الخطوة 6: احفظ المصنف المستهدف
بعد أن حققنا جميع النسخ لدينا، حان الوقت لحفظ عملنا الشاق:
```csharp
// حفظ المصنف المستهدف
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
تأكد من تعديل اسم ملف الإخراج حسب الحاجة. بمجرد حفظه، فإنك تقوم فعليًا بإنشاء نسخة مخصصة لك من المصنف مليئة بوحدات الماكرو ونماذج المستخدم. ما مدى روعة هذا؟
## الخطوة 7: تأكيد النجاح
وأخيرًا، دعنا نطبع رسالة النجاح على وحدة التحكم:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
يطمئنك هذا السطر الصغير إلى أن العملية سارت بسلاسة. إنه الكرز الموجود فوق حلوى الترميز الخاصة بك!
## خاتمة
تهانينا! لقد أكملت الدليل خطوة بخطوة لنسخ مصمم نموذج مستخدم ماكرو VBA من مصنف إلى آخر باستخدام Aspose.Cells for .NET. قد يبدو الأمر مرهقًا بعض الشيء في البداية، ولكن مع الممارسة، ستتمكن من التعامل مع معالجات المصنف مثل المحترفين. تذكر أن البرمجة تتعلق بالممارسة، لذا لا تتردد في تجربة أشياء مختلفة في ملفات Excel الخاصة بك. إذا كانت لديك أي أسئلة أو واجهت أي مشكلات، فلا تتردد في مراجعة منتديات Aspose أو الوثائق للحصول على الدعم!
## الأسئلة الشائعة
### ما هي إصدارات Excel التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells مجموعة واسعة من تنسيقات Excel بما في ذلك XLSX، وXLSM، وCSV، والمزيد.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
 نعم! يمكنك البدء بإصدار تجريبي مجاني، والذي يسمح لك بتقييم المكتبة:[نسخة تجريبية مجانية](https://releases.aspose.com/).
### هل أحتاج إلى Visual Studio لتشغيل هذا الكود؟
على الرغم من أنه يوصى به بشدة بسبب ميزاته سهلة الاستخدام، فإن أي C# IDE سوف يقوم بالمهمة طالما أنه يدعم تطوير .NET.
### أين يمكنني العثور على المزيد من الأمثلة والوثائق؟
 يمكنك استكشاف[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) لمزيد من الأمثلة والشروحات المتعمقة.
### كيف يمكنني حل المشكلات أثناء استخدام Aspose.Cells؟
 ينبغي عليك زيارة[منتدى دعم Aspose](https://forum.aspose.com/c/cells/9) للحصول على المساعدة من المجتمع وموظفي دعم Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
