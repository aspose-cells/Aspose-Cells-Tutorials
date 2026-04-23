---
category: general
date: 2026-02-09
description: C#'da SmartMarker ile sayfaları nasıl adlandırılır – sadece birkaç satır
  kodla birden fazla sayfa oluşturmayı ve sayfa adlandırmayı otomatikleştirmeyi öğrenin.
draft: false
keywords:
- how to name sheets
- generate multiple sheets
- automate sheet naming
- SmartMarker sheet naming
- workbook automation
language: tr
og_description: C#'ta SmartMarker seçeneklerini kullanarak sayfaları nasıl adlandırılır.
  Bu rehber, birden fazla sayfa oluşturmayı ve sayfa adlandırmayı zahmetsizce otomatikleştirmeyi
  gösterir.
og_title: Sayfaları Otomatik Olarak Nasıl Adlandırılır – Hızlı C# Rehberi
tags:
- C#
- Aspose.Cells
- Excel automation
title: Sayfaları Otomatik Olarak Nasıl Adlandırılır – C#'ta Çoklu Sayfa Oluşturma
url: /tr/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sayfaları Otomatik Olarak Adlandırma – C#'ta Birden Çok Sayfa Oluşturma

Her seferinde “Rename” (Yeniden Adlandır) düğmesine manuel olarak tıklamadan bir Excel çalışma kitabında **sayfaları nasıl adlandıracağınızı** hiç merak ettiniz mi? Yalnız değilsiniz. Birçok raporlama senaryosunda, sistematik adlara ihtiyaç duyan onlarca detay sayfası elde edersiniz ve bunları elle yapmak bir kabus olur.  

İyi haber şu ki, birkaç satır C# kodu ile **birden çok sayfa oluşturabilir** ve **sayfa adlandırmayı otomatikleştirebilirsiniz**, böylece her yeni detay sayfası öngörülebilir bir desen izler. Bu öğreticide tam çözümü adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve size çalıştırmaya hazır bir kod örneği sunacağız.

## Bu Kılavuzda Neler Kapsanıyor

* SmartMarkers içeren bir çalışma kitabı ayarlama.
* `SmartMarkerOptions` yapılandırarak oluşturulan sayfaların temel adını kontrol etme.
* `ProcessSmartMarkers` çalıştırarak kütüphanenin `Detail`, `Detail_1`, `Detail_2`, … otomatik olarak oluşturmasını sağlama.
* Mevcut sayfa adları veya özel adlandırma kuralları gibi uç durumları ele alma ipuçları.
* Visual Studio'ya yapıştırıp sonucu anında görebileceğiniz tam, çalıştırılabilir bir örnek.

Aspose.Cells ile ilgili önceden bir deneyime ihtiyacınız yok—sadece temel bir C# kurulumu ve tercih ettiğiniz bir IDE yeterli.

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 or later | Modern dil özellikleri ve kütüphane uyumluluğu |
| Aspose.Cells for .NET (NuGet package) | `SmartMarker` işleme ve sayfa oluşturmayı sağlar |
| A blank console project (or any .NET app) | Kodu çalıştırmak için bir yer sağlar |

Kütüphaneyi şu şekilde kurun:

```bash
dotnet add package Aspose.Cells
```

Temel konuları ele aldığımıza göre, gerçek uygulamaya dalalım.

## Adım 1: SmartMarkers ile Bir Çalışma Kitabı Oluşturma

İlk olarak içinde bir SmartMarker yer tutucusu bulunan bir çalışma kitabına ihtiyacımız var. SmartMarker'ı, motorun veriyi nereye enjekte edeceğini ve bizim durumumuzda yeni bir sayfa ne zaman oluşturulacağını belirten bir şablon etiketi olarak düşünün.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣  Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // 2️⃣  Insert a SmartMarker that will trigger sheet creation
        // The marker {{detail}} tells Aspose.Cells to repeat the row for each item in the "detail" collection.
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // 3️⃣  Prepare sample data for the SmartMarker
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };
```

> **Pro tip:** Şablon sayfasını hafif tutun. Yalnızca çoğaltma gerektiren satırlar SmartMarkers içermeli; diğer her şey statik kalır.

## Adım 2: SmartMarker Seçeneklerini Yapılandırma – Sayfa Adlandırmanın Çekirdeği

Şimdi sihir devreye giriyor. `DetailSheetNewName` ayarlayarak motorun her oluşturulan sayfa için hangi temel adı kullanacağını belirtiyoruz. Kütüphane, temel ad zaten mevcut olduğunda “_1”, “_2” vb. ekleyecek.

```csharp
        // 4️⃣  Define naming options – this is where we answer “how to name sheets”
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // Primary keyword appears here: how to name sheets
            DetailSheetNewName = "Detail"   // Base name for all generated sheets
        };
