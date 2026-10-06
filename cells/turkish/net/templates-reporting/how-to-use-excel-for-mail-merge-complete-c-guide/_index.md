---
category: general
date: 2026-06-21
description: C# ile Excel'i posta birleştirme için nasıl kullanılır. Hücreye açılış
  etiketi eklemeyi, şablonlar oluşturmayı ve dakikalar içinde birleştirilmiş dosyalar
  üretmeyi öğrenin.
draft: false
keywords:
- how to use excel for mail merge
- add opening tag to cell
- excel mail merge c#
- c# asp.net mail merge
- generate excel templates programmatically
language: tr
og_description: Excel'i toplu mektup birleştirme için nasıl kullanılır? Bu rehber,
  hücreye açılış etiketi eklemeyi, bir şablon oluşturmayı ve C# kullanarak birleştirmeyi
  nasıl çalıştıracağınızı gösterir.
og_title: Excel'i Mail Birleştirme İçin Nasıl Kullanılır – Adım Adım C# Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use Excel for mail merge with C#. Learn to add opening tag to
    cell, build templates, and generate merged files in minutes.
  headline: How to Use Excel for Mail Merge – Complete C# Guide
  type: TechArticle
tags:
- Excel
- Mail Merge
- C#
- Aspose.Cells
title: Excel'i Mail Birleştirme İçin Nasıl Kullanılır – Tam C# Rehberi
url: /tr/net/templates-reporting/how-to-use-excel-for-mail-merge-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i Mail Merge için Nasıl Kullanılır – Tam C# Rehberi

Hiç **Excel'i mail merge için nasıl kullanacağınızı** merak ettiniz mi ve her seferinde Excel'i manuel olarak açmak zorunda kalmadınız mı? Tek başınıza değilsiniz. Birçok kurumsal panoda, önceden biçimlendirilmiş bir çalışma sayfasına veri serpiştirip sonucu bir müşteriye ya da raporlama sistemine göndermemiz gerekir. İyi haber? Birkaç C# satırıyla boş bir çalışma kitabını tam özellikli bir mail‑merge şablonuna dönüştürebilir ve motorun ağır işi yapmasını sağlayabilirsiniz.

Bu öğreticide, Aspose.Cells kütüphanesini kullanarak **Excel'i mail merge için nasıl kullanacağınızı** adım adım göstereceğiz. Ayrıca, **add opening tag to cell** adımını da ele alacağız; bu, Departmanlar → Çalışanlar gibi koleksiyonları iç içe yerleştirmenin anahtarıdır. Sonunda, `template.xlsx` dosyasından `output.xlsx` üreten, çalıştırmaya hazır bir proje elde edeceksiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 SDK veya daha yeni bir sürüm (kod .NET Core ve .NET Framework üzerinde çalışır)
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör
- Aspose.Cells for .NET NuGet paketi (`Install-Package Aspose.Cells`)
- `YOUR_DIRECTORY` adlı bir klasör (ya da kod içindeki yolları değiştirin)

Başka bir bağımlılık gerekmez ve örnek Windows, Linux veya macOS üzerinde çalışır.

## Adım 1: Projeyi Oluşturun ve Namespace'leri İçe Aktarın

Yeni bir konsol uygulaması oluşturmak çok kolay:

```bash
dotnet new console -n ExcelMailMergeDemo
cd ExcelMailMergeDemo
dotnet add package Aspose.Cells
```

Şimdi `Program.cs` dosyasını açın ve gerekli `using` ifadelerini ekleyin:

