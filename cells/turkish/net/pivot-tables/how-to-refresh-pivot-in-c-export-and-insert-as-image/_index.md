---
category: general
date: 2026-05-04
description: C#'ta pivot tabloyu nasıl yenileyip PNG olarak dışa aktarılır, ardından
  resmi çalışma sayfasına nasıl eklenir. Tam kodlu adım adım rehberi izleyin.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: tr
og_description: C#'ta pivot nasıl yenilenir? Pivot tablosunu resim olarak dışa aktarmayı
  ve tam kod örnekleriyle bir çalışma sayfasına eklemeyi öğrenin.
og_title: C#'ta Pivot'ı Yenileme – Görüntü Olarak Dışa Aktarma ve Ekleme
tags:
- C#
- Aspose.Cells
- Excel Automation
title: C#'de Pivot'ı Yenileme – Görüntü Olarak Dışa Aktarma ve Ekleme
url: /tr/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Pivot Yenileme – Görüntü Olarak Dışa Aktarma ve Ekleme

C#'ta pivot yenilemek, Excel raporlarını otomatikleştirirken sık karşılaşılan bir engeldir. Bu rehberde **pivot nasıl yenilenir**, PNG olarak nasıl dışa aktarılır ve bu görüntünün bir çalışma sayfası yer tutucusuna nasıl yerleştirilir—tek bir çalıştırılabilir programla—göreceksiniz.

Eğer *pivot nasıl dışa aktarılır* konusunda da merakınız varsa ya da **görüntüyü çalışma sayfasına ekleme** ihtiyacınız varsa doğru yerdesiniz. Her satırı adım adım inceleyecek, neden önemli olduğunu açıklayacak ve gerçek dünya projelerinde karşılaşabileceğiniz birkaç kenar durumunu da ele alacağız.

---

## Gerekenler

- **Aspose.Cells for .NET** (`Workbook`, `Worksheet`, `ImageOrPrintOptions` vb. sınıfları sağlayan kütüphane). NuGet üzerinden edinebilirsiniz: `Install-Package Aspose.Cells`.
- .NET 6 veya üzeri (aşağıdaki kod .NET 6 hedefli, ancak herhangi bir yeni sürüm de çalışır).
- C# ve dosya I/O hakkında temel bir anlayış—karmaşık bir şey gerekmez.

Hepsi bu. Ek DLL'lere, COM interop'a gerek yok, sadece temiz bir C# konsol uygulaması.

---

## Adım 1 – Excel Çalışma Kitabını C# Tarzında Yükleme

İlk olarak, kaynak dosyayı açmamız gerekiyor. İşte **load excel workbook c#** kısmının yer aldığı yer.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Neden?**  
> Çalışma kitabını yüklemek, sayfalarına, pivot tablolarına ve resim yer tutucularına erişmemizi sağlar. Dosya bulunamazsa Aspose, yakalanabilir bir `FileNotFoundException` fırlatır; bu da daha dost bir UI için yakalanabilir.

---

## Adım 2 – Pivot Dışa Aktarmak İçin Görüntü Seçeneklerini Hazırlama

Şimdi Aspose'a dışa aktarılacak görüntünün nasıl görünmesini istediğimizi söylüyoruz. Bu, **pivot nasıl dışa aktarılır** sorusunun çekirdeğidir.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Pro tip:**  
> Daha küçük dosya boyutu için JPEG isterseniz `SaveFormat.Png` yerine `SaveFormat.Jpeg` kullanın ve `Quality` değerini buna göre ayarlayın.

---

## Adım 3 – Pivot Tabloyu Yenileme Kodu

Eski bir pivot tablo, geçmiş verileri gösterir. Yenilemek, görüntünün en güncel sayıları yansıtmasını garantiler.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Neden yenilenir?**  
> Pivot tablolar, oluşturuldukları zaman kaynak veriyi önbelleğe alır. Altındaki çalışma sayfası değişirse (ör. yeni satırlar eklenirse) önbellek güncelliğini yitirir. `Refresh()` çağrısı, Aspose'un kaynak aralığını yeniden sorgulamasını sağlar ve dışa aktarılan görüntünün eski toplamlarla takılı kalmasını önler.

---

## Adım 4 – Yenilenmiş Pivotu Görüntüye Dönüştürme

İşte **pivot dışa aktar** işlemini gerçekten yapan sihirli satır; bir bayt dizisine dönüştürür.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Ne elde edersiniz:**  
> `pivotImage` artık pivot tablonun PNG kodlu bir resmini tutar; diske yazılabilir ya da başka bir yere gömülebilir.

---

## Adım 5 – Görüntüyü Çalışma Sayfasına Ekleme

