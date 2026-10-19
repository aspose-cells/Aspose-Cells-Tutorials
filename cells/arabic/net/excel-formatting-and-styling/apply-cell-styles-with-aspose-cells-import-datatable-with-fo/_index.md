---
category: general
date: 2026-06-05
description: تطبيق أنماط الخلايا أثناء استخدام استيراد Aspose.Cells. تعلّم كيفية استيراد
  DataTable مع التنسيق، تنسيق الصفوف، والحفاظ على تنظيم أوراق العمل.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: ar
og_description: تطبيق أنماط الخلايا أثناء استيراد DataTable إلى ورقة عمل Aspose.Cells.
  دليل خطوة بخطوة مع الكود الكامل والنصائح.
og_title: تطبيق أنماط الخلايا باستخدام Aspose.Cells – استيراد جدول البيانات
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: تطبيق أنماط الخلايا باستخدام Aspose.Cells – استيراد DataTable مع التنسيق
url: /ar/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق أنماط الخلايا باستخدام Aspose.Cells – استيراد DataTable مع التنسيق

هل تساءلت يومًا كيف **تطبيق أنماط الخلايا** عند سحب `DataTable` إلى ورقة Excel؟ لست وحدك. في العديد من سيناريوهات التقارير تحتاج البيانات أن تبدو جيدة مباشرةً دون الحاجة لتنسيق يدوي لاحقًا. الخبر السار هو أن Aspose.Cells يجعل **استيرادًا مع تنسيق** سهلًا بحيث يمكن أن تكون صفوفك حمراء أو زرقاء، غامقة، أو أي شيء تريده.

في هذا البرنامج التعليمي سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح **كيفية استيراد DataTable** إلى ورقة عمل **مع تطبيق أنماط الخلايا**. في النهاية ستحصل على تطبيق C# Console جاهز للتشغيل ينشئ مصنفًا، ينسق العمودين الأولين، ويحفظ الملف—كل ذلك باستخدام واجهة برمجة `aspose cells import`.

## ما ستتعلمه

- إعداد Aspose.Cells في مشروع .NET  
- بناء `DataTable` تجريبي يحاكي بيانات العالم الحقيقي  
- تعريف كائنات `Style` للخط الأحمر والأزرق  
- استخدام `Worksheet.Cells.ImportDataTable` **استيراد ورقة عمل DataTable** مع تطبيق الأنماط  
- التحقق من النتيجة وحفظ المصنف  

لا توجد أدوات خارجية، فقط C# صافي و Aspose.Cells. لنبدأ.

---

## المتطلبات المسبقة

قبل أن نغوص في الشيفرة، تأكد من توفر ما يلي:

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث | Aspose.Cells 23.x يستهدف .NET Standard 2.0+، لذا يمنحك .NET 6 أحدث ميزات وقت التشغيل. |
| Aspose.Cells for .NET (NuGet) | المكتبة توفر الكائنات `Workbook`، `Worksheet`، `Style`، وطرق `ImportDataTable` التي نحتاجها. |
| معرفة أساسية بـ C# | ستفهم الفئات، المصفوفات، وتعليمات `using`. |
| بيئة تطوير (Visual Studio، VS Code، Rider) | أي محرر يعمل، لكن ستحتاج لاستعادة حزم NuGet. |

يمكنك تثبيت الحزمة من سطر الأوامر:

```bash
dotnet add package Aspose.Cells
```

---

## الخطوة 1: إنشاء مصنف جديد والوصول إلى ورقة العمل الأولى

أولًا وقبل كل شيء—لننشئ `Workbook` ونحصل على الورقة الأولى. فكر في المصنف كدفتر ملاحظات فارغ؛ ورقة العمل الأولى هي الصفحة التي سنكتب عليها.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **نصيحة احترافية:** إذا احتجت إلى عدة أوراق، فقط أضفها باستخدام `wb.Worksheets.Add()` وارجع إليها بالاسم أو الفهرس.

---

## الخطوة 2: إعداد DataTable تجريبي (كيفية استيراد DataTable)

الآن نحتاج إلى شيء لاستيراده. في المشاريع الحقيقية قد تستدعي قاعدة بيانات، لكن للتوضيح سنبني `DataTable` في الذاكرة.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **لماذا هذا مهم:** وجود `DataTable` يتيح لنا اختبار تدفق **aspose cells import** دون أي تبعيات خارجية.

---

## الخطوة 3: تعريف الأنماط لتطبيقها على الخلايا المستوردة

هنا يحدث السحر. سننشئ كائنين `Style`: أحدهما بخط أحمر، والآخر بخط أزرق. سيتم تطبيقهما على مستوى الأعمدة أثناء الاستيراد.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **احذر:** يجب أن يتطابق طول `importStyles` مع عدد الأعمدة التي تستوردها، وإلا سيطرح Aspose استثناءً من نوع `ArgumentException`.

