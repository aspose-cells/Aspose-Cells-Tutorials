---
title: Aspose.Cells ile Excel'de Satır ve Sütunların Gruplandırılmasını Kaldırma
linktitle: Aspose.Cells ile Excel'de Satır ve Sütunların Gruplandırılmasını Kaldırma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kapsamlı kılavuzla Aspose.Cells for .NET kullanarak Excel'de satır ve sütunların gruplarını nasıl çözeceğinizi öğrenin. Excel veri işlemenizi basitleştirin.
weight: 15
url: /tr/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'de Satır ve Sütunların Gruplandırılmasını Kaldırma

## giriiş
Excel dosyalarını ele alırken, satır ve sütunları gruplandırmamanız gereken durumlarla karşılaşabilirsiniz. İster bir elektronik tabloyu temizleyin, ister daha iyi sunum için verileri yeniden biçimlendirin, Aspose.Cells for .NET süreci basitleştiren harika bir araçtır. Bu eğitimde, Aspose.Cells kullanarak Excel'de satır ve sütunları gruplandırmama adımlarında size rehberlik edeceğim. Sonunda, Excel dosyalarıyla programatik olarak nasıl çalışılacağına dair sağlam bir anlayışa sahip olacaksınız.
## Ön koşullar
Koda dalmadan önce her şeyin ayarlandığından emin olalım. İhtiyacınız olanlar şunlar:
1.  Visual Studio: Makinenizde çalışan bir Visual Studio sürümü yüklü olmalıdır. Eğer henüz yoksa, şuradan indirebilirsiniz:[Visual Studio'nun sitesi](https://visualstudio.microsoft.com/).
2. .NET için Aspose.Cells: Aspose.Cells kütüphanesini indirmeniz gerekecek. Bunu şuradan alabilirsiniz:[Aspose Sürümleri sayfası](https://releases.aspose.com/cells/net/) . Gerekli lisanslara sahip olduğunuzdan emin olun; bunlar satın alınabilir veya bir[geçici lisans](https://purchase.aspose.com/temporary-license/).
3. Temel C# Bilgisi: C# programlamanın temellerini anlamak, konuyu daha kolay takip etmenize yardımcı olacaktır.
Her şey hazır olduğunda, eğlenceli kısma, yani kod kısmına geçebiliriz!
## Paketleri İçe Aktar
Başlamak için, C# projenize gerekli paketleri içe aktarmanız gerekir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
1. Projenizi Visual Studio’da açın.
2. Aspose.Cells kütüphanesine bir referans ekleyin. Bunu projenizdeki Referanslar'a sağ tıklayıp Referans Ekle'yi seçerek yapabilirsiniz. Aspose.Cells DLL'sini kaydettiğiniz konuma gidin.
3. C# dosyanızın en üstüne aşağıdaki using yönergelerini ekleyin:
```csharp
using System.IO;
using Aspose.Cells;
```
Artık her şey ayarlandığına göre, Excel sayfanızdaki satır ve sütunları gruplandırmayı kaldırma adımlarını inceleyelim. 
## Adım 1: Belge Dizinini Tanımlayın
Öncelikle Excel dosyanızın bulunduğu dizini belirtmeniz gerekir. Bunu şu şekilde ayarlayabilirsiniz:
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` Excel dosyasının bilgisayarınızda kaydedildiği gerçek yol. 
## Adım 2: Bir Dosya Akışı Oluşturun
Sonra, Excel dosyasını açmak için bir dosya akışı oluşturmanız gerekir. Bunu şu şekilde yapabilirsiniz:
```csharp
// Açılacak Excel dosyasını içeren bir dosya akışı oluşturma
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Burada, adlı dosyayı açıyorsunuz`book1.xls`Bu dosyanın belirttiğiniz dizinde bulunduğundan emin olun, aksi takdirde dosya bulunamadı hatasıyla karşılaşırsınız.
## Adım 3: Bir Çalışma Kitabı Nesnesi Oluşturun
Şimdi Excel dosyasını bir Çalışma Kitabı nesnesine yükleyelim. Bu, çalışma kitabını programatik olarak düzenlemenizi sağlar:
```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
// Excel dosyasını dosya akışı aracılığıyla açma
Workbook workbook = new Workbook(fstream);
```
Bu kod satırıyla Excel dosyasını belleğe başarıyla yüklediniz ve artık onunla çalışmaya hazırsınız.
## Adım 4: Çalışma Sayfasına Erişim
Çalışma kitabına sahip olduktan sonraki adım, satırları ve sütunları gruplandırmayı kaldırmak istediğiniz belirli çalışma sayfasına erişmektir. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
// Excel dosyasındaki ilk çalışma sayfasına erişim
Worksheet worksheet = workbook.Worksheets[0];
```
Bu durumda, ilk çalışma sayfasına erişiyoruz. Verileriniz farklı bir sayfadaysa, dizini buna göre değiştirebilirsiniz.
## Adım 5: Satırları Gruplandırmayı Kaldır
Şimdi heyecan verici kısım geliyor! İlk altı satırı (0. satırdan 5. satıra) gruplandıralım. Aşağıdaki kodu kullanın:
```csharp
// İlk altı satırın gruplandırılması (0'dan 5'e)
worksheet.Cells.UngroupRows(0, 5);
```
Bu yöntem belirtilen satırlara uygulanan herhangi bir gruplamayı kaldırır. İşte bu kadar kolay!
## Adım 6: Sütunları Gruplandırmayı Kaldır
Tıpkı satırlar gibi, sütunları da gruplandırabilirsiniz. İşte ilk üç sütunu (sütun 0'dan sütun 2'ye) gruplandırmanın nasıl yapılacağı:
```csharp
// İlk üç sütunu gruplandırma (0'dan 2'ye)
worksheet.Cells.UngroupColumns(0, 2);
```
## Adım 7: Değiştirilen Excel Dosyasını Kaydedin
 Satırları ve sütunları gruplandırmayı kaldırdıktan sonraki adım, değişiklikleri bir Excel dosyasına geri kaydetmektir. Bunu, şunu kullanarak yapabilirsiniz:`Save` yöntem:
```csharp
// Değiştirilen Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xls");
```
 Bu örnekte, değiştirilen dosyayı şu şekilde kaydediyoruz:`output.xls`Dosya adını istediğiniz gibi değiştirebilirsiniz.
## Adım 8: Dosya Akışını Kapatın
Son olarak kaynakları serbest bırakmak için dosya akışını kapatmalısınız:
```csharp
// Tüm kaynakları serbest bırakmak için dosya akışını kapatıyorum
fstream.Close();
```
Bu, uygulamanızın dosya tanıtıcılarını gereğinden uzun süre tutmamasını sağlamak için iyi bir uygulamadır.
## Çözüm
Ve işte karşınızda! Aspose.Cells for .NET kullanarak bir Excel dosyasındaki satır ve sütunları gruplandırmayı başarıyla öğrendiniz. Sadece birkaç satır kodla Excel dosyalarınızda programatik olarak önemli değişiklikler yapabilirsiniz. İster raporları otomatikleştirin, ister analiz için veri hazırlayın, bu tekniklerde ustalaşmak size bir ton zaman kazandırabilir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, .NET uygulamalarında Excel dosyalarıyla çalışmak için güçlü bir kütüphanedir ve elektronik tabloların kolayca düzenlenmesine, dönüştürülmesine ve oluşturulmasına olanak tanır.
### Excel'deki satır ve sütunları diğer kütüphaneleri kullanarak gruplandırabilir miyim?
Evet, .NET'te Excel düzenleme için kullanılabilen başka kütüphaneler de var, ancak Aspose.Cells kapsamlı özellikler ve kullanım kolaylığı sunuyor.
### Kaydettikten sonra değişiklikleri geri almanın bir yolu var mı?
Bir Excel dosyasını kaydettikten sonra, orijinal dosyanın bir yedeğine sahip olmadığınız sürece önceki durumu geri yükleyemezsiniz.
### Aspose.Cells için desteği nasıl alabilirim?
 Ziyaret ederek destek alabilirsiniz.[Aspose Destek forumu](https://forum.aspose.com/c/cells/9)Sorularınızı sorabileceğiniz ve çözüm bulabileceğiniz yer.
### Lisans olmadan Aspose.Cells'i kullanabilir miyim?
Evet, Aspose.Cells'i belirli sınırlamalarla ücretsiz olarak kullanabilirsiniz ve bir başlangıç yapabilirsiniz.[geçici lisans](https://purchase.aspose.com/temporary-license/) tam işlevsellik için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
