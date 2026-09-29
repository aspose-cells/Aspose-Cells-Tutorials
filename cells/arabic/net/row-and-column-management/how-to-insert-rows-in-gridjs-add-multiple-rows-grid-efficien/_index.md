---
category: general
date: 2026-03-29
description: تعلم كيفية إدراج الصفوف في GridJs بسرعة. يغطي هذا الدليل أيضًا كيفية
  إضافة الصفوف وإضافة عدة صفوف إلى الشبكة باستخدام عملية دفعة.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: ar
og_description: تعلم كيفية إدراج الصفوف في GridJs بسرعة. يوضح هذا الدليل كيفية إضافة
  الصفوف، إضافة عدة صفوف إلى الشبكة، والتعامل مع عمليات الإدراج الضخمة.
og_title: كيفية إدراج صفوف في GridJs – إضافة صفوف متعددة إلى الشبكة بكفاءة
tags:
- GridJs
- C#
- data‑grid
title: كيفية إدراج صفوف في GridJs – إضافة عدة صفوف إلى الشبكة بكفاءة
url: /ar/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إدراج الصفوف في GridJs – إضافة صفوف متعددة إلى الشبكة بكفاءة

هل تساءلت يوماً **عن طريقة إدراج الصفوف** في جدول GridJs ضخم دون تجميد واجهة المستخدم؟ ربما واجهت صعوبة عند محاولة **إضافة الصفوف** واحدةً تلو الأخرى وتدهورت الأداء. الخبر السار هو أن GridJs يوفر واجهة برمجة تطبيقات دفعية تسمح لك **بإضافة صفوف متعددة إلى الشبكة** في استدعاء واحد، مما يبقي الأمور سريعة حتى عند التعامل مع ملايين السجلات.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح بالضبط **كيفية إدراج الصفوف** باستخدام `InsertRowsBatch`. ستتعرف على أهمية التجميع، وكيفية التحقق من النتيجة، وما يجب الانتباه إليه عندما يكون الفهرس المستهدف كبيرًا. بنهاية الدرس ستتمكن من إضافة ألف سجل جديد إلى أي مثيل من GridJs بثقة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (الكود يُترجم مع أي SDK حديث)
- إشارة إلى حزمة NuGet `GridJs` (أو ملف DLL إذا كنت تستخدم بناءً مخصصًا)
- معرفة أساسية بـ C# – لا تحتاج لأن تكون خبيرًا، فقط أن تكون مرتاحًا مع الفئات والطرق
- بيئة تطوير أو محرر من اختيارك (Visual Studio، Rider، VS Code… كلها تعمل)

> **نصيحة احترافية:** إذا كنت تخطط للعمل مع شبكات ضخمة حقًا (عشرات الملايين من الصفوف)، فعّل `gridJs.EnableVirtualization = true;` للحفاظ على خفة رسم واجهة المستخدم.

## الخطوة 1: إنشاء وتكوين كائن GridJs

أولاً وقبل كل شيء: تحتاج إلى كائن `GridJs` حي. فكر فيه كالقماش الذي سترسم عليه الصفوف.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **لماذا هذه الخطوة مهمة:** تهيئة الشبكة وإضافة بيانات مبدئية تحاكي سيناريو واقعي حيث تحتوي الشبكة بالفعل على كمية كبيرة من المعلومات. عملية الإدراج الدفعي التي سنجريها لاحقًا يجب أن تحترم الفهرس الصفري، لذا نقوم بملء بعض البيانات مسبقًا لتوضيح نقطة الإدراج الدقيقة.

## الخطوة 2: استخدام `InsertRowsBatch` لـ **إضافة صفوف متعددة إلى الشبكة**

الآن نصل إلى جوهر الدرس – الاستدعاء الذي يضيف **صفوفًا** بالجملة. توقيع الطريقة هو `InsertRowsBatch(int startIndex, int count)`. في مثالنا سنبدأ عند الفهرس 2 000 000 (ما يعادل الصف رقم 2 000 001) ونضيف عشرة صفوف.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **كيف يعمل:** `InsertRowsBatch` يخصص عدد الصفوف المطلوب داخليًا ويُزاح الصفوف الموجودة إلى الأسفل. لأن العملية تُنفّذ في معاملة واحدة، يتم تحديث واجهة المستخدم مرة واحدة فقط، وهذا هو السبب في أن هذه الطريقة هي الطريقة الموصى بها لـ **كيفية إضافة الصفوف** بكفاءة.

