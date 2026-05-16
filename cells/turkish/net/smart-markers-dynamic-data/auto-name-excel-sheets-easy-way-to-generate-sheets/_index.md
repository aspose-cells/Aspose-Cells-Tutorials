---
category: general
date: 2026-02-23
description: Excel sayfalarını otomatik olarak adlandırın ve SmartMarkers kullanarak
  sayfaları otomatik olarak oluşturmayı öğrenin. Dinamik çalışma kitapları için adım
  adım C# rehberi.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: tr
og_description: Excel sayfalarını anında otomatik adlandırın. C#'ta SmartMarkers ile
  sayfaları nasıl oluşturacağınızı öğrenin – eksiksiz, çalıştırılabilir örnek.
og_title: Excel Sayfalarını Otomatik Adlandırma – Hızlı C# Öğreticisi
tags:
- C#
- Excel
- Aspose.Cells
title: Excel Sayfalarını Otomatik İsimlendir – Sayfaları Oluşturmanın Kolay Yolu
url: /tr/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

– Tam C# Öğreticisi"

But keep "Auto Name Excel Sheets" maybe keep as is? The instruction: translate all text content naturally to Turkish, keep technical terms in English. "Auto Name Excel Sheets" is a phrase, but maybe keep as is? It's a feature name. Could translate to "Excel Sayfalarını Otomatik İsimlendirme". We'll translate.

Now go through each paragraph.

I'll produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Sayfalarını Otomatik İsimlendirme – Tam C# Öğreticisi

Hiç **excel sayfalarını otomatik isimlendirme** işlemini, her sekmeyi manuel olarak yeniden adlandıran bir döngü yazmadan yapmayı düşündünüz mü? Tek başınıza değilsiniz. Birçok raporlama projesinde çalışma sayfası sayısı çalışma zamanında artar ve isimlerin düzenli tutulması bir sıkıntı haline gelir. İyi haber? Aspose.Cells’in **SmartMarkers** özelliği sayesinde isimlendirmeyi kütüphaneye bırakabilir ve hatta **sayfaları nasıl oluşturacağınızı** anında öğrenebilirsiniz.

Bu rehberde gerçek bir senaryoyu adım adım inceleyeceğiz: bir çalışma kitabı oluşturma, SmartMarker seçeneklerini yapılandırarak detay sayfalarının otomatik olarak *Detail*, *Detail1*, *Detail2*, … şeklinde adlandırılmasını sağlama ve ardından sayfaların beklendiği gibi göründüğünü doğrulama. Sonunda, dinamik çalışma sayfası oluşturma ihtiyacı olan herhangi bir projeye uyarlayabileceğiniz, kopyala‑yapıştır hazır bir çözüm elde edeceksiniz.

---

## Gereksinimler

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

- **.NET 6+** (veya .NET Framework 4.6.2+). Kod, herhangi bir yeni çalışma zamanında çalışır.
- **Aspose.Cells for .NET** NuGet paketi – `Install-Package Aspose.Cells`.
- Temel bir C# projesi (Console App, WinForms veya ASP.NET – aynı kod her yerde çalışır).
- Visual Studio, VS Code veya tercih ettiğiniz IDE.

Ek Excel interop, COM yok; sadece saf yönetilen kod.

---

## Adım 1: SmartMarkers ile Excel Sayfalarını Otomatik İsimlendirme

İlk yapmanız gereken, Aspose.Cells’e otomatik oluşturulan detay sayfaları için hangi temel ismi istediğinizi söylemek. Bu, `SmartMarkerOptions` sınıfı üzerinden yapılır.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Neden önemli:** `DetailSheetNewName` ayarını yaparak isimlendirme mantığını kütüphaneye devredersiniz. Mevcut sayfa adlarını kontrol edip bir sayaç artıran bir `for` döngüsü yazmanıza gerek kalmaz – API bunu sizin için yapar ve veri kaynağınızda onlarca satır olsa bile benzersiz adlar garantiler.

---

## Adım 2: Veri Kaynağını Hazırlama

SmartMarkers, herhangi bir `IEnumerable` koleksiyonu, bir `DataTable` veya hatta düz bir nesne listesiyle çalışır. Bu demoda sipariş detaylarını temsil eden basit bir nesne listesi kullanacağız.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Neden önemli:** Veri kaynağı, kaç adet detay sayfası üretileceğini belirler. Koleksiyondaki her öğe, bir sonraki adımda ekleyeceğimiz SmartMarker şablonuna dayanarak yeni bir sayfa oluşturur.

---

## Adım 3: Ana Sayfaya SmartMarker Şablonu Ekleme

SmartMarker şablonu, yer tutucular içeren bir hücre (veya aralıktır). `Apply` metodu çalıştırıldığında, yer tutucular gerçek veriyle değiştirilir ve her satır için yeni bir sayfa oluşturulur.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Neden önemli:** `&=` sözdizimi, SmartMarkers’a “değer veri kaynağından alınsın” der. `Apply` çalıştığında, Aspose.Cells bu satırı `orders` içindeki her öğe için yeni bir sayfaya kopyalar ve sayfayı daha önce belirlediğimiz seçenekle otomatik olarak isimlendirir.