```csharp
using System;
using Aspose.Cells;
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, IDE `Workbook` yazdığınızda `using` eklemenizi otomatik olarak önerir.

## Adım 2: Şablonu İçerecek Çalışma Kitabını Yükleyin

**add opening tag to cell** işlemini yapmadan önce bellekte bir çalışma kitabı yüklü olmalıdır. Bu çalışma kitabı daha sonra mail‑merge motoru için şablon haline gelecektir.

```csharp
// Step 1: Load the workbook that will contain the template
Workbook workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");
```

`template.xlsx` henüz yoksa, Aspose.Cells sizin için yeni, boş bir çalışma kitabı oluşturur. Bu, hızlı denemeler için kullanışlıdır.

## Adım 3: Hedef Çalışma Sayfasına Erişin

Çoğu şablon ilk sayfada bulunur, ancak istediğiniz herhangi bir indeksi hedefleyebilirsiniz. Burada ilk çalışma sayfasını alıyoruz:

```csharp
// Step 2: Access the first worksheet where the template will be placed
Worksheet ws = workbook.Worksheets[0];
```

Unutmayın, çalışma sayfaları sıfır‑tabanlıdır, yani `[0]` Excel'de gördüğünüz ilk sekmedir.

## Adım 4: **Add Opening Tag to Cell** – Üst Koleksiyonu Başlatın

Mail merge etiketleri Mustache/Handlebars sözdizimini (`{{#Collection}}`) takip eder. Motorun bir departman koleksiyonunun başlayacağını anlaması için açılış etiketini bir hücreye yazarız:

```csharp
// Step 3: Insert the opening tag for the parent collection (Departments)
ws.Cells["A1"].PutValue("{{#Departments}}");
```

Neden `A1` hücresine? Çünkü etiketin motor tarafından okunan ilk şey olmasını istiyoruz. Başka bir hücre de seçebilirsiniz, ancak etiketleri üstte tutmak şablonu okumayı kolaylaştırır.

## Adım 5: Departman Adı İçin Yer Tutucu Ekleyin

Şimdi, birleştirme sırasında her departmanın adının görüneceği bir yer eklememiz gerekiyor:

```csharp
// Step 4: Add a placeholder for the department name
ws.Cells["A2"].PutValue("Dept: {{Name}}");
```

`{{Name}}` token'ı, motorun alacağı her `Department` nesnesinin `Name` özelliğiyle değiştirilecektir.

## Adım 6: **Add Opening Tag to Cell** – İç İçe Koleksiyonu Başlatın

Departmanların genellikle birçok çalışanı vardır. Bunları yinelemek için, departman adının hemen ardından iç içe bir koleksiyon açarız:

```csharp
// Step 5: Mark the start of the nested collection (Employees) inside each department
ws.Cells["A3"].PutValue("{{#Employees}}");
```

Yine **add opening tag to cell** yapıyoruz—bu sefer etiket `{{#Employees}}`. İç içe yerleştirme, motorun açılan etiketlerin bir yığını tutması sayesinde çalışır.

## Adım 7: Çalışan Detayları İçin Yer Tutucular Ekleyin

Her çalışanın genellikle bir adı ve soyadı vardır. Her çalışan için tekrarlanacak tek bir satır ekleyelim:

```csharp
// Step 6: Insert placeholders for employee details
ws.Cells["A4"].PutValue("{{FirstName}} {{LastName}}");
```

Daha fazla sütun ekleyebilirsiniz (ör. `{{Title}}`, `{{Salary}}`) mantığı değiştirmeden; sadece yan yana hücrelere koyun.

## Adım 8: İç ve Üst Koleksiyonları Kapatın

Her açılış etiketinin bir kapanış etiketi olmalıdır. Önce `Employees` koleksiyonunu, ardından `Departments` koleksiyonunu kapatıyoruz:

```csharp
// Step 7: Close the nested collection and then the parent collection
ws.Cells["A5"].PutValue("{{/Employees}}");
ws.Cells["A6"].PutValue("{{/Departments}}");
```

Kapanış etiketini unutursanız, birleştirme bir istisna fırlatır—bunu “Yaygın Hatalar” bölümünde ele alacağız.

## Adım 9: Şablonu Birleştirme İçin Kaydedin

Bu noktada çalışma kitabı tam bir şablon içeriyor. Mail‑merge işlemcisi daha sonra kullanabilsin diye kaydedin:

```csharp
// Step 8: Save the workbook with the template ready for mail‑merge processing
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Artık sadece etiketleri içeren `output.xlsx` dosyanız var. Üretim ortamında bu dosyayı ayrı tutar ve yeniden kullanılabilir bir şablon olarak kullanırsınız.

## Adım 10: Mail Merge'i Çalıştırın (Opsiyonel ama Tavsiye Edilir)

Tüm süreci görmek isterseniz, basit bir veri modeli oluşturup birleştirmeyi tetikleyin:

```csharp
// Define data models
public class Department
{
    public string Name { get; set; }
    public Employee[] Employees { get; set; }
}

public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

// Build sample data
var data = new[]
{
    new Department
    {
        Name = "Sales",
        Employees = new[]
        {
            new Employee { FirstName = "Alice", LastName = "Anderson" },
            new Employee { FirstName = "Bob", LastName = "Brown" }
        }
    },
    new Department
    {
        Name = "Engineering",
        Employees = new[]
        {
            new Employee { FirstName = "Charlie", LastName = "Clark" },
            new Employee { FirstName = "Dana", LastName = "Doe" }
        }
    }
};

// Load the template we just saved
Workbook template = new Workbook("YOUR_DIRECTORY/output.xlsx");

// Perform the mail merge
template.Worksheets[0].MailMerge.ExecuteTemplate(data);

// Save the merged result
template.Save("YOUR_DIRECTORY/merged_result.xlsx");
```

Bu kod parçasını çalıştırdığınızda, veri dizisi tarafından tanımlanan sırayla her departman ve çalışanların göründüğü `merged_result.xlsx` oluşur.

### Beklenen Çıktı

| A (birleştirilmiş) |
|--------------------|
| Bölüm: Satış |
| Alice Anderson |
| Bob Brown |
| Bölüm: Mühendislik |
| Charlie Clark |
| Dana Doe |

Dosyayı Excel'de açtığınızda, etiketlerin tarif ettiği tam içeriği göreceksiniz.

## Yaygın Hatalar & Kenar Durumları

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **Kapanış etiketi eksik** (`{{/Employees}}` veya `{{/Departments}}`) | Motor dengeli bir etiket yığını bekler. | Her `{{#…}}` için eşleşen bir `{{/…}}` olduğundan emin olun. |
| **Etiket birleştirilmiş hücrede** | Birleştirilmiş hücreler, temel hücre adresi değiştiği için ayrıştırıcıyı şaşırtabilir. | Etiketleri basit, birleştirilmemiş hücrelerde tutun (ör. A1‑A6). |
| **Büyük veri setleri** | Binlerce satır oluşturmak bellek sınırlarını aşabilir. | `MailMerge.ExecuteTemplate` ile `SaveOptions` kullanarak veriyi diske akıtın. |
| **Farklı sayfa düzeni** | Şablon farklı bir sayfa sırası kullanıyorsa, kod hâlâ `[0]`'a işaret eder. | Sayfayı isme göre alın: `workbook.Worksheets["Template"]`. |
| **Veride özel karakterler** | `{` veya `}` gibi karakterler veri içinde etiket sözdizimini bozar. | Bu karakterleri kaçırın veya farklı bir yer tutucu sözdizimi (`[[FirstName]]`) kullanın. |

## Sorunsuz Bir Deneyim İçin İpuçları

- **Pro ipucu:** Tüm etiketleri **A** sütununda tutun ve geri kalan sütunları statik içerik (başlıklar, formüller, biçimlendirme) için kullanın. Bu ayrım şablonu bakımını kolaylaştırır.
- **Dikkat:** Koşullu bölümler (`{{#if …}}`) eklemeniz gerekiyorsa, Aspose.Cells temel koşullu etiketleri destekler, ancak bunlar da aynı şekilde **add opening tag to cell** ile eklenmelidir.
- **Sürüm kontrolü:** Yukarıdaki kod Aspose.Cells 23.9.0 sürümünü kullanır. Daha yeni sürümler ufak API değişiklikleri içerebilir; her zaman sürüm notlarını gözden geçirin.

## Görsel Genel Bakış

![Excel mail merge şablonu örneği, excel for mail merge nasıl kullanılır gösteriyor](/images/excel-mail-merge-template.png){: .center alt="excel for mail merge nasıl kullanılır şablon örneği"}

Ekran görüntüsü (alt metin ana anahtar kelimeyi içerir) A1‑A6 hücrelerindeki etiketlerin tam yerleşimini gösterir.

## Sonuç

İşte bu kadar—başlangıçtan bitişe kadar **Excel'i mail merge için nasıl kullanacağınızı** gösteren tam çalışabilir bir örnek ve **add opening tag to cell** işlemini nasıl yapacağınızı gösteren bir rehber.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir, böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose.Cells for .NET ile Excel Hücresine Adı ile Nasıl Erişilir: Adım Adım Kılavuz](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel Hücrelerine Kenarlık Ekleme: Adım Adım Kılavuz](/cells/english/net/formatting/add-borders-excel-cells-aspose-cells-dotnet/)
- [Aspose.Cells for .NET ile Excel'de Sayfa Sonu Eklemek – Kapsamlı Kılavuz](/cells/english/net/headers-footers/aspose-cells-net-add-page-breaks-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}