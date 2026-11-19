---
category: general
date: 2026-11-19
description: Dizi verileriyle Excel doldurulurken çalışma sayfasını nasıl tekrarlayacağınızı
  öğrenin. Birkaç adımda birden fazla çalışma sayfası oluşturmayı ve çalışma sayfasını
  listeden doldurmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: tr
lastmod: 2026-11-19
og_description: SmartMarkerProcessor kullanarak çalışma sayfasını nasıl tekrar ederiz.
  Bu kılavuzu izleyerek Excel'i dizi verileriyle doldurun, birden fazla çalışma sayfası
  oluşturun ve çalışma sayfasını listeden doldurun.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Excel'de Çalışma Sayfasını Tekrarlama – Adım Adım Rehber
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: SmartMarkerProcessor ile Excel’de çalışma sayfasını nasıl tekrarlarsınız?
url: /tr/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de SmartMarkerProcessor ile Çalışma Sayfasını Tekrarlama

If you need to **how to repeat worksheet** when generating Excel reports, this guide shows you a complete, runnable solution. By the end of the tutorial you’ll be able to **populate Excel with array** data, **generate multiple worksheets**, and **populate worksheet from list** using the SmartMarkerProcessor library.

Excel raporları oluştururken **how to repeat worksheet** ihtiyacınız varsa, bu rehber size eksiksiz, çalıştırılabilir bir çözüm gösterir. Eğitim sonunda **populate Excel with array** verileriyle Excel'i doldurabilecek, **generate multiple worksheets** oluşturabilecek ve SmartMarkerProcessor kütüphanesini kullanarak **populate worksheet from list** yapabileceksiniz.

Repeating a worksheet is a common requirement when each department, region, or time period needs its own tab. The example below demonstrates the exact steps, explains why each setting matters, and covers edge cases such as empty lists or custom naming.

Bir çalışma sayfasını tekrarlamak, her departman, bölge veya zaman diliminin kendi sekmesine ihtiyaç duyduğu durumlarda yaygın bir gereksinimdir. Aşağıdaki örnek tam adımları gösterir, her ayarın neden önemli olduğunu açıklar ve boş listeler veya özel adlandırma gibi uç durumları kapsar.

## Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm yüklü
- `SmartMarkerProcessor` içeren **GroupDocs.Viewer** (veya eşdeğeri) NuGet paketine referans
- `${repeat:Dept}` gibi bir işaretçi satırına yerleştirilmiş bir Excel şablon çalışma kitabı (`.xlsx`)
- C# ve LINQ konusunda temel bilgi (isteğe bağlı ancak faydalı)

Ek üçüncü‑taraf kütüphanelerine ihtiyaç yoktur.

## Adım 1: SmartMarkerProcessor örneğini oluşturma

The processor orchestrates the marker replacement and worksheet duplication. Instantiating it without arguments uses the default options.

İşlemci, işaretçi değişimini ve çalışma sayfası çoğaltılmasını yönetir. Argümansız oluşturulduğunda varsayılan seçenekler kullanılır.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Creating the processor early lets you configure global options before any data is applied. This is the foundation for **how to repeat worksheet** correctly.

İşlemciyi erken oluşturmak, herhangi bir veri uygulanmadan önce global seçenekleri yapılandırmanıza olanak tanır. Bu, **how to repeat worksheet** doğru bir şekilde yapmanın temelidir.

## Adım 2: Çalışma sayfası tekrarlamayı etkinleştirme

By default the processor replaces markers on the current sheet only. Setting `RepeatWorksheet` to `true` tells the engine to clone the entire worksheet for each item in the data collection.

Varsayılan olarak işlemci, işaretçileri yalnızca mevcut sayfada değiştirir. `RepeatWorksheet` seçeneğini `true` olarak ayarlamak, motorun veri koleksiyonundaki her öğe için tüm çalışma sayfasını kopyalamasını sağlar.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Enabling this option is the key to **generate multiple worksheets**—the processor will create a new tab for every element in the `Dept` array and keep the original formatting.

Bu seçeneği etkinleştirmek, **generate multiple worksheets** için anahtardır—işlemci, `Dept` dizisindeki her öğe için yeni bir sekme oluşturur ve orijinal biçimlendirmeyi korur.

