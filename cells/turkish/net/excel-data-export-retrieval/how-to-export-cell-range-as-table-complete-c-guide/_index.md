---
category: general
date: 2026-07-13
description: C# ve ExportTableOptions kullanarak hücre aralığını tablo olarak nasıl
  dışa aktarılır. Adım adım çalışma kitabı kurulumu, biçimlendirme ve tablo dışa aktarımını
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: tr
lastmod: 2026-07-13
og_description: C#'ta ExportTableOptions ile hücre aralığını tablo olarak nasıl dışa
  aktarılır. Hücreleri biçimlendirmek, bir çalışma kitabı oluşturmak ve tabloyu zahmetsizce
  dışa aktarmak için bu rehberi izleyin.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Hücre Aralığını Tablo Olarak Dışa Aktarma – Tam C# Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Hücre Aralığını Tablo Olarak Dışa Aktarma – Tam C# Rehberi
url: /tr/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hücre Aralığını Tablo Olarak Dışa Aktarma – Tam C# Kılavuzu

Hiç **hücre aralığını tablo olarak nasıl dışa aktaracağınızı** formatlama tuhaflıkları yüzünden saçınızı yolmak zorunda kalmadan merak ettiniz mi? Tek başınıza değilsiniz. Verileri bir raporlama hattına besliyor olun ya da sadece hızlı bir CSV‑stil dökümüne ihtiyacınız olsun, dışa aktarma sürecine hâkim olmak size saatlerce manuel kopyala‑yapıştır işinden tasarruf ettirebilir.

Bu öğreticide, sayısal bir hücreyi alıp bilimsel gösterim uygulayarak **ExportTableOptions** kullanarak tablo olarak dışa aktarmak için gereken adımları adım adım göstereceğiz. Sonunda çalıştırılabilir bir kod parçacığına sahip olacak, her çağrının *neden* yapıldığını anlayacak ve kodu daha büyük aralıklar ya da farklı formatlar için nasıl ayarlayacağınızı bileceksiniz.

## Önkoşullar

- .NET 6 veya üzeri (API .NET Framework 4.7+ üzerinde aynı şekilde çalışır)
- Aspose.Cells for .NET yüklü (`Install-Package Aspose.Cells`)
- C# sözdizimi hakkında temel bir kavrayış; derin Excel iç detayları gerekmez

Hepsi hazır mı? Harika—hadi başlayalım.

## Adım 1: Dışa Aktarma Seçeneklerini Ayarlama – Hücre Aralığını Tablo Olarak Dışa Aktarma

İlk olarak, kütüphaneye hücre içeriğini nasıl işleyeceğini söyleyen bir **ExportTableOptions** örneğine ihtiyacınız var. Bunun olmaması durumunda dışa aktarma ham sayısal değerlere varsayılan olarak döner ve bu da metin bekleyen sonraki tüketicileri bozabilir.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Neden Önemli:**  
- `ExportAsString = true` kütüphanenin hücrenin görünen metnini, altında yatan double değerini değil, yazmasını zorlar.  
- `CustomFormat` **bilimsel gösterim dışa aktarımı** uygulamanıza izin verir; çok büyük ya da çok küçük sayılarla çalışırken faydalıdır.

> **Pro ipucu:** Tarih ya da para birimi formatına ihtiyacınız varsa, `"0.00E+00"` ifadesini sırasıyla `"yyyy‑MM‑dd"` veya `"$#,##0.00"` ile değiştirin.

## Adım 2: Bir Workbook Oluşturun ve İlk Worksheet'i Alın – Workbook ve Worksheet İşleme

Bir **Workbook**, tüm Excel dosyasını temsil ederken, bir **Worksheet** tek bir sekmedir. Basit bir dışa aktarma için her zaman indeks 0'da bulunan ilk sayfayı kullanacağız.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Neden Önemli:**  
Yeni bir `Workbook` oluşturmak temiz bir başlangıç sağlar—gizli stiller ya da kalan veriler sizi şaşırtmaz. `Worksheets[0]`'a erişmek, sayfa adlarıyla uğraşmadan aktif sayfayı elde etmenin en hızlı yoludur.

## Adım 3: Hedef Hücreyi Doldurun – Hücre Değeri Biçimlendirme C#

