---
category: general
date: 2026-03-18
description: Excel'den tarihi çıkar ve tarihi yyyy‑mm‑dd formatında ISO olarak çıktı
  al. Japon era tarihlerini nasıl okuyacağını, dönüştüreceğini ve C#'ta ISO tarihlerini
  nasıl görüntüleyeceğini öğren.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: tr
og_description: Excel'den tarihi çıkarın ve tarihi ISO formatında yyyy‑mm‑dd olarak
  çıktı alın. Tam kod ve açıklamalarla adım adım C# öğreticisi.
og_title: Excel'den tarih çıkar – Tarihi C#'ta yyyy‑mm‑dd formatında çıktı
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Excel'ten tarihi çıkar ve yyyy‑mm‑dd formatında çıktı al – Tam C# Rehberi
url: /tr/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den Tarih Çıkarma – yyyy‑mm‑dd Formatında ISO Tarih Nasıl Çıktılanır

Excel'den **tarih çıkarmak** gerektiğinde, Japon dönem tarihlerini nasıl ele alacağınızdan veya temiz bir `yyyy‑mm‑dd` dizesi elde etmekten emin olmadığınız oldu mu? Yalnız değilsiniz. Birçok veri taşıma projesinde kaynak çalışma kitabı tarihleri Japon İmparator takvimini kullanarak saklar ve sonraki sistem ISO‑uyumlu bir tarih, örneğin `2024-04-01` bekler.  

Bu rehberde, bir hücreyi okuyup Japon dönemini yorumlayan ve **tarihi yyyy‑mm‑dd olarak çıktılan** tam, çalıştırılabilir bir çözümü adım adım inceleyeceğiz. Sonunda, herhangi bir .NET uygulamasında **tarihi ISO formatında görüntüleme** konusunda tam bilgi sahibi olacaksınız ve kendi projenize ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığı elde edeceksiniz.

## İhtiyacınız Olanlar

