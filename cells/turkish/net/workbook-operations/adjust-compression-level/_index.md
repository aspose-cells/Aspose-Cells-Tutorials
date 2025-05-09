---
"description": "Bu adım adım kılavuzla Aspose.Cells for .NET kullanarak Excel çalışma kitaplarının sıkıştırma düzeyini nasıl ayarlayacağınızı öğrenin. Dosya yönetiminizi optimize edin."
"linktitle": "Çalışma Kitabında Sıkıştırma Düzeyini Ayarla"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Çalışma Kitabında Sıkıştırma Düzeyini Ayarla"
"url": "/tr/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabında Sıkıştırma Düzeyini Ayarla

## giriiş
Büyük Excel dosyalarını yönetmeye gelince, sıkıştırma oyunun kurallarını değiştirir. Sadece depolama alanından tasarruf etmekle kalmaz, aynı zamanda dosya transferlerini daha hızlı ve daha verimli hale getirir. .NET için Aspose.Cells ile çalışıyorsanız, çalışma kitaplarınızın sıkıştırma seviyesini kolayca ayarlayabilirsiniz. Bu kılavuzda, kodun her bir bölümünü ve nasıl çalıştığını anlamanızı sağlayarak sizi adım adım süreçte yönlendireceğiz.
## Ön koşullar
Koda dalmadan önce, yerine getirmeniz gereken birkaç ön koşul vardır:
1. Temel C# Bilgisi: C# programlamaya aşina olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
2. Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesinin yüklü olması gerekir. Bunu şuradan indirebilirsiniz: [Burada](https://releases.aspose.com/cells/net/).
3. Visual Studio: Kodun çalıştırılabilmesi için Visual Studio benzeri bir geliştirme ortamına ihtiyaç duyulacaktır.
4. .NET Framework: Projenizin .NET Framework'ün uyumlu bir sürümüyle kurulduğundan emin olun.
## Paketleri İçe Aktar
Başlamak için, C# projenize gerekli paketleri içe aktarmanız gerekir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
Bu paketler, Aspose.Cells kitaplığını kullanarak Excel dosyalarıyla çalışmak için gereklidir. `Aspose.Cells` namespace, Excel dosyalarını düzenlemek için ihtiyaç duyduğunuz tüm sınıfları içerirken `Aspose.Cells.Xlsb` dosyaları XLSB formatında kaydetme seçeneklerini sunar.
Şimdi, bir çalışma kitabında sıkıştırma seviyesini ayarlama sürecini yönetilebilir adımlara bölelim.
## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın
Öncelikle kaynak dosyalarınızın nerede bulunduğunu ve çıktı dosyalarını nereye kaydetmek istediğinizi belirtmeniz gerekir. Bu, programınızın çalışması gereken dosyaları nerede bulacağını bilmesini sağlamak için çok önemlidir.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Yer değiştirmek `"Your Document Directory"` dizinlerinize giden gerçek yol ile. Bu, programın sıkıştırmak istediğiniz dosyaları bulmasına yardımcı olacaktır.
## Adım 2: Çalışma Kitabını Yükleyin
Sonra, sıkıştırmak istediğiniz çalışma kitabını yükleyeceksiniz. Sihir burada başlıyor!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Bu satırda, yeni bir örnek oluşturuyoruz `Workbook` sınıfını açın ve mevcut bir Excel dosyasını yükleyin. Dosya adının kaynak dizininizde bulunan adla eşleştiğinden emin olun.
## Adım 3: Kaydetme Seçeneklerini Ayarlayın
Şimdi kaydetme seçeneklerini yapılandırma zamanı. Çıktı dosyası için sıkıştırma türünü ayarlayacağız. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
The `XlsbSaveOptions` class, çalışma kitabınızı XLSB biçiminde kaydederken sıkıştırma düzeyleri de dahil olmak üzere çeşitli seçenekleri belirtmenize olanak tanır.
## Adım 4: Seviye 1 için Sıkıştırma Süresini Ölçün
İlk sıkıştırma seviyesiyle başlayalım. Çalışma kitabını bu sıkıştırma seviyesiyle kaydetmenin ne kadar sürdüğünü ölçeceğiz.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Burada, sıkıştırma türünü Seviye 1'e ayarlıyoruz, çalışma kitabını kaydediyoruz ve ardından geçen süreyi ölçüyoruz. Bu bize sürecin ne kadar sürdüğüne dair bir fikir veriyor.
## Adım 5: Seviye 6 için Sıkıştırma Süresini Ölçün
Şimdi Seviye 6 sıkıştırmanın nasıl performans gösterdiğine bakalım.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Bu adım bir öncekine benzer, ancak sıkıştırma seviyesini Seviye 6 olarak değiştiriyoruz. Çalışma kitabının karmaşıklığına bağlı olarak zamanın değişebileceğini fark edeceksiniz.
## Adım 6: Seviye 9 için Sıkıştırma Süresini Ölçün
Son olarak en yüksek sıkıştırma seviyesine sahip performansa bakalım.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Bu adımda sıkıştırma seviyesini Seviye 9'a ayarlıyoruz. Dosya boyutunda en önemli azalmayı genellikle burada göreceksiniz, ancak işlenmesi daha uzun sürebilir.
## Adım 7: Son Çıktı
Tüm sıkıştırma seviyelerini çalıştırdıktan sonra, işlemin başarıyla tamamlandığını belirten bir mesaj çıktısı alabilirsiniz.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Bu basit kod satırı, programınızın herhangi bir aksama olmadan yürütüldüğünü doğrular.
## Çözüm
Aspose.Cells for .NET kullanarak çalışma kitaplarınızın sıkıştırma seviyesini ayarlamak, dosya boyutu ve performans açısından önemli faydalar sağlayabilecek basit bir işlemdir. Bu kılavuzda özetlenen adımları izleyerek, uygulamalarınızda sıkıştırmayı kolayca uygulayabilir ve Excel dosya yönetiminizin verimliliğini artırabilirsiniz.
## SSS
### Aspose.Cells Nedir?  
Aspose.Cells, geliştiricilerin Microsoft Excel'e ihtiyaç duymadan Excel dosyaları oluşturmalarına, düzenlemelerine ve dönüştürmelerine olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'i nasıl kurarım?  
Aspose.Cells'i şuradan indirip yükleyebilirsiniz: [Aspose web sitesi](https://releases.aspose.com/cells/net/).
### Hangi sıkıştırma seviyeleri mevcut?  
Aspose.Cells, Seviye 1'den (en düşük sıkıştırma) Seviye 9'a (en yüksek sıkıştırma) kadar çeşitli sıkıştırma seviyelerini destekler.
### Aspose.Cells'i ücretsiz deneyebilir miyim?  
Evet! Aspose.Cells'in ücretsiz denemesini alabilirsiniz [Burada](https://releases.aspose.com/).
### Aspose.Cells için desteği nereden bulabilirim?  
Herhangi bir soru veya destek için Aspose destek forumunu ziyaret edebilirsiniz [Burada](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}