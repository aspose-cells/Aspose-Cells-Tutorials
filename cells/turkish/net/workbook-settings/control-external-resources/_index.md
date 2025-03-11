---
title: Çalışma Kitabı Ayarını Kullanarak Harici Kaynakları Kontrol Etme
linktitle: Çalışma Kitabı Ayarını Kullanarak Harici Kaynakları Kontrol Etme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Kapsamlı adım adım eğitimimiz ile Aspose.Cells for .NET kullanarak Excel'de harici kaynakları nasıl kontrol edeceğinizi öğrenin.
weight: 10
url: /tr/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabı Ayarını Kullanarak Harici Kaynakları Kontrol Etme

## giriiş
Veri işleme ve sunumu alanında, harici kaynakları verimli bir şekilde yönetmek oyunun kurallarını değiştirebilir. Excel dosyalarıyla çalışıyorsanız ve .NET için Aspose.Cells kullanarak harici kaynakları sorunsuz bir şekilde yönetmek istiyorsanız, doğru yerdesiniz! Bu makalede, Excel çalışma kitaplarıyla çalışırken harici kaynakları kontrol etme konusuna derinlemesine ineceğiz. Bu kılavuzun sonunda, harici kaynaklardan zahmetsizce resim ve veri yüklemek için özelleştirilmiş bir çözüm uygulayabileceksiniz.
## Ön koşullar
Kodlamanın inceliklerine dalmadan önce, yerine getirmeniz gereken birkaç ön koşul var. Şunlardan emin olun:
1. Visual Studio'ya sahip olun: .NET uygulamalarınızı yazmak ve test etmek için bir IDE'ye ihtiyacınız olacak. Visual Studio, kapsamlı desteği ve kullanım kolaylığı nedeniyle en çok önerilen seçenektir.
2.  .NET için Aspose.Cells'i indirin: Henüz yapmadıysanız, Aspose.Cells kitaplığını şu adresten edinin:[indirme bağlantısı](https://releases.aspose.com/cells/net/). 
3. C# Temel Anlayışı: C# ve .NET framework kavramlarına aşinalık, süreci sizin için daha sorunsuz hale getirecektir.
4. Ortamınızı Ayarlayın: Projenizin Aspose.Cells kütüphanesine başvurduğundan emin olun. Bunu Visual Studio içindeki NuGet Paket Yöneticisi aracılığıyla yapabilirsiniz.
5. Örnek Dosyalar: Bağlantılı bir resim gibi harici bir kaynak içeren örnek bir Excel dosyası hazırlayın. Bu dosya, tartıştığımız işlevleri göstermenize yardımcı olacaktır.
Bunları ayarladıktan sonra, Aspose.Cells ile harici kaynakları kontrol etmeye hazırsınız.
## Paketleri İçe Aktar
Kodlamaya başlamak için, gerekli paketleri C# dosyanıza aktarmanız gerekir. İhtiyacınız olanlar şunlardır:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Bu ad alanları, Excel dosyalarını düzenlemek ve görselleri işlemek için gereken işlevlere erişim sağlar.
 Harici kaynakları kontrol etmenize yardımcı olmak için bunu yönetilebilir adımlara bölelim`Workbook Settings`. Özel bir akış sağlayıcısı oluşturma, bir Excel dosyası yükleme ve bir çalışma sayfasını bir görüntüye dönüştürme konusunda yol göstereceğiz. Takip etmekten çekinmeyin!
## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın
Başlamak için, dosyalarımızı okuyacağımız ve çıktımızı kaydedeceğimiz dizinleri belirtmemiz gerekir. Dosya bulunamadı hatalarından kaçınmak için doğru yolları ayarlamak önemlidir.
```csharp
// Kaynak dizini
static string sourceDir = "Your Document Directory";
// Çıktı dizini
static string outputDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` dosyalarınızın bulunduğu gerçek yol ile.
## Adım 2: IStreamProvider Arayüzünü Uygulayın
 Daha sonra, aşağıdakileri uygulayan özel bir sınıf oluşturacağız:`IStreamProvider` arayüz. Bu sınıf, harici kaynaklara (görüntüler gibi) nasıl erişileceğini yönetecektir.
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Gerekirse kaynakları temizleyin
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Harici kaynağın dosya akışını açın
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
 İçinde`InitStream` yöntem, harici kaynağımız olarak işlev gören dosyayı açar ve onu`Stream`özellik. Bu, çalışma kitabının işleme sırasında kaynağa erişmesine izin verir.
