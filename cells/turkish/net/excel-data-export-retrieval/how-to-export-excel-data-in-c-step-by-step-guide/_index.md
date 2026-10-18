---
category: general
date: 2026-03-21
description: Aspose.Cells kullanarak C#'ta sütun adlarıyla Excel verilerini dışa aktarma,
  sayı formatını koruma ve belirli satırları okuma. Excel çalışma sayfasını okumayı
  ve belirli satırları verimli bir şekilde dışa aktarmayı öğrenin.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: tr
og_description: Aspose.Cells kullanarak sütun adlarıyla Excel verilerini dışa aktarma,
  sayı formatını koruma ve belirli satırları okuma. C# geliştiricileri için tam, çalıştırılabilir
  bir örnek.
og_title: C#'ta Excel Verilerini Dışa Aktarma – Tam Programlama Rehberi
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C# ile Excel Verilerini Dışa Aktarma – Adım Adım Rehber
url: /tr/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Excel Verilerini Dışa Aktarma – Tam Programlama Rehberi

Orijinal biçimlendirmeyi kaybetmeden **excel verilerini nasıl dışa aktaracağınızı** hiç merak ettiniz mi? Belki hızlı bir kopyala‑yapıştır denediniz ve tarihlerin “44728” gibi göründüğünü ya da sütun başlıklarının eksik olduğunu gördünüz. Bu can sıkıcı, değil mi? Bu öğreticide, bir Excel çalışma sayfasını okumanın, sayı biçimini korumanın, sütun adlarıyla dışa aktarmanın ve hatta sadece ihtiyacınız olan satırları seçmenin temiz, uçtan uca bir yolunu göreceksiniz.

Aspose.Cells kütüphanesini kullanacağız çünkü dışa aktarma seçenekleri üzerinde ince ayar kontrolü sağlıyor. Bu rehberin sonunda, herhangi bir .NET projesine ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız ve her seçeneğin neden önemli olduğunu anlayacaksınız. Harici belgelere ihtiyaç yok—gereken her şey burada.

---

## Öğrenecekleriniz

- **Read Excel worksheet**'i Aspose.Cells ile belleğe okuyun.
- **Export specific rows** (ör. rows 0‑49) sütun adlarını koruyarak dışa aktarın.
- **Preserve number format**'ı koruyarak para birimleri, tarih ve yüzde değerlerinin bozulmamasını sağlayın.
- **export with column names**'i nasıl yapacağınızı ve gerekirse hücre yorumlarını eklemeyi öğrenin.
- Tam, çalıştırmaya hazır bir C# örneği ve yaygın hatalar için ipuçları.

### Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.6+ ile de çalışır).
- NuGet üzerinden kurulan Aspose.Cells for .NET (`Install-Package Aspose.Cells`).
- Referans verebileceğiniz bir klasöre yerleştirilmiş bir Excel dosyası (`input.xlsx`).

> **Pro tip:** Bir CI hattındaysanız, lisans sürprizlerinden kaçınmak için NuGet paketini özel bir beslemeden çekmeyi düşünün.

---

## 1. Adım – Aspose.Cells'i Kurun ve Ad Alanlarını Ekleyin

