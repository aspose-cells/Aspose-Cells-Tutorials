---
category: general
date: 2026-05-23
description: C#'ta Excel çalışma kitabı oluşturun ve özel sayı biçimi uygulamayı,
  hücre stilini programlı olarak ayarlamayı, hücreyi bilimsel gösterimle biçimlendirmeyi
  öğrenin, ardından çalışma kitabını xlsx olarak kaydedin.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: tr
og_description: C#'ta hızlıca Excel çalışma kitabı oluşturun. Özel sayı biçimini uygulamayı,
  hücreleri programlı olarak biçimlendirmeyi, bilimsel gösterimi formatlamayı ve xlsx
  olarak kaydetmeyi öğrenin.
og_title: C#'ta Excel Çalışma Kitabı Oluştur – Özel Sayı Formatı Uygula
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: C# ile Excel Çalışma Kitabı Oluştur – Özel Sayı Biçimi Uygula
url: /tr/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Excel Çalışma Kitabı Oluşturma – Özel Sayı Biçimi Uygulama

C# ile excel çalışma kitabı oluşturmak düşündüğünüzden çok daha kolay. Bu rehberde size özel bir sayı biçimi uygulamayı, bir hücreyi bilimsel gösterimde biçimlendirmeyi, hücre stilini programatik olarak ayarlamayı ve sonunda çalışma kitabını bir xlsx dosyasına kaydetmeyi adım adım göstereceğiz.

Eğer hiç boş bir elektronik tabloya bakıp tüm süreci otomatikleştirmeyi—veri doldurmaktan sayıları tam istediğiniz gibi göstermeye kadar—düşündüyseniz, bu öğretici tam size göre. Sonunda, herhangi bir elektronik tablo programında açabileceğiniz tam işlevsel bir Excel dosyanız olacak ve **nasıl** kod yazacağınızı değil, **neden** her adımın önemli olduğunu da anlayacaksınız.

## İhtiyacınız Olanlar

- **.NET 6+** (veya kütüphaneyi destekleyen herhangi bir yeni .NET Framework)  
- **Aspose.Cells for .NET** (veya `Workbook`, `Cell` ve `CellFormat` sınıflarını sunan başka bir API)  
- Biraz C# deneyimi – `Console.WriteLine` yazabiliyorsanız yeterli.  

Ek yapılandırma dosyası, COM etkileşimi ve kesinlikle manuel Excel kurulumu gerekmez.

---

## Excel Çalışma Kitabı Oluştur – Workbook Nesnesini Başlat

İlk yapmamız gereken boş bir çalışma kitabı oluşturmak. `Workbook` sınıfını, satır, sütun ve stilleri “boyayacağınız” boş bir tuval olarak düşünün.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Hepsi bu—tek bir satır ve bellekte yepyeni bir Excel dosyanız var. `Workbook` yapıcı metodu, varsayılan çalışma sayfası koleksiyonunu oluşturur, böylece verileri hemen eklemeye başlayabilirsiniz.

> **Pro ipucu:** Birden fazla sayfa ihtiyacınız varsa, hücreleri doldurmaya başlamadan önce `workbook.Worksheets.Add()` çağırabilirsiniz.

![excel çalışma kitabı oluşturma örneği](image-placeholder.png "excel çalışma kitabı oluşturma ekran görüntüsü")

*Görsel alt metni: IDE içinde boş bir Excel sayfasını gösteren excel çalışma kitabı oluşturma örneği.*

## Bir Hücreye Özel Sayı Biçimi Uygula

Artık çalışma kitabı var, **A1** hücresine bir sayı koyup ona özel bir biçim verelim. Özel sayı biçimleri, sayıları nasıl göstereceğinizi kontrol etmenizi sağlar—para birimi, yüzde, tarih veya bizim örneğimizde bilimsel gösterim gibi.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Neden önce stili alıyoruz? Çünkü `Cell` nesnesi, yazı tipleri, kenarlıklar, hizalama ve sayı biçimlendirmesini tek bir yerde tutan bir **Style** nesnesi saklar. `Custom` özelliğini düzenleyerek Excel'e “bu değeri iki ondalık basamaklı bilimsel gösterimde göster” diyoruz.

