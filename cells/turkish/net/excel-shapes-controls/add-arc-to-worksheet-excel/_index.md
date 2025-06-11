---
"description": "Aspose.Cells for .NET kullanarak Excel çalışma sayfalarına yay eklemeyi öğrenin. Elektronik tablo tasarımlarınızı geliştirmek için adım adım kılavuzumuzu izleyin."
"linktitle": "Excel'de Çalışma Sayfasına Yay Ekleme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Çalışma Sayfasına Yay Ekleme"
"url": "/tr/net/excel-shapes-controls/add-arc-to-worksheet-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Yay Ekleme

## giriiş
Görsel olarak çekici Excel elektronik tabloları oluşturmak veri sunumu için çok önemlidir ve Aspose.Cells kitaplığı geliştiricilere bu görevi başarmaları için sağlam araçlar sunar. Excel belgelerinize dahil etmek isteyebileceğiniz ilginç bir özellik, yaylar gibi şekiller ekleme yeteneğidir. Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel çalışma sayfasına adım adım yay eklemeyi ele alacağız. Bu makalenin sonunda, yalnızca yay eklemeyi öğrenmekle kalmayacak, aynı zamanda genel olarak şekilleri yönetme konusunda da fikir sahibi olacaksınız.
## Ön koşullar
Çalışma sayfanıza yay eklemenin inceliklerine dalmadan önce, birkaç şeyin yerli yerinde olduğundan emin olmanız önemlidir. Başlamak için ihtiyaç duyacağınız ön koşullar şunlardır:
1. Visual Studio: Programlama dilimiz olarak C# kullanacağımız için bilgisayarınızda Visual Studio'nun yüklü olması gerekiyor.
2. .NET Framework: .NET Framework veya .NET Core'un yüklü olduğundan emin olun. Aspose.Cells her ikisini de destekler.
3. .NET için Aspose.Cells: Aspose.Cells kütüphanesine sahip olmanız gerekir. Bunu şuradan indirebilirsiniz: [Aspose.Cells İndirmeleri](https://releases.aspose.com/cells/net/) sayfa.
4. C# Temel Anlayışı: C#'a aşina olmak, kod parçacıklarını fazla uğraşmadan takip etmenize yardımcı olacaktır.
## Paketleri İçe Aktar
Projenizde Aspose.Cells ile çalışmaya başlamak için gerekli paketleri içe aktarmanız gerekir. İşte nasıl yapacağınız:
### Yeni Bir Proje Oluştur
- Visual Studio’yu açın.
- "Yeni proje oluştur" seçeneğini seçin.
- .NET ile çalışan bir şablon seçin (örneğin Konsol Uygulaması).
  
### Aspose.Cells Referanslarını Ekle
- Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
- "NuGet Paketlerini Yönet" seçeneğini seçin.
- “Aspose.Cells”i arayın ve yükleyin.
Artık arc eklemeyi kodlamaya başlamaya hazırsınız.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
İşte Excel'de bir çalışma sayfasına yayların nasıl ekleneceğini gösteren kodun adım adım dökümü.
## Adım 1: Dizini Ayarlama
İlk adım Excel dosyanızı kaydedeceğiniz bir dizin oluşturmaktır. Bu, çıktı dosyalarınızı kolayca yönetmenize yardımcı olur.
```csharp
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu kod parçasında, belge dizinine giden yolu belirtiyoruz. Ayrıca dizinin var olup olmadığını da kontrol ediyoruz; yoksa, onu oluşturuyoruz. Bu, çıktımızın temelini oluşturuyor.
## Adım 2: Bir Çalışma Kitabı Oluşturun
Şimdi yeni bir çalışma kitabı örneği oluşturalım.
```csharp
// Yeni bir Çalışma Kitabı örneği oluşturun.
Workbook excelbook = new Workbook();
```
Bu satır yeni bir Excel çalışma kitabı oluşturur. Bunu şekiller, veriler ve daha fazlasını ekleyebileceğimiz boş bir tuval olarak düşünün.
## Adım 3: İlk Yay Şeklini Ekleyin
Şimdi çalışma kağıdımıza ilk yay şeklimizi ekleyelim.
```csharp
// Bir yay şekli ekleyin.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Burada, ilk çalışma sayfasına bir yay ekliyoruz. Parametreler, yayın konumunu ve boyutunu tanımlar: `(left, top, width, height, startAngle, endAngle)`. Bir dairenin parçasını çizmek gibi!
## Adım 4: İlk Arkı Özelleştirin
Yayı ekledikten sonra görünümünü özelleştirmek isteyebilirsiniz.
```csharp
// Dolgu şekli rengini ayarlayın
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Yayın yerleşimini ayarlayın.
arc1.Placement = PlacementType.FreeFloating;           
// Çizgi kalınlığını ayarlayın.
arc1.Line.Weight = 1;      
// Yayın çizgi stilini ayarlayın.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Bu bölümde, yayı özelleştiriyoruz. Dolgu türünü düz renge (bu durumda mavi) ayarlıyoruz, nasıl yerleştirileceğini tanımlıyoruz, çizgi kalınlığını belirliyoruz ve bir çizgi stili seçiyoruz. Temel olarak, yayımızı görsel olarak çekici hale getirmek için giydiriyoruz!
## Adım 5: İkinci Bir Yay Şekli Ekleyin
Daha fazla bağlam sağlamak için başka bir yay şekli ekleyelim.
```csharp
// Başka bir yay şekli ekleyin.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
İlk yaya benzer şekilde, aynı çalışma sayfasına ikinci bir yay ekliyoruz. Buradaki koordinatlar, farklı şekilde konumlandırılması için biraz kaydırıldı.
## Adım 6: İkinci Yayı Özelleştirin
İlk yayda yaptığımız gibi ikinci yayda da özelleştirme yapacağız.
```csharp
// Çizgi rengini ayarlayın
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Yayın yerleşimini ayarlayın.
arc2.Placement = PlacementType.FreeFloating;          
// Çizgi kalınlığını ayarlayın.
arc2.Line.Weight = 1;           
// Yayın çizgi stilini ayarlayın.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Burada, ikinci yaya birincisiyle aynı stili veriyoruz. Benzersizlik veya tematik amaçlar için istediğiniz gibi rengi veya stili değiştirebilirsiniz.
## Adım 7: Çalışma Kitabını Kaydedin
Son olarak yeni oluşturduğunuz çalışma kitabını yaylarla birlikte kaydetmenin zamanı geldi.
```csharp
// Excel dosyasını kaydedin.
excelbook.Save(dataDir + "book1.out.xls");
```
Bu satır, kaydet düğmesine basmak gibi çalışır. Çalışmamızı belirtilen konuma, belirlenmiş bir dosya adıyla kaydediyoruz. Başyapıtınızı Excel formatında görmek için dizininizi kontrol ettiğinizden emin olun!
## Çözüm
Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel çalışma sayfasına yay şekilleri ekleme sürecini inceledik. Basit bir adım adım kılavuz aracılığıyla, yeni bir çalışma kitabı oluşturmayı, yaylar eklemeyi, görünümlerini özelleştirmeyi ve belgenizi kaydetmeyi öğrendiniz. Bu özellik yalnızca elektronik tablolarınızın görsel çekiciliğini artırmakla kalmaz, aynı zamanda veri sunumlarınızı daha bilgilendirici hale getirir. İster grafikler, raporlar oluşturun, ister sadece denemeler yapın, yaylar gibi şekiller kullanmak projelerinize yaratıcı bir dokunuş katabilir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Microsoft Excel'e ihtiyaç duymadan Excel dosyalarını programlı bir şekilde oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan güçlü bir kütüphanedir.
### Aspose.Cells'i kullanmak için Microsoft Excel'i yüklemem gerekiyor mu?
Hayır, Aspose.Cells tamamen bağımsızdır ve Microsoft Excel'in kurulu olmasını gerektirmez.
### Aspose.Cells'i ücretsiz deneyebilir miyim?
Evet, Aspose.Cells'i kullanarak deneyebilirsiniz [Ücretsiz Deneme](https://releases.aspose.com/).
### Aspose.Cells hangi programlama dillerini destekliyor?
Aspose.Cells, C#, VB.NET ve daha fazlası dahil olmak üzere birden fazla dili destekler.
### Aspose.Cells için desteği nereden alabilirim?
Destek almak için: [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}