---
title: Excel'de Dişli Türü Akıllı Sanatından Metin Çıkarma
linktitle: Excel'de Dişli Türü Akıllı Sanatından Metin Çıkarma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de dişli tipi SmartArt'tan metnin nasıl çıkarılacağını öğrenin. Adım adım kılavuz ve kod örneği dahildir.
weight: 10
url: /tr/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Dişli Türü Akıllı Sanatından Metin Çıkarma

## giriiş
Excel ile çalışırken, mesajlarınızı görsel olarak çekici bir şekilde iletmenize yardımcı olan SmartArt grafikleriyle karşılaşabilirsiniz. Bu grafikler arasında, dişli tipi SmartArt, hiyerarşik ve yönsel akışları nedeniyle favori bir tanesidir ve genellikle proje yönetimi veya sistem modellemede kullanılır. Peki ya bu şekillerden programatik olarak metin çıkarmanız gerekirse? İşte tam bu noktada Aspose.Cells for .NET işe yarıyor! Bu blog yazısında, Aspose.Cells for .NET kullanarak Excel'de dişli tipi SmartArt şekillerinden metin çıkarma konusunda adım adım bir kılavuzda size yol göstereceğiz.
## Ön koşullar
Başlamadan önce, sahip olmanız gereken bazı temel ön koşullar var. Endişelenmeyin; basit ve sizi bu konuda yönlendireceğim.
### .NET Ortamı
Bilgisayarınızda bir .NET geliştirme ortamının kurulu olduğundan emin olun. Bu, Visual Studio veya .NET geliştirmeyi destekleyen herhangi bir IDE olabilir.
### .NET için Aspose.Cells
 Sonra, Aspose.Cells kütüphanesini yüklemeniz gerekecek. Bu, Excel dosyalarını sorunsuz bir şekilde düzenlemenizi sağlayacak güç merkezidir. Bunu şuradan indirebilirsiniz:[Aspose Sürümleri sayfası](https://releases.aspose.com/cells/net/) . Eğer önce keşfetmek istiyorsanız, şu avantajdan yararlanın:[ücretsiz deneme](https://releases.aspose.com/).
### C# Temel Bilgisi
Bu eğitimde takip etmeniz gereken tek şey C# programlamanın temel bir anlayışıdır. Eğer yeniyseniz endişelenmeyin—adımları mümkün olduğunca yeni başlayanlar için uygun olacak şekilde tasarlayacağım.
### Örnek Excel Dosyası
Bu eğitim için, dişli tipi SmartArt şekilleri içeren bir örnek Excel dosyasına da ihtiyacınız olacak. Kolayca bir tane oluşturabilir veya çevrimiçi bir şablon bulabilirsiniz. Sadece SmartArt'ın en az bir dişli tipi şekil içerdiğinden emin olun.
## Paketleri İçe Aktar
Kodlamaya başlamak için gerekli paketleri içe aktarmanız gerekir. İşte nasıl yapacağınız:
### Yeni Bir Proje Oluştur
1. .NET IDE'nizi açın.
2. Yeni bir proje oluşturun. Örneğin, .NET seçenekleri altında 'Konsol Uygulaması'nı seçin.
3. Projenize bir isim verin ve istediğiniz çerçeveyi ayarlayın. 
### Referans Ekle
Aspose.Cells'i kullanmak için projenize kütüphane referanslarını eklemeniz gerekir:
1. Çözüm Gezgini'nde projenizin adına sağ tıklayın.
2. “NuGet Paketlerini Yönet” seçeneğini seçin.
3. "Aspose.Cells"i arayın ve yükleyin.
Kurulum tamamlandıktan sonra kodlamaya başlayabilirsiniz!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Şimdi metni çıkarmak için kullanacağınız kodu parçalayalım. Bunu adım adım yapacağız.
## Adım 1: Kaynak Dizini Ayarlayın
Öncelikle Excel dosyanızın bulunduğu dizini tanımlayarak başlayın:
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
```
 Değiştirdiğinizden emin olun`"Your Document Directory"` Excel dosyanızın gerçek yolunu belirtin.
## Adım 2: Excel Çalışma Kitabını yükleyin
Sonra Excel çalışma kitabını yükleyeceğiz. İçeriğine şu şekilde erişebiliriz:
```csharp
// Dişli tipi akıllı sanat şeklini içeren örnek Excel dosyasını yükleyin.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Bu parça örnek Excel çalışma kitabınızı yükleyecektir.
## Adım 3: İlk Çalışma Sayfasına Erişim
Çalışma kitabını yüklediğimize göre, SmartArt'ımızın bulunduğu ilk çalışma sayfasına erişelim:
```csharp
// İlk çalışma sayfasına erişin.
Worksheet ws = wb.Worksheets[0];
```
Bu, daha fazla düzenleme için ilk çalışma sayfasını alır.
## Adım 4: İlk Şekle Erişim
Sonra, çalışma sayfamızdaki ilk şekle erişmemiz gerekiyor. Bunu yaparak, SmartArt grafiklerimizde gezinebiliriz:
```csharp
// İlk şekle erişin.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Burada, ihtiyacımız olan SmartArt olduğunu düşündüğümüz ilk şekle odaklanıyoruz.
## Adım 5: Grup Şeklini Alın
Şeklimizi elde ettikten sonra, SmartArt gösteriminin sonucunu alma zamanı geldi:
```csharp
// Dişli tipi akıllı sanat şeklinin sonucunu grup şekli şeklinde alın.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Bu, dişli tipi SmartArt'ımızı gruplanmış bir şekil olarak geri getirir.
## Adım 6: Bireysel Şekilleri Çıkarın
Şimdi SmartArt'ımızı oluşturan bireysel şekilleri çıkaralım:
```csharp
// Grup şekillerinden oluşan bireysel şekillerin listesini alın.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Bu dizi, döngüye almamız gereken tüm bireysel şekilleri tutacaktır.
## Adım 7: Metni Çıkarın ve Yazdırın
Son olarak, şekiller dizimizde bir döngü oluşturabilir ve herhangi bir dişli tipi şekilden metni çıkarabiliriz:
```csharp
// Dişli tipi şekillerin metinlerini çıkartıp konsolda yazdır.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Bu döngüde şeklin türünü kontrol ediyoruz ve eğer dişli tipi bir şekil ise metni yazdırıyoruz.
## Adım 8: Yürütme Onayı
Son olarak, işlem başarıyla tamamlandığında bir onay mesajı eklemek isteyebilirsiniz:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Böylece çıkarma işleminiz tamamlanmış olacak ve konsolda metin çıktınızı görmelisiniz!
## Çözüm
 Tebrikler! Excel'de Aspose.Cells for .NET kullanarak dişli tipi SmartArt şekillerinden metin çıkarmayı öğrendiniz. Bu kullanışlı teknik, görsel veri gösterimine dayanan raporları veya belgeleri otomatikleştirmenin kapılarını açar. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, SmartArt'tan bilgi kontrol etmek ve çıkarmak iş akışınızı kolaylaştırabilir ve sizi daha verimli hale getirebilir. Ayrıntılı[Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/) daha fazla yetenek için.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını kolayca oluşturmalarına ve düzenlemelerine olanak tanıyan bir .NET kütüphanesidir.
### Aspose.Cells'i diğer dillerle kullanabilir miyim?
Evet! Aspose.Cells, Java ve Python da dahil olmak üzere birden fazla programlama dilinde mevcuttur.
### .NET için Aspose.Cells'i satın almam gerekir mi?
 Aspose.Cells ücretsiz deneme sunuyor ancak uzun süreli kullanım için satın alma gerekiyor. Satın alma seçeneklerini bulabilirsiniz[Burada](https://purchase.aspose.com/buy).
### Aspose.Cells kullanıcıları için destek mevcut mu?
 Kesinlikle! Topluluk desteğini şu adreste bulabilirsiniz:[Aspose.Cells forumu](https://forum.aspose.com/c/cells/9).
### Bu yöntemi kullanarak başka SmartArt türleri de çıkarabilir miyim?
Evet, kodunuzdaki koşulları değiştirerek çeşitli SmartArt şekillerinden küçük değişikliklerle metin çıkarabilirsiniz.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
