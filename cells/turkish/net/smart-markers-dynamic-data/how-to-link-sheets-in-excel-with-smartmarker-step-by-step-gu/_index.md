---
category: general
date: 2026-06-08
description: SmartMarkerProcessor kullanarak Excel'de master‑detail raporları için
  sayfaları nasıl bağlayacağınızı öğrenin. Master sayfasını doldurun ve master‑detail
  Excel raporunu zahmetsizce oluşturun.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: tr
og_description: SmartMarkerProcessor kullanarak Excel’de sayfaları nasıl bağlayacağınızı
  öğrenin. Ana sayfayı doldurmayı ve dakikalar içinde bir ana‑detay raporu oluşturmayı
  keşfedin.
og_title: SmartMarker ile Excel'de Sayfaları Bağlama – Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: SmartMarker ile Excel'de Sayfaları Bağlama – Adım Adım Kılavuz
url: /tr/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de SmartMarker ile Sayfaları Bağlama – Adım Adım Kılavuz

Hiç **sayfaları nasıl bağlayacağınızı** Excel'de manuel olarak satır kopyalamadan ya da sonsuz VBA döngüleri yazmadan merak ettiniz mi? Tek başınıza değilsiniz. Çoğu geliştirici, veri değiştikçe senkronize kalan temiz bir master‑detail raporuna ihtiyaç duyduğunda bir duvara çarpar. İyi haber? SmartMarkerProcessor, işi sizin için halleder ve birkaç C# satırını tam teşekküllü bir master‑detail çalışma kitabına dönüştürür.

Bu öğreticide **master sayfasını doldurma**, detay sayfasını ayarlama ve sonunda otomatik olarak güncellenen **master‑detail raporu oluşturma** adımlarını adım adım göstereceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz yeniden kullanılabilir bir desen elde edeceksiniz.

> **Önkoşul notu:** GrapeCity Documents for Excel (GcExcel) 2024 veya daha yeni bir sürüm, bir .NET geliştirme ortamı (Visual Studio 2022 harika çalışır) ve temel C# bilgisine ihtiyacınız var. GcExcel dışındaki ekstra NuGet paketlerine gerek yok.

---

## Çözümün Genel Bakışı

Koda dalmadan önce, “sayfaları bağlamak” ifadesinin SmartMarker bağlamında ne anlama geldiğini inceleyelim:

1. **Master sayfa** – Her varlık için bir satır tutar (ör. müşteri listesi).
2. **Detail sayfa** – Bir master satıra ait satırları içerir (ör. her müşterinin siparişleri).
3. **SmartMarker sözdizimi** – İşlemcinin iki veri tablosunu nasıl bağlayacağını belirten küçük bir işaretleme dili (`{MasterSheet}#master;{DetailSheet}#detail`).
4. **İşlemci seçenekleri** – `MasterDetail` özelliğini etkinleştirmek, motorun master satırlarını otomatik olarak tekrarlamasını ve ilgili detail satırlarını altına yerleştirmesini sağlar.

Bu parçaları anlamak, ileride yaklaşımı özelleştirmenize yardımcı olur—belki üç seviyeli iç içeleme ya da koşullu biçimlendirme ihtiyacınız vardır. Uygulamayı adım adım izlerken bu zihinsel modeli elinizde bulundurun.

---

## Adım 1: Master‑Detail İşleme İçin Hiyerarşik Veri Hazırlama

İlk olarak, master‑detail ilişkisinin yansıtıldığı bir veri kaynağına ihtiyacınız var. Çoğu gerçek dünyada bu veri bir veritabanından gelir, ancak açıklık olması açısından anonim bir nesne literalı kullanacağız.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Neden önemli:** SmartMarker ilişkileri sihirli bir şekilde tahmin etmez; eşleşen özellik adlarını (`MasterId` → `Id`) arar. Veriyi bu şekilde yapılandırarak işleme motoruna net bir harita veririz; bu da **sayfaları nasıl bağlayacağınız**ın temel taşıdır.

> **Pro ipucu:** Veriniz `DataTable` nesnelerinde ise, aynı adlarla özellik olarak ortaya koyun—SmartMarker herhangi bir enumerable koleksiyonla çalışır.

---

## Adım 2: Bir Çalışma Kitabı Oluşturma ve Şablon Yükleme

SmartMarker, genellikle sayfa adlarını ve yer tutucu işaretçileri zaten içeren mevcut bir Excel çalışma kitabı üzerinde çalışır. Bellekte bir çalışma kitabı oluşturalım ve *MasterSheet* ve *DetailSheet* adında iki boş çalışma sayfası ekleyelim.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

İsterseniz bir `.xlsx` dosyasını diskten (`wb.Open("Template.xlsx")`) yükleyebilirsiniz; bu, düzeni önce Excel'de tasarlamak istediğinizde faydalıdır. Önemli olan, sayfa adlarının SmartMarker dizesinde referans vereceğiniz adlarla eşleşmesidir.

