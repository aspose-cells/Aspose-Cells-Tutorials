---
category: general
date: 2026-06-21
description: كيفية استخدام Excel للدمج البريدي مع C#. تعلم إضافة علامة الفتح إلى الخلية،
  بناء القوالب، وإنشاء ملفات مدمجة في دقائق.
draft: false
keywords:
- how to use excel for mail merge
- add opening tag to cell
- excel mail merge c#
- c# asp.net mail merge
- generate excel templates programmatically
language: ar
og_description: كيف تستخدم Excel للدمج البريدي؟ يوضح لك هذا الدليل كيفية إضافة علامة
  افتتاحية إلى الخلية، وإنشاء قالب، وتشغيل الدمج باستخدام C#.
og_title: كيفية استخدام Excel للدمج البريدي – دليل C# خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use Excel for mail merge with C#. Learn to add opening tag to
    cell, build templates, and generate merged files in minutes.
  headline: How to Use Excel for Mail Merge – Complete C# Guide
  type: TechArticle
tags:
- Excel
- Mail Merge
- C#
- Aspose.Cells
title: كيفية استخدام Excel للدمج البريدي – دليل C# الكامل
url: /ar/net/templates-reporting/how-to-use-excel-for-mail-merge-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم Excel للدمج البريدي – دليل C# كامل

هل تساءلت يومًا **كيف تستخدم Excel للدمج البريدي** دون فتح Excel يدويًا في كل مرة؟ لست وحدك. في العديد من لوحات التحكم المؤسسية نحتاج إلى رش البيانات في جدول مُنسق مسبقًا، ثم إرسال النتيجة إلى عميل أو نظام تقارير. الخبر السار؟ ببضع أسطر من C# يمكنك تحويل مصنف فارغ إلى قالب دمج بريدي كامل المميزات وتترك المحرك يقوم بالعمل الشاق.

في هذا البرنامج التعليمي سنستعرض خطوة بخطوة **كيف تستخدم Excel للدمج البريدي** باستخدام مكتبة Aspose.Cells. سنغطي أيضًا الخطوة التي تُهمل غالبًا وهي **إضافة وسم الفتح إلى الخلية**، والتي تُعد المفتاح لتضمين مجموعات مثل الأقسام → الموظفين. بنهاية الدليل ستحصل على مشروع جاهز للتنفيذ ينتج `output.xlsx` من ملف `template.xlsx`.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث (الكود يعمل على .NET Core و .NET Framework)
- Visual Studio 2022 أو أي محرر تفضله
- حزمة NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- مجلد باسم `YOUR_DIRECTORY` (أو غيّر المسارات في الكود)

لا توجد تبعيات أخرى مطلوبة، والمثال يعمل على Windows أو Linux أو macOS.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

إنشاء تطبيق console جديد سهل للغاية:

```bash
dotnet new console -n ExcelMailMergeDemo
cd ExcelMailMergeDemo
dotnet add package Aspose.Cells
```

الآن افتح `Program.cs` وأضف عبارات `using` اللازمة:

```csharp
using System;
using Aspose.Cells;
```

> **نصيحة محترف:** إذا كنت تستخدم Visual Studio، سيقترح IDE إضافة الـ `using` تلقائيًا عندما تكتب `Workbook`.

## الخطوة 2: تحميل المصنف الذي سيحتوي القالب

أول ما تحتاج إلى القيام به عندما **تضيف وسم الفتح إلى الخلية** هو تحميل مصنف في الذاكرة. سيصبح هذا المصنف لاحقًا القالب لمحرك الدمج البريدي.

```csharp
// Step 1: Load the workbook that will contain the template
Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");
```

إذا لم يكن `template.xlsx` موجودًا بعد، سيقوم Aspose.Cells بإنشاء مصنف جديد فارغ لك. هذا مفيد للتجارب السريعة.

## الخطوة 3: الوصول إلى ورقة العمل المستهدفة

معظم القوالب توجد في الورقة الأولى، لكن يمكنك استهداف أي فهرس. هنا نأخذ الورقة الأولى:

```csharp
// Step 2: Access the first worksheet where the template will be placed
Worksheet ws = workbook.Worksheets[0];
```

