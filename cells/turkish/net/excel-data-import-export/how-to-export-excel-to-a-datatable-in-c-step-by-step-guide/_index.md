---
category: general
date: 2026-03-18
description: C#'ta belirli hücreleri işleyen, Excel'i DataTable'a dönüştüren ve sayıları
  biçimlendiren kodla Excel verilerini DataTable'a nasıl dışa aktarılır. Belirli hücrelerin
  dışa aktarımını ve daha fazlasını öğrenin.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: tr
og_description: C#'ta Excel verilerini bir DataTable'a nasıl dışa aktarılır. Bu öğreticide
  belirli hücrelerin dışa aktarılması, Excel'in DataTable'a dönüştürülmesi ve sayıların
  kolayca biçimlendirilmesi gösterilmektedir.
og_title: C#'ta Excel'i DataTable'a Nasıl Dışa Aktarırsınız – Tam Rehber
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C#'ta Excel'i DataTable'a Nasıl Dışa Aktarılır – Adım Adım Kılavuz
url: /tr/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i C#'ta DataTable'a Nasıl Dışa Aktarılır – Adım Adım Kılavuz

Hiç **Excel'i dışa aktarmanın** `DataTable`'a nasıl yapılacağını, biçimlendirmeyi kaybetmeden merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak raporlama, doğrulama veya toplu ekleme işlemleri için bir elektronik tablonun bir dilimini belleğe çekmek zorunda kalıyor. İyi haber? Birkaç C# satırıyla belirli bir aralığı (örneğin *A1:F11*) dışa aktarabilir, her hücreyi string olarak işleyebilir ve hatta özel bir sayı biçimi uygulayabilirsiniz.

Bu öğreticide bilmeniz gereken her şeyi ele alacağız: çalışma kitabını yüklemek, **belirli hücreleri dışa aktarmayı** yapılandırmak, aralığı bir `DataTable`'a dönüştürmek ve boş satırlar ya da bölgeye bağlı sayılar gibi uç durumları ele almak. Sonunda, üretim kodunda **excel to datatable c#** senaryolarında çalışan yeniden kullanılabilir bir metoda sahip olacaksınız.

