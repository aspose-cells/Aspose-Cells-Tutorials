---
title: .NET'te Programlı Olarak Konsolidasyon Fonksiyonları
linktitle: .NET'te Programlı Olarak Konsolidasyon Fonksiyonları
second_title: Aspose.Cells .NET Excel İşleme API'si
description: .NET için Aspose.Cells'i kullanarak konsolidasyon fonksiyonlarını programlı olarak nasıl uygulayacağınızı öğrenin. Veri analizi görevlerinizi verimli bir şekilde otomatikleştirin.
weight: 12
url: /tr/net/creating-and-configuring-pivot-tables/consolidation-functions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Programlı Olarak Konsolidasyon Fonksiyonları

## giriiş
Veri analizi için Excel'in gücünden yararlanmak istiyor ancak bununla ilgili sıkıcı süreçleri otomatikleştirmek mi istiyorsunuz? Doğru yerdesiniz! Bu makalede, özellikle birleştirme işlevlerine odaklanarak .NET için Aspose.Cells dünyasına dalıyoruz. Tekrarlayan görevlere saatler harcamadan verilerinizi kolayca analiz edebildiğinizi ve özetleyebildiğinizi hayal edin.
## Ön koşullar
Veri analizi yolculuğumuza başlamadan önce, her şeyin yerli yerinde olduğundan emin olalım. İhtiyacınız olanlar şunlar:
1. .NET Ortamı: Çalışan bir .NET ortamınız olmalı. .NET Core veya .NET Framework kullanıyor olmanız fark etmeksizin, adımlar büyük ölçüde aynı kalacaktır.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesinin yüklü olması gerekir. Bunu şuradan kolayca indirebilirsiniz:[Aspose sürüm sayfası](https://releases.aspose.com/cells/net/).
3. C#'ın Temel Anlayışı: C# programlamaya biraz aşinalık faydalı olacaktır. Zaten C#'da kod yazıyorsanız, hazırsınız!
4. Örnek Excel Dosyası: Örneğimiz için, adında bir Excel dosyanız olduğundan emin olun.`Book.xlsx` Belgeler dizininizde hazır.
## Paketleri İçe Aktar
Kodlamaya başlamak için öncelikle gerekli paketleri içe aktarmanız gerekir. Projenizde Aspose.Cells kütüphanesine başvurulması gerekir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
1.  NuGet Paketini Yükleyin: Projenizi Visual Studio'da açın, Çözüm'e sağ tıklayın ve "NuGet Paketlerini Yönet"i seçin.`Aspose.Cells` ve kuruluma basın.
2. Yönergeyi Kullanma: C# dosyanızın en üstüne, ihtiyaç duyduğumuz sınıflara erişmek için aşağıdaki ad alanlarını eklemeniz gerekir:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Şimdi konsolidasyon fonksiyonlarımızı uygulamaya geçelim!
Şimdi, ana programımızı net, sindirilebilir adımlara böleceğiz. Hazır mısınız? Hadi başlayalım!
## Adım 1: Belge Dizininizi Ayarlayın
Öncelikle belgelerimiz için bir yol belirlememiz gerekiyor. Bu, Excel dosyalarınızın saklandığı klasörü ifade eder.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Değiştirdiğinizden emin olun`"Your Document Directory"` gerçek yolunuzla`Book.xlsx` dosya bulunur.
## Adım 2: Bir Çalışma Kitabı Örneği Oluşturun
Sonra, kaynak Excel dosyamızdan bir çalışma kitabı örneği oluşturalım. Bu nesne, içindeki verilerle etkileşime girmemizi sağlayacaktır.`Book.xlsx`.
```csharp
// Kaynak excel dosyasından çalışma kitabı oluştur
Workbook workbook = new Workbook(dataDir + "Book.xlsx");
```
Burada çalışma kitabını yükleyerek içindeki sayfalara ve verilere erişebiliyoruz.
## Adım 3: İlk Çalışma Sayfasına Erişim
Çalışma kitabımız olduğunda, pivot tablomuzun bulunduğu çalışma sayfasına erişmemiz gerekir. Burada, bunun ilk çalışma sayfası olduğunu varsayıyoruz.
```csharp
// Çalışma kitabının ilk çalışma sayfasına erişin
Worksheet worksheet = workbook.Worksheets[0];
```
Bu kod satırı ilk sayfayı alır ve doğrudan üzerinde çalışmamıza olanak tanır.
## Adım 4: Pivot Tablosuna Erişim
Harika! Şimdi çalışmak istediğimiz pivot tabloyu bulmamız gerekiyor. Bu örnek için çalışma sayfamızın ilk pivot tablosuna erişeceğiz.
```csharp
// Çalışma sayfasının ilk pivot tablosuna erişin
PivotTable pivotTable = worksheet.PivotTables[0];
```
Bu adımın başarılı olması için Excel dosyanızın gerçekten bir pivot tablo içerdiğinden emin olun.
## Adım 5: Konsolidasyon Fonksiyonlarını Uygula
Şimdi konsolidasyon fonksiyonlarını uygulama zamanı! İlk veri alanı için ortalamayı hesaplayalım ve ikinci veri alanı için farklı girişleri sayalım.
```csharp
// Ortalama konsolidasyon fonksiyonunu ilk veri alanına uygulayın
pivotTable.DataFields[0].Function = ConsolidationFunction.Average;
// İkinci veri alanına DistinctCount konsolidasyon işlevini uygulayın
pivotTable.DataFields[1].Function = ConsolidationFunction.DistinctCount;
```
Sonuçların nasıl değiştiğini görmek için bu fonksiyonları farklı alanlarla karıştırmayı deneyin.
## Adım 6: Değişiklikleri Hesaplayın
Fonksiyonlarınızı ayarladıktan sonra, yaptığımız değişiklikleri yansıtacak şekilde verileri hesaplamak çok önemlidir. Bu, Excel çalışma sayfanızdaki 'yenile' düğmesine basmak gibidir.
```csharp
// Değişikliklerin etki etmesini sağlamak için verileri hesaplayın
pivotTable.CalculateData();
```
Bu adımı, yudum almadan önce kahvenizin demlendiğinden emin olmak olarak düşünün. Sonuçları kaçırmak istemezsiniz!
## Adım7: Değişikliklerinizi Kaydedin
 Son olarak, çalışmamızı kaydetme zamanı geldi. Değiştirilen çalışma kitabını yeni bir Excel dosyasına kaydedeceğiz.`output.xlsx`.
```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xlsx");
```
Ve işte! .NET'te Aspose.Cells kütüphanesini kullanarak verileri başarıyla birleştirdiniz.
## Çözüm
Aspose.Cells for .NET kullanarak fonksiyonları birleştirmeye ilişkin eğitimimizin sonuna geldiniz! Bu süreç size sadece zaman kazandırmakla kalmaz, aynı zamanda üretkenliğinizi de artırır. Bu yeni edinilen bilgiyi alıp veri analizi görevlerinizde birleştirme fonksiyonlarının çeşitli kullanımlarını keşfedebilirsiniz. Görüşlerinizi yorumlarda paylaşmayı unutmayın ve sorularınız varsa çekinmeden bize ulaşabilirsiniz.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin uygulamalarında Excel dosyalarını programlı bir şekilde oluşturmalarına, düzenlemelerine ve yönetmelerine olanak tanıyan bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, Aspose bulabileceğiniz ücretsiz bir deneme sunuyor[Burada](https://releases.aspose.com).
### Aspose.Cells belgelerine nasıl erişebilirim?
 Kapsamlı belgelere erişebilirsiniz[Burada](https://reference.aspose.com/cells/net/).
### Aspose.Cells için destek mevcut mu?
 Kesinlikle! Onların yardımına başvurabilirsiniz[destek forumu](https://forum.aspose.com/c/cells/9).
### Aspose.Cells için lisansı nereden satın alabilirim?
 Lisans satın alabilirsiniz[Burada](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
