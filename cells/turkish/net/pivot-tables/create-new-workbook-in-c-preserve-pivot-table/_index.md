---
category: general
date: 2026-02-15
description: C#'ta yeni bir çalışma kitabı oluşturun ve bir pivot tabloyu tanımını
  kaybetmeden kopyalayın. Satırları nasıl kopyalayacağınızı, pivot tabloyu nasıl koruyacağınızı
  ve pivot tabloyu kolayca nasıl çoğaltacağınızı öğrenin.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: tr
og_description: C#'te yeni bir çalışma kitabı oluşturun ve bir pivot tabloyu tanımını
  koruyarak kopyalayın. Geliştiriciler için adım adım rehber.
og_title: C# ile Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Koru
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'ta Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Koru
url: /tr/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

However the phrase appears many times; maybe keep as is. We'll keep bold English phrase unchanged.

Similarly "preserve pivot table", "duplicate pivot table", "copy rows". Those are technical actions; maybe keep English. But we can translate surrounding text.

Let's translate.

Proceed.

Will produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Koru

Başka bir dosyadan bir pivot tablosunun tam bir kopyasını içeren **create new workbook**’a C#’ta ihtiyaç duyduğunuz oldu mu? Tek başınıza değilsiniz. Birçok raporlama sürecinde pivot tablosu analizlerin kalbidir ve veriyi taşıdığınızda tanımının kaybolması bir kabus olur.

İyi haber? Birkaç satır Aspose.Cells kodu ile satırları—pivot tablo dahil—yeni bir çalışma kitabına kopyalayabilir ve her şeyi aynı tutabilirsiniz. Aşağıda **copy rows**, **preserve pivot table** ayarlarını nasıl yapacağınızı ve hatta **duplicate pivot table**’ı dosyalar arasında formülleri ya da önbelleği bozmadan nasıl çoğaltacağınızı göreceksiniz.

## Bu Öğreticide Neler Ele Alınıyor

Bu rehberde şunları adım adım inceleyeceğiz:

1. Pivot tablosu zaten bulunan kaynak çalışma kitabını yükleme.  
2. Hedef için **create new workbook** nesnelerini oluşturma.  
3. Pivot tabloyu içeren aralığı aktarmak için `CopyRows` kullanma.  
4. Sonucu kaydederken pivot tablonun işlevsel kalmasını sağlama.  

Harici bir dokümantasyona gerek yok—sadece kod, nedenleri ve projenize doğrudan yapıştırabileceğiniz birkaç pratik ipucu.

> **Pro tip:** Aspose.Cells .NET Core, .NET Framework ve hatta Xamarin ile çalışır, bu yüzden aynı snippet ihtiyacınız olan her yerde çalışır.

---

![Create new workbook with copied pivot table](/images/create-new-workbook-pivot.png "create new workbook with copied pivot table")

## Adım 1 – Yeni Çalışma Kitabı Oluştur ve Kaynak Dosyayı Yükle

İlk yaptığımız şey **create new workbook** nesnelerini oluşturmaktır. Biri orijinal veriyi tutar, diğeri kopyalanan aralığı alacak.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Bunun önemi:*  
`Workbook`, Aspose.Cells içinde herhangi bir Excel işleminin giriş noktasıdır. Yeni bir çalışma kitabı örneği oluşturarak temiz bir sayfa garantileriz—daha sonra karışabilecek gizli stiller ya da gereksiz çalışma sayfaları olmaz.

## Adım 2 – Pivot Tablo Dahil Satırları Nasıl Kopyalarız

Şimdi sorunun özü geliyor: **copy rows** yaparak pivot tabloyu düzleştirmeden nasıl kopyalarız? `CopyRows` metodu tam da bunu yapar.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Dikkat edilmesi gereken birkaç nokta:

* `startRow` ve `totalRows` pivot tablonun bulunduğu bloğu tanımlar.  
* Metod **hem** ham veriyi hem de pivot önbelleğini kopyalar, böylece hedef çalışma kitabı pivot tabloyu anında yeniden oluşturabilir.  
* Pivot tablonuz sayfanın daha derin bir yerinde başlıyorsa sadece indeksleri değiştirin—farklı bir API çağrısına gerek yok.

