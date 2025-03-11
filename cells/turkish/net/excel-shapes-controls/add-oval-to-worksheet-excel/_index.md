---
title: Excel'de Çalışma Sayfasına Oval Ekleme
linktitle: Excel'de Çalışma Sayfasına Oval Ekleme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel çalışma sayfasına oval eklemeyi öğrenin. Ayrıntılı kod açıklamalarıyla adım adım kılavuz.
weight: 17
url: /tr/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Oval Ekleme

## giriiş
Çarpıcı ve etkileşimli Excel dosyaları oluşturmak yalnızca sayılar ve formüller içermeyebilir. Oval gibi şekiller, çalışma sayfalarınıza görsel bir çekicilik katabilir veya işlevsel öğeler sağlayabilir. Bu eğitimde, Aspose.Cells for .NET'i kullanarak Excel çalışma sayfalarına programatik olarak oval eklemeyi keşfedeceğiz. İster biraz gösteriş ister işlevsellik katmak isteyin, her şeyi açıklayan adım adım bir kılavuzla sizi koruduk.
## Ön koşullar
Koda dalmadan önce, yerinde olması gereken birkaç şey var:
1.  Aspose.Cells for .NET Kütüphanesi: Buradan indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/) veya Visual Studio'da NuGet kullanarak kurun.
2. Geliştirme Ortamı: Visual Studio benzeri AC# IDE.
3. C# Temel Anlayışı: C# dilindeki temel kodlama kavramlarına aşina olmalısınız.
 Ayrıca, Aspose.Cells for .NET kütüphanesini yükleyerek projenizi kurmayı unutmayın. Henüz bir lisansınız yoksa, bir lisans için başvurabilirsiniz.[geçici lisans](https://purchase.aspose.com/temporary-license/) veya kullanın[ücretsiz deneme](https://releases.aspose.com/) Versiyon.
## Paketleri İçe Aktar
Herhangi bir kod yazmadan önce, gerekli ad alanlarını eklediğinizden emin olun. Doğru kütüphaneleri kullandığınızdan emin olmak için işte C# kod parçacığı:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Adım 1: Dizininizi Ayarlayın
Bir Excel sayfasına oval eklemenin ilk adımı, Excel dosyanızın nereye kaydedileceğini belirtmektir. Çalışmamızı kaydetmeden önce dizin yolunu tanımlayalım ve dizinin mevcut olduğundan emin olalım.

Bir dizin yolu oluşturacağız ve var olup olmadığını doğrulayacağız. Klasör yoksa, oluşturulacak.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu adım, dosyanızın doğru yere kaydedilmesini ve daha sonra dosya yolu sorunlarıyla karşılaşmamanızı sağladığı için önemlidir.
## Adım 2: Yeni Bir Çalışma Kitabı Başlatın
Sonra, oval şekillerimizi ekleyeceğimiz yeni bir çalışma kitabı oluşturmamız gerekiyor. Çalışma kitabı bir Excel dosyasını temsil ediyor ve içine içerik veya şekiller ekleyebiliriz.

 Bu adımda yeni bir örnek oluşturuyoruz`Workbook` Excel dosyamızın kapsayıcısı olarak hizmet edecek nesne.
```csharp
// Yeni bir Çalışma Kitabı örneği oluşturun.
Workbook excelbook = new Workbook();
```
## Adım 3: İlk Oval Şekli Ekleyin
Şimdi eğlenceli kısma geliyoruz: çalışma sayfasına oval bir şekil eklemek. Bu oval, bir düğme veya vurgulama gibi görsel bir öğeyi temsil edebilir. Çalışma kitabımızın ilk çalışma sayfasına ilk oval şekli ekleyerek başlayacağız.

 Burada şunu kullanıyoruz:`Shapes.AddOval()` Çalışma sayfasında belirli bir satır ve sütunda oval oluşturma yöntemi.
```csharp
// Oval bir şekil ekleyin.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
 İçerideki parametreler`AddOval()` aşağıdaki gibidir:
- İlk iki sayı ovalin sol üst köşesindeki satırı ve sütunu temsil eder.
- Sonraki iki sayı ovalin yüksekliğini ve genişliğini temsil eder.
## Adım 4: Ovalin Yerleşimini ve Stilini Ayarlayın
 Oval oluşturulduktan sonra, konumunu, çizgi kalınlığını ve çizgi stilini ayarlayabiliriz.`Placement` özellik, çalışma sayfasındaki hücreleri yeniden boyutlandırdığınızda veya taşıdığınızda ovalin nasıl davranacağını belirler.

Ovalimizi serbest yüzer hale getirip görünümünü ayarlıyoruz.
```csharp
// Ovalin yerleşimini ayarlayın.
oval1.Placement = PlacementType.FreeFloating;
// Çizgi kalınlığını ayarlayın.
oval1.Line.Weight = 1;
// Ovalin çizgi stilini ayarlayın.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Bu, ovalin çalışma sayfası içerisinde serbestçe hareket etmesini sağlar ve çizgi kalınlığı ile stili görsel tutarlılık için ayarlanır.
## Adım 5: Başka Bir Oval (Daire) Şekil Ekleyin
Neden bir taneyle yetinelim? Bu adımda, yüksekliği ve genişliği aynı yaparak mükemmel bir daire oluşturarak başka bir oval şekil ekleyeceğiz.

Başka bir oval daha oluşturup farklı bir yere yerleştiriyoruz ve eşit yükseklik ve genişlik ayarlayarak dairesel bir şekle sahip olmasını sağlıyoruz.
```csharp
// Bir oval (daire) şekli daha ekleyin.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Adım 6: İkinci Ovali Şekillendirin
Tıpkı daha önce yaptığımız gibi, bu ikinci ovalin (veya dairenin) yerleşimini, ağırlığını ve çizgi stilini ayarlayacağız.

İlk ovalin tarzına uyması için ikinci ovalde de benzer özellikler uyguluyoruz.
```csharp
// Ovalin yerleşimini ayarlayın.
oval2.Placement = PlacementType.FreeFloating;
// Çizgi kalınlığını ayarlayın.
oval2.Line.Weight = 1;
// Ovalin çizgi stilini ayarlayın.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Adım 7: Çalışma Kitabını Kaydedin
Son olarak, az önce eklediğimiz ovallerle çalışma kitabını kaydetmemiz gerekiyor. Dosyayı kaydetmek, tüm değişikliklerimizin saklandığından emin olmamızı sağlar.

Çalışma kitabını daha önce tanımladığımız dizin yoluna kaydediyoruz.
```csharp
// Excel dosyasını kaydedin.
excelbook.Save(dataDir + "book1.out.xls");
```
Ve işte bu kadar! Excel çalışma sayfanıza oval şekilleri başarıyla eklediniz ve dosyayı kaydettiniz.
## Çözüm
Aspose.Cells for .NET kullanarak bir Excel sayfasına oval gibi şekiller eklemek yalnızca basit değil, aynı zamanda elektronik tablolarınızı ek görsel öğelerle geliştirmenin eğlenceli bir yoludur. İster tasarım amaçlı ister tıklanabilir öğeler eklemek için olsun, şekiller Excel dosyalarınızın nasıl göründüğü ve çalıştığı konusunda önemli bir rol oynayabilir. Yani, bir dahaki sefere etkileşimli veya görsel olarak çekici Excel sayfaları gerektiren bir proje üzerinde çalıştığınızda, o mükemmel ovalleri nasıl ekleyeceğinizi tam olarak biliyorsunuz!
## SSS
### Aspose.Cells for .NET kullanarak dikdörtgenler veya çizgiler gibi başka şekiller ekleyebilir miyim?
 Evet, dikdörtgenler, çizgiler ve oklar gibi çeşitli şekiller ekleyebilirsiniz.`Shapes` Aspose.Cells'deki koleksiyon.
### Ovalleri ekledikten sonra boyutlarını değiştirmek mümkün mü?
Kesinlikle! Ovalleri ekledikten sonra yükseklik ve genişlik özelliklerini değiştirebilirsiniz.
### Çalışma kitabını XLS dışında hangi dosya biçimlerinde kaydedebilirim?
Aspose.Cells, XLSX, CSV ve PDF gibi birden fazla formatı destekler.
### Ovalin dış hatlarının rengini değiştirebilir miyim?
 Evet, ovalin çizgi rengini şu şekilde değiştirebilirsiniz:`Line.Color` mülk.
### Aspose.Cells için lisansa sahip olmak gerekli mi?
 Aspose.Cells'i ücretsiz deneme sürümüyle deneyebilirsiniz ancak bir[lisans](https://purchase.aspose.com/buy) uzun süreli kullanım veya gelişmiş özelliklere erişim için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
