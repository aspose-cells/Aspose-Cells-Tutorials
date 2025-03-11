---
title: .NET için Aspose.Cells kullanarak Satırları Kopyala
linktitle: .NET için Aspose.Cells kullanarak Satırları Kopyala
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel dosyalarındaki satırları nasıl verimli bir şekilde kopyalayacağınızı öğrenin. Bu adım adım kılavuz, veri yönetimi ihtiyaçlarınız için satır kopyalamayı basitleştirir.
weight: 11
url: /tr/net/row-and-column-management/copying-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET için Aspose.Cells kullanarak Satırları Kopyala

## giriiş
.NET ortamında Excel dosyalarıyla çalışıyorsanız, Aspose.Cells for .NET bilmek isteyeceğiniz güçlü bir araçtır. Bununla, yeni çalışma sayfaları oluşturma, hücreleri biçimlendirme ve hatta satırları sorunsuz bir şekilde kopyalama gibi görevleri otomatikleştirebilirsiniz. Büyük veri kümelerini veya şablon satırlarını zahmetsizce tekrarlamayı hayal edin—Aspose.Cells for .NET bu görevleri çocuk oyuncağı haline getirir! Bu eğitimde, belirli bir göreve odaklanacağız: Excel dosyasındaki satırları kopyalama. Ön koşulları, gerekli paketleri içe aktarmayı ve bu süreci kolaylaştırmak için adım adım bir kılavuzu ele alacağız. Hadi başlayalım!
## Ön koşullar
Koda geçmeden önce ihtiyacınız olanlar şunlardır:
1.  Aspose.Cells for .NET: En son sürüme sahip olduğunuzdan emin olun.[buradan indirin](https://releases.aspose.com/cells/net/) veya[ücretsiz deneme alın](https://releases.aspose.com/).
2. Geliştirme Ortamı: Visual Studio gibi herhangi bir .NET uyumlu ortam.
3. C# Temel Bilgileri: Bu rehber başlangıç seviyesindekilere yönelik olsa da, C# ile ilgili bilgi sahibi olmak her adımı daha iyi anlamanıza yardımcı olacaktır.
4.  Lisans: Tam erişim için bir tane edinin[geçici lisans](https://purchase.aspose.com/temporary-license/) eğer gerekirse.
## Paketleri İçe Aktar
Başlamak için, kodunuza gerekli ad alanlarını içe aktardığınızdan emin olun. Bu kütüphaneler, Excel dosyalarını işlemek için gereken sınıflara ve yöntemlere erişmenizi sağlayacaktır.
```csharp
using System.IO;
using Aspose.Cells;
```
Kodu basit adımlara bölelim. Her adım, bir Excel çalışma kitabını açmaktan kopyalanan satırlarla güncellenmiş dosyayı kaydetmeye kadar sizi süreçte yönlendirecektir.
## Adım 1: Dizininizin Yolunu Ayarlayın
İlk önce, Excel dosyalarınızın bulunduğu dizin yolunu ayarlamamız gerekiyor. Bunu, programın üzerinde çalışılacak dosyaları nerede bulacağını bilmesi için çalışma alanını ayarlamak olarak düşünün.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` Excel dosyanızın bulunduğu makinenizdeki gerçek yol ile (`book1.xls`) saklanır.
## Adım 2: Mevcut Excel Dosyasını Açın
 Artık yol ayarlandığına göre Excel dosyasını programımıza yükleyelim.`Workbook` Aspose.Cells sınıfından Excel dosyamızı kolayca açabilir ve erişebiliriz.
```csharp
// Mevcut Excel dosyasını açın.
Workbook excelWorkbook1 = new Workbook(dataDir + "book1.xls");
```
 Burada,`excelWorkbook1` artık tüm verileri içeren çalışma kitabı nesnenizdir`book1.xls`Bu, bu dosya içindeki çalışma sayfaları, hücreler ve satırlarla çalışmamızı sağlar.
## Adım 3: İstenilen Çalışma Sayfasına Erişim
Çalışma kitabı açıkken, bir sonraki adım satır kopyalama işlemini gerçekleştirmek istediğiniz çalışma sayfasını seçmektir. Bu örnekte, çalışma kitabındaki ilk çalışma sayfasıyla çalışacağız.
```csharp
// Çalışma kitabındaki ilk çalışma kağıdını al.
Worksheet wsTemplate = excelWorkbook1.Worksheets[0];
```
 The`Worksheets[0]` index ilk çalışma sayfasını seçer. Verileriniz farklı bir çalışma sayfasındaysa, dizini buna göre ayarlayın.
## Adım 4: Hedef Satırı Kopyalayın
Şimdi eğitimimizin temel kısmına geliyoruz: bir satırı kopyalamak. Burada, verileri aynı çalışma sayfasında satır 2'den (dizin 1, çünkü satırlar sıfır dizinlidir) satır 16'ya (dizin 15) kopyalayacağız.
```csharp
// Veriler, biçimlendirmeler, resimler ve çizim nesnelerinin bulunduğu ikinci satırı 16. satıra kopyalayın.
wsTemplate.Cells.CopyRow(wsTemplate.Cells, 1, 15);
```
Bu komutta:
- Kaynak Satırı (1): Bu, Excel'deki 2. satıra karşılık gelen kopyaladığımız satırdır.
- Hedef Satır (15): Kopyalanan satırın yapıştırılmasını istediğimiz yer burasıdır, Excel'deki 16. satıra karşılık gelir.
 The`CopyRow` Bu yöntem etkilidir; yalnızca verileri değil, aynı zamanda o satırdaki tüm biçimlendirmeleri, görüntüleri veya nesneleri de kopyalar.
## Adım 5: Güncellenen Excel Dosyasını Kaydedin
Satır kopyalama işlemi tamamlandıktan sonra, değiştirilmiş Excel dosyasını kaydetme zamanı gelir. Bu, yapılan tüm değişikliklerin`excelWorkbook1` korunmaktadır.
```csharp
// Excel dosyasını kaydedin.
excelWorkbook1.Save(dataDir + "output.xls");
```
 Burada güncellenen çalışma kitabını şu şekilde kaydediyoruz:`output.xls` orijinal dosyayla aynı dizinde. Gerekirse dosya adını ve konumunu değiştirebilirsiniz.
## Çözüm
Ve işte karşınızda! Sadece birkaç satır kodla, .NET için Aspose.Cells kullanarak Excel'de bir satırı başarıyla kopyaladınız. Bu eğitim, belge yolunu ayarlamaktan güncellenmiş dosyanızı kaydetmeye kadar temel adımları kapsar. İster satırları kopyalıyor, ister hücreleri biçimlendiriyor veya büyük veri kümelerini işliyor olun, Aspose.Cells Excel manipülasyonunu kolaylaştırır. Yani, bir dahaki sefere verileri satırlar arasında kopyalamanız gerektiğinde, bunu tam olarak nasıl yapacağınızı bileceksiniz.
## SSS
### Aspose.Cells for .NET kullanarak birden fazla satırı aynı anda kopyalayabilir miyim?  
 Evet, satırlar arasında dolaşabilir ve şunu kullanabilirsiniz:`CopyRow` birden fazla satırı kopyalamak için döngü içindeki yöntem.
### Farklı çalışma sayfaları arasında satırları nasıl kopyalarım?  
Kaynak ve hedef çalışma sayfalarını belirtmeniz yeterlidir.`CopyRow` yöntem. Bu yöntem aynı çalışma kitabındaki farklı çalışma sayfalarında çalışır.
### Aspose.Cells for .NET kopyalama sırasında satır biçimlendirmesini koruyor mu?  
 Kesinlikle!`CopyRow` yöntem verileri, biçimlendirmeyi, görüntüleri ve hatta çizim nesnelerini kopyalar.
### Aspose.Cells for .NET, .NET Core ile uyumlu mudur?  
Evet, Aspose.Cells .NET Framework, .NET Core ve .NET Standard'ı destekleyerek farklı .NET ortamlarında esneklik sağlar.
### Aspose.Cells for .NET'i kullanmak için lisansa ihtiyacım var mı?  
 Ücretsiz bir deneme sürümü mevcut olsa da,[geçici veya tam lisans](https://purchase.aspose.com/buy) Tam işlevsellik ve tüm sınırlamaların kaldırılması için önerilir.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
