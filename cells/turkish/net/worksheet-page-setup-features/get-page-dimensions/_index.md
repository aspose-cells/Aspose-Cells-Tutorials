---
"description": "Aspose.Cells for .NET ile bir Excel çalışma sayfasında sayfa boyutlarının nasıl alınacağını öğrenin. A2, A3, A4 ve Letter kağıt boyutlarını özelleştirmek için adım adım bir kılavuz."
"linktitle": "Çalışma Sayfasının Sayfa Boyutlarını Alın"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Çalışma Sayfasının Sayfa Boyutlarını Alın"
"url": "/tr/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Sayfasının Sayfa Boyutlarını Alın

## giriiş
Aspose.Cells for .NET kullanarak Excel dosyalarıyla programatik olarak çalışıyorsanız, bir çalışma sayfasının sayfa boyutlarına erişmeniz ve bunları ayarlamanız gereken zamanlar olabilir. Boyutları bilmek, belirli amaçlar için Excel sayfalarının düzenleri, yazdırılması ve özelleştirilmesi konusunda yardımcı olabilir. Bu makalede, Aspose.Cells for .NET kullanarak Excel'de çeşitli sayfa boyutlarının nasıl alınacağını ve görüntüleneceğini inceleyeceğiz. Başlamak için tüm ayrıntılara sahip olduğunuzdan emin olmak için adım adım bir öğreticiyi ele alacağız.
## Ön koşullar
Başlamadan önce, bu eğitimi takip etmek için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.
1. Aspose.Cells for .NET: Aspose.Cells for .NET'in yüklü olduğundan emin olun. [kütüphaneyi buradan indirin](https://releases.aspose.com/cells/net/) veya NuGet aracılığıyla .NET projenize yükleyin.
2. .NET Ortamı: Uyumlu bir .NET geliştirme ortamı (örneğin, Visual Studio).
3. Lisans Kurulumu: Aspose.Cells'in tüm işlevselliği için bir lisans uygulayın. [ücretsiz geçici lisans talebinde bulunun](https://purchase.aspose.com/temporary-license/) değerlendirme amaçlı.
Eğer Aspose.Cells'i ilk defa değerlendiriyorsanız, ücretsiz deneme sürümüyle başlayın.
## Paketleri İçe Aktar
Koda geçmeden önce, gerekli tüm sınıflara ve yöntemlere erişmek için Aspose.Cells ad alanını projenize aktarmanız gerekir.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
İşlemi kolay adımlara bölelim. Burada, farklı kağıt boyutlarına erişeceğiz, bunları bir çalışma sayfasına uygulayacağız ve her birinin boyutlarını yazdıracağız.
## Adım 1: Bir Çalışma Kitabı Örneği Oluşturun
İlk adım, bir örnek oluşturmaktır `Workbook` sınıf. Bu nesne, üzerinde değişiklik yapabileceğimiz çalışma sayfalarını içeren ana çalışma kitabımız gibi davranacaktır.
```csharp
Workbook book = new Workbook();
```
Düşünün `Workbook` Excel dosyanız için ana kapsayıcı olarak. Bireysel çalışma sayfalarına erişmek ve bunları kontrol etmek için buna ihtiyacımız var.
## Adım 2: İlk Çalışma Sayfasına Erişim
Sonra, çalışma kitabındaki ilk çalışma sayfasına erişelim. Varsayılan olarak, yeni bir çalışma kitabı bir sayfayla gelir, bu nedenle bir dizin kullanarak doğrudan başvurabiliriz `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
The `Worksheets` koleksiyonda `Workbook` her çalışma sayfasına dizine göre erişmemizi sağlar. Burada, sayfa boyutlarını ayarlamaya başlamak için ilk sayfayı alıyoruz.
## Adım 3: Kağıt Boyutunu A2 Olarak Ayarlayın ve Boyutları Görüntüleyin
Artık çalışma sayfamıza erişebildiğimize göre, kağıt boyutunu A2 olarak ayarlayalım. Sayfa boyutunu ayarlamak, yazdırmadan veya dışa aktarmadan önce sayfayı biçimlendirmek için kullanışlıdır. Kağıt boyutunu ayarladıktan sonra, sayfa boyutlarını inç cinsinden yazdıracağız.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Burada, şunu değiştiriyoruz: `PaperSize` mülk `PaperA2`Boyutu ayarladıktan sonra, `PageSetup.PaperWidth` Ve `PageSetup.PaperHeight` Sayfanın genişliğini ve yüksekliğini inç cinsinden alın. Bu bize sayfa boyutlarına dair hızlı bir genel bakış sağlar.
## Adım 4: Kağıt Boyutunu A3 Olarak Ayarlayın ve Boyutları Görüntüleyin
Yukarıdaki adımların aynısını izleyerek sayfa boyutlarını A3 boyutuna ayarlayalım. Bu değişiklik biraz daha büyük baskılar veya bir sayfaya daha fazla içerik sığdırmak için kullanışlıdır.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 boyutu A4 boyutunun iki katıdır, bu da onu büyük tablolar veya ayrıntılı grafikler için iyi bir seçim yapar. Kağıt boyutunu değiştirmek, çalışma sayfası düzenini buna göre uyarlamaya yardımcı olur.
## Adım 5: Kağıt Boyutunu A4 Olarak Ayarlayın ve Boyutları Görüntüleyin
Şimdi kağıt boyutunu A4 olarak ayarlayalım. Bu, belgeleri yazdırmak için en yaygın kullanılan sayfa boyutudur. Güncellenmiş boyutları daha sonra göstereceğiz.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Hedefiniz standart bir belge formatıysa, A4 genellikle en uygun boyuttur. Boyutları bilmek, yazdırma sorunlarından kaçınmak için içerik düzenini ayarlamanıza yardımcı olabilir.
## Adım 6: Kağıt Boyutunu Letter ve Ekran Boyutlarına Ayarlayın
Son olarak, kağıt boyutunu Kuzey Amerika'da yaygın olarak kullanılan Letter formatına ayarlayacağız. Boyutları son kez yazdıralım.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Kuzey Amerika'daki belgeler için Letter boyutu yaygın olarak kullanılır, dolayısıyla bu boyutu ayarlamak oradaki ekiplerle veya müşterilerle işbirliği yaparken işinize yarar.
## Çözüm
Bu eğitimde, Aspose.Cells for .NET kullanarak farklı kağıt boyutları için sayfa boyutlarının nasıl ayarlanacağını ve alınacağını ele aldık. A2, A3, A4 ve Letter gibi sayfa boyutlarını yapılandırarak, Excel çalışma sayfalarını belirli yazdırma ve düzen ihtiyaçlarına uyacak şekilde biçimlendirebilirsiniz. Sayfa boyutları üzerindeki bu kontrol, içeriğinizin her sayfa boyutuna mükemmel şekilde uymasını sağladığı için profesyonel raporlama ve sunum için özellikle değerlidir.
## SSS
### Aspose.Cells'de sayfanın yönünü nasıl değiştirebilirim?  
Yönlendirmeyi kullanarak değiştirebilirsiniz. `PageSetup.Orientation` mülk, onu ikisinden birine ayarlayarak `PageOrientationType.Pveyatrait` or `PageOrientationType.Landscape`.
### Aspose.Cells'de özel sayfa boyutları ayarlayabilir miyim?  
Evet, kenar boşluklarını ve ölçekleme seçeneklerini ayarlayarak özel sayfa boyutları belirleyebilirsiniz. `PageSetup` Daha fazla kontrol için.
### Aspose.Cells'de varsayılan kağıt boyutu nedir?  
Varsayılan kağıt boyutu genellikle A4'tür. Ancak bu, bölgesel ayarlara bağlı olabilir ve ihtiyaç halinde ayarlanabilir.
### Aspose.Cells'te sayfa düzenlerini önizlemek mümkün mü?  
Aspose.Cells grafiksel önizleme sunmasa da, Excel'de düzenleri programlı olarak ayarlayabilir ve baskı önizlemelerini kullanabilirsiniz.
### Aspose.Cells for .NET'i nasıl kurarım?  
Aspose.Cells'i Visual Studio'daki NuGet Paket Yöneticisi'ni kullanarak yükleyebilir veya DLL'yi şu adresten indirebilirsiniz: [Aspose.Cells indirme sayfası](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}