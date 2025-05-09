---
"description": "Aspose.Cells for .NET kullanarak Excel grafiğinizle bir PDF oluşturun. Bu adım adım kılavuzla nasıl yapacağınızı öğrenin."
"linktitle": "İstenilen Sayfa Boyutunda Grafik PDF'i Oluşturun"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "İstenilen Sayfa Boyutunda Grafik PDF'i Oluşturun"
"url": "/tr/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# İstenilen Sayfa Boyutunda Grafik PDF'i Oluşturun

## giriiş

Görsel olarak çekici ve bilgilendirici grafikler oluşturmak, çeşitli alanlardaki veri temsili için olmazsa olmazdır. İster satış verileriyle, ister performans ölçümleriyle veya başka herhangi bir bilgi türüyle uğraşıyor olun, yüksek kaliteli grafikler üretme becerisine sahip olmak bulgularınıza derinlik ve netlik kazandırır. .NET uygulamalarıyla çalışıyorsanız, Aspose.Cells Excel belgelerini yönetmeyi ve grafikler oluşturmayı kolaylaştıran güçlü bir kütüphanedir. Bu eğitimde, istediğiniz sayfa boyutuna sahip bir Excel dosyasından bir grafiğin PDF'sini oluşturma sürecinde size rehberlik edeceğiz.

## Ön koşullar

Koda dalmadan önce, sorunsuz bir deneyim sağlamak için yerine getirmeniz gereken birkaç ön koşul vardır:

### C# ve .NET'in Temel Bilgileri

C# programlama ve .NET framework hakkında temel bir anlayışa ihtiyacınız olacak. Bu, bu kılavuzda karşılaşacağınız kodun yapısını kavramanıza yardımcı olacaktır.

### .NET için Aspose.Cells

Aspose.Cells for .NET'in yüklü olduğundan emin olun. Tüm ayrıntıları şu adreste bulabilirsiniz: [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/). 

### Geliştirme Ortamı

Geliştirme ortamınızı kurun. Bu, Visual Studio veya C# destekleyen herhangi bir IDE olabilir. Aspose.Cells kütüphanesini şuradan indirin ve yükleyin: [indirme sayfası](https://releases.aspose.com/cells/net/).

### Örnek Excel Dosyası

En az bir grafik içeren bir örnek Excel dosyasına ihtiyacınız olacak. Bu eğitim boyunca kullanmak için bir örnek dosya oluşturabilir veya indirebilirsiniz.

## Paketleri İçe Aktar

Aspose.Cells ile çalışmaya başlamak için, C# uygulamanıza gerekli ad alanlarını içe aktarmanız gerekir. Bunu şu şekilde yapabilirsiniz:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Bu ad alanları, Excel çalışma kitaplarını ve içeriklerini yönetmek için gereken sınıflara ve yöntemlere erişmenizi sağlar.

Artık tüm ön koşulları hallettiğimize göre, süreci ayrıntılı adımlara bölelim.

## Adım 1: Çıktı ve Kaynak Dizinlerini Ayarlayın

Başlamak için çıktı PDF'inizin nereye kaydedileceğini ve kaynak Excel belgenizin nerede bulunduğunu tanımlamanız gerekir.

```csharp
//Çıktı dizini
string outputDir = "Your Output Directory";

//Kaynak dizini
string sourceDir = "Your Document Directory";
```

"Çıktı Dizininiz" ve "Belge Dizininiz"i sisteminizdeki gerçek yollarla değiştirdiğinizden emin olun. Bu, Aspose'un oluşturulan PDF'yi nereye kaydedeceğini ve Excel dosyasını nerede bulacağını belirler.

## Adım 2: Örnek Excel Dosyasını Yükleyin

Sonra, grafiği içeren Excel dosyasını yüklemeniz gerekir. İşte nasıl:

