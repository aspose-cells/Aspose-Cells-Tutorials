---
category: general
date: 2026-06-27
description: حذف عدة صفوف في Word باستخدام C#. تعلّم كيفية حذف صفوف الجداول، وإزالة
  صفوف الجداول، وتعديل جداول مستند Word بكفاءة.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: ar
og_description: احذف عدة صفوف في Word فورًا. يوضح هذا الدرس كيفية حذف صفوف الجدول،
  وإزالة الصفوف من جدول Word، وتحرير جدول المستند الرئيسي في Word.
og_title: حذف عدة صفوف في Word – تحرير الجداول خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: حذف عدة صفوف في Word – دليل كامل لإزالة صفوف الجدول
url: /ar/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف عدة صفوف في Word – دليل كامل لإزالة صفوف الجدول

هل احتجت يوماً إلى **حذف عدة صفوف في مستندات Word** لكن لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عند محاولة تقليل حجم جدول مع الحفاظ على الرأس.

في هذا البرنامج التعليمي سنستعرض حلاً مختصراً من البداية إلى النهاية يوضح *كيفية حذف صفوف الجدول* برمجيًا، *كيفية إزالة صفوف الجدول* بأمان، ولماذا يعمل هذا النهج في كل سيناريو **حذف صفوف من جدول Word** قد تواجهه.

بنهاية الدليل ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع C#، بالإضافة إلى مجموعة من النصائح لمهام **تحرير جداول مستندات Word** الأوسع.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.6+)
- Aspose.Words for .NET مثبت (`dotnet add package Aspose.Words`)
- فهم أساسي لصياغة C#
- ملف `.docx` إدخالي يحتوي على جدول واحد على الأقل مع صف رأس

> **نصيحة احترافية:** إذا لم يكن لديك ترخيص بعد، تقدم Aspose.Words وضع تقييم مجاني مثالي للاختبار.

## الخطوة 1: إعداد المشروع وتحميل مستند Word

أولاً، أنشئ تطبيقًا سطريًا (أو دمجه في خدمة موجودة) وأضف توجيهات `using` اللازمة. ثم قم بتحميل المستند المصدر.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**لماذا هذا مهم:**  
`Document` هو نقطة الدخول لكل عملية في Aspose.Words. تحميل الملف مرة واحدة يقلل استهلاك الذاكرة ويمنحك مقبضًا لجميع عمليات تعديل الجداول اللاحقة.

## الخطوة 2: تحديد الجدول الأول (أو أي جدول تحتاجه)

إذا كان مستندك يحتوي على عدة جداول، يمكنك اختيار الجدول المطلوب عبر الفهرس أو بالبحث عن كلمة مفتاحية. للتبسيط سنأخذ الجدول الأول، الذي عادةً يحتوي على البيانات التي نريد تقليمها.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**شرح:**  
`GetChild(NodeType.Table, 0, true)` يتجول في شجرة المستند بعمق أول ويعيد أول عقدة `Table` يصادفها. التحويل `as Table` يحول العقدة بأمان، مما يتيح لنا العمل مع `Rows` لاحقًا.

## الخطوة 3: حذف عدة صفوف مع الحفاظ على الرأس

الآن نصل إلى جوهر الموضوع: **حذف عدة صفوف في مستندات Word**. افترض أن الرأس موجود في الصف 0 وتريد حذف الصفين التاليين (المؤشرات 1 و 2). طريقة `DeleteRows` تفعل ذلك بالضبط.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### كيفية حذف صفوف الجدول – تنويعات

- **حذف صف واحد:** `firstTable?.DeleteRows(rowIndex, 1);`
- **حذف جميع الصفوف باستثناء الرأس:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **حذف الصفوف بناءً على شرط:** قم بتكرار `firstTable.Rows` واستدعِ `DeleteRows` عندما يتطابق محتوى خلية مع معاييرك.

هذه المقاطع تجيب على السؤال الشائع **كيفية إزالة صفوف الجدول** بطريقة مرنة.

## الخطوة 4: حفظ المستند المعدل

