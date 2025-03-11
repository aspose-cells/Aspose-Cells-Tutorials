---
title: .NET'te Pivot Tablosunun Kaynak Verilerini Programatik Olarak Değiştirme
linktitle: .NET'te Pivot Tablosunun Kaynak Verilerini Programatik Olarak Değiştirme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Kapsamlı adım adım eğitimimiz ile Aspose.Cells for .NET kullanarak pivot tablo kaynak verilerini programatik olarak nasıl değiştireceğinizi öğrenin.
weight: 10
url: /tr/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Pivot Tablosunun Kaynak Verilerini Programatik Olarak Değiştirme

## giriiş
Veri analizi dünyasında, çok az araç Microsoft Excel kadar parlaktır. Her gün, sayısız kullanıcı verileri yönetmek ve analiz etmek için Excel'e güveniyor, ancak perde arkasında, sadece tıklayıp sürüklemekten çok daha karmaşıktır. Excel dosyalarını programatik olarak değiştirmek istediyseniz, özellikle bir pivot tablonun kaynak verilerini değiştirmek için, doğru yerdesiniz! Bu kılavuzda, bunu .NET için Aspose.Cells kullanarak nasıl başarabileceğinizi inceleyeceğiz. İster deneyimli bir geliştirici olun, ister programlama denizine yeni adım atıyor olun, takip etmesi kolay değerli bilgilerle dolu bu öğreticiyi bulacaksınız.
## Ön koşullar
Pivot tablonun kaynak verilerini değiştirme yolculuğumuza başlamadan önce, her şeyin ayarlandığından ve kullanıma hazır olduğundan emin olalım:
1. Visual Studio: Burada kodumuzu yazacağımız için Microsoft Visual Studio'nun bir kopyasının yüklü olduğundan emin olun.
2. Aspose.Cells Kütüphanesi: Projenizde Aspose.Cells kütüphanesini indirip referans göstermeniz gerekir. Bunu indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: Bu eğitim basitleştirilmiş olsa da, C# bilgisine sahip olmak kodu daha iyi anlamanıza yardımcı olacaktır.
4. Excel Dosyası: İçinde işlem yapabileceğimiz bir pivot tablonun bulunduğu örnek bir Excel dosyanız (örneğin "Book1.xlsx") olmalıdır.
Tamam, tüm ön koşullar sağlandıktan sonra gerekli paketleri içe aktarıp kodlamaya başlayabiliriz!
## Paketleri İçe Aktar
İlk önce ilk şeyler—ihtiyacımız olan paketleri içe aktaralım. C# projenizi Visual Studio'da açın ve kod dosyanızın en üstüne aşağıdaki using yönergelerini ekleyin:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Bu ad alanları, Excel dosyalarıyla çalışmak ve Aspose.Cells kullanarak içeriklerini düzenlemek için ihtiyaç duyduğunuz temel sınıflara erişmenizi sağlayacaktır.

Şimdi, süreci yönetilebilir adımlara bölelim. Bir Excel dosyasını açma, çalışma sayfasını değiştirme, pivot tablonun veri kaynağını değiştirme ve sonuçları kaydetme adımlarını ele alacağız.
## Adım 1: Belge Dizininizi Tanımlayın
 Öncelikle Excel dosyanızın nerede bulunduğunu belirtmeniz gerekir.`dataDir` "Book1.xlsx" dosyanızı içeren klasörü işaret eden değişken.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
Bu satır, Excel dosyanızın saklandığı dizini belirler ve daha sonra erişimi kolaylaştırır.
## Adım 2: Giriş Yolunu Belirleyin
Şimdi, giriş Excel dosyanızın tam yolunu belirten bir dize oluşturalım:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Bu, dosya erişiminizi kolaylaştırmaya yardımcı olur; kodunuz boyunca aynı yolu birden çok kez yazmak zorunda kalmazsınız.
## Adım 3: Bir Dosya Akışı Oluşturun
 Şimdi Excel dosyasını açmanın zamanı geldi. Bir tane oluşturacağız`FileStream` Excel dosyasının içeriğini okumanızı sağlar:
