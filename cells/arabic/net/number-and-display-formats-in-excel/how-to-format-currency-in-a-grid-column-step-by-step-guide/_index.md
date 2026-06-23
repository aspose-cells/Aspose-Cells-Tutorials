---
category: general
date: 2026-02-15
description: كيفية تنسيق العملة بسرعة باستخدام تعيين تنسيق رقم العمود وتطبيق تنسيق
  رقمي مخصص في C#. تعلم استرجاع العمود بالاسم وتعيين محاذاة عمود الشبكة.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: ar
og_description: كيفية تنسيق العملة في عمود شبكة باستخدام C#. يوضح هذا الدرس كيفية
  استرجاع العمود بالاسم، ضبط تنسيق الأرقام للعمود، تطبيق تنسيق رقمي مخصص، وضبط محاذاة
  عمود الشبكة.
og_title: كيفية تنسيق العملة في عمود الشبكة – دليل شامل
tags:
- C#
- GridFormatting
- UI
title: كيفية تنسيق العملة في عمود الشبكة – دليل خطوة بخطوة
url: /ar/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

what is there.

We need to keep the incomplete part as is? Probably keep as is, but translate the visible text. The bullet list after "If you’re ready to take this further, try:" includes "- **Dynamic cultures** – switch the format string based on the user’s locale.  - **Conditional". The second bullet is incomplete. We'll translate "Dynamic cultures" and "Conditional" maybe keep as is.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنسيق العملة في عمود شبكة – دليل برمجي كامل

هل تساءلت يومًا **كيف تنسق العملة** في عمود شبكة دون أن تفقد أعصابك؟ لست وحدك. عندما تنظر إلى رقم بسيط مثل `1234.5` وتتمنى أن يظهر سحريًا كـ `$1,234.50`، يكون الجواب عادةً بضع أسطر من الإعدادات فقط.  

في هذا الدليل سنقوم **باسترجاع العمود بالاسم**، **بتعيين تنسيق رقم العمود**، و**بتطبيق تنسيق رقمي مخصص** يحترم تنسيق المحاسبة التقليدي. على طول الطريق سنقوم أيضًا **بتعيين محاذاة عمود الشبكة** وإضافة حد رقيق لتبدو الواجهة أكثر صقلًا.

> **TL;DR** – بنهاية هذا الدليل ستحصل على مقتطف جاهز للتنفيذ يحول القيم العشرية الخام إلى قيم عملة منسقة بشكل جميل داخل أي عنصر تحكم من نمط `GridJs`.

---

## ما ستحتاجه

