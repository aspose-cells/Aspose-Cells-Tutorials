---
category: general
date: 2026-02-14
description: Excel'de özel tarih ayrıştırma ile Japonya dönemi tarihlerini çözümleyin.
  Seçeneklerle Excel'i yükleyerek dosyadan çalışma kitabını nasıl yükleyeceğinizi
  öğrenin ve yaygın tuzaklardan kaçının.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: tr
og_description: Aspose.Cells kullanarak Excel'de Japon dönemi tarihlerini ayrıştırın.
  Bu kılavuz, özel tarih ayrıştırma seçenekleriyle dosyadan çalışma kitabını nasıl
  yükleyeceğinizi gösterir.
og_title: Japon Dönemi Tarihlerini Ayrıştırma – Adım Adım C# Öğreticisi
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel'de Japon Dönemi Tarihlerini Ayrıştırma – C# Geliştiricileri için Tam
  Kılavuz
url: /tr/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japon Dönemi Tarihlerini Ayrıştırma – Tam C# Öğreticisi

Hiç **Japon dönemi tarihlerini** bir Excel sayfasından ayrıştırmanız gerekti ve değerlerin garip sayılara dönüşmesinden şikayetçi oldunuz mu? Yalnız değilsiniz. Birçok geliştirici, varsayılan `DateTime` ayrıştırıcısının Japon takvimlerinde kullanılan “Reiwa 1/04/01” biçimini tanımadığı zaman bu soruna takılır.  

İyi haber: Aspose.Cells’e bu hücreleri **seçeneklerle Excel yüklerken** Japon‑dönemi tarihleri olarak ele almasını söyleyebilirsiniz. Bu rehberde bir çalışma kitabını dosyadan yüklemeyi, özel tarih ayrıştırmasını yapılandırmayı ve tarihlerin tam istediğiniz gibi çıktığını doğrulamayı adım adım göstereceğiz.

Bu öğreticinin sonunda şunları yapabilecek duruma geleceksiniz:

* `DateTimeParsing.JapaneseEra` belirterek dosyadan bir çalışma kitabı yüklemek.
* Hücre değerlerine doğru `DateTime` nesneleri olarak erişmek.
* Boş hücreler veya karışık takvimler gibi kenar durumlarını ele almak.
* Karşılaşabileceğiniz **custom date parsing excel** senaryolarına bu yaklaşımı genişletmek.

> **Önkoşul** – Aspose.Cells for .NET kütüphanesine (v23.9 veya sonrası) ve .NET‑uyumlu bir IDE’ye (Visual Studio, Rider vb.) ihtiyacınız var. Başka bir paket gerekli değil.

---

## Adım 1: Japon Dönemi Ayrıştırması İçin Metin Yükleme Seçeneklerini Yapılandırma  

İlk olarak, yükleyiciye Japon dönemi tarihi gibi görünen metni nasıl yorumlayacağını söylememiz gerekiyor. Bu, `TxtLoadOptions` ve `DateTimeParsing` enum’u aracılığıyla yapılır.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Neden önemli:** `JapaneseEra` bayrağı olmadan Aspose.Cells hücreyi düz bir string olarak kabul eder ve siz de dönemi ayırıp dönüştürmek zorunda kalırsınız. Bayrak, ağır işi yapar, kodunuzu temiz ve hata‑olası olmayan hâle getirir.

---

## Adım 2: Seçenekleri Kullanarak Dosyadan Çalışma Kitabı Yükleme  

Şimdi gerçek anlamda Excel dosyasını açıyoruz. `loadOptions` nesnesinin `Workbook` yapıcısına geçirildiğine dikkat edin — bu, **load workbook from file** adımının özel ayrıştırma kurallarımızı göz önünde bulundurmasını sağlar.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Dosya başka bir konumda (ör. ağ paylaşımı) ise `filePath`i ona göre ayarlayın. Önemli olan aynı `loadOptions` örneğinin kullanılması; aksi takdirde Japon dönemi dönüşümü gerçekleşmez.

---

## Adım 3: Ayrıştırılan Tarihlere Erişim  

Çalışma kitabı yüklendikten sonra, hücre değerlerini normal bir tarih gibi alabilirsiniz. API otomatik olarak bir `DateTime` nesnesi döndürür.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Beklenen çıktı** (A1 hücresinde “R1/04/01” olduğu varsayılırsa):

