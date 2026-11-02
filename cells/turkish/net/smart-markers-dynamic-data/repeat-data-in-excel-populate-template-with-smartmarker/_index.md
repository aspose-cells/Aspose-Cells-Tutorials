---
category: general
date: 2026-02-21
description: SmartMarker kullanarak Excel'de verileri hızlıca tekrarlayın—Excel şablonunu
  nasıl dolduracağınızı ve satırları zahmetsizce nasıl tekrarlayacağınızı öğrenin.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: tr
og_description: SmartMarker kullanarak Excel'de verileri tekrarlayın. Excel şablonunu
  doldurmayı, satırları tekrarlamayı ve elektronik tablolarınızı otomatikleştirmeyi
  öğrenin.
og_title: Excel'de verileri tekrarlama – SmartMarker ile şablonu doldurun
tags:
- excel
- csharp
- smartmarker
- automation
title: Excel'de verileri tekrarlama – SmartMarker ile şablonu doldur
url: /tr/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de veri tekrarı – SmartMarker ile şablonu doldurma

Hiç **Excel'de veri tekrarlama** ihtiyacı duydunuz mu ama manuel kopyala‑yapıştırdan nasıl kaçınacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok raporlama senaryosunda, otomatik olarak satırlara genişlemesi gereken bir öğe listesi vardır ve bunu elle yapmak hata kaynağıdır.

İşte asıl nokta—**GemBox.Spreadsheet** kütüphanesindeki `SmartMarkerProcessor`ı kullanarak **tek bir C# satırıyla bir Excel şablonunu doldurabilir** ve koleksiyonunuzdaki her öğe için satırların otomatik olarak tekrarlanmasını sağlayabilirsiniz. Bu rehberde tam adımları, eksiksiz kodu ve her parçanın neden önemli olduğunu gösterecek, böylece tereddüt etmeden Excel'de satırları tekrarlayabileceksiniz.

## Öğrenecekleriniz

* Tekrarlama işlemini yönlendiren veri yapısının nasıl tanımlanacağını.  
* Gizli bir şablon sayfası içeren bir çalışma kitabına nasıl `SmartMarkerProcessor` bağlanacağını.  
* `${Repeat:Item}` işaretçisinin nasıl otomatik olarak birden fazla satıra genişlediğini.  
* Boş koleksiyonlar veya özel biçimlendirme gibi kenar durumlarını nasıl yöneteceğinizi.  

Bu öğreticinin sonunda **veriden excel doldurma** işlemini ölçeklenebilir, bakımı kolay ve herhangi bir .NET projesiyle çalışan bir şekilde yapabileceksiniz.

---

## Önkoşullar

