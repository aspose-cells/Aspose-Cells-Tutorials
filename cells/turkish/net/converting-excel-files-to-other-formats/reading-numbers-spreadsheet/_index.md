---
"description": "Bu detaylı eğitimde Aspose.Cells for .NET kullanarak Numbers elektronik tablolarını nasıl okuyacağınızı ve bunları PDF'ye nasıl dönüştüreceğinizi öğrenin."
"linktitle": ".NET'te Sayısal Tabloları Programatik Olarak Okuma"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": ".NET'te Sayısal Tabloları Programatik Olarak Okuma"
"url": "/tr/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Sayısal Tabloları Programatik Olarak Okuma

## giriiş
Günümüzün dijital dünyasında, veri yönetimi hayati bir beceridir ve elektronik tablolar veri organizasyonunun ön saflarındadır. Peki ya .NET kullanarak bir Numbers elektronik tablosuyla (Apple'ın Numbers uygulaması tarafından oluşturulan dosyalar) çalışmanız gerekirse? Endişelenmeyin; yalnız değilsiniz! Bu eğitimde, .NET için Aspose.Cells ile bir Numbers elektronik tablosunu programatik olarak okuma sürecini ele alacağız. Bir Numbers dosyasını nasıl yükleyeceğinizi ve PDF'ye nasıl dönüştüreceğinizi öğreneceksiniz.
## Ön koşullar
Başlamadan önce, yerinde olması gereken birkaç şey var:
1. Aspose.Cells for .NET: Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. İndirebilirsiniz [Burada](https://releases.aspose.com/cells/net/).
2. Visual Studio: Bilgisayarınızda Visual Studio'nun (veya herhangi bir .NET uyumlu IDE'nin) yüklü olması önerilir.
3. Temel C# Bilgisi: C# programlamaya dair biraz bilgi sahibi olmak, konuyu rahatça takip etmenize yardımcı olacaktır.
4. Belge Dizininiz: Numbers dosyanızın saklandığı bir dizine ve dönüştürülen PDF'yi kaydedeceğiniz bir konuma ihtiyacınız olacak.
Bu ön koşulları yerine getirdiğinizde, başlamaya hazırsınız!
## Paketleri İçe Aktar
Başlamak için, gerekli paketleri C# projemize aktarmamız gerekiyor. Bu önemli bir adımdır çünkü Aspose.Cells kütüphanesinin sağladığı işlevselliklerden yararlanmamızı sağlar.
1. C# projenizi Visual Studio’da açın.
2. Aspose.Cells kütüphanesine bir referans ekleyin:
   - NuGet kullanıyorsanız, Paket Yöneticisi Konsolunda aşağıdaki komutu çalıştırmanız yeterlidir:
```
 Install-Package Aspose.Cells
 ```
3. Gerekli ad alanlarını kodunuza aktarın:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Artık gerekli paketleri içe aktardığımıza göre, Numbers elektronik tablosunu adım adım okuma kılavuzuna geçelim.
## Adım 1: Kaynak ve Çıktı Dizinlerini Belirleyin
Bu adımda, kaynak Numbers dosyanızın bulunduğu ve çıktı PDF'inizi kaydetmek istediğiniz dizinleri ayarlayacağız.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory"; // Bunu gerçek dizininize güncelleyin
// Çıktı dizini
string outputDir = "Your Document Directory"; // Bunu gerçek dizininize güncelleyin
```
Burada iki dize değişkeni tanımlıyoruz, `sourceDir` Ve `outputDir`, giriş ve çıkış dosyalarının konumlarını belirtmek için. Değiştirdiğinizden emin olun `"Your Document Directory"` sisteminizdeki gerçek yollarla.
## Adım 2: Sayılar Biçimi için Yükleme Seçeneklerini Ayarlayın
Sonra, Numbers elektronik tablosunu okumak için yükleme seçeneklerini belirteceğiz. Bu adım, Aspose'a Numbers dosyasını nasıl yorumlayacağını söylediği için önemlidir.
```csharp
// Yükleme seçeneklerini belirtin; Sayılar elektronik tablosunu yüklemek istiyoruz
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
Biz bir tane yaratıyoruz `LoadOptions` nesneyi seçin ve biçimini belirtin `LoadFormat.Numbers`Bu, Aspose.Cells kütüphanesine bir Numbers dosyasıyla çalıştığımızı söyler. 
## Adım 3: Sayılar E-Tablosunu bir Çalışma Kitabına Yükleyin
Şimdi, gerçek Sayılar elektronik tablosunu bir `Workbook` nesne.
```csharp
// Sayılar elektronik tablosunu yukarıdaki yükleme seçenekleriyle çalışma kitabına yükleyin
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
Bir örnek oluşturuyoruz `Workbook` nesneyi seçin ve Numbers dosyasının dosya yolunu yükleme seçeneklerimizle birlikte geçirin. Dosya adının (`sampleNumbersByAppleInc.numbers`) Numbers dosyanızın gerçek adıyla eşleşir.
## Adım 4: Çalışma Kitabını PDF olarak kaydedin
Numbers dosyası başarıyla yüklendikten sonraki adım onu farklı bir biçimde, özellikle PDF biçiminde kaydetmektir.
```csharp
// Çalışma kitabını PDF formatına kaydedin
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
Burada şunu diyoruz: `Save` yöntem üzerinde `Workbook` nesne, çıktı dosyası yolunu ve kaydetmek istediğimiz biçimi belirtir. Bu durumda, bunu PDF olarak kaydediyoruz. Çıktı dosyası adının (`outputNumbersByAppleInc.pdf`) benzersizdir ve mevcut dosyaların üzerine yazmaz.
## Adım 5: Başarılı Olduğunu Onaylayın
Son olarak işlemimizin başarılı olduğunu teyit eden bir mesaj ekleyelim.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Bu kod satırı her şey tamamlandığında konsola bir başarı mesajı yazdıracaktır. Geri bildirim almak her zaman iyidir, değil mi?
## Çözüm
Ve işte karşınızda! Aspose.Cells for .NET kullanarak bir Numbers elektronik tablosunu başarıyla okudunuz ve PDF'e dönüştürdünüz. Bu güçlü kütüphane, elektronik tabloları zahmetsizce düzenlemenizi sağlayarak veri yönetimi görevlerinizi kolaylaştırır. İster uygulamalar geliştiriyor olun, ister sadece elektronik tabloları daha verimli bir şekilde işlemeniz gereksin, Aspose.Cells araç setinizde bulunması gereken harika bir araçtır.
## SSS
### Aspose.Cells hangi dosya türlerini okuyabilir?  
Aspose.Cells, XLS, XLSX, CSV ve Numbers dosyaları da dahil olmak üzere çeşitli dosya biçimlerini okuyabilir. 
### Aspose.Cells kullanarak Numbers dosyalarını düzenleyebilir miyim?  
Evet, Aspose.Cells ile Numbers dosyalarını okuyabilir, düzenleyebilir ve kaydedebilirsiniz.
### Aspose.Cells'i kullanmak ücretsiz mi?  
Aspose.Cells ücretsiz deneme sunuyor ancak genişletilmiş kullanım için bir lisansa ihtiyacınız olacak. Fiyatlandırmayı kontrol edin [Burada](https://purchase.aspose.com/buy).
### Numbers dosyasını yüklerken bir hatayla karşılaşırsam ne yapmalıyım?  
Doğru yükleme seçeneklerini kullandığınızdan ve dosya yolunun doğru olduğundan emin olun. Daha fazla destek için şurayı ziyaret edin: [Aspose Destek Forumu](https://forum.aspose.com/c/cells/9).
### Aspose.Cells için geçici lisansı nasıl alabilirim?  
Geçici lisans başvurusunda bulunabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}