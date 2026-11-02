---
category: general
date: 2026-09-24
description: Excel çalışma kitabını programlı olarak oluşturun ve birden fazla detay
  sayfası oluşturmayı öğrenin, ardından çalışma kitabını xlsx dosyası olarak kaydedin,
  net bir C# örneğiyle.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: tr
lastmod: 2026-09-24
og_description: Excel çalışma kitabını programlı olarak oluşturun, birden fazla detay
  sayfası oluşturmayı ve çalışma kitabını tek bir çalıştırılabilir örnek içinde xlsx
  dosyası olarak kaydetmeyi görün.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Excel çalışma kitabını programlı olarak oluşturma – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Akıllı İşaretçiler Kullanarak Programlı Şekilde Excel Çalışma Kitabı Oluştur
url: /tr/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programatik Olarak Smart Markers Kullanarak Excel Çalışma Kitabı Oluşturma

Programatik olarak **Excel çalışma kitabı oluşturmanız** gerekiyorsa, bu kılavuz Aspose.Cells .NET ile bunu tam olarak nasıl yapacağınızı gösterir. Ayrıca tek bir veri kaynağından **birden fazla detay sayfası oluşturmayı** ve sonunda **çalışma kitabını xlsx dosyası olarak kaydetmeyi** manuel adım olmadan keşfedeceksiniz.  

Çözüm bağımsızdır: kodun her satırını adım adım inceler, her ayarın neden önemli olduğunu açıklarız ve yinelenen sayfa adları gibi yaygın tuzakları ele alırız. Sonunda, bir ana sayfa ve bir dizi detay sayfası içeren bir çalışma kitabı üreten, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Gereksinimler

| Önkoşul | Sebep |
|--------------|--------|
| .NET 6.0 SDK or later | C# konsol uygulaması için çalışma zamanını sağlar |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | `Workbook`, `SmartMarkerProcessor`, and `SmartMarkerOptions` sınıflarını sağlar |
| A simple data source (e.g., `DataTable` or a list of objects) | Smart Markers'ın genişleteceği değerleri sağlar |
| Visual Studio 2022 or any editor that supports .NET | Kodu derlemeyi ve çalıştırmayı kolaylaştırır |

> **Pro ipucu:** Başlamadan önce CLI üzerinden Aspose.Cells paketini kurun:  
> `dotnet add package Aspose.Cells`

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol projesi oluşturun ve gerekli ad alanlarını kapsam içine alın.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Neden önemli*: `Aspose.Cells` çalışma kitabı yaşam döngüsünü yönetirken, `Aspose.Cells.SmartMarkers` tek bir şablondan birden fazla sayfa oluşturabilen güçlü Smart Marker motorunu size sağlar.

## Adım 2: Excel çalışma kitabını programatik olarak oluşturun

İlk somut adım, bir `Workbook` örneği oluşturmaktır. Bu nesne, tüm Excel dosyasını bellek içinde temsil eder.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Eğer zaten başlık satırları veya biçimlendirme içeren bir şablondan başlamak isterseniz, `new Workbook()` ifadesini `new Workbook("Template.xlsx")` ile değiştirin. Sürecin geri kalanı aynı şekilde çalışır.

## Adım 3: Smart Marker şablonunu hazırlayın

Smart Markers, `&=Employees.Name` gibi yer tutucular içeren hücre içeriklerinde çalışır. Bu öğreticide basit bir şablonu doğrudan kodla ekleyeceğiz, ancak sayfayı Excel'de manuel olarak da düzenleyebilirsiniz.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Neden önemli*: `&=Employees.Name` yer tutucusu, Smart Marker işlemcisine `Employees` koleksiyonunu yinelemesini söyler. Her yineleme yeni bir çalışma sayfası oluşturur çünkü işlemciyi her satır için bir **detay sayfası** oluşturacak şekilde yapılandıracağız.

## Adım 4: Birden fazla satır içeren veri kaynağı oluşturun

Çalışan kayıtları koleksiyonunu taklit etmenin hızlı bir yolu olarak bir `DataTable` kullanacağız.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Bunu herhangi bir `IEnumerable` (ör. `List<Employee>`) ile değiştirebilirsiniz – Smart Markers, `IEnumerable` uygulayan herhangi bir veri kaynağını kabul eder.

## Adım 5: Smart Marker seçeneklerini yapılandırın – birden fazla detay sayfası nasıl oluşturulur

