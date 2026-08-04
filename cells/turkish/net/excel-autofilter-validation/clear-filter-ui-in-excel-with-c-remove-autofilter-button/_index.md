---
category: general
date: 2026-02-09
description: AutoFilter düğmesini kaldırarak C# ile Excel’de filtre arayüzünü temizleyin.
  Filtre düğmesini nasıl gizleyeceğinizi, başlık satırını nasıl göstereceğinizi ve
  sayfalarınızı düzenli tutmayı öğrenin.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: tr
og_description: C# kullanarak Excel'de filtre arayüzünü temizleyin. Bu kılavuz, filtre
  düğmesini gizlemeyi, başlık satırını göstermeyi ve çalışma sayfalarını temiz tutmayı
  gösterir.
og_title: C# ile Excel'de Filtre Arayüzünü Temizle – AutoFilter Düğmesini Kaldır
tags:
- excel
- csharp
- epplus
- automation
title: C# ile Excel'de Filtre Arayüzünü Temizle – Otomatik Filtre Düğmesini Kaldır
url: /tr/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel'de Filtre Arayüzünü Temizleme – AutoFilter Düğmesini Kaldırma

Excel sayfasında **clear filter UI**'yi temizlemeniz gerektiğinde, o küçük açılır oka hangi kod satırının aslında gizlediğinden emin olmadınız mı? Tek başınıza değilsiniz. Filtre düğmesi, raporu görünümü hiç değiştirmesi gerekmeyen son kullanıcılara gönderdiğinizde göz yorgunluğuna neden olabilir.  

Bu öğreticide, bir tablodan **AutoFilter düğmesini kaldıran**, başlık satırının görünür kalmasını sağlayan ve hatta *filter button*'ı kalıcı olarak nasıl gizleyeceğinize değinen eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda C#'ta **AutoFilter'ı nasıl kaldıracağınızı** ve her adımın neden önemli olduğunu tam olarak öğreneceksiniz.

## Gereksinimler

- .NET 6+ (veya .NET Framework 4.7.2+) – herhangi bir yeni çalışma zamanı yeterlidir.
- **EPPlus** NuGet paketi (version 6.x veya üzeri) – bize `ExcelWorksheet`, `ExcelTable` vb. sağlar.
- **SalesTable** adlı bir tablo içeren basit bir Excel dosyası (birkaç tıklamayla oluşturabilirsiniz).

Hepsi bu. COM interop yok, ekstra DLL yok, sadece birkaç `using` ifadesi ve birkaç satır kod.

## Filtre Arayüzünü Temizleme: AutoFilter Düğmesini Kaldırma

Çözümün çekirdeği üç küçük ifadede yer alır. *Neden* gerekli olduklarını, sadece *ne* yaptıklarını değil, anlamanız için bunları adım adım inceleyelim.

### Adım 1 – Tabloya referans alın

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Neden önemli: EPPlus **tablolar** (`ExcelTable`) ile çalışır, ham aralıklarla değil. Tablo nesnesini alarak, sayfada gördüğünüz UI öğesini kontrol eden `AutoFilter` özelliğine erişiriz. Çalışma sayfasını doğrudan manipüle etmeye çalışırsanız, sadece değerleri etkilersiniz, filtre düğmesini değil.

### Adım 2 – AutoFilter düğme satırını kaldırın

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

`AutoFilter`'ı `null` olarak ayarlamak, EPPlus'a temel filtre satırını silmesini söyler. Bu, geliştiricilerin “**how to remove autofilter**” sorularında aradığı *clear filter UI* işlemidir. EPPlus'ın desteklediği herhangi bir Excel sürümünde çalışan temiz, tek satırlık bir yaklaşımdır.

### Adım 3 – Başlık satırının görünür kalmasını sağlayın

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Filtre UI'sını kaldırdığınızda, tablonun `ShowHeader` bayrağı false ise Excel bazen başlık satırını gizleyebilir. Bunu açıkça `true` olarak ayarlayarak, sütun başlıklarının ekranda kalmasını garanti ederiz – son raporun şık görünümü için ince ama önemli bir detay.

### Tam, çalıştırılabilir örnek

Aşağıda, mevcut bir çalışma kitabını açan, üç adımı uygulayan ve sonucu kaydeden minimal bir console uygulaması bulunuyor. Kopyala‑yapıştır, **F5** tuşuna bas ve filtre düğmesinin kaybolduğunu izle.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Beklenen sonuç:** *SalesReport_NoFilter.xlsx* dosyasını açın – filtre okları yok, ancak sütun başlıkları kalır. Artık “tıklayarak filtreleme” UI karmaşası yok.

