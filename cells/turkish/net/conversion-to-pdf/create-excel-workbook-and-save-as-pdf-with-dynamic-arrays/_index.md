---
category: general
date: 2026-09-15
description: C#'ta Excel çalışma kitabı oluşturun ve EXPAND işlevini kullanarak dinamik
  dizileri yayarken çalışma kitabını PDF olarak kaydetmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: tr
lastmod: 2026-09-15
og_description: C#'ta Excel çalışma kitabı oluşturun ve dinamik bir dizi yaymak için
  EXPAND işlevini kullanarak çalışma kitabını hızlıca PDF olarak kaydedin.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Excel çalışma kitabı oluştur ve dinamik dizilerle PDF olarak kaydet
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Excel çalışma kitabı oluştur ve dinamik dizilerle PDF olarak kaydet
url: /tr/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabı oluşturun ve dinamik dizileri PDF olarak kaydedin

Programlı olarak **Excel çalışma kitabı oluşturmanız** ve ardından **çalışma kitabını PDF olarak kaydetmeniz** gerektiğinde, bu kılavuz C# içinde tam bir uçtan‑uca çözüm gösterir. Ayrıca **EXPAND işlevi**ni kullanarak **dinamik dizi sonuçlarını yayma** (spill) nasıl yapılır, VBA olmadan diziler oluşturmanın modern yolunu da göreceksiniz.  

