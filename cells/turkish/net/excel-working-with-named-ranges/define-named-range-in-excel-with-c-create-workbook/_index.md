---
category: general
date: 2026-08-07
description: C# ile Excel'de adlandırılmış aralık tanımlayın ve bir çalışma sayfasına
  tablo eklemeyi öğrenin, ardından çalışma kitabını programlı olarak dosyaya kaydedin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: tr
lastmod: 2026-08-07
og_description: C# ile Excel'de adlandırılmış aralık tanımlayın ve bir tablo eklemeyi,
  programlı olarak bir çalışma kitabı oluşturmayı ve tek bir akışta çalışma kitabını
  dosyaya kaydetmeyi görün.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: C# ile Excel’de Adlandırılmış Aralık Tanımlama – Tam Çalışma Kitabı Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: C# ile Excel’de adlandırılmış aralık tanımlama – çalışma kitabı oluşturma
url: /tr/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de adlandırılmış aralık tanımlama C# ile – çalışma kitabı oluşturma

Eğer **C# kodundan Excel'de adlandırılmış aralık tanımlamanız** gerekiyorsa, bu öğretici tam olarak nasıl yapılacağını gösterir. Ayrıca **bir çalışma sayfasına tablo eklemeyi**, **çalışma kitabını programlı olarak oluşturmayı** ve sonunda **IDE'den çıkmadan çalışma kitabını dosyaya kaydetmeyi** de göreceksiniz.

Excel dosyalarıyla programlı olarak çalışmak zaman kazandırır, manuel hataları ortadan kaldırır ve otomatik raporlama hatlarını mümkün kılar. Bu rehberde şunları yapacaksınız:

* Sıfırdan yeni bir Excel çalışma kitabı oluşturma.  
* Belirli bir hücre aralığını kapsayan bir tablo ekleme.  
* Adlandırılmış bir aralık tanımlama ve ad çakışmalarını yönetme.  
* Çalışma kitabını diske kalıcı olarak kaydetme.

Tüm adımlar **Aspose.Cells for .NET** kütüphanesini kullanır; bu kütüphane .NET 6+ ve .NET Framework 4.6+ ile çalışır. Ek bir COM interop veya Office kurulumu gerekmez.

## Gereksinimler

* .NET 6 SDK (veya .NET Framework 4.6+).  
* Visual Studio 2022 veya herhangi bir C#‑uyumlu IDE.  
* Aspose.Cells for .NET NuGet paketi (`Install-Package Aspose.Cells`).  

> **Pro tip:** Test aşamasında ücretsiz değerlendirme lisansını kullanın; dağıtıma geçmeden önce üretim lisansı ile değiştirin.

## Adım 1: Excel çalışma kitabını programlı olarak oluşturma

İlk işlem bir `Workbook` nesnesi örneklemektir. Bu nesne, bellekteki tüm Excel dosyasını temsil eder.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Bu neden önemli*: Çalışma kitabını kod içinde oluşturmak, dosya diske dokunmadan önce sayfalar, stiller ve veriler üzerinde tam kontrol sağlar.

## Adım 2: Çalışma sayfasına tablo ekleme

Bir tablo (ListObject olarak da bilinir) yerleşik filtreleme, sıralama ve stil özellikleri sunar. Burada **A1:B5** hücrelerini kapsayan bir tablo oluşturuyor ve ona **SalesData** adını veriyoruz.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Bu neden önemli*: Tabloyu erken eklemek, daha sonra **adlandırılmış aralık** ile veriye referans vermenizi sağlar; tablonun yapılandırılmış referansı formüllerde kullanılabilir.

## Adım 3: Excel’de adlandırılmış aralık tanımlama – çakışmaları yönetme

**Adlandırılmış bir aralık**, bir hücre ya da hücre aralığını işaret eden bir tanımlayıcıdır ve formülleri okunabilir kılar. Eğer aynı ad zaten mevcutsa (örneğin tablo adı **SalesData**), Excel bir çakışma hatası verir. Aşağıdaki kod, bu istisna yakalanıp güvenli bir şekilde devam edilmesini gösterir.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Bu neden önemli*: Ad çakışmalarını ele almak, otomatik görevlerde çalışma zamanında çöküşleri önler. İkinci adlandırılmış aralık **SalesTotal**, tablonun sütununu bir formülde referans alarak gösterir.

## Adım 4: Çalışma kitabını dosyaya kaydetme

Tüm değişikliklerden sonra çalışma kitabını diske kalıcı olarak kaydedin. `Save` metodu birçok formatı destekler; burada varsayılan **.xlsx** kullanılıyor.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Bu neden önemli*: **Programlı olarak çalışma kitabını dosyaya kaydetmek**, toplu işleme, zamanlanmış rapor üretimi ve web API entegrasyonları için olanak tanır.

## Tek bir görünümde tam kaynak kodu

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Beklenen sonuç

* `C:\Temp` içinde **NameConflictHandled.xlsx** adlı bir Excel dosyası oluşur.  
* Sheet 1, ürün‑birim satırlarıyla biçimlendirilmiş **SalesData** tablosunu içerir.  
* **B6** hücresi, **SalesTotal** adlandırılmış aralığı kullanılarak hesaplanan **Units** sütununun toplamını gösterir.  
* Konsol, varsa ad çakışması hakkında bir mesaj ve dosya konumunu onaylayan bir çıktı verir.

## Yaygın sorular & kenar durumları

| Soru | Cevap |
|----------|--------|
| **Birden fazla çalışma sayfasını kapsayan bir adlandırılmış aralık tanımlayabilir miyim?** | Evet. `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` kullanın ve herhangi bir sayfadan referans verin. |
| **Mevcut bir dosyanın üzerine yazmam gerekirse ne yapmalıyım?** | `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })` çağırın. |
| **İsim zaten mevcutken çakışma olmadan bir adlandırılmış aralık nasıl eklenir?** | Yeni eklemeden önce `worksheet.Names.Remove("ExistingName")` kullanın veya benzersiz bir tanımlayıcı üretin (ör. `Guid.NewGuid().ToString("N")`). |
| **Tabloya otomatik stil uygulamanın bir yolu var mı?** | Tabloyu oluşturduktan sonra `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` ayarlayın. |
| **Bu .NET Core’da çalışır mı?** | Aspose.Cells .NET Core, .NET 5/6/7 ve .NET Framework’ü destekler. Aynı NuGet paketini referans göstermeniz yeterlidir. |

## Sonuç

Artık **C# kullanarak Excel’de adlandırılmış aralık tanımlamayı**, **çalışma sayfasına tablo eklemeyi** ve **programlı olarak çalışma kitabını dosyaya kaydetmeyi** biliyorsunuz. Tam örnek, sıfırdan bir Excel çalışma kitabı oluşturmayı, ad çakışmalarını yönetmeyi ve tek bir tekrarlanabilir akışta kullanılabilir bir rapor dosyası üretmeyi gösteriyor.

Sonraki adımda **çalışma sayfasına grafik ekleme**, **PDF’ye dışa aktarma** veya **var olan çalışma kitaplarını okuma** gibi konuları keşfedin. Bu konular, burada ele alınan temeller üzerine inşa edildiği için çözümünüzü daha karmaşık otomasyon senaryolarına genişletmeye hazır olacaksınız. İyi kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve kendi projelerinizde ek API özelliklerini keşfetmenize ve alternatif uygulama yaklaşımlarını denemenize yardımcı olur.

- [Create Named Range of Cells in Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}