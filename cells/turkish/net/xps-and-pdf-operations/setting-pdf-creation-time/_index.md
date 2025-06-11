---
"description": "Aspose.Cells kullanarak .NET'te PDF oluşturma süresini nasıl ayarlayacağınızı öğrenin. Excel'den PDF'e kusursuz dönüşüm için adım adım kılavuzumuzu izleyin."
"linktitle": ".NET'te PDF Oluşturma Süresini Ayarlama"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": ".NET'te PDF Oluşturma Süresini Ayarlama"
"url": "/tr/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te PDF Oluşturma Süresini Ayarlama

## giriiş
Günümüzün dijital çağında, belgeleri farklı biçimlere dönüştürme yeteneği birçok uygulama için hayati önem taşır. Yaygın ihtiyaçlardan biri Excel elektronik tablolarını PDF dosyalarına dönüştürmektir. Bu yalnızca biçimlendirmeyi korumakla kalmaz, aynı zamanda paylaşmayı ve yazdırmayı da çok daha kolay hale getirir. .NET ile çalışan bir geliştiriciyseniz, Aspose.Cells bu süreci basitleştiren harika bir kütüphanedir. Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel dosyasını PDF'ye dönüştürürken PDF oluşturma süresinin nasıl ayarlanacağını inceleyeceğiz.
## Ön koşullar
Kodun ayrıntılarına girmeden önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.
### İhtiyacınız Olanlar
1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. Bu sizin geliştirme ortamınız olacak.
2. .NET için Aspose.Cells: Aspose.Cells kitaplığını şu adresten indirin: [web sitesi](https://releases.aspose.com/cells/net/)Ayrıca, işlevselliğini test etmek için ücretsiz denemeye de başlayabilirsiniz.
3. Temel C# Bilgisi: C# programlamaya aşina olmak, kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
4. Excel Dosyası: Dönüştürmeye hazır bir Excel dosyanız olsun. Bu örnek için, adlı bir dosya kullanacağız `Book1.xlsx`.
Artık ön koşulları tamamladığımıza göre, eğlenceli kısma geçebiliriz: Gerekli paketleri içe aktarmak ve kodu yazmak!
## Paketleri İçe Aktar
Başlamak için, C# dosyanıza gerekli ad alanlarını içe aktarmanız gerekir. Bu, Aspose.Cells kütüphanesi tarafından sağlanan sınıflara ve yöntemlere erişmenizi sağladığı için önemlidir.
### C# Projenizi Açın
Visual Studio'yu açın ve yeni bir proje oluşturun veya PDF dönüştürme özelliğini uygulamak istediğiniz mevcut bir projeyi açın.
### Aspose.Cells Referansını Ekle
Aspose.Cells kütüphanesini projenize eklemek için Çözüm Gezgini'nde projenize sağ tıklayın, “NuGet Paketlerini Yönet” seçeneğini belirleyin ve “Aspose.Cells” ifadesini arayın. Paketi yükleyin.
### Ad Alanlarını İçe Aktar
C# dosyanızın en üstüne aşağıdaki ad alanlarını ekleyin:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Bu ad alanları size Çalışma Kitabı sınıfına ve diğer temel işlevlere erişim sağlayacaktır.

Paketlerimiz içe aktarıldığına göre, şimdi bir Excel dosyasını PDF'ye dönüştürme sürecini, oluşturulma zamanını ayarlayarak inceleyelim.
## Adım 1: Belge Dizinini Tanımlayın
Öncelikle belgelerinizin saklandığı dizini belirtmeniz gerekir. Excel dosyanızın bulunduğu ve çıktı PDF'inin kaydedileceği yer burasıdır.
```csharp
string dataDir = "Your Document Directory"; // Belge dizininizi belirtin
```
Yer değiştirmek `"Your Document Directory"` gerçek yolunuzla `Book1.xlsx` dosya bulunur. Bu yol, uygulamanın işleme için dosyayı bulmasına yardımcı olacaktır.
## Adım 2: Excel Dosyasını Yükleyin
Daha sonra Excel dosyasını bir `Workbook` nesne. Aspose.Cells'in öne çıktığı nokta tam da burasıdır, çünkü Excel dosyalarıyla zahmetsizce çalışmanıza olanak tanır.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excel dosyanıza giden yol
Workbook workbook = new Workbook(inputPath); // Excel dosyasını yükleyin
```
The `Workbook` sınıfı Excel dosyalarını yüklemek ve düzenlemek için kullanılır. Giriş yolunu geçirerek, uygulamaya hangi dosyayla çalışacağını söylersiniz.
## Adım 3: PdfSaveOptions'ı Oluşturun
Şimdi, bir örnek oluşturmanın zamanı geldi `PdfSaveOptions`Bu sınıf, oluşturma zamanı da dahil olmak üzere çalışma kitabınızı PDF olarak kaydetmek için çeşitli seçenekleri belirtmenize olanak tanır.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // PdfSaveOptions örneğini oluştur
options.CreatedTime = DateTime.Now; // Oluşturma zamanını şimdi ayarlayın
```
Ayarlayarak `options.CreatedTime` ile `DateTime.Now`, PDF'in oluşturulduğu andaki tarih ve saati yansıtacağından emin olursunuz.
## Adım 4: Çalışma Kitabını PDF olarak kaydedin
Son olarak, az önce tanımladığınız seçenekleri kullanarak çalışma kitabını PDF dosyası olarak kaydedeceksiniz.
```csharp
workbook.Save(dataDir + "output.pdf", options); // PDF olarak kaydet
```
Bu kod satırı çalışma kitabını alır ve belirtilen konuma PDF formatında kaydeder. `options` PDF meta verilerine oluşturulma zamanını dahil etmek için parametre geçirilir.

## Çözüm
Ve işte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasını başarıyla PDF'e dönüştürdünüz, oluşturma zaman damgasıyla birlikte. Bu özellik, belge sürümlerini takip etmeniz gerektiğinde veya alıcılara belgenin ne zaman oluşturulduğu hakkında bilgi sağlamak istediğinizde inanılmaz derecede yararlı olabilir.
Aspose.Cells'in daha fazla özelliğini keşfetmek istiyorsanız, şuraya göz atmaktan çekinmeyin: [belgeleme](https://reference.aspose.com/cells/net/).
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyaları oluşturmasına, düzenlemesine ve dönüştürmesine olanak tanıyan güçlü bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
Evet, ücretsiz deneme sürümüyle başlayabilirsiniz. [Aspose web sitesi](https://releases.aspose.com/).
### Diğer PDF özelliklerini nasıl ayarlarım?
Çeşitli PDF özelliklerini kullanarak ayarlayabilirsiniz. `PdfSaveOptions` sayfa boyutu, sıkıştırma ve daha fazlası gibi sınıflar.
### Birden fazla Excel dosyasını aynı anda dönüştürmek mümkün müdür?
Evet, bir dosya listesi arasında geçiş yapabilir ve her birine aynı dönüştürme işlemini uygulayabilirsiniz.
### Aspose.Cells için desteği nereden alabilirim?
Aspose topluluğundan destek alabilirsiniz [destek forumu](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}