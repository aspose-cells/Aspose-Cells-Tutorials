---
category: general
date: 2026-03-30
description: Aspose.Cells kullanarak C#'de sayı formatlamayı ayırıcı ile nasıl yapacağınızı
  öğrenin. Özel sayı formatı ayarlama, binlik ayırıcı ekleme, ondalık basamakları
  biçimlendirme ve hücreyi nasıl biçimlendireceğinizi içerir.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: tr
og_description: C#'da sayıyı ayırıcıyla biçimlendirin. Bu rehber, özel sayı biçimi
  ayarlamayı, binlik ayırıcı eklemeyi, ondalık basamakları biçimlendirmeyi ve Aspose.Cells
  kullanarak hücreyi nasıl biçimlendireceğinizi gösterir.
og_title: C#'da Ayırıcı ile Sayı Formatlama – Aspose.Cells Öğreticisi
tags:
- C#
- Aspose.Cells
- Number Formatting
title: C#'da Ayırıcı ile Sayı Formatlama – Tam Aspose.Cells Rehberi
url: /tr/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Sayıyı Ayırıcıyla Biçimlendirme – Tam Aspose.Cells Rehberi

Hiç bir elektronik tabloda **format number with separator** yapmanız gerekti ama hangi API çağrısını kullanacağınızdan emin değildiniz mi? Tek başınıza değilsiniz—geliştiriciler veri dışa aktarırken binlik ayırıcılar, ondalık basamaklar ve özel desenlerle sürekli mücadele ediyor.  

İyi haber: Aspose.Cells bunu çocuk oyuncağı haline getiriyor. Bu öğreticide, **sets a custom number format**, **adds a thousands separator**, **formats decimal places**, ve **how to format cell** çıktısını bir dize olarak gösteren gerçek bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz çalıştırmaya hazır bir kod parçacığına sahip olacaksınız.

## Bu Rehberde Neler Kapsanıyor

* İhtiyacınız olan tam NuGet paketini ve nasıl kuracağınızı.  
* Çalışma kitabı oluşturan, sayısal bir değer yazan ve özel bir format uygulayan adım adım kod.  
* `ExportTableOptions.ExportAsString`'in biçimlendirilmiş bir değeri almanın tercih edilen yolu olmasının nedeni.  
* Yaygın tuzaklar—örneğin `ExportAsString`'i etkinleştirmeyi unutmak veya yanlış format maskesi kullanmak.  
* Farklı bir ondalık basamak sayısı veya farklı bir ayırıcı stili ihtiyacınız varsa format maskesini nasıl ayarlayacağınızı.

Harici dokümantasyon bağlantılarına gerek yok; ihtiyacınız olan her şey burada. Hadi başlayalım.

---