```
Parsed date from A1: 2024-04-01
```

Hücre “2023‑12‑31” gibi bir Gregoryen tarih içeriyorsa, ayrıştırıcı hâlâ çalışır — sadece orijinal tarih değişmeden döner.

---

## Adım 4: Bir Sütundaki Tüm Tarihleri Doğrulama  

Genellikle bir sütundaki tüm Japon dönemi tarihlerini taramanız gerekir. Aşağıdaki kompakt döngü, boşlukları ve karışık içeriği sorunsuz bir şekilde nasıl ele alacağınızı gösterir.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**İpucu:** `CellValueType.IsDateTime` ayrıştırmanın başarılı olup olmadığını kontrol etmenin en güvenli yoludur. Bu, hücre beklenmedik bir metin içerdiğinde `InvalidCastException` almanızı önler.

---

## Adım 5: Yaygın Tuzaklar ve Çözüm Yolları  

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Boş hücreler `DateTime.MinValue` döndürür** | Ayrıştırıcı boş stringleri minimum tarih olarak kabul eder. | `DateTimeValue`ye erişmeden önce `cell.IsNull` kontrol edin. |
| **Aynı sütunda karışık takvimler (Japon + Gregoryen)** | Ayrıştırıcı her ikisini de işler, ancak raporlama için ayırmanız gerekebilir. | `cell.Type` `IsString` ise orijinal metni incelemek için `cell.StringValue` kullanın. |
| **Yanlış era (ör. “H30” Heisei için) 2019 sonrası** | Heisei 2019’da sona erdi; sonraki tarihler “R” kullanılmalı. | Ayrıştırılmış sonuca güvenmeden önce era önekini doğrulayın. |
| **Büyük dosyalarda performans yavaşlaması** | Özel seçeneklerle yükleme küçük bir ek yük getirir. | Yalnızca gerekli çalışma sayfalarını yükleyin (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Adım 6: Tam Çalışan Örnek  

Hepsini bir araya getiren, kopyalayıp çalıştırabileceğiniz bağımsız bir konsol uygulaması aşağıdadır. **custom date parsing excel** sürecini baştan sona gösterir.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**`japan_dates.xlsx` şu verileri içerdiğinde**:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

Konsol çıktısı:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Kaydedilen dosya artık doğru tarih hücreleri içerir; Excel’de açtığınızda normal tarih biçimlendirmesini görürsünüz.

---

## Sonuç  

`TxtLoadOptions` ile **Japon dönemi tarihlerini** nasıl ayrıştıracağınızı, bu seçeneklerle **load workbook from file** yaparak çalışma kitabını nasıl yükleyeceğinizi ve elde edilen `DateTime` değerleriyle nasıl çalışacağınızı gösterdik. Aynı desen—özel ayrıştırma bayraklarını ayarlayıp ardından çalışma kitabını yüklemek—herhangi bir **custom date parsing excel** ihtiyacına uygulanabilir; ister mali dönemler, ISO hafta numaraları, ister özel formatlar olsun.

Farklı bir era ya da karışık takvimli bir elektronik tablo mu var? `DateTimeParsing.JapaneseEra` yerine başka bir enum değeri (ör. `DateTimeParsing.Custom`) koyun ve bir format dizesi sağlayın. Aspose.Cells’in esnekliği sayesinde manuel dönüşüm kodu yazma ihtiyacınız neredeyse ortadan kalkar.

**İleride keşfedebileceğiniz adımlar:**

* CSV dosyaları için **Load Excel with options** (`CsvLoadOptions`) kullanarak bölge‑özel ayırıcıları ele alma.
* Temizlenmiş veriyi dışa aktarmak için `Workbook.Save` ile `SaveFormat.Xlsx` kullanma.
* Bu yaklaşımı **Aspose.Slides** veya **Aspose.Words** ile birleştirerek raporlama boru hatları oluşturma.

Deneyin, seçenekleri ayarlayın ve kütüphanenin ağır işi yapmasına izin verin. Kodlamanın tadını çıkarın!  

![Konsol penceresinde ayrıştırılmış Japon dönemi tarihlerinin ekran görüntüsü – parse japanese era dates example](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}