---

## Adım 3: SmartMarkerProcessor'ı Örnekleme ve Master‑Detail Modunu Etkinleştirme

Şimdi işaretçileri okuyup veriyi yapıştıracak motoru devreye alıyoruz. `SmartMarkerProcessor`, çalışma kitabını bir yapıcı argümanı olarak alır ve `Options.MasterDetail` bayrağı, `#master` ve `#detail` işaretçilerini bağlı bir çift olarak ele almasını sağlar.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**`MasterDetail` neden etkinleştirilmeli?** Bu bayrak olmadan, işlemci `{MasterSheet}#master` ve `{DetailSheet}#detail` ifadelerini bağımsız işlemler olarak görür, satırlar arasındaki kritik ilişkiyi kaybeder. Bayrağı ayarlamak, **sayfaları nasıl bağlayacağınız**ın gerçekten çalışmasını sağlayan tek satırdır.

---

## Adım 4: SmartMarker Dizesini Tanımlama ve İşlemciyi Çalıştırma

İşaretçi dizesi, hangi sayfanın master, hangisinin detail olduğunu SmartMarker'a bildirir. Sözdizimi basittir: `{SheetName}#master;{SheetName}#detail`. Ek işaretçiler (ör. `#header`) ekleyebilirsiniz ancak temel bir rapor için gerekli değildir.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

`Process` çalıştırıldığında motor:

1. Her master satırını başlığın altındaki ilk boş satırdan başlayarak *MasterSheet*'e yazar.
2. Her master satırı için `Details` koleksiyonunu tarar, `MasterId` değeri master `Id` ile eşleşen satırları bulur ve bunları *DetailSheet*'e ilgili master kaydının hemen altına yazar.

---

## Adım 5: Sonuç Çalışma Kitabını Kaydetme veya Dışa Aktarma

Bu noktada tamamen doldurulmuş bir çalışma kitabınız var. Diske kaydedebilir, bir web istemcisine akış olarak gönderebilir ya da PDF'ye dönüştürebilirsiniz.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Dosyayı açtığınızda iki sayfa göreceksiniz: *MasterSheet* `A` ve `B` değerlerini listeler, *DetailSheet* ise master `1` altında `Item1`, master `2` altında `Item2` gösterir. Bu, **master sayfasını doldurma** ve **master‑detail raporu oluşturma**ın tek seferde gerçekleşmesinin özüdür.

---

## Görsel Genel Bakış

![SmartMarkerProcessor kullanarak Excel'de sayfaları nasıl bağlayacağınızı gösteren diyagram](https://example.com/diagram.png "Sayfaları bağlama diyagramı")

Diyagram (alt metin ana anahtar kelimeyi içerir), veri akışını C# nesnelerinden → SmartMarkerProcessor → bağlanmış Excel sayfalarına gösterir.

---

## Yaygın Kenar Durumlarını Ele Alma

### Master Başına Birden Çok Detay Satırı

Bir master satırının birden fazla ilgili detayı varsa, SmartMarker master satırını bir kez tekrar eder ve ardından *tüm* eşleşen detay satırlarını altına yazar. Ek bir koda gerek yok—sadece `Details` koleksiyonunuzun tüm satırları içerdiğinden emin olun.

### Detay Eksikliği

Bir master kaydının eşleşen detay satırı yoksa, detay sayfası o bölümü basitçe atlar. Bir yer tutucu (ör. “No items”) istiyorsanız, şablonda `=IF(COUNTA(A2:B2)=0,"No items","")` gibi bir Excel formülü kullanan hesaplanmış bir sütun ekleyebilirsiniz.

### Büyük Veri Setleri

On binlerce satırı işlemek bellek yoğun olabilir. Performansı yüksek tutmak için:

- `processor.Options.EnableStreaming = true` kullanın (GcExcel 2025+ sürümlerde mevcuttur).
- Veriyi parçalara bölüp her parçayı ayrı ayrı işleyin, ardından çalışma kitaplarını birleştirin.

### Özel Sütun Eşlemesi

Özellik adlarınız eşleşmiyorsa (`MasterKey` vs `Id`), işleme başlamadan önce `SmartMarkerProcessor.Map` metodunu kullanarak bir takma ad oluşturabilirsiniz.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, hemen çalıştırabileceğiniz eksiksiz, kopyala‑yapıştır hazır bir program aşağıdadır.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar ve tam çalışan kod örnekleri içerir.

- [Aspose.Cells for Java Kullanarak Excel'de Dış Bağlantı Formüllerini Yönetme](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Aspose.Cells ile Java'da Dinamik Excel Sayfaları: Kapsamlı Bir Kılavuz](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Aspose.Cells Java ile Dinamik Excel Raporları: Adlandırılmış Aralıklar ve Karmaşık Formüller](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}