- **.NET 6+** (veya .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – çalışma kitabını yüklerken özel bir takvim ayarlamamızı sağlayan kütüphane.  
- Japon dönem hücresinde tarih içeren bir Excel dosyası (`japan-date.xlsx`) (ör. `令和3年4月1日`).  
- Sevdiğiniz bir IDE – Visual Studio, Rider ya da hatta VS Code işinizi görecektir.

Ek bir NuGet paketi gerekmiyor; sadece Aspose.Cells yeterli ve kod Windows, Linux ya da macOS üzerinde çalışıyor.

## Adım 1: Projeyi Oluşturun ve Aspose.Cells'i Yükleyin

İlk olarak bir konsol uygulaması oluşturun:

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro ipucu:** CI sunucusunda çalışıyorsanız, tekrarlanabilir derlemeler için paket sürümünü (`Aspose.Cells 23.12`) sabitleyin.

## Adım 2: Çalışma Kitabını Japon İmparator Takvimiyle Yükleyin

Kaynak takvim Gregorian olmayan bir takvim olduğunda **Excel'den tarih çıkarmak** için anahtar, Aspose.Cells'e yükleme sırasında hangi takvimi uygulaması gerektiğini söylemektir. Bunu `LoadOptions.Calendar` ile yaparız.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Neden Önemli:** Özel takvim olmadan Aspose.Cells hücreyi düz bir metin olarak değerlendirir ve dönem bilgisini kaybedersiniz. `JapaneseEmperorCalendar` atandığında kütüphane, `令和3年4月1日` değerini otomatik olarak `2021‑04‑01`e dönüştürür.

## Adım 3: Belirli Bir Hücreden Tarihi Alın

Çalışma kitabı artık dönemi yorumlayabildiğine göre, hücreyi bir `DateTime` olarak okuyabiliriz. Tarihin ilk çalışma sayfasında, **A1** hücresinde (satır 0, sütun 0) olduğunu varsayalım.

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Hücre boşsa ya da tarih olmayan bir değer içeriyorsa, `GetDateTime()` bir istisna fırlatır. Savunmacı bir yaklaşım şöyle görünür:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Köşe durumu:** Bazı eski Excel dosyaları tarihleri sayı (seri tarih) olarak saklar. Aspose.Cells bunları otomatik olarak işler, ancak karışık içerik bekliyorsanız hücre tipini yine de kontrol etmelisiniz.

## Adım 4: Tarihi yyyy‑mm‑dd (ISO) Olarak Çıktılayın ve Doğrulayın

`DateTime` elinizde olduğunda, **tarihi yyyy‑mm‑dd olarak çıktılan** tek satırlık bir formatlama yeterlidir:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Programı `令和3年4月1日` içeren bir dosya üzerinde çalıştırdığınızda şu çıktı alınır:

```
Extracted date (ISO): 2021-04-01
```

Bu, birçok API'nin istediği tam **display date iso format**’dır.

## Tam Çalışan Örnek

Tüm parçaları bir araya getirerek, kopyala‑yapıştır‑hazır tam program aşağıdadır:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Not:** `YOUR_DIRECTORY` kısmını `japan-date.xlsx` dosyasının bulunduğu gerçek klasörle değiştirin. Kod herhangi bir sayfa ve hücreyle çalışır – sadece indeksleri ayarlamanız yeterlidir.

## Diğer Takvimleri İşleme (İsteğe Bağlı)

Eğer bir kez **Excel'den tarih çıkarmak** ve Thai Budist takvimi ya da İbrani takvimi gibi farklı bir takvim kullanan bir dosyayla çalışmanız gerekirse, takvim örneğini şu şekilde değiştirin:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Mantığın geri kalanı değişmez, bu da yaklaşımın esnekliğini gösterir.

## Yaygın Tuzaklar ve Çözümleri

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| `GetDateTime()` **InvalidCastException** fırlatıyor | Hücre tarih değil (belki bir metin) | `Cell.Type` kontrol edin ya da `Cell.StringValue` üzerinde `DateTime.TryParse` kullanın. |
| Dönüşüm sonrası yıl hatalı | Çalışma kitabı `Calendar` ayarlanmadan yüklendi | Dosyayı açmadan **önce** uygun takvimle `LoadOptions` oluşturun. |
| ISO çıktısı zaman kısmını gösteriyor (`2021-04-01 00:00:00`) | Format dizesi olmadan `ToString()` kullanıldı | `"yyyy-MM-dd"` biçim belirtecini kullanarak **tarihi yyyy‑mm‑dd** zorlayın. |
| Dosya bulunamadı | Göreceli yol yanlış klasöre işaret ediyor | `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` kullanın ya da mutlak yol verin. |

## Üretim‑Hazır Kod İçin Pro İpuçları

1. **Workbook'u önbelleğe alın**; aynı dosyadan birden çok tarih okumanız gerekiyorsa, çalışma kitabını açmak nispeten maliyetlidir.  
2. **Çıkarma mantığını yeniden kullanılabilir bir metoda sarın:**

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Orijinal dönem metnini** (`cell.StringValue`) ISO çıktısıyla birlikte loglayarak denetim izleri oluşturun.  
4. **Metodu birim test edin**; Heisei, Reiwa gibi farklı dönemleri kapsayan birkaç sabit Excel dosyasıyla doğruluğu garanti altına alın.

## Görsel Genel Bakış

Aşağıda, Excel hücresinden ISO dizesine veri akışını gösteren hızlı bir diyagram yer almaktadır.

![Excel'ten tarih çıkarma örneği, Excel → LoadOptions → DateTime → ISO dizesi gösteriyor]  

*Alt metin: “extract date from excel” diyagramı dönüşüm hattını gösteriyor.*

## Sonuç

**Excel'den tarih çıkarmak**, Japon dönem değerlerini işlemek ve **tarihi yyyy‑mm‑dd** olarak **display date iso format**’ına dönüştürmek için ihtiyaç duyduğunuz her şeyi ele aldık. Çözüm bağımsız, Aspose.Cells'i destekleyen herhangi bir .NET sürümüyle çalışır ve tek bir satır değişikliğiyle diğer takvimlere de genişletilebilir.

Farklı bir takvim mi aklınızda? Ya da birden fazla sütundan tarih mi çekiyorsunuz? `ExtractIsoDate` yardımcı metodunu istediğiniz gibi uyarlayın ya da aşağıya yorum bırakın. Kodlamanız keyifli olsun ve tarihleriniz her zaman mükemmel ISO senkronizasyonunda kalsın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}