---
category: general
date: 2026-03-21
description: تعلم كيفية حفظ ملفات xlsb في C# مع إضافة خاصية مخصصة مثل ProjectId. يوضح
  هذا الدليل كيفية إنشاء مصنف Excel، إضافة الخاصية المخصصة، والتحقق منها.
draft: false
keywords:
- how to save xlsb
- add custom property
- create excel workbook
- how to add custom property
- add project id
language: ar
og_description: اكتشف كيفية حفظ ملفات xlsb وإضافة خاصية مخصصة مثل ProjectId باستخدام C#.
  دليل خطوة بخطوة مع الشيفرة الكاملة.
og_title: كيفية حفظ XLSB – إضافة خاصية مخصصة في C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: كيفية حفظ ملف XLSB – إضافة خاصية مخصصة في C#
url: /ar/net/document-properties/how-to-save-xlsb-add-custom-property-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ XLSB – إضافة خاصية مخصصة في C#

هل تساءلت يومًا **كيفية حفظ xlsb** الملفات مع تضمين قطعة من البيانات الوصفية داخلها؟ ربما تكون تبني محرك تقارير يحتاج إلى معرف ProjectId مخفي، أو ربما تريد فقط وضع علامة على أوراق العمل لمعالجة لاحقة. **كيفية حفظ xlsb** ليست علم صواريخ، لكن دمجها مع خاصية مخصصة يضيف لمسة بسيطة يتغاضى عنها كثير من المطورين.

في هذا الدرس سنستعرض إنشاء مصنف Excel، إضافة خاصية مخصصة (نعم، *add custom property*)، حفظ الملف كمصنف **XLSB** ثنائي، وأخيرًا تحميله مرة أخرى لإثبات بقاء الخاصية. على طول الطريق سنتطرق أيضًا إلى **كيفية إضافة خاصية مخصصة** مثل قيمة ProjectId، بحيث تحصل على نمط قابل لإعادة الاستخدام في المشاريع المستقبلية.

> **نصيحة احترافية:** إذا كنت تستخدم مكتبة Aspose.Cells بالفعل (الكود أدناه يفعل ذلك)، ستحصل على دعم أصلي للخصائص المخصصة دون أي مشاكل في COM interop.

---

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.6+).  
- Aspose.Cells for .NET – تثبيت عبر NuGet: `Install-Package Aspose.Cells`.  
- معرفة أساسية بـ C# – لا شيء معقد، فقط بضع عبارات `using`.  

هذا كل شيء. لا تحتاج إلى تثبيت Office، ولا إلى interop، فقط كود مُدار نقي.

## الخطوة 1: كيفية حفظ XLSB – إنشاء مصنف Excel

أول شيء تحتاج إلى القيام به هو إنشاء كائن مصنف جديد. فكر فيه كفتح ملف Excel فارغ يعيش فقط في الذاكرة حتى تقرر كتابته إلى القرص.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // (Optional) Give the first worksheet a friendly name
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Name = "DataSheet";

        // From here we can start adding data or properties…
```

لماذا نبدأ بمصنف؟ لأن **create excel workbook** هو الأساس لأي تعديل لاحق—سواء أضفت صيغًا، رسومًا بيانية، أو خصائص مخصصة. فئة `Workbook` تمثل الملف بأكمله، بينما توفر `Worksheets` الوصول إلى الأوراق الفردية.

## الخطوة 2: إضافة خاصية مخصصة إلى ورقة العمل

الآن يأتي الجزء الممتع—**add custom property**. في Aspose.Cells يمكنك إرفاق خاصية مباشرةً إلى ورقة العمل (أو إلى المصنف نفسه). هنا سنخزن معرف ProjectId رقمي يمكن للخدمات اللاحقة قراءته دون لمس الخلايا الظاهرة.

```csharp
        // Step 2: Add a custom property called "ProjectId"
        // The value 12345 could come from your database, config, etc.
        sheet.CustomProperties.Add("ProjectId", 12345);

        // You can also add string or date properties:
        // sheet.CustomProperties.Add("Author", "Jane Doe");
        // sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);
