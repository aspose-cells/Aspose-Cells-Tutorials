---
title: Excel'de Font Alt Çizgisi Kullanımı
linktitle: Excel'de Font Alt Çizgisi Kullanımı
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Adım adım kılavuzumuzla Excel hücrelerindeki metinlerin altını kolayca çizmek için Aspose.Cells for .NET'i nasıl kullanacağınızı öğrenin.
weight: 14
url: /tr/net/working-with-fonts-in-excel/using-font-underline-type/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Font Alt Çizgisi Kullanımı

## giriiş
.NET uygulamalarında elektronik tablolar oluşturma veya Excel dosyalarını düzenleme söz konusu olduğunda, verimlilik ve kullanım kolaylığı en önemli unsurdur. .NET için Aspose.Cells, geliştiricilerin Excel dosyalarıyla sorunsuz bir şekilde çalışmasını sağlayan güçlü bir kütüphanedir. Bu eğitimde, Aspose.Cells kullanarak Excel'de alt çizgi yazı tipinin nasıl kullanılacağını inceleyeceğiz. Kavramları kavrayabilmenizi ve bunları kendi projelerinizde hiçbir zorluk çekmeden uygulayabilmenizi sağlayarak, takip etmesi kolay, adım adım talimatlar sunacağız!
## Ön koşullar
Kod örneklerimize dalmadan önce, geliştirme ortamınızın kullanıma hazır olduğundan emin olmak için birkaç ön koşul bulunmaktadır.
### C# Temel Bilgisi
C# programlama konusunda temel bir anlayışa sahip olmalısınız. Nesne yönelimli prensiplere aşinalık da kavramları daha iyi kavramanıza yardımcı olacaktır.
### Visual Studio'yu yükledim
 Kodunuzu etkili bir şekilde çalıştırmak ve test etmek için Visual Studio'nun yüklü olması önemlidir. Bunu şuradan indirebilirsiniz:[Microsoft web sitesi](https://visualstudio.microsoft.com/).
