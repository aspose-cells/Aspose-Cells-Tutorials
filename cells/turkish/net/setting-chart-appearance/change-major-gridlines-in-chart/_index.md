---
title: Grafikteki Ana Kılavuz Çizgilerini Değiştir
linktitle: Grafikteki Ana Kılavuz Çizgilerini Değiştir
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Ayrıntılı adım adım kılavuzumuzla Aspose.Cells for .NET'i kullanarak Excel grafiklerindeki ana kılavuz çizgilerini nasıl değiştireceğinizi öğrenin.
weight: 11
url: /tr/net/setting-chart-appearance/change-major-gridlines-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafikteki Ana Kılavuz Çizgilerini Değiştir

## giriiş

Excel'de görsel olarak çekici grafikler oluşturmak, etkili veri sunumu için olmazsa olmazdır. İster veri analisti, ister proje yöneticisi veya sadece veri görselleştirmeyle ilgilenen biri olun, grafiklerin nasıl özelleştirileceğini anlamak raporlarınızı önemli ölçüde iyileştirebilir. Bu makalede, .NET için Aspose.Cells kitaplığını kullanarak bir Excel grafiğindeki ana kılavuz çizgilerini nasıl değiştireceğinizi öğreneceğiz.

## Ön koşullar

Başlamadan önce, Aspose.Cells ile çalışırken sorunsuz bir deneyim sağlamak için yerinde olması gereken birkaç şey var:

- Visual Studio: Bilgisayarınızda Visual Studio'nun yüklü olduğundan emin olun. Kodunuzu burada yazacak ve çalıştıracaksınız.
-  .NET için Aspose.Cells: Aspose.Cells'in en son sürümünü şu adresten indirebilirsiniz:[web sitesi](https://releases.aspose.com/cells/net/) Satın almadan önce denemek istiyorsanız, bir üyeliğe kaydolmayı düşünebilirsiniz.[ücretsiz deneme](https://releases.aspose.com/).
- Temel C# Bilgisi: C# programlamaya aşina olmak, bu eğitimdeki örnekleri takip etmenizi kolaylaştıracaktır.

Her şeyi ayarladıktan sonra kodumuzu yazmaya başlayabiliriz!

## Paketleri İçe Aktar

Aspose.Cells ile çalışmak için ilk adım, gerekli paketleri C# projenize içe aktarmaktır. Visual Studio projenizi açın ve C# dosyanızın en üstüne aşağıdaki using yönergelerini ekleyin:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Bu paketler, Excel çalışma kitapları ve grafikleri oluşturmak ve değiştirmek için ihtiyaç duyacağınız sınıflara ve yöntemlere erişmenizi sağlar.

Şimdi, süreci detaylı ve takip etmesi kolay adımlara bölelim. Bazı verilerle basit bir grafik oluşturacağız ve ardından ana kılavuz çizgilerinin rengini değiştireceğiz.

## Adım 1: Çıktı Dizininizi Ayarlayın

Yapmak isteyeceğiniz ilk şey çıktı Excel dosyasını nereye kaydetmek istediğinizi tanımlamaktır. Bu, kodunuzda bir dizin yolu belirterek yapılır:

```csharp
// Çıktı dizini
string outputDir = "Your Output Directory"; // İstediğiniz yolla güncelleyin
```

 Yer değiştirmek`"Your Output Directory"` dosyanızı kaydetmek istediğiniz gerçek yol ile.

## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturun

 Daha sonra, yeni bir örnek oluşturmanız gerekir`Workbook` sınıf. Bu nesne Excel dosyanızı temsil edecek ve içeriğini düzenlemenize olanak tanıyacaktır.

```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```

Bu kod satırı, çalışma sayfamız ve grafiğimiz için boş bir tuval sağlayacak yeni bir çalışma kitabı başlatır.

## Adım 3: Çalışma Sayfasına Erişim

 Çalışma kitabını oluşturduktan sonra, varsayılan çalışma sayfasına erişebilirsiniz. Aspose.Cells'deki çalışma sayfaları dizinlenmiştir, bu nedenle ilk çalışma sayfasını istiyorsanız, ona dizine göre başvurursunuz`0`.

```csharp
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[0];
```

## Adım 4: Çalışma Sayfasını Örnek Verilerle Doldurun

Çalışma sayfası hücrelerine, grafiğimiz için veri görevi görecek bazı örnek değerler ekleyelim. Bu önemlidir çünkü grafik bu verilere başvuracaktır.

```csharp
// Hücrelere örnek değerler ekleme
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Burada, belirli hücrelere birkaç sayısal değer giriyoruz. "A" ve "B" sütunları görselleştireceğimiz veri noktalarını tutar.

## Adım 5: Çalışma Sayfasına Bir Grafik Ekleyin

Verilerimiz yerli yerindeyken, bir grafik oluşturmanın zamanı geldi. Veri setimizi görselleştiren bir sütun grafiği ekleyeceğiz.

```csharp
// Çalışma sayfasına bir grafik ekleme
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