> **Önkoşullar** – `ExportDataTable` sağlayan Aspose.Cells for .NET kütüphanesine (veya benzer bir API'ye) ihtiyacınız olacak. Örnek .NET 6+ varsayar, ancak kavramlar daha eski sürümlere de uygulanabilir.

---

## Öğrenecekleriniz

- Aspose.Cells kullanarak **Excel'i DataTable'a dönüştürmeyi** öğrenin.
- Tüm değerleri string olarak ele alarak özel bir aralığı (`excel range to datatable`) dışa aktarma.
- Dışa aktarım sırasında iki ondalık basamaklı sayı biçimini (`#,#00.00`) uygulama.
- Yaygın tuzaklar (null satırlar, gizli sütunlar) ve bunlardan nasıl kaçınılacağı.
- Kopyalamaya hazır, tamamen çalıştırılabilir bir kod örneği.

---

## Önkoşullar ve Kurulum

Koda geçmeden önce şunların olduğundan emin olun:

1. **Aspose.Cells for .NET**'i NuGet üzerinden kurun:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Referans verebileceğiniz bir klasöre yerleştirilmiş bir Excel dosyası (`input.xlsx`), örneğin `YOUR_DIRECTORY/input.xlsx`.

3. .NET 6 veya daha yeni bir hedefe sahip bir proje (aşağıda gösterilen `using` ifadeleri doğrudan çalışır).

> **Pro ipucu:** Farklı bir kütüphane (ör. EPPlus veya ClosedXML) kullanıyorsanız, kavram aynı kalır—çalışma kitabını yükleyin, bir aralık seçin ve bir `DataTable` döndüren bir metodu çağırın.

---

## Adım 1: Çalışma Kitabını Yükleyin ve İlk Çalışma Sayfasını Alın

İlk olarak, Excel dosyanızı temsil eden bir `Workbook` nesnesine ihtiyacınız var. Bunu edindikten sonra, herhangi bir çalışma sayfasına indeks ya da ad ile erişebilirsiniz.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Neden Önemli:** Çalışma kitabını erken yüklemek, dışa aktarılacak hücreleri seçmeden önce yapısını (gizli sayfalar, koruma) incelemenizi sağlar. Dosya büyükse, yalnızca gerekli bölümleri akış olarak almak için `LoadOptions` kullanmayı düşünün.

---

## Adım 2: Dışa Aktarım Seçeneklerini Yapılandırın – Tüm Değerleri String Olarak İşleyin

Verileri sonraki işleme (ör. SQL'e toplu ekleme) dışa aktarırken, genellikle **tutarlı bir string temsili** istersiniz. Bu, ileride tip uyuşmazlığı hatalarını önler.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Açıklama:**  
- `ExportAsString = true` Aspose.Cells'e yerel hücre tipini yok saymasını ve biçimlendirilmiş metni döndürmesini söyler.  
- `NumberFormat = "#,##0.00"` sayıları örneğin `1234.5`'i `"1,234.50"` haline getirir—finansal raporlar için faydalıdır.

Orijinal veri tiplerine ihtiyacınız varsa, sadece `ExportAsString` değerini `false` yapın ve dönüşümü kendiniz yönetin.

---

## Adım 3: Belirli Bir Aralığı (A1:F11) DataTable'a Dışa Aktarın

Şimdi **belirli hücreleri dışa aktarma** konusunun özü geliyor. `ExportDataTable` metodu, başlangıç/bitiş satır/sütun indekslerini (sıfır‑tabanlı) ve başlık ekleme bayrağını alır.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Elde Edecekleriniz:** `A`‑`F` sütunlarıyla 11 satır (başlık dahil) içeren bir `DataTable`. Tüm değerler `exportOptions`'a göre biçimlendirilmiş stringler.

---

## Adım 4: Sonucu Doğrulayın – Konsola Yazdırın

Tabloyu başka bir bileşene vermeden önce çıktıyı kontrol etmek her zaman iyi bir fikirdir.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Şuna benzer bir şey görmelisiniz:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Sayısal sütunların iki ondalık basamakla gösterildiğine, tam olarak belirttiğimiz gibi, dikkat edin.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda her şeyi birleştiren tam program yer alıyor. Yeni bir konsol projesine ekleyin, dosya yolunu ayarlayın ve çalıştırın—ekstra yapılandırma gerekmez.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Koddan Çıkarılacak Önemli Noktalar:**

- `ExportTableOptions` nesnesi yeniden kullanılabilir; birden fazla aralık dışa aktarmanız gerektiğinde aynı nesneyi birden çok `ExportDataTable` çağrısına aktarabilirsiniz.
- Dizinleme **0**'dan başlar, bu yüzden `A1` `(0,0)` konumuna karşılık gelir.
- `includeColumnNames` değerini `true` yapmak, ilk satırı otomatik olarak sütun başlıkları olarak kullanır—sonraki `DataTable` işlemleri için harikadır.

---

## Kenar Durumları ve Yaygın Soruların Ele Alınması

### Çalışma sayfasında gizli satırlar veya sütunlar varsa ne olur?

Aspose.Cells varsayılan olarak görünürlüğü korur. Gizli verileri dışa aktarmanız gerekiyorsa, `exportOptions.ExportHiddenRows = true` ve `ExportHiddenColumns = true` olarak ayarlayın.

### Excel dosyam formüller içeriyor—hesaplanmış değerleri alacak mıyım?

Evet. Varsayılan olarak `ExportDataTable` **görüntülenen değeri** (formülün sonucunu) döndürür. Ham formül metnini istiyorsanız, `exportOptions.ExportFormulas = true` olarak ayarlayın.

### Tamamen boş satırları nasıl atlarım?

Dışa aktardıktan sonra `DataTable`'ı temizleyebilirsiniz:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Ayrık bir aralığı (ör. A1:B5 ve D1:E5) dışa aktarabilir miyim?

Aspose.Cells tek bir çağrıda ayrık aralıkları desteklemez. Bunun yerine, her bloğu ayrı ayrı dışa aktarın ve ardından elde edilen `DataTable`'ları manuel olarak birleştirin.

---

## Performans İpuçları

- Birden fazla dışa aktarımda **`ExportTableOptions`'ı yeniden kullanın**; her seferinde yeni bir örnek oluşturmak ihmal edilebilir bir ek yük getirir ancak kodu dağınık hâle getirir.
- **`LoadOptions` ile büyük dosyaları akış olarak işleyin**, böylece tüm çalışma kitabını belleğe yüklemekten kaçının.
- Sadece hızlı bir CSV dışa aktarma ihtiyacınız varsa **`DataTable`'dan kaçının**—`ExportDataTable` kullanışlıdır ancak büyük sayfalar için en bellek‑verimli yöntem değildir.

---

## Sonuç

**Excel'i dışa aktarmanın** `DataTable`'a nasıl yapılacağını, biçimlendirmeyi kontrol ederek, belirli hücre aralıklarını işleyerek ve her değerin string olarak gelmesini sağlayarak adım adım gösterdik. Tam örnek, **convert excel to datatable**, **export specific cells** veya karşılaşabileceğiniz herhangi bir **excel range to datatable** senaryosuna uyarlayabileceğiniz temiz, üretim‑hazır bir yaklaşımı gösteriyor.

Denemekten çekinmeyin: aralığı değiştirin, `ExportAsString`'i açıp kapatın veya `DataTable`'ı doğrudan Entity Framework'e toplu ekleme için yönlendirin. Bu sağlam temele sahip olduğunuzda, sınır yok.

### Sonraki Adımlar ve İlgili Konular

- **DataTable'ı Excel'e geri aktarma** – ters işlemi `ImportDataTable` ile öğrenin.  
- **DataTable'ı SQL Server'a toplu ekleme** – hızlı yüklemeler için `SqlBulkCopy` kullanın.  
- **EPPlus veya ClosedXML ile çalışma** – aynı görevin alternatif kütüphanelerle nasıl göründüğüne bakın.  
- **Dışa aktarımda hücreleri biçimlendirme** – tarih formatları, özel kültür ayarları ve daha fazlası için `ExportTableOptions`'ı daha ayrıntılı inceleyin.

Sorularınız veya farklı bir kullanım senaryonuz mu var? Bir yorum bırakın, sohbeti sürdürelim. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}