```csharp
// Açılacak Excel dosyasını içeren bir dosya akışı oluşturma
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Bu satır dosyayı okuma modunda açar ve verilerine erişmemizi sağlar.
## Adım 4: Çalışma Kitabını Yükleyin
Dosya akışı hazır olduğunda, bir sonraki adım çalışma kitabını yüklemektir:
```csharp
// Excel dosyasını dosya akışı aracılığıyla açma
Workbook workbook = new Workbook(fstream);
```
 Bu komut Excel dosyanızı alır ve onu bir`Workbook` nesne. Yüklendikten sonra, dosyayı gerektiği gibi düzenleyebilirsiniz.
## Adım 5: Çalışma Sayfasına Erişim
Ayrıntılara dalmanın zamanı geldi. Çalışma kitabındaki ilk çalışma sayfasına erişeceğiz:
```csharp
// Excel dosyasındaki ilk çalışma sayfasına erişim
Worksheet worksheet = workbook.Worksheets[0];
```
Bu, ilk çalışma sayfasındaki verilere doğrudan erişmenizi sağlayarak değişiklik yapmayı kolaylaştırır.
## Adım 6: Yeni Verileri Doldurun
Sonra, hücrelere yeni veri eklemek istiyoruz. Bu örnekte, bazı örnek veriler ekleyeceğiz:
```csharp
// Çalışma sayfası hücrelerine yeni veriler dolduruluyor
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Burada "Golf", "Qtr4" değerlerini koyuyoruz ve`7000` belirli hücrelere. Bu değerleri ihtiyaçlarınıza uygun şekilde değiştirebilirsiniz.
## Adım 7: Adlandırılmış Aralığı Değiştirin
Şimdi, pivot tablonun başvurduğu adlandırılmış aralığı değiştireceğiz. Bu, bir aralık oluşturmayı veya güncellemeyi içerir:
```csharp
// "DataSource" adlı aralığı değiştirme
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Yeni bir aralık tanımlayarak, pivot tablonun yenilendiğinde bu yeni verileri kullanmasını sağlarız.
## Adım 8: Değiştirilen Excel Dosyasını Kaydedin
Tüm değişikliklerden sonra çalışmanızı kaydetmeniz çok önemli! Değiştirilen çalışma kitabını kaydedelim:
```csharp
// Değiştirilen Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xls");
```
Bu komut çalışma kitabını yeni bir dosyaya kaydeder, böylece siz istemediğiniz sürece orijinal dosyanızın üzerine yazmazsınız!
## Adım 9: Dosya Akışını Kapatın
Son olarak, kullandığınız kaynakları serbest bırakmak için dosya akışını kapatmanız önemlidir:
```csharp
// Tüm kaynakları serbest bırakmak için dosya akışını kapatıyorum
fstream.Close();
```
Bu adım, uygulamanızın bellek sızdırmamasını ve verimli kalmasını sağlar.
## Çözüm
Tebrikler! .NET'te Aspose.Cells kullanarak bir pivot tablonun kaynak verilerini programatik olarak başarıyla değiştirdiniz. Bu işlevsellik, Excel görevlerini otomatikleştirmek ve iş akışınızı iyileştirmek için birçok olasılık sunar. İster finansal raporları güncelleyin, ister satış verilerini izleyin veya sadece veri kümeleriyle oynayın, bunu programatik olarak yapabilme yeteneği size çok zaman kazandırabilir ve hata riskini azaltabilir.

## SSS
### Aspose.Cells Nedir?
Aspose.Cells, Excel dosyalarıyla çalışmak için güçlü bir .NET kütüphanesidir ve kullanıcıların Excel belgelerini programlı bir şekilde oluşturmalarına, değiştirmelerine ve düzenlemelerine olanak tanır.
### Bu yöntemi kullanarak mevcut pivot tablolarımın kaynak verilerini değiştirebilir miyim?
Kesinlikle! Bu yöntem, Excel çalışma kitabınızdaki mevcut pivot tablolar için veri kaynağını güncellemenize olanak tanır.
### Aspose.Cells'i kullanmak için Office'in yüklü olması gerekir mi?
Hayır! Aspose.Cells bağımsız bir kütüphanedir, yani Excel dosyalarıyla çalışmak için Microsoft Office'in yüklü olmasına ihtiyacınız yoktur.
### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ücretsiz deneme sürümü sunar, ancak tam işlevsellik için bir lisans satın almanız gerekir. Ayrıntıları burada bulabilirsiniz[Burada](https://purchase.aspose.com/buy).
### Daha fazla örnek ve desteği nerede bulabilirim?
 Daha fazla örnek ve destek için şuraya göz atın:[Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) ve onların topluluk forumu[Burada](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