Bu kodda, grafiğin türünü (bu durumda sütun grafiği) ve onu yerleştirmek istediğimiz konumu belirtiyoruz.

## Adım 6: Grafik Örneğine Erişim

 Tabloyu oluşturduğumuzda, özelliklerini değiştirmek için örneğine erişmemiz gerekir. Bu, onu şu şekilde alarak yapılır:`Charts`koleksiyon.

```csharp
// Yeni eklenen grafiğin örneğine erişim
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Adım 7: Grafiğe Veri Serileri Ekleyin

Şimdi verilerimizi grafiğe bağlamamız gerekiyor. Bu, hücreleri grafiğe veri kaynağı olarak belirtmeyi içerir.

```csharp
// "A1" hücresinden "B3" hücresine kadar olan grafiğe SeriesCollection (grafik veri kaynağı) ekleniyor
chart.NSeries.Add("A1:B3", true);
```

Bu adımda, grafiğe görselleştirmesi gereken veri aralığını bildiriyoruz.

## Adım 8: Grafik Görünümünü Özelleştirin

Grafik alanı, grafik alanı ve seri koleksiyonlarının renklerini değiştirerek grafiğimizi biraz süsleyelim. Bu, grafiğimizin öne çıkmasına ve görsel çekiciliğinin artmasına yardımcı olacaktır.

```csharp
// Arsa alanının ön plan renginin ayarlanması
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Grafik alanının ön plan rengini ayarlama
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// 1. SeriKoleksiyon alanının ön plan rengini ayarlama
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// 1. SeriKoleksiyon noktasının alanının ön plan renginin ayarlanması
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// 2. Seri Koleksiyonunun alanını bir degrade ile doldurma
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

Bu kodda, grafiğin farklı bölümleri için çeşitli renkler ayarladık. Görünümü özelleştirmek verilerinizi çok daha ilgi çekici hale getirebilir!

## Adım 9: Ana Izgara Çizgisi Renklerini Değiştirin

Şimdi, ana etkinliğe geçelim! Okunabilirliği artırmak için, grafiğimizin her iki eksenindeki ana kılavuz çizgilerinin rengini değiştireceğiz.

```csharp
// Kategori Ekseninin ana kılavuz çizgilerinin rengini gümüşe ayarlama
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Değer Ekseninin ana kılavuz çizgilerinin renginin kırmızıya ayarlanması
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Bu komutlar kategori ve değer eksenleri için ana kılavuz çizgilerini sırasıyla gümüş ve kırmızıya ayarlar. Bu farklılaştırma, izleyicilerinizin kılavuz çizgilerini grafik boyunca kolayca takip edebilmesini sağlar.

## Adım 10: Çalışma Kitabını Kaydedin

Tüm değişikliklerinizi yaptıktan sonra, çalışma kitabını kaydetme zamanı. Bu, çabanızı meyveye dönüştüren son adımdır.

```csharp
// Excel dosyasını kaydetme
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Bu satır, yeni oluşturduğunuz Excel dosyasını amacını yansıtan bir adla belirtilen çıktı dizinine kaydeder.

## Adım 11: Onay Mesajı

Son olarak görevimizin başarılı olduğunu doğrulayan bir mesaj ekleyelim:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Bu basit konsol çıktısı, programınızın herhangi bir aksaklık olmadan doğru bir şekilde çalıştığını size bildirir.

## Çözüm

Ve işte karşınızda! .NET için Aspose.Cells'i kullanarak bir grafikteki ana kılavuz çizgilerini nasıl değiştireceğinizi başarıyla öğrendiniz. Bu adım adım kılavuzu izleyerek, Excel dosyalarını yalnızca programatik olarak düzenlemekle kalmadınız, aynı zamanda renk özelleştirmeleriyle görsel çekiciliklerini de artırdınız. Veri sunum becerilerinizi derinleştirmek ve grafiklerinizi daha da dinamik hale getirmek için Aspose.Cells ile daha fazla deneme yapmaktan çekinmeyin!

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, Excel dosyalarını program aracılığıyla oluşturmak, düzenlemek ve yönetmek için tasarlanmış bir .NET kütüphanesidir.

### Aspose.Cells'i ücretsiz deneyebilir miyim?  
 Evet, ücretsiz denemeye kaydolabilirsiniz[Burada](https://releases.aspose.com/).

### Aspose.Cells kullanarak bir grafikteki diğer öğeleri nasıl değiştirebilirim?  
 Benzer şekilde, grafik öğelerine erişerek çeşitli grafik özelliklerini özelleştirebilirsiniz.`Chart` başlıklar, açıklamalar ve veri etiketleri gibi sınıflar.

### Aspose.Cells hangi dosya formatlarını destekler?  
Aspose.Cells, XLSX, XLS, CSV ve diğerleri de dahil olmak üzere birden fazla dosya formatını destekler.

### Aspose.Cells için dokümanları nerede bulabilirim?  
 Ayrıntılı belgelere şu adresten ulaşabilirsiniz:[Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
