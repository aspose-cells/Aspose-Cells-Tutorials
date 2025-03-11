---
title: Bağlantı Noktalarıyla Ark Kontrolü Ekleyin
linktitle: Bağlantı Noktalarıyla Ark Kontrolü Ekleyin
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu ayrıntılı kılavuzda, Aspose.Cells for .NET kullanarak bağlantı noktalarıyla yay denetimlerinin nasıl ekleneceğini öğrenin.
weight: 27
url: /tr/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bağlantı Noktalarıyla Ark Kontrolü Ekleyin

## giriiş
Görsel olarak ilgi çekici Excel raporları oluşturmaya gelince, çizimler hayati bir rol oynar. İster finansal bir rapor, ister bir proje dökümü hazırlıyor olun, yaylar gibi şekiller kullanmak veri sunumunuza derinlik ve netlik katabilir. Bugün, Excel çalışma sayfalarınıza bağlantı noktalarıyla yay denetimleri eklemek için Aspose.Cells for .NET'i nasıl kullanacağınızı derinlemesine inceliyoruz. Dolayısıyla, elektronik tablolarınızı nasıl renklendireceğinizi veya verilerinizi nasıl şarkı söyleteceğinizi merak ettiyseniz, okumaya devam edin!
## Ön koşullar
Kodlamanın heyecanına dalmadan önce, her şeyin hazır olduğundan emin olalım. İhtiyacınız olanlar şunlar:
1. .NET Framework: Uyumlu bir sürümün yüklü olduğundan emin olun. Aspose.Cells, .NET Core dahil olmak üzere birden fazla sürümle çalışır.
2.  .NET için Aspose.Cells: Aspose.Cells kütüphanesini indirip yüklemeniz gerekecek. Bunu şuradan kolayca alabilirsiniz:[indirme bağlantısı](https://releases.aspose.com/cells/net/).
3. İyi Bir IDE: Her .NET geliştiricisinin sadık dostu Visual Studio, kodlama deneyiminizi kolaylaştırmaya yardımcı olacak.
4. Temel C# Bilgisi: Eğer C# konusunda bilginiz varsa, bu eğitimi rahatlıkla takip edebilirsiniz.
5. Belge Dizininize Erişim: Excel dosyalarınızı nereye kaydedeceğinizi bilin. Çıktınızı verimli bir şekilde düzenlemek için önemlidir.
## Paketleri İçe Aktar
Bir sonraki adım, projenize doğru paketlerin aktarıldığından emin olmaktır. .NET için Aspose.Cells çeşitli işlevlere sahiptir, bu yüzden basit tutacağız. Dahil etmeniz gerekenler şunlardır:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Bu ad alanları, bu kılavuzda kullanacağınız tüm çizim özelliklerine ve hücre yönetimi işlevlerine erişmenizi sağlayacaktır.
## Adım 1: Belge Dizininizi Ayarlayın
İlk önce ilk şeyler—parlak yeni Excel dosyalarını kaydedeceğiniz bir dizin oluşturalım. Bunu nasıl yaptığımızı anlatalım:
```csharp
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu kod parçası belirtilen klasörünüzün var olup olmadığını kontrol eder. Yoksa bir tane oluşturur. Basit, değil mi? Karmaşayı önlemek için dosyalarınız için her zaman belirli bir yer olması iyidir.
## Adım 2: Bir Çalışma Kitabı Oluşturun
Artık dizinimiz hazır olduğuna göre yeni bir Excel çalışma kitabı oluşturalım.
```csharp
Workbook excelbook = new Workbook();
```
 Arayarak`Workbook` constructor'ı kullandığınızda, aslında şunu söylüyorsunuz: "Hey, yeni bir Excel dosyası başlatalım!" Bu, tüm şekilleriniz ve verileriniz için bir tuval olacaktır.
## Adım 3: İlk Yay Şeklini Ekleme
Eğlence burada başlıyor! İlk yay şeklimizi ekleyelim.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Bu kod satırı ilk çalışma sayfasına bir yay şekli ekler. Parametreler, yayın koordinatlarını ve eğriliğini tanımlayan açıları belirtir. 
## Adım 4: Arc'ın Görünümünü Özelleştirin
Boş bir yay şekli, boyasız bir tuval gibidir; biraz gösteriş gerektirir!
### Ark Dolgu Rengini Ayarla
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Bu, yayı düz mavi yapar. Rengi istediğiniz herhangi bir tona değiştirerek değiştirebilirsiniz.`Color.Blue` başka bir renk için.
### Ark Yerleşimini Ayarla
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Yerleşimi "Serbest Yüzen" olarak ayarlamak, yayın hücre sınırlarından bağımsız olarak hareket etmesini sağlayarak konumlandırmada esneklik sağlar.
### Çizgi Kalınlığını ve Stilini Ayarla
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Burada çizginin ağırlığını ve stilini tanımlayarak onu daha belirgin ve görsel olarak çekici hale getirebilirsiniz.
## Adım 5: Başka Bir Yay Şekli Ekleme
Neden bir taneyle yetinelim? Excel görselimizi zenginleştirmek için bir yay şekli daha ekleyelim.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
İlk yay gibi bu da farklı bir konuma ekleniyor; tasarımın sihrinin gerçekleştiği yer burası!
## Adım 6: İkinci Yayı Özelleştirin
İkinci hikayemize de biraz kişilik katalım!
### Yay Çizgisi Rengini Değiştir
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Biz mavi renkle tutarlılığımızı koruduk, ancak siz her zaman tasarımınıza en uygun olanı görmek için karıştırıp eşleştirebilirsiniz!
### İlk Ark'a Benzer Özellikleri Ayarla
Bu estetik tercihleri tekrarladığınızdan emin olun:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Burada yapmanız gereken tek şey, ikinci yayın birincisiyle uyumlu olmasını sağlayarak çalışma sayfanız boyunca tutarlı bir görünüm yaratmaktır.
## Adım 7: Çalışma Kitabınızı Kaydedin
Hiçbir şaheser kaydedilmeden tamamlanmış sayılmaz, değil mi? Arklarınızı bir Excel dosyasına yazmanın zamanı geldi.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Bu satır, yeni oluşturduğunuz yayları belirlediğiniz dizindeki "book1.out.xls" adlı bir Excel dosyasına kaydeder.
## Çözüm
Tebrikler! Aspose.Cells for .NET kullanarak Excel sayfalarınıza bağlantı noktalarıyla yay denetimleri eklemenin temellerini yeni öğrendiniz. Bu işlevsellik yalnızca elektronik tablolarınızı güzelleştirmekle kalmaz, aynı zamanda karmaşık verileri daha kolay sindirilebilir hale getirebilir. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, bu görsel öğeler raporlarınızı sıradanlıktan görkemliliğe dönüştürebilir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla oluşturmalarına ve düzenlemelerine olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet! Ücretsiz denemeyi deneyebilirsiniz. Ziyaret edin[bu bağlantı](https://releases.aspose.com/) başlamak için.
### Yayların dışında başka şekiller nasıl eklerim?
Dikdörtgenler, daireler ve daha fazlası gibi çeşitli şekiller eklemek için Aspose.Cells.Drawing ad alanında bulunan farklı sınıfları kullanabilirsiniz.
### Aspose.Cells ile hangi tür dosyalar oluşturabilirim?
XLS, XLSX, CSV ve daha fazlası dahil olmak üzere çeşitli Excel formatlarını oluşturabilir ve düzenleyebilirsiniz.
### Aspose.Cells için teknik destek mevcut mu?
 Kesinlikle! Şuraya erişebilirsiniz:[Aspose destek forumu](https://forum.aspose.com/c/cells/9) yardım için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