## Adım 3: Veri kaynağını dizi veya liste olarak hazırlama

SmartMarkerProcessor works with any enumerable, but using an array makes the intent clear when you want to **populate worksheet from list**. Here we create an anonymous object that contains a `Dept` property holding a string array.

SmartMarkerProcessor herhangi bir enumerable ile çalışır, ancak bir dizi kullanmak, **populate worksheet from list** istediğinizde niyeti netleştirir. Burada, `Dept` özelliği içinde bir string dizisi tutan anonim bir nesne oluşturuyoruz.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

If you already have a `List<string>` you can pass it directly; the processor will treat it the same way. The important part is that the property name (`Dept`) matches the marker `${repeat:Dept}` in the template.

Eğer zaten bir `List<string>`'iniz varsa doğrudan geçirebilirsiniz; işlemci aynı şekilde ele alır. Önemli olan, özellik adının (`Dept`) şablondaki `${repeat:Dept}` işaretçisiyle eşleşmesidir.

## Adım 4: Şablon çalışma sayfasını yükleme

Assuming you have an `ExcelPackage` (from EPPlus) or a `Workbook` object, retrieve the worksheet you want to repeat. The variable `ws` represents that sheet.

Bir `ExcelPackage` (EPPlus'tan) veya bir `Workbook` nesnesine sahip olduğunuzu varsayarak, tekrarlamak istediğiniz çalışma sayfasını alın. `ws` değişkeni bu sayfayı temsil eder.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

If you prefer a different library (e.g., ClosedXML), the same principle applies: obtain a worksheet object that implements the required interface.

Farklı bir kütüphane (ör. ClosedXML) tercih ediyorsanız, aynı prensip geçerlidir: gerekli arayüzü uygulayan bir çalışma sayfası nesnesi elde edin.

## Adım 5: Çalışma sayfasını veri ile işleme

Now apply the data to the template. The processor clones the worksheet for each department, replaces the `${repeat:Dept}` marker with the actual department name, and leaves the rest of the sheet untouched.

Şimdi veriyi şablona uygulayın. İşlemci, her departman için çalışma sayfasını kopyalar, `${repeat:Dept}` işaretçisini gerçek departman adıyla değiştirir ve sayfanın geri kalanını dokunulmamış bırakır.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

After `Process` completes, `ws` becomes the first of several worksheets—one per department. The original sheet’s name is preserved, while the duplicates receive incremental suffixes (e.g., “Sheet1 (1)”, “Sheet1 (2)”). You can rename them afterward if you need a custom naming scheme.

`Process` tamamlandıktan sonra, `ws` birkaç çalışma sayfasından ilkine dönüşür—her departman için bir tane. Orijinal sayfanın adı korunur, kopyalar ise artan ekler alır (ör. “Sheet1 (1)”, “Sheet1 (2)”). Özel bir adlandırma şeması gerekiyorsa, sonradan yeniden adlandırabilirsiniz.

### Beklenen çıktı

When you open the resulting workbook, you should see:

Oluşturulan çalışma kitabını açtığınızda şunları görmelisiniz:

- **Sheet1** – orijinal şablon (genellikle boş bırakılır veya ana şablon olarak kullanılır)
- **Sheet1 (1)** – “HR” ile doldurulmuş
- **Sheet1 (2)** – “IT” ile doldurulmuş
- **Sheet1 (3)** – “Finance” ile doldurulmuş

Each sheet contains the same layout but with the department name substituted where `${repeat:Dept}` appeared.

Her sayfa aynı düzeni içerir ancak `${repeat:Dept}` göründüğü yerde departman adı yer alır.

## Kenar durumlarını ele alma

### Boş veya null diziler

If `Dept` is null or empty, the processor will not create any additional worksheets. To avoid a completely blank workbook, you can add a guard:

`Dept` null veya boş ise, işlemci ek çalışma sayfası oluşturmaz. Tamamen boş bir çalışma kitabını önlemek için bir koruma ekleyebilirsiniz:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Özel çalışma sayfası adları

The default naming scheme may not suit every reporting requirement. After processing, rename each sheet using a loop:

Varsayılan adlandırma şeması her raporlama ihtiyacına uymayabilir. İşlemden sonra, bir döngü kullanarak her sayfayı yeniden adlandırın:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Ek sütunları doldurma

If you need to **populate excel with array** values beyond a single marker, extend the data object:

Tek bir işaretçinin ötesinde **populate excel with array** değerlerine ihtiyacınız varsa, veri nesnesini genişletin:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Then adjust the template markers to `${repeat:Dept.Name}` and `${repeat:Dept.Headcount}`. The processor will repeat the row for each department and fill both columns.

Ardından şablon işaretçilerini `${repeat:Dept.Name}` ve `${repeat:Dept.Headcount}` olarak ayarlayın. İşlemci, her departman için satırı tekrar eder ve her iki sütunu da doldurur.

## Tam çalışan örnek

Below is a self‑contained console application that demonstrates the entire flow from template loading to saving the final workbook.

Aşağıda, şablon yüklemeden son çalışma kitabını kaydetmeye kadar tüm akışı gösteren bağımsız bir konsol uygulaması bulunmaktadır.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Ana bölümlerin açıklaması**

- **Processor creation** – işaretçileri yorumlayacak motoru kurar.
- **RepeatWorksheet option** – *how to repeat worksheet* sorusuna yanıt veren temel özelliği etkinleştirir.
- **Data source** – **populate excel with array** gereksinimini karşılamak için bir dizi (`new[]`) kullanır.
- **Template loading** – bir çalışma sayfası nesnesi elde etmenin yaygın bir yolunu gösterir.
- **Processing** – çoğaltma ve veri eklemeyi tek bir çağrıda gerçekleştirir.
- **Renaming** – genel “(1)”, “(2)” adlarını anlamlı başlıklara dönüştürmeyi gösterir; bu, **generate multiple worksheets** sonrasında tipik bir gereksinimdir.

Running this program produces `Result.xlsx` with three department‑specific tabs, each populated from the array.

Bu programı çalıştırdığınızda, dizi üzerinden doldurulmuş üç departmana özgü sekme içeren `Result.xlsx` oluşturulur.

## Yaygın tuzaklar ve profesyonel ipuçları

- **Marker spelling** – işaretçi, özellik adıyla tam olarak eşleşmelidir (`${repeat:Dept}`). Bir yazım hatası tekrarı engeller.
- **Worksheet index** – işlemden sonra, orijinal sayfa indeks 0'da kalır; oluşturulan sayfalar sırasıyla eklenir. Yanlış indeksleme, yanlış sekmenin yeniden adlandırılmasına yol açabilir.
- **Large data sets** – yüzlerce çalışma sayfası oluşturmak dosya boyutunu büyük ölçüde artırabilir. Performans sorunu ortaya çıkarsa raporları bölmeyi veya gruplanmış bölümlerle tek bir sayfa kullanmayı düşünün.
- **Thread safety** – `SmartMarkerProcessor` iş parçacığı‑güvenli değildir. Paralel olarak birden fazla çalışma kitabı işliyorsanız, her iş parçacığı için ayrı bir örnek oluşturun.

## Sonuç

Artık SmartMarkerProcessor kullanarak Excel'de **how to repeat worksheet**, **populate excel with array** verileriyle doldurma, **generate multiple worksheets** oluşturma ve **populate worksheet from list** verimli bir şekilde yapma konularını biliyorsunuz. Tam örnek tüm kavramları birleştirir ve isteğe bağlı yeniden adlandırma adımı, temiz ve kullanıcı‑dostu sekme adları üretmenizi sağlar.

Sonraki adımda şunları keşfedebilirsiniz:

- **populate worksheet from list** kullanarak karmaşık nesneler (iç içe koleksiyonlar) ile çalışmak
- Çalışma sayfası çoğaltmadan sonra koşullu biçimlendirme uygulamak
- Oluşturulan çalışma kitabını PDF veya CSV'ye dışa aktararak sonraki tüketim için kullanmak

Kodu kendi raporlama senaryolarınıza göre uyarlamaktan çekinmeyin ve Excel çalışma kitaplarını otomatikleştirmenin keyfini güvenle çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanarak ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Çalışma Sayfalarını Tekrarlama – Excel Otomasyonu için Tam Kılavuz](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Öğe Başına Çalışma Sayfası Oluşturma – C#'ta Çalışma Sayfasını Tekrarlama](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Excel'de diziyi genişletme ve bir şablonu doldurma](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}