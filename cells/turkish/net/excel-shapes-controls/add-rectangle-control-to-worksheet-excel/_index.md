---
title: Excel'de Çalışma Sayfasına Dikdörtgen Denetimi Ekleme
linktitle: Excel'de Çalışma Sayfasına Dikdörtgen Denetimi Ekleme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel çalışma sayfasına dikdörtgen denetiminin nasıl ekleneceğini ayrıntılı, adım adım bir kılavuzla öğrenin.
weight: 25
url: /tr/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Dikdörtgen Denetimi Ekleme

## giriiş
Excel görevlerini otomatikleştirmeye gelince, Aspose.Cells for .NET çeşitli hedeflere ulaşmanıza yardımcı olabilecek güçlü bir araçtır; bunlardan biri de çalışma sayfalarınıza dikdörtgenler gibi şekiller eklemektir. Bu kılavuzda, Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına dikdörtgen denetiminin nasıl ekleneceğini inceleyeceğiz. Sonunda, içine dikdörtgen denetimi yerleştirilmiş bir çalışma sayfası oluşturabilecek, özelleştirebilecek ve kaydedebileceksiniz.
Ancak konuya girmeden önce ön koşullardan bahsedelim.
## Ön koşullar
Bu eğitimi takip edebilmek için aşağıdaki ön koşulların mevcut olduğundan emin olun:
1.  Aspose.Cells for .NET kütüphanesi: Eğer henüz yapmadıysanız,[kütüphaneyi indir](https://releases.aspose.com/cells/net/) veya Visual Studio'da NuGet kullanarak kurun.
2. .NET Framework: Makinenizde .NET geliştirme ortamının kurulu olması gerekir.
3. Temel C# bilgisi: Adım adım size rehberlik edecek olsak da, C# ve nesne yönelimli programlama konusunda temel bir bilgi sahibi olmanız faydalı olacaktır.
4.  Lisans: Aspose.Cells'i değerlendirme modunda kullanmak temel görevler için iyi çalışır, ancak tam işlevsellik için bir tane edinmeyi düşünün[geçici lisans](https://purchase.aspose.com/temporary-license/)veya bir tane satın almak[Burada](https://purchase.aspose.com/buy).
Şimdi kodlara geçelim!
## Paketleri İçe Aktar
Aspose.Cells ile başlamak için, projenize gerekli ad alanlarını içe aktardığınızdan emin olun. Bu içe aktarımlar, Excel dosyalarıyla etkileşime girmeniz için gereken çeşitli sınıflara ve yöntemlere erişim sağlayacaktır.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Bu satırlar projenizin dosya dizinleriyle etkileşime girebilmesini sağlar (`System.IO`), Excel çalışma kitapları (`Aspose.Cells`), ve şekil çizimi (`Aspose.Cells.Drawing`).
Şimdi, süreci basit adımlara bölelim, böylece siz de kolayca takip edebilir ve kendi projelerinizde bunu uygulayabilirsiniz.
## Adım 1: Dizin Yolunu Ayarlama
Yapmanız gereken ilk şey Excel dosyanızın kaydedileceği dizini tanımlamaktır. Bu adım, projenizin çıktı dosyasını nerede oluşturacağını ve depolayacağını bilmesini sağlar.
### Veri Dizinini Tanımlama
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Burada, Excel dosyasının depolanacağı dizin yolunu belirtirsiniz. Değiştirebilirsiniz`"Your Document Directory"` Bilgisayarınızdaki gerçek yolu kullanarak veya eğer yoksa dinamik olarak bir klasör oluşturarak.
### Dizin Kontrolü ve Oluşturulması
```csharp
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu blok dizinin var olup olmadığını kontrol eder. Yoksa bir tane oluşturur. Bunu, herhangi bir belgeyi depolamadan önce dosya dolabınızın hazır olması gibi düşünün.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturma
 Bu adımda, aşağıdakileri kullanarak yeni bir Excel çalışma kitabı oluşturursunuz:`Aspose.Cells.Workbook` sınıf. Bu, çalışma sayfanız ve şekilleriniz için bir kap görevi görecektir.
```csharp
// Yeni bir Çalışma Kitabı örneği oluşturun.
Workbook excelbook = new Workbook();
```
 Arayarak`Workbook` Oluşturucuyu kullanarak artık özelleştirmeye hazır boş bir Excel çalışma kitabınız var.
## Adım 3: Dikdörtgen Denetimi Ekleme
İşte sihrin gerçekleştiği yer burası. Çalışma kitabınızın ilk çalışma sayfasına bir dikdörtgen şekli ekleyeceksiniz.
```csharp
// Bir dikdörtgen denetimi ekleyin.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Bunu biraz açalım:
- `excelbook.Worksheets[0]`: Bu, çalışma kitabınızdaki ilk çalışma sayfasına erişim sağlar.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Bu, çalışma sayfasına bir dikdörtgen şekli ekler. Buradaki parametreler, dikdörtgenin konumunu (satır ve sütun) ve genişliğini ve yüksekliğini tanımlar.
## Adım 4: Dikdörtgeni Özelleştirme
Sadece bir dikdörtgen eklemek yeterli değil; onu özelleştirmek isteyeceksiniz. Bu adımda, dikdörtgenin yerleşimini, çizgi kalınlığını ve çizgi stilini ayarlayacağız.
### Yerleşimi Ayarlama
```csharp
// Dikdörtgenin yerleşimini ayarlayın.
rectangle.Placement = PlacementType.FreeFloating;
```
Bu, dikdörtgenin serbestçe hareket edebildiğini, yani hücre boyutlarına bağlı olmayacağını belirtir.
### Çizgi Ağırlığını Ayarlama
```csharp
// Çizgi kalınlığını ayarlayın.
rectangle.Line.Weight = 4;
```
Burada dikdörtgenin çizgi kalınlığını 4 noktaya ayarlıyoruz. Sayı ne kadar yüksekse çizgi o kadar kalındır.
### Dash Stilini Ayarlama
```csharp
// Dikdörtgenin çizgi stilini ayarlayın.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Bu çizgi dikdörtgenin sınırının çizgi stilini düz olarak ayarlar. Farklı stilleri deneyebilirsiniz.`Dash` veya`Dot` İhtiyaçlarınıza bağlı olarak.
## Adım 5: Çalışma Kitabını Kaydetme
Dikdörtgen eklenip özelleştirildikten sonra, son adım çalışma kitabını belirtilen dizine kaydetmektir.
```csharp
// Excel dosyasını kaydedin.
excelbook.Save(dataDir + "book1.out.xls");
```
 Bu, çalışma kitabını bir`.xls` Daha önce tanımladığınız klasördeki dosya. Dosya biçimini, uzantıyı değiştirerek değiştirebilirsiniz, örneğin`.xlsx` Eğer daha yeni Excel formatını tercih ediyorsanız.
## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına dikdörtgen denetimi eklemek, adım adım açıklığa kavuşturduğunuzda basit bir işlemdir. Görsel çekicilik için şekiller eklemeniz, verilerinizin bölümlerini vurgulamanız veya raporlarınızı özelleştirmeniz gerekip gerekmediğine bakılmaksızın, Aspose.Cells bunu programatik olarak yapma esnekliğini size sunar.
Bu kılavuz, Aspose.Cells ile Excel sayfalarınıza dikdörtgenler gibi şekiller eklemeye başlamak için ihtiyacınız olan tüm bilgileri size sağlamalıdır. Şimdi deneme yapmanın ve bu güçlü kütüphaneyle başka neler başarabileceğinizi görmenin zamanı!
## SSS
### Aspose.Cells for .NET kullanarak daire veya çizgi gibi başka şekiller ekleyebilir miyim?  
Evet, Aspose.Cells daireler, çizgiler, oklar ve daha fazlası dahil olmak üzere çeşitli şekiller eklemenize olanak tanır.
### Dikdörtgen denetimi için başka hangi özellikleri ayarlayabilirim?  
Dolgu rengini, çizgi rengini, şeffaflığı özelleştirebilir ve hatta dikdörtgenin içine metin ekleyebilirsiniz.
### Aspose.Cells .NET Core ile uyumlu mu?  
Evet, Aspose.Cells .NET Core'un yanı sıra .NET Framework ve diğer .NET tabanlı platformları da destekler.
### Dikdörtgeni belirli bir hücreye göre konumlandırabilir miyim?  
 Evet, dikdörtgeni belirli satır ve sütunlara yerleştirebilir veya`PlacementType` nasıl sabitleneceğini kontrol etmek için.
### Aspose.Cells için ücretsiz deneme sürümü mevcut mu?  
 Evet, alabilirsiniz[ücretsiz deneme](https://releases.aspose.com/) Satın almadan önce kütüphanenin özelliklerini test etmek için web sitesinden yararlanabilirsiniz.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
