---
category: general
date: 2026-09-24
description: تصدير نطاق إكسل كصورة في C# باستخدام Aspose.Cells – دليل خطوة بخطوة لحفظ
  منطقة ورقة العمل كملف PNG أو JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: ar
lastmod: 2026-09-24
og_description: تصدير نطاق إكسل كصورة في C# باستخدام Aspose.Cells. تعلّم كيفية تحويل
  أي منطقة في ورقة العمل، بما في ذلك جداول المحور، إلى PNG أو JPEG في دقائق.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: تصدير نطاق إكسل كصورة باستخدام C# – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: كيفية تصدير نطاق إكسل كصورة باستخدام C# و Aspose.Cells
url: /ar/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير نطاق إكسل كصورة باستخدام C# و Aspose.Cells

إذا كنت بحاجة إلى **تصدير نطاق إكسل كصورة** في تطبيق .NET، يوضح لك هذا الدليل حلاً كاملاً وجاهزًا للتنفيذ. سواءً كنت تنشر لوحة معلومات، أو تدمج جدولًا محوريًا في صفحة ويب، أو تنشئ صورة مصغرة لتقرير، يمكنك تحويل أي مساحة من ورقة العمل إلى PNG (أو JPEG) ببضع أسطر فقط من كود C#.

في هذا الدرس ستتعلم كيفية:

* تحميل دفتر عمل موجود (`Workbook` class)  
* تحديد النطاق الخلوي الدقيق الذي تريد التقاطه (`PrintArea`)  
* تكوين خيارات تصدير الصورة (`ImageOrPrintOptions`)  
* حفظ الصورة الناتجة على القرص  

جميع المتطلبات المسبقة، وحالات الحافة، والمشكلات الشائعة مغطاة بحيث يمكنك تعديل الكود لمشاريعك دون مفاجآت.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

| المتطلب | السبب |
|-------------|--------|
| **Aspose.Cells for .NET** (أحدث نسخة) | يوفر واجهات `Workbook` و `Worksheet` و `ImageOrPrintOptions` المستخدمة في المثال. |
| **.NET 6.0 أو أحدث** | العينة تستهدف .NET 6، لكن أي نسخة من .NET Core/Framework تدعم Aspose.Cells تعمل. |
| **ملف إكسل صالح** (مثال: `input.xlsx`) | دفتر العمل الذي تريد تحويله. |
| **صلاحية كتابة إلى مجلد الإخراج** | مطلوب لكي ينجح الأمر `Save`. |

يمكنك تثبيت Aspose.Cells عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

## تصدير نطاق إكسل كصورة – نظرة عامة على العملية

تتكون العملية من ثلاث مراحل منطقية:

1. **تحميل** دفتر العمل من القرص.  
2. **تحديد** مساحة الخلايا التي ستصبح الصورة (*منطقة الطباعة*).  
3. **تصدير** المنطقة باستخدام `ImageOrPrintOptions` وكتابة الملف.

فيما يلي تفصيل كل مرحلة إلى خطوة مخصصة مع الكود الكامل والشرح.

## الخطوة 1: تحميل دفتر العمل

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**لماذا هذا مهم:**  
`Workbook` هو نقطة الدخول لجميع عمليات إكسل. تحميل الملف مرة واحدة يقلل من استهلاك الذاكرة ويسمح لك بالوصول إلى أي ورقة عمل لاحقًا.

## الخطوة 2: الوصول إلى ورقة العمل المستهدفة

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**نصيحة:** إذا كنت بحاجة إلى ورقة معينة بالاسم، استبدل الفهرس بـ `workbook.Worksheets["SheetName"]`. هذا يتجنب الأخطاء عندما يتغير تخطيط دفتر العمل.

## الخطوة 3: تحديد النطاق الذي تريد تصديره

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**لماذا نحدد `PrintArea`؟**  
Aspose.Cells يقوم برندر *منطقة الطباعة* عند إنشاء الصورة. بتقييدها إلى النطاق الدقيق، تتجنب المساحات الفارغة الزائدة وتحسن الأداء.

### بديل: تصدير الورقة بالكامل

إذا كنت تريد تصدير كامل ورقة العمل، ببساطة احذف تعيين `PrintArea`. سيستخدم Aspose.Cells النطاق المستخدم في الورقة بشكل افتراضي.

## الخطوة 4: تكوين خيارات تصدير الصورة

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**شرح الخصائص الرئيسية:**