Varsayılan olarak, Smart Markers verileri aynı sayfaya yazar. **Birden fazla detay sayfası** oluşturmak için `DetailSheetNewName` özelliğini ayarlamanız gerekir. Bu aynı zamanda **birden fazla detay sayfası oluşturmanın** isim çakışması olmadan nasıl yapılacağını gösterir.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Veri kaynağı yinelenen isimler içeriyorsa, işlemci otomatik olarak sayısal bir ek (ör. `Detail_1`, `Detail_2`) ekler. Bu, çalışma zamanı hatalarını önler ve tüm detay sayfalarının kaydedilmesini sağlar.

## Adım 6: Smart Markers'ı işleyin

Şimdi işlemciyi çağırıyoruz, veri kaynağını ve az önce tanımladığımız seçenekleri geçiriyoruz.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Neden önemli*: İşlemci `&=Employees.Name` yer tutucusunu okur, `employees` tablosundaki her satırı yineleyerek “Detail” adlı yeni bir sayfa oluşturur ve satır verilerini o sayfaya yazar. Orijinal sayfa bir özet ya da ana sayfa olarak kalır.

## Adım 7: Çalışma kitabını xlsx dosyası olarak kaydedin

Son olarak, **çalışma kitabını xlsx dosyası olarak kaydet** desenini kullanarak çalışma kitabını diske kaydedin.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`SaveFormat.Xlsx` enum'u, dosyanın modern Office Open XML formatında saklanmasını garanti eder; bu format Excel 2007+ ve çoğu bulut hizmetiyle uyumludur.

## Tam, çalıştırılabilir örnek

Aşağıdaki kodu bir .NET konsol projesinin `Program.cs` dosyasına kopyalayıp çalıştırın. Program, `output` klasöründe `detail.xlsx` dosyasını oluşturacak; bu dosya bir ana sayfa ve üç detay sayfası (her çalışan için bir) içerecek.

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Beklenen çıktı**

- `output/detail.xlsx` şunları içerir:
  - **Sheet1** – “Employee Report” başlığıyla orijinal şablon.
  - **Detail** – Alice kaydıyla ilk detay sayfası.
  - **Detail_1** – Bob kaydıyla ikinci detay sayfası.
  - **Detail_2** – Carol kaydıyla üçüncü detay sayfası.

Dosyayı Excel'de açtığınızda her çalışanın kendi sayfasında olduğunu göreceksiniz; bu da **birden fazla detay sayfası oluşturduğumuzu** ve **çalışma kitabını xlsx dosyası olarak kaydettiğimizi** kanıtlar.

## Yaygın sorular ve kenar‑durum yönetimi

| Soru | Cevap |
|----------|--------|
| *Her detay sayfası için özel bir isim gerekirse ne yapmalıyım?* | `DetailSheetNewName = "Employee_"` ayarlayın ve veri kaynağında `SheetName` adlı bir sütun ekleyin. İşlemci, temel isme `SheetName` değerini ekleyecektir. |
| *Orijinal sayfayı tüm detayların bir özeti olarak tutabilir miyim?* | Evet. Ana sayfa dokunulmaz kalır; oluşturulan detay sayfalarına referans veren formüller ekleyebilirsiniz. |
| *Veri kaynağı boş olduğunda ne olur?* | Detay sayfaları oluşturulmaz, ancak çalışma kitabı yine de kaydedilir. Özel bir işlem yapmanız gerekiyorsa işlemden önce `employees.Rows.Count` değerini kontrol etmeyi düşünün. |
| *Mevcut bir şablon dosyasını kullanmak mümkün mü?* | `new Workbook()` ifadesini `new Workbook("Template.xlsx")` ile değiştirin. Tüm Smart Marker mantığı aynı şekilde çalışır. |

## Sonuç

Artık **Excel çalışma kitabını programatik olarak nasıl oluşturacağınızı**, Smart Markers kullanarak **birden fazla detay sayfası nasıl oluşturacağınızı** ve Aspose.Cells ile **çalışma kitabını xlsx dosyası olarak nasıl kaydedeceğinizi** biliyorsunuz. Tam örnek, faturalar, raporlar veya bir ana‑detay Excel çıktısının gerektiği herhangi bir senaryo için uyarlanabilir.

### Sonraki adımlar

- **group markers** ve **conditional formatting** gibi diğer Smart Marker özelliklerini keşfedin.
- `DataTable` yerine gerçek bir veritabanı sorgusu kullanarak büyük ölçekli raporlar oluşturun.
- Aynı veriyi PDF olarak dağıtmak için `Workbook.Save("output.pdf", SaveFormat.Pdf)` kullanın.

Farklı adlandırma şemaları, stil veya ek çalışma sayfalarıyla denemeler yapmaktan çekinmeyin—yeni programatik Excel oluşturma becerileriniz üretim kullanımına hazır. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}