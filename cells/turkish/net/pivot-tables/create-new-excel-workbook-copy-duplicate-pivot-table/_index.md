---
category: general
date: 2026-02-09
description: Yeni bir Excel çalışma kitabı oluşturun ve özet tabloları zahmetsizce
  kopyalamayı öğrenin. Bu kılavuz, özet tabloyu nasıl çoğaltacağınızı ve çalışma kitabını
  yeni olarak kaydedeceğinizi gösterir.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: tr
og_description: C#'ta yeni bir Excel çalışma kitabı oluşturun ve bir pivot tabloyu
  anında kopyalayın. Pivot tabloyu nasıl çoğaltacağınızı ve çalışma kitabını yeni
  bir dosya olarak nasıl kaydedeceğinizi eksiksiz bir kod örneğiyle öğrenin.
og_title: Yeni Excel Çalışma Kitabı Oluştur – Adım Adım Pivot Kopyalama
tags:
- excel
- csharp
- aspose.cells
- automation
title: Yeni Excel Çalışma Kitabı Oluştur – Pivot Tablosunu Kopyala ve Çoğalt
url: /tr/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yeni Excel Çalışma Kitabı Oluştur – Pivot Tablosunu Kopyala ve Çoğalt

Hiç **yeni bir Excel çalışma kitabı** oluşturup, mevcut bir dosyadan karmaşık bir pivot tablosunu aktarmak zorunda kaldınız mı? Tek başınıza değilsiniz—birçok geliştirici raporlama boru hatlarını otomatikleştirirken bu engelle karşılaşıyor. İyi haber şu ki, birkaç satır C# ve Aspose.Cells kütüphanesi ile **pivot nasıl kopyalanır** sorusunu hızlıca yanıtlayabilir, **pivot tabloyu çoğaltabilir** ve **çalışma kitabını yeni olarak kaydedebilirsiniz**; Excel’i manuel olarak açmanıza gerek kalmaz.

Bu rehberde, kaynak çalışma kitabını yüklemekten çoğaltılmış sürümü kaydetmeye kadar tüm süreci adım adım inceleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, çalıştırmaya hazır bir kod parçacığı elde edeceksiniz. Gereksiz ayrıntı yok, sadece bugün test edebileceğiniz pratik bir çözüm.

## Bu Öğreticide Neler Ele Alınıyor

* **Önkoşullar** – .NET 6+ (veya .NET Framework 4.6+), Visual Studio ve Aspose.Cells for .NET NuGet paketi.
* **Adım adım kod** – **yeni Excel çalışma kitabı oluşturur**, pivotu kopyalar ve sonucu diske yazar.
* **Her satırın neden önemli olduğu** açıklamaları, sadece **ne yaptığı** değil.
* Gizli çalışma sayfaları veya büyük veri aralıkları gibi kenar durumlarını ele alma ipuçları.
* **Çalışma sayfasını nasıl kopyalanır** konusuna hızlı bir bakış; sadece pivot yerine tüm sayfayı kopyalamanız gerektiğinde.

Hazır mısınız? Hadi başlayalım.

![create new excel workbook illustration](image.png "Diagram showing source workbook, pivot copy, and destination workbook")

## Adım 1: Projeyi Kurun ve Aspose.Cells’i Yükleyin

**yeni Excel çalışma kitabı oluşturmak** için, doğru kütüphaneye referans veren bir projeye ihtiyacımız var.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Bu neden önemli:* Aspose.Cells tamamen bellek içinde çalışır, bu sayede sunucuda Excel’i hiç başlatmanız gerekmez. Ayrıca pivot önbellek bilgilerini korur; bu da gerçek bir **pivot tablo çoğaltması** için şarttır.

> **Pro ipucu:** .NET Core hedefliyorsanız, projenizin çalışma zamanı tanımlayıcısının (RID) dağıtım yapacağınız platformla eşleştiğinden emin olun; aksi takdirde yerel kütüphane yükleme hataları alabilirsiniz.

## Adım 2: Pivotu İçeren Kaynak Çalışma Kitabını Yükleyin

Şimdi mevcut bir dosyadan **pivot nasıl kopyalanır** sorusunu ele alacağız. Kaynak çalışma kitabı disk üzerindeki herhangi bir konumda, bir akışta ya da bir bayt dizisinde olabilir.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Bu aralığı seçmemizin nedeni:* Pivot tablo, normal bir hücre aralığı içinde bulunur, ancak aynı zamanda sayfaya bağlı gizli önbellek verileri de vardır. **Pivot dahil olmak üzere aralığı** kopyaladığınızda, Aspose.Cells önbelleğin de taşınmasını sağlar ve hedef dosyada işlevsel bir **pivot tablo çoğaltması** elde edersiniz.