بعد حذف الصفوف، ببساطة تكتب المستند مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء نسخة جديدة.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**ما ستراه:**  
إذا كان الجدول الأصلي يحتوي، على سبيل المثال، على خمسة صفوف (رأس + أربعة صفوف بيانات)، فإن `output.docx` المحفوظ سيحتوي الآن على ثلاثة صفوف فقط (رأس + صفين بيانات متبقيين). افتح الملف في Word للتحقق من أن الصفوف غير المرغوب فيها اختفت دون إزعاج أي محتوى آخر.

![نص بديل للصورة: حذف عدة صفوف في Word – لقطة شاشة قبل وبعد لجدول Word](delete-multiple-rows-word.png)

*نص بديل للصورة: حذف عدة صفوف في Word – لقطة شاشة قبل وبعد لجدول Word.*

## مثال كامل وجاهز للتنفيذ

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

شغّل البرنامج، افتح `output.docx`، وسترى أن الرأس لا يزال موجودًا بينما اختفت الصفوف المختارة. هذا هو **حذف عدة صفوف في Word** عمليًا.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| **NullReferenceException** عندما يكون `firstTable` `null` | المستند لا يحتوي على جداول أو الفهرس غير صحيح | تأكد دائمًا من أن `firstTable != null` قبل استدعاء `DeleteRows`. |
| **الصفوف لم تُحذف** | استخدام فهرس بداية خاطئ (جداول Word تبدأ من الصفر) | تذكر أن الرأس هو الصف 0؛ ابدأ من 1 للحفاظ عليه. |
| **الحفظ فوق ملف للقراءة فقط** | أذونات الملف تمنع الكتابة | احفظ إلى مسار مختلف أو عدّل خصائص الملف. |
| **تغييرات غير متوقعة في التخطيط** | حذف صفوف تحتوي على خلايا مدمجة قد يفسد الجدول | تأكد من معالجة الخلايا المدمجة—قم بفك الدمج أولاً أو احذف الصفوف بالكامل بحذر. |

## توسيع الحل – المزيد من تحرير جداول مستندات Word

إذا كنت مهتمًا بـ **تحرير جداول مستندات Word** بشكل أوسع، فكر في الخطوات التالية:

- **إدراج صفوف جديدة**: `firstTable?.Rows.Add(new Row(doc));`
- **تحديث نص الخلية**: `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **تطبيق الأنماط**: استخدم `CellFormat` أو `RowFormat` لتعيين التظليل أو الحدود أو خصائص الخط.
- **التصدير إلى PDF**: `doc.Save("output.pdf", SaveFormat.Pdf);`

جميع هذه العمليات تعتمد على نموذج الكائن نفسه الذي استخدمناه لحذف الصفوف، مما يحافظ على اتساق قاعدة الشيفرة الخاصة بك.

## الخلاصة

لقد أظهرنا لك الآن كيفية **حذف عدة صفوف في مستندات Word** باستخدام بضع أسطر من كود C#. يغطي النهج *كيفية حذف صفوف الجدول*، *كيفية إزالة صفوف الجدول*، والموضوع الأوسع **تحرير جداول مستندات Word**.

أصبح لديك الآن نمط ثابت وقابل لإعادة الاستخدام: تحميل المستند، تحديد الجدول، استدعاء `DeleteRows` بالمؤشرات الصحيحة، ثم الحفظ. من هنا يمكنك تعديل نطاق الصفوف، التكرار على الجداول، أو دمج ميزات تحرير أخرى لتناسب أي مهمة أتمتة.

هل أنت مستعد للانتقال للخطوة التالية؟ جرّب أتمتة إنشاء الفواتير، تنظيف قوالب التقارير، أو بناء أداة تحديث جماعي تعالج عشرات ملفات Word دفعة واحدة. السماء هي الحد، وAPI يجعل الأمر سهلًا.

إذا واجهت أي صعوبات، اترك تعليقًا أدناه—برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إدراج وحذف الصفوف في Excel باستخدام Aspose.Cells لـ .NET: دليل شامل](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [حذف عدة صفوف في Excel باستخدام Aspose.Cells .NET: دليل شامل لمعالجة البيانات](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [حذف عدة صفوف في Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}