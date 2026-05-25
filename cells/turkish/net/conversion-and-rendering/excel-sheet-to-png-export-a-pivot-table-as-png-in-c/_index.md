---
category: general
date: 2026-03-18
description: Aspose.Cells kullanarak pivot tabloyu dışa aktarma, baskı alanı pivotunu
  ayarlama ve Excel aralığını resim olarak dışa aktarma adımlarını gösteren Excel
  sayfasını PNG'ye dönüştürme öğreticisi.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: tr
og_description: Excel sayfasını PNG'ye dönüştürme öğreticisi; pivot tabloları dışa
  aktarma, yazdırma alanı pivotunu ayarlama ve C# ile Excel aralığı görüntüsünü dışa
  aktarma adımlarını size gösterir.
og_title: Excel sayfasını PNG'ye Dönüştür – Pivot Tabloları Dışa Aktarma Tam Kılavuzu
tags:
- Aspose.Cells
- C#
- Excel automation
title: excel sayfasını png'ye – Pivot Tablosunu C#'ta PNG olarak dışa aktar
url: /tr/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sayfasını png’ye – Pivot Tablosunu C# ile PNG Olarak Dışa Aktarma

Ever needed to turn an **excel sheet to png** but weren’t sure how to capture just the pivot table? You’re not alone. In many reporting pipelines the visual of a pivot is the star, and exporting it as a PNG lets you embed it in emails, dashboards, or documentation without pulling the whole workbook along.

Bu rehberde size **how to export pivot** verilerini, **set print area pivot**'ı ve nihayet **export excel range image**'i göstereceğiz, böylece temiz bir **export worksheet to image** dosyası elde edeceksiniz. Harici belgelere gizemli bağlantılar yok—sadece eksiksiz, çalıştırılabilir bir kod parçacığı ve her satırın mantığı.

## İhtiyacınız Olanlar

- **Aspose.Cells for .NET** (NuGet paketi `Aspose.Cells` – sürüm 23.12 veya daha yeni).  
- .NET geliştirme ortamı (Visual Studio, Rider veya `dotnet` CLI).  
- En az bir pivot tablo içeren bir Excel dosyası (`input.xlsx`).

Hepsi bu. Eğer bunlara sahipseniz, hemen başlayalım.

## 1. Adım – Çalışma Kitabını Yükleyin ve İlk Çalışma Sayfasını Alın

Pivotla işlem yapmadan önce, çalışma kitabının bellekte olması gerekir.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:* Dosyayı yüklemek, tüm nesnelere (tablolar, grafikler, pivotlar) erişim sağlar. İlk çalışma sayfasını kullanmak basit bir varsayılandır; gerekirse `0`'ı gerçek sayfa indeksi ya da adıyla değiştirebilirsiniz.

## 2. Adım – Pivot Tablo Aralığını Alın

Pivot tablo bir hücre bloğu içinde bulunur. Bu bloğu almamız, Excel'e neyi yazdıracağını söylememiz için gerekir.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Why we do this:* `PivotTableRange` bize başlangıç ve bitiş satır/ sütunlarını tam olarak söyler. Onsuz, dışa aktarma tüm sayfayı içerir ve bu da **set print area pivot** amacını bozar.

## 3. Adım – Yazdırma Alanını Tanımlayın, Böylece Sadece Pivot Render Edilsin

Excel'in yazdırma motoru `PrintArea` özelliğine saygı duyar. Bunu pivota daraltarak gereksiz veri veya boş hücrelerden kaçınırız.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Pro tip:* Aynı sayfada birden fazla pivot varsa, aralıklarını virgülle ayrılmış bir liste (`"0,0:10,5,12,0:22,5"`) kullanarak birleştirebilirsiniz. Bu, birkaç blok için **export excel range image** tekniğidir.

## 4. Adım – Görüntü Dışa Aktarma Seçeneklerini Ayarlayın (PNG Formatı)

Aspose.Cells çıktıyı ince ayar yapmanıza olanak tanır. PNG kayıpsızdır, net pivot görselleri için mükemmeldir.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Why PNG?* JPEG'in aksine, PNG metin keskinliğini ve şeffaf arka planları korur, bu da **excel sheet to png** senaryoları için tercih edilen formattır.

## 5. Adım – Çalışma Sayfasını (Pivot Alanı) PNG Dosyasına Dışa Aktarın

Şimdi sihir gerçekleşiyor—tanımlı yazdırma alanını bir görüntüye render ediyoruz.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*What you’ll see:* Sadece pivot tabloyu içeren `pivot.png` adlı bir dosya, ekstra satır veya sütun yok. Herhangi bir görüntü görüntüleyicide açın ve paylaşmaya hazır bir görsel elde edin.

---

## Sık Sorulan Sorular & Kenar Durumları

### Çalışma kitabında **birden fazla pivot tablo** varsa ne olur?

Her pivotun `PivotTableRange`'ini alın, aralıkları birleştirin ve birleşik dizeyi `PrintArea`'ya atayın. Örnek:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### **Diğer görüntü formatlarına** dışa aktarabilir miyim?

Kesinlikle. `imgOptions.ImageFormat = ImageFormat.Jpeg;` (veya `Bmp`, `Gif`, `Tiff`) şeklinde değiştirin. Ancak JPEG sıkıştırma artefaktları ekler—genellikle metin ağırlıklı pivotlar için ideal değildir.

### Birçok sayfaya yayılan **büyük pivotlar**ı nasıl yönetirim?

`imgOptions.OnePagePerSheet = false;` ayarlayarak çok sayfalı rendera izin verin, ardından sayfalar arasında döngü yapın:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### **Gizli satır/sütunlar** hakkında ne söyleyebiliriz?

Aspose, çalışma sayfasının görünürlük ayarlarına saygı gösterir. Gizli öğeleri yok saymanız gerekiyorsa, dışa aktarmadan önce geçici olarak görünür hâle getirin veya `PrintArea`'yı manuel olarak ayarlayın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Programı çalıştırın, `pivot.png` dosyasını belirttiğiniz konumda bulacaksınız. Dosyayı açın—sadece pivot tablonun net bir renderını göreceksiniz, başka bir şey yok.

---

## Sonuç

Artık **tam, uçtan uca bir çözüm** elde ettiniz; **excel sheet to png**'yi sadece bir pivot tabloya odaklanarak dönüştürmek için. **set print area pivot**'ı ayarlayarak, **image export options**'ı yapılandırarak ve Aspose.Cells'in `ToImage` metodunu kullanarak rapor üretimini otomatikleştirebilir, görselleri web sayfalarına yerleştirebilir veya sadece analiz anlık görüntülerini arşivleyebilirsiniz.

Sırada ne var? PNG yerine yüksek çözünürlüklü bir PDF (`ImageFormat.Pdf`) deneyin, tek bir sayfada birden fazla pivotla deney yapın veya bu yaklaşımı grafik dışa aktarımlarıyla birleştirerek tam özellikli bir gösterge paneli dışa aktarma hattı oluşturun.

Paylaşmak istediğiniz bir püf noktası mı var? Yorum bırakın ya da bir sonraki öğreticide **export worksheet to image**'ı tüm sayfa anlık görüntüleri, grafikler ve koşullu biçimlendirme dahil olmak üzere keşfedeceğiz. İyi kodlamalar!  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}