تذكر أن أوراق العمل تبدأ من الصفر، لذا `[0]` هو أول تبويب تراه في Excel.

## الخطوة 4: **إضافة وسم الفتح إلى الخلية** – بدء مجموعة الأصل

وسوم الدمج البريدي تتبع صيغة Mustache/Handlebars (`{{#Collection}}`). لإخبار المحرك بأن مجموعة من الأقسام ستبدأ، نكتب وسم الفتح في خلية:

```csharp
// Step 3: Insert the opening tag for the parent collection (Departments)
ws.Cells["A1"].PutValue("{{#Departments}}");
```

لماذا نضعه في `A1`؟ لأننا نريد أن يكون الوسم أول شيء يقرأه المحرك. يمكنك اختيار أي خلية، لكن إبقاء الوسوم في الأعلى يجعل القالب أسهل للقراءة.

## الخطوة 5: إدراج عنصر نائب لاسم القسم

الآن نحتاج إلى موضع يظهر فيه اسم كل قسم أثناء الدمج:

```csharp
// Step 4: Add a placeholder for the department name
ws.Cells["A2"].PutValue("Dept: {{Name}}");
```

ستُستبدل العلامة `{{Name}}` بخصائص `Name` لكل كائن `Department` تمرره إلى المحرك.

## الخطوة 6: **إضافة وسم الفتح إلى الخلية** – بدء المجموعة المتداخلة

غالبًا ما يحتوي الأقسام على العديد من الموظفين. لتكرارهم نفتح مجموعة متداخلة مباشرة بعد اسم القسم:

```csharp
// Step 5: Mark the start of the nested collection (Employees) inside each department
ws.Cells["A3"].PutValue("{{#Employees}}");
```

لاحظ أننا مرة أخرى **نضيف وسم الفتح إلى الخلية**—هذه المرة الوسم هو `{{#Employees}}`. التداخل يعمل لأن المحرك يحتفظ بستاك من الوسوم المفتوحة.

## الخطوة 7: إدراج عناصر نائب لتفاصيل الموظف

عادةً ما يكون لكل موظف اسم أول واسم عائلة. لنضيف سطرًا واحدًا سيتكرر لكل موظف:

```csharp
// Step 6: Insert placeholders for employee details
ws.Cells["A4"].PutValue("{{FirstName}} {{LastName}}");
```

يمكنك إضافة أعمدة أخرى (مثل `{{Title}}`، `{{Salary}}`) دون تغيير المنطق؛ فقط ضعها في خلايا متجاورة.

## الخطوة 8: إغلاق المجموعات المتداخلة والأساسية

كل وسم فتح يحتاج إلى نظيره من إغلاق. نغلق مجموعة `Employees` أولاً، ثم مجموعة `Departments`:

```csharp
// Step 7: Close the nested collection and then the parent collection
ws.Cells["A5"].PutValue("{{/Employees}}");
ws.Cells["A6"].PutValue("{{/Departments}}");
```

إذا نسيت وسم إغلاق، سيتسبب الدمج في استثناء—سنتناول ذلك في قسم “المشكلات الشائعة”.

## الخطوة 9: حفظ القالب جاهزًا للدمج

في هذه المرحلة يحمل المصنف قالبًا مكتملًا. احفظه حتى يتمكن معالج الدمج البريدي من استخدامه لاحقًا:

```csharp
// Step 8: Save the workbook with the template ready for mail‑merge processing
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

الآن لديك `output.xlsx` يحتوي فقط على الوسوم. في بيئة الإنتاج ستحافظ على هذا الملف منفصلًا وتستخدمه كقالب قابل لإعادة الاستخدام.

## الخطوة 10: تشغيل الدمج البريدي (اختياري لكن مُوصى به)

إذا أردت رؤية الخط بأكمله يعمل، أنشئ نموذج بيانات بسيط واستدعِ عملية الدمج:

```csharp
// Define data models
public class Department
{
    public string Name { get; set; }
    public Employee[] Employees { get; set; }
}

public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

