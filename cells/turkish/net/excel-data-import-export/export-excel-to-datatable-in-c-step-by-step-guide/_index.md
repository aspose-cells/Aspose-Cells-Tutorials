---
category: general
date: 2026-03-25
description: C#'ta Excel'i DataTable'a hızlı bir şekilde nasıl dışa aktaracağınızı
  öğrenin. Bu öğreticide, sütun adlarıyla Excel dışa aktarımı ve güvenilir veri işleme
  için Excel verilerini string olarak dışa aktarma konuları ele alınmaktadır.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: tr
og_description: C#'ta Excel'i sütun adları ve dize dönüşümüyle DataTable'a aktarın.
  Hazır‑çalıştırılabilir bir çözüm için bu özlü öğreticiyi izleyin.
og_title: C#'ta Excel'i DataTable'a Aktarma – Tam Kılavuz
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: C#'ta Excel'i DataTable'a Aktarma – Adım Adım Kılavuz
url: /tr/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i DataTable'a Aktarma C# – Adım Adım Kılavuz

Hiç **Excel'i DataTable'a aktarmak** istediğinizde hangi bayrakları ayarlamanız gerektiğinden emin olmadınız mı? Yalnız değilsiniz—birçok geliştirici, bir elektronik tablo verisini `DataTable`'a ilk kez çekmeye çalıştığında aynı sorunla karşılaşıyor.  

İyi haber? Sadece birkaç satır kodla **Excel'i sütun adlarıyla dışa aktarabilir** ve hatta **Excel verilerini string olarak dışa aktararak** tip uyumsuzluğu sorunlarından kaçınabilirsiniz. Aşağıda, her ayarın “neden”ini açıklayan eksiksiz, çalıştırılabilir bir örnek bulacaksınız; böylece tahmin yürütmeden herhangi bir projeye uyarlayabilirsiniz.

## Bu Eğitimde Neler Ele Alınıyor

* Bellekte bir çalışma kitabı (workbook) oluşturma (fiziksel dosya gerekmez).  
* Sonucu anında görebilmeniz için birkaç örnek satır doldurma.  
* `ExportTableOptions` ayarını, her hücreyi string olarak ele alacak şekilde yapılandırma.  
* İlk satırı sütun başlığı olarak koruyarak dikdörtgen bir aralığı `DataTable`'a dışa aktarma.  
* Çıktıyı doğrulama ve ilk satırı konsola yazdırma.  

Harici dokümantasyon bağlantılarına gerek yok—gereken her şey burada. Diskte zaten bir Excel dosyanız varsa, sadece workbook oluşturma satırını `new Workbook("path/to/file.xlsx")` ile değiştirin, gerisi aynı kalır.

---

## Adım 1: Projeyi Hazırlayın ve Aspose.Cells NuGet Paketini Ekleyin

Kod yazmaya başlamadan önce projenizin **Aspose.Cells for .NET** ( `Workbook` sınıfını sağlayan kütüphane) referansına sahip olduğundan emin olun. NuGet Package Manager üzerinden ekleyebilirsiniz:

```bash
dotnet add package Aspose.Cells
```

> **Pro ipucu:** En yeni kararlı sürümü (Mart 2026 itibarıyla 22.12) kullanarak en yeni hata düzeltmeleri ve performans iyileştirmelerinden faydalanın.

---

## Adım 2: Bir Workbook Oluşturun ve Örnek Veri ile Doldurun

Yeni bir `Workbook` ile başlayacağız ve dışa aktarımı anında görebilmeniz için birkaç satır ekleyeceğiz. Bu adım aynı zamanda **excel'i datatable'a nasıl dışa aktarılır** konusunu, kaynak verinin yalnızca bellekte bulunduğu durumlarda gösterir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Bu neden önemli:* Başlık satırını (`A1` & `B1`) önce ekleyerek, dışa aktarıcının ilk satırı sütun adı olarak ele almasını sağlayabiliriz—tam da **excel'i sütun adlarıyla dışa aktarma** anlamı budur.

---

## Adım 3: Aspose.Cells'ı Her Hücreyi String Olarak İşlemeye Zorlayın

Sayısal veya tarih hücrelerini dışa aktarırken Aspose .NET tipini tahmin etmeye çalışır. Bu, alt kodunuzun string beklediği durumlarda ince hatalara yol açabilir. `ExportTableOptions.ExportAsString` bayrağı, tek tip string dönüşümünü zorlar.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Bunu neden kullanmalı?* Bazen sayılar, bazen metin içeren bir sütun düşünün (ör. “00123” vs. “ABC”). Her şeyi string olarak dışa aktararak ön ek sıfırlarını kaybetmez ve tip dönüşüm istisnaları almazsınız.

