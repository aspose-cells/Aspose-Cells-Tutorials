---
"description": "Aspose.Cells for .NET kullanarak Excel'de şekillerle metni nasıl döndüreceğinizi öğrenin. Mükemmel Excel sunumu için bu adım adım kılavuzu izleyin."
"linktitle": "Excel'de Şekille Metni Döndürme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Şekille Metni Döndürme"
"url": "/tr/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Şekille Metni Döndürme

## giriiş
Excel dünyasında, görsel temsil, verinin kendisi kadar önemlidir. İster bir rapor hazırlayın ister dinamik bir gösterge paneli tasarlayın, bilgilerin düzenlenme şekli, okunabilirliğini ve genel görünümünü önemli ölçüde etkileyebilir. Peki, hiç metni döndürüp şekillerle şık bir şekilde hizalamak istediniz mi? Şanslısınız! Bu eğitimde, .NET için Aspose.Cells kullanarak şekillerle metni nasıl döndüreceğinizi inceleyeceğiz ve elektronik tablolarınızın yalnızca bilgilendirmekle kalmayıp aynı zamanda etkilemesini sağlayacağız.
## Ön koşullar
Başlamadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1. Visual Studio: Kodumuzu yazacağımız yer olan Visual Studio'nun makinenizde yüklü olduğundan emin olun.
2. .NET için Aspose.Cells: Aspose.Cells kütüphanesine ihtiyacınız olacak. [en son sürümü buradan indirin](https://releases.aspose.com/cells/net/) veya ücretsiz olarak deneyin [ücretsiz deneme](https://releases.aspose.com/).
3. Temel C# Bilgisi: C# ve .NET ortamına aşina olmanız faydalı olacaktır, ancak her adımda size rehberlik edeceğiz.
4. Excel Dosyası: Örnek bir Excel dosyası diyelim `sampleRotateTextWithShapeInsideWorksheet.xlsx`, kodumuzu test etmek için gereklidir. Bu dosyayı kolayca erişebileceğiniz bir dizine koymalısınız.
Her şey hazır mı? Harika! Hadi eğlenceli kısma geçelim.
## Paketleri İçe Aktar
Atılmak için gerekli paketleri projemize aktarmamız gerekiyor. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
### Yeni Bir Proje Oluştur
1. Visual Studio’yu açın.
2. "Yeni proje oluştur" seçeneğini seçin.
3. "Konsol Uygulaması"nı seçin ve tercih ettiğiniz programlama dili olarak C#'ı seçin.
### Aspose.Cells'i yükleyin
Şimdi Aspose.Cells'i projenize ekleyelim. Bunu NuGet Paket Yöneticisi'ni kullanarak yapabilirsiniz:
1. Üst menüden "Araçlar"ı açın.
2. "NuGet Paket Yöneticisi"ni ve ardından "Çözüm için NuGet Paketlerini Yönet"i seçin.
3. "Aspose.Cells" ifadesini arayın.
4. Projenize eklemek için "Yükle"ye tıklayın.
### Yönergeyi Kullanarak Ekle
Ana C# dosyanızın en üstüne aşağıdaki yönergeyi eklemeniz gerekir:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Artık kodlamaya başlamaya hazırız!
İşlemi kolayca sindirilebilir adımlara bölelim. İşte bir Excel dosyasında şekillerle metni döndürme yöntemi:
## Adım 1: Dizin Yollarınızı Ayarlayın
Öncelikle Excel dosyalarınızın saklanacağı kaynak ve çıktı dizinlerinizi ayarlamanız gerekir. İşte nasıl:
```csharp
//Kaynak dizini
string sourceDir = "Your Document Directory"; // Belge dizininizi ayarlayın
//Çıktı dizini
string outputDir = "Your Document Directory"; // Çıkış dizininizi ayarlayın
```
Yer değiştirmek `"Your Document Directory"` gerçek yolunuzla `sampleRotateTextWithShapeInsideWorksheet.xlsx` dosya bulundu.
## Adım 2: Örnek Excel Dosyasını Yükleyin
Şimdi örnek Excel dosyasını yükleyelim. Bu çok önemli çünkü mevcut verileri düzenlemek istiyoruz.
```csharp
//Örnek Excel dosyasını yükleyin.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Adım 3: Çalışma Sayfasına Erişim
Dosya yüklendikten sonra, değiştirmek istediğimiz belirli çalışma sayfasına erişmemiz gerekir. Bizim durumumuzda, bu ilk çalışma sayfasıdır.
```csharp
//İlk çalışma sayfasına erişin.
Worksheet ws = wb.Worksheets[0];
```
## Adım 4: Bir Hücreyi Değiştirin
Sonra, bir mesajı görüntülemek için belirli bir hücreyi değiştireceğiz. Örneğimizde, B4 hücresini kullanacağız.
```csharp
//B4 hücresine erişin ve içine bir mesaj ekleyin.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Bu adım tamamen iletişimle ilgilidir; bu sayfayı açan kişinin neyi değiştirdiğimizi anlamasını sağlamak.
## Adım 5: İlk Şekle Erişim
Metni döndürmek için, üzerinde çalışacağımız bir şekle ihtiyacımız var. Burada, çalışma sayfasındaki ilk şekle erişeceğiz.
```csharp
//İlk şekle erişin.
Shape sh = ws.Shapes[0];
```
## Adım 6: Şekil Metin Hizalamasını Ayarlayın
İşte sihir burada gerçekleşiyor. Şeklin metin hizalama özelliklerini ayarlayacağız.
```csharp
//Şekil metin hizalamasına erişin.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//RotateTextWithShape'i false olarak ayarlayarak şekli olan metni döndürmeyin.
shapeTextAlignment.RotateTextWithShape = false;
```
Ayarlayarak `RotateTextWithShape` false olarak ayarlayarak metnin dik kalmasını ve şekille birlikte dönmemesini sağlıyoruz, böylece her şey temiz ve düzenli kalıyor.
## Adım 7: Çıktı Excel Dosyasını Kaydedin
Son olarak, değişikliklerimizi yeni bir Excel dosyasına kaydedelim. Bu, düzenlemelerimizi kaybetmememizi ve düzenli bir çıktıya sahip olmamızı sağlar.
```csharp
//Çıktı Excel dosyasını kaydedin.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Ve işte bu kadar! Çıktı dosyanız artık kaydedildi, B4 hücresindeki metin ve şekle yapılan ayarlamalar dahil.
## Adım 8: Kodu Çalıştırın
Senin içinde `Main` yöntemini kullanın, yukarıdaki tüm kod parçacıklarını sarın ve projenizi çalıştırın. Değişikliklerin çıktı dosyanıza yansıdığını görün!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Çözüm
Aspose.Cells for .NET kullanarak Excel'de şekillerle metni döndürmek ilk başta ayrıntılı bir işlem gibi görünebilir, ancak parçalara ayırdığınızda oldukça basittir. Bu basit adımları izleyerek, elektronik tablolarınızı daha profesyonel ve görsel olarak çekici görünecek şekilde özelleştirebilirsiniz. Şimdi, bunu bir müşteri veya kişisel projeleriniz için yapıyor olun, herkes işinizin kalitesinden övgüyle bahsedecek!
## SSS
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet! Şunu kullanabilirsiniz: [ücretsiz deneme](https://releases.aspose.com/) Kütüphaneyi denemek için.
### Aspose.Cells hangi Excel sürümlerini destekliyor?
Aspose.Cells, XLS, XLSX, CSV ve daha fazlası dahil olmak üzere çeşitli Excel formatlarını destekler.
### Excel'in eski sürümlerinde şekiller içeren metni döndürmek mümkün müdür?
Evet, bu işlevsellik Aspose.Cells tarafından desteklenen eski formatlara uygulanabilir.
### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?
Kapsamlı içeriği keşfedebilirsiniz [belgeleme](https://reference.aspose.com/cells/net/) Daha fazla bilgi için.
### Aspose.Cells için desteği nasıl alabilirim?
Destek almak için şu adresi ziyaret edebilirsiniz: [Aspose forumu](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}