## Adım 3: Kopyalanan Veriyi Alacak Yeni Excel Çalışma Kitabını Oluşturun

İşte **yeni Excel çalışma kitabı oluştur** ve çoğaltılmış pivotu içine yerleştir.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Neden temiz bir çalışma kitabı?** Sıfırdan başlamak, kalan formatlamaların veya gizli nesnelerin kopyalanan pivotu etkilemesini önler. Ayrıca sonuç dosya daha küçük olur; bu da otomatik e‑posta ekleri için kullanışlıdır.

## Adım 4: Pivot Aralığını Yeni Çalışma Kitabına Kopyalayın

Şimdi gerçek **pivot nasıl kopyalanır** işlemini yapıyoruz.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Bu tek satır tüm işi yapar:

* Hücre değerleri, formüller ve biçimlendirme aktarılır.
* Pivot önbelleği çoğaltılır, böylece yeni pivot tamamen işlevsel kalır.
* Pivot içindeki göreli referanslar yeni konuma otomatik olarak uyum sağlar.

### Kenar Durumlarını Ele Alma

* **Gizli çalışma sayfaları:** Kaynak sayfa gizli olsa bile pivot sorunsuz kopyalanır, ancak kullanıcı görünürlüğü için hedef sayfayı göstermek isteyebilirsiniz:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Büyük veri kümeleri:** Birkaç bin satırdan büyük aralıklar için `CopyTo` ve `CopyOptions` kullanarak işlemi akışa alabilir, bellek baskısını azaltabilirsiniz.

## Adım 5: Hedef Çalışma Kitabını Yeni Bir Dosya Olarak Kaydedin

Son olarak **çalışma kitabını yeni olarak kaydedin** ve sonucu doğrulayın.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

`copied.xlsx` dosyasını açtığınızda, orijinal pivotun tam bir kopyasını göreceksiniz; artık ek manipülasyonlar ya da dağıtım için hazır.

### Opsiyonel: Sadece Pivot Yerine Çalışma Sayfasını Nasıl Kopyalarsınız

Bazen tüm sayfayı, sadece pivotu değil, kopyalamak isteyebilirsiniz. Aynı API bunu çok basit hâle getirir:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Bu, **çalışma sayfası nasıl kopyalanır** sorusuna yanıt verir ve ek sayfa‑seviyesi ayarları korumanız gerektiğinde işe yarar.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, derleyip çalıştırabileceğiniz bağımsız bir konsol uygulaması şöyle:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Beklenen çıktı:** Konsol bir başarı mesajı verir ve `C:\Reports` içinde `copied.xlsx` dosyası, `source.xlsx`deki pivotla aynı işlevselliğe sahip bir pivotla ortaya çıkar.

## Yaygın Sorular ve Tuzaklar

* **Pivot içindeki formüller kırılır mı?** Hayır—pivot önbelleği aralıkla birlikte taşındığı için tüm hesaplanan alanlar aynı kalır.
* **Kaynak pivot dış veri bağlantıları kullanıyorsa ne olur?** Bu bağlantılar *kopyalanmaz*. Bağlantıları hedef çalışma kitabında yeniden oluşturmanız ya da pivotu önce statik bir tabloya dönüştürmeniz gerekir.
* **Birden fazla pivotu aynı anda kopyalayabilir miyim?** Kesinlikle—tüm pivotları kapsayan daha büyük bir aralık tanımlayabilir veya `sourceSheet.PivotTables` koleksiyonundaki her `PivotTable` nesnesini döngüyle tek tek kopyalayabilirsiniz.
* **`Workbook` nesnelerini dispose etmem gerekiyor mu?** `IDisposable` uygularlar, bu yüzden özellikle yüksek hacimli servislerde `using` blokları içinde kullanmak iyi bir alışkanlıktır.

## Sonuç

Artık **yeni Excel çalışma kitabı nasıl oluşturulur**, bir pivot nasıl kopyalanır, **pivot tablo nasıl çoğaltılır** ve **çalışma kitabı yeni olarak nasıl kaydedilir** konularını C# ve Aspose.Cells ile biliyorsunuz. Adımlar basit: yükle, oluştur, kopyala ve kaydet. Opsiyonel **çalışma sayfası nasıl kopyalanır** kod parçacığı sayesinde tam sayfa çoğaltma ihtiyacınız da karşılanıyor.

İleriye dönük olarak şunları keşfedebilirsiniz:

* Çoğaltılmış pivot için özel biçimlendirme ekleme.
* Veri değişikliklerinden sonra pivot önbelleğini programatik olarak yenileme.
* Çalışma kitabını PDF veya CSV’ye dışa aktararak sonraki sistemlere gönderme.

Deneyin, aralığı ayarlayın ve otomasyonun raporlama iş akışınızdaki zahmetli kısmı halletmesine izin verin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}