> **Pro tip:** **Birden fazla tablo**'unuz varsa ve hepsi için filtre düğmesini gizlemek istiyorsanız, `worksheet.Tables` içinde döngü yapın ve aynı üç satırı döngü içinde uygulayın.

## C# ile Excel'de AutoFilter'ı Nasıl Kaldırırsınız – Derinlemesine İnceleme

Şöyle düşünebilirsiniz: “Çalışma kitabında zaten bir filtre uygulanmışsa ne olur? `AutoFilter = null` ayarlamak filtrelenmiş satırları da temizler mi?” Cevap **evet**. EPPlus, UI'yı ve temel filtre kriterlerini temizler, verileri orijinal sırasına bırakır.  

Sadece düğmeyi *gizlemek* ve filtreyi aktif tutmak istiyorsanız, `AutoFilter` özelliğini **yeni boş bir filtre** olarak ayarlayabilirsiniz:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Bu varyasyon, şık bir görünüm için *filter button*'ı gizlemek istediğinizde, ancak gelişmiş kullanıcıların VBA veya şerit üzerinden filtreleri açıp kapatmasına izin vermek istediğinizde kullanışlıdır.

### Kenar Durumu: Başlık Satırı Olmayan Tablolar

Bazı eski raporlar tablo yerine düz aralıklar kullanır. Bu durumda EPPlus bir `ExcelTable` nesnesi sunmaz, bu yüzden yukarıdaki kod hata verir. Çözüm, önce **aralığı bir tabloya dönüştürmektir**:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Artık resmi bir tablo olmadan başlayan bir aralıkta bile *removed autofilter excel* tarzı UI'yi kaldırdiniz.

## Filtre Düğmesini Gizledikten Sonra Başlık Satırını Göster – Neden Önemli

Yaygın bir şikayet, filtre UI'sını gizledikten sonra başlık satırının bazen kaybolmasıdır, özellikle çalışma kitabı “Hide Header” (Başlığı Gizle) açıkken oluşturulmuşsa. `salesTable.ShowHeader = true;` ifadesini açıkça ayarlayarak bu sürprizi önleriz.  

Eğer **filter button**'ı gizlemeniz ama başlığı gizli tutmanız (belki ham veri dökümü oluşturuyorsunuz) gerekiyorsa, filtreyi temizledikten sonra `salesTable.ShowHeader = false;` olarak ayarlayın. Kod simetriktir, bu da bir yapılandırma bayrağına göre geçişi kolaylaştırır.

## Filter Düğmesini Gizleme – Pratik İpuçları ve Tuzaklar

- **Version compatibility:** EPPlus 6+ yalnızca `.xlsx` dosyalarıyla çalışır. Daha eski `.xls` formatıyla çalışıyorsanız, farklı bir kütüphane (ör. NPOI) kullanmanız gerekir, çünkü *clear filter UI* API'si mevcut değildir.
- **Performance:** Tek bir düğmeyi gizlemek için büyük bir çalışma kitabını yüklemek yavaş olabilir. **read‑only** (yalnızca‑okunur) modda açmak için `ExcelPackage.Load(stream, true)` kullanmayı düşünün, değişikliği uygulayın ve ardından kaydedin.
- **Testing:** İlk seferde çıktıyı her zaman manuel olarak doğrulayın. Otomatik UI testleri, filtre oklarının gerçekten kaybolduğunu (`worksheet.Tables[0].AutoFilter == null`) doğrulayabilir.
- **Licensing:** EPPlus, sürüm 5'te çift lisansa geçiş yaptı. Ticari projeler için ücretli bir lisans almanız ya da alternatif bir kütüphane kullanmanız gerekir.

## Kopyala‑Yapıştır İçin Tam Kaynak Dosyası

Aşağıda, yeni bir console projesine ekleyebileceğiniz tam dosya yer alıyor. Gizli bağımlılık yok, her şey kendi içinde.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

`dotnet add package EPPlus --version 6.0.8` (veya en son sürüm) komutunu derlemeden önce çalıştırın, ve dağıtıma hazır temiz bir sayfanız olacak.

## Sonuç

Excel çalışma kitabında C# kullanarak **AutoFilter'ı nasıl kaldıracağınızı** ve **filter UI'yi nasıl temizleyeceğinizi** gösterdik. Üç satırlık çekirdek (`AutoFilter = null;`, `ShowHeader = true;`) ağır işi yaparken, çevresindeki altyapı çözümü 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}