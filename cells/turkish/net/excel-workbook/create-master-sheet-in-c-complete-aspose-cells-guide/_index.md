---
category: general
date: 2026-03-30
description: Aspose.Cells kullanarak C#'de ana sayfa oluşturun. Excel çalışma kitabını
  C#'de nasıl oluşturacağınızı, aynı sayfa adlarına izin vermeyi ve birkaç adımda
  çalışma kitabını XLSX olarak kaydetmeyi öğrenin.
draft: false
keywords:
- create master sheet
- create excel workbook c#
- save workbook as xlsx
- allow duplicate sheet names
language: tr
og_description: Aspose.Cells ile C#'ta ana sayfa oluşturun. Bu rehber, C#'ta Excel
  çalışma kitabı oluşturmayı, aynı ada sahip sayfalara izin vermeyi ve çalışma kitabını
  XLSX olarak kaydetmeyi gösterir.
og_title: C#'ta ana sayfa oluşturma – Tam Aspose.Cells Rehberi
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'de ana sayfa oluşturma – Tam Aspose.Cells Rehberi
url: /tr/net/excel-workbook/create-master-sheet-in-c-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Ana Sayfa Oluşturma – Tam Aspose.Cells Rehberi

Bir Excel dosyasında **master sheet** oluşturmanız gerektiğinde, aynı temel adı paylaşan bir sürü detay sayfasını nasıl yöneteceğinizden emin olmadınız mı? Yalnız değilsiniz. Birçok raporlama senaryosunda onlarca detay sekmesiyle karşılaşırsınız ve çoğu kütüphanenin varsayılan davranışı, iki sayfanın aynı isimle oluşması durumunda bir istisna fırlatmaktır.

Şanslıysanız, Aspose.Cells **master sheet** oluşturmayı, motoru **duplicate sheet names** (yinelenen sayfa adlarına) izin verecek şekilde yapılandırmayı ve ardından **workbook as XLSX** (çalışma kitabını XLSX olarak) kaydetmeyi temiz C# koduyla çok kolay hâle getirir. Bu öğreticide tamamen çalıştırılabilir bir örnek üzerinden adım adım ilerleyecek, her satırın neden önemli olduğunu açıklayacak ve kendi projelerinizde doğrudan kullanabileceğiniz bir dizi ipucu sunacağız.

> **Neler Öğreneceksiniz**  
> * Aspose.Cells kullanarak **C# tarzı Excel çalışma kitabı oluşturma**.  
> * Her veri satırı için bir detay sayfası oluşturan smart‑marker ekleme.  
> * Kütüphanenin otomatik olarak sayısal bir sonek eklemesi için `DetailSheetNewName = DuplicateAllowed` ayarını yapma.  
> * Ek bir adım gerektirmeden diske **workbook as XLSX** (çalışma kitabını XLSX olarak) kaydetme.

Harici bir belgeye gerek yok—gereken her şey burada.

---

## Önkoşullar