* .NET 6.0 veya üzeri (kod modern C# özelliklerini kullanıyor).  
* **GemBox.Spreadsheet** NuGet paketi (ücretsiz sürüm 150 satıra kadar çalışır).  
* `Template.xlsx` adlı gizli bir sayfaya (`HiddenTemplate`) sahip temel bir Excel şablon dosyası.  
* C# nesneleri ve LINQ konusunda temel bilgi faydalı ancak zorunlu değil.

---

## Adım 1 – Tekrarlama veri yapısını tanımlama

İlk olarak, SmartMarker motorunun üzerinde dönebileceği bir veri kaynağına ihtiyacınız var. Çoğu gerçek dünya uygulamasında bu veri bir veritabanı, API veya CSV dosyasından gelir. Açıklık olması açısından, tek bir `Item` özelliği içeren ve dizi (array) tutan anonim bir tip kullanacağız.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Neden önemli:** Excel şablonundaki `${Repeat:Item}` işaretçisi `Item` adlı bir özelliği arar. Özelliğin adını değiştirirseniz, işaretçiyi de buna göre güncelleyin. Bu sıkı bağ, şablonun kodunuzla senkronize kalmasını sağlar ve **excel şablonunu doldurma** işlemini sütun adlarını tahmin etmeden yapmanızı kolaylaştırır.

### Yaygın varyasyonlar

* **Karmaşık nesneler:** Basit bir dizi yerine nesne listesi (`new[] { new { Name = "A", Qty = 10 } }`) sağlayabilirsiniz. İşaretçi satırları tekrar eder ve sayfada `${Item.Name}` ve `${Item.Qty}` gibi referanslar kullanabilirsiniz.  
* **Boş koleksiyonlar:** `Item` boşsa, SmartMarker tekrarlama bloğunu basitçe kaldırır ve şablonu olduğu gibi bırakır—opsiyonel bölümler için harika.

---

## Adım 2 – Gizli şablon sayfası için SmartMarkerProcessor oluşturma

Sonra, çalışma kitabınızı yükleyin ve bir `SmartMarkerProcessor` örneği oluşturun. Gizli şablon sayfasını içeren çalışma kitabına işaret edin; SmartMarker bu sayfayı görünür bir sayfaya kopyalar ve tekrarlama işaretçilerini genişletir.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro ipucu:** Aynı dosyada birden fazla şablon varsa, `processor.Process` çağrısında kaynak sayfa adını belirtebilirsiniz. Bu, raporun farklı bölümleri için **excel'de satırları tekrarlama** ihtiyacını karşılamada yardımcı olur.

### Kenar durumları yönetimi

* **Şablon sayfası eksik:** Yüklemeyi try/catch içinde sarın ve net bir hata mesajı kaydedin—dosya yolu yanlış olduğunda sessiz hataları önler.  
* **Büyük veri setleri:** Binlerce satır için, tüm veriyi bellekte tutmak yerine çıktıyı bir dosyaya (`processor.Save`) akıtmayı düşünün.

---

## Adım 3 – Veriyi uygulama ve `${Repeat:Item}` işaretçisini genişletme

Şimdi satırları gerçekten tekrarlayan sihirli satır geliyor. Adım 1'de oluşturduğunuz nesneyi `processor.Process`'e geçirin. SmartMarker her `${Repeat:Item}` işaretçisini bulur, satırı her öğe için çoğaltır ve yer tutucuları gerçek değerlerle değiştirir.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Görmeniz gerekenler

`Result.xlsx` dosyasını açtığınızda, gizli şablon sayfası yeni bir görünür sayfaya (varsayılan adı `Sheet1`) kopyalanmış olur. `${Repeat:Item}` içeren satır üç kez görünür ve hücrelerde sırasıyla **A**, **B** ve **C** gösterilir.

| Öğe |
|------|
| A    |
| B    |
| C    |

Daha fazla sütun eklediyseniz, örneğin `${Item.Price}`, bu değerler veri kaynağından otomatik olarak doldurulur.

---

## SmartMarker olmadan Excel'de satırları tekrarlama (hızlı karşılaştırma)

| Yaklaşım                | Kod Karmaşıklığı | Bakım | Performans |
|-------------------------|------------------|-------|------------|
| Manuel kopyala‑yapıştır | Yüksek           | Düşük | Kötü       |
| VBA makro               | Orta             | Orta  | İyi        |
| **SmartMarkerProcessor**| Düşük            | Yüksek| Mükemmel   |

Gördüğünüz gibi, **excel'de veri tekrarlama** için SmartMarker kullanmak şablon tasarımı ile iş mantığı arasındaki en temiz ayrımı sağlar. Ayrıca dil bağımsızdır—Java, Python ve JavaScript kütüphanelerinde benzer kavramlar bulunur.

---

## İleri ipuçları ve yaygın tuzaklar

### 1. Tekrarlanan satırların biçimlendirilmesi

SmartMarker tüm satırı—hücre stilleri, kenarlıklar ve koşullu biçimlendirme dahil—kopyalar. İlk veya son satır için farklı bir stil gerekiyorsa, `${If:Item.IsFirst}` gibi ekstra işaretçiler ekleyin ve Excel içinde koşullu formüller kullanın.

### 2. Büyük veri setleriyle çalışmak

10 000'den fazla satırla çalışırken, işlem öncesinde Excel'in otomatik hesaplamasını devre dışı bırakın:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Kaydetme işleminden sonra tekrar etkinleştirerek performansı yüksek tutun.

### 3. Gerçek bir veritabanından Excel doldurma

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Ardından şablonda `${Repeat:Order}` kullanarak her siparişi listeleyin. Bu desen, Entity Framework'ten **veriden excel doldurma** işleminin ne kadar kolay olduğunu gösterir.

### 4. Birden fazla tekrar bloğu kullanma

Aynı sayfada veya farklı sayfalarda birden fazla `${Repeat:...}` işaretçisi bulundurabilirsiniz. SmartMarker bunları sırasıyla işler, bu yüzden bir bloğun çıktısı diğerine bağlıysa sıralama önem kazanır.

---

## Tam çalıştırılabilir örnek

Aşağıda, Visual Studio'ya yapıştırıp hemen çalıştırabileceğiniz, tüm üç adımı ve dosya kaydetmeyi gösteren bağımsız bir konsol uygulaması bulunuyor.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Beklenen çıktı:** `Result.xlsx` dosyasında `${Repeat:Item}` satırı üç kez görünür ve A, B, C değerlerini gösterir. Manuel ayarlama gerekmez.

---

## Sonuç

Artık **excel'de veri tekrarlama** işlemini SmartMarkerProcessor sayesinde verimli bir şekilde yapmayı biliyorsunuz. Basit bir veri nesnesi tanımlayarak, bir şablon çalışma kitabı yükleyerek ve `Process` metodunu çağırarak **excel şablonunu doldurabilir**, **excel'de satırları tekrarlayabilir** ve genel olarak **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}