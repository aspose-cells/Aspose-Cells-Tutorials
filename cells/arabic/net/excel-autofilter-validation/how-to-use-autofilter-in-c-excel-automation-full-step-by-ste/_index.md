---
category: general
date: 2026-05-30
description: كيفية استخدام AutoFilter في أتمتة Excel باستخدام C#. تعلم كيفية إنشاء
  مصنف Excel، وتصفية الصفوف حسب القيمة، وتبسيط مهام جداول البيانات الخاصة بك.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: ar
og_description: كيفية استخدام AutoFilter في أتمتة Excel باستخدام C#. إتقان إنشاء مصنف
  Excel، وتصفية الصفوف حسب القيمة، وأتمتة الجداول بسهولة.
og_title: كيفية استخدام AutoFilter في أتمتة Excel باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: كيفية استخدام AutoFilter في أتمتة Excel باستخدام C# – دليل كامل خطوة بخطوة
url: /ar/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام AutoFilter في أتمتة Excel باستخدام C# – دليل كامل

هل تساءلت يومًا **كيف تستخدم AutoFilter** عندما تقوم بإنشاء ملفات Excel من كود C#؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحتاجون إلى إخفاء الصفوف التي لا تطابق معيارًا معينًا.  

في هذا الدرس سنستعرض مثالًا عمليًا قابلًا للتنفيذ **ينشئ مصنف Excel**، يضيف جدولًا، ثم **يفلتر الصفوف حسب القيمة** في العمود B. في النهاية ستحصل على قطعة شفرة نظيفة وقابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع C# يحتاج إلى أتمتة Excel.

## ما ستتعلمه

- إعداد مشروع C# مع مكتبة Aspose.Cells (أو Microsoft.Office.Interop).  
- **إنشاء مصنف Excel** برمجيًا وإضافة جدول منسق.  
- تطبيق **AutoFilter** لإظهار الصفوف التي يكون فيها **العمود B** يساوي سلسلة محددة.  
- إزالة الفلتر بالكامل، واستعادة مجموعة البيانات الكاملة.  
- نصائح للتعامل مع الحالات الحدية مثل الأعمدة المفقودة أو معايير الفلترة المتعددة.

لا تحتاج إلى خبرة سابقة في Excel‑VBA؛ فقط فهم أساسي لـ C# وحزم NuGet.

---

## المتطلبات المسبقة

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.7+) | توفر بيئات التشغيل الحديثة أداءً أفضل وإدارة حزم أسهل. |
| Aspose.Cells لـ .NET (أو Microsoft.Office.Interop.Excel) مثبت عبر NuGet | توفر هذه المكتبة كائنات `Workbook` و `Worksheet` و `Table` المستخدمة في الشيفرة. |
| محرر شفرة (Visual Studio, VS Code, Rider, إلخ) | ستحتاج إلى تجميع وتشغيل المثال. |
| معرفة أساسية بـ C# | يشرح الدرس *لماذا* كل سطر موجود، وليس فقط *ماذا* يفعل. |

يمكنك تثبيت Aspose.Cells باستخدام:

```bash
dotnet add package Aspose.Cells
```

---

## كيفية استخدام AutoFilter مع Aspose.Cells في C#

فيما يلي البرنامج الكامل المستقل. احفظه كملف `Program.cs` في مشروع وحدة تحكم وشغّله – ستحصل على `FilteredWorkbook.xlsx` في مجلد الإخراج.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### كيف يعمل الكود