> **Sık sorulan soru:** *Yerleşik bir biçim yerine özel bir biçim kullanabilir miyim?*  
> Evet—yerleşik bilimsel bir biçim için `style.Number = 10` ayarlayabilirsiniz, ancak özel dize ondalık basamaklar üzerinde kesin kontrol sağlar.

## Hücre Stilini Programatik Olarak Ayarla (Sayı Biçiminin Ötesinde)

Çoğu zaman sadece sayı biçiminden daha fazlasını istersiniz. Hücreyi öne çıkarmak için kalın bir yazı tipi ve açık gri bir arka plan ekleyelim.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Daha önce düzenlediğimiz aynı `style` nesnesini yeniden kullandığımıza dikkat edin. **Programatik olarak hücre stilini ayarlama** güzelliği burada; stili sadece bir kez alır, ihtiyacınız olan özellikleri değiştirir ve geri yazarız. Nesneleri yeniden oluşturmanıza ya da zaten ayarladığınız sayı biçimini kaybetmenize gerek yok.

## Hücreyi Bilimsel Gösterimde Biçimlendir (Köşe‑Durum İşleme)

Çok büyük ya da çok küçük sayılarla çalışıyorsanız, bilimsel gösterim bir kurtarıcıdır. Kullandığımız özel biçim (`0.00E+00`) ondalık noktadan sonra iki basamak garantiler ve üs için artı işareti zorlar. İşte hızlı bir doğrulama:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Oluşturulan dosyayı açtığınızda, B2 hücresi `1.23E-05` olarak görünecek ve **format cell scientific notation** yönergesinin hem büyük hem de küçük sayılar için çalıştığını onaylayacaktır.

## Çalışma Kitabını XLSX Olarak Kaydet

Tüm eğlence, dosyayı diske gerçekten yazdığınızda sona erer. `Save` metodu, bellekteki temsili doğru bir `.xlsx` paketi haline getirerek işi halleder.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Bu satır **save workbook to xlsx** hedefini gerçekleştirir. Klasör mevcut değilse, `Save` bir istisna fırlatır—bu yüzden klasörü önceden oluşturduğunuzdan emin olun ya da çağrıyı bir try/catch bloğuna alın.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Artık güzel biçimlendirilmiş bir bilimsel sayı, kalın stil ve açık gri arka plan içeren, paylaşmaya hazır bir Excel dosyanız var.

## Tam Çalışan Örnek

Aşağıda, her parçayı bir araya getiren, kopyala‑yapıştır‑hazır program yer alıyor. Konsol uygulaması olarak derlenir, ancak mantığı herhangi bir C# projesine de ekleyebilirsiniz.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Beklenen sonuç:** `CustomFormatted.xlsx` dosyasını açtığınızda şunları göreceksiniz:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Her iki hücre de kalın, açık gri dolgu içerir ve sayılar iki ondalık basamaklı bilimsel gösterimde görüntülenir.

---

## Özet

Sıfırdan **excel çalışma kitabı oluşturduk**, **özel sayı biçimi uyguladık**, **hücreyi bilimsel gösterimde biçimlendirdik**, **hücre stilini programatik olarak ayarladık** ve **çalışma kitabını xlsx olarak kaydettik**—hepsi sadece birkaç C# satırıyla. Yaklaşım ölçeklenebilir: satırlar üzerinde döngü kurun, `style` nesnesini klonlayın ve saniyeler içinde tamamen stilize bir rapor elde edin.

### Sıradaki Adım Ne?

- **Dinamik biçimlendirme:** Değer büyüklüğüne göre biçimleri değiştirin (ör. para birimi vs. yüzde).  
- **Birden fazla sayfa:** `workbook.Worksheets.Add("Summary")` kullanarak gösterge panoları oluşturun.  
- **İleri seviye stil:** Kenarlıklar, koşullu biçimlendirme ve veri doğrulama

## İlgili Öğreticiler

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}