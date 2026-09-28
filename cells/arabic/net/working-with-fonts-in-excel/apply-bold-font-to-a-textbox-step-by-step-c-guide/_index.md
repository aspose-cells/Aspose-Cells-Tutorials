---
category: general
date: 2026-03-29
description: تطبيق الخط العريض على مربع النص بسرعة. تعلّم كيفية تعيين نص مربع النص،
  وتعيين خط مربع النص، وجعل النص عريضًا في C# مع أمثلة واضحة.
draft: false
keywords:
- apply bold font
- set textbox text
- how to set font
- how to make bold
- set textbox font
language: ar
og_description: تطبيق خط غامق على مربع نص في C#. يوضح هذا الدليل كيفية تعيين نص مربع
  النص، وتعيين الخط، وجعل النص غامقًا مع مثال كامل قابل للتنفيذ.
og_title: تطبيق الخط العريض على مربع النص – دليل C# الكامل
tags:
- C#
- UI development
- GridJs
title: تطبيق الخط العريض على مربع النص – دليل C# خطوة بخطوة
url: /ar/net/working-with-fonts-in-excel/apply-bold-font-to-a-textbox-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق خط عريض على مربع النص – دليل C# كامل

هل احتجت يوماً إلى **تطبيق خط عريض** على مربع نص لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من أطر واجهة المستخدم يبدو الـ API مشتتًا قليلًا، وكلمة “عريض” قد تُخفى خلف خصائص مثل `Bold`، `Weight`، أو حتى تعداد `FontStyle` منفصل.  

الخبر السار هو أنه ببضع أسطر من C# يمكنك تعيين نص مربع النص، اختيار خط، وجعل ذلك النص عريضًا—كل ذلك في كتلة واحدة مرتبة. أدناه سترى بالضبط **كيفية تطبيق خط عريض** على `GridJsTextbox`، لماذا كل خاصية مهمة، وعينة جاهزة للتنفيذ يمكنك إضافتها إلى مشروعك.

## ما يغطيه هذا الدرس

- كيفية **تعيين نص مربع النص** وربطه بحاوية واجهة المستخدم.  
- الطريقة الصحيحة **لتعيين خط مربع النص** باستخدام كائن `GridJsFont`.  
- الخطوات الدقيقة **لتطبيق خط عريض** لجعل النص يبرز.  
- معالجة الحالات الخاصة (مثال: ماذا لو لم تكن عائلة الخط مثبتة).  
- مقتطف شفرة كامل وجاهز للترجمة يمكنك اختباره اليوم.

لا تحتاج إلى مكتبات خارجية بخلاف مجموعة أدوات UI الافتراضية `GridJs`، والشروحات مفصلة عمدًا لتفهم “السبب” وراء كل سطر.

---

## كيفية تطبيق خط عريض على مربع النص (الخطوة 1)

### تعريف نمط الخط

الأمر الأول الذي تحتاجه هو مثال `GridJsFont` يصف الحجم، العائلة، **والعِرض**. ضبط `Bold = true` يخبر محرك العرض برسم الأحرف بوزن أثقل.

```csharp
// Step 1: Define the font style for the textbox
var noteFont = new GridJsFont
{
    Size   = 12,          // Font size in points – 12 is a comfortable default
    Family = "Arial",    // Choose a widely‑available family; you can swap this out
    Bold   = true        // This flag makes the text appear bold
};
```

> **لماذا هذا مهم:**  
> - `Size` يتحكم في قابلية القراءة؛ إذا كان صغيرًا جدًا سيحكم المستخدمون.  
> - `Family` يضمن التناسق عبر الأنظمة.  
> - `Bold` هو الخاصية التي **تطبق الخط العريض** فعليًا؛ بدونها سيظهر النص بشكل عادي.

---

## تعيين نص مربع النص وربط الخط (الخطوة 2)

الآن بعد أن الخط جاهز، أنشئ مربع النص، أعطه **النص** المطلوب، واربطه بـ `noteFont` الذي أنشأته للتو.

```csharp
// Step 2: Create the textbox and assign its text and font
var noteTextbox = new GridJsTextbox
{
    Text = "Note",   // This is the content the user will see
    Font = noteFont  // Linking the bold font we defined above
};
```

> **نصيحة:** إذا كنت تحتاج إلى جعل مربع النص قابلًا للتحرير لاحقًا، اضبط `IsReadOnly = false`. بشكل افتراضي معظم مجموعات أدوات UI تعتبر مربع النص قابلًا للتحرير، لكن بعض المكتبات تتطلب علمًا صريحًا.

---

## إضافة مربع النص إلى حاوية UI (الخطوة 3)

مربع النص بمفرده لا يظهر حتى يُوضع داخل حاوية بصرية—فكر في `Grid` أو `StackPanel` أو أي عنصر تخطيط آخر. أدناه نافذة بسيطة تستضيف مربع النص.

```csharp
using System;
using GridJs;               // Hypothetical UI namespace

namespace BoldFontDemo
{
    class Program
    {
        static void Main()
        {
            // Create a window (or any container your framework provides)
            var window = new GridJsWindow
            {
                Title = "Bold Font Demo",
                Width = 300,
                Height = 150
            };

            // Add the textbox we prepared earlier
            window.Content = noteTextbox;

            // Show the window – this call blocks until the user closes it
            window.ShowDialog();
        }
    }
}
```

