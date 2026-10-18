---
category: general
date: 2026-02-14
description: إن إنشاء التسلسل الهرمي في قوالب SmartMarker أسهل مما تظن – تعلم كيفية
  إنشاء بيانات هرمية وكيفية سرد الموظفين بكفاءة.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: ar
og_description: كيفية إنشاء التسلسل الهرمي في قوالب SmartMarker بسيطة. اتبع هذا الدليل
  لإنشاء بيانات هرمية وقائمة الموظفين بنطاقات متداخلة.
og_title: كيفية إنشاء التسلسل الهرمي باستخدام SmartMarker – دليل كامل
tags:
- SmartMarker
- C#
- templating
title: كيفية إنشاء التسلسل الهرمي باستخدام SmartMarker – دليل خطوة بخطوة
url: /ar/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء تسلسل هرمي باستخدام SmartMarker – دليل كامل

هل تساءلت يومًا **كيف تنشئ تسلسلًا هرميًا** داخل قالب SmartMarker دون أن تفقد صبرك؟ لست وحدك. في العديد من سيناريوهات التقارير تحتاج إلى علاقة أب‑ابن—فكر في الأقسام والأشخاص الذين يعملون فيها. الخبر السار هو أن SmartMarker يجعل الأمر سهلًا بمجرد معرفة الخطوات الصحيحة.

في هذا البرنامج التعليمي سنستعرض العملية بالكامل: من **إنشاء بيانات هرمية** في C#، تمكين النطاقات المتداخلة، وأخيرًا عرض قالب **يسرد الموظفين** لكل قسم. في النهاية ستحصل على مثال جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

---

## ما ستحتاجه

- .NET 6+ (أي نسخة حديثة تعمل)
- إشارة إلى مكتبة **SmartMarker** (مساحة الأسماء `ws.SmartMarkerProcessor`)
- معرفة أساسية بـ C# – لا شيء معقد، مجرد بعض الكائنات وتعابير لامبدا قليلة
- بيئة تطوير أو محرر من اختيارك (Visual Studio، Rider، VS Code… إلخ)

إذا كان لديك كل ذلك، رائع—لنبدأ.

---

## نظرة عامة على إنشاء التسلسل الهرمي

الفكرة الأساسية هي بناء **رسم بياني كائنات متداخلة** يعكس البنية التي تريد رؤيتها في المستند النهائي. في حالتنا يبدو الرسم البياني كالتالي:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

يمكن لـ SmartMarker بعد ذلك التكرار على `Departments`، وبما أننا سنفعل **معالجة النطاق المتداخل**، سيتكرر أيضًا على مجموعة `Employees` لكل قسم تلقائيًا.

---

## الخطوة 1: بناء نموذج البيانات الهرمية

أولاً ننشئ كائنًا مجهولًا يحتوي على مصفوفة من الأقسام، كل قسم يحتوي على قائمة موظفيه. استخدام النوع المجهول يبقي المثال خفيفًا—يمكنك استبداله بفئات POCO حقيقية لاحقًا.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **لماذا هذا مهم:** مصفوفة `Departments` هي المجموعة ذات المستوى الأعلى. كل عنصر يحتوي على مصفوفة `Employees`، مما يمنحنا المستوى الثاني من التسلسل الهرمي الذي سنصل إليه لاحقًا باستخدام `#Departments.Employees#`.

---

## الخطوة 2: تمكين معالجة النطاق المتداخل

لن يغوص SmartMarker في المجموعات الداخلية إلا إذا أخبرته بذلك. كائن `SmartMarkerOptions` يحتوي على هذا المفتاح.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **نصيحة احترافية:** إذا نسيت تفعيل هذا العلم، فإن نطاق `#Employees#` الداخلي سيعيد لا شيء، وستتساءل لماذا القالب فارغ.

---

## الخطوة 3: تشغيل المعالج مع بياناتك

