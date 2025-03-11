---
title: Çalışma Sayfasının Kağıt Boyutunun Otomatik Olup Olmadığını Kontrol Edin
linktitle: Çalışma Sayfasının Kağıt Boyutunun Otomatik Olup Olmadığını Kontrol Edin
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET'i kullanarak bir çalışma sayfasının kağıt boyutunun otomatik olup olmadığını nasıl kontrol edeceğinizi ayrıntılı adım adım kılavuzumuzda keşfedin.
weight: 11
url: /tr/net/worksheet-page-setup-features/check-automatic-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfasının Kağıt Boyutunun Otomatik Olup Olmadığını Kontrol Edin

## giriiş
Elektronik tabloları yönetme ve yazdırma için mükemmel bir biçimde biçimlendirilmelerini sağlama söz konusu olduğunda, dikkate alınması gereken kritik bir husus kağıt boyutu ayarlarıdır. Bu kılavuzda, .NET için Aspose.Cells kullanarak bir çalışma sayfasının kağıt boyutunun otomatik olarak ayarlanıp ayarlanmadığını nasıl kontrol edeceğinizi inceleyeceğiz. Bu kitaplık, Excel ile ilgili tüm ihtiyaçlarınız için güçlü araçlar sunarak işinizi yalnızca kolaylaştırmakla kalmaz, aynı zamanda daha verimli hale getirir.
## Ön koşullar
Gerçek kodlamaya dalmadan önce, her şeyin ayarlandığından emin olalım. İşte ihtiyacınız olan ön koşullar:
1. C# Geliştirme Ortamı: Visual Studio gibi bir C# IDE'ye ihtiyacınız var. Henüz yüklemediyseniz, Microsoft web sitesine gidin.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine sahip olduğunuzdan emin olun. Bunu şu adresten indirebilirsiniz:[bu bağlantı](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlama kavramlarına aşinalık, örnekleri ve kod parçacıklarını etkili bir şekilde anlamanıza yardımcı olacaktır.
4. Örnek Excel Dosyaları: Gerekli sayfa düzenine sahip örnek Excel dosyalarınızın olduğundan emin olun. Örneğimiz için iki dosyaya ihtiyacınız olacak:
- `samplePageSetupIsAutomaticPaperSize-False.xlsx`
- `samplePageSetupIsAutomaticPaperSize-True.xlsx`
Bu ön koşullara sahip olmak, Aspose.Cells'in sunduğu işlevselliği keşfederken sizi başarıya hazırlayacaktır.
## Paketleri İçe Aktar
Başlamak için, C# projenize gerekli paketleri içe aktarmanız gerekir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:
### Yeni Bir C# Projesi Oluşturun
- Visual Studio'yu açın ve yeni bir C# Konsol Uygulaması oluşturun.
-  Buna şöyle bir isim verin:`CheckPaperSize`.
### Aspose.Cells Referansını Ekle
- Çözüm Gezgini’nde projenizin üzerine sağ tıklayın.
- "NuGet Paketlerini Yönet" seçeneğini seçin.
- "Aspose.Cells"i arayın ve yükleyin.
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Her şeyi ayarladıktan sonra artık eğlenceli kısma geçmeye hazırsınız!
Şimdi süreci yönetilebilir adımlara bölelim.
## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın
Öncelikle örnek Excel dosyalarımızın nerede bulunduğunu ve çıktıları nereye kaydetmek istediğimizi belirtmemiz gerekiyor. 
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` örnek Excel dosyalarınızın saklandığı gerçek yol ile. Bu, programın çalışması için ihtiyaç duyduğu dosyaları bulması için önemlidir.
## Adım 2: Çalışma Kitaplarını Yükleyin
Daha sonra, daha önce hazırladığımız iki çalışma kitabını yükleyeceğiz. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
// Otomatik kağıt boyutu yanlış olan ilk çalışma kitabını yükle
Workbook wb1 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-False.xlsx");
// Otomatik kağıt boyutu doğru olan ikinci çalışma kitabını yükleyin
Workbook wb2 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-True.xlsx");
```
İki çalışma kitabını belleğe yüklüyoruz. İlk çalışma kitabının otomatik kağıt boyutu özelliği devre dışı olacak şekilde ayarlanmışken, ikincisinde etkinleştirilmiş. Bu kurulum, bunları daha sonra kolayca karşılaştırmamızı sağlar.
## Adım 3: Çalışma Sayfalarına Erişim
Şimdi her iki çalışma kitabındaki ilk çalışma sayfasına erişip kağıt boyutu ayarlarını kontrol edeceğiz.
```csharp
// Her iki çalışma kitabının ilk çalışma sayfasına erişin
Worksheet ws11 = wb1.Worksheets[0];
Worksheet ws12 = wb2.Worksheets[0];
```
Her iki çalışma kitabından da ilk çalışma sayfasına (indeks 0) erişerek, incelemek istediğimiz ilgili sayfalara odaklanıyoruz. 
## Adım 4: IsAutomaticPaperSize Özelliğini Kontrol Edin
 Bir an durup kontrol edelim`IsAutomaticPaperSize` Her çalışma sayfasından özellik.
```csharp
// Her iki çalışma sayfasının PageSetup.IsAutomaticPaperSize özelliğini yazdırın
Console.WriteLine("First Worksheet of First Workbook - IsAutomaticPaperSize: " + ws11.PageSetup.IsAutomaticPaperSize);
Console.WriteLine("First Worksheet of Second Workbook - IsAutomaticPaperSize: " + ws12.PageSetup.IsAutomaticPaperSize);
```
 Burada, her çalışma sayfasının otomatik kağıt boyutu özelliğinin etkin olup olmadığını yazdırıyoruz. Özellik`IsAutomaticPaperSize` ayarı belirten bir Boole değeri (doğru veya yanlış) döndürür.
## Adım 5: Son Çıktı ve Onay
Son olarak programımızın sonuçlarını bağlamına oturtalım ve başarılı bir şekilde yürütüldüğünü doğrulayalım.
```csharp
Console.WriteLine();
Console.WriteLine("DetermineIfPaperSizeOfWorksheetIsAutomatic executed successfully.\r\n");
```
Ayarları yazdırdıktan sonra programımızın sorunsuz çalıştığını belirten bir başarı mesajı yazdırıyoruz.
## Çözüm
Bu eğitimde, Excel dosyalarındaki çalışma sayfalarının kağıt boyutu ayarının Aspose.Cells for .NET kullanılarak otomatik olarak ayarlanıp ayarlanmadığını nasıl kontrol edeceğinizi ele aldık. Bu adımları izleyerek, artık Excel dosyalarını programatik olarak kolayca düzenlemek ve kağıt boyutu gibi belirli yapılandırmaları kontrol etmek için temel becerilere sahipsiniz. 
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, .NET uygulamalarında Excel belge biçimlerini düzenlemek için tasarlanmış güçlü bir kütüphanedir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, Aspose ücretsiz deneme sürümü sunuyor. İndirebilirsiniz[Burada](https://releases.aspose.com/).
### Aspose.Cells için lisans nasıl satın alabilirim?
 Satın alma sayfalarından lisans satın alabilirsiniz[Burada](https://purchase.aspose.com/buy).
### Aspose.Cells'i kullanarak hangi tür Excel dosyalarıyla çalışabilirim?
XLS, XLSX, CSV ve daha birçok Excel formatıyla çalışabilirsiniz.
### Aspose.Cells için desteği nerede bulabilirim?
 Destek forumları ve kaynakları bulabilirsiniz[Burada](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
