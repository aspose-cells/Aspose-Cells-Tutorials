---
"description": "تعلّم كيفية نسخ مُصمّم نماذج مستخدم ماكرو VBA بكفاءة في Aspose.Cells لـ .NET من خلال برنامجنا التعليمي الشامل خطوة بخطوة! أطلق العنان لإمكانيات Excel."
"linktitle": "نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells"
"url": "/ar/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# نسخ مساحة تخزين مصمم نماذج مستخدم VBAMacro إلى مصنف باستخدام Aspose.Cells

## مقدمة
أهلاً بك! إذا كنت ترغب في تحسين تجربة استخدامك لبرنامج Excel باستخدام وحدات ماكرو VBA ونماذج المستخدم، فأنت في المكان المناسب! في هذا الدليل، نتعمق في كيفية نسخ مُصمم نماذج المستخدم VBA Macro UserForm بسهولة من مصنف إلى آخر باستخدام Aspose.Cells لـ .NET. سواءً كنت مطورًا محترفًا أو مبتدئًا، سنرشدك خلال كل خطوة مهمة. اعتبر هذا دليلك لإتقان فن التعامل مع ملفات Excel برمجيًا. هل أنت مستعد للبدء؟ هيا بنا!
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة للترميز، دعنا نتأكد من أن لديك كل ما تحتاجه:
1. بيئة تطوير C#: يجب أن تكون لديك بيئة عمل جاهزة لتطوير C#. يُنصح بشدة باستخدام Visual Studio.
2. مكتبة Aspose.Cells لـ .NET: تأكد من دمج مكتبة Aspose.Cells في مشروعك. يمكنك بسهولة [قم بتحميله هنا](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بـ VBA ووحدات الماكرو في Excel: إن الفهم الجيد لـ VBA وكيفية عمل وحدات الماكرو في Excel سيساعدك على التنقل عبر هذا البرنامج التعليمي بسهولة.
4. ملف Excel يحتوي على نموذج مستخدم: للتجربة أو إنشاء أو الحصول على مصنف Excel يحتوي على نموذج مستخدم، ويفضل أن يكون مع تمكين وحدات الماكرو (مثل `.xlsm` الملفات).
## استيراد الحزم
في مشروع C# الخاص بك، ستحتاج إلى استيراد مساحات أسماء معينة في أعلى ملفك للاستفادة من وظائف Aspose.Cells. إليك كيفية القيام بذلك:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
يتيح لك تضمين هذه المساحات الأسماء الوصول إلى جميع الأدوات القوية المضمنة في مكتبة Aspose.Cells. 
بعد أن اكتملت متطلباتنا الأساسية وحزمنا، حان وقت الانتقال إلى الجزء الممتع: البرمجة! لنشرحها خطوة بخطوة.
## الخطوة 1: تحديد دليل المصدر والإخراج
أولاً، عليك تحديد مكان وجود ملفاتك:
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
هنا، استبدل `"Your Document Directory"` مع المسار الفعلي لتخزين ملفاتك. هذا هو المكان الذي سيتم فيه الحصول على مصنف العمل المصدر (مع نموذج المستخدم) ومكان حفظ المصنف الجديد.
## الخطوة 2: إنشاء مصنف هدف فارغ
بعد ذلك، دعنا نقوم بإنشاء مصنف الهدف الذي سنقوم فيه بنسخ نموذج المستخدم والماكرو الخاص بنا:
```csharp
// إنشاء مصنف هدف فارغ
Workbook target = new Workbook();
```
هذا السطر من التعليمات البرمجية يُنشئ مُصنّف عمل جديد فارغًا لنملأه بالبيانات. تخيّلها كلوحة فارغة لتحفتك الفنية!
## الخطوة 3: تحميل مصنف القالب الخاص بك
نحن بحاجة إلى تحميل المصنف الذي يحتوي على نموذج المستخدم والماكرو الخاص بك:
```csharp
// قم بتحميل ملف Excel الذي يحتوي على نموذج مستخدم VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
تأكد من التغيير `"sampleDesignerForm.xlsm"` إلى اسم ملفك الفعلي. هذا الكتاب يشبه كتاب وصفاتك، فهو مصدر مكوناتنا!
## الخطوة 4: نسخ أوراق العمل إلى المصنف المستهدف
الآن، لنبدأ بنسخ أوراق العمل من قالبنا إلى المصنف المستهدف:
```csharp
// نسخ جميع أوراق عمل القالب إلى المصنف المستهدف
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
في هذه الخطوة، نمرر كل ورقة عمل في القالب وننسخها إلى مصنفنا المستهدف. لو فكرت في الأمر، لوجدت أن الأمر أشبه بنقل أفضل وصفاتك من كتاب طبخ إلى آخر!
## الخطوة 5: نسخ وحدات الماكرو VBA من القالب
بعد ذلك، سنقوم بنسخ وحدات ماكرو VBA، بما في ذلك وحدات UserForm Designer، إلى مصنف العمل الجديد الخاص بنا:
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
        // نسخ كود وبيانات الوحدات النمطية الأخرى
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
            // أضف وحدة تخزين المصمم إلى مشروع Vba المستهدف
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
هذا الجزء الضخم من الكود يتولى فحص كل وحدة VBA في ملف القالب. نقوم بنسخ تصميم UserForm والأكواد المرتبطة به. الأمر أشبه بضمان حصولك ليس فقط على وصفة فطيرة جدتك الشهيرة، بل أيضًا على تقنيات خبزها الدقيقة!
## الخطوة 6: حفظ المصنف المستهدف
بعد أن حققنا جميع النسخ لدينا، حان الوقت لحفظ عملنا الشاق:
```csharp
// حفظ المصنف المستهدف
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
تأكد من تعديل اسم ملف الإخراج حسب الحاجة. بمجرد حفظه، ستُنشئ نسختك المُخصصة من المصنف، مليئةً بوحدات الماكرو ونماذج المستخدم. ما مدى روعة هذا؟
## الخطوة 7: تأكيد النجاح
وأخيرًا، دعنا نطبع رسالة النجاح على وحدة التحكم:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
هذا السطر الصغير يُطمئنك بأن عمليتك سارت بسلاسة. إنه بمثابة الكرز الذي يُزيّن كعكة البرمجة الخاصة بك!
## خاتمة
تهانينا! لقد أكملتَ الدليل خطوة بخطوة لنسخ مُصمم نماذج مستخدم ماكرو VBA من مصنف إلى آخر باستخدام Aspose.Cells لـ .NET. قد يبدو الأمر مُرهقًا بعض الشيء في البداية، ولكن مع الممارسة، ستُتقن التعامل مع المصنفات باحترافية. تذكر أن البرمجة أساسها الممارسة، لذا لا تتردد في تجربة أشياء مختلفة في ملفات Excel. إذا كانت لديك أي أسئلة أو واجهت أي مشاكل، فلا تتردد في زيارة منتديات Aspose أو وثائقها للحصول على الدعم!
## الأسئلة الشائعة
### ما هي إصدارات Excel التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells مجموعة واسعة من تنسيقات Excel بما في ذلك XLSX وXLSM وCSV والمزيد.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم! يمكنك البدء بفترة تجريبية مجانية تتيح لك تقييم المكتبة: [نسخة تجريبية مجانية](https://releases.aspose.com/).
### هل أحتاج إلى Visual Studio لتشغيل هذا الكود؟
على الرغم من أنه يوصى به بشدة بسبب ميزاته سهلة الاستخدام، فإن أي بيئة تطوير متكاملة لـ C# ستفي بالغرض طالما أنها تدعم تطوير .NET.
### أين يمكنني العثور على المزيد من الأمثلة والوثائق؟
يمكنك استكشاف [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) لمزيد من الأمثلة والشروحات المتعمقة.
### كيف يمكنني حل المشكلات أثناء استخدام Aspose.Cells؟
ينبغي عليك زيارة [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9) للحصول على المساعدة من المجتمع وموظفي دعم Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}