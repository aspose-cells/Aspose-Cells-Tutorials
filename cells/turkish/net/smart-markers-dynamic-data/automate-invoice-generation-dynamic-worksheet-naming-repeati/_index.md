---
category: general
date: 2026-02-14
description: 'SmartMarker ile fatura oluşturmayı otomatikleştirin: çalışma sayfalarını
  nasıl tekrarlayacağınızı, dinamik olarak nasıl adlandıracağınızı öğrenin ve dakikalar
  içinde dinamik çalışma sayfası adlandırma konusunda uzmanlaşın.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: tr
og_description: SmartMarker ile fatura oluşturmayı otomatikleştirin. Bu kılavuz, çalışma
  sayfalarını nasıl tekrarlayacağınızı, dinamik olarak nasıl adlandıracağınızı ve
  dinamik çalışma sayfası adlandırma konusunda uzmanlaşacağınızı gösterir.
og_title: Fatura Oluşturmayı Otomatikleştir – Dinamik Çalışma Sayfası Adlandırma ve
  Tekrarlama
tags:
- C#
- SmartMarker
- Excel Automation
title: Fatura Oluşturmayı Otomatikleştir – C#'ta Dinamik Çalışma Sayfası Adlandırma
  ve Tekrarlama
url: /tr/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

-backtop-button >}}

We must keep them unchanged.

Check for any other markdown links: none.

Check for any other code blocks: placeholders.

Make sure to keep bold formatting.

Now produce final output with all translated content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fatura Oluşturmayı Otomatikleştirme – Dinamik Çalışma Sayfası Adlandırma ve Tekrarlama C#'ta

Hiç **fatura oluşturmayı otomatikleştirme**yi, her sipariş için sayfaları manuel olarak kopyalamadan nasıl yapabileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, her fatura için ayrı bir çalışma sayfasına ihtiyaç duyduğunda ve sayfa adının sipariş numarasını yansıtmasını istediğinde bir engelle karşılaşıyor. Bu öğreticide, SmartMarker’ın `SmartMarkerProcessor`ını kullanarak bu sorunu çözecek ve **çalışma sayfalarını dinamik olarak adlandırma** ile **her kayıt için çalışma sayfasını tekrarlama** konularını göstereceğiz. Sonunda, her faturanın kendi, güzel adlandırılmış sekmesinde bulunduğu bir çalışma kitabı üreten, çalıştırmaya hazır bir C# örneğine sahip olacaksınız.

Veri kaynağından siparişleri çekmekten `SmartMarkerOptions`ı dinamik çalışma sayfası adlandırması için yapılandırmaya kadar her adımı adım adım göstereceğiz. Harici belgelere ihtiyaç yok; ihtiyacınız olan her şey burada. C# hakkında temel bir bilgi ve Aspose.Cells kütüphanesine (veya herhangi bir SmartMarker‑uyumlu motor) bir referans yeterli olacaktır.

---

## Oluşturacağınız Şeyler

- Sipariş nesnelerinin bir koleksiyonunu alın.
- SmartMarker'ı her sipariş için **çalışma sayfasını tekrarlamak** için yapılandırın.
- `{OrderId}` yer tutucusunu kullanarak **dinamik çalışma sayfası adlandırması** uygulayın.
- Her sekmenin `Invoice_12345`, `Invoice_67890` vb. şekilde adlandırıldığı bir Excel dosyası oluşturun.
- Çıktıyı, çalışma kitabını açarak doğrulayın.

## Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET 5+ ile de derlenir).
- Aspose.Cells for .NET (veya SmartMarker'ı uygulayan herhangi bir kütüphane). NuGet üzerinden kurun:

```bash
dotnet add package Aspose.Cells
```

- Temel bir `Order` sınıfı (kendi DTO'nuzla değiştirebilirsiniz).

## Adım 1: Projeyi ve Modeli Kurun

İlk olarak, yeni bir konsol uygulaması oluşturun ve bir siparişi temsil eden veri modelini tanımlayın.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro ipucu:** Demo için modeli hafif tutun; daha sonra satır öğeleri, vergi detayları vb. ile her zaman zenginleştirebilirsiniz.

## Adım 2: Excel Şablonunu Hazırlayın

SmartMarker bir şablon çalışma kitabı üzerinde çalışır. `InvoiceTemplate.xlsx` adlı bir dosya oluşturun ve içinde `InvoiceTemplate` adında tek bir çalışma sayfası bulunsun. **A1** hücresine aşağıdaki gibi bir SmartMarker yer tutucusu yerleştirin:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Hücreleri istediğiniz gibi biçimlendirebilirsiniz—kalın başlıklar, para birimi formatı vb. Dosyayı projenin kök klasörüne kaydedin.

> **Neden şablon?** Düzeni koddan ayırır, tasarımcıların görünümü mantığı etkilemeden ayarlamasına izin verir.

## Adım 3: SmartMarker Seçeneklerini Yapılandırın – Tekrarlama ve Çalışma Sayfalarını Adlandırma

Şimdi SmartMarker'a şablon çalışma sayfasını her sipariş için *tekrarlamasını* ve her kopyaya sipariş kimliğini içeren bir ad vermesini söyleyeceğiz. Bu, **dinamik çalışma sayfası adlandırmasının** özüdür.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Nasıl Çalışır

- **`RepeatWorksheet = true`** motoru, `orders` koleksiyonundaki her öğe için kaynak sayfayı çoğaltmasını söyler. Bu, **çalışma sayfasını nasıl tekrarlarsınız** gereksinimini karşılar.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** bir şablon dizesidir; `{OrderId}` SmartMarker tarafından geçerli siparişin kimliğiyle değiştirilir. Bu, **çalışma sayfalarını nasıl adlandırırsınız** ve **dinamik çalışma sayfası adlandırması** sorusunun cevabıdır.
- İşlemci, her siparişin alanlarını (`{{OrderId}}`, `{{Customer}}` vb.) çoğaltılan sayfaya birleştirir ve tamamen doldurulmuş bir fatura üretir.

## Adım 4: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Konsol uygulamasını derleyip çalıştırın:

```bash
dotnet run
```

Konsolda başarı mesajını görmelisiniz. `GeneratedInvoices.xlsx` dosyasını açın ve üç sekme bulacaksınız:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Her sayfa, yer tutuculara sipariş verileri yerleştirilmiş şekilde içerir. Şablonda tasarladığınız düzen korunur ve **fatura oluşturmayı otomatikleştirme**'nin uçtan uca çalıştığını gösterir.

### Beklenen Ekran Görüntüsü (SEO için alt metin)

![dinamik olarak adlandırılmış üç çalışma sayfası gösteren fatura otomasyon örneği](/images/invoice-automation.png)

> *Görsel alt metni, SEO'yu karşılamak için birincil anahtar kelimeyi içerir.*

## Adım 5: Kenar Durumları ve Yaygın Varyasyonlar

### OrderId yasadışı karakterler içerirse ne olur?

Excel çalışma sayfası adları `\ / ? * [ ] :` karakterlerini içeremez. Kimlikleriniz bu karakterleri içerebilir ise, onları temizleyin:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

`Order` sınıfına hesaplanmış bir özellik ekleyin:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Orijinal şablon sayfasını korumak mı istiyorsunuz?

`smartMarkerOptions.RemoveTemplate = false;` olarak ayarlayın (varsayılan `true`). Bu, orijinal `InvoiceTemplate`'i referans olarak dokunulmaz bırakır.

### Faturaları müşteriye göre gruplamak mı istiyorsunuz?

**repeat gruplarını** iç içe kullanabilirsiniz. İlk önce müşteriye göre, ardından her müşteri çalışma sayfası içinde siparişlere göre tekrarlayın. Sözdizimi biraz daha karmaşık olur, ancak prensip aynı kalır—`RepeatWorksheet` kullanın ve hiyerarşiyi yansıtan bir adlandırma deseni uygulayın.

## Tam Çalışan Örnek (Tüm Kod Tek Bir Yerde)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Bunu `Program.cs` dosyasına kopyalayıp yapıştırın, yanına `InvoiceTemplate.xlsx` dosyasını koyun ve hazırsınız.

## Sıkça Sorulan Sorular

**S: Bu yaklaşım büyük veri setleri (binlerce fatura) ile çalışır mı?**  
C: Evet. SmartMarker verileri verimli bir şekilde akıtır, ancak bellek kullanımına dikkat edin. Sınırlarla karşılaşırsanız, işlemleri partiler halinde yapmayı ve her partiyi ayrı bir çalışma kitabına yazmayı düşünün.

**S: Her fatura için otomatik olarak bir logo ekleyebilir miyim?**  
C: Kesinlikle. Logoyu şablon sayfasına yerleştirin. Sayfa çoğaltıldığı için logo, ekstra kod olmadan her oluşturulan faturada görünür.

**S: Çalışma sayfalarını korumam gerekirse ne yapmalıyım?**  
C: İşlemden sonra `wb.Worksheets` üzerinde döngü kurup `ws.Protect(Password, ProtectionType.All)` metodunu çağırın.

## Sonuç

SmartMarker’ın çalışma sayfasını tekrarlama özelliği ve akıllı bir adlandırma deseni kullanarak **fatura oluşturmayı otomatikleştirdik**. Öğreticide **çalışma sayfalarını nasıl adlandırırsınız**, her sipariş için **çalışma sayfasını nasıl tekrarlarsınız** gösterildi ve **dinamik çalışma sayfası adlandırması** ile çalışma kitabınızın düzenli ve aranabilir kalması sağlandı.

Veri çekmekten, şablon oluşturmak, `SmartMarkerOptions` yapılandırmak ve kenar durumlarını ele almaya kadar, artık eksiksiz, çalıştırılabilir bir çözümünüz var. Sonraki adımda satır‑ögesi tabloları eklemeyi, koşullu biçimlendirme uygulamayı veya aynı verileri PDF'ye dışa aktararak tam otomatik bir faturalama hattı oluşturmayı deneyin.

Bir üst seviyeye geçmeye hazır mısınız? “Aspose.Cells ile toplu Excel dışa aktarımı”, “çalışma sayfalarının PDF dönüşümü” veya “C# üzerinden oluşturulan faturaları doğrudan e‑posta ile gönderme” gibi ilgili konuları keşfedin. Sınır yok—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}