## Adım 3: Excel Dosyasını Yükleyin
Artık akış sağlayıcımız hazır olduğuna göre, harici kaynağı içeren Excel çalışma kitabını yükleyelim.
```csharp
public static void Run()
{
    // Örnek Excel dosyasını yükle
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // IStreamProvider uygulamanızı sağlayın
    wb.Settings.StreamProvider = new SP();
```
 Bu kod parçacığında Excel dosyamızı yükleyip özel kodumuzu atıyoruz.`StreamProvider` dış kaynakları yönetmek için uygulama.
## Adım 4: Çalışma Sayfasına Erişim
Çalışma kitabını yükledikten sonra, istediğimiz çalışma sayfasına kolayca erişebiliriz. İlkini alalım.
```csharp
    // İlk çalışma sayfasına erişin
    Worksheet ws = wb.Worksheets[0];
```
Çok basit, değil mi? Herhangi bir çalışma sayfasına dizinini belirterek erişebilirsiniz.
## Adım 5: Görüntü veya Yazdırma Seçeneklerini Yapılandırın
Şimdi çıktı görüntüsünün nasıl görünmesini istediğimizi tanımlayacağız. Her sayfa için bir sayfa olduğundan emin olmak ve çıktı görüntü türünü belirtmek gibi seçenekleri yapılandıracağız.
```csharp
    // Resim veya baskı seçeneklerini belirtin
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Çıktı formatını PNG olarak seçmek, kalitenin canlı ve net kalmasını sağlar!
## Adım 6: Çalışma Sayfasını Bir Görüntüye Dönüştürün
Her şey ayarlandıktan sonra, seçtiğimiz çalışma sayfasını bir resim dosyasına dönüştürelim! Heyecan verici kısım burası; Excel sayfanızın güzel bir resme dönüştüğünü göreceksiniz.
```csharp
    // Gerekli parametreleri geçirerek sayfa oluşturma
    SheetRender sr = new SheetRender(ws, opts);
    // Tüm çalışma sayfanızı png resmine dönüştürün
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 The`ToImage` fonksiyonu tüm ağır işi yapar ve sayfayı bir görüntüye dönüştürür. Bu adım tamamlandığında, görüntünün çıktı dizininize kaydedildiğini göreceksiniz.
## Çözüm
Ve işte oldu! Artık .NET'te Aspose.Cells kullanarak Excel dosyalarıyla çalışırken harici kaynakları kontrol etme bilgisine sahipsiniz. Bu yalnızca uygulamanızın yeteneklerini geliştirmekle kalmaz, aynı zamanda veri kümelerini ve sunumları işlemeyi bir sahil yürüyüşü haline getirir. Sağlanan adımları izleyerek, bu işlevselliği projenizin özel ihtiyaçlarına uyacak şekilde kolayca çoğaltabilir ve uyarlayabilirsiniz.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, C# ve .NET geliştiricilerinin Microsoft Excel'in kurulumuna ihtiyaç duymadan Excel dosyaları oluşturması, düzenlemesi ve yönetmesi için tasarlanmış güçlü bir kütüphanedir.
### Aspose.Cells for .NET'i nasıl indirebilirim?
 Bunu şuradan indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/cells/net/).
### Ücretsiz deneme imkanı var mı?
 Evet! Aspose.Cells'in ücretsiz deneme sürümüne şu adresten erişebilirsiniz:[yayın sayfası](https://releases.aspose.com/).
### Aspose.Cells hangi dosya türlerini destekler?
Aspose.Cells, XLS, XLSX, CSV ve daha fazlası dahil olmak üzere çeşitli Excel formatlarını destekler.
### Aspose.Cells için desteği nerede bulabilirim?
 Aspose destek forumunu şu adresten ziyaret edebilirsiniz:[Aspose Forum](https://forum.aspose.com/c/cells/9) yardım için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