## Ön Koşullar

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6.0 or later | Aspose.Cells 23.10+ .NET Standard 2.0+ hedeflediği için .NET 6 güvenli ve güncel bir sürümdür. |
| Visual Studio 2022 (or any C# IDE) | Hata ayıklamayı ve paket yönetimini sorunsuz hale getirir. |
| Aspose.Cells for .NET NuGet package | Kullanacağımız `Workbook`, `Worksheet` ve `ExportTableOptions` sınıflarını sağlar. |

Paketi Package Manager Console üzerinden şu şekilde kurabilirsiniz:

```powershell
Install-Package Aspose.Cells
```

Hepsi bu—ekstra DLL yok, COM interop yok, sadece tek bir NuGet referansı.

## Adım 1: Yeni Bir Workbook Başlatma (How to Format Cell)

İlk olarak, yeni bir `Workbook` örneği oluşturuyoruz. Bunu, veri almaya hazır boş bir Excel dosyası olarak düşünebilirsiniz.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Neden önemli:** `Workbook`, Aspose.Cells'teki her işlemin giriş noktasıdır. İlk çalışma sayfasını (`Worksheets[0]`) alarak, bir sayfa adı vermeye gerek kalmadan temiz bir tuval elde ederiz.

## Adım 2: Hedef Hücreye Sayısal Bir Değer Yazma

Sonra, **A1** hücresine ham bir sayı koyuyoruz. Değer henüz biçimlendirilmemiştir—sadece bir double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro ipucu:** Daha sonra sayısal biçimlendirme uygulamayı planlıyorsanız `PutString` yerine `PutValue` kullanın. Bu, temel veri tipini korur ve Excel uyumlu hesaplamalara izin verir.

## Adım 3: Özel Sayı Formatı Ayarlama (Binlik Ayırıcı Ekleme ve Ondalık Basamakları Biçimlendirme)

Şimdi öğreticinin kalbine geliyoruz: Aspose.Cells'in sayıyı nasıl göstereceğini belirten bir format maskesi tanımlama. `#,##0.00` maskesi üç şey yapar:

1. **`#,##0`** – binlik ayırıcı ekler (varsayılan olarak virgül).  
2. **`.00`** – tam iki ondalık basamak zorunlu kılar.  

Farklı bir ondalık sayısı ihtiyacınız varsa, ondalık noktasından sonraki `0` sayısını değiştirmeniz yeterlidir.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Neden `ExportAsString` kullanıyoruz**: Varsayılan olarak, `ExportString` ham değeri döndürür. `ExportAsString = true` ayarı, API'nin metne dönüştürmeden önce `NumberFormat` maskesini uygulamasını zorlar. Bu, raporlar, JSON yükleri veya UI gösterimi için tam dize temsiline ihtiyaç duyduğunuzda gereklidir.

## Adım 4: Biçimlendirilmiş Metni Dışa Aktarma (How to Format Cell)

Seçenekler hazır olduğunda, aynı hücrede `ExportString` metodunu çağırıyoruz. Metot, az önce tanımladığımız maskeyi dikkate alır ve güzel biçimlendirilmiş bir dize döndürür.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Programı çalıştırdığınızda konsola **`12,345.68`** yazdırır—tam olarak istediğimiz format.

> **Köşe durumu:** Kaynak sayı iki ondalıktan fazla basamak içeriyorsa, maske onu yuvarlar. Yuvarlama yerine kesme (truncation) istiyorsanız, `PutValue`'yi çağırmadan önce değeri `Math.Truncate` ile ön işlemden geçirmeniz gerekir.

## Adım 5: Formatı Ayarlama – Yaygın Varyasyonlar

### 5.1 Ondalık Hassasiyeti Değiştirme

Üç ondalık basamak ister misiniz? Sadece maskeyi değiştirin:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Farklı Bir Binlik Ayırıcı Kullanma

Bazı yerel ayarlar boşluk veya nokta tercih eder. Karakteri doğrudan yerleştirebilirsiniz:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Ya da çalışma kitabının kültür ayarlarına güvenebilirsiniz:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Önek veya Sonek (Para Birimi, Yüzde)

Maskeye doğrudan bir dolar işareti veya yüzde işareti ekleyin:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Not:** Maske büyük/küçük harfe duyarlıdır. `$` ve `%` literal sembollerdir; temel sayısal değeri etkilemezler.

## Adım 6: Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, yeni bir konsol uygulamasına kopyalayabileceğiniz tam program yer alıyor. Tüm adımları, yorumları ve son çıktı doğrulamasını içerir.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Programı çalıştırın (`dotnet run` terminalden veya Visual Studio'da F5 tuşuna basarak) ve biçimlendirilmiş sayının tam olarak gösterildiği gibi yazdırıldığını göreceksiniz.

## Sıkça Sorulan Sorular (SSS)

**S: Bu, eski Excel sürümleriyle çalışır mı?**  
C: Evet. Format maskesi Excel'in yerel sayı‑formatı sözdizimini izler, bu yüzden `#,##0.00`'ı anlayan herhangi bir sürüm aynı dizeyi üretir.

**S: Hücre aralığını biçimlendirmem gerekirse?**  
C: İstenen aralık üzerinde döngü yaparak aynı `ExportTableOptions`'ı her hücreye uygulayabilir ya da aralığın `Style.Custom` özelliğini ayarlayıp ardından tek bir hücrede `ExportString` çağırabilirsiniz.

**S: Bu formatları uygulayarak doğrudan CSV'ye dışa aktarabilir miyim?**  
C: Kesinlikle. Her hücreye formatı uyguladıktan sonra `Workbook.Save("output.csv", SaveFormat.CSV);` kullanın. Aspose.Cells, CSV oluştururken hücrenin `Style`'ını dikkate alır.

## Sonuç

Aspose.Cells kullanarak C#'ta **format number with separator** nasıl yapılacağını gösterdik; **set custom number format**, **add thousands separator**, **format decimal places** ve dize dışa aktarımı için temel **how to format cell** konularını kapsadık. Kod tamamen bağımsızdır, .NET 6+ ile çalışır ve herhangi bir yerel ayar ya da hassasiyet gereksinimi için uyarlanabilir.

Sonra şu konuları keşfedebilirsiniz:

* Aynı tekniği tarih ve zamanlara uygulama (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Her sütunun farklı bir maske gerektirdiği toplu dışa aktarmaları otomatikleştirme.  
* Biçimlendirilmiş dizeleri Aspose.Words ile PDF raporlarına entegre etme.

Bunları deneyin, ve ekibinizde elektronik tablo biçimlendirme konusunda başvurulacak kişi haline geleceksiniz. Kodlamanın tadını çıkarın!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Aspose.Cells çıktısında ayırıcıyla biçimlendirilmiş sayının görüntüsü"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}