Raporlama servisi, bir ERP sistemi için dışa aktarma özelliği veya veri‑odaklı bir gösterge paneli oluşturuyor olun, aşağıdaki adımlar bir çalışma kitabı üretmenizi, akıllı‑işaretçi (Smart‑Marker) verileriyle doldurmanızı ve gelişmiş yazı tipi özelliklerini koruyan bir PDF üretmenizi sağlar.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.8 ile de çalışır)
* **Aspose.Cells for .NET**’in son sürümü (v25.8 veya üzeri) – `Workbook`, `PdfSaveOptions` ve `SmartMarkerProcessor` sağlar.
* Visual Studio 2022 gibi bir IDE (C# derleyebilen herhangi bir editör yeterlidir).

Projeye NuGet paketini ekleyin:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Adım 1: Excel çalışma kitabı oluşturun ve ilk çalışma sayfasını ayarlayın

İlk görev **Excel çalışma kitabı oluşturmak** ve varsayılan çalışma sayfasına bir referans almaktır. Bu sayfa dinamik dizi ve Smart Marker şablonunu barındıracaktır.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Neden önemli*: `Workbook` nesnesini örneklemek iç çalışma kitabı yapısını tahsis eder, `Worksheets[0]`a erişmek ise manuel olarak bir sayfa eklemenize gerek kalmadan hazır bir sayfa verir.

## Adım 2: EXPAND işleviyle dinamik dizi yayma

Excel’in **EXPAND işlevi**, statik bir dizi literalini istediğiniz boyutta bir yayma aralığına dönüştürebilir. Burada `{1,2,3}` dizisini `A1` hücresinden başlayan 5 satır × 1 sütunluk bir aralığa genişletmesini istiyoruz.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Neden önemli*: `EXPAND` kullanmak C# içinde manuel döngülerden kaçınmanızı sağlar. Motor yayma aralığını hesaplar ve değerleri doğrudan çalışma sayfasına yazar; bu değerler daha sonra PDF’de görünür.

## Adım 3: Çalışma kitabını PDF olarak kaydederken yazı tipi varyasyon seçicilerini koruyun

**Çalışma kitabını PDF olarak kaydetmeniz** gerektiğinde, aynı zamanda gelişmiş tipografik özellikleri (ör. yazı tipi varyasyon seçicileri – Aspose.Cells v25.8’den itibaren mevcut) etkinleştirebilirsiniz. Bu, PDF’lerin karmaşık betikleri doğru şekilde görüntülemesini sağlar.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Neden önemli*: `FontVariationSelectors` değerini `true` yapmak, glif varyasyonuna (ör. Çince, Japonca, emoji) dayanan diller için şarttır. Oluşturulan PDF, ekrandaki Excel görünümünü yansıtır.

## Adım 4: İç içe veri kaynağına başvuran bir Smart Marker şablonu ekleyin

Smart Marker’lar, yer tutucuları doğrudan çalışma sayfasına gömmenizi sağlar. Aşağıdaki şablon, siparişlerin ve onların öğelerinin bir listesini oluşturacaktır.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Neden önemli*: Şablonu `A1` hücresine yerleştirerek Aspose.Cells’e veriyi nereden genişletmeye başlayacağını söylersiniz. `:` sözdizimi (`Items:ItemName`) işlemciye iç içe bir koleksiyon üzerinde yineleme yapmasını söyler.

## Adım 5: İç içe veri kaynağını tanımlayın (öğeler içeren siparişler)

Her biri kendi öğe koleksiyonuna sahip siparişlerden oluşan anonim bir dizi oluşturuyoruz. Bu, tipik bir master‑detail senaryosunu yansıtır.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Neden önemli*: İç içe yapı, **Excel’de dinamik dizi oluşturmanın** Smart Marker aracılığıyla nasıl yapılacağını gösterir; hiçbir VBA ya da manuel hücre döngüsü yazmanıza gerek kalmaz.

## Adım 6: Smart Marker’ları işleyin ve son Excel dosyasını kaydedin

Şimdi çalışma kitabını ve veri kaynağını `SmartMarkerProcessor`a veriyoruz. İşleme sonrası yer tutucular gerçek satırlarla değiştirilir ve sonuç normal bir `.xlsx` dosyası olarak kaydedilir.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Neden önemli*: `SmartMarkerProcessor` şablonu otomatik olarak genişletir, gerekli satırları oluşturur ve verilerle doldurur. Son çalışma kitabı Excel’de açılarak her siparişin ve öğelerinin doğru şekilde göründüğü doğrulanabilir.

## Beklenen çıktı

* **VarSelector.pdf** – 1‑3 sayılarının beş satıra yayılması gösteren, etkinleştirdiğiniz OpenType yazı tipi varyasyonlarıyla render edilen bir PDF dosyası.
* **NestedSmartMarker.xlsx** – aşağıdaki satırları içeren bir Excel dosyası (`A1`’den başlar):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF sürümü aynı sayısal yaymayı korur çünkü çalışma sayfası durumu Smart Marker işlenmeden önce kaydedilmiştir; isterseniz işleme sonrası da PDF kaydedebilirsiniz.

## Profesyonel ipuçları ve yaygın hatalar

| İpucu | Açıklama |
|-----|-------------|
| **Aynı `PdfSaveOptions` nesnesini yeniden kullanın** | Seçenek nesnesini bir kez oluşturup yeniden kullanmak, (ör. eksik varyasyon seçicileri) gibi ince render farklarını önler. |
| **Formülleri ayarladıktan sonra `ws.Calculate()` çağırın** | Açık bir hesaplama yapılmazsa, yayma aralığı programatik olarak çalışma kitabını incelediğinizde boş kalabilir. |
| **Smart Marker şablonlarını temiz bir sayfaya yerleştirin** | Şablonları mevcut verilerle karıştırmak beklenmedik satır eklemelerine yol açabilir. Mümkünse ayrı bir sayfa kullanın. |
| **Dosya yollarına dikkat edin** | `Path.Combine(Environment.CurrentDirectory, "output.pdf")` kullanarak farklı makinelerde sabit dizinlerden kaçının. |
| **Sürüm kontrolü** | `FontVariationSelectors` yalnızca 25.8 ve üzeri sürümlerde mevcuttur; eski sürümler özelliği yoksayar ve hata vermez. |

## Sonraki adımlar

Artık **Excel çalışma kitabı oluşturmayı**, **dinamik dizi yaymayı** ve **çalışma kitabını PDF olarak kaydetmeyi** bildiğinize göre şunları keşfedebilirsiniz:

* PDF dönüşümünden önce grafikler veya resimler eklemek.
* `Save` aşırı yüklemelerini kullanarak aynı çalışma kitabını diğer formatlara (ör. HTML, CSV) dışa aktarmak.
* **Smart Marker ifadeleri** (`${Orders.Total:SUM(Items.Price)}`) ile anlık toplamlar hesaplamak.
* Bu kodu bir ASP.NET Core API’ye entegre ederek kullanıcıların üretilen PDF’yi doğrudan bir web uç noktasından indirmesini sağlamak.

---

**Özet** – Bu öğreticide **Excel çalışma kitabı oluşturmayı**, **EXPAND işlevi**yle **dinamik dizi yaymayı**, iç içe veri kaynağıyla çalışan bir **Smart Marker** eklemeyi ve son olarak gelişmiş yazı tipi özelliklerini koruyarak **çalışma kitabını PDF olarak kaydetmeyi** gösterdik. Tam, çalıştırılabilir örnek herhangi bir C# projesine kopyalanıp kendi veri yapılarınıza uyarlanabilir. Kodlamanın tadını çıkarın!


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}