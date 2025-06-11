---
"description": "Aspose.Cells for .NET kullanarak Excel'de şekillerin öne veya arkaya nasıl gönderileceğini keşfedin. Bu kılavuz, ipuçlarıyla adım adım bir eğitim sağlar."
"linktitle": "Excel'de Şekli Öne veya Arkaya Gönder"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Şekli Öne veya Arkaya Gönder"
"url": "/tr/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Şekli Öne veya Arkaya Gönder

## giriiş
Excel dosyalarıyla çalışırken, elektronik tablonuzdaki görsel öğeler üzerinde daha fazla kontrole ihtiyaç duyabilirsiniz. Resimler ve grafikler gibi şekiller de verilerinizin sunumunu geliştirebilir. Peki bu şekiller üst üste geldiğinde veya yeniden sıralanması gerektiğinde ne olur? İşte .NET için Aspose.Cells'in parladığı yer burasıdır. Bu eğitimde, bir Excel çalışma sayfasındaki şekilleri işleme adımlarında size yol göstereceğiz, özellikle şekilleri diğer şekillerin önüne veya arkasına göndereceğiz. Excel oyununuzu geliştirmeye hazırsanız, hemen başlayalım!
## Ön koşullar
Başlamadan önce birkaç şeyin hazır olması gerekir:
1. Aspose.Cells Kütüphanesinin Kurulumu: .NET için Aspose.Cells kütüphanesinin kurulu olduğundan emin olun. Bunu bulabilirsiniz [Burada](https://releases.aspose.com/cells/net/).
2. Geliştirme Ortamı: Visual Studio gibi .NET desteği olan bir geliştirme ortamınız olduğundan emin olun.
3. Temel C# Bilgisi: C# programlamaya aşina olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
Tamam, ön koşullar listesindeki tüm kutuları işaretlediniz mi? Harika! Hadi eğlenceli kısma geçelim - biraz kod yazmak!
## Paketleri İçe Aktar
Gerçek kodlamaya dalmadan önce, gerekli paketleri içe aktaralım. Sadece C# dosyanızın en üstüne aşağıdaki using yönergesini ekleyin:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Bu ad alanları, Excel dosyalarını ve şekillerini düzenlemek için kullanacağımız sınıfları ve yöntemleri içerdiğinden önemlidir.
## Adım 1: Dosya Yollarınızı Tanımlayın
Bu ilk adımda kaynak ve çıktı dizinlerini belirlememiz gerekiyor. Excel dosyanızın bulunduğu ve değiştirilmiş dosyayı kaydetmek istediğiniz yer burasıdır.
```csharp
//Kaynak dizini
string sourceDir = "Your Document Directory";
//Çıktı dizini
string outputDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` Excel dosyalarınızın saklandığı gerçek yol ile.
## Adım 2: Çalışma Kitabını Yükleyin
Artık dizinlerimizi ayarladığımıza göre, üzerinde değişiklik yapmak istediğimiz şekilleri içeren çalışma kitabını (Excel dosyasını) yükleyelim.
```csharp
//Kaynak Excel dosyasını yükle
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Bu kod satırı yeni bir başlatır `Workbook` nesnesi, belirtilen Excel dosyasını belleğe yükleyerek üzerinde çalışmamızı sağlar.
## Adım 3: Çalışma Sayfasına Erişim 
Sonra, şekillerimizin bulunduğu belirli çalışma sayfasına erişmemiz gerekiyor. Bu örnek için ilk çalışma sayfasını kullanacağız.
```csharp
//İlk çalışma sayfasına erişin
Worksheet ws = wb.Worksheets[0];
```
Referans vererek `Worksheets[0]`, çalışma kitabımızın ilk sayfasını hedefliyoruz. Şekilleriniz farklı bir sayfadaysa, dizini buna göre ayarlayın.
## Adım 4: Şekillere Erişim
Çalışma kağıdına erişimimiz hazır olduğuna göre, ilgilendiğimiz şekilleri alalım. Bu örnek için, birinci ve dördüncü şekillere erişeceğiz.
```csharp
//Birinci ve dördüncü şekle erişin
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Bu çizgiler, indekslerine göre çalışma kağıdından belirli şekilleri alırlar.
## Adım 5: Şekillerin Z-Sıralama Pozisyonunu Yazdırın
Herhangi bir şekli hareket ettirmeden önce, mevcut Z-Sırası konumlarını yazdıralım. Bu, değişiklik yapmadan önce konumlarını takip etmemize yardımcı olur.
```csharp
//Şeklin Z-Sıra konumunu yazdır
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Arayarak `ZOrderPosition`, her şeklin çizim sırasında nerede durduğunu görebiliriz.
## Adım 6: İlk Şekli Öne Gönderin
Şimdi harekete geçme zamanı! İlk şekli Z-Order'ın önüne gönderelim.
```csharp
//Bu şekli öne gönder
sh1.ToFrontOrBack(2);
```
Geçerek `2` ile `ToFrontOrBack`, Aspose.Cells'e bu şekli öne getirmesini söylüyoruz. 
## Adım 7: İkinci Şeklin Z-Sıra Pozisyonunu Yazdırın
İkinci şekli arkaya göndermeden önce nerede konumlandığına bir bakalım.
```csharp
//Şeklin Z-Sıra konumunu yazdır
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Bu, herhangi bir değişiklik yapmadan önce dördüncü şeklin konumuna dair bize fikir verir.
## Adım 8: Dördüncü Şekli Arkaya Gönderin
Son olarak dördüncü şekli Z-Order yığınının sonuna göndereceğiz.
```csharp
//Bu şekli arkaya gönder
sh4.ToFrontOrBack(-2);
```
Kullanarak `-2` parametre şekli yığının arkasına gönderdiğinden, diğer şekilleri veya metni engellemeyeceğinden emin olur.
## Adım 9: Çalışma Kitabını Kaydedin 
Son adım, çalışma kitabınızı yeni konumlandırılmış şekillerle kaydetmektir.
```csharp
//Çıktı Excel dosyasını kaydedin
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Bu komut, değiştirilen çalışma kitabını belirtilen çıktı dizinine kaydeder.
## Adım 10: Onay Mesajı
Son olarak görevimizin başarıyla tamamlandığını bize bildiren basit bir onay verelim.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Ve böylece eğitimimizin kodu tamamlanmış oldu!
## Çözüm
Aspose.Cells for .NET kullanarak Excel'deki şekilleri düzenlemek yalnızca basit değil, aynı zamanda güçlüdür. Bu kılavuzu izleyerek artık şekilleri kolayca öne veya arkaya gönderebilmeli ve Excel sunumlarınız üzerinde daha iyi kontrol sağlamalısınız. Bu araçlar elinizin altında olduğunda, elektronik tablolarınızın görsel çekiciliğini artırmaya hazırsınız.
## SSS
### Aspose.Cells için hangi programlama diline ihtiyacım var?  
Aspose.Cells ile çalışmak için C# veya .NET destekli herhangi bir dili kullanmanız gerekir.
### Aspose.Cells'i ücretsiz deneyebilir miyim?  
Evet, Aspose.Cells'in ücretsiz deneme sürümüne başlayabilirsiniz [Burada](https://releases.aspose.com/).
### Excel'de hangi şekilleri işleyebilirim?  
Dikdörtgenler, daireler, çizgiler ve resimler gibi çeşitli şekilleri işleyebilirsiniz.
### Aspose.Cells için nasıl destek alabilirim?  
Herhangi bir destek veya soru için topluluk forumlarını ziyaret edebilirsiniz. [Burada](https://forum.aspose.com/c/cells/9).
### Aspose.Cells için geçici bir lisans mevcut mu?  
Evet, geçici lisans talebinde bulunabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}