```

**كيفية إضافة خاصية مخصصة**؟ فقط استدعِ `CustomProperties.Add(name, value)`. الـ API يتعامل تلقائيًا مع XML الداخلي، لذا لا تحتاج للقلق بشأن التفاصيل منخفضة المستوى. هذه هي الطريقة الأكثر أمانًا لتضمين بيانات وصفية غير مرئية للمستخدم النهائي.

## الخطوة 3: حفظ المصنف كـ XLSB

مع جاهزية المصنف وإرفاق الخاصية المخصصة، حان الوقت لـ **how to save xlsb**. تنسيق XLSB يخزن البيانات في تمثيل ثنائي، عادةً ما يكون أصغر وأسرع في الفتح مقارنةً بـ XLSX الكلاسيكي.

```csharp
        // Step 3: Define the output path – adjust as needed
        string outputPath = @"C:\Temp\WithCustomProp.xlsb";

        // Save the workbook in XLSB format
        workbook.Save(outputPath, SaveFormat.Xlsb);

        Console.WriteLine($"Workbook saved to {outputPath}");
```

الحفظ كـ XLSB بسيط مثل تمرير `SaveFormat.Xlsb` إلى طريقة `Save`. إذا كنت تتساءل ما إذا كان سيزيل الخاصية المخصصة—اطمئن، Aspose.Cells يحافظ على خصائص مستوى المصنف ومستوى ورقة العمل في الملف الثنائي.

## الخطوة 4: التحقق من الخاصية المخصصة

عادة جيدة هي إعادة تحميل الملف والتأكد من بقاء الخاصية بعد الجولة. هذا أيضًا يوضح **كيفية إضافة خاصية مخصصة** لاحقًا إذا احتجت لتحديثها.

```csharp
        // Step 4: Load the saved XLSB to verify the property
        Workbook loaded = new Workbook(outputPath);

        // Retrieve the first worksheet again
        Worksheet loadedSheet = loaded.Worksheets[0];

        // Access the "ProjectId" custom property
        var projectId = loadedSheet.CustomProperties["ProjectId"].Value;

        Console.WriteLine($"Loaded ProjectId: {projectId}"); // Should print 12345
    }
}
```

إذا طبع الطرفية `12345`، فقد نجحت في **how to save xlsb** *و* **add project id** في خطوة واحدة. الخاصية تعيش داخل البيانات الوصفية الداخلية للملف، غير مرئية للواجهة لكن قابلة للقراءة تمامًا عبر الكود.

## نصائح إضافية: إضافة خصائص متعددة وحالات الحافة

### إضافة أكثر من خاصية واحدة

يمكنك تجميع عدد غير محدود من الخصائص كما تشاء:

```csharp
sheet.CustomProperties.Add("Department", "Finance");
sheet.CustomProperties.Add("IsConfidential", true);
```

### تحديث خاصية موجودة

إذا كانت الخاصية موجودة بالفعل، فقط عيّن قيمة جديدة:

```csharp
sheet.CustomProperties["ProjectId"].Value = 67890; // Overwrites the old ID
```

### التعامل مع الخصائص المفقودة

محاولة قراءة خاصية غير موجودة تُلقي استثناء `KeyNotFoundException`. احمِ نفسك من ذلك:

```csharp
if (sheet.CustomProperties.ContainsKey("ClientCode"))
{
    var clientCode = sheet.CustomProperties["ClientCode"].Value;
    // Use clientCode...
}
else
{
    Console.WriteLine("ClientCode property not found.");
}
```

### التوافق عبر الإصدارات

يعمل XLSB على Excel 2007 + وعلى نسخة الويب من Excel. ومع ذلك، الإصدارات القديمة من Office (< 2007) لا يمكنها فتح ملفات XLSB. إذا كنت تحتاج إلى توافق أوسع، فكر في حفظ نسخة ثانية كـ XLSX.

### اعتبارات الأداء

ملفات XLSB الثنائية عادةً أصغر بنسبة 30‑50 % مقارنةً بـ XLSX، وتُحمَّل أسرع. بالنسبة لمجموعات البيانات الكبيرة (مئات الآلاف من الصفوف)، يمكن أن يكون تحسين السرعة ملحوظًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم. يتضمن جميع الخطوات، معالجة الأخطاء، والتعليقات التي تحتاجها لتبدأ العمل فورًا.

```csharp
using Aspose.Cells;
using System;

