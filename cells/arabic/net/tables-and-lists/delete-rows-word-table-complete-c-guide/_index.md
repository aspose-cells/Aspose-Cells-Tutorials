---
category: general
date: 2026-06-08
description: حذف صفوف جدول Word باستخدام Aspose.Words. تعلّم كيفية حذف الصفوف، حذف
  عدة صفوف في Word، وإتقان تحرير الجداول في دقائق.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: ar
og_description: احذف صفوف جدول Word باستخدام Aspose.Words. يوضح هذا الدرس كيفية حذف
  الصفوف، حذف عدة صفوف في Word، والحفاظ على جداولك مرتبة.
og_title: حذف صفوف جدول Word – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: حذف صفوف جدول Word – دليل C# الكامل
url: /ar/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف صفوف جدول Word – دليل C# كامل

هل احتجت يومًا إلى **delete rows word table** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عند تنظيف التقارير المولدة أو تقليص الجداول المستندة إلى البيانات. الخبر السار؟ ببضع أسطر من C# و Aspose.Words يمكنك بسهولة إزالة الصفوف غير المرغوب فيها، سواء كانت سطرًا واحدًا أو مجموعة منها. في هذا الدليل سنستعرض *how to delete rows* وحتى نتناول الحالة الأكثر تعقيدًا وهي **delete multiple rows word** في خطوة واحدة.

سنغطي كل ما تحتاج معرفته: الكود الدقيق، لماذا كل خطوة مهمة، الأخطاء الشائعة، ومثال جاهز للتنفيذ. بنهاية هذا الدليل ستكون قادرًا على حذف الصفوف من أي جدول Word دون كسر بنية المستند. لا إطالة، فقط تقنيات عملية ومجربة.

## المتطلبات المسبقة

