---
category: general
date: 2026-02-26
description: Çalışma kitabını gömülü yazı tipleriyle PDF olarak dışa aktar ve ayrıca
  C#'ta grafikleri PowerPoint'e dışa aktar. Pivot tablo çalışma sayfasını kopyalamayı
  ve çalışma kitabını PPTX olarak kaydetmeyi öğrenin.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: tr
og_description: Gömülü yazı tipleriyle çalışma kitabını PDF olarak dışa aktar ve ayrıca
  C#'ta grafikleri PowerPoint'e dışa aktar. Pivot tablolarını kopyalamak ve PPTX olarak
  kaydetmek için adım adım kılavuzu izleyin.
og_title: Çalışma Kitabını PDF Olarak Dışa Aktarma – Tam C# Rehberi
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Çalışma Kitabını PDF'ye Dışa Aktarma – Tam C# Rehberi
url: /tr/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabını PDF Olarak Dışa Aktarma – Tam C# Kılavuzu

Çalışma kitabını PDF olarak dışa aktarmak, Excel yüklü olmayan paydaşlarla raporları paylaşmanız gerektiğinde yaygın bir gereksinimdir. Bu öğreticide ayrıca **grafikleri PowerPoint'e dışa aktarmayı**, bir **pivot tablo çalışma sayfasını kopyalamayı** ve PDF'nin ekranınızdaki tasarım gibi görünmesi için yazı tiplerini gömmeyi göstereceğiz.  

Bazı PDF'lerin orijinal düzeni kaybetmesinin ya da PowerPoint slaytlarının eksik şekillerle kalmasının nedenini hiç merak ettiniz mi? Cevap genellikle dışa aktarma sürecindeki eksik seçeneklerde yatar. Bu kılavuzun sonunda, tüm bu sorunları ele alan tek bir yeniden kullanılabilir C# yönteminize sahip olacaksınız—artık manuel kopyala‑yapıştır ya da dışa aktarma ayarlarıyla uğraşmak yok.

## Neler Öğreneceksiniz

- Bir çalışma kitabı oluşturmayı, Smart Marker ifadeleri eklemeyi ve bunları işlemeyi.  
- Veri kaynağını bozmadan **pivot tablo çalışma sayfasını kopyalamayı**.  
- **Grafikleri, şekilleri ve metin kutularını** düzenlenebilir tutarak bir PowerPoint sunumuna dışa aktarmayı.  
- PDF dışa aktarımı sırasında **standart yazı tiplerini gömmeyi**, her makinede tutarlı render sağlamak için.  
- `save workbook as pptx` yaklaşımını kullanarak **çalışma kitabını PPTX olarak kaydetmeyi**.

Bunların tümü, en son Aspose.Cells ve Aspose.Slides .NET kütüphaneleriyle (yazım anında sürüm 23.11) çalışır. Harici araçlar, post‑işleme betikleri yok—sadece saf C#.

> **Pro ipucu:** Projenizde zaten Aspose kullanıyorsanız, kod parçacıklarını olduğu gibi ekleyebilirsiniz; aksi takdirde önce NuGet paketlerini `Aspose.Cells` ve `Aspose.Slides` ekleyin.

## Önkoşullar

- .NET 6.0 veya üzeri (kod ayrıca .NET Framework 4.7.2'de de çalışır).  
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE).  
- NuGet üzerinden kurulu Aspose.Cells .NET ve Aspose.Slides .NET.  
- C# ve Smart Markers ve PivotTables gibi Excel kavramlarına temel aşinalık.

![Çalışma kitabını PDF olarak dışa aktarma diyagramı](export-workbook-to-pdf.png "PDF ve PPTX çıktıları gösteren çalışma kitabını PDF olarak dışa aktarma iş akışı")

## Çalışma Kitabını PDF Olarak Dışa Aktarma – Adım Adım Uygulama

Aşağıda tam, çalıştırmaya hazır örnek yer alıyor. Bir çalışma kitabı oluşturur, Smart Marker ifadelerini enjekte eder, bunları işler, bir pivot tablo aralığını kopyalar ve sonunda hem PDF hem de PowerPoint dosyasını kaydeder.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Neden Bu Çalışıyor

1. **Smart Marker işleme** sayesinde, döngü yazmadan çalışma kitabını herhangi bir veri kaynağından (JSON, DataTables vb.) doldurabilirsiniz.  
2. **DetailSheetNewName** her departman için ayrı bir sayfa oluşturur, size temiz, departmana özgü bir sekme sağlar.  
3. **Aralığı kopyalama** (`sourceRange.Copy`) pivot tabloyu *önbelleği dahil* çoğaltır, böylece kopyalanan sayfa orijinali gibi davranır.  
4. `ExportCharts`, `ExportShapes` ve `ExportTextBoxes` içeren **PresentationOptions**, Aspose'a bu nesneleri yerel PowerPoint öğeleri olarak render etmesini söyler ve düzenlenebilirliği korur.  
5. **PdfSaveOptions.EmbedStandardFonts**, orijinal yazı tipleri yüklü olmayan makinelerde PDF'nin aynı görünmesini sağlar.

