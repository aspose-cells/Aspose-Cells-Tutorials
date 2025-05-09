---
"description": "Aspose.Cells for .NET kullanarak Excel grafiklerinizi özelleştirilmiş veri etiketi şekilleriyle geliştirin. Veri sunumunuzu yükseltmek için bu adım adım kılavuzu izleyin."
"linktitle": "Grafik Veri Etiketlerinin Şekil Türünü Ayarla"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Grafik Veri Etiketlerinin Şekil Türünü Ayarla"
"url": "/tr/net/advanced-chart-operations/set-shape-type-of-data-labels-of-chart/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafik Veri Etiketlerinin Şekil Türünü Ayarla

## giriiş

Veri görselleştirme dünyasında, grafikler karmaşık bilgileri erişilebilir bir şekilde sunmak için başvurulan bir yöntemdir. Ancak, tüm veri etiketleri eşit yaratılmamıştır! Bazen, bu etiketleri öne çıkarmanız gerekir ve farklı şekiller kullanmak önemli bir fark yaratabilir. Excel grafiklerinizdeki veri etiketlerini özel şekillerle geliştirmek istiyorsanız, doğru yerdesiniz. Bu kılavuz, .NET için Aspose.Cells kullanarak bir grafikteki veri etiketlerinin şekil türünü nasıl ayarlayacağınızı gösterecektir. Hadi başlayalım!

## Ön koşullar

Kodlamaya başlamadan önce, her şeyin doğru şekilde ayarlandığından emin olalım. İhtiyacınız olanlar şunlardır:

1. .NET için Aspose.Cells: Henüz indirmediyseniz, şu adresten indirin: [Aspose web sitesi](https://releases.aspose.com/cells/net/)Bu kütüphane Excel dokümanları üzerinde her türlü manipülasyona olanak sağlar.
2. Visual Studio: .NET uygulamaları yazmak ve çalıştırmak için sisteminizde yüklü olması gerekir. Projenizin ihtiyaçlarına göre .NET Framework veya .NET Core'u destekleyen sürüm olduğundan emin olun.
3. C# Hakkında Temel Bilgi: Temel programlama kavramlarına ve C# sözdizimine aşinalık, kod parçacıklarını daha iyi anlamanıza kesinlikle yardımcı olacaktır.
4. Bir Excel dosyası: Çalışmak için bir örnek Excel çalışma kitabına da ihtiyacınız olacak. Kendi çalışma kitabınızı oluşturabilir veya mevcut olanlardan herhangi birini kullanabilirsiniz.

Artık ön koşulları sağladığımıza göre hemen başlayalım!

## Paketleri İçe Aktar

Kodlamaya başlamadan önce ilgili Aspose.Cells ad alanlarını içe aktarmanız gerekir. Bu, kütüphanenin sunduğu zengin işlevselliğe erişmenizi sağlayacaktır. İşte nasıl yapacağınız:

### Aspose.Cells'i içe aktar

Visual Studio projenizi açın ve C# dosyanızın en üstüne aşağıdaki using yönergesini ekleyin:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
```

Bu ad alanları, Çalışma Kitapları, Çalışma Sayfaları ve Grafikleri kolayca oluşturmanıza ve düzenlemenize olanak tanır.

Artık her şey hazır olduğuna göre, kodlama kısmına geçelim! Netlik için adım adım açıklayacağız.

## Adım 1: Dizinlerinizi Tanımlayın

Öncelikle dosyalarınızın nerede bulunduğunu tanımlayalım; hem kaynak dosyayı hem de değiştirilen dosyayı kaydetmek istediğiniz hedef klasörü.

```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";

// Çıktı dizini
string outputDir = "Your Output Directory";
```

Yer değiştirmek `"Your Document Directory"` Ve `"Your Output Directory"` makinenizdeki gerçek yollarla.

## Adım 2: Kaynak Excel Dosyasını Yükleyin

Sonra, çalışmak istediğiniz Excel dosyasını yüklemeniz gerekecek. Sihir burada başlıyor!

```csharp
// Kaynak Excel dosyasını yükle
Workbook wb = new Workbook(sourceDir + "sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```

Bu satır yeni bir satır oluşturur `Workbook` nesneyi seçin ve onu mevcut dosyanıza yönlendirin. Dosya yolunun doğru olduğundan emin olun!

## Adım 3: İlk Çalışma Sayfasına Erişim

Artık çalışma kitabımız olduğuna göre, özelleştirmek istediğiniz grafiği içeren çalışma sayfasına erişmemiz gerekiyor.

```csharp
// İlk çalışma sayfasına erişin
Worksheet ws = wb.Worksheets[0];
```

Burada ilk çalışma sayfasına (indeks) erişiyoruz `0`). Grafiğiniz farklı bir sayfada yer alıyorsa endeksi ayarlayın.

## Adım 4: İlk Tabloya Erişim

Çalışma sayfanızı aldıktan sonra, tabloya erişme zamanı. Her çalışma sayfası birden fazla tablo içerebilir, ancak basitlik adına, burada ilk tabloya bağlı kalacağız.

```csharp
// İlk grafiğe erişin
Chart ch = ws.Charts[0];
```

Tekrar ediyorum, eğer istediğiniz grafik ilk grafik değilse endeksi ona göre değiştirebilirsiniz.

## Adım 5: Grafik Serisine Erişim

Grafik artık erişilebilir olduğundan, veri etiketlerini değiştirmek için daha derine inmeniz gerekir. Seri, grafiğinizdeki veri noktalarını temsil eder.

```csharp
// İlk seriye erişim
Series srs = ch.NSeries[0];
```

Burada genellikle değiştirmek isteyebileceğiniz etiketleri içeren ilk seriyi hedefliyoruz.

## Adım 6: Veri Etiketlerinin Şekil Türünü Ayarlayın

Şimdi kritik kısma geçelim! Veri etiketlerinin şekil türünü ayarlayalım. Aspose.Cells çeşitli şekilleri destekler ve bu örnek için eğlenceli bir dokunuş için bir konuşma balonu ovali seçeceğiz.

```csharp
// Veri etiketlerinin şekil türünü ayarlayın, örneğin Konuşma Balonu Oval
srs.DataLabels.ShapeType = DataLabelShapeType.WedgeEllipseCallout;
```

Farklı şekil türlerini değiştirerek denemekten çekinmeyin `DataLabelShapeType.WedgeEllipseCallout` Diğer mevcut seçeneklere!

## Adım 7: Çıktı Excel Dosyasını Kaydedin

Ağır işi hallettiniz ve şimdi çalışmanızı kaydetme zamanı. Değiştirilen veri etiketi şeklini bir Excel dosyasına geri koyalım.

```csharp
// Çıktı Excel dosyasını kaydedin
wb.Save(outputDir + "outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

Bu, değiştirilen çalışma kitabını belirttiğiniz çıktı dizinine kaydedecektir.

## Adım 8: Çalıştırın ve Onaylayın

Son olarak, programınızı çalıştırmanın zamanı geldi. Çalıştırdıktan sonra, her şeyin sorunsuz gittiğini doğrulayan mesajı görmelisiniz!

```csharp
Console.WriteLine("SetShapeTypeOfDataLabelsOfChart executed successfully.");
```

Bu mesajı gördüğünüzde, yeni Excel dosyasını kontrol etmek için çıktı dizininize gidin. Açın ve yeni şekillendirilmiş veri etiketleriyle yaratıcılığınızı serbest bırakın!

## Çözüm

Ve işte karşınızda—Aspose.Cells for .NET kullanarak Excel grafiklerindeki veri etiketlerini geliştirmeye yönelik basit bir kılavuz! Şekil türlerini özelleştirmek yalnızca grafiklerinizi görsel olarak daha çekici hale getirmekle kalmaz, aynı zamanda veri hikayenizi daha etkili bir şekilde aktarmanıza da yardımcı olur. Unutmayın, veri görselleştirmesi tamamen açıklık ve etkileşimle ilgilidir. Bu nedenle, farklı şekiller ve stillerle oynamaktan çekinmeyin—sonuçta, verileriniz en iyi sunumu hak ediyor.

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla düzenlemelerine olanak tanıyan güçlü bir .NET kütüphanesidir.

### Aspose kullanarak Excel grafiğinin farklı yönlerini değiştirebilir miyim?  
Kesinlikle! Aspose.Cells, veri serileri, etiketler, stiller ve daha fazlası dahil olmak üzere grafikleri değiştirmek için kapsamlı işlevler sunar.

### Aspose.Cells ile hangi programlama dillerini kullanabilirim?  
Bu makale .NET'e odaklansa da, Aspose.Cells ayrıca REST API'leri aracılığıyla Java, PHP, Python ve daha fazlasını da destekler.

### Aspose.Cells için ödeme yapmam gerekir mi?  
Aspose.Cells ticari bir üründür, ancak ücretsiz deneme sürümü sunarlar; bu sürümü bulabilirsiniz [Burada](https://releases.aspose.com/).

### Aspose.Cells ile ilgili sorunlar yaşarsam nereden yardım alabilirim?  
Herhangi bir sorunla karşılaşırsanız, [destek forumu](https://forum.aspose.com/c/cells/9) Uzmanlardan yardım almak için harika bir kaynaktır.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}