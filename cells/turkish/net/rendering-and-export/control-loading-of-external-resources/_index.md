---
"description": "Aspose.Cells for .NET'i kullanarak Excel'den PDF'e dönüştürmede harici kaynakların nasıl kontrol edileceğini kolay takip edilebilir kılavuzumuzla öğrenin."
"linktitle": "Aspose.Cells'de Excel'deki Harici Kaynakları PDF'ye Dönüştürme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Aspose.Cells'de Excel'deki Harici Kaynakları PDF'ye Dönüştürme"
"url": "/tr/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells'de Excel'deki Harici Kaynakları PDF'ye Dönüştürme

## giriiş
Günümüzün dijital çağında, Excel elektronik tablolarını PDF belgelerine dönüştürmek yaygın bir görevdir. İster raporlar, ister finansal veriler veya sunum materyalleri hazırlıyor olun, PDF'lerinizin tam olarak istediğiniz gibi görünmesini sağlamak istersiniz. .NET için Aspose.Cells, özellikle Excel dosyalarınıza eşlik eden resimler gibi harici kaynakları işlerken bu dönüştürme sürecini en ince ayrıntısına kadar kontrol etmenizi sağlayan sağlam bir kütüphanedir. Bu kılavuzda, Aspose.Cells kullanarak Excel'den PDF'ye dönüştürme işlemi sırasında harici kaynakları nasıl kontrol edeceğinizi ele alacağız. O halde en sevdiğiniz içeceği alın ve başlayalım!
## Ön koşullar
Ayrıntılara girmeden önce, harekete geçmek için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım. İşte hızlı bir kontrol listesi:
1. Visual Studio veya herhangi bir .NET uyumlu IDE: Kodunuzu yazıp test edebileceğiniz bir ortama ihtiyacınız olacak.
2. .NET için Aspose.Cells: Henüz yüklemediyseniz, şuraya gidin: [Aspose İndirmeleri](https://releases.aspose.com/cells/net/) sayfasına gidin ve en son sürümü edinin.
3. C# Temel Bilgisi: C# programlama diline aşinalık faydalı olacaktır. Herhangi bir kavramdan emin değilseniz, bunları araştırmaktan çekinmeyin.
4. Örnek Bir Excel Dosyası: Dönüştürmek istediğiniz herhangi bir dış kaynakla bir Excel dosyası hazırlayın. Sağlanan örnek dosyayı "samplePdfSaveOptions_StreamProvider.xlsx" kullanabilirsiniz.
5. Test için Bir Görüntü Dosyası: Bu, dönüştürme sırasında harici bir kaynak olarak kullanılacaktır. "newPdfSaveOptions_StreamProvider.png" görüntü dosyası iyi bir yer tutucudur.
## Paketleri İçe Aktar
Başlamak için, Aspose.Cells kütüphanesinden gerekli ad alanlarını içe aktarmanız gerekir. Bu, işlevlerine erişmek için önemlidir. Dosyanızın en üstüne aşağıdaki using yönergelerini eklediğinizden emin olun:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Bu paketler, görevlerinizi yerine getirmek için ihtiyaç duyacağınız tüm temel dersleri ve yöntemleri sağlayacaktır.
## Adım 1: Akış Sağlayıcı Sınıfınızı Oluşturun
Yapılacak ilk iş, akış sağlayıcı sınıfını oluşturmaktır. `IStreamProvider` arayüz. Bu sınıf, harici kaynakların nasıl yükleneceğini kontrol etmenize olanak tanır.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Yeni görüntüyü bir bellek akışında okuyun ve onu Akış özelliğine atayın
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
Bu sınıfta:
- CloseStream: Bu yöntem, akış kapatıldığında çağrılacaktır. Şimdilik, yalnızca izleme için bir hata ayıklama mesajı yazıyoruz.
- InitStream: Sihir burada başlıyor. Burada, harici görüntünüzü bir bayt dizisi olarak okuyacak, onu bir bellek akışına dönüştürecek ve onu `options.Stream` mülk.
## Adım 2: Kaynak ve Çıktı Dizinlerini Ayarlayın
Artık akış sağlayıcınız hazır olduğuna göre, Excel dosyanızın nerede bulunduğunu ve PDF'inizi nereye kaydetmek istediğinizi belirlemenin zamanı geldi.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// Çıktı dizini
string outputDir = "Your Document Directory";
```
Basitçe değiştirin `"Your Document Directory"` Bilgisayarınızda dosyalarınızın bulunduğu gerçek yol ile. Dosyalarınızı düzenli tutmak çok önemlidir!
## Adım 3: Excel Dosyanızı Yükleyin
Daha sonra PDF'ini oluşturmak istediğiniz Excel dosyasını yükleyeceksiniz.
```csharp
// Harici görseller içeren kaynak Excel dosyasını yükleyin
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Biz kullanıyoruz `Workbook` Excel dosyanızı temsil eden Aspose.Cells'den sınıf. Dosya, dönüştürme sırasında kontrol etmek istediğiniz resimler gibi çeşitli harici kaynakları içerebilir.
## Adım 4: PDF Kaydetme Seçeneklerini Ayarlayın
Çalışma kitabını PDF olarak kaydetmeden önce, nasıl kaydedilmesini istediğinizi belirtelim. Bu seçenekleri ihtiyaçlarınıza göre ayarlayabilirsiniz.
```csharp
// PDF Kaydetme Seçeneklerini Belirleyin - Akış Sağlayıcısı
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Her sayfayı yeni bir sayfada kaydedin
```
Burada, yeni bir örnek oluşturuyoruz `PdfSaveOptions`PDF'nizin nasıl biçimlendirileceğini özelleştirmenize olanak tanır. `OnePagePerSheet` Bu seçenek, her Excel sayfasının son PDF'de kendi sayfasına sahip olmasını sağlamak için kullanışlıdır.
## Adım 5: Akış Sağlayıcınızı Atayın
PDF seçenekleriniz ayarlandıktan sonra, Aspose'a harici kaynaklar için özel akış sağlayıcınızı kullanmasını söylemeniz gerekir.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Bu hat sizi birbirine bağlar `Workbook` örnek ile `MyStreamProvider` daha önce oluşturduğunuz sınıf. Bu, dönüştürme sırasında harici kaynaklarla karşılaşıldığında, sağlayıcınızın bunları belirtildiği şekilde ele alacağı anlamına gelir.
## Adım 6: Çalışma Kitabını PDF olarak kaydedin
Her şey hazır, artık Excel çalışma kitabınızı PDF olarak kaydetmenin zamanı geldi.
```csharp
// Çalışma kitabını PDF'e kaydet
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Arayarak `Save` Çalışma kitabı nesnesindeki yöntemi kullanarak ve çıktı dizininizi PDF seçenekleriyle birlikte geçirerek, Excel dosyasını güzelce biçimlendirilmiş bir PDF'ye dönüştürüyorsunuz.
## Adım 7: Başarılı Yürütmeyi Onaylayın
Özetle, sürecinizin başarılı olduğunu teyit etmek her zaman iyidir!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Konsola bir başarı mesajı yazdırmak, operasyonunuzun durumu hakkında bilgi sahibi olmanıza yardımcı olur. Bu küçük onayları kodunuza dahil etmek iyi bir alışkanlıktır.
## Çözüm
İşte oldu! Bu basit adımları izleyerek, Aspose.Cells kullanarak Excel'den PDF'e dönüştürmeler sırasında harici kaynakların nasıl işlendiğini uzmanca kontrol edebilirsiniz. Bu, belgelerinizin artık görüntüleri ve diğer harici öğeleri doğru bir şekilde içerebileceği ve her seferinde cilalı bir son ürün elde edilebileceği anlamına gelir.
## SSS
### Aspose.Cells Nedir?  
Aspose.Cells, .NET geliştiricileri için Excel dosyalarını çeşitli formatlarda oluşturmanıza, düzenlemenize, dönüştürmenize ve işlemenize olanak tanıyan güçlü bir kütüphanedir.
### Aspose.Cells'i nasıl indirebilirim?  
Aspose.Cells'in en son sürümünü şu adresten indirebilirsiniz: [İndirme bağlantısı](https://releases.aspose.com/cells/net/).
### Aspose.Cells'i ücretsiz deneyebilir miyim?  
Evet! Ücretsiz denemeyi şurayı ziyaret ederek alabilirsiniz: [Ücretsiz deneme sayfası](https://releases.aspose.com/).
### Aspose.Cells için desteği nereden bulabilirim?  
Destekle ilgili herhangi bir sorunuz varsa şu adresi ziyaret edebilirsiniz: [Aspose Destek forumu](https://forum.aspose.com/c/cells/9).
### Aspose.Cells için geçici lisansı nasıl alabilirim?  
Geçici lisans başvurusunda bulunabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}