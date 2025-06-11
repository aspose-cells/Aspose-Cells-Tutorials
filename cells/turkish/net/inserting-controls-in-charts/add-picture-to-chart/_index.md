---
"description": "Aspose.Cells for .NET kullanarak Excel grafiklerine kolayca resim eklemeyi öğrenin. Grafiklerinizi ve sunumlarınızı sadece birkaç basit adımda geliştirin."
"linktitle": "Tabloya Resim Ekle"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Tabloya Resim Ekle"
"url": "/tr/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tabloya Resim Ekle

## giriiş

Kişisel bir dokunuştan yoksun sıkıcı grafiklerden bıktınız mı? Excel görsellerinizi resim ekleyerek nasıl renklendireceğinizi öğrenmek mi istiyorsunuz? Şanslısınız! Bu eğitimde, .NET için Aspose.Cells dünyasına dalacağız ve Excel'de grafiklere resim eklemeyi öğreneceğiz. O halde en sevdiğiniz fincan kahvenizi alın ve başlayalım!

## Ön koşullar

Kodlamanın inceliklerine dalmadan önce, sorunsuz bir şekilde ilerleyebilmeniz için sahip olmanız gereken birkaç ön koşul vardır:

- Visual Studio: .NET kodunuzu yazacağınız ve çalıştıracağınız yer burasıdır. Yüklü olduğundan emin olun.
- Aspose.Cells for .NET: Excel dosyalarıyla çalışmak için bu kütüphaneye ihtiyacınız olacak. [buradan indirin](https://releases.aspose.com/cells/net/).
- C#'ın Temel Anlayışı: Kod boyunca size rehberlik edeceğim, ancak C# temellerine hakim olmak işleri daha net hale getirecektir.

### Kurulum Adımları

1. Aspose.Cells'i yükleyin: NuGet Paket Yöneticisi aracılığıyla Visual Studio projenize Aspose.Cells ekleyebilirsiniz. Bunu Araçlar > NuGet Paket Yöneticisi > Çözüm için NuGet Paketlerini Yönet'e giderek ve “Aspose.Cells”i arayarak yapın. Yükle'ye tıklayın.
2. Projenizi Kurma: Visual Studio'da yeni bir C# konsol uygulaması projesi oluşturun.

## Paketleri İçe Aktar

Her şeyi ayarladıktan sonraki adım, gerekli paketleri projenize aktarmaktır. İşte nasıl yapacağınız:

### Gerekli Ad Alanlarını İçe Aktar

C# kod dosyanızın en üstüne aşağıdaki ad alanlarını içe aktarmanız gerekir:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Bu, programınıza "Hey! Aspose.Cells'in bu harika özelliklerini kullanacağım." der.

Artık ön koşullarımız hazır olduğuna göre, süreci küçük adımlara bölelim. 

## Adım 1: Dizinlerinizi Tanımlayın

İlk önce, giriş ve çıkış dosyalarımız için yolları ayarlamamız gerekiyor. Bu adım çok önemli çünkü mevcut Excel dosyamızı nerede bulacağımızı ve değiştirilen dosyayı nereye kaydedeceğimizi bilmemiz gerekiyor.

```csharp
//Kaynak dizini
string sourceDir = "Your Document Directory/";

//Çıktı dizini
string outputDir = "Your Output Directory/";
```

Yer değiştirmek `Your Document Directory` Ve `Your Output Directory` Bilgisayarınızdaki gerçek yollarla. 

## Adım 2: Mevcut Çalışma Kitabını Yükleyin

Şimdi resmimizi grafiğe eklemek istediğimiz mevcut Excel dosyasını yükleyelim.

```csharp
// Mevcut dosyayı açın.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Bu kod çalışma kitabını açar ve düzenlemeye hazır hale getirir.

## Adım 3: Görüntü Akışını Hazırlayın

Resmi eklemeden önce, grafiğe eklemek istediğimiz resmi okumamız gerekiyor. 

```csharp
// Akışa bir görüntü dosyası alın.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Resmin belirtilen dizine kaydedildiğinden emin olun.

## Adım 4: Grafiği Hedefleyin

Şimdi, resmimizi hangi grafiğe ekleyeceğimizi belirtelim. Bu örnekte, ilk çalışma sayfasındaki ilk grafiğe odaklanacağız.

```csharp
// İkinci sayfadaki tasarımcı şemasını alın.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

İstediğiniz çalışma sayfasına indeksi değiştirerek ulaşabilirsiniz.

## Adım 5: Resmi Tabloya Ekleyin

Tabloyu seçtikten sonra sıra geldi resmi eklemeye! 

```csharp
// Tabloya yeni bir resim ekleyin.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Burada, `50` Ve `50` görüntünün yerleştirileceği X ve Y koordinatlarıdır ve `200` resmin genişliği ve yüksekliğidir.

## Adım 6: Resmin Çizgi Formatını Özelleştirin

Resminize biraz hava katmak mı istiyorsunuz? Kenarlığını özelleştirebilirsiniz! İşte nasıl yapacağınız:

```csharp
// Resmin çizgi format türünü alın.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Çizgi stilini ayarlayın.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Çizgi kalınlığını ayarlayın.
lineformat.Weight = 4;    
```

Bu kod parçası, kenarlığın nasıl görüneceğini ve ne kadar kalın olacağını seçmenize olanak tanır. Sunumunuzla uyumlu herhangi bir stili seçin!

## Adım 7: Değiştirilen Çalışma Kitabını Kaydedin

Tüm bu sıkı çalışmalardan sonra, aşağıdaki kod satırını çalıştırarak değişikliklerinizi kaydedelim:

```csharp
// Excel dosyasını kaydedin.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Artık resminiz grafiğe başarıyla entegre edildi ve çıktı dosyanız görüntülenmeye hazır!

## Adım 8: Başarılı Olduğunu Göster

Son olarak, işleminizin başarılı olduğunu doğrulamak için basit bir mesaj ekleyebilirsiniz:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Çözüm

Bu eğitimde, Aspose.Cells for .NET kullanarak resimler ekleyerek Excel grafiklerinize biraz kişilik katmanın yollarını inceledik. Sadece birkaç basit adımla, sunumlarınızı sıradanlıktan unutulmazlığa yükseltebilirsiniz. Öyleyse, ne bekliyorsunuz? Bir deneyin ve grafiklerinizin parlamasına izin verin!

## SSS

### Tek bir tabloya birden fazla resim ekleyebilir miyim?
Evet! arayabilirsiniz `AddPictureInChart` İstediğiniz kadar resim eklemek için yöntemi birden fazla kez deneyin.

### Aspose.Cells hangi görüntü formatlarını destekliyor?
Aspose.Cells PNG, JPEG, BMP ve GIF dahil olmak üzere çeşitli resim formatlarını destekler.

### Resmin konumunu özelleştirebilir miyim?
Kesinlikle! X ve Y koordinatları `AddPictureInChart` yöntem hassas konumlandırmaya izin verir.

### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ücretsiz deneme sunuyor ancak tüm özellikler için lisans gerekiyor. Fiyatlandırmayı bulabilirsiniz [Burada](https://purchase.aspose.com/buy).

### Daha fazla örneği nerede bulabilirim?
Şuna bir göz atın: [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Daha detaylı örnekler ve işlevler için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}