---

## الخطوة 4: استيراد DataTable إلى ورقة العمل **مع التنسيق**

الآن نجمع كل شيء معًا. التحميل الزائد `ImportDataTable` الذي نستخدمه يقبل مصفوفة `Style[]`، مما يتيح لنا **تطبيق أنماط الخلايا** عندما تُدخل البيانات إلى الورقة.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### كيف يعمل

1. **العناوين** – لأننا مررنا `true`، يكتب Aspose “Name” و “Score” في الصف الأول.  
2. **صفوف البيانات** – كل صف لاحق يحصل على النمط المقابل من `importStyles`.  
3. **الأداء** – الطريقة تبث البيانات مباشرةً إلى ورقة العمل، وهو أسرع من التكرار خلية بخلية.

---

## الخطوة 5: التحقق من النتيجة وحفظ المصنف

لنلقِ نظرة سريعة على أول few خلايا للتأكد من أن الأنماط تم تطبيقها، ثم نكتب الملف إلى القرص.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

عند فتح **StyledImport.xlsx**، ستلاحظ:

- عمود “Name” بنص **أحمر**.  
- عمود “Score” بنص **أزرق**.  
- عناوين الأعمدة بالنمط الافتراضي (يمكنك تنسيقها أيضًا، لكن هذا دليل آخر).

![مثال على تطبيق أنماط الخلايا](https://example.com/images/apply-cell-styles.png "تطبيق أنماط الخلايا في Aspose.Cells")

> **ملاحظة:** الصورة أعلاه توضح الشكل النهائي. يحتوي سمة `alt` على الكلمة المفتاحية الأساسية، لتلبية متطلبات تحسين محركات البحث.

---

## أسئلة شائعة وحالات حافة

### ماذا لو كان لدى DataTable الخاص بي أعمدة أكثر من الأنماط؟

سيطبق Aspose النمط الأخير في المصفوفة على أي أعمدة إضافية. لتجنب ألوان غير متوقعة، احرص دائمًا على مطابقة طول المصفوفة مع عدد الأعمدة، أو مرر `null` للأعمدة التي لا تريد تنسيقها.

### هل يمكنني تطبيق أنماط مختلفة على صفوف معينة؟

بالطبع. بعد الاستيراد، يمكنك التكرار عبر الصفوف وتعيين كائنات `Style` جديدة بناءً على شروط (مثلاً، تمييز الدرجات > 90 باللون الأخضر). إليك مقتطفًا سريعًا:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### هل يعمل هذا مع مجموعات بيانات كبيرة؟

نعم. `ImportDataTable` يبث البيانات بكفاءة، وتطبيق مصفوفة أنماط ثابتة يضيف عبئًا ضئيلًا. لملايين الصفوف، فكر في استخدام `ImportDataTable` على دفعات أو الاستفادة من `Cells.ImportDataTable` مع `DataReader` لتحسين استهلاك الذاكرة.

### كيف أحافظ على التنسيق الموجود في ورقة العمل؟

إذا كان النطاق المستهدف يحتوي بالفعل على تنسيق تريد الاحتفاظ به، اضبط معامل `importOptions` في التحميل الزائد `ImportDataTable` (`ImportTableOptions`) وعدل `ImportDataTableOptions.PreserveCellFormatting`. السلوك الافتراضي يستبدل الأنماط بالأنماط التي تزودها.

---

## ملخص: ما أنجزناه

- **تطبيق أنماط الخلايا** أثناء عملية **aspose cells import**.  
- توضيح **الاستيراد مع التنسيق** بتمرير مصفوفة `Style[]`.  
- إظهار **كيفية استيراد DataTable** إلى ورقة عمل وحفظ النتيجة.  
- تغطية حالات الحافة مثل عدم تطابق عدد الأنماط وتنسيق الصفوف الشرطي.

كل هذا تم في تطبيق Console واحد مكتمل—بدون سكريبتات خارجية، دون تعديل يدوي في Excel. الآن لديك أساس قوي لأي ميزة تقارير أو تصدير بيانات تحتاج إلى مخرجات Excel مصقولة.

---

## الخطوات التالية

هل أنت مستعد للارتقاء؟ إليك بعض الأفكار التي تبني على ما تعلمته للتو:

- **تنسيق صف العنوان** (مثلاً، غامق، لون خلفية).  
- **تطبيق تنسيق شرطي** باستخدام `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **تصدير إلى صيغ أخرى** مثل CSV أو PDF باستخدام `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **دمج عدة DataTables** في مصنف واحد، كل واحدة في ورقة منفصلة، باستخدام نفس نهج التنسيق.

إذا واجهت أي صعوبات، اترك تعليقًا أو راجع الوثائق الرسمية لـ Aspose حول `ImportDataTable`. برمجة سعيدة، واستمتع بملفات Excel ذات الأنماط الجميلة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑By‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Apply Text Shadow in Excel Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}