* `ImageFormat` – يحدد نوع الملف (`Png`, `Jpeg`, `Bmp`, إلخ). PNG مثالي للمخططات والنص لأنه يحافظ على الحواف الواضحة.  
* `HorizontalResolution` / `VerticalResolution` – يتحكمان في كثافة البكسل. للصور المصغرة على الويب 96 DPI كافية؛ للرسومات الجاهزة للطباعة يوصى بـ 300 DPI.  
* `PageOrientation` – يساعد عندما يكون النطاق المختار أوسع من ارتفاعه.

## الخطوة 5: تصدير النطاق إلى ملف صورة

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**ما يحدث في الخلفية:**  
عند ضبط `PrintArea`، يقوم Aspose.Cells بإنشاء صورة مؤقتة تمثل تلك المنطقة. ثم يتم حفظ كائن `Pictures[0]` باستخدام الخيارات التي حددتها.

### معالجة أوراق العمل بدون صور

إذا لم تحتوي ورقة العمل على صورة بالفعل (مثال: ملف جديد تمامًا)، يمكنك إنشاء واحدة مباشرةً:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك تطبيق console مستقل يمكنك نسخه، لصقه، وتشغيله:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**الناتج المتوقع:**  
يظهر ملف باسم `range.png` في `YOUR_DIRECTORY`. عند فتحه ستظهر الخلايا من **A1 إلى G20** مُرَسَّمة كصورة PNG واضحة.

## تنويعات شائعة ومعالجة حالات الحافة

| السيناريو | التعديل |
|----------|------------|
| **تصدير إلى JPEG** | غيّر `ImageFormat = ImageFormat.Jpeg` ويمكنك أيضًا ضبط `Quality = 90` (النطاق 0‑100). |
| **نطاقات متعددة** | استدعِ `sheet.Pictures.Add` لكل نطاق واحفظ كل صورة باسم ملف مميز. |
| **أوراق عمل كبيرة** | زد `HorizontalResolution`/`VerticalResolution` فقط للنطاق المطلوب لتجنب ارتفاع استهلاك الذاكرة. |
| **عدم توليد صورة** | تأكد من أن `PrintArea` مُنسَّقة بشكل صحيح (`"A1:G20"`). العنوان غير صالح ينتج مجموعة `Pictures` فارغة. |
| **الحفظ إلى تدفق (Stream)** | استخدم `pic.Save(Stream, imgOptions)` عندما تحتاج الصورة في الذاكرة (مثال: لاستجابة ASP.NET). |

## نصائح احترافية لتصدير الصور بشكل موثوق

* **تحقق من صحة منطقة الطباعة** – استخدم تحليل `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) لبناء النطاقات برمجيًا وتجنب الأخطاء الإملائية.  
* **تحرير الموارد** – ضع `Workbook` داخل كتلة `using` إذا كنت تعالج ملفات متعددة لتحرير الموارد الأصلية بسرعة.  
* **المعالجة الدفعية** – عند تصدير عشرات النطاقات، أعد استخدام نفس كائن `ImageOrPrintOptions` لتقليل استهلاك الذاكرة.  
* **سلامة الخيوط** – كائنات Aspose.Cells **ليست** آمنة للاستخدام المتعدد الخيوط. أنشئ `Workbook` منفصل لكل خيط أو قم بمزامنة الوصول.

## الخاتمة

أصبح لديك الآن طريقة كاملة وجاهزة للإنتاج **لتصدير نطاق إكسل كصورة** باستخدام C# و Aspose.Cells. تغطي الخطوات—تحميل دفتر العمل، ضبط منطقة الطباعة، تكوين `ImageOrPrintOptions`، وحفظ الصورة—كل من “كيفية” و“لماذا”، مما يضمن قدرتك على تعديل الكود لجداول محورية، مخططات، أو أي كتلة خلايا مخصصة.

بعد ذلك، قد ترغب في استكشاف:

* **تصدير نطاق إكسل كصورة** بصيغ أخرى (SVG, BMP) – كلمة مفتاحية ثانوية أخرى لتجربتها.  
* **دمج PNG في PDF** باستخدام Aspose.PDF لإنشاء تقارير شاملة من البداية إلى النهاية.  
* **أتمتة تصدير دفعات** عبر عدة دفاتر عمل باستخدام حلقة console بسيطة.

لا تتردد في تجربة دقات مختلفة، واتجاهات، ومجلدات إخراج. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تصدير خلايا إكسل إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [تصدير دفتر عمل إكسل كصورة باستخدام Aspose.Cells للـ Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [كيفية تصدير ورقة عمل إكسل إلى PNG باستخدام Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}