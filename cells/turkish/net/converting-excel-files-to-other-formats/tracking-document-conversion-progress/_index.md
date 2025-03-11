---
title: .NET'te Belge Dönüştürme İlerlemesini Programatik Olarak İzleme
linktitle: .NET'te Belge Dönüştürme İlerlemesini Programatik Olarak İzleme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu ayrıntılı eğitimde, Aspose.Cells for .NET kullanarak belge dönüştürme ilerlemesini programatik olarak nasıl takip edeceğinizi öğrenin.
weight: 20
url: /tr/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Belge Dönüştürme İlerlemesini Programatik Olarak İzleme

## giriiş
Aspose.Cells for .NET kullanarak belge dönüştürme sürecinizi geliştirmeyi mi düşünüyorsunuz? Öyleyse doğru yerdesiniz! Bu eğitimde, Excel belgelerinin PDF formatına dönüştürülürken dönüşüm sürecini derinlemesine takip edeceğiz. Bunu başarmak için gerekli adımlarda size rehberlik etmekle kalmayacağız, aynı zamanda bu süreçte bazı yararlı içgörüler de serpiştireceğiz. Hadi başlayalım!
## Ön koşullar
Belge dönüşümlerini izlemenin inceliklerine girmeden önce, yerine getirmeniz gereken birkaç ön koşul vardır:
1. C# Temel Bilgisi: Kodlamada C# kullanacağımız için, bu programlama dilinin temellerine dair bilgi sahibi olmak işimize yarayacaktır.
2. Visual Studio Kurulu: Bu, geliştirme ortamımız olarak hizmet edecektir. Tercih ettiğiniz herhangi bir sürümü kullanabilirsiniz, ancak en son sürüm her zaman iyi bir seçimdir.
3.  Aspose.Cells for .NET: Aspose.Cells'in yüklü olduğundan emin olun. Bunu şuradan indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/cells/net/).
4.  Bir Excel Dosyası: Dönüştürmeye hazır bir örnek Excel dosyası bulundurun. Basit bir Excel dosyası oluşturabilirsiniz.`.xlsx` takip edilecek dosya.
## Paketleri İçe Aktar
Artık ön koşullarımızı tamamladığımıza göre, gerekli paketleri C# projenize içe aktarma zamanı. İşte nasıl yapacağınız:
### Yeni Bir Proje Oluştur
1. Visual Studio'yu açın ve yeni bir proje oluşturun. Basitlik için bir Konsol Uygulaması şablonu seçin.
### Aspose.Cells'e Referans Ekle
2. Çözüm Gezgini'ndeki Referanslar'a sağ tıklayın, Referans Ekle'yi seçin ve otomatik olarak eklenmemişse Aspose.Cells derlemesine gidin. NuGet Paket Yöneticisi'ni Paket Yöneticisi Konsolu'nda aşağıdaki komutu çalıştırarak da kullanabilirsiniz:
```bash
Install-Package Aspose.Cells
```
### Ad Alanlarını İçe Aktar
3.  En üstte`Program.cs` dosyaya, aşağıdaki using yönergesini ekleyin:
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Artık projemizin kurulumu tamamlandı!

Temeli attıktan sonra, belge dönüşümünü izleme sürecinin gerçek sürecini anlaşılır adımlara bölelim. 
## Adım 1: Dizinlerinizi Tanımlayın
Kaynak ve çıktı dosyalarınızın bulunacağı dizinleri belirterek başlayın. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// Çıktı dizini
string outputDir = "Your Document Directory";
```
 Değiştirdiğinizden emin olun`"Your Document Directory"` sisteminizdeki gerçek yol ile. Bu dosyalarınızı kolayca bulmanıza yardımcı olacaktır.
## Adım 2: Çalışma Kitabını Yükleyin
 Daha sonra Excel çalışma kitabınızı yüklemeniz gerekir`Workbook` sınıf. İşte nasıl:
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
 Bu kod satırı bir`Workbook` Belirlediğimiz Excel dosyası ile etkileşime girmemizi sağlayacak nesne.
## Adım 3: PDF Kaydetme Seçeneklerini Ayarlayın
Şimdi, PDF kaydetme seçeneklerini ayarlayalım. İlerlemeyi izlemenin büyüsü burada başlar. Bir örnek oluşturacaksınız`PdfSaveOptions` ve ona bir geri çağırma atayın.
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
Özel bir geri arama atayarak (`TestPageSavingCallback`), sayfa dönüşüm ilerlemesini izlemek için kendi mantığımızı uygulayabiliriz.
## Adım 4: Çalışma Kitabını PDF olarak kaydedin
 Her şey ayarlandıktan sonra, çalışma kitabınızı PDF olarak kaydetme zamanı geldi.`Save` yöntemi`Workbook` sınıf şöyle:
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
Bu satır, sayfalar işlenirken dönüştürme sürecini tetikleyecek ve geri çağırma yöntemlerimizi çağıracaktır.
## Adım 5: Geri Arama Sınıfını Uygulayın
 Şimdi şunu yaratalım:`TestPageSavingCallback` sınıf. Burada her sayfanın kaydedilmesinin başında ve sonunda ne olacağını tanımlayabilirsiniz.
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Sayfa indeksi 2'den önce sayfa çıktısı almayın.
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Sayfa indeksinden sonra sayfa çıktısı vermeyin 8.
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`Bu yöntem, bir sayfa kaydedilmeye başlamadan hemen önce çağrılır. Burada, her sayfa için kaydetme işleminin başlangıcını günlüğe kaydederiz. Ek olarak, sayfanın çıktısını alıp almayacağımızı kontrol edebiliriz. Bu durumda, 2. dizinden önceki sayfalar atlanır.
- `PageEndSaving`: Bu yöntem bir sayfa kaydedildikten sonra çağrılır. Her sayfa için kaydetmenin ne zaman sona erdiğini günlüğe kaydetmenize ve daha fazla sayfanın işlenip işlenmeyeceğini kontrol etmenize olanak tanır. Bu örnekte, sayfa dizini 8'den sonra dururuz.
## Çözüm
Tebrikler! Aspose.Cells for .NET kullanarak belge dönüştürmenin ilerlemesini izlemek için bir sistemi başarıyla uyguladınız. Bu yaklaşım yalnızca dönüştürme sürecini izlemenizi sağlamakla kalmaz, aynı zamanda hangi sayfaların dahil edileceği veya hariç tutulacağı konusunda da kontrol sahibi olmanızı sağlayarak belge yönetiminizi çok daha verimli hale getirir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'in ücretsiz deneme sürümünü nasıl edinebilirim?
 Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/).
### Dönüştürme sürecini özelleştirmek mümkün mü?
Evet, geri aramaları kullanarak sayfaların dönüştürme sırasında nasıl işleneceğini özelleştirebilirsiniz.
### Çıktı dosya adını kontrol edebilir miyim?
Kesinlikle! Çalışma kitabını kaydederken çıktı dosyanız için herhangi bir ad belirtebilirsiniz.
### Aspose.Cells için desteği nerede bulabilirim?
 Destek almak için şu adresi ziyaret edebilirsiniz:[Aspose forumu](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