1. **إنشاء المصنف** – `new Workbook()` يمنحك ملفًا فارغًا؛ `Worksheets[0]` يحصل على الورقة الافتراضية.  
2. **ملء بيانات عينة** – نكتب مجموعة بيانات صغيرة لتتمكن من رؤية الفلتر يعمل.  
3. **إضافة جدول** – `ListObjects.Add` يحول النطاق إلى جدول Excel، الذي يدعم الفلترة والتنسيق تلقائيًا.  
4. **تطبيق AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` يوجه المحرك: “أظهر فقط الصفوف التي يكون فيها العمود الثاني (B) يساوي *Apple*.”  
5. **حفظ الملفات** – يتم كتابة ملفين: أحدهما مفلتر، والآخر مع إزالة الفلتر، مما يثبت أن `RemoveAutoFilter()` يعمل كما هو متوقع.

> **نصيحة احترافية:** إذا كنت بحاجة إلى الفلترة وفقًا لعدة معايير (مثلاً “Apple” *أو* “Banana”)، استخدم النسخة المتعددة `Filter(int columnIndex, string criteria1, string criteria2)` أو مرّر مصفوفة من السلاسل.

---

## فلترة الصفوف حسب القيمة – تنويعات شائعة

بينما يركز المثال أعلاه على **تصفية العمود B**، قد ترغب في تصفية أعمدة أخرى أو استخدام معايير رقمية. إليك ورقة غش سريعة:

| Desired filter | Code snippet |
|----------------|--------------|
| مطابقة نصية في العمود C | `table.AutoFilter.Filter(2, "Cherry");` |
| أرقام أكبر من 10 في العمود C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| قيم متعددة في العمود B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**حالة حدية:** إذا كان عنوان العمود مكتوبًا بشكل خاطئ أو كان فهرس العمود خارج النطاق، تقوم Aspose.Cells برمي استثناء `ArgumentException`. احمِ نفسك من ذلك بالتحقق من `table.ListColumns.Count` قبل تطبيق الفلتر.

---

## إزالة AutoFilter – متى يتم إعادة الضبط

أحيانًا تحتاج إلى عرض مجموعة البيانات الكاملة مرة أخرى (مثلاً، بعد أن يمسح المستخدم مربع البحث). استدعاء `table.RemoveAutoFilter()` ينجز المهمة في سطر واحد. إذا كنت تستخدم Microsoft.Office.Interop بدلاً من ذلك، ستستدعي `worksheet.AutoFilterMode = false;`.

---

## ملخص المثال الكامل العامل

فيما يلي البرنامج *الكامل* مرة أخرى، بدون تعليقات لأولئك الذين يفضلون عرضًا مختصرًا:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

تشغيل هذا ينتج ملفين:

- **FilteredWorkbook.xlsx** – فقط الصفوف التي تحتوي على *Apple* مرئية.  
- **UnfilteredWorkbook.xlsx** – استعادة البيانات الأصلية.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات .xls القديمة؟**  
ج: نعم. يمكن لـ Aspose.Cells حفظ الملفات بصيغة `.xlsx` أو `.xls` عن طريق تغيير امتداد الملف أو استخدام `SaveOptions`.

**س: ماذا لو احتجت إلى الفلترة *بعد* حفظ المصنف؟**  
ج: حمّل الملف باستخدام `new Workbook("path.xlsx")`، طبّق الفلتر، ثم احفظ مرة أخرى باستخدام `Save`.

**س: هل يمكنني تطبيق فلتر على *نطاق* ليس جدولًا؟**  
ج: بالتأكيد. استخدم `worksheet.AutoFilter.Range = "A1:C5";` ثم `worksheet.AutoFilter.ApplyFilter();`. ومع ذلك، الجداول توفر تنسيقًا مدمجًا وإشارة أسهل إلى الأعمدة.

---

## صورة – تأكيد بصري

![Screenshot showing AutoFilter applied to column B in an Excel workbook created with C#](/images/autofilter-column-b.png "AutoFilter on column B")

*(توضح الصورة العرض المفلتر حيث تبقى فقط الصفوف التي تحتوي على “Apple”.)*

---

## الخلاصة

لقد غطينا للتو **كيفية استخدام AutoFilter** في سيناريو أتمتة Excel باستخدام C#، بدءًا من **إنشاء مصنف Excel** إلى **فلترة الصفوف حسب القيمة** في **العمود B**، وأخيرًا **إزالة الفلتر** عندما لا يكون مطلوبًا. الخطوات الأساسية — التهيئة، إضافة جدول، تطبيق الفلتر، والتنظيف — قابلة لإعادة الاستخدام في أي مشروع يحتاج إلى **excel automation c#**.

هل أنت مستعد للتحدي التالي؟ جرّب:

- إضافة تنسيق شرطي لتسليط الضوء على الصفوف المفلترة.  
- تصدير البيانات المفلترة إلى CSV للمعالجة اللاحقة.  
- دمج عدة فلاتر (مثلاً “Apple” *و* الكمية > 8).

جرّب، اكسر الأشياء، ثم أصلحها—

## ماذا يجب أن تتعلم بعد ذلك؟

- [كيفية تنفيذ AutoFilter في Excel باستخدام Aspose.Cells لـ .NET (دليل تحليل البيانات)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [كيفية استخدام Autofilter Not Contains في Aspose.Cells .NET لتحليل بيانات Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [كيفية تنفيذ Excel Autofilter 'EndsWith' باستخدام Aspose.Cells لـ .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}