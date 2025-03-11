---
title: Grafik Oluştur
linktitle: Grafik Oluştur
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells kullanarak .NET'te grafiklerin nasıl oluşturulacağını keşfedin. Çarpıcı görselleri zahmetsizce oluşturmak için adım adım eğitimimizi izleyin.
weight: 10
url: /tr/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafik Oluştur

## giriiş

Grafikler, veri sunumu ve analizinde temel bir unsurdur ve karmaşık bilgileri kolayca sindirilebilir hale getirir. .NET ile çalışıyorsanız ve grafikleri programatik olarak oluşturmanız gerekiyorsa, Aspose.Cells, Excel dosyalarını ve grafiklerini işlemek için sezgisel ve gelişmiş özellikler sağlayan güçlü bir kütüphanedir. Bu kılavuzda, .NET için Aspose.Cells kullanarak bir grafik oluşturma sürecini ele alacağız. İlgi çekici ve takip etmesi kolay olacak şekilde tasarlanmış bu ayrıntılı öğreticiye dalmaya hazır olun!

## Ön koşullar

Koda geçmeden önce her şeyin hazır olduğundan emin olalım. İhtiyacınız olanlar şunlar:

1. .NET Ortamı: .NET geliştirme ortamınızın kurulu olduğundan emin olun. Visual Studio veya .NET'i destekleyen herhangi bir IDE kullanabilirsiniz.
2.  .NET için Aspose.Cells: Aspose.Cells kütüphanesinin yüklü olması gerekir. Buradan indirebilirsiniz[Aspose'un yayın sayfası](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlamaya aşinalık, örnekleri daha iyi anlamanıza yardımcı olacaktır, ancak yeniyseniz endişelenmeyin; bu kılavuz her şeyi adım adım açıklayacaktır!

## Paketleri İçe Aktar

Kodlama yolculuğunuzdaki ilk adım gerekli paketleri içe aktarmaktır. Projenizi IDE'nizde açın ve aşağıdaki ad alanını ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Bu ad alanları, Aspose.Cells kütüphanesinin sunduğu işlevselliğe erişmenizi sağlayarak grafiklerinizi sorunsuz bir şekilde oluşturmanıza ve düzenlemenize olanak tanır.


Artık ön koşulları ve içe aktarmaları ele aldığımıza göre, bir grafiğin işlenmesinin inceliklerine dalalım! Bunu net, yönetilebilir adımlara böleceğiz.

## Adım 1: Çıktı Dizininizi Ayarlayın

Çalışma kitabımızı ve grafiğimizi oluşturmadan önce çıktılarımızın nereye kaydedileceğini belirlememiz gerekir. Bu şekilde, grafiğimiz oluşturulduğunda, onu tam olarak nerede bulacağınızı bilirsiniz.

```csharp
string outputDir = "Your Output Directory"; // Çıktı dizinini buraya belirtin.
```

"Çıktı Dizininiz" kısmını grafik görsellerinizi kaydetmek istediğiniz yol ile değiştirdiğinizden emin olun.

## Adım 2: Bir Çalışma Kitabı Oluşturun

Sonra, yeni bir çalışma kitabı başlatacağız. Tüm sihir burada gerçekleşiyor!

```csharp
Workbook workbook = new Workbook();
```

 Bu satır, yeni bir örnek oluşturur`Workbook` Sayfalar ve grafiklerle çalışmamıza olanak sağlayan sınıf.

## Adım 3: Yeni bir Çalışma Sayfası Ekleyin

Artık çalışma kitabımız olduğuna göre, yeni bir çalışma sayfası ekleme zamanı geldi. Çalışma sayfalarını, verilerinizi düzenli tutabileceğiniz bir not defterindeki farklı sayfalar olarak düşünün.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Burada yeni bir çalışma sayfası ekliyoruz ve ona bir referans elde ediyoruz. Verilerinizi ve grafiklerinizi girmek için bu çalışma sayfasıyla çalışacaksınız.

## Adım 4: Örnek Değerleri Girin

Çalışma sayfamız oluşturulduktan sonra hücrelere bazı örnek veriler ekleyelim. Bu veriler grafiğinizin dayanacağı verilerdir, bu yüzden grafik türünüz için mantıklı olan değerleri seçin!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Bu kod parçasında, "A1" ile "A3" arasındaki hücreleri bazı sayısal değerlerle ve "B1" ile "B3" arasındaki hücreleri başka bir değer kümesiyle dolduruyoruz. Bu sayıları ihtiyaçlarınıza uyacak şekilde özelleştirmekten çekinmeyin!

## Adım 5: Bir Grafik Oluşturun

Şimdi grafiğinizi oluşturma zamanı. Değerleri karşılaştırmak için harika olan bir sütun grafik türü ekleyeceğiz.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Burada, düzenini tanımlayarak belirtilen konuma bir grafik ekliyoruz: ilk sayı kümesi, grafiğin ızgaradaki konumunu temsil eder.

## Adım 6: Grafiğe Veri Serileri Ekleme

Oluşturulan tabloya göre şimdi bunu önceki adımlarda girdiğimiz verilerle ilişkilendirmemiz gerekiyor.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Bu çizgi, grafiğin veri serisini "A1" ile "B3" arasındaki hücrelerdeki değerlere bağlar. Bu, grafiğinizin verileri görsel olarak amaçlandığı gibi temsil edeceği anlamına gelir.

## Adım 7: Grafiği Görüntü Olarak Kaydedin

Şimdi grafiğimizi daha kolay paylaşılabilecek ve görüntülenebilecek bir resim formatına dönüştürelim.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

Bu adımda, grafiği belirtilen çıktı dizinine EMF (Gelişmiş Meta Dosyası) görüntüsü olarak kaydediyoruz. Ayrıca BMP veya PNG gibi farklı formatlarda da kaydedebilirsiniz.

## Adım 8: Grafiği Bitmap'e Dönüştür

Eğer bitmap'lerle çalışmayı tercih ediyorsanız, grafiğinizi Bitmap formatına nasıl dönüştürebileceğinizi burada bulabilirsiniz.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Bu, grafiğinizi bir BMP görüntüsü olarak kaydedecektir. Unutmayın, BMP dosyaları daha büyük olma eğilimindedir ancak inanılmaz derecede yüksek kalitededir!

## Adım 9: Gelişmiş Seçeneklerle İşleme

Ayrıca grafiği daha iyi kalite ve çözünürlük için bazı gelişmiş görüntü seçenekleriyle de oluşturabiliriz. Birkaç seçenek ayarlayalım:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Bu seçenekler, özellikle sunumlar veya yayınlar için ürettiğiniz görüntünün görsel kalitesini artırmaya yardımcı olur.

## Adım 10: Gelişmiş Seçeneklerle Grafiği Görüntüye Dönüştürün

Şimdi gelişmiş seçenekleri kullanarak grafiği dönüştürelim.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Bu, grafiğinizi gelişmiş kalite ayarlarıyla PNG dosyası olarak kaydeder.

## Adım 11: Tabloyu PDF'e Aktarma

Son olarak, eğer cilalı, kolayca paylaşılabilir bir belge istiyorsanız, grafiğinizi doğrudan PDF formatına aktarabilirsiniz.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Bu adım, grafiğinizi içeren bir PDF oluşturacaktır; bu da onu dijital raporlar hazırlamak veya meslektaşlarınızla paylaşmak için mükemmel hale getirir.

## Çözüm 

Tebrikler! Aspose.Cells for .NET kullanarak bir grafiği başarıyla oluşturdunuz. Bu güçlü kütüphane, Excel dosyalarının ve grafiklerinin oluşturulmasını ve işlenmesini basitleştirerek verilerinizi çok daha erişilebilir ve görsel olarak çekici hale getirir. İster raporlar, analizler veya sunumlar hazırlıyor olun, grafikler önemli bir etki yaratır ve Aspose ile bunları programatik olarak kolayca oluşturabilirsiniz.

## SSS

### Aspose.Cells for .NET ile hangi tür grafikler oluşturabilirim?
Sütun, çizgi, pasta ve çubuk grafikleri de dahil olmak üzere çeşitli grafikler oluşturabilirsiniz.

### Grafiklerin görünümünü özelleştirebilir miyim?
Evet, Aspose.Cells renkler, stiller ve grafik öğeleri de dahil olmak üzere kapsamlı özelleştirmeye olanak tanır.

### Ücretsiz deneme imkanı var mı?
Kesinlikle! Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.Cells için desteği nereden alabilirim?
 Topluluk desteği ve kaynaklarını şu adreste bulabilirsiniz:[Aspose Destek Forumu](https://forum.aspose.com/c/cells/9).

### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?
 Evet, deneme süresinin ötesinde sürekli kullanım için bir lisans gereklidir, ancak geçici bir lisans için başvuruda bulunabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