### .NET için Aspose.Cells
 Aspose.Cells for .NET kütüphanesini yüklediğinizden emin olun. Bunu şuradan indirebilirsiniz:[Aspose sürüm sayfası](https://releases.aspose.com/cells/net/) veya Visual Studio'daki NuGet Paket Yöneticisini kullanın.
### .NET Çerçevesi
Projenizde uygun .NET framework'ünün kurulu olduğundan emin olun. Aspose.Cells çeşitli sürümleri destekler; uyumluluk için belgelerini kontrol edin.
Bu ön koşullar sağlandığında, altı çizili metin içeren ilk Excel belgenizi oluşturmaya hazırsınız!
## Paketleri İçe Aktar
Başlamak için, C# projenize birkaç temel ad alanını içe aktarmanız gerekir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
using System.IO;
using Aspose.Cells;
```
Bu ad alanlarını eklemek, Aspose.Cells kullanarak Excel dosyalarıyla çalışmak için ihtiyaç duyacağınız tüm sınıflara ve yöntemlere erişmenizi sağlayacaktır.

Artık her şeyi ayarladığımıza göre, bir Excel hücresindeki metnin altını çizmek için gereken kodun her bir yönünü inceleyelim.
## Adım 1: Belge Dizininizi Ayarlayın
Her şeyden önce, Excel dosyalarınızı kaydedebileceğiniz sürücünüzde bir konuma ihtiyacınız olacak. Bu dizini şu şekilde oluşturabilirsiniz:
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Bu kod parçacığı belirtilen dizinin var olup olmadığını kontrol eder. Yoksa, sizin için oluşturur. Değiştir`"Your Document Directory"` İstediğiniz yol ile.
## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturun
Sonra, esasen Excel dosyanız olan bir çalışma kitabının yeni bir örneğini oluşturmak isteyeceksiniz. İşte nasıl:
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```
Bu satır yeni bir çalışma kitabı başlatır. Bunu, başyapıtınızı oluşturmaya başlayabileceğiniz boş bir tuval açmak olarak düşünün.
## Adım 3: Yeni bir Çalışma Sayfası Ekleyin
Çalışma kitabınız olduğunda, üzerinde çalışmak için bir çalışma sayfasına ihtiyacınız olacak. Bir tane ekleyelim:
```csharp
// Excel nesnesine yeni bir çalışma sayfası ekleme
int i = workbook.Worksheets.Add();
```
 Bu, çalışma kitabınıza yeni bir çalışma sayfası ekler ve yeni eklenen sayfanın dizinini değişkende depolar`i`.
## Adım 4: Yeni Çalışma Sayfasına Başvurun
Şimdi, az önce eklediğiniz çalışma sayfasına bir referans almanız gerekiyor. Bu, onu düzenlemenize olanak tanır:
```csharp
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[i];
```
Bu adımla kodunuzu doğrudan yeni çalışma sayfasına yönlendiriyor ve içerik eklemeye hazır hale getiriyorsunuz.
## Adım 5: Belirli Bir Hücreye Erişim
Şimdi metninizin nerede olmasını istediğinize karar verme zamanı. Bu durumda, A1 hücresini kullanacağız:
```csharp
// Çalışma sayfasından "A1" hücresine erişim
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
Burada A1 pozisyonundaki hücreyi tutup içine biraz metin ekleyelim.
## Adım 6: Hücreye Değer Ekleyin
Hadi o hücreye biraz içerik koyalım:
```csharp
// "A1" hücresine bir değer ekleniyor
cell.PutValue("Hello Aspose!");
```
Bu noktada, "Merhaba Aspose!" artık A1 hücrenizin içeriğidir. Basit, değil mi?
## Adım 7: Hücre Stilini Edinin
Metni altını çizmek için stil özelliklerine erişmeniz gerekir. Hücrenin geçerli stilini şu şekilde alabilirsiniz:
```csharp
// Hücre stilinin elde edilmesi
Style style = cell.GetStyle();
```
Bu satır, hücreye uygulanan mevcut stili getirir ve onu değiştirmenize olanak tanır.
## Adım 8: Yazı Tipini Altı Çizili Olarak Ayarlayın
Şimdi heyecan verici kısma geliyoruz! Yazı tipini güncelleyelim:
```csharp
// Yazı tipini altı çizili olarak ayarlama
style.Font.Underline = FontUnderlineType.Single;
```
Bu, font alt çizgi özelliğini tek bir alt çizgiye değiştirir. Diğer türleri de keşfedebilirsiniz, ancak şimdilik basit tutalım!
## Adım 9: Stili Hücreye Uygula
Yarı yolda bırakamazsın! Şimdi bu güncellenmiş stili hücrene geri ayarlaman gerekiyor:
```csharp
// Stili hücreye uygulama
cell.SetStyle(style);
```
İşte! Hücre artık yeni stili, altı çizili metinle yansıtıyor.
## Adım 10: Çalışma Kitabını Kaydedin
Son olarak şaheserinizi bir Excel dosyasına kaydedelim:
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Bu satır çalışma kitabını Excel 97-2003 biçiminde kaydeder. Dosya adının ve yolunun dosyanın bulunmasını istediğiniz yere doğru şekilde ayarlandığından emin olun.
## Çözüm
Gördüğünüz gibi, Aspose.Cells for .NET ile çalışmak yalnızca güçlü değil, aynı zamanda kullanıcı dostudur ve Excel dosyalarını zahmetsizce oluşturmanıza ve düzenlemenize olanak tanır. Bir hücredeki metnin altını çizmek, bu kütüphanenin yapabileceklerinin sadece yüzeyini tırmalamak. İster karmaşık raporlar oluşturun, ister büyük veri kümelerini işleyin, Aspose.Cells .NET uygulamalarınızda başarılı olmak için ihtiyaç duyduğunuz araçları size sağlar.
## SSS
### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, .NET uygulamalarında Excel dosyalarını program aracılığıyla işlemek için sağlam bir kütüphanedir.
### Aspose.Cells'i nasıl kurarım?
NuGet Paket Yöneticisi'ni kullanarak Visual Studio'ya yükleyebilir veya Aspose sürümleri sayfasından indirebilirsiniz.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet! Aspose, değerlendirme amaçlı ücretsiz deneme ve geçici lisans sunuyor.
### Aspose.Cells hangi Excel formatlarını destekler?
Aspose.Cells XLS, XLSX, CSV ve daha birçok formatı destekler.
### Aspose.Cells için yardım veya desteği nerede bulabilirim?
Aspose web sitesinde topluluk desteğine ve forumlara erişebilirsiniz.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
