---
title: Aspose.Cells ile Excel'de Liste Nesnesini Biçimlendirin
linktitle: Aspose.Cells ile Excel'de Liste Nesnesini Biçimlendirin
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de bir liste nesnesinin nasıl biçimlendirileceğini öğrenin. Tabloları kolayca oluşturun ve biçimlendirin.
weight: 11
url: /tr/net/tables-and-lists/formatting-list-object/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'de Liste Nesnesini Biçimlendirin

## giriiş
Excel verilerinizin öne çıkmasını hiç istediniz mi? .NET'te Excel dosyalarıyla çalışıyorsanız, Aspose.Cells tam da bunu yapabilen harika bir kütüphanedir. Bu araç, birçok gelişmiş Excel görevinin yanı sıra programatik olarak tablolar oluşturmanıza, biçimlendirmenize ve stillendirmenize olanak tanır. Bugün, belirli bir kullanım örneğine dalacağız: Excel'de bir liste nesnesini (veya tabloyu) biçimlendirme. Bu eğitimin sonunda, bir veri tablosu oluşturmayı, stil eklemeyi ve hatta özet hesaplamaları ayarlamayı öğreneceksiniz.
## Ön koşullar
Kodlama sürecine başlamadan önce birkaç şeyi ayarladığınızdan emin olun:
1. Visual Studio veya herhangi bir .NET IDE: .NET kodunuzu yazmak ve çalıştırmak için bir geliştirme ortamına ihtiyacınız olacak.
2.  .NET için Aspose.Cells: Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. Bunu şuradan indirebilirsiniz:[Aspose.Cells for .NET indirme sayfası](https://releases.aspose.com/cells/net/) veya Visual Studio'da NuGet aracılığıyla yükleyebilirsiniz.
3. Temel .NET bilgisi: Bu kılavuz C# ve .NET'e aşina olduğunuzu varsayar.
4.  Aspose Lisansı (İsteğe bağlı): Filigran olmadan tam işlevsellik için, bir tane edinmeyi düşünün[geçici lisans](https://purchase.aspose.com/temporary-license/) veya bir tane satın al[Burada](https://purchase.aspose.com/buy).

## Paketleri İçe Aktar
Her şey hazır olduğunda, gerekli using yönergelerini kodunuza ekleyin. Bu, tüm Aspose.Cells işlevlerinin projenizde mevcut olmasını sağlar.
```csharp
using System.IO;
using Aspose.Cells;
```
Süreci, her biri açık talimatlar içeren, sindirilebilir adımlara bölelim.
## Adım 1: Belge Dizininizi Ayarlayın
Herhangi bir dosyayı kaydetmeden önce, çıktı dosyalarımızın kaydedileceği bir dizin belirtelim. Bu dizin yolu, ortaya çıkan Excel dosyasını oluşturmak ve depolamak için kullanılacaktır.
```csharp
string dataDir = "Your Document Directory";
// Dizinin var olup olmadığını kontrol edin; yoksa oluşturun
if (!System.IO.Directory.Exists(dataDir))
    System.IO.Directory.CreateDirectory(dataDir);
```
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
 Excel'deki bir çalışma kitabı yeni bir dosya veya elektronik tablo gibidir. Burada, yeni bir örnek oluşturuyoruz`Workbook` Verilerimizi tutacak sınıf.
```csharp
Workbook workbook = new Workbook();
```
## Adım 3: İlk Çalışma Sayfasına Erişim
Her yeni çalışma kitabının varsayılan olarak en az bir çalışma sayfası vardır. Burada, çalışmak için o ilk çalışma sayfasını alacağız.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
## Adım 4: Hücreleri Verilerle Doldurun
Şimdi eğlenceli kısma geliyoruz: veri ekleme! Basit bir veri tablosu oluşturmak için bir dizi hücreyi dolduralım. Bu veri, çalışanlara ve bölgelere göre üç aylık satışlar gibi küçük bir veri kümesini temsil edebilir.
```csharp
Cells cells = sheet.Cells;
// Başlık ekle
cells["A1"].PutValue("Employee");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Product");
cells["D1"].PutValue("Continent");
cells["E1"].PutValue("Country");
cells["F1"].PutValue("Sale");
// Örnek veri ekle
cells["A2"].PutValue("David");
cells["A3"].PutValue("David");
// Daha fazla satır ekle...
cells["B2"].PutValue(1);
cells["C2"].PutValue("Maxilaku");
// İhtiyaca göre daha fazla veri eklemeye devam edin
```
Bu veriler sadece bir örnektir. Özel ihtiyaçlarınıza göre özelleştirebilirsiniz.
## Adım 5: Çalışma Sayfasına Bir Liste Nesnesi (Tablo) Ekleyin
Excel'de "Liste Nesnesi" bir tabloyu ifade eder. Bu liste nesnesini verilerimizi içeren aralığa ekleyelim. Bu, biçimlendirme ve özet işlevlerini uygulamayı kolaylaştıracaktır.
```csharp
Aspose.Cells.Tables.ListObject listObject = sheet.ListObjects[sheet.ListObjects.Add("A1", "F15", true)];
```
 Burada,`"A1"` ile`"F15"` verilerimizi kapsayan aralıktır.`true` parametresi, ilk satırın (Satır 1) başlık olarak ele alınması gerektiği anlamına gelir.
## Adım 6: Tabloyu Şekillendirin
Artık tablomuz kurulduğuna göre, ona biraz stil ekleyelim. Aspose.Cells, aralarından seçim yapabileceğiniz bir dizi önceden tanımlanmış tablo stili sunar. Burada, orta bir stil uygulayacağız.
```csharp
listObject.TableStyleType = TableStyleType.TableStyleMedium10;
```
Farklı stiller deneyin (örneğin`TableStyleMedium9` veya`TableStyleDark1`) ihtiyaçlarınıza uygun olanı bulmak için.
## Adım 7: Toplamlar Satırını Görüntüle
 Verilerimizi özetlemek için bir toplamlar satırı ekleyelim.`ShowTotals` özellik tablonun alt kısmında yeni bir satırın açılmasını sağlayacaktır.
```csharp
listObject.ShowTotals = true;
```
## Adım 8: Toplamlar Satırı için Hesaplama Türünü Ayarlayın
Toplamlar satırında, her sütun için ne tür bir hesaplama istediğimizi belirtebiliriz. Örneğin, "Çeyrek" sütunundaki giriş sayısını sayalım.
```csharp
listObject.ListColumns[1].TotalsCalculation = TotalsCalculation.Count;
```
 Bu kod satırı, "Çeyrek" sütunu için toplam hesaplamasını şu şekilde ayarlar:`Count` . Ayrıca şu seçenekleri de kullanabilirsiniz:`Sum`, `Average`ve ihtiyaçlarınıza göre daha fazlası.
## Adım 9: Çalışma Kitabını Kaydedin
Son olarak çalışma kitabını daha önce oluşturduğumuz dizine Excel dosyası olarak kaydedelim.
```csharp
workbook.Save(dataDir + "output.xlsx");
```
Bu, tablonuzu içeren tam biçimlendirilmiş ve tasarlanmış bir Excel dosyası oluşturacaktır.

## Çözüm
Ve işte karşınızda—Aspose.Cells for .NET ile programatik olarak oluşturulmuş, tamamen biçimlendirilmiş, işlevsel bir Excel tablosu. Bu öğreticiyi takip ederek, yalnızca birkaç satır kodla bir veri tablosu kurmayı, stiller eklemeyi ve toplamları hesaplamayı öğrendiniz. Aspose.Cells güçlü bir araçtır ve bununla, doğrudan .NET uygulamalarınızdan dinamik, görsel olarak çekici Excel belgeleri oluşturabilirsiniz.

## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını programatik olarak oluşturmasına, düzenlemesine ve dönüştürmesine yardımcı olmak için tasarlanmış bir .NET kütüphanesidir. Çalışma sayfaları, grafikler, tablolar ve daha fazlasıyla çalışmak için güçlü seçenekler sunar.
### Aspose.Cells'i ücretsiz deneyebilir miyim?
 Evet, alabilirsiniz[ücretsiz deneme](https://releases.aspose.com/) Aspose.Cells'in özelliklerini keşfetmek için. Sınırlamalar olmadan tam erişim için, bir tane edinmeyi düşünün[geçici lisans](https://purchase.aspose.com/temporary-license/).
### Excel tabloma nasıl daha fazla stil ekleyebilirim?
 Aspose.Cells çeşitli seçenekler sunar`TableStyleType` tabloları biçimlendirmek için seçenekler. Farklı değerler deneyin`TableStyleLight1` veya`TableStyleDark10` Tablonuzun görünümünü değiştirmek için.
### Toplamlar satırında özel formüller kullanabilir miyim?
 Kesinlikle! Özel formülleri kullanarak ayarlayabilirsiniz.`ListColumn.TotalsCalculation`Toplam, ortalama veya özel formüller gibi belirli hesaplamaları uygulamak için özellik.
### Excel yüklü olmadan Excel dosyalarının otomatikleştirilmesi mümkün müdür?
Evet, Aspose.Cells, kodu çalıştıran sunucuya veya makineye Microsoft Excel'in kurulmasını gerektirmeyen bağımsız bir API'dir.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
