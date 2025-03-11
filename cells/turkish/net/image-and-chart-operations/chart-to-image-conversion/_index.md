---
title: .NET'te Grafikten Görüntüye Dönüştürme
linktitle: .NET'te Grafikten Görüntüye Dönüştürme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım kılavuzla Aspose.Cells kullanarak .NET'te grafikleri resimlere nasıl dönüştüreceğinizi öğrenin. Excel grafiklerini kolayca yüksek kaliteli resimlere dönüştürün.
weight: 10
url: /tr/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Grafikten Görüntüye Dönüştürme

## giriiş
Excel'den bir grafiği bir görüntüye dönüştürmek, raporlama sistemleri oluştururken veya görsel veri gösterimlerini paylaşırken önemli bir gereklilik olabilir. Neyse ki, .NET için Aspose.Cells ile bu işlem çocuk oyuncağı! İster raporlar oluşturun, ister Excel grafiklerini daha iyi görüntüleme için görüntülere dönüştürün, bu kılavuz sizi adım adım süreçte yönlendirecektir.
## Ön koşullar
Başlamadan önce, bu eğitimi takip etmek için her şeyin yerinde olduğundan emin olalım.
### Aspose.Cells for .NET Kütüphanesi
Öncelikle projenizde Aspose.Cells for .NET kütüphanesini indirip referans göstermeniz gerekecek. En son sürümü buradan edinebilirsiniz:
- [.NET için Aspose.Cells'i indirin](https://releases.aspose.com/cells/net/)
### .NET Ortamı
Sisteminizde .NET framework'ün yüklü olduğundan emin olun. Bu örneği çalıştırmak için Visual Studio veya başka bir .NET geliştirme ortamını kullanabilirsiniz.
### Lisans Kurulumu (İsteğe bağlı)
 Aspose.Cells'i ücretsiz deneme sürümüyle kullanabilmenize rağmen, sınırlama olmaksızın tam işlevsellik için bir lisans başvurusunda bulunmayı düşünün.[geçici lisans](https://purchase.aspose.com/temporary-license/) veya bir tane satın alın[Burada](https://purchase.aspose.com/buy).

## Paketleri İçe Aktar
Başlamak için, Aspose.Cells kütüphanesiyle çalışmak için gerekli ad alanlarını içe aktaralım. Bu, Excel dosyalarını düzenlememize ve resimler oluşturmamıza olanak tanır.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Kodlama kısmına başlamadan önce bu paketlerin hazır olduğundan emin olun.

Şimdi bir grafiğin görüntüye dönüştürülme sürecini basit adımlara bölelim.
## Adım 1: Proje Dizininizi Ayarlayın
Oluşturduğunuz görselleri kaydedebileceğiniz bir yere ihtiyacınız var, değil mi? Öncelikle çıktı görsellerinin kaydedileceği bir dizin oluşturalım.

Belge dizinimiz için yolu tanımlayarak ve klasörün var olduğundan emin olarak başlıyoruz. Yoksa, bir tane oluşturacağız.
```csharp
// Resimlerin kaydedileceği dizini tanımlayın
string dataDir = "Your Document Directory";
//Dizinin var olup olmadığını kontrol edin
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu adımla grafik görsellerinizi oluşturmaya ve bu dizine kaydetmeye hazırsınız.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
Burada bir Çalışma Kitabı nesnesi oluşturacağız. Bu, grafiğin yerleştirileceği Excel dosyamızı temsil edecektir.

Bir çalışma kitabı, sayfalar içeren bir Excel dosyası gibidir. Yeni bir çalışma kitabı oluşturarak, boş bir Excel dosyasıyla yeni bir başlangıç yapıyoruz.
```csharp
// Yeni bir Çalışma Kitabı nesnesi oluşturun
Workbook workbook = new Workbook();
```
## Adım 3: Yeni bir Çalışma Sayfası Ekleyin
Her Excel dosyasının çalışma sayfaları (veya sekmeleri) vardır. Çalışma kitabımıza bir tane ekleyelim.

Yeni bir çalışma sayfası eklemek önemlidir çünkü verilerimizi ve grafiklerimizi bu sayfaya ekleyeceğiz. Sayfa eklendiğinde, referansını alırız.
```csharp
// Çalışma kitabına yeni bir çalışma sayfası ekle
int sheetIndex = workbook.Worksheets.Add();
// Yeni eklenen çalışma sayfasını al
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Adım 4: Çalışma Sayfasını Verilerle Doldurun
Anlamlı bir grafik oluşturmak için biraz veriye ihtiyacımız var, değil mi? Birkaç hücreyi örnek değerlerle dolduralım.

Çalışma sayfasındaki belirli hücrelere veri ekleyeceğiz. Bu veri daha sonra grafiğimizi oluşturmak için kullanılacak.
```csharp
// Hücrelere örnek veri ekle
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Adım 5: Çalışma Sayfasına Bir Grafik Ekleyin
Şimdi, eklediğimiz verileri görselleştiren bir sütun grafiği oluşturalım.

Grafik türünü (sütun grafiği) belirliyoruz ve çalışma sayfasındaki boyutunu ve konumunu tanımlıyoruz.
```csharp
// Çalışma sayfasına bir sütun grafiği ekleyin
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Adım 6: Grafik Veri Kaynağını Tanımlayın
İşte sihir burada gerçekleşiyor: Tabloyu çalışma sayfasındaki verilere bağlamak!

Grafiği A1 ila B3 sütunlarındaki verilere bağlıyoruz. Bu, grafiğe verileri nereden çekeceğini söyler.
```csharp
// Tabloyu A1 ile B3 aralığındaki verilere bağlayın
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Adım 7: Grafiği Görüntüye Dönüştürün
Gerçek an: Bu grafiği bir görüntü dosyasına dönüştüreceğiz!

 Burada şunu kullanıyoruz:`ToImage` grafiği istediğiniz bir görüntü biçimine dönüştürme yöntemi. Bu durumda, onu bir EMF (Gelişmiş Meta Dosyası) biçimine dönüştürüyoruz.
```csharp
// Tabloyu bir görüntüye dönüştürün ve dizine kaydedin
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
Ve işte bu kadar! Grafiğiniz artık bir resim olarak kaydedildi. Kendinizi tebrik etme zamanı.
## Adım 8: Başarı Mesajını Göster
Konuyu toparlamak için, görüntü oluşturma işlemini doğrulayan bir mesaj gösterelim.
```csharp
// Başarıyı belirtmek için bir mesaj görüntüle
System.Console.WriteLine("Image generated successfully.");
```
## Çözüm
Pat! Aspose.Cells for .NET kullanarak Excel'den bir grafiği bir görüntüye dönüştürmek işte bu kadar kolay. Bu işlem yalnızca verilerin sunumunu basitleştirmekle kalmaz, aynı zamanda gömülü grafikler yerine görüntülerin tercih edildiği raporların veya panoların esnekliğini de artırır.
Bu kılavuzda özetlenen adımları izleyerek artık herhangi bir Excel grafiğini görüntüye dönüştürebilir, görsel verileri çeşitli uygulamalara sorunsuz bir şekilde entegre edebilirsiniz.
## SSS
### Bu yöntemi kullanarak farklı grafik türlerini dönüştürebilir miyim?
Evet, Aspose.Cells tarafından desteklenen pasta grafikleri, çubuk grafikleri, çizgi grafikleri ve daha fazlası dahil olmak üzere tüm grafik türlerini dönüştürebilirsiniz!
### Resim formatını değiştirmek mümkün mü?
 Kesinlikle! Bu örnekte EMF kullanmış olsak da, görüntü formatını PNG, JPEG, BMP ve diğerlerine basitçe değiştirerek değiştirebilirsiniz.`ImageFormat` parametre.
### Aspose.Cells yüksek çözünürlüklü görüntüleri destekliyor mu?
Evet, Aspose.Cells grafikleri görsellere aktarırken görüntü çözünürlüğünü ve kalite ayarlarını kontrol etmenize olanak tanır.
### Birden fazla grafiği tek seferde görsele dönüştürebilir miyim?
Evet, bir çalışma kitabındaki birden fazla grafik arasında dolaşabilir ve hepsini sadece birkaç satır kodla görsellere dönüştürebilirsiniz.
### Dönüştürebileceğim grafik sayısında bir sınırlama var mı?
Aspose.Cells tarafından dayatılan doğal bir sınır yoktur, ancak büyük miktarda verinin işlenmesi sisteminizin belleğine ve performans yeteneklerine bağlı olabilir.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
