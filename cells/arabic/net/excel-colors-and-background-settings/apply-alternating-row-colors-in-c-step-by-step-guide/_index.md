---
category: general
date: 2026-03-18
description: تعلم كيفية تطبيق ألوان الصفوف المتناوبة في ورقة العمل باستخدام C#. يتضمن
  تعيين لون خلفية الصف، إضافة خلفية صفراء فاتحة، وتلوين الصفوف بالتناوب.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: ar
og_description: تطبيق ألوان الصفوف المتناوبة في C# لتحسين قابلية القراءة. يوضح هذا
  الدليل كيفية تعيين لون خلفية الصف، إضافة خلفية صفراء فاتحة، وتلوين الصفوف بشكل متناوب.
og_title: تطبيق ألوان الصفوف المتناوبة في C# – دليل كامل
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: تطبيق ألوان الصفوف المتناوبة في C# – دليل خطوة بخطوة
url: /ar/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق ألوان الصفوف المتناوبة في C# – دليل كامل

هل احتجت يومًا إلى **تطبيق ألوان الصفوف المتناوبة** على ورقة عمل مدفوعة بالبيانات ولكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك — معظم المطورين يواجهون هذه المشكلة عندما يحاولون لأول مرة جعل الجداول تبدو أكثر ودية. الخبر السار؟ في بضع أسطر فقط من C# يمكنك **تعيين لون خلفية الصف**، وإضافة **خلفية أصفر فاتح**، وستحصل على شبكة مصقولة تحسن القراءة على الفور.

في هذا الدليل سنستعرض العملية بالكامل، من جلب `DataTable` إلى الذاكرة إلى تنسيق كل صف بخط أصفر‑أبيض خفيف. في النهاية ستتمكن من **تلوين الصفوف بالتناوب** بثقة، وسترى أيضًا بعض الاختلافات المفيدة عندما تحتاج إلى ظلال مختلفة أو ثيمات ديناميكية.

## ما الذي ستحتاجه

- مشروع .NET يستهدف .NET 6 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- مكتبة جداول بيانات تدعم كائنات النمط – المثال يستخدم API عام `Workbook`/`Worksheet` يشبه مكتبات مثل **Aspose.Cells**, **GemBox.Spreadsheet**, أو **ClosedXML**.  
- مصدر `DataTable` – يمكن أن يكون من استعلام قاعدة بيانات، استيراد CSV، أو أي مجموعة في الذاكرة.  

لا توجد حزم NuGet إضافية بخلاف مكتبة جداول البيانات نفسها. إذا كنت تستخدم Aspose.Cells، فإن مساحة الاسم هي `Aspose.Cells`؛ بالنسبة إلى ClosedXML فهي `ClosedXML.Excel`. استبدل استدعاءات `CreateStyle` و `ImportDataTable` وفقًا لذلك.

## الخطوة 1: استرجاع بيانات المصدر كـ DataTable

أولًا وقبل كل شيء—احصل على البيانات التي تريد عرضها. في التطبيقات الواقعية هذا عادةً يعني استدعاء قاعدة بيانات، لكن للتوضيح سننشئ طريقة مساعدة تسمى `GetData()` تُعيد `DataTable` مُعبأة.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **لماذا هذا مهم:** يحدد `DataTable` الصفوف والأعمدة التي ستستقبل التظليل المتناوب لاحقًا. إذا كان الجدول فارغًا، لا يوجد ما لتنسيقه، لذا تأكد دائمًا أن `Rows.Count` > 0 قبل المتابعة.

### نصحة احترافية
إذا كنت تستخرج البيانات من Entity Framework، يمكنك استخدام `DataTable.Load(reader)` بعد تنفيذ `SqlCommand`. هذا يحافظ على نظافة الكود ويتجنب تعريف الأعمدة يدويًا.

## الخطوة 2: تخصيص مصفوفة للاحتفاظ بنمط لكل صف

بعد ذلك، نحتاج إلى حاوية تتطابق مع عدد الصفوف. معظم APIs لجداول البيانات تسمح بتمرير مصفوفة نمط إلى طريقة الاستيراد، لذا سننشئ `Style[]` بحجم يساوي عدد الصفوف بالضبط.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **شرح:** من خلال تخصيص المصفوفة مسبقًا، نتجنب إنشاء كائن نمط جديد في كل تكرار، وهو ما يمكن أن يكون فوزًا في الأداء عند التعامل مع آلاف الصفوف.

## الخطوة 3: تطبيق ألوان الصفوف المتناوبة (أصفر فاتح / أبيض)