Sonuç, `FinalReport.pdf` ve `FinalPresentation.pptx` adlı iki dosya olur; bu dosyalar e-posta ile gönderilebilir, arşivlenebilir veya herhangi bir görüntüleyicide kalite kaybı olmadan gösterilebilir.

## Grafikleri PowerPoint'e Dışa Aktarma (Çalışma Kitabını PPTX Olarak Kaydet)

Raporunuz grafikler içeriyorsa, muhtemelen bunların PowerPoint'te düzenlenebilir olmasını isteyeceksiniz. `PresentationOptions` sınıfı anahtar. İşte sadece grafik dışa aktarma kısmını gösteren odaklanmış bir kod parçacığı:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Arka planda ne olur?** Aspose, her Excel grafiğini yerel bir PowerPoint grafiğine dönüştürür, serileri, eksen başlıklarını ve biçimlendirmeyi korur. Bu, grafiği statik bir görüntü olarak dışa aktarmaktan çok daha iyidir, çünkü izleyicileriniz daha sonra veri noktalarını ayarlayabilir.

## Veri Kaybı Olmadan Pivot Tablo Çalışma Sayfasını Kopyalama

Pivot tablolar, gizli bir önbelleğe dayandıkları için dışa aktarmanın genellikle en zor kısmıdır. Basit `Copy` yöntemi çalışır çünkü Aspose, görünen aralığı **ve** altındaki önbellek nesnesini de kopyalar.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Not:** Aynı çalışma kitabı içinde yeni bir sayfada sadece pivot tabloya ihtiyacınız varsa, önceki `sourceRange.Copy` yaklaşımı daha hafiftir ve tamamen yeni bir çalışma kitabı oluşturmayı önler.

## PDF Dışa Aktarımı İçin Yazı Tiplerini Gömme – Neden Önemli

Orijinal yazı tiplerinin yüklü olmadığı bir makinede PDF açtığınızda, metin kayabilir, satır sonları değişebilir veya karakterler kaybolabilir. `EmbedStandardFonts = true` ayarı, Aspose'a en yaygın yazı tiplerini (Arial, Times New Roman vb.) doğrudan PDF akışına gömmesini söyler.

Özel yazı tipleri kullanıyorsanız, `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll` olarak değiştirin. İşte bir örnek:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Artık her alıcı, tasarladığınız aynı düzeni görür—sürpriz yok.

## Tam Çalışan Örnek Özeti

Her şeyi bir araya getirdiğimizde, önceki bölümde gösterilen tam program aşağıdakileri yapar:

1. **Smart Marker yer tutucularıyla** bir çalışma kitabı **oluşturur**.  
2. Yer tutucuları **işler**, departmana göre adlandırılmış bir detay sayfası üretir.  
3. Pivot tablo içeren bir aralığı yeni bir çalışma sayfasına **kopyalar**, işlevselliğini korur.  
4. Çalışma kitabını PowerPoint'e **dışa aktarır**, grafik, şekil ve metin kutularını düzenlenebilir tutar.  
5. Aynı çalışma kitabını PDF'ye **dışa aktarır**, güvenilir render için standart yazı tiplerini gömer.

Programı çalıştırın, oluşturulan dosyaları açın ve şunları göreceksiniz:

- **PDF**: Keskin tablolar, gömülü yazı tipleri ve Excel kaynağıyla aynı görsel stil.  
- **PowerPoint**: PowerPoint'te sağ‑tıklayıp → *Edit Data* (Veriyi Düzenle) yapabileceğiniz düzenlenebilir grafikler ve tamamen manipüle edilebilir şekiller.

---

## Sıkça Sorulan Sorular (SSS)

**S: Bu .NET Core ile çalışır mı?**  
Evet—Aspose.Cells ve Aspose.Slides çapraz platformdur. Sadece .NET 6 veya üzerini hedefleyin, aynı kod Windows, Linux veya macOS'ta çalışır.

**S: Yalnızca bir alt küme sayfayı dışa aktarmam gerekirse?**  
`Workbook.Save` metodunu, `SheetNames` belirtebilen `SaveOptions` ile kullanın. Örnek: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**S: PDF'yi şifreleyebilir miyim?**  
Kesinlikle. `Save` çağırmadan önce bir şifre ile `PdfSaveOptions.EncryptionDetails` ayarlayın.

**S: Pivot tablom dış bir veri kaynağı kullanıyor—kopyalama bağlantıyı kırar mı?**  
Kopyalama işlemi önbelleği içerir, dış bağlantıyı değil. Pivot tablo çevrim dışı çalışmaya devam eder, ancak orijinal kaynağa karşı yenilenmez. Canlı yenileme gerekiyorsa, kaynak veriyi çalışma kitabıyla birlikte dışa aktarın.

## Sonraki Adımlar ve İlgili Konular

- **Dinamik Veri Kaynakları** – Gerçek zamanlı raporlama için JSON veya DataTable'ı Smart Markers'a nasıl besleyeceğinizi öğrenin.  
- **Gelişmiş PDF Stilizasyonu** – Keşfedin `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}