الآن نمرر البيانات والخيارات إلى المعالج. المتغير `ws` يمثل **WebService** الخاص بك (أو أي كائن يستضيف محرك SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

في هذه المرحلة يقوم SmartMarker بتحليل القالب، ويستبدل `#Departments.Name#` باسم كل قسم، ثم، لأن النطاقات المتداخلة مفعلة، يتكرر عبر مجموعة `Employees` لكل قسم.

---

## الخطوة 4: صياغة علامات القالب

فيما يلي قالب بسيط يوضح كلًا من الحلقة الخارجية والداخلية. الصقه في محرر قالب SmartMarker (أو ملف `.txt` تمرره إلى المعالج).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

عند العرض ستحصل على:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **ما تراه:** الحلقة الخارجية `#Departments.Name#` تطبع عنوان القسم. كتلة `#Departments.Employees#` الداخلية تتكرر على كل موظف، و`#Departments.Employees#` داخل الكتلة تُخرج الاسم الفعلي.

---

## النتيجة المتوقعة والتحقق

تشغيل المثال الكامل (البيانات + الخيارات + القالب) يجب أن ينتج القائمة المعروضة أعلاه بالضبط. للتحقق السريع، يمكنك طباعة النتيجة إلى وحدة التحكم:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

إذا رأيت عنواني القسمين متبوعين بنقاط الموظفين، فقد نجحت في **إنشاء تسلسل هرمي** و**قائمة الموظفين**.

---

## الأخطاء الشائعة وحالات الحافة

| المشكلة | السبب | الحل |
|-------|--------|------|
| لا يظهر أي إخراج للموظفين | `EnableNestedRange` ترك كـ false | اضبط `EnableNestedRange = true` |
| تكرار أسماء الموظفين | إعادة استخدام نفس المصفوفة عبر الأقسام | استنسخ المصفوفة أو استخدم مجموعات متميزة |
| التسلسلات الهرمية الكبيرة تسبب ضغطًا على الذاكرة | SmartMarker يحمل الرسم البياني بالكامل في الذاكرة | استخدم التدفق (stream) أو قسم المجموعات الكبيرة إلى صفحات |
| أخطاء في صياغة القالب | نسيان إغلاق وسوم `#/…#` | استخدم أداة التحقق من SmartMarker أو جرّب قالبًا صغيرًا سريعًا |

---

## التعمق – تنويعات من العالم الحقيقي

1. **مصادر بيانات ديناميكية** – استخرج الأقسام من قاعدة بيانات واطبقها على الهيكل المجهول باستخدام LINQ.  
2. **تنسيق شرطي** – أضف علم `IsManager` لكل موظف واستخدم وسوم الشرط في SmartMarker (`#if …#`) لتسليط الضوء على المديرين.  
3. **مستويات تداخل متعددة** – إذا احتجت فرق داخل الأقسام، أضف مجموعة أخرى (`Teams`) وابقِ `EnableNestedRange` مفعلة.

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**القالب (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

تشغيل البرنامج سيطبع التسلسل الهرمي تمامًا كما ظهر سابقًا.

---

## الخلاصة

غطينا **كيفية إنشاء تسلسل هرمي** في SmartMarker، من تشكيل **البيانات الهرمية** في C# إلى تفعيل النطاقات المتداخلة وأخيرًا عرض قالب **يسرد الموظفين** لكل قسم. النمط قابل للتوسيع—فقط أضف مجموعات متداخلة أخرى أو منطقًا شرطيًا وستحصل على محرك تقارير قوي بين يديك.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال الأنواع المجهولة بفئات POCO قوية، أو دمج هذا التدفق في نقطة نهاية ASP.NET Core تُعيد ملف PDF أو Word. السماء هي الحد، والآن لديك أساس صلب.

---

![How to create hierarchy diagram](image.png){alt="مخطط إنشاء التسلسل الهرمي يوضح علاقة القسم‑الموظف"}

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أسفل هذه الصفحة—سأكون سعيدًا بالمساعدة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}