---
title: تحريك الصف الأول للأسفل عند إدراج صفوف جدول البيانات في Excel
linktitle: تحريك الصف الأول للأسفل عند إدراج صفوف جدول البيانات في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعلم كيفية إدراج صفوف جدول البيانات في Excel دون تحريك الصف الأول لأسفل باستخدام Aspose.Cells for .NET. دليل خطوة بخطوة للأتمتة السهلة.
weight: 11
url: /ar/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحريك الصف الأول للأسفل عند إدراج صفوف جدول البيانات في Excel

## مقدمة

هل سئمت من تحويل الصفوف يدويًا عند إدخال بيانات جديدة في جداول بيانات Excel؟ حسنًا، أنت محظوظ! في هذه المقالة، سنتعمق في كيفية أتمتة هذه العملية باستخدام Aspose.Cells for .NET. بحلول نهاية هذا البرنامج التعليمي، لن تتعلم فقط كيفية العمل مع جداول البيانات في Excel، بل ستتعلم أيضًا كيفية تخصيص خيارات الاستيراد لتناسب احتياجاتك بشكل أفضل. صدقني؛ يمكن أن يوفر لك هذا الكثير من الوقت والمتاعب! لذا، تناول كوبًا من القهوة، ولنبدأ!

## المتطلبات الأساسية

قبل أن ننتقل إلى الترميز، دعنا نتأكد من إعداد كل شيء:

1. Visual Studio: تأكد من تثبيت Visual Studio (يجب أن يعمل الإصدار 2017 أو الأحدث بشكل جيد).
2.  Aspose.Cells لـ .NET: يجب أن يكون لديك مكتبة Aspose.Cells. إذا لم تقم بذلك بعد، فيمكنك تنزيلها[هنا](https://releases.aspose.com/cells/net/).
3. الفهم الأساسي لـ C# وExcel: إن الفهم الأساسي لبرمجة C# وكيفية عمل Excel سيساعدك بالتأكيد على المتابعة بشكل أكثر فعالية.

 ستحتاج أيضًا إلى الاحتفاظ بملف Excel نموذجي في متناول يدك. في هذا الدليل، سنستخدم نموذجًا يسمى`sampleImportTableOptionsShiftFirstRowDown.xlsx`يمكنك إنشاء هذا الملف أو العثور على قالب يناسب احتياجاتك.

## استيراد الحزم

قبل أن نتعمق في البرمجة، نحتاج إلى التأكد من استيراد الحزم اللازمة. في مشروع C# الخاص بك، قم بتضمين المساحات التالية:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

تُعد هذه الحزم ضرورية للعمل مع المصنف وأوراق العمل والجداول.

## الخطوة 1: إعداد مشروعك

### إنشاء مشروع C# جديد

ابدأ بإنشاء تطبيق وحدة تحكم C# جديد في Visual Studio. أعطِ مشروعك اسمًا مناسبًا، مثل "ExcelDataImport".

### إضافة حزمة Aspose.Cells NuGet

لإضافة حزمة Aspose.Cells، انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول، وحدد إدارة حزم NuGet، وابحث عن "Aspose.Cells". قم بتثبيت الحزمة للتأكد من إمكانية الوصول إلى جميع الوظائف التي نحتاجها.

## الخطوة 2: تحديد جدول البيانات

 بعد ذلك، سوف نقوم بتنفيذ`ICellsDataTable` واجهة لإنشاء فئة توفر البيانات المراد استيرادها. إليك كيفية هيكلة`CellsDataTable` فصل:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... تنفيذ الأعضاء الآخرين ...
}
```

هنا، نقوم بتعريف أسماء الأعمدة والبيانات لكل عمود، مما يسهل هيكلة الجدول المستورد لدينا.

## الخطوة 3: تنفيذ عناصر واجهة ICellsDataTable

 في غضون`CellsDataTable` الصف، تحتاج إلى تنفيذ أعضاء`ICellsDataTable` الواجهة. فيما يلي التنفيذ المطلوب:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

يتعامل هذا الجزء من الفصل مع استرجاع البيانات، وتحديد عدد الصفوف والأعمدة، وإدارة حالة الفهرس الحالية.

## الخطوة 4: كتابة الدالة الرئيسية

 الآن، دعونا ننشئ`Run`الطريقة لتنظيم عملية استيراد الجدول بأكملها:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## الخطوة 5: تعيين خيارات الاستيراد

 للتحكم في سلوك الاستيراد، يجب عليك إنشاء مثيل لـ`ImportTableOptions` وضبط الخصائص وفقًا لذلك. على وجه التحديد، نريد ضبط`ShiftFirstRowDown` ل`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // نحن لا نريد تحريك الصف الأول إلى الأسفل
```

## الخطوة 6: استيراد جدول البيانات

 الآن يمكننا استيراد البيانات من`CellsDataTable` في ورقة العمل.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

سيقوم هذا الأمر بإدراج جدول البيانات الخاص بك مباشرةً بدءًا من الصف والعمود المحددين.

## الخطوة 7: احفظ المصنف

وأخيرًا، سنقوم بحفظ المصنف المعدّل في ملف مرة أخرى:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## خاتمة

والآن، لقد تعلمت كيفية إدراج صفوف جدول البيانات في ورقة Excel دون تحريك الصف الأول باستخدام Aspose.Cells for .NET. لا تعمل هذه العملية على تبسيط معالجة البيانات داخل Excel فحسب، بل تعمل أيضًا على تحسين أداء تطبيقك من خلال أتمتة مهمة مرهقة عادةً. وبفضل هذه المعرفة في مجموعة أدواتك، أصبحت مجهزًا بشكل أفضل للتعامل مع مهام أتمتة Excel، مما يوفر لك الوقت والجهد.

## الأسئلة الشائعة

### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells for .NET هي مكتبة برمجة تتيح للمطورين إنشاء ملفات Excel ومعالجتها وتحويلها في تطبيقات .NET.

### هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟
نعم، ستحتاج إلى ترخيص صالح للاستفادة من الميزات الكاملة. ومع ذلك، تتوفر نسخة تجريبية مجانية للاختبار الأولي.

### هل يمكنني استخدام Aspose.Cells في تطبيقات الويب؟
بالتأكيد! Aspose.Cells مثالي لتطبيقات سطح المكتب والويب والسحابة الإلكترونية التي تم تطويرها باستخدام .NET.

### ما هي أنواع ملفات Excel التي يمكنني إنشاؤها باستخدام Aspose.Cells؟
يمكنك إنشاء مجموعة متنوعة من تنسيقات ملفات Excel، بما في ذلك XLSX، وXLS، وCSV، والمزيد.

### أين يمكنني الحصول على الدعم لـ Aspose.Cells؟
 يمكنك طرح الأسئلة أو العثور على المساعدة في[منتديات اسبوس](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