> **Sık sorulan soru:** *Kopyalanan pivot kaynağının veri referansını kaybeder mi?*  
> Hayır. Aspose.Cells önbelleği doğrudan çalışma sayfasına gömer, bu yüzden pivot yeni dosyada kendi içinde bağımsız olur.

## Adım 3 – Hedefi Kaydederken Pivot Tabloyu Koru

Satırlar kopyalandıktan sonra pivot tablo, kaynakta olduğu gibi hedef çalışma kitabında da bulunur. Dosyayı kaydetmek basittir.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

`destination.xlsx` dosyasını Excel’de açtığınızda pivot tablonun yenilenmeye hazır olduğunu göreceksiniz. **preserve pivot table** davranışı otomatik olarak gerçekleşir çünkü önbellek satırlarla birlikte taşınmıştır.

### Sonucu Doğrulama

Dosyayı açın ve:

1. Pivot tabloya tıklayın.  
2. Alan listesi görünür—bu, önbelleğin sağlam olduğu anlamına gelir.  
3. Yenilemeyi deneyin; veri hatasız güncellenir.

Eğer *#REF!* hatası alırsanız, kopyalanan aralığın gizli önbellek satırlarını (genellikle görünür verinin hemen ardından) içerdiğinden emin olun.

## Adım 4 – Pivot Tabloyu Birden Çok Çalışma Kitabına Çoğalt (Opsiyonel)

Bazen aynı pivot tabloyu birkaç raporda kullanmanız gerekir. Az önce kullandığımız desen rahatça ölçeklenir—her yeni çalışma kitabı için kopyalamayı tekrarlayın.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Bu snippet **duplicate pivot table** işlemini tek bir döngüyle üç kez gerçekleştirir. `targets` dizisini raporlama takviminize göre ayarlayın.

### Dikkat Edilmesi Gereken Kenar Durumları

| Durum | Dikkat Edilmesi Gereken | Çözüm |
|-----------|-------------------|-----|
| Pivot dış veri kaynağı kullanıyor | Önbellek, yeni makinede bulunmayan bir bağlantıya referans verebilir | Veri kaynağını gömün ya da hedef çalışma kitabında bağlantıyı yeniden oluşturun |
| Çok büyük pivot ( > 100 k satır ) | `CopyRows` bellek yoğun olabilir | `CopyRows`’u parçalar halinde kullanın ya da bellek kullanımını sınırlamak için `Copy` + `PasteOptions` düşünün |
| Çalışma sayfasında gizli satır/sütunlar | Sadece görünür satırları kopyalarsanız gizli önbellek satırları atlanabilir | Görünür alanı değil, önbelleği içeren tam satır aralığını her zaman kopyalayın |

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, konsol uygulamasına bırakabileceğiniz bağımsız bir program elde edersiniz.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Programı çalıştırın, `destination.xlsx` dosyasını açın ve aynı pivot tablonun verilerinizi dilimleyip dilimleyeceğini görün. Manuel yeniden oluşturma gerekmez.

---

## Sonuç

**create new workbook**’ı C#’ta nasıl **copy pivot table** yaparak her ayarı koruyarak gerçekleştireceğinizi gösterdik. `CopyRows` kullanarak **preserve pivot table** işlevselliğini güvenilir bir şekilde elde eder, “**how to copy rows**” sorusuna yanıt bulur ve **duplicate pivot table**’ı birden çok raporda minimum kodla yapabilirsiniz.

Sonraki adımlar? Kopyalanan aralığı, aynı pivot’a referans veren grafikleri de içerecek şekilde genişletin ya da biçimlendirmeyi tam olarak korumak için `PasteOptions` ile deneyler yapın. Aynı desen, tablolar ve adlandırılmış aralıklar gibi diğer Aspose.Cells nesneleri için de çalışır; genişletmekten çekinmeyin.

Harici bir DB’den veri çeken bir pivot ya da bulutta yaşayan bir çalışma kitabı gibi bir sorunla karşılaştıysanız, aşağıya yorum bırakın; birlikte çözelim. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}