// Build sample data
var data = new[]
{
    new Department
    {
        Name = "Sales",
        Employees = new[]
        {
            new Employee { FirstName = "Alice", LastName = "Anderson" },
            new Employee { FirstName = "Bob", LastName = "Brown" }
        }
    },
    new Department
    {
        Name = "Engineering",
        Employees = new[]
        {
            new Employee { FirstName = "Charlie", LastName = "Clark" },
            new Employee { FirstName = "Dana", LastName = "Doe" }
        }
    }
};

// Load the template we just saved
Workbook template = new Workbook("YOUR_DIRECTORY/output.xlsx");

// Perform the mail merge
template.Worksheets[0].MailMerge.ExecuteTemplate(data);

// Save the merged result
template.Save("YOUR_DIRECTORY/merged_result.xlsx");
```

تشغيل هذا المقتطف ينتج `merged_result.xlsx` حيث يظهر كل قسم وموظفيه بالترتيب المحدد في مصفوفة البيانات.

### النتيجة المتوقعة

| A (merged) |
|------------|
| Dept: Sales |
| Alice Anderson |
| Bob Brown |
| Dept: Engineering |
| Charlie Clark |
| Dana Doe |

إذا فتحت الملف في Excel سترى بالضبط ما تصفه الوسوم.

## المشكلات الشائعة وحالات الحافة

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **فقدان وسم الإغلاق** (`{{/Employees}}` أو `{{/Departments}}`) | المحرك يتوقع ستاك وسوم متوازن. | تأكد من أن كل `{{#…}}` له وسم إغلاق مطابق `{{/…}}`. |
| **وضع الوسم في خلية مدمجة** | الخلايا المدمجة قد تشوش المحلل لأن عنوان الخلية الأساسي يتغير. | احتفظ بالوسوم في خلايا بسيطة غير مدمجة (A1‑A6 في مثالنا). |
| **مجموعات بيانات كبيرة** | عرض آلاف الصفوف قد يستهلك الذاكرة. | استخدم `MailMerge.ExecuteTemplate` مع `SaveOptions` التي تبث البيانات إلى القرص. |
| **تخطيط ورقة مختلف** | إذا كان قالبك يستخدم ترتيب أوراق مختلف، لا يزال الكود يشير إلى `[0]`. | استخرج الورقة بالاسم: `workbook.Worksheets["Template"]`. |
| **حروف خاصة في البيانات** | حروف مثل `{` أو `}` داخل البيانات تكسر صيغة الوسم. | قم بتهريبها أو استخدم صيغة عنصر نائب مختلفة (`[[FirstName]]`). |

## نصائح لتجربة سلسة

- **نصيحة محترف:** ضع جميع الوسوم في العمود **A** ودع باقي الأعمدة تحمل محتوى ثابت (عناوين، صيغ، تنسيقات). هذا الفصل يجعل القالب أسهل للصيانة.
- **احذر من:** إذا احتجت أقسامًا شرطية (`{{#if …}}`)، يدعم Aspose.Cells الوسوم الشرطية الأساسية، لكن يجب أيضًا **إضافة وسم الفتح إلى الخلية** بنفس الطريقة.
- **فحص الإصدار:** الكود أعلاه يستخدم Aspose.Cells 23.9.0. قد تُدخل الإصدارات الأحدث تغييرات طفيفة في الـ API، لذا راجع ملاحظات الإصدار دائمًا.

## نظرة بصرية

![قالب مثال دمج بريدي في Excel يوضح كيفية استخدام Excel للدمج البريدي](/images/excel-mail-merge-template.png){: .center alt="قالب مثال دمج بريدي في Excel يوضح كيفية استخدام Excel للدمج البريدي"}

لقطة الشاشة (النص البديل يتضمن الكلمة المفتاحية الأساسية) تُظهر الموضع الدقيق للوسوم في الخلايا A1‑A6.

## الخلاصة

ها أنت ذا—مثال كامل قابل للتنفيذ يوضح **كيف تستخدم Excel للدمج البريدي** من البداية إلى النهاية، ويظهر لك بالضبط كيف **تضيف وسم الفتح إلى الخلية** لـ


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)
- [How to Add Borders to Excel Cells Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/formatting/add-borders-excel-cells-aspose-cells-dotnet/)
- [How to Add Page Breaks in Excel Using Aspose.Cells for .NET - A Comprehensive Guide](/cells/english/net/headers-footers/aspose-cells-net-add-page-breaks-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}