İlk olarak, Aspose.Cells paketinin projenizde olduğundan emin olun. Package Manager Console'u açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.Cells
```

Ardından, C# dosyanızın en üstüne gerekli `using` yönergelerini ekleyin:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Bu importlar, **reading an Excel worksheet** ve veri dışa aktarma için temel parçalar olan `Workbook`, `Worksheet`, `ExportTableOptions` ve `DataTable`'a erişim sağlar.

---

## 2. Adım – Çalışma Kitabını Yükleyin (Excel Dosyasını Okuyun)

Şimdi gerçekten **read the Excel worksheet** yapıyoruz. `Workbook` yapıcı metodu dosyanın yolunu alır ve Aspose.Cells hem `.xlsx` hem de eski `.xls` formatlarını işleyebilir.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Neden önemli:** Çalışma kitabını bir kez yükleyip aynı `Worksheet` nesnesini tekrar kullanmak, özellikle büyük elektronik tablolarda dosyayı tekrar tekrar açmaktan çok daha verimlidir.

---

## 3. Adım – Dışa Aktarma Seçeneklerini Yapılandırın (Sayı Biçimini Koru & Sütun Adları)

Burada Aspose.Cells'e *nasıl* dışa aktarılacağını söylüyoruz. `ExportTableOptions` sınıfı çıktıyı ince ayar yapmamıza izin verir. Üç bayrağı etkinleştireceğiz:

1. `ExportAsString = true` – her hücreyi bir dizeye zorlar, bu da sayıların görsel temsillerini korur.
2. `IncludeCellComments = true` – hücrelere eklenmiş yorumları kopyalar (belgeleme için kullanışlı).
3. `PreserveNumberFormat = true` – orijinal sayı biçimini korur (para birimi simgeleri, tarih desenleri vb.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Köşe durumu:** `ExportAsString`'i `false` yaparsanız ama yine de sayı biçimlerini korumak isterseniz, ham sayısal değerlerle (ör. bir tarih için 44728) karşılaşabilirsiniz. Her iki bayrağı da açık tutmak bu sürprizi önler.

---

## 4. Adım – İlk Çalışma Sayfasını Alın (Excel Worksheet'ı Okuyun)

Çoğu basit dosyada ihtiyacınız olan veri ilk sayfada bulunur, bu yüzden indekse göre alacağız. Farklı bir sayfa gerekiyorsa, `0` yerine uygun sıfır‑tabanlı indeksi koyun ya da `workbook.Worksheets["SheetName"]` kullanın.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Neden faydalı:** Çalışma sayfası nesnesine doğrudan erişmek, `Cells` koleksiyonu üzerinde tam kontrol sağlar; bu, daha sonra **export specific rows** için esastır.

---

## 5. Adım – Hücre Aralığını Dışa Aktarın (Belirli Satırları Dışa Aktarın)

Şimdi öğreticinin kalbi: rows 0‑49 ve columns 0‑4 (yani ilk 50 satır ve ilk beş sütun) `DataTable`'a dışa aktarmak. Ayrıca Aspose.Cells'ten `DataTable`'ın ilk satırı olarak sütun adlarını eklemesini isteyeceğiz.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Bunun Ne Yaptığı

- **`startRow: 0`** – sayfanın en üstünden başlar.
- **`totalRows: 50`** – ilk 50 satırı alır (yani **export specific rows**).
- **`totalColumns: 5`** – dışa aktarmayı ilk beş sütunla sınırlar.
- **`includeColumnNames: true`** – `DataTable` sütun başlıklarının Excel başlık satırıyla eşleşmesini sağlar, **export with column names** gereksinimini karşılar.
- **`exportOptions`** – Adım 3'teki ayarları uygular, böylece sayısal değerler “$1,234.56” gibi görünür, “1234.56” yerine.

---

## 6. Adım – Dışa Aktarmayı Doğrulayın (Sonuç Nasıl Görünüyor)

İlk birkaç satırı konsola yazdıralım, böylece biçimlendirmelerin korunduğunu görebilirsiniz.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Beklenen çıktı (örnek):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Tarihlerin `MM/dd/yyyy` formatında ve para biriminin `$` sembolünü koruduğuna dikkat edin—**preserve number format** sayesinde.

---

## Yaygın Tuzaklar ve Nasıl Önlenir

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Tarihler büyük sayılara dönüşür | `ExportAsString` `false` bırakıldı | `ExportAsString = true` tutun` veya hücreleri manuel olarak dönüştürün |
| Sütun başlıkları eksik | `includeColumnNames` `false` olarak ayarlandı | **export with column names** gerektiğinde `true` olarak ayarlayın |
| Yorumlar kaybolur | `IncludeCellComments` etkinleştirilmedi | `ExportTableOptions` içinde `IncludeCellComments`'i açın |
| Yanlış sayfa dışa aktarılıyor | Çok sayfalı dosyada `Worksheets[0]` kullanılması | Sayfa adını belirtin: `workbook.Worksheets["Data"]` |
| Aralık dışı istisna | `totalRows` gerçek satır sayısını aşıyor | `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` kullanın |

---

## Bonus: Tüm Sayfayı Dışa Aktarma ve Biçimleri Korumaya Devam Etme

Daha sonra tüm sayfaya ihtiyacınız olursa, `totalRows` ve `totalColumns` değerlerini sayfanın maksimum boyutlarıyla değiştirin:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Artık herhangi bir boyutta çalışan bir **read excel worksheet** rutininiz var, aynı zamanda **preserving number format** ve **exporting with column names** özelliklerini koruyor.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, bir console uygulamasına ekleyebileceğiniz tam program yer alıyor. Tüm adımları, importları ve basit bir doğrulama çıktısını içerir.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

`Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve terminalinizde biçimlendirilmiş önizlemeyi görmelisiniz.

---

## Sonuç

Aspose.Cells kullanarak **how to export excel** verilerini nasıl dışa aktaracağımızı adım adım inceledik; çalışma kitabını yüklemekten sayı biçimini korumaya, sütun adlarıyla dışa aktarmaya ve dışa aktarmayı belirli satırlarla sınırlamaya kadar her şeyi kapsadık. Kod bağımsız, tamamen çalıştırılabilir ve en yaygın köşe durumları için pratik önlemler içeriyor.

Bir sonraki meydan okumaya hazır mısınız? Orijinal sayı biçimini koruyarak doğrudan CSV'ye dışa aktarmayı deneyin ya da `DataTable`'ı toplu veri eklemek için bir Entity Framework Core bağlamına gönderin. Her iki senaryo da burada ele aldığımız aynı temeller üzerine kuruludur.

Bu rehberi faydalı bulduysanız

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}