---

## Adım 4: SmartMarker Seçeneklerini Uygulama – Sayfalar Otomatik İsimlendirildiği Yer

Şimdi kütüphanenin ağır işi yaptığı an geliyor. `Apply` çağrısı şablonu okur, detay sayfalarını oluşturur ve `DetailSheetNewName` değerine göre isimlendirir.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Neden önemli:** `Apply` metodu sadece veriyi doldurmakla kalmaz, aynı zamanda sağladığınız adlandırma desenine de uyar. *AutoNamedSheets.xlsx* dosyasını açtığınızda şunları göreceksiniz:

- **Detail** – ilk siparişi içerir.
- **Detail1** – ikinci sipariş.
- **Detail2** – üçüncü sipariş.

Manuel yeniden adlandırma gerekmez.

---

## Adım 5: Sonucu Doğrulama – Sayfaları Doğru Şekilde Nasıl Oluşturursunuz

Programı çalıştırdıktan sonra oluşturulan dosyayı açın. Yukarıda açıklanan tam adlarla üç yeni çalışma sayfası görmelisiniz. Bu, **sayfaları otomatik oluşturmayı** başarıyla öğrendiğinizi kanıtlar.

> **İpucu:** Özel bir ek (ör. “_Report”) istiyorsanız, sadece `DetailSheetNewName = "Detail_Report"` olarak ayarlayın; kütüphane temel dizeye sayı ekleyecektir.

---

## Kenar Durumları ve Yaygın Sorular

### Temel ad zaten varsa ne olur?

Aspose.Cells mevcut sayfa adlarını kontrol eder ve benzersiz bir ad bulunana kadar artan bir sayı ekler. Yani çalışma kitabında zaten bir *Detail* sayfası varsa, bir sonraki oluşturulan sayfa *Detail1* olur.

### Oluşturulan sayfaların sırasını kontrol edebilir miyim?

Evet. Sıra, veri kaynağının dizilimine göre belirlenir. Belirli bir sıralama istiyorsanız, `Apply`'a geçmeden önce koleksiyonu sıralayın.

### Farklı bir çalışma kitabında sayfa oluşturmak mümkün mü?

Kesinlikle. İkinci bir `Workbook` örneği oluşturun, bir yer tutucu çalışma sayfası ekleyin ve `Apply` metodunu o sayfada çağırın. Aynı adlandırma mantığı geçerli olur.

### Büyük veri setleriyle bu nasıl çalışır?

SmartMarkers performans için optimize edilmiştir. Binlerce satırda bile kütüphane veriyi verimli bir şekilde akıtabilir. Tek yapmanız gereken son çalışma kitabının boyutu için yeterli belleğe sahip olduğunuzdan emin olmak.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda yeni bir console projesine yapıştırabileceğiniz tam program yer alıyor. Eksik bir parça yok – `using` yönergelerinden son `Save` çağrısına kadar her şey dahil.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Programı çalıştırın, ortaya çıkan *AutoNamedSheets.xlsx* dosyasını açın ve **excel sayfalarını otomatik isimlendirme** özelliğinin nasıl çalıştığını görün.

---

## Sık Sorulan Takip Soruları

- **Bunu mevcut bir şablon dosyasıyla kullanabilir miyim?**  
  Evet. `new Workbook("Template.xlsx")` ile çalışma kitabını yükleyin ve `master` değişkenini SmartMarker yer tutucularını içeren sayfaya yönlendirin.

- **Farklı sayfa türleri için farklı adlandırma kuralları gerekirse?**  
  Her biri kendi `DetailSheetNewName` değerine sahip birden fazla `SmartMarkerOptions` nesnesi oluşturun ve bunları farklı ana sayfalara uygulayın.

- **Şablon sayfasını (temel sayfayı) gizlemek mümkün mü?**  
  `Apply` işleminden sonra ana çalışma sayfasını basitçe silebilirsiniz: `workbook.Worksheets.RemoveAt(0);` – detay sayfaları etkilenmez.

---

## Sonuç

Artık Aspose.Cells SmartMarkers kullanarak **excel sayfalarını otomatik isimlendirme** yöntemini biliyorsunuz ve C# içinde **sayfaları nasıl oluşturacağınızı** dinamik olarak görmüş oldunuz. Temel fikir basit: `SmartMarkerOptions.DetailSheetNewName` ayarlayın, bir koleksiyon besleyin ve kütüphanenin geri kalanını halletmesine izin verin. Bu yaklaşım gereksiz döngüleri ortadan kaldırır, benzersiz adlar garantiler ve sorunsuz ölçeklenir.

Bir sonraki adıma hazır mısınız? Veri kaynağını bir `Data` ile değiştirerek deneyin.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}