- مشروع .NET (أي نسخة تدعم C# 8.0+ – Visual Studio 2022 يعمل بشكل ممتاز).  
- مكوّن شبكة يُظهر مجموعة `Columns` (المثال يستخدم فئة خيالية `GridJs`، لكن المفاهيم تُطبق على شبكات DevExpress أو Telerik أو Syncfusion).  
- إلمام أساسي بصياغة C# – لا تحتاج إلى حيل متقدمة.

إذا كان لديك كل ذلك، رائع. إذا لم يكن، فقط أنشئ تطبيق Console؛ يمكن محاكاة الشبكة للتوضيح.

---

## تنفيذ خطوة بخطوة

أسفل كل خطوة ستجد كتلة كود مُدمجة، شرحًا قصيرًا **لماذا** السطر مهم، ونصيحة لتجنب الأخطاء الشائعة.

### ## الخطوة 1 – استرجاع عمود “Amount” بالاسم

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**لماذا هذا مهم:**  
معظم واجهات برمجة تطبيقات الشبكات تُظهر الأعمدة عبر فهرس شبيه بالقاموس. استرجاع العمود باسم رأسه (`"Amount"`) يتيح لك تعديل مظهره دون لمس مصدر البيانات الأساسي.  

**نصيحة احترافية:** احرص دائمًا على الحماية من إرجاع `null` – أي خطأ إملائي في اسم العمود أو تغيير مخطط ديناميكي قد يتسبب في حدوث `NullReferenceException` وقت التشغيل.

---

### ## الخطوة 2 – تعيين تنسيق رقم العمود باستخدام قناع عملة مخصص

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**لماذا هذا مهم:**  
سلسلة التنسيق تتبع قواعد تنسيق المحاسبة في Excel:

- `_(* #,##0.00_)` → الأرقام الموجبة، محاذاة لليمين مع مسافة بادئة لرمز العملة.  
- `_(* (#,##0.00)` → الأرقام السالبة محاطة بأقواس.  
- `_(* \"-\"??_)` → القيم الصفرية تُعرض كشرطة.  
- `_(@_)` → القيم النصية تظل دون تغيير.

استخدام **apply custom numeric format** يمنحك تحكمًا كاملًا في فواصل الآلاف، عدد المنازل العشرية، ومكان رمز العملة.  

**حالة خاصة:** إذا كان تطبيقك يحتاج إلى احترام لغة مختلفة (مثلاً يورو بدلاً من الدولار)، استبدل المسافة البادئة بالرمز المناسب أو استخدم تنسيق يعتمد على `CultureInfo` في مصدر البيانات.

---

### ## الخطوة 3 – محاذاة محتويات العمود إلى اليمين للقراءة السهلة

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**لماذا هذا مهم:**  
قيمة العملة تكون أسهل في المسح عندما تكون محاذية على الفاصل العشري. ضبط **set grid column alignment** إلى `Right` يعكس طريقة عرض الجداول للبيانات المالية.  

**ملاحظة:** بعض الشبكات تتجاهل المحاذاة في الخلايا التي تحتوي على قوالب مخصصة. إذا لاحظت أن المحاذاة لا تُطبق، تحقق من أن العمود لا يستخدم مُعالج خلية مخصص.

---

### ## الخطوة 4 – إضافة حد رمادي رفيع حول خلايا العمود

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**لماذا هذا مهم:**  
حد رقيق يفرق عمود “Amount” عن الأعمدة المجاورة، خاصةً عندما تكون الشبكة ذات ألوان صفوف متناوبة. إنه إشارة بصرية تُظهر أن البيانات تمثل قيمة مالية مميزة.  

**نصيحة:** إذا احتجت إلى خط أسمك للطباعة، غيّر `BorderLineStyle` إلى `Medium` أو غير `Color` إلى `Color.Black`.

---

## مثال كامل يعمل

إليك المقتطف الكامل الذي يمكنك وضعه في مشروع WinForms أو WPF يستخدم عنصر تحكم من نمط `GridJs`. المثال يطبع القيم المنسقة إلى وحدة التحكم لتتمكن من التحقق من النتيجة دون واجهة مستخدم.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

لاحظ كيف أن الرقم الموجب محاذٍ لليمين، والرقم السالب يظهر بين أقواس، والصفر يُظهر شرطة – تمامًا ما تُحدده سلسلة التنسيق المخصصة.

---

## الأسئلة المتكررة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت الشبكة تستخدم ثقافة مختلفة (مثلاً € بدلاً من $؟)* | استبدل المسافة البادئة في سلسلة التنسيق بالرمز المطلوب أو دع مصدر البيانات يُصدر سلسلة مُنسقة مسبقًا باستخدام `CultureInfo.CurrentCulture`. |
| *هل يمكن إعادة استخدام نفس التنسيق لعدة أعمدة؟* | بالتأكيد. احفظ سلسلة التنسيق في ثابت (`const string CurrencyMask = "...";`) وعيّنها أينما احتجت للعملة. |
| *ماذا يحدث إذا كان العمود يحتوي على قيمة نصية؟* | سلسلة التنسيق تؤثر فقط على الأنواع الرقمية. النصوص تمر دون تعديل، وهذا هو سبب وجود الجزء الأخير من القناع (`_(@_)`) – للحفاظ على المحتوى غير الرقمي. |
| *هل هناك تأثير على الأداء؟* | لا يذكر. يتم تطبيق التنسيق وقت العرض، وليس أثناء استرجاع البيانات. ما لم تكن تُظهر آلاف الصفوف في كل إطار، لن تلاحظ أي بطء. |
| *كيف أجعل الحد أسمك لتقارير الطباعة؟* | استبدل `BorderLineStyle.Thin` بـ `BorderLineStyle.Medium` أو `BorderLineStyle.Thick`. بعض المكتبات تسمح أيضًا بتحديد عرض البكسل مباشرة. |

---

## الخلاصة

لقد استعرضنا **كيفية تنسيق العملة** في عمود شبكة من البداية حتى النهاية: استرجاع العمود بالاسم، تعيين تنسيق رقم العمود، تطبيق تنسيق رقمي مخصص، محاذاة الخلايا، وإضافة حد أنيق. المثال الكامل يعمل فورًا ويُظهر النتيجة البصرية المتوقعة.

إذا كنت مستعدًا للانتقال إلى مستوى أعلى، جرّب:

- **ثقافات ديناميكية** – غيّر سلسلة التنسيق بناءً على لغة المستخدم.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}