---

## Adım 4: İstenen Aralığı DataTable'a Dışa Aktarın

Şimdi gerçekten **excel'i datatable'a dışa aktarıyoruz**. `ExportDataTable` metodu, başlangıç satır/sütun, satır/sütun sayısı, sütun adı çıkarma bayrağı ve az önce oluşturduğumuz seçenekleri alır.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Arka planda ne oluyor?*  
- `startRow: 0` ilk Excel satırını (başlık satırı) işaret eder.  
- `exportColumnNames: true` Aspose'a “Name” ve “Age” değerlerini `DataTable`'ın sütun koleksiyonuna eklemesini söyler.  
- `totalRows`/`totalColumns` gerçek veriden daha büyük olabilir; fazla hücreler `ExportAsString` sayesinde boş string olarak döner.

---

## Adım 5: Sonucu Doğrulayın – İlk Satırı Yazdırın

Konsola hızlı bir dump, dönüşümün başarılı olduğunu ve sütun adlarının korunduğunu kanıtlar.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Beklenen çıktı**

```
First row: Alice, 30
```

Örnek veriyi değiştirirseniz, konsol otomatik olarak bu değişiklikleri yansıtacaktır—ekstra bir kod eklemenize gerek yok.

---

## Sık Sorulan Sorular & Kenar Durumlar

| Soru | Cevap |
|----------|--------|
| **Diskte zaten var olan bir sayfayı dışa aktarabilir miyim?** | Evet—`new Workbook()` ifadesini `new Workbook("myFile.xlsx")` ile değiştirin. Diğer adımlar aynı kalır. |
| **Excel dosyamda birleştirilmiş hücreler varsa ne olur?** | Birleştirilmiş hücreler açılır; üst‑sol hücrenin değeri tüm birleştirilmiş aralık için kullanılır. |
| **Kültüre özgü sayı formatlarıyla uğraşmam gerekir mi?** | `ExportAsString = true` olduğunda gerek yok; her şey Excel'de görülen ham string olarak gelir. |
| **Bir seferde kaç satır dışa aktarabilirim?** | Aspose.Cells milyonlarca satırı işleyebilir, ancak `DataTable` boyutu arttıkça bellek tüketimi artar. Limitlere ulaşırsanız sayfalama (paging) düşünün. |
| **Gizli sütunlar dışa aktarılıyor mu?** | Gizli sütunlar varsayılan olarak dışa aktarılır; `ExportTableOptions` içinde `ExportHiddenColumns = false` ayarlarsanız gizlenir. |

---

## Bonus: DataTable Yerine CSV'ye Dışa Aktarma

Bazen düz bir dosya tercih edebilirsiniz. Aynı `ExportTableOptions` nesnesi `ExportDataTableToCSV` ile yeniden kullanılabilir:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Bu tek satır, **excel verilerini string olarak dışa aktarırken** hazır bir CSV sunar.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Programı çalıştırın (`dotnet run`) ve **excel'i datatable'a dışa aktarma** sonucunun konsola yazdırıldığını göreceksiniz. Örnek veriyi değiştirin, `totalRows`/`totalColumns` değerlerini ayarlayın veya workbook'u gerçek bir dosyaya yönlendirin—her şey ölçeklenebilir.

---

## Sonuç

Artık C# içinde **Excel'i DataTable'a dışa aktarmak** için **tam, bağımsız bir çözüm** elinizde. `ExportTableOptions.ExportAsString` ayarını yapılandırarak **excel verilerini string olarak dışa aktar** garantisini elde eder, `exportColumnNames: true` ile **excel'i sütun adlarıyla dışa aktarma** ihtiyacınızı karşılayabilirsiniz.  

Bundan sonra şunları yapabilirsiniz:

* `DataTable`'ı Entity Framework veya Dapper ile toplu eklemeler için besleyin.  
* **FastReport** veya **RDLC** gibi bir raporlama motoruna aktarın.  
* API yanıtı için JSON'a dönüştürün (`JsonConvert.SerializeObject(table)`).

Denemekten çekinmeyin—belki daha büyük bir sayfa dışa aktarın ya da **excel'i datatable'a nasıl dışa aktarılır** konusunu bir ağ paylaşımından deneyin. Desen aynı kalır ve kod üretime hazırdır.

---

![Excel → DataTable dönüşüm akışı diyagramı – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}