> **النتيجة المتوقعة:**  
> عند تشغيل البرنامج، تظهر نافذة صغيرة تعرض كلمة **“Note”** بخط **Arial، 12 pt، عريض**. يجب أن يكون النص أثقل بوضوح من عناصر UI المحيطة، مما يؤكد أن **تطبيق خط عريض** نجح كما هو مقصود.

---

## تنويعات شائعة وحالات خاصة

### تغيير عائلة الخط ديناميكيًا

إذا أردت السماح للمستخدمين باختيار خط مختلف أثناء التشغيل، استبدل ببساطة `Family` في كائن `GridJsFont` الحالي وأعد ربطه بمربع النص.

```csharp
noteFont.Family = "Calibri";
noteTextbox.Font = noteFont;   // Refresh the textbox with the new font
```

> **احذر:** بعض الخطوط لا تدعم الوزن العريض. في هذه الحالة قد يقوم UI بإنشاء نمط عريض اصطناعي، مما قد يبدو غير واضح. اختبر دائمًا مع عائلة الخط المستهدفة.

### جعل النص عريضًا بدون خاصية `Bold` مخصصة

تُظهر بعض الـ APIs الوزن عبر عدد صحيح (مثال: `Weight = 700`). إذا صادفت مثل هذه الـ API، قم بربط المفهوم وفقًا لذلك:

```csharp
var legacyFont = new GridJsFont
{
    Size   = 12,
    Family = "Arial",
    Weight = 700   // 700 typically corresponds to “Bold”
};
```

### تعيين النص برمجيًا بعد الإنشاء

أحيانًا يتغير محتوى النص بعد أن تُرسم الواجهة (مثال: استجابةً لإدخال المستخدم). يمكنك تحديثه بأمان:

```csharp
noteTextbox.Text = "Updated Note";
```

يبقى نمط العريض ثابتًا لأن كائن `Font` لا يزال مرتبطًا.

---

## نصائح احترافية لواجهة مصقولة

- **نصيحة احترافية:** استخدم `Padding` أو `Margin` على مربع النص لتجنب ملامسة النص لحواف الحاوية.  
- **احذر من:** الشاشات ذات الدقة العالية (High‑DPI)؛ قد تحتاج إلى تعديل `Size` بناءً على إعدادات DPI للنظام.  
- **ملاحظة أداء:** إعادة استخدام كائن `GridJsFont` واحد عبر عدة مربعات نص يقلل من استهلاك الذاكرة.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

أدناه البرنامج بالكامل—ما عليك سوى نسخه إلى مشروع كونسول جديد، إضافة مرجع لمكتبة `GridJs`، والضغط على **Run**.

```csharp
using System;
using GridJs;   // Replace with the actual namespace of your UI toolkit

namespace BoldFontDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Define the font style (apply bold font)
            var noteFont = new GridJsFont
            {
                Size   = 12,
                Family = "Arial",
                Bold   = true
            };

            // Step 2: Create the textbox with text and font
            var noteTextbox = new GridJsTextbox
            {
                Text = "Note",
                Font = noteFont
            };

            // Step 3: Host the textbox inside a window
            var window = new GridJsWindow
            {
                Title   = "Bold Font Demo",
                Width   = 300,
                Height  = 150,
                Content = noteTextbox
            };

            // Show the UI – blocks until closed
            window.ShowDialog();
        }
    }
}
```

**النتيجة:** تظهر نافذة بحجم 300 × 150 بكسل بعنوان *Bold Font Demo*، تعرض كلمة **Note** بخط Arial 12 pt عريض.  

لا تتردد في استبدال `"Note"` بأي سلسلة، تعديل `Size`، أو تغيير `Family`—سيتبع نمط العريض التغييرات تلقائيًا.

---

## الخلاصة

الآن تعرف بالضبط كيف **تطبق خط عريض** على `GridJsTextbox`، وكيف **تعيّن نص مربع النص**، والطريقة الصحيحة **لتعيين خط مربع النص** للحصول على مظهر UI متسق. عبر تعريف `GridJsFont` بـ `Bold = true`، ربطه بمربع النص، ووضع التحكم داخل حاوية، ستحصل على تسمية نظيفة وعريضة في ثلاث خطوات مختصرة فقط.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذه التقنية مع:

- **اختيار خط ديناميكي** (`how to set font` أثناء التشغيل).  
- **تطبيق عريض مشروط** (`how to make bold` فقط عندما يتحقق شرط).  
- **تنسيق عدة عناصر** (`set textbox font` لنموذج كامل).

جرّب، كرّر، ودع واجهتك تتحدث بصوت أعلى باستخدام النص العريض حيثما كان ذلك مهمًا. برمجة سعيدة!  

![لقطة شاشة لنافذة تعرض مربع نص بخط عريض “Note” – مثال تطبيق خط عريض](https://example.com/images/bold-font-textbox.png "مثال تطبيق خط عريض")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}