- **Aspose.Words for .NET** (الإصدار 23.12 أو أحدث). يمكنك الحصول عليه من NuGet: `Install-Package Aspose.Words`.
- بيئة تطوير .NET (Visual Studio، Rider، أو VS Code مع امتداد C#).
- ملف Word الإدخالي (`input.docx`) الذي يحتوي على جدول واحد على الأقل مع صف رأس.

هذا كل شيء—لا مكتبات إضافية، لا تفاعل COM، فقط كود مُدار نقي.

## الخطوة 1: تحميل مستند Word

أول شيء تقوم به هو فتح المستند. Aspose.Words يتعامل مع ملف Word ككائن `Document`، مما يمنحك وصولًا كاملًا إلى الأقسام، الأجسام، الجداول، وأكثر.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*لماذا هذا مهم:* تحميل المستند يُنشئ تمثيلًا في الذاكرة، لذا أي تغييرات تقوم بها تكون سريعة ولا تمس نظام الملفات حتى تقوم بالحفظ صراحةً.

## الخطوة 2: الحصول على الجدول المستهدف

في معظم السيناريوهات تعرف أي جدول تريد تحريره—غالبًا الأول. Aspose.Words يجعل من السهل جلبه عبر خاصية `FirstSection`.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

إذا كان مستندك يحتوي على جداول متعددة، يمكنك التكرار عبر `doc.GetChildNodes(NodeType.Table, true)` واختيار الجدول المناسب بناءً على الفهرس أو علامة مخصصة.

## الخطوة 3: حذف الصفوف – فردي أو متعدد

### 3.1 كيفية حذف الصفوف (صف واحد)

لإزالة صف واحد، استدعِ `DeleteRows(startIndex, count)` حيث `startIndex` يبدأ من الصفر. تخطي صف الرأس (الفهرس 0) شائع:

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 حذف عدة صفوف Word – إزالة دفعة

عندما تحتاج إلى حذف نطاق—مثلاً الصفوف 2‑6—تمرر فهرس البداية وعدد الصفوف التي تريد مسحها. هذا هو نمط **delete multiple rows word**:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*لماذا استخدام استدعاء واحد؟* حذف الصفوف واحدًا تلو الآخر يجبر الجدول على إعادة الفهرسة بعد كل حذف، مما قد يسبب أخطاء ويكون أبطأ. طريقة الحذف الجماعي تحافظ على تماسك البنية الداخلية للجدول.

#### حالة الحافة: حذف خارج حجم الجدول

إذا كان `startIndex + count` يتجاوز عدد الصفوف الفعلي، فإن Aspose.Words يرمي استثناء `ArgumentOutOfRangeException`. يمكن إضافة حماية دفاعية كالتالي:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

هذا المقتطف يضمن أنك لا تحاول حذف أكثر من عدد الصفوف الموجودة.

## الخطوة 4: حفظ المستند المعدل

بعد حذف الصفوف، حفظ التغييرات يكون بسطر واحد:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

طريقة `Save` تختار تلقائيًا التنسيق بناءً على امتداد الملف، لذا يمكنك الإخراج إلى PDF أو HTML أو حتى ODT بامتداد مختلف.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الجاهز للتنفيذ:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### النتيجة المتوقعة

- `output.docx` يحتوي على الجدول الأصلي **بدون** الصفوف 2‑6.
- جميع الصفوف المتبقية تتحرك للأعلى، مع الحفاظ على تنسيق الخلايا وعرض الأعمدة.
- صف الرأس يبقى سليمًا، مما يحافظ على عناوين الأعمدة مرئية.

## لماذا هذا النهج يتفوق على البدائل

| النهج | الإيجابيات | السلبيات |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | حذف جماعي بسطر واحد، يحافظ على الأنماط، لا يعتمد على COM | يتطلب مكتبة تجارية (يتوفر نسخة تجريبية مجانية) |
| Office Interop | يعمل مع Word الأصلي | يتطلب تثبيت Word على الخادم، بطيء، مشاكل تنظيف COM |
| Open XML SDK | مجاني، مفتوح المصدر | تلاعب يدوي بـ XML؛ حذف الصفوف بأمان معقد |

إذا كنت بالفعل تستخدم Aspose.Words لمهام مستندات أخرى، فإن الالتزام بـ `DeleteRows` يحافظ على نظافة وتناسق قاعدة الشيفرة الخاصة بك.

## نصائح احترافية ومخاطر شائعة

- **نصيحة احترافية:** احرص دائمًا على إبقاء صف الرأس (الفهرس 0) دون تعديل ما لم تكن ترغب فعلاً في حذفه. حذف الرأس قد يفسد المعالجة اللاحقة التي تتوقع أسماء الأعمدة.
- **احذر الخلايا المدمجة.** إذا كان الصف يحتوي على خلية مدمجة عموديًا تمتد إلى الصف الذي تحذفه، فإن Aspose.Words سيضبط نطاق الدمج تلقائيًا، لكن تحقق من النتيجة البصرية.
- **ملاحظة أداء:** حذف العديد من الصفوف من جدول ضخم (آلاف الصفوف) لا يزال سريعًا، ولكن إذا كنت تعالج مئات المستندات في حلقة، فكر في إعادة استخدام كائن `Document` حيثما أمكن لتقليل عبء التخصيص.

## الأسئلة المتكررة

**س: هل يمكنني حذف الصفوف بناءً على محتوى الخلية بدلاً من الفهرس؟**  
ج: بالتأكيد. قم بالتكرار عبر `table.Rows`، افحص `row.Cells[i].GetText()`، وجمع الفهارس المطابقة. ثم استدعِ `DeleteRows` مع أصغر فهرس وإجمالي العدد، أو احذف الصفوف بترتيب عكسي لتجنب إعادة الفهرسة.

**س: هل يعمل هذا مع ملفات .doc؟**  
ج: نعم. Aspose.Words يدعم كلًا من `.doc` و `.docx`. فقط غيّر امتداد الملف في مُنشئ `Document` واستدعاء `Save`.

**س: ماذا لو كان الجدول داخل رأس أو تذييل الصفحة؟**  
ج: استخرجه عبر مجموعة `doc.FirstSection.HeadersFooters`، ثم طبّق نفس منطق `DeleteRows`.

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية لـ **delete rows word table** باستخدام C#. يوضح المثال *how to delete rows* بشكل فردي وكيفية **delete multiple rows word** في استدعاء واحد فعال. مع Aspose.Words تحصل على API نظيفة، بدون متاعب COM، وتحكم كامل في مستندات Word.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة صف جديد مع مجموعات محسوبة، أو صدّر الجدول المقتطع إلى CSV باستخدام `Table.ToTxt`. السماء هي الحد عندما تتقن التعامل مع الجداول.

برمجة سعيدة، ولتظل جداول Word مرتبة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حذف الصفوف في Excel باستخدام Aspose.Cells للغة Java | دليل وتعليم](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [كيفية حذف الصفوف الفارغة في Excel باستخدام Aspose.Cells .NET لتنظيف البيانات](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [كيفية إدراج وحذف الصفوف في Excel باستخدام Aspose.Cells للـ .NET&#58; دليل شامل](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}