```csharp
//Tabloyu içeren örnek Excel dosyasını yükleyin.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

The `Workbook` sınıf, Excel belgenizle etkileşim kurmanız için merkezi öneme sahiptir. Yolun Excel dosyanıza doğru bir şekilde işaret ettiğinden emin olun; buradaki bir hata, kodun geri kalanının yürütülmesini engelleyecektir.

## Adım 3: İlk Çalışma Sayfasına Erişim

Çalışma kitabı yüklendikten sonraki adım, istenen grafiği içeren çalışma sayfasına erişmektir.

```csharp
//İlk çalışma sayfasına erişin.
Worksheet ws = wb.Worksheets[0];
```

Aspose.Cells'de çalışma sayfaları sıfırdan başlayarak dizinlenir, bu nedenle `Worksheets[0]` ilk sayfaya atıfta bulunur.

## Adım 4: İlk Tabloya Erişim

Şimdi, PDF'e aktarmak istediğiniz grafiğe erişelim. Bu adım, çalışma sayfanızın en az bir grafik içerdiğini varsayar.

```csharp
//Çalışma kağıdının içindeki ilk grafiğe erişin.
Chart ch = ws.Charts[0];
```

Tekrar ediyorum, bu çalışma sayfasındaki ilk grafiğe erişim sağlar; çalışma sayfanızın yapısının bu yaklaşıma uygun olduğundan emin olun.

## Adım 5: İstenilen Sayfa Boyutunda PDF Oluşturun

Son olarak, belirtilen sayfa boyutuyla grafikten PDF oluşturma zamanı. İşte her şeyi yapan sihirli kod satırı:

```csharp
//İstediğiniz sayfa boyutunda grafik pdf'i oluşturun.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

Bu kodda:
- PDF daha önce belirttiğiniz çıktı dizinine kaydedilecektir.
- Sayılar `7, 7` sırasıyla istenilen sayfa boyutunun genişliğini ve yüksekliğini temsil eder.
- PageLayoutAlignmentType.Center, grafiğin sayfada ortalanmasını sağlar.

## Adım 6: Onay Mesajı

Her şeyin yolunda gittiğini kendinize (ve başkalarına) bildirmek için kodunuzun sonuna bir onay mesajı ekleyin:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

İşlem tamamlandığında konsol penceresinde bu mesaj görünecek ve PDF'nizin sorunsuz bir şekilde oluşturulduğunu bildirecektir.

## Çözüm

Tebrikler! Excel dosyasında bulunan bir grafikten PDF oluşturmak için Aspose.Cells for .NET'i nasıl kullanacağınızı öğrendiniz. Bu güçlü kütüphane, Excel belgelerini düzenleme ve verilerin görsel temsillerini oluşturma sürecini basitleştirir ve saatlerce süren manuel biçimlendirmeden tasarruf etmenizi sağlar. Aspose.Cells'in yalnızca PDF oluşturmanın ötesinde sunduğu diğer özellikleri keşfetmeyi unutmayın; projelerinizi daha da geliştirebilecek şeyleri asla bilemezsiniz!

## SSS

### Aspose.Cells for .NET ne için kullanılır?  
Aspose.Cells for .NET, .NET uygulamalarında Excel belgelerini programlı olarak oluşturmak, düzenlemek ve dönüştürmek için kullanılır.

### Aspose.Cells'i ücretsiz kullanabilir miyim?  
Evet, Aspose.Cells bir [ücretsiz deneme](https://releases.aspose.com/) değerlendirme amaçlı.

### Deneme süremi başlangıç süresinin ötesine uzatmanın bir yolu var mı?  
Başvuruda bulunabilirsiniz [geçici lisans](https://purchase.aspose.com/temporary-license/) Genişletilmiş testler için.

### Ya sorunlarla karşılaşırsam veya sorularım olursa?  
Aspose topluluğundan yardım isteyebilirsiniz [destek forumu](https://forum.aspose.com/c/cells/9).

### Aspose.Cells'i nasıl satın alabilirim?  
Aspose.Cells'i şu adresten satın alabilirsiniz: [satın alma sayfası](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}