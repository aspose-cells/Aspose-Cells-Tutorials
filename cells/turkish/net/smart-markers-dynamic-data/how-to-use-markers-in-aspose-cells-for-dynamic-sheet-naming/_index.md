---
category: general
date: 2026-05-23
description: Aspose.Cells ile işaretçileri kullanarak dinamik sayfa adlandırma Excel
  otomasyonu nasıl yapılır. Akıllı işaretçileri, JSON veri bağlamayı ve dakikalar
  içinde sayfa oluşturmayı öğrenin.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: tr
og_description: Aspose.Cells'te işaretçileri kullanarak dinamik sayfa adlandırmalı
  Excel dosyaları oluşturma. Tam adım adım rehber ve eksiksiz C# örneği.
og_title: İşaretçileri Nasıl Kullanılır – Aspose.Cells ile Excel'de Dinamik Sayfa
  Adlandırma
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel'de Dinamik Sayfa Adlandırma İçin Aspose.Cells'te İşaretçileri Nasıl Kullanılır
url: /tr/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells'ta Dinamik Sayfa Adlandırma için İşaretçileri Nasıl Kullanılır

Hiç **işaretçileri nasıl kullanacağınızı** merak ettiniz mi, sabit bir Excel şablonunu tam teşekküllü bir master‑detail çalışma kitabına dönüştürmek için? Tek başınıza değilsiniz. Birçok geliştirici, özellikle sayfa adlarının JSON veya bir veritabanından gelen veri değerlerini yansıtması gerektiğinde *dynamic sheet naming excel* yeteneklerine ihtiyaç duyduklarında bir duvara çarpar.

Bu öğreticide, **işaretçileri nasıl kullanacağınızı** gösteren eksiksiz, çalıştırmaya hazır bir C# örneği üzerinden adım adım ilerleyeceğiz; **Aspose.Cells** akıllı işaretçileri, JSON verisini bağlayacak ve işlemcinin adları anlık olarak değişen sayfalar oluşturmasını sağlayacak. Gereksiz ayrıntı yok, sadece Visual Studio'ya yapıştırıp anında sonuçları görebileceğiniz tam kod.

## Öğrenecekleriniz

- **smart markers** kavramı ve neden master‑detail senaryoları için mükemmel oldukları.  
- Bir çalışma kitabına işaretçi etiketlerini gömerek daha sonra gerçek sayfa adlarıyla değiştirilmesini nasıl sağlayacağınızı.  
- `DetailSheetNewName` seçeneğini kullanarak **dynamic sheet naming excel** ayarlama.  
- `SmartMarkerProcessor`'ı JSON verisi üzerinde çalıştırarak birden fazla sayfa otomatik olarak oluşturma.  
- Çıktıyı doğrulama ve yaygın hatalardan kaçınmak için birkaç kullanışlı ipucu.  

