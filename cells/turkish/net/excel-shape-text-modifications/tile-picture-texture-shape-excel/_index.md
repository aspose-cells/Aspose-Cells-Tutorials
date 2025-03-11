---
title: Excel'de Şekilde Doku Olarak Resim Döşeme
linktitle: Excel'de Şekilde Doku Olarak Resim Döşeme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kolay takip edilebilen, adım adım eğitimle, Aspose.Cells for .NET kullanarak Excel'de bir resmi doku olarak nasıl döşeyeceğinizi öğrenin.
weight: 13
url: /tr/net/excel-shape-text-modifications/tile-picture-texture-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Şekilde Doku Olarak Resim Döşeme

## giriiş
Excel çalışma sayfalarının görsel çekiciliğini artırmaya gelince, dokular olarak resim kullanmak gerçekten fark yaratabilir. Hiç sayılarla dolu sıkıcı bir Excel sayfasına bakıp daha ilgi çekici bir düzen istediğiniz oldu mu? Resimleri Excel'deki şekillere doku olarak uygulayarak, dikkat çeken ve bilgileri güzelce düzenleyen bir yaratıcılık öğesi ekleyebilirsiniz. Bu makalede, .NET için Aspose.Cells kullanarak Excel'de bir resmi bir şeklin içine doku olarak nasıl döşeyeceğinizi inceleyeceğiz. Bu kılavuz size adım adım talimatlar sağlayacak ve yeni başlayan biri olsanız bile takip etmenizi kolaylaştıracaktır.
## Ön koşullar
Başlamadan önce, yerinde olduğundan emin olmanız gereken birkaç şey var:
1. Visual Studio: Sisteminizde Visual Studio yüklü olmalıdır. Bu, kodu yazmak ve yürütmek için birincil IDE'miz olacaktır.
2.  Aspose.Cells for .NET: Bu kütüphane Excel dosyalarını düzenlemek için olmazsa olmazdır. Bunu şuradan indirebilirsiniz:[Aspose.Cells İndirmeler sayfası](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: Programımızı C# dilinde yazacağımız için söz dizimi ve yapı hakkında temel bir anlayışa sahip olmak faydalı olacaktır.
4. Örnek Excel Dosyası: Eğitimimiz için bir Excel örnek dosyası kullanacağız. Şekillerle basit bir Excel dosyası oluşturabilir veya Aspose web sitesinden bir örnek indirebilirsiniz.
## Paketleri İçe Aktar
Örneğe geçmeden önce, gerekli paketleri içe aktaralım. İşte ihtiyacımız olan şeylerin temel bir özeti:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Bu kod aktarımının her bir parçasını inceleyelim:
- `Aspose.Cells` Excel dosyalarını düzenlemek için kullandığımız temel kütüphanedir.
- `Aspose.Cells.Drawing` Excel'de şekillerle çalışırken gereklidir.
- `System` temel C# uygulamaları oluşturmak için standart bir kütüphanedir.
Artık her şeyi ayarladığımıza göre, Excel belgemizde bir resmi bir şeklin içine doku olarak döşeyerek başlayalım. Bunu ayrıntılı adımlara ayıracağız.
## Adım 1: Dizin Yollarını Ayarlayın
İlk önce kaynak ve çıktı dizinlerini ayarlamanız gerekir. Bu, Excel dosyanızın nerede bulunduğunu ve çıktıyı nereye kaydetmek istediğinizi belirtmenize yardımcı olacaktır.
```csharp
string sourceDir = "Your Document Directory"; // Gerçek dizininizle değiştirin
string outputDir = "Your Document Directory"; // Gerçek dizininizle değiştirin
```
 Bu kod parçacığında, şunu değiştirdiğinizden emin olun:`"Your Document Directory"` Bilgisayarınızda örnek Excel dosyasının saklandığı dizinlerin yolunu ve yeni dosyayı kaydetmek istediğiniz yeri belirtin.
## Adım 2: Örnek Excel Dosyasını Yükleyin
Sonra, düzenlemek istediğiniz şekli içeren Excel dosyasını yüklememiz gerekiyor. Bunu şu şekilde yapabilirsiniz:
```csharp
Workbook wb = new Workbook(sourceDir + "sampleTextureFill_IsTiling.xlsx");
```
 Bu adımda, bir örnek oluşturuyoruz`Workbook` sınıf ve Excel dosyamızın yolunu geçiriyoruz. Dosya`sampleTextureFill_IsTiling.xlsx` aşağıdaki adımlarla işleme alınacaktır.
## Adım 3: Çalışma Sayfasına Erişim
Çalışma kitabı yüklendikten sonra bir sonraki hedefimiz üzerinde çalışmak istediğimiz belirli çalışma sayfasına erişmektir. Aşağıdaki kodu kullanın:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Burada, çalışma kitabındaki ilk çalışma sayfasına erişiyoruz. Birden fazla çalışma sayfanız varsa ve belirli birine erişmek istiyorsanız, dizini istediğiniz çalışma sayfasına uyacak şekilde değiştirebilirsiniz.
## Adım 4: Şekle Erişim
Çalışma sayfasına eriştikten sonra, bir resimle doldurmak istediğimiz şekle ulaşma zamanı. Bu, şu kodla gerçekleştirilebilir:
```csharp
Shape sh = ws.Shapes[0];
```
Bu satırla belirtilen çalışma sayfasındaki ilk şekle erişiriz. Çalışma sayfasına erişime benzer şekilde, birden fazla şekliniz varsa ve belirli birini seçmek istiyorsanız dizin değerini değiştirebilirsiniz.
## Adım 5: Resmi Doku Olarak Döşeyin
Şimdi heyecan verici kısma geçelim! Resmi şeklin içine bir doku olarak döşeyeceğiz. İşte nasıl:
```csharp
sh.Fill.TextureFill.IsTiling = true;
```
 Ayarlayarak`IsTiling` true ise, şeklin dokuyu görüntüyü germek yerine tekrarlanan bir desende görüntülemesine izin veren döşeme özelliğini etkinleştiriyorsunuz. Bu, özellikle arka plan görselleri için elektronik tablolarınıza yaratıcılık katar.
## Adım 6: Çıktı Excel Dosyasını Kaydedin
Tüm değişiklikleri yaptıktan sonra, bir sonraki mantıksal adım çalışma kitabımızı yapılan değişikliklerle kaydetmektir. İşte nasıl:
```csharp
wb.Save(outputDir + "outputTextureFill_IsTiling.xlsx");
```
 Biz çağırıyoruz`Save` değişiklikleri adlı yeni bir dosyaya yazma yöntemi`outputTextureFill_IsTiling.xlsx` belirtilen çıktı dizininde.
## Adım 7: Onay Mesajı
Son olarak, kodumuzun düzgün çalıştığını doğrulamak için biraz geri bildirim almak her zaman iyidir. Şu satırı kullanabilirsiniz:
```csharp
Console.WriteLine("TilePictureAsTextureInsideShape executed successfully.\r\n");
```
Bu mesaj konsolunuzda görüntülenecek ve işlemin başarıyla gerçekleştirildiğini doğrulayacaktır.
## Çözüm
Ve işte karşınızda! Aspose.Cells for .NET kullanarak Excel'de bir şeklin içine bir resmi doku olarak döşemeyi başarıyla öğrendiniz. Bu teknik yalnızca elektronik tablolarınızın estetiğini geliştirmekle kalmaz, aynı zamanda Excel dosyalarını sorunsuz bir şekilde düzenleme konusunda Aspose.Cells'in gücünü ve esnekliğini de gösterir. Bu yüzden bir dahaki sefere bir Excel sayfasını canlandırmak istediğinizde, bu kullanışlı numarayı kullanmayı unutmayın! 
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, Microsoft Excel'e ihtiyaç duymadan Excel dosyaları oluşturmak, düzenlemek ve dönüştürmek için kullanılan bir .NET kütüphanesidir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, Aspose kütüphanenin özelliklerini kullanabileceğiniz ücretsiz bir deneme süresi sunuyor. Şunlara göz atın:[ücretsiz deneme bağlantısı](https://releases.aspose.com/).
### Birden fazla resmi doku olarak eklemek mümkün müdür?
Kesinlikle! Excel belgenizdeki çeşitli şekillere farklı dokular uygulamak için adımları tekrarlayabilirsiniz.
### Aspose.Cells kullanırken sorunlarla karşılaşırsam ne olur?
Herhangi bir sorun veya sorunuz varsa Aspose'un destek forumundan yardım alabilirsiniz.
### Aspose.Cells için lisansı nereden satın alabilirim?
 Lisansı doğrudan şu adresten satın alabilirsiniz:[Aspose satın alma sayfası](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