```

Farklı bir adlandırma kuralına (ör. “Report_2023”) ihtiyacınız olursa, sadece dizeyi değiştirin. Motor çakışmaları otomatik olarak yönetir; bu yüzden bu yaklaşım ek kod olmadan **sayfa adlandırmayı otomatikleştirir**.

## Adım 3: SmartMarkers İşleme ve Sayfaları Oluşturma

Çalışma kitabı, veri ve seçenekler hazır olduğunda, tek bir metod çağrısı işi halleder.

```csharp
        // 5️⃣  Run the SmartMarker processor – this will create Detail, Detail_1, Detail_2…
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // 6️⃣  Save the result so you can open it in Excel
        wb.Save("GeneratedSheets.xlsx");

        // 7️⃣  Let the user know we’re done
        System.Console.WriteLine("Workbook created – check GeneratedSheets.xlsx");
    }
}
```

### Beklenen Sonuç

*GeneratedSheets.xlsx* dosyasını açtığınızda şunları göreceksiniz:

| Sayfa Adı | İçerik |
|------------|---------|
| Template   | Orijinal işaretçi düzeni (referans için tutulur) |
| Detail     | İlk satır seti (Apple, Banana, Cherry) |
| Detail_1   | İkinci kopya – aynı veri (birden çok koleksiyonunuz olduğunda faydalı) |
| Detail_2   | …ve böyle devam eder, kaç farklı SmartMarker grubunuz olduğuna bağlı olarak |

Adlandırma deseni (`Detail`, `Detail_1`, `Detail_2`) programatik olarak **sayfaları nasıl adlandıracağınızı** gösterirken aynı zamanda gerektiğinde **birden çok sayfa oluşturmayı** da gösterir.

## Kenar Durumları ve Varyasyonlar

### 1. Mevcut Sayfa Adları

Çalışma kitabınız zaten “Detail” adlı bir sayfa içeriyorsa, motor “Detail_1” ile başlayacaktır. Bu, yanlışlıkla üzerine yazılmayı önler.

### 2. Özel Artış Biçimleri

Sayısal ekler yerine “Detail‑A”, “Detail‑B” istiyor musunuz? `ProcessSmartMarkers` sonrası adları post‑process edebilirsiniz:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet sh = wb.Worksheets[i];
    if (sh.Name.StartsWith("Detail_"))
    {
        string suffix = ((char)('A' + i - 1)).ToString(); // A, B, C…
        sh.Name = $"Detail-{suffix}";
    }
}
```

### 3. Birden Çok SmartMarker Grubu

Çalışma kitabınız birden fazla SmartMarker grubu (ör. `{{invoice}}` ve `{{detail}}`) içeriyorsa, her grup aynı `DetailSheetNewName` temelinde kendi sayfa setini oluşturur. Her gruba ayrı bir önek vermek için ayrı `SmartMarkerOptions` örnekleri oluşturun ve her koleksiyon için `ProcessSmartMarkers` çağırın.

## Alandan Pratik İpuçları

* **Pro tip:** `WorkbookSettings` içinde `AllowDuplicateNames` özelliğini kapatın; böylece kütüphane sayfaları sessizce yeniden adlandırmak yerine bir istisna fırlatır. Bu, adlandırma mantığı hatalarını erken yakalamaya yardımcı olur.
* **Dikkat edin:** Çok uzun temel adlar. Excel sayfa adlarını 31 karakterle sınırlar; kütüphane otomatik olarak kırpar, ancak yine de belirsiz adlarla karşılaşabilirsiniz.
* **Performans notu:** Yüzlerce sayfa oluşturmak bellek tüketebilir. Uzun ömürlü bir hizmet içinde çalışıyorsanız, işiniz bittiğinde çalışma kitabını (`wb.Dispose()`) hemen serbest bırakın.

## Görsel Genel Bakış

![sayfaları nasıl adlandırma diyagramı](image.png "SmartMarker şablonundan oluşturulan sayfalara akışı gösteren diyagram – sayfaları nasıl adlandırma")

*Alt metin, SEO'yu karşılamak için ana anahtar kelimeyi içerir.*

## Tam Kaynak Kodu (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and template sheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Template";

        // SmartMarker layout
        ws.Cells["A1"].PutValue("{{detail}}");
        ws.Cells["B1"].PutValue("Item Name");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["A2"].PutValue("&=detail.Name");
        ws.Cells["B2"].PutValue("&=detail.Quantity");

        // Sample data
        var data = new
        {
            detail = new[]
            {
                new { Name = "Apple",  Quantity = 10 },
                new { Name = "Banana", Quantity = 20 },
                new { Name = "Cherry", Quantity = 30 }
            }
        };

        // Configure naming – this answers how to name sheets
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // Process markers → generates Detail, Detail_1, Detail_2 …
        wb.ProcessSmartMarkers(data, smartMarkerOptions);

        // Save and finish
        wb.Save("GeneratedSheets.xlsx");
        System.Console.WriteLine("Workbook created – open GeneratedSheets.xlsx to see the result.");
    }
}
```

Programı çalıştırın, oluşturulan dosyayı açın ve sayfaların tanımladığımız desene göre otomatik olarak adlandırıldığını göreceksiniz.

## Sonuç

Artık bir C# çalışma kitabında **sayfaları nasıl adlandıracağınızı**, SmartMarker ile **birden çok sayfa nasıl oluşturacağınızı** ve **sayfa adlandırmayı otomatikleştirerek** artık hiçbir şeyi manuel olarak yeniden adlandırmanız gerekmeyeceğini biliyorsunuz. Bu yaklaşım birkaç detay sayfasından yüzlerceye ölçeklenebilir ve aynı desen, `ProcessSmartMarkers` içine beslediğiniz herhangi bir koleksiyon için çalışır.

Sıradaki adım ne? Veri kaynağını bir veritabanı sorgusuyla değiştirin, özel ek biçimleriyle deney yapın veya tam bir raporlama motoru için birden çok SmartMarker grubunu zincirleyin. Kütüphane tekrarlayan adlandırma işini üstlendiğinde sınır yoktur.

Bu kılavuzu faydalı bulduysanız, GitHub'da yıldız verin, ekip arkadaşlarınızla paylaşın veya kendi adlandırma ipuçlarınızı aşağıya yorum olarak bırakın. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}