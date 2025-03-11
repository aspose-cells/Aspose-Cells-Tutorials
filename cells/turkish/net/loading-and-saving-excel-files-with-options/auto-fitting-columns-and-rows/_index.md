---
title: Çalışma Kitabında HTML Yüklenirken Sütunları ve Satırları Otomatik Olarak Sığdır
linktitle: Çalışma Kitabında HTML Yüklenirken Sütunları ve Satırları Otomatik Olarak Sığdır
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak HTML'yi Excel'e yüklerken sütunları ve satırları otomatik olarak nasıl sığdıracağınızı öğrenin. Adım adım kılavuz dahildir.
weight: 10
url: /tr/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabında HTML Yüklenirken Sütunları ve Satırları Otomatik Olarak Sığdır

## giriiş
Aspose.Cells for .NET kullanarak bir Excel çalışma kitabına HTML içeriği yüklerken sütun ve satır boyutlarını otomatik olarak nasıl ayarlayacağınızı hiç merak ettiniz mi? Doğru yerdesiniz! Bu eğitimde, bir HTML tablosunu bir çalışma kitabına nasıl yükleyebileceğinizi ve sütunların ve satırların içerikle eşleşecek şekilde otomatik olarak sığdırılmasını nasıl sağlayabileceğinizi derinlemesine inceleyeceğiz. Sık sık değişen dinamik verilerle çalışıyorsanız, bu kılavuz HTML'den iyi biçimlendirilmiş Excel sayfaları oluşturmak için başvuracağınız rehber olacaktır.
### Ön koşullar
Koda geçmeden önce sisteminizde birkaç şeyi ayarlamanız gerekiyor. Endişelenmeyin, basit ve anlaşılır!
1. Visual Studio Kurulu: Visual Studio veya herhangi bir .NET geliştirme ortamına ihtiyacınız olacak.
2.  Aspose.Cells for .NET: Şunları yapabilirsiniz[en son sürümü indirin](https://releases.aspose.com/cells/net/) veya NuGet paket yöneticisini kullanarak kurulumunu yapabilirsiniz.
3. .NET Framework: .NET Framework 4.0 veya üzeri sürümün yüklü olduğundan emin olun.
4. C# Temel Anlayışı: C# hakkında biraz bilgi sahibi olmak bu eğitimi sizin için daha akıcı hale getirecektir.
5. HTML Tablo Verileri: Excel'e yüklemek istediğiniz bazı HTML içeriklerini (hatta basit bir tabloyu) hazırlayın.
## Paketleri İçe Aktar
İlk önce ilk şeyler—başlamak için gerekli ad alanlarını içe aktaralım. İçe aktarmanız gerekenlerin basit bir listesi şöyle:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Bu paketler çalışma kitabını yönetmenize, HTML verilerini düzenlemenize ve bunları sorunsuz bir şekilde Excel'e yüklemenize olanak tanır.
Bu süreci kolayca takip edebilmeniz için yönetilebilir parçalara bölelim. Bunun sonunda, .NET için Aspose.Cells kullanarak bir çalışma kitabına HTML yüklerken sütunları ve satırları otomatik olarak nasıl sığdıracağınıza dair çalışan bir örneğiniz olacak.
## Adım 1: Belge Dizinini Ayarlayın
Dosyaları kolayca kaydetmek ve geri almak için, belgelerinizin depolanacağı yolu belirteceğiz. Dizin yolunu kendi klasör konumunuzla değiştirebilirsiniz.
```csharp
string dataDir = "Your Document Directory";
```
Bu satır Excel dosyalarınızın kaydedileceği dizini belirler. Birden fazla proje üzerinde çalışırken dosyalarınızı düzgün bir şekilde organize etmek önemlidir. Bunu projenizin dosya dolabı olarak düşünün!
## Adım 2: HTML Verilerini Bir Dize Olarak Oluşturun
Sonra, bazı temel HTML içeriklerini tanımlayacağız. Bu örnek için basit bir HTML tablosu kullanacağız. Bunu projenizin ihtiyaçlarına göre özelleştirebilirsiniz.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Burada çok temel bir HTML dizesi tanımlıyoruz. Birkaç satır ve sütundan oluşan bir tablo içeriyor. İhtiyaçlarınıza göre daha fazla satır veya sütun ekleyebilirsiniz. Bunu bir yemeği pişirmeden önce malzemeleri hazırlamak olarak düşünün!
## Adım 3: HTML Dizesini MemoryStream'e Yükleyin
 Artık HTML içeriğimiz hazır olduğuna göre, bir sonraki adım onu kullanarak belleğe yüklemektir.`MemoryStream`Bu, HTML içeriğini önce diske kaydetmeden bellekte düzenlememize olanak tanır.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 HTML dizesini bir bayt dizisine dönüştürerek ve bunu bir`MemoryStream`, bellekteki HTML verileriyle çalışabiliriz. Bu adımı, yemeği fırına koymadan önce tencerede hazırlamak olarak düşünün!
## Adım 4: MemoryStream'i bir Çalışma Kitabına Yükleyin (Otomatik Sığdırma Olmadan)
 HTML içeriğini hafızaya aldığımızda, bunu bir Aspose'a yükleriz`Workbook`Bu noktada, henüz sütunları ve satırları otomatik olarak yerleştirmiyoruz. Bu, daha sonra otomatik olarak yerleştirilmiş sürümle karşılaştıracağımız "önceki" senaryomuzdur.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Çalışma kitabı HTML içeriğiyle yüklenir, ancak sütunlar ve satırlar henüz metne otomatik olarak sığdırılmaz. Bunu bir kek pişirmek ama sıcaklığı kontrol etmeyi unutmak olarak düşünün; işe yarıyor, ancak mükemmel olmayabilir!
## Adım 5: Otomatik Sığdırma Etkinken HTML Yükleme Seçeneklerini Belirleyin
 Şimdi, işte sihir! Bir örnek oluşturuyoruz`HtmlLoadOptions` ve etkinleştirin`AutoFitColsAndRows` özellik. Bu, HTML içeriği yüklendiğinde sütunların ve satırların içlerindeki içeriğe uyacak şekilde ayarlanmasını sağlar.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Bu seçeneği ayarlayarak, Aspose.Cells'e satırları ve sütunları otomatik olarak yeniden boyutlandırmasını söylüyoruz. Bunu, fırını kekin tam kıvamında kabarması için mükemmel sıcaklığa ayarlamak gibi düşünün!
## Adım 6: Otomatik Sığdırma Etkinleştirilmiş Olarak Çalışma Kitabına HTML Yükleyin
 Şimdi HTML içeriğini tekrar yüklüyoruz, ancak bu sefer`AutoFitColsAndRows`seçeneği etkinleştirildi. Bu, sütun genişliklerini ve satır yüksekliklerini içlerindeki içeriğe göre ayarlayacaktır.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Bu adım HTML içeriğini yeni bir çalışma kitabına yükler ve Excel dosyası olarak kaydeder, ancak şimdi sütunlar ve satırlar otomatik olarak sığdırılır! Bunu, her şeyin tam doğru boyutta olduğu mükemmel pişmiş bir pasta olarak düşünün.
## Çözüm
Bu basit adımları izleyerek, .NET için Aspose.Cells kullanarak bir çalışma kitabına HTML içeriği yüklemeyi ve sütunları ve satırları otomatik olarak sığdırmayı öğrendiniz. Bu, içerik ne kadar dinamik olursa olsun Excel sayfalarınızın her zaman düzenli görünmesini sağlar. Excel verilerinizi biçimlendirme ve düzenlemede size tonlarca zaman kazandırabilecek basit ama güçlü bir özelliktir.
Artık bu bilgiye sahip olduğunuza göre, daha karmaşık HTML içerikleriyle deneyler yapabilir, stil ekleyebilir ve hatta web sayfalarından komple Excel çalışma kitapları oluşturabilirsiniz!
## SSS
### Büyük HTML tablolarını yüklemek için bu yöntemi kullanabilir miyim?
Evet, Aspose.Cells büyük HTML tablolarını verimli bir şekilde yönetir, ancak en iyi performans için veri boyutlarınızla test yapmanız önerilir.
### Otomatik sığdırmadan sonra belirli sütun genişliklerini ve satır yüksekliklerini manuel olarak uygulayabilir miyim?
Kesinlikle! Otomatik sığdırma özelliğini kullandıktan sonra bile, tek tek sütunları ve satırları özelleştirebilirsiniz.
### HTML'i yükledikten sonra tabloyu nasıl biçimlendirebilirim?
HTML'yi yükledikten sonra Aspose.Cells'in kapsamlı stil seçeneklerini kullanarak stiller uygulayabilirsiniz.
### Aspose.Cells for .NET, .NET Framework'ün eski sürümleriyle uyumlu mudur?
Evet, Aspose.Cells for .NET, .NET Framework 4.0 ve sonraki sürümlerini destekler.
### Aspose.Cells kullanarak Excel'e HTML dışında başka içerik türleri de yükleyebilir miyim?
Evet, Aspose.Cells CSV, JSON ve XML gibi çeşitli formatların Excel'e yüklenmesini destekler.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
