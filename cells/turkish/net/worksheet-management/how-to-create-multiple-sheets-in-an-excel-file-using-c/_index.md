---
category: general
date: 2026-11-25
description: C# kullanarak bir Excel dosyasında birden fazla sayfa oluşturmayı öğrenin.
  Bu rehber, çalışma kitabını XLSX olarak kaydetmeyi ve aynı ada sahip sayfaları yönetmeyi
  kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: tr
lastmod: 2026-11-25
og_description: C# kullanarak bir Excel dosyasında birden fazla sayfa oluşturun. Çalışma
  kitabını XLSX olarak kaydetmek ve yinelenen sayfa adlarını yönetmek için bu kapsamlı
  öğreticiyi izleyin.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: C# ile bir Excel dosyasında birden fazla sayfa oluşturma – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: C# kullanarak bir Excel dosyasında birden fazla sayfa nasıl oluşturulur
url: /tr/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile bir Excel dosyasında birden fazla sayfa nasıl oluşturulur?

Eğer C# üzerinden bir Excel çalışma kitabında **birden fazla sayfa** oluşturmanız gerekiyorsa, bu öğretici size çalıştırmaya hazır bir çözüm sunar. Kılavuzun sonunda, bir ana sayfa (master sheet) oluşturan, akıllı işaretçiler (smart markers) aracılığıyla detay sayfaları ekleyen ve sonucu **XLSX** dosyası olarak kaydeden bir programınız olacak—ve aynı zamanda **yinelenen sayfa adları** güvenli bir şekilde ele alınacak.

Ayrıca Aspose.Cells kütüphanesi ile **excel dosyası oluşturma c#** projelerinin nasıl yapılacağını göreceksiniz; bu kütüphane sunucu tarafı elektronik tablo otomasyonu için popüler bir tercihtir.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 SDK veya daha yeni bir sürüm  
* Visual Studio 2022 (veya .NET destekleyen herhangi bir IDE)  
* **Aspose.Cells for .NET** NuGet paketi (`Aspose.Cells`) – kodda kullanılan `Workbook`, `Worksheet` ve `SmartMarkersFactory` sınıflarını sağlar.  

Paketi aşağıdaki CLI komutuyla ekleyebilirsiniz:

```bash
dotnet add package Aspose.Cells
```

> **Pro ipucu:** Sadece temel özelliklere ihtiyacınız varsa özel bir NuGet beslemesi veya ücretsiz topluluk sürümünü kullanın.

## Çözümün genel görünümü

Yaklaşım dört mantıksal adımdan oluşur:

1. **Yeni bir çalışma kitabı oluşturun** ve ilk çalışma sayfasının adını *Master* olarak belirleyin.  
2. **Akıllı bir işaretçi ekleyin**; bu işaretçi Aspose.Cells’e detay çalışma sayfalarının nasıl adlandırılacağını söyler.  
3. **Akıllı işaretçiyi**, yinelenen adlar içerebilecek bir veri kaynağıyla işleyin.  
4. **Çalışma kitabını** bir XLSX dosyası olarak kaydedin.

Her adım aşağıda ayrıntılı olarak açıklanmıştır ve makalenin sonunda tam kaynak dosyası sağlanmıştır.

## Adım 1: Yeni bir çalışma kitabı oluşturun ve bir ana sayfa ekleyin

`Workbook` sınıfı, bir Excel dosyasının tamamını temsil eder. Parametresiz bir örnek oluşturduğunuzda, Aspose.Cells varsayılan olarak içinde tek bir çalışma sayfası bulunan bir çalışma kitabı yaratır. Bu sayfanın adını *Master* olarak değiştirmek, sayfanın amacını netleştirir.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Neden önemli:**  
Temiz bir çalışma kitabı ile başlamak, önceki çalıştırmalardan kalan biçimlendirme veya gizli sayfaların oluşmasını engeller. Sayfayı *Master* olarak adlandırmak, akıllı işaretçiyi daha sonra bulmanızı kolaylaştırır ve dosyayı teknik olmayan kullanıcılar için okunabilir tutar.

## Adım 2: Detay sayfa adlarını tanımlayan bir akıllı işaretçi ekleyin

Akıllı işaretçiler, Aspose.Cells’in çalışma zamanında veri ile değiştirdiği yer tutuculardır. `&=DetailSheetNewName=Detail` sözdizimi, motorun veri kaynağındaki her satır için yeni bir çalışma sayfası oluşturmasını ve `Detail` sütununun değerini sayfa adı olarak kullanmasını sağlar.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Neden önemli:**  
Akıllı işaretçi, çalışma sayfalarını manuel olarak ekleyen bir döngü yazma ihtiyacını ortadan kaldırır. Ayrıca, ana sayfanın düzenini otomatik olarak her yeni oluşturulan sayfaya kopyalar, böylece tutarlı bir stil sağlanır.

## Adım 3: Yinelenen adlar içerebilecek bir veri kaynağıyla akıllı işaretçiyi işleyin

