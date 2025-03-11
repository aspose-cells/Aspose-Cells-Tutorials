---
title: Çalışma Sayfasında Bölmeleri Dondur'u Uygula
linktitle: Çalışma Sayfasında Bölmeleri Dondur'u Uygula
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu ayrıntılı, adım adım kılavuzla Aspose.Cells for .NET'i kullanarak Excel'de dondurma bölmelerini nasıl uygulayacağınızı öğrenin. Çalışma sayfanızın kullanılabilirliğini verimli bir şekilde artırın.
weight: 15
url: /tr/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfasında Bölmeleri Dondur'u Uygula

## giriiş
Büyük bir veri kümesine sahip bir Excel çalışma sayfanız olduğunu ve her aşağı veya yukarı kaydırdığınızda bu önemli başlıkların izini kaybettiğinizi hayal edin. Bu başlıklar kaydırırken yerinde kalabilseydi kullanışlı olmaz mıydı? İşte dondurma bölmeleri tam da burada devreye girerek gezinmeyi pürüzsüz ve verimli hale getirir. .NET için Aspose.Cells bu süreci basitleştirir ve dondurma bölmelerini sorunsuz bir şekilde uygulama gücü verir. Bu kılavuz sizi süreç boyunca yönlendirecek ve donmuş başlıkları hemen ayarlayabilmeniz için adım adım açıklayacaktır.
## Ön koşullar
Başlamadan önce birkaç şeyi hazır bulundurduğunuzdan emin olun:
-  Aspose.Cells for .NET Kütüphanesi: Bu kütüphaneyi şu adresten indirmeniz gerekecek:[Aspose'un sürüm sayfası](https://releases.aspose.com/cells/net/).
- .NET Framework Kurulu: Geliştirme ortamınızda .NET'in kurulu olduğundan emin olun.
- Temel C# Bilgisi: C# ile aşinalık takip etmenizde yardımcı olacaktır.
- Excel Dosyası: Dondurma bölmelerini uygulayacağınız bir Excel dosyanız hazır olsun (örneğin, “book1.xls”).
Aspose.Cells hakkında daha fazla ayrıntıyı şu adreste bulabilirsiniz:[dokümantasyon sayfası](https://reference.aspose.com/cells/net/).

## Paketleri İçe Aktar
Gerekli paketleri içe aktararak başlayalım. C# projenizi açın ve şunları içe aktardığınızdan emin olun:
```csharp
using System.IO;
using Aspose.Cells;
```
Paketler hazır olduğuna göre adım adım kılavuza geçelim.
Aspose.Cells for .NET kullanarak dondurma bölmelerini ayarlamanın her aşamasını ele alacağız. Her adımı dikkatlice takip edin ve dondurma bölmelerini çalışma sayfanıza zahmetsizce uygulayacaksınız.
## Adım 1: Belgeler Dizininize Giden Yolu Tanımlayın
 Excel dosyanızı açabilmeniz için belgenizin yolunu belirtmeniz gerekir.`dataDir` Dosyalarınızın dizin yolunu tutan değişken.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` Excel dosyalarınızın saklandığı gerçek yol ile. Bu, programın dosyanızı bulmasına yardımcı olacaktır.
## Adım 2: Excel Dosyasını FileStream Kullanarak Açın
Sonra, Aspose.Cells'in sihrini gösterebilmesi için Excel dosyasını yüklememiz gerekiyor. Bunu yapmak için bir dosya akışı oluşturacağız ve Excel dosyasını bu akışı kullanarak açacağız.
```csharp
// Açılacak Excel dosyasını içeren bir dosya akışı oluşturma
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Bir dosya akışı kullanarak, orijinal dosyayı açıkça kaydetmediğiniz sürece dosyayı Aspose.Cells'in erişimine açıyorsunuz.
## Adım 3: Çalışma Kitabı Nesnesini Örneklendirin
 Dosya akışı hazır olduğunda, bir dosya oluşturmanın zamanı geldi`Workbook` nesne. Bu nesne, Excel çalışma kitabınızın tamamını temsil ettiği ve dosya içindeki tek tek sayfalar, hücreler ve ayarlarla çalışmanıza olanak tanıdığı için önemlidir.
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
// Excel dosyasını dosya akışı aracılığıyla açma
Workbook workbook = new Workbook(fstream);
```
 Düşünün`Workbook` tüm sayfalarınızı bir arada tutan klasör olarak. Klasörü açtığınızda, içindeki herhangi bir sayfaya (çalışma kağıdı) erişebilirsiniz.
## Adım 4: İlk Çalışma Sayfasına Erişim
Artık çalışma kitabınız yüklendiğine göre, dondurma bölmelerinin hangi çalışma sayfasına uygulanacağını seçebilirsiniz. Bu örnekte, ilk sayfayla çalışacağız. Aspose.Cells, bir sayfayı dizinleyerek seçmeyi kolaylaştırır.
```csharp
// Excel dosyasındaki ilk çalışma sayfasına erişim
Worksheet worksheet = workbook.Worksheets[0];
```
 Farklı bir sayfada çalışmanız gerekiyorsa, dizini ayarlamanız yeterlidir.`workbook.Worksheets[0]`.
## Adım 5: Dondurma Bölmeleri Ayarlarını Uygula
 İşte sihir burada gerçekleşiyor! Dondurulmuş bölmeleri ayarlamak için şunu kullanın:`FreezePanes`dondurma işleminin hangi satır ve sütunda başlayacağını ve kaç satır ve sütunun dondurulacağını belirten yöntem.
```csharp
// Dondurma bölmeleri ayarlarının uygulanması
worksheet.FreezePanes(3, 2, 3, 2);
```
Parametreleri parçalayalım:
- Birinci Sıra (3): Dondurmaya 3. sıradan başlayın.
- Birinci Sütun (2): Dondurmayı 2. sütundan başlat.
- Satır Sayısı (3): 3 satırı dondur.
- Sütun Sayısı (2): 2 sütunu dondur.
Bu değerleri özel ihtiyaçlarınıza göre ayarlayın. Donma noktası belirtilen satır ve sütunun kesişimi olacaktır.
## Adım 6: Değiştirilen Excel Dosyasını Kaydedin
 Dondur bölmelerini uyguladıktan sonra, değişikliklerinizi kaydetme zamanı geldi. Değiştirilen çalışma kitabı dosyasını kaydetmek, dondurma ayarlarınızın korunmasını sağlar. Güncellenen dosyayı kullanarak kaydedebilirsiniz`Save` yöntem.
```csharp
// Değiştirilen Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xls");
```
Eğer orijinal dosyayı da korumak istiyorsanız, dosyayı farklı bir adla kaydettiğinizden emin olun.
## Adım 7: Dosya Akışını Kapatın
Son olarak, dosya akışını kapatmayı unutmayın. Bu, sistem kaynaklarını serbest bırakır ve dosyaya olan tüm açık bağlantıları sonlandırır.
```csharp
// Tüm kaynakları serbest bırakmak için dosya akışını kapatıyorum
fstream.Close();
```
Akışı kapatmayı, işiniz bittiğinde dosyayı rafa geri koymak olarak düşünün. Bu iyi bir ev idaresi alışkanlığıdır.

## Çözüm
Tebrikler! Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına dondurma bölmelerini başarıyla uyguladınız. Bu teknik, büyük veri kümelerini yönetmek, başlıklar veya belirli satır ve sütunların veriler arasında gezinirken görünür kalmasını sağlamak için inanılmaz derecede kullanışlıdır. Bu adım adım kılavuzu izleyerek, dondurma bölmelerini güvenle uygulayabilir ve elektronik tablolarınızın kullanılabilirliğini artırabilirsiniz.
## SSS
### Bir çalışma kitabında birden fazla sayfayı dondurabilir miyim?
 Evet, sadece tekrarlayın`FreezePanes` Her sayfaya uygulamak istediğiniz yöntemi yazın.
### Sayfanın aralığını aşan satır ve sütun değerleri kullanırsam ne olur?
Aspose.Cells bir istisna fırlatacaktır, bu nedenle değerlerinizin çalışma sayfasının sınırları içinde olduğundan emin olun.
### Dondurma bölmeleri ayarlarını uyguladıktan sonra değiştirebilir miyim?
 Kesinlikle! Sadece arayın`FreezePanes`Ayarları güncellemek için yeni parametrelerle yöntemi tekrar çalıştırın.
### Dondurma bölmesi Excel dosyalarının tüm sürümlerinde çalışır mı?
Evet, dondurma bölmeleri Aspose.Cells tarafından desteklenen çoğu Excel biçiminde (örneğin, XLS, XLSX) korunacaktır.
### Camları çözebilir miyim?
 Dondurulmuş bölmeleri kaldırmak için, sadece arayın`UnfreezePanes()` çalışma kağıdında.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