Şimdi **A1** hücresine (satır 0, sütun 0) sayısal bir değer ekliyoruz. Seçtiğimiz değer, bilimsel gösterimin nasıl çalıştığını görebilmeniz için kasıtlı olarak uzun ondalıklı.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Neden Önemli:**  
`PutValue` çağrısı hücrenin veri tipini otomatik olarak çıkarır. Daha sonra string olarak dışa aktardığımız için, ham double önceki ayarladığımız formatla dönüştürülür ve bize düzenli bir `"1.23E+04"` çıktısı verir.

## Adım 4: Tanımlı Hücre Aralığını Tablo Olarak Dışa Aktarın – Hücre Aralığını Tablo Olarak Dışa Aktarma

Seçenekler ve veri hazır olduğunda, son adım Aspose.Cells'e aralığı yazmasını söylemektir. `ExportTable` metodu başlangıç satır/sütun, aralığın boyutu ve oluşturduğumuz seçenek nesnesini bekler.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Neden Önemli:**  
- `totalRows = 1` ve `totalColumns = 1` dışa aktarmayı tek bir hücreyle sınırlar, ancak bu sayıları daha büyük blokları kapsayacak şekilde genişletebilirsiniz (ör. 5 satır × 3 sütun aralığı için `5, 3`).  
- Metod, veriyi CSV, HTML olarak kaydedilebilecek ya da doğrudan bir istemciye akıtılabilecek iç bir tablo yapısına yazar.

### Sonucu Kaydetme (İsteğe Bağlı)

Dışa aktarılan tabloyu diske kalıcı olarak kaydetmek isterseniz, bir CSV dosyasına yazabilirsiniz:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Yukarıdakini çalıştırmak aşağıdaki içeriğe sahip bir dosya oluşturur:

```
1.23E+04
```

## Kenar Durumları ve Yaygın Varyasyonlar

| Durum | Ne Değiştirilmeli | Sebep |
|-----------|----------------|--------|
| **Birden fazla satırı dışa aktarma** | `totalRows`'u ayarlayın ve gerekirse satırlar üzerinde döngü yapın | `ExportTable` metodunu tekrarlamadan toplu dışa aktarmaya izin verir |
| **Formüllerin korunması** | Set `ExportAsString = false` | Orijinal formülü, görüntülenen değer yerine tutar |
| **Farklı ayırıcılar** | Use `ExportTableToCSV(..., ',', ...)` overload | Virgül‑ayırmalıdan sekme‑ayırmalıya ya da boru‑ayırmalı değerlere geçiş yapar |
| **Büyük çalışma sayfaları** | Stream the export to avoid `OutOfMemoryException` | `OutOfMemoryException` hatasından kaçınmak için akış kullanın; 10 000'den fazla satır için iyi çalışır |

## Tam Çalışan Örnek

Aşağıda, tamamen kopyala‑yapıştır‑hazır program yer alıyor. Aspose.Cells referansı eklenmiş herhangi bir .NET konsol projesiyle derlenebilir.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Beklenen çıktı:**  
`ExportedTable.csv` adlı bir dosya, tek bir satır içerir:

```
1.23E+04
```

CSV'yi bir metin düzenleyicide açarsanız, bilimsel gösterimin tam olarak tanımlandığı gibi uygulandığını göreceksiniz.

## Sonuç

**hücre aralığını tablo olarak nasıl dışa aktaracağınızı** baştan sona ele aldık: `ExportTableOptions` ayarlama, `Workbook` oluşturma, veri ekleme ve sonunda `ExportTable` çağırma. Her parçayı anladığınızda, yöntemi daha büyük aralıklar, farklı formatlar için ölçeklendirebilir ya da Excel‑türevi verileri anlık olarak sunan bir web API'sine entegre edebilirsiniz.

İleride, şunları keşfetmek isteyebilirsiniz:

- **ExportTableToHTML** web‑hazır ön izlemeler için
- **ExportTableToDataTable** doğrudan ADO.NET veri akışlarına beslemek için
- Tarihler, para birimleri veya yüzdeler için gelişmiş **özel formatlar**

Bunları deneyin, basit bir hücre dışa aktarmasını çok yönlü bir veri‑teslim motoruna dönüştüreceksiniz. Sorularınız veya ilginç bir kullanım senaryonuz mu var? Aşağıya yorum bırakın—mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Görünür Excel Satırlarını Dışa Aktarma: Adım Adım Kılavuz](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells ile .NET'te Excel Dosyalarını Dışa Aktarma: Kapsamlı Rehber](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET ile Excel Hücresine İsmiyle Erişme: Adım Adım Kılavuz](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}