class SaveXlsbWithCustomProperty
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "DataSheet";

            // 2️⃣ Add a custom property (ProjectId) – this is how to add custom property
            sheet.CustomProperties.Add("ProjectId", 12345);
            sheet.CustomProperties.Add("CreatedBy", Environment.UserName);
            sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);

            // 3️⃣ Save as XLSB – this shows how to save xlsb
            string path = @"C:\Temp\WithCustomProp.xlsb";
            workbook.Save(path, SaveFormat.Xlsb);
            Console.WriteLine($"✅ Workbook saved as XLSB to {path}");

            // 4️⃣ Load the file back and verify the property
            Workbook loaded = new Workbook(path);
            Worksheet loadedSheet = loaded.Worksheets[0];

            if (loadedSheet.CustomProperties.ContainsKey("ProjectId"))
            {
                var projId = loadedSheet.CustomProperties["ProjectId"].Value;
                Console.WriteLine($"🔎 Loaded ProjectId: {projId}"); // Expected: 12345
            }
            else
            {
                Console.WriteLine("❗ ProjectId not found after loading.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع**

```
✅ Workbook saved as XLSB to C:\Temp\WithCustomProp.xlsb
🔎 Loaded ProjectId: 12345
```

إذا رأيت ما سبق، فقد أتقنت **how to save xlsb**، **add custom property**، و **add project id**—كل ذلك في مقتطف منظم وقابل لإعادة الاستخدام.

## الأسئلة المتكررة

**س: هل يعمل هذا مع .NET Core؟**  
ج: بالتأكيد. Aspose.Cells متوافق مع .NET Standard، لذا يعمل نفس الكود على .NET 5/6/7 وعلى .NET Framework.

**س: هل يمكنني إضافة خاصية مخصصة إلى كامل المصنف بدلاً من ورقة واحدة؟**  
ج: نعم. استخدم `workbook.CustomProperties.Add("Key", value);` لإرفاقها على مستوى المصنف.

**س: ماذا لو احتجت لتخزين سلسلة نصية طويلة (مثل JSON) كخاصية؟**  
ج: الـ API يقبل سلاسل بأي طول، لكن ضع في اعتبارك أن الكتل الكبيرة قد تزيد من حجم الملف. للبيانات الضخمة، فكر في ورقة مخفية بدلاً من ذلك.

**س: هل الخاصية المخصصة مرئية في واجهة Excel؟**  
ج: ليست مباشرة. يمكن للمستخدمين رؤيتها عبر **File → Info → Properties → Advanced Properties → Custom**، لكنها لن تظهر في الجدول.

## الخلاصة

لقد غطينا **how to save xlsb** الملفات في C# مع **إضافة خاصية مخصصة** مثل ProjectId. باتباع نمط الخطوة‑ب‑خطوة—**create excel workbook**، **add custom property**، **save as XLSB**، و **verify**—أصبح لديك مرجع قوي وجدير بالاستشهاد يعمل لكل من محركات البحث ومساعدي الذكاء الاصطناعي.

بعد ذلك، قد تستكشف:

- **How to add custom property** إلى عدة أوراق عمل داخل حلقة.  
- تصدير البيانات من DataTable إلى المصنف قبل الحفظ.  
- تشفير ملف XLSB لمزيد من الأمان.

لا تتردد في التجربة، تعديل أسماء الخصائص، أو استبدال التنسيق الثنائي بـ XLSX إذا كنت تحتاج إلى توافق أوسع. هل لديك سيناريو معقد؟ اترك تعليقًا، وسنحل المشكلة معًا. برمجة سعيدة!  

![how to save xlsb example](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}