Burada **görüntüyü çalışma sayfasına ekleme** işlemini yapıyoruz. Görüntüyü ilk resim yer tutucusuna (varsa) yerleştireceğiz.

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Neden yer tutucu kullanılır?**  
> Birçok Excel şablonu, önceden biçimlendirilmiş bir resim şekli (boyut, kenarlık, konum) ile gelir. `Pictures[0]` hedefleyerek düzeni bozmadan yerleştiririz. Şablonda yer tutucu yoksa, yedekleme A1 hücresine sabitlenmiş yeni bir resim oluşturur.

---

## Adım 6 – Çalışma Kitabını Kaydetme (İsteğe Bağlı)

Son olarak değişiklikleri kalıcı hâle getirin. Orijinali üzerine yazabilir ya da yeni bir dosyaya kaydedebilirsiniz.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Beklenen sonuç:**  
> `output.xlsx` dosyasını açtığınızda pivot tablonun yenilendiğini, net bir PNG olarak dışa aktarıldığını ve ilk resim slotunda gösterildiğini göreceksiniz. Çalışma kitabının geri kalanı dokunulmamış kalır.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda yeni bir konsol projesine yapıştırabileceğiniz eksiksiz kod bloğu yer alıyor. Hiçbir parça eksik değil.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Programı çalıştırın, oluşan dosyayı açın ve pivotun en son verileri yansıttığını ve yüksek çözünürlüklü bir görüntü olarak göründüğünü doğrulayın.

---

## Sık Sorulan Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| **Çalışma kitabının birden fazla çalışma sayfası olması durumunda ne yapılmalı?** | Uygun dizini veya adı (`workbook.Worksheets[0]` yerine `workbook.Worksheets["Sheet2"]`) ayarlayın. |
| **Birden fazla pivot tablo dışa aktarabilir miyim?** | `worksheet.PivotTables` üzerinde döngü kurarak adım 3‑4'ü her biri için tekrarlayın. Her resmi ayrı bir yer tutucuya kaydedin ya da tek bir sayfada birleştirin. |
| **Büyük pivot tabloları bellek baskısı yaratıyorsa ne yapmalıyım?** | `ImageOrPrintOptions` içinde daha düşük DPI ayarlayın veya JPEG olarak dışa aktararak bayt‑dizi boyutunu küçültün. |
| **Herhangi bir nesneyi dispose etmem gerekiyor mu?** | Aspose nesneleri yönetilmektedir; `using` ifadesi zorunlu değildir, ancak deterministik temizlik isterseniz `Workbook` nesnesini bir `using` bloğu içinde tutabilirsiniz. |
| **Bu .NET Core ile uyumlu mu?** | Evet. Aspose.Cells, .NET Core, .NET 5/6 ve .NET Framework'ü destekler. Sadece uygun NuGet paketini referans gösterin. |

---

## İpuçları & En İyi Uygulamalar

- **Yolları doğrulayın**: Sabit ayraçlardan kaçınmak için `Path.Combine` ve `Environment.GetFolderPath` kullanın.  
- **Hata yönetimi**: Tüm `Main` gövdesini bir `try/catch` içine alın ve üretim script'lerinde `Exception.Message`'ı loglayın.  
- **Şablon tasarımı**: Pivot görüntüsünün konulmasını istediğiniz yere şeffaf bir resim şekli yerleştirin; bu, sütun genişliklerini ve satır yüksekliklerini korur.  
- **Performans**: Sadece görüntüye ihtiyacınız varsa, çalışma kitabını kaydetmeyi atlayabilir ve `pivotImage`'ı ayrı bir PNG dosyasına yazabilirsiniz.

---

## Sonuç

Artık **C#'ta pivot nasıl yenilenir**, yenilenmiş görünümü bir görüntü olarak dışa aktarılır ve **görüntü çalışma sayfasına nasıl eklenir** sorularının cevaplarını biliyorsunuz. Tam çözüm—çalışma kitabını yükleme, dışa aktarma seçeneklerini ayarlama, pivotu yenileme, PNG'ye dönüştürme ve dosyayı kaydetme—istediğiniz tüm iş akışını kapsar.

Bir sonraki zorluğa hazır mısınız? **Pivot nasıl dışa aktarılır** adımını birden çok dosyanın toplu işlenmesiyle birleştirin ya da dinamik veri kaynakları (veritabanları, CSV akışları) için **pivot tabloyu yenileme kodu**nu keşfedin. Aynı desen geçerli: yükle, yenile, dışa aktar, ekle, kaydet.

İyi kodlamalar, Excel otomasyonlarınız taze ve resim‑kusursuz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}