Aşağıda bir `DataTable` oluşturup veri kaynağını taklit ediyoruz. *Detail* sütununun yinelenen değerler (`"Report"` iki kez) içerdiğine dikkat edin. `SmartMarkersFactory.Process` yöntemi, bu örnek için varsayılan olarak **true** olan `AllowDuplicateSheetNames` ayarını dikkate alır.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Önemli:** Eğer sayfa adlarının kesinlikle benzersiz olmasını istiyorsanız, işleme başlamadan önce `workbook.Settings.CheckDuplicateSheetNames = true;` satırını ekleyin. Varsayılan davranış aynı ada sahip sayfalar oluşturur; Excel bunu izin verse de dosya içinde gezinirken karışıklığa yol açabilir.

## Adım 4: Çalışma kitabını bir XLSX dosyası olarak kaydedin

Son olarak, oluşturulan çalışma kitabını diske kalıcı hâle getirin. `Save` yöntemi, dosya uzantısına göre uygun yazıcıyı otomatik olarak seçer.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Beklenen sonuç**

`duplicate_detail_sheets.xlsx` dosyasını açtığınızda şu tabloyu görmelisiniz:

| Sayfa Adı | İçerik (ilk satır) |
|------------|---------------------|
| Master     | Akıllı işaretçi yer tutucu (veri yok) |
| Report     | Veri satırı 1 (`123.45`) |
| Summary    | Veri satırı 2 (`67.89`) |
| Report (2) | Veri satırı 3 (`101.12`) |

İkinci *Report* sayfası, Aspose.Cells tarafından aynı adı önlemek için otomatik olarak *Report (2)* olarak yeniden adlandırılır; bu sayede hatalı bir durum oluşmaz ancak orijinal yinelenen niyet korunur.

## Tam kaynak kodu

Aşağıdaki dosyayı bir konsol projesine (`dotnet new console`) kopyalayıp çalıştırın. Program, **birden fazla sayfa oluşturma**, **workbook xlsx kaydetme** ve **yinelenen sayfa adlarını yönetme** süreçlerini tam olarak gösterir.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Proje klasöründen `dotnet run` komutunu çalıştırın. Çalıştırma tamamlandığında, üç detay sayfasının oluşturulduğunu, bunlardan ikisinin temel adı **Report** olduğunu doğrulamak için oluşturulan dosyayı açın.

## Kenar durumları ve en iyi uygulamalar

| Durum | Önerilen yaklaşım |
|-----------|----------------------|
| **Çok büyük veri setleri** ( > 10 000 satır) | `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` kullanarak bellek tüketimini azaltın. |
| **Özel sayfa adlandırma kuralları** | `Process` çağırmadan önce `Detail` sütunundaki geçersiz karakterleri (`/ \ ? * [ ] :`) değiştirin. |
| **Gerçekten benzersiz adlar gerekir** | `workbook.Settings.CheckDuplicateSheetNames = true;` ayarını etkinleştirin ve bir yedek adlandırma şeması (ör. GUID ekleme) sağlayın. |
| **XLSX yerine PDF üretmek** | Kaydetme işleminden sonra `workbook.Save("output.pdf", SaveFormat.Pdf);` çağrısı yapın – Aspose.Cells doğrudan PDF’ye dışa aktarabilir. |
| **Web servisinde çalıştırma** | Çalışma kitabını bir `MemoryStream` içine yazın ve dosya indirme olarak döndürerek disk I/O’sundan kaçının. |

### İpucu: Birden fazla dışa aktarma için aynı `Workbook` örneğini yeniden kullanın

Uygulamanız bir istek başına birkaç rapor oluşturuyorsa, tek bir `Workbook` nesnesini bellekte tutun, çalışma sayfalarını `workbook.Worksheets.Clear();` ile temizleyin ve adımları tekrarlayın. Bu, Aspose.Cells çalışma zamanını tekrar tekrar yüklemenin getirdiği yükü azaltır.

## Sonuç

Artık C# kullanarak bir Excel çalışma kitabında **birden fazla sayfa** oluşturmayı, Aspose.Cells ile **excel dosyası oluşturma c#** işlemini, **yinelenen sayfa adlarını** yönetmeyi ve **workbook xlsx** dosyasını güvenilir bir şekilde kaydetmeyi biliyorsunuz. Tam örnek, hızlı betiklerden üretim‑ağır hizmetlere kadar ölçeklenebilen temiz ve sürdürülebilir bir desen sunar.

### Sırada ne var?

* Oluşturulan sayfalarda **koşullu biçimlendirme** ekleyerek kritik değerleri vurgulayın.  
* **Smart Markers** kullanarak tabloları, grafikleri veya pivot tabloları otomatik olarak doldurun.  
* Kodu bir ASP.NET Core API’ye entegre edip XLSX dosyasını indirme akışı olarak döndürün.

Farklı veri kaynakları (JSON, XML veya bir veritabanı) ile denemeler yapın ve raporlama ihtiyaçlarınıza uygun şekilde akıllı işaretçi sözdizimini uyarlayın. Kodlamanın tadını çıkarın!

## Bir sonraki öğrenmeniz gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve konuyla yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Create Excel Workbook C# – Step‑by‑Step Guide to Write Dates & Save as XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create excel workbook and save it to file in C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}