الآن يأتي جوهر الموضوع: **تطبيق ألوان الصفوف المتناوبة**. سنقوم بالتكرار عبر كل صف، إنشاء نسخة جديدة من النمط من الـ workbook، وتعيين خلفيته بناءً على فهرس الصف. الصفوف الزوجية تحصل على تعبئة أصفر فاتح، والصفوف الفردية تبقى بيضاء.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### لماذا يعمل هذا
- **`rowIndex % 2 == 0`** يتحقق ما إذا كان الصف زوجيًا.  
- **`Color.LightYellow`** يعطي لونًا هادئًا غير مزعج وهو مثالي لجداول البيانات.  
- **`BackgroundType.Solid`** يضمن أن التعبئة تغطي الخلية بالكامل، محققًا تأثير **set row background color**.  

يمكنك استبدال `Color.LightYellow` بأي ظل آخر (مثلاً `Color.LightCyan`) إذا كنت تفضل مظهرًا مختلفًا. نفس المنطق يتيح لك أيضًا **تلوين الصفوف بالتناوب** بناءً على معايير أخرى، مثل أعلام الحالة.

## الخطوة 4: استيراد DataTable إلى Worksheet مع الأنماط المُحضرة

أخيرًا، نقوم بإدخال كل شيء إلى الـ worksheet. معظم المكتبات توفر نسخة `ImportDataTable` التي تقبل مصفوفة نمط. العلامة `true` تخبر الـ API بكتابة رؤوس الأعمدة، وإحداثيات `0, 0` تبدأ من الخلية العليا اليسرى.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **النتيجة:** الآن يعرض الـ worksheet بياناتك بنمط **تظليل الصفوف المتناوب** نظيف — أصفر فاتح على الصفوف الزوجية، أبيض على الصفوف الفردية. يمكن للمستخدمين تصفح الشبكة دون أن تتقافز عيونهم ذهابًا وإيابًا.

### الناتج المتوقع
إذا فتحت جدول البيانات الناتج، سترى شيئًا مشابهًا لهذا:

| المعرف | الاسم | الكمية |
|--------|-------|--------|
| **1** | تفاح | 50 |
| **2** | موز | 30 |
| **3** | كرز | 20 |
| **4** | تمر | 15 |

الصفوف 1، 3، 5… لها **خلفية أصفر فاتح**، بينما الصفوف 2، 4، 6… تبقى **بيضاء**. صف الرأس (الصف 0) يرث النمط الافتراضي ما لم تقم بتخصيصه بشكل منفصل.

## البدائل الاختيارية وحالات الحافة

### 1. استخدام لوحة ألوان مختلفة
إذا كان الأصفر الفاتح يتعارض مع هوية علامتك التجارية، استبدل ببساطة `Color.LightYellow` بلون آخر من `System.Drawing.Color`. للحصول على ثيم أزرق‑رمادي يمكنك استخدام:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. تظليل ديناميكي بناءً على البيانات
أحيانًا تريد إبراز الصفوف التي تستوفي شرطًا معينًا (مثلاً المخزون المنخفض). اجمع فحص الـ modulo مع اختبار مخصص:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. تطبيق الأنماط على أعمدة محددة فقط
إذا كنت تحتاج فقط إلى **set row background color** على أعمدة معينة، أنشئ نمطًا منفصلًا لكل عمود وعيّنها بعد الاستيراد باستخدام API نطاق الخلايا للـ worksheet.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. نصيحة أداء للجداول الكبيرة
عند التعامل مع أكثر من 10,000 صف، فكر في إعادة استخدام كائن نمط واحد لكل لون بدلاً من إنشاء جديد لكل صف. ثم تحتفظ المصفوفة بمراجع إلى النمطين المشتركين، مما يقلل استهلاك الذاكرة بشكل كبير.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## مثال كامل يعمل
فيما يلي برنامج مستقل يمكنك لصقه في تطبيق Console. يستخدم API تخيلي `Workbook`/`Worksheet`؛ استبدل الأنواع بما يتناسب مع المكتبة التي اخترتها.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**الناتج:** ملف اسمه `AlternatingRows.xlsx` حيث يتناوب كل صف بين تعبئة أصفر فاتح وأبيض، مما يجعل الجدول أسهل للعين.

## الأسئلة المتكررة

**س: هل يعمل هذا النهج مع تنسيق الشرط على نمط Excel؟**  
ج: نعم. إذا كانت مكتبتك تدعم قواعد الشرط، يمكنك تحويل نفس المنطق إلى قاعدة تتحقق من `MOD(ROW(),2)=0`. الطريقة القائمة على الكود الموضحة هنا أكثر قابلية للنقل بين المكتبات التي لا تدعم تنسيق الشرط المدمج.

**س: ماذا لو احتجت إلى **تلوين الصفوف بالتناوب** في جدول PDF بدلاً من ورقة Excel؟**  
ج: معظم مولدات جداول PDF (مثل iTextSharp، PdfSharp) تسمح لك بتعيين `BackgroundColor` لكل صف. نفس حساب الـ modulo يُطبق—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}