| Gereksinim | Neden önemli |
|-------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.Cells 23.x+ bu çalışma zamanlarını hedefler. |
| Visual Studio 2022 (or any C# IDE) | Kolay proje oluşturma ve hata ayıklama için. |
| Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`) | Tüm smart‑marker sihrini sağlayan kütüphane. |
| Basic C# knowledge | Sözdizimini ek bir eğitim almadan anlayacaksınız. |

Eğer bunlardan herhangi birine sahip değilseniz, hemen ekleyin—yarım kalmış bir ortamda devam etmenin bir anlamı yok.

## Adım 1: Aspose.Cells ile master sheet oluşturma

İlk yaptığımız şey, bir `Workbook` nesnesi oluşturarak **C# tarzı Excel çalışma kitabı** oluşturmak. Bu nesne zaten bir varsayılan çalışma sayfası içerir; bunu “Master” olarak yeniden adlandıracağız ve tüm detay sayfaları için şablon olarak kullanacağız.

```csharp
using Aspose.Cells;

// Step 1: Initialise a new workbook – this automatically gives us one sheet
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet that comes with a fresh workbook
Worksheet masterSheet = workbook.Worksheets[0];

// Give it a meaningful name – this will be our master sheet
masterSheet.Name = "Master";
```

*Sayfayı neden yeniden adlandırıyoruz?*  
“Sheet1” gibi bir varsayılan ad, amacını yansıtmaz ve dosyayı daha sonra incelerken master sekmesinin hemen tanınmasını istersiniz. İsimlendirme ayrıca daha sonra eklediğiniz sayfaların çakışmasını önler.

## Adım 2: Detay sayfalarını oluşturacak smart‑marker'ı hazırlama

Smart‑marker'lar, Aspose.Cells'in çalışma zamanında veri ile değiştirdiği yer tutuculardır. Hücre **A1**'e `{{#detail:DataSheetName}}` koyarak motoru şu şekilde yönlendiririz: “Veri kaynağındaki her kayıt için, adı `DataSheetName` alanından gelen yeni bir sayfa oluştur.”

```csharp
// Step 2: Insert a smart‑marker into cell A1.
// The marker #detail tells Aspose.Cells to generate a new sheet per data row.
masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");
```

Marker'ı, çalışma sayfasına yapıştırılmış küçük bir talimat kartı gibi düşünün. İşlemci çalıştığında kartı okur, veri kaynağından uygun değeri alır ve ardından master sheet'i yeni bir sekmeye kopyalar.

## Adım 3: Veri kaynağını oluşturma – bilinçli olarak yinelenen sayfa adları

Gerçek hayatta bunu bir veritabanından çekebilirsiniz, ancak demo için anonim nesnelerden oluşan bellek içi bir dizi kullanacağız. Her iki öğenin de aynı temel adı `"Detail"` kullandığına dikkat edin; işte **duplicate sheet names** (yinelenen sayfa adlarına) izin vermenin kritik olduğu senaryo.

```csharp
// Step 3: Create a data source with two items that share the same base sheet name.
var dataSource = new[]
{
    new { DataSheetName = "Detail" },
    new { DataSheetName = "Detail" }
};
```

Eğer bunu özel bir seçenek olmadan denerseniz, Aspose.Cells ikinci yinelemede “Detail” adlı bir sayfa zaten var olduğu için bir istisna fırlatır. Bu yüzden bir sonraki adım önemlidir.

## Adım 4: Yinelenen sayfa adlarını etkinleştirme

Aspose.Cells `SmartMarkerOptions.DetailSheetNewName` özelliğini sunar. Bunu `DetailSheetNewName.DuplicateAllowed` olarak ayarlamak, motorun bir isim çakışması olduğunda otomatik olarak sayısal bir sonek (ör. “Detail_1”) eklemesini sağlar.

```csharp
// Step 4: Configure SmartMarker options to permit duplicate sheet names.
var smartMarkerOptions = new SmartMarkerOptions
{
    // This makes the library rename clashes to "Detail_1", "Detail_2", etc.
    DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
};
```

*Her satıra elle benzersiz bir ad vermek neden tercih edilmiyor?*  
Çünkü kaynak veri genellikle benzersizliği garanti etmez, özellikle kullanıcılar serbest metin girdiğinde. Kütüphanenin soneki otomatik eklemesine izin vermek, birçok hatayı ortadan kaldırır.

## Adım 5: Smart‑marker'ları işleme ve detay sayfalarını oluşturma

Şimdi `SmartMarkers.Process` metodunu çağırıyoruz, veri kaynağını ve az önce yapılandırdığımız seçenekleri geçiriyoruz. Metot her öğeyi dolaşır, master sheet'i kopyalar ve kopyayı `DataSheetName` alanına göre (gerekirse sonek ekleyerek) yeniden adlandırır.

```csharp
// Step 5: Run the smart‑marker processor – this creates the detail sheets.
masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);
```

Bu satır çalıştırıldıktan sonra çalışma kitabında üç sekme olacak:

1. **Master** – orijinal şablon.  
2. **Detail** – ilk oluşturulan sayfa (sonek gerekmez).  
3. **Detail_1** – ikinci oluşturulan sayfa (sonek otomatik eklenir).

Bunu Excel'de dosyayı açarak doğrulayabilirsiniz; iki detay sayfasını yan yana göreceksiniz.

## Adım 6: Çalışma kitabını XLSX dosyası olarak kaydetme

Son olarak, dosyayı diske kaydediyoruz. `.xlsx` uzantısı verdiğinizde `Save` metodu otomatik olarak XLSX formatını seçer.

```csharp
// Step 6: Persist the workbook – this is the moment we finally “save workbook as XLSX”.
string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
workbook.Save(outputPath);
```

**Pro ipucu:** Dosyayı doğrudan bir web yanıtına (ör. ASP.NET Core) akıtmanız gerekiyorsa, dosya yolunu kullanmak yerine `workbook.Save(stream, SaveFormat.Xlsx)` yöntemini tercih edin.

## Tam Çalışan Örnek

Aşağıda tam ve çalıştırılabilir program yer alıyor. Bir konsol uygulamasına kopyalayıp yapıştırın, F5'e basın ve oluşturulan dosyayı açarak sonucu görün.

```csharp
using System;
using Aspose.Cells;

namespace MasterSheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and rename the default sheet to "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // 2️⃣ Insert a smart‑marker that will generate a detail sheet per data row
            masterSheet.Cells["A1"].PutValue("{{#detail:DataSheetName}}");

            // 3️⃣ Prepare a data source where two rows share the same sheet name
            var dataSource = new[]
            {
                new { DataSheetName = "Detail" },
                new { DataSheetName = "Detail" }
            };

            // 4️⃣ Allow duplicate sheet names – the library will add "_1", "_2", …
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = DetailSheetNewName.DuplicateAllowed
            };

            // 5️⃣ Process the smart‑markers; this creates the detail sheets
            masterSheet.SmartMarkers.Process(dataSource, smartMarkerOptions);

            // 6️⃣ Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\DuplicateDetailSheets.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Beklenen sonuç:** `DuplicateDetailSheets.xlsx` dosyasını açın; üç çalışma sayfası göreceksiniz—`Master`, `Detail` ve `Detail_1`. Her detay sayfası, master'ın tam bir kopyasıdır ve daha sonra satır‑özel verilerle doldurmanız için hazırdır.

## Sık Sorulan Sorular & Kenar Durumlar

### Eğer iki'den fazla yinelenen sayfa gerekirse ne olur?

Problem yok. Aynı `DuplicateAllowed` ayarı, her satırın kendi sekmesine sahip olana kadar artan sayılar (`Detail_2`, `Detail_3`, …) eklemeye devam eder.

### Sonek formatını özelleştirebilir miyim?

Varsayılan olarak, Aspose.Cells bir alt çizgi ve sayısal bir indeks kullanır. Farklı bir desen (ör. “Detail‑A”, “Detail‑B”) isterseniz, `Process` çalıştıktan sonra çalışma kitabını `workbook.Worksheets` üzerinde döngüyle gezerek istediğiniz gibi yeniden adlandırmanız gerekir.

### Bu yöntem büyük veri setleri (yüzlerce satır) ile çalışır mı?

Evet, ancak bellek kullanımına dikkat edin. Oluşturulan her sayfa, master'ın tam bir kopyasıdır; bu yüzden çok sayıda satır dosya boyutunu hızla artırabilir. Eğer sayfa başına sadece birkaç satıra ihtiyacınız varsa, fazla hücreleri temizlemek için `SmartMarkerOptions.RemoveEmptyRows = true` kullanmayı düşünün.

### Oluşturulan dosya gerçekten bir XLSX dosyası mı?

Kesinlikle. `Save` metodu, Excel'in beklediği Open XML paketini yazar. Dosyayı LibreOffice veya Google Sheets ile herhangi bir dönüşüm yapmadan bile açabilirsiniz.

## Üretim‑Hazır Kod İçin İpuçları

| İpucu | Neden önemli |
|-----|----------------|
| **Dispose `Workbook

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}