> **Önkoşullar** – Güncel bir .NET çalışma zamanı (≥ .NET 6 yeterli), Aspose.Cells for .NET kütüphanesi (Aspose'tan ücretsiz deneme alabilirsiniz) ve C# hakkında temel bir aşinalık gerekir.  

---

![Aspose.Cells'ta işaretçileri kullanma örneği](example.png "Aspose.Cells'ta işaretçileri kullanma örneği")

## İşaretçileri Kullanarak Dinamik Sayfa Adlandırma Oluşturma (Adım 1)

İlk olarak ihtiyacımız olan, şablon olarak kullanılacak boş bir çalışma kitabıdır. Gerçek bir projede muhtemelen zaten düzen, biçimlendirme ve yer tutucu hücreler içeren mevcut bir `.xlsx` dosyasından başlardınız. Açıklık olması için her şeyi programlı olarak oluşturacağız.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Neden önemli*: `Worksheet` nesnesi, **smart marker** etiketlerimizi bırakacağımız yerdir. Etiketleri, işlemcinin daha sonra JSON'dan gerçek değerlerle değiştireceği küçük yer tutucular olarak düşünün.

## Akıllı İşaretçi Etiketlerini Ekleme (Adım 2)

Şimdi işaretçi etiketlerini doğrudan hücrelere yerleştiriyoruz. `${...}` sözdizimi Aspose.Cells'e “bu bir işaretçidir” der. Örneğimizde iki işaretçiye ihtiyacımız var: biri master sayfa adı için, diğeri detay sayfa adı için.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro ipucu** – İşaretçi adlarını kısa ve anlamlı tutun; JSON yükünüzde kullanacağınız anahtarlar haline gelirler.

## JSON Verisini Hazırlama (Adım 3)

İşlemci, JSON, bir `DataSet` veya hatta düz bir nesne olarak temsil edilebilen herhangi bir veri kaynağıyla çalışır. İşte bir master‑detail koleksiyonu içeren minimal bir JSON dizesi. Her siparişin hem `MasterSheetName` hem de `DetailSheetName` taşıdığını fark edin.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Neden JSON?* Hafiftir, insan tarafından okunabilir ve web API'leriyle harika çalışır. Bu veriyi bir SQL sorgusundan çekip `Newtonsoft.Json` ile serileştirmeniz de aynı derecede kolaydır.

## SmartMarkerProcessor'ı Başlatma (Adım 4)

`SmartMarkerProcessor`, çalışma kitabını tarayan, işaretçileri bulan ve veri bağlamasını gerçekleştiren motorudur. Örneğini oluşturmak tek satırlık bir işlemdir.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Dinamik Sayfa Adlandırmayı Tanımlama (Adım 5)

İşte **dynamic sheet naming excel**'in gerçek anlamda parladığı yer. `DetailSheetNewName` ayarlayarak işlemciye her sipariş için yeni bir detay sayfası oluşturmasını ve adını `OrderId`'ye göre belirlemesini söylüyoruz. `${OrderId}` yer tutucusu, işleme sırasında geçerli kayıttan çözülür.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Dikkat** – `${}` sözdizimini eklemeyi unutursanız, sayfa gerçekten “Detail_${OrderId}” olarak adlandırılır; “Detail_1”, “Detail_2” gibi adlar yerine.

## JSON'u Uygula ve Sayfaları Oluştur (Adım 6)

Şimdi işlemciye ağır işi bırakalım. JSON'u okuyacak, işaretçileri değiştirecek ve gerektiğinde yeni çalışma sayfaları oluşturacak.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Arkada Ne Oluyor?

1. İşlemci `Orders` dizisini okur.  
2. Her sipariş için bir **master sheet** (`${Orders.MasterSheetName}` kullanarak) ve bir **detail sheet** (`DetailSheetNewName` kalıbını kullanarak) oluşturur.  
3. Hücre değerleri ilgili JSON alanlarıyla değiştirilir, böylece master sayfanın ilk hücresi “Master_1”, “Master_2” vb. içerir.  

## Sonucu Kaydet ve Doğrula (İsteğe Bağlı)

Son olarak, çalışma kitabını diske yazın. Dosyayı Excel'de açın ve iki master sayfa (`Master_1`, `Master_2`) ve iki dinamik olarak adlandırılmış detay sayfa (`Detail_1`, `Detail_2`) görmelisiniz.  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Beklenen çıktı** – `output.xlsx` dosyasını açtıktan sonra şunları göreceksiniz:

- Sayfa **Master_1** hücre A1 = “Master_1”.  
- Sayfa **Detail_1** hücre A1 = “Detail_1”.  
- Sayfa **Master_2** hücre A1 = “Master_2”.  
- Sayfa **Detail_2** hücre A1 = “Detail_2”.  

Bu, **işaretçileri nasıl kullanacağınız**ın **dynamic sheet naming excel**'i **Aspose.Cells smart markers** ile başarmak için tam döngüsüdür.

---

## Yaygın Sorular ve Kenar Durumları

### Hiyerarşi iki seviyeden fazla olursa ne olur?

Yeni oluşturulan detay sayfalar içinde işaretçileri iç içe yerleştirebilirsiniz. İşleme başlamadan önce şablon sayfaya ek `${...}` etiketleri ekleyin. İşlemci her seviyeyi otomatik olarak kademeli olarak işler.

### JSON yerine DataTable kullanabilir miyim?

Kesinlikle. `SmartMarkerProcessor`'ın `DataSet`, `DataTable` ve hatta özel nesneler için aşırı yüklemeleri vardır. Tek değişiklik `ApplyJson` çağrısıdır – bunun yerine `ApplyDataSet(myDataSet)` kullanırsınız.

### Sayfa oluşturma sırasını nasıl kontrol ederim?

Sıra, kaynak koleksiyonun dizilimini izler. Özel bir sıralamaya ihtiyacınız varsa, JSON dizisini (veya DataTable'ı) işlemciye göndermeden önce sıralayın.

### İşlemden sonra şablon sayfasını gizlemenin bir yolu var mı?

Evet. `ApplyJson`'u çağırmadan önce `sm.Options.RemoveTemplateSheets = true;` olarak ayarlayın. Orijinal sayfa (indeks 0) final çalışma kitabından kaldırılacaktır.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, yeni bir C# konsol projesine kopyalayıp yapıştırabileceğiniz eksiksiz program yer alıyor. `Aspose.Cells` NuGet paketine referans verdiğinizden emin olun.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Programı çalıştırın, `output.xlsx` dosyasını açın ve daha önce açıklanan dinamik sayfaları tam olarak gördüğünüzü göreceksiniz.

---

## Sonuç

Aspose.Cells'ta **işaretçileri nasıl kullanacağınızı** ele aldık ve basit bir çalışma kitabını **dynamic sheet naming excel** ile bir master‑detail çözümüne dönüştürdük. Önemli çıkarımlar şunlardır:

1. Verinin görünmesini istediğiniz yere `${...}` akıllı işaretçileri yerleştirin.  
2. JSON'u (veya desteklenen herhangi bir veri kaynağını) `SmartMarkerProcessor`'a besleyin.  
3. `DetailSheetNewName`'i kullanarak işlemcinin yeni sayfaları anlık olarak adlandırmasını sağlayın.  

Buradan daha gelişmiş senaryoları keşfedebilirsiniz—tablolar eklemek, hücreleri biçimlendirmek ya da hatta grafik eklemek—tüm bunlar **Aspose.Cells** tarafından yönlendirilir.

## İlgili Öğreticiler

- [Dinamik Excel Raporlaması için Aspose.Cells Smart Markers'ı C#'ta Nasıl Uygularsınız](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Aspose.Cells .NET Smart Markers Kullanarak Dinamik Excel Raporları Oluşturma](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose.Cells .NET'de Uzmanlaşma: Dinamik Excel Raporları için Smart Markers ve Özel Etiketler Uygulama](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}