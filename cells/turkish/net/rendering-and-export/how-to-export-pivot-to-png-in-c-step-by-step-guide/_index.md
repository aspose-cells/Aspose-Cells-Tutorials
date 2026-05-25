---
category: general
date: 2026-02-14
description: Aspose.Cells kullanarak bir Excel çalışma kitabındaki pivotu PNG olarak
  nasıl dışa aktarılır. Excel çalışma kitabını nasıl yükleyeceğinizi, pivot tabloyu
  görüntüye nasıl dönüştüreceğinizi ve pivot görüntüsünü zahmetsizce nasıl kaydedeceğinizi
  öğrenin.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: tr
og_description: C#'ta Excel'den pivot'ı PNG olarak dışa aktarma. Bu kılavuz, Excel
  çalışma kitabını nasıl yükleyeceğinizi, bir pivot tabloyu PNG'ye nasıl render edeceğinizi
  ve pivot görüntüsünü nasıl kaydedeceğinizi gösterir.
og_title: C#'ta pivot'i PNG olarak dışa aktarma – Tam Kılavuz
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'ta Pivot'ı PNG Olarak Nasıl Dışa Aktarılır – Adım Adım Rehber
url: /tr/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot'ı PNG olarak C#'ta Dışa Aktarma – Tam Kılavuz

Hiç **pivot'ı nasıl dışa aktaracağınızı** bir Excel sayfasından net bir PNG dosyası olarak merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler genellikle raporlar, gösterge panoları veya e‑posta ekleri için bir pivot tablosunun hızlı bir görseline ihtiyaç duyar. İyi haber? Aspose.Cells ile Excel çalışma kitabını yükleyebilir, ilk pivot tablosunu alabilir, bir görüntüye dönüştürebilir ve **pivot görüntüsünü kaydedebilir** sadece birkaç C# satırıyla.

Bu öğreticide ihtiyacınız olan her şeyi adım adım inceleyeceğiz: **load excel workbook** temellerinden, **pivot table to png** oluşturma sürecine, ve son olarak dosyayı diske kaydetmeye kadar. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, bağımsız ve çalıştırılabilir bir programınız olacak.

---

## Gereksinimler

- **.NET 6 veya daha yenisi** (kod .NET Framework 4.7+ üzerinde de çalışır)
- **Aspose.Cells for .NET** NuGet paketi (yazım anında sürüm 23.12)
- En az bir pivot tablo içeren bir Excel dosyası (`input.xlsx`)
- Size uygun bir Visual Studio veya VS Code ortamı

Ek kütüphane, COM interop veya Excel kurulumu gerekmez—Aspose.Cells her şeyi bellekte yönetir.

---

## Adım 1 – Excel Çalışma Kitabını Yükleme

İlk iş, çalışma kitabını belleğe getirmektir. İşte **load excel workbook** ifadesinin devreye girdiği nokta.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Neden önemli:**  
> Çalışma kitabını bir kez yüklemek işlemi hızlı tutar ve kaynak dosyanın kilitlenmesini önler. Aspose.Cells dosyayı yönetilen bir akışa okur, böylece daha sonra bir bayt dizisinden ya da ağ konumundan da yükleyebilirsiniz.

---

## Adım 2 – Pivot Tablosunu Görüntüye Dönüştürme

Çalışma kitabı bellekte olduğuna göre pivot tablolara erişebiliriz. API, `System.Drawing.Image` döndüren kullanışlı bir `ToImage()` metoduna sahiptir.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Pro ipucu:** Çalışma kitabınız birden fazla pivot tablo içeriyorsa, sadece `worksheet.PivotTables` üzerinde döngü kurup her birini dışa aktarın. `ToImage()` çağrısı mevcut görünümü (filtreler, dilimleyiciler vb.) korur, böylece kullanıcıya gördüğü tam olarak elde edersiniz.

---

## Adım 3 – Oluşturulan PNG Dosyasını Kaydetme

Son olarak bitmap'i diske kalıcı olarak yazdırıyoruz. `Save` aşırı yüklemesi, dosya uzantısına göre formatı otomatik seçer.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

Programı çalıştırdığınızda, Excel içindeki pivot tabloya birebir benzeyen bir `pivot.png` dosyası oluşur. Herhangi bir görüntü görüntüleyicide açtığınızda satırları, sütunları ve toplamları pikselle mükemmel bir şekilde render edilmiş olarak görürsünüz.

---

## Yaygın Durumların Yönetimi

### Birden Çok Çalışma Sayfası veya Pivot Tablosu

Pivot farklı bir sayfada saklanıyorsa, çalışma sayfası indeksini değiştirin ya da sayfa adını kullanın:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Ardından döngü kurun:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Büyük Pivot Tabloları

Çok büyük pivotların varsayılan görüntü boyutu devasa olabilir. `ToImage()` çağrısından önce çalışma sayfasının yakınlaştırma faktörünü ayarlayarak render boyutunu kontrol edebilirsiniz:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Bellek Yönetimi

`System.Drawing.Image` `IDisposable` uygular. Üretim kodunda, yerel kaynakları hızlıca serbest bırakmak için resmi bir `using` bloğu içinde tutun:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Tam Çalışan Örnek

Aşağıda, tamamen hazır, çalıştırılabilir program yer alıyor. Yeni bir konsol projesine yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Beklenen çıktı:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

Ve `pivot.png` dosyası, orijinal pivot tablosunun görsel bir kopyasını içerecek.

---

## Sık Sorulan Sorular

- **Bu, grafik içeren .xlsx dosyalarıyla çalışır mı?**  
  Evet. `ToImage()` metodu yalnızca pivot tablo düzenine bakar; grafikler etkilenmez.

- **PNG yerine JPEG veya BMP olarak dışa aktarabilir miyim?**  
  Kesinlikle—`Save` içindeki `ImageFormat` argümanını değiştirmeniz yeterli. PNG kayıpsızdır, bu yüzden veriyi net tutmak için önerilir.

- **Çalışma kitabı şifre korumalıysa ne yapmalıyım?**  
  Şifreli yükleme aşırı yüklemesini kullanın:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Sonuç

Aspose.Cells kullanarak bir Excel dosyasından PNG görüntüsü olarak **pivot'ı nasıl dışa aktaracağınızı** yeni öğrendiniz. Adımlar—**load excel workbook**, **pivot table to png** ve **save pivot image**—basit ama gerçek dünya raporlama hatları için güçlü.

İleride şunları keşfedebilirsiniz:

- Bir klasördeki tüm pivot tabloları otomatik dışa aktarma (export excel pivot in bulk)  
- PNG'yi bir PDF veya HTML e‑postaya gömme (iTextSharp veya Razor ile birleştirme)  
- Dışa aktarılan görüntüye filigran ekleme veya özel stil uygulama  

Bunları deneyin ve bir sonraki gösterge panonuzda görsellerin konuşmasına izin verin.

---

![pivot dışa aktarma örnek çıktısı](assets/pivot-export-example.png "pivot dışa aktarma örnek çıktısı")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}