## الخطوة 3: التحقق من الإدراج – هل وصلت الصفوف إلى الموقع المتوقع؟

بعد عملية الدفعة، ستحتاج إلى التأكد من أن الصفوف موجودة حيث توقعت. المساعد التالي يقرأ أول وآخر صف من الكتلة التي أُضيفت حديثًا ويطبعهما على وحدة التحكم.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**المخرجات المتوقعة**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

الخلايا الفارغة تشير إلى أن الصفوف ما زالت أماكن حجز تنتظر البيانات. يمكنك الآن ملؤها فرديًا أو تشغيل دفعة تحديث أخرى.

> **ملاحظة حالة حافة:** إذا تجاوز `startIndex` عدد الصفوف الحالي، سيقوم GridJs تلقائيًا بإلحاق الصفوف الجديدة في النهاية. وعلى العكس، فالفهرس السالب يُسبب استثناء `ArgumentOutOfRangeException`، لذا احرص دائمًا على التحقق من الفهارس التي يزودك بها المستخدم.

## الخطوة 4: ملء الصفوف الجديدة (اختياري لكن شائع)

غالبًا لا تريد صفوفًا فارغة؛ تحتاج إلى تعبئتها بقيم ذات معنى. يمكنك التجول عبر النطاق الذي تم إنشاؤه حديثًا واستدعاء `SetCell` أو واجهة برمجة تطبيقات مماثلة.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

يمكنك استدعاء `PopulateNewRows(gridJs, startIndex, rowsToAdd);` مباشرة بعد الإدراج الدفعي إذا كنت بحاجة إلى أن تكون الصفوف جاهزة للعرض فورًا.

## الخطوة 5: نصائح الأداء للشبكات الضخمة جدًا

عند التعامل مع **إضافة صفوف متعددة إلى الشبكة** بالملايين، ضع هذه الحيل في اعتبارك:

1. **حجم الدفعة مهم** – إدراج 10 000 صف مرة واحدة قد يكون أسرع من عشر دفعات كل منها 1 000 صف لأن كل دفعة تتسبب في تحديث واجهة مستخدم واحد.
2. **إيقاف تحديثات الواجهة** – بعض إصدارات GridJs توفر `grid.SuspendLayout()` / `grid.ResumeLayout()`. غلف دفعتك بهذه الاستدعاءات إذا لاحظت بطء.
3. **استخدام الافتراضية** – كما ظهر سابقًا، `EnableVirtualization` يقلل بشكل كبير من استهلاك الذاكرة ووقت الرسم.
4. **تجنب النسخ العميق** – مرّر أنواع قيم بسيطة أو كائنات خفيفة إلى الشبكة؛ الكائنات الثقيلة تجبر الشبكة على استنساخ البيانات، مما يضر بالأداء.

## مثال كامل يعمل

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

شغّل البرنامج، وسترى مخرجات وحدة التحكم التي تؤكد أن الصفوف العشرة أُضيفت في الموقع الصحيح ثم تم ملؤها.

## الخلاصة

غطّينا **كيفية إدراج الصفوف** في GridJs باستخدام واجهة برمجة التطبيقات الدفعية، وأظهرنا **كيفية إضافة الصفوف** بكفاءة، واستعرضنا طرقًا لـ **إضافة صفوف متعددة إلى الشبكة** دون إبطاء الواجهة. النقاط الرئيسية هي:

- استخدم `InsertRowsBatch(startIndex, count)` لأي عملية دفعية.
- تحقق من صحة الفهارس وفكّر في الافتراضية للبيانات الضخمة.
- املأ الصفوف بعد الدفعة إذا كنت بحاجة إلى محتوى فوري.

بعد ذلك، قد ترغب في استكشاف **كيفية حذف الصفوف**، أو تنفيذ **تراجع/إعادة** لتعديلات الدفعات، أو دمج GridJs مع خدمة خلفية تبث البيانات عند الطلب. جميع هذه المواضيع تبني مباشرةً على المفاهيم التي تعلمتها الآن.

لا تتردد في التجربة—غيّر حجم الدفعة، جرّب الإدراج في بداية الشبكة، أو اجمع دفعات متعددة في معاملة واحدة. كلما لعبت أكثر، كلما أصبحت أكثر ارتياحًا مع التعامل مع الشبكات الكبيرة.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}