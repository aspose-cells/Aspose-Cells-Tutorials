---
"description": "Bu kolay takip edilebilir kılavuzla Aspose.Cells for .NET'i kullanarak Excel'deki grafiklerin boyutunu ve konumunu değiştirmeyi öğrenin."
"linktitle": "Grafik Boyutunu ve Pozisyonunu Değiştir"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Grafik Boyutunu ve Pozisyonunu Değiştir"
"url": "/tr/net/advanced-chart-operations/change-chart-size-and-position/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafik Boyutunu ve Pozisyonunu Değiştir

## giriiş

Programlı olarak elektronik tabloları düzenlemeye gelince, Aspose.Cells for .NET'in çok yönlülüğünü ve gücünü görmezden gelmek zordur. Excel dosyalarınızdaki grafikleri yeniden boyutlandırma veya yeniden konumlandırma konusunda hiç zorluk çektiniz mi? Öyleyse, sizi bir şölene hazır! Bu kılavuz, Aspose.Cells kullanarak elektronik tablolarınızdaki grafiklerin boyutunu ve konumunu değiştirmek için sizi inanılmaz derecede basit adımlara götürecek. Emniyet kemerlerinizi bağlayın, çünkü bu konuya derinlemesine dalıyoruz!

## Ön koşullar

Kodlama ve grafik düzenlemenin inceliklerine dalmadan önce, birkaç ön koşulu açıklığa kavuşturalım. Sağlam bir temel, yolculuğunuzu daha pürüzsüz ve daha keyifli hale getirecektir.

### C# Temel Bilgisi
- C# programlama diline aşinalık şarttır. C# sözdiziminde gezinebiliyorsanız, zaten bir adım öndesiniz!

### Aspose.Cells .NET Kütüphanesi
- Aspose.Cells kütüphanesinin yüklü olması gerekir. Eğer henüz yüklü değilse, endişelenmeyin! Bunu şu adresten kolayca indirebilirsiniz: [Burada](https://releases.aspose.com/cells/net/).

### Geliştirme Ortamı
- C# kodlarınızı sorunsuz bir şekilde yazıp çalıştırabileceğiniz geliştirme ortamınızı (örneğin Visual Studio) kurun.

### Grafikli Excel Dosyası
- Bu eğitim için kullanabileceğimiz en azından bir grafiğin bulunduğu bir Excel dosyasına sahip olmak faydalı olacaktır.

Listenizdeki bu ön koşulları tamamladığınızda, grafik boyutunu ve konumunu bir profesyonel gibi nasıl değiştireceğinizi öğrenmeye hazırsınız!

## Paketleri İçe Aktar

Artık her şey ayarlandığına göre, gerekli paketleri içe aktaralım. Bu adım çok önemlidir çünkü Excel dosyalarını işlemek için gereken Aspose.Cells sınıflarına ve yöntemlerine erişmemizi sağlar.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
```

Bu ifadeler derleyiciye Aspose.Cells kütüphanesindeki sınıfları kullanacağımızı bildirir. Daha sonra engebeli bir yolda ilerlemekten kaçınmak için bunu kodunuzun en üstüne koyduğunuzdan emin olun!

Şimdi, süreci yönetilebilir adımlara bölelim. Her şeyin kristal kadar açık olduğundan emin olarak adım adım ilerleyeceğiz.

## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın

```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

İlk önce, kaynak dosyamızın nerede bulunduğunu ve çıktı dosyasının nereye kaydedilmesini istediğimizi tanımlamamız gerekiyor. "Your Document Directory" ve "Your Output Directory" ifadelerini gerçek klasör yollarınızla değiştirin. Bu dizinleri dosyalarınızın bulunduğu ana üssünüz ve fırlatma rampanız olarak düşünün.

## Adım 2: Çalışma Kitabını Yükleyin

```csharp
Workbook workbook = new Workbook(sourceDir + "sampleChangeChartSizeAndPosition.xlsx");
```

Burada, yeni bir örnek oluşturuyoruz `Workbook` sınıfa gidin ve Excel dosyamızı içine yükleyin. Çalışma kitabını tüm sayfalarınızı ve grafiklerinizi içeren dijital bir not defteri olarak düşünün. Geçirdiğimiz parametre Excel dosyamıza giden tam yoldur, bu yüzden dosya adını içerdiğinden emin olun!

## Adım 3: Çalışma Sayfasına Erişim

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

Artık çalışma kitabımız yüklendiğine göre, üzerinde çalışmak istediğimiz belirli çalışma sayfasına erişmemiz gerekiyor; bu durumda bu, ilk çalışma sayfasıdır (indeks `[0]`). Bir kitapta doğru sayfayı çevirmek gibi, bu adım düzenlemelerimiz için istediğimiz sayfaya odaklanmamıza yardımcı olur.

## Adım 4: Grafiği Yükleyin

```csharp
Chart chart = worksheet.Charts[0];
```

Çalışma kağıdını aldıktan sonra, doğrudan grafiğe erişmeye başlıyoruz! İlk grafiğe (tekrar, dizin) geçiyoruz `[0]`). Bu, süslemek istediğiniz sanat eserini seçmek gibidir. Tablonuzun o çalışma sayfasında mevcut olduğundan emin olun, yoksa kafanız karışır!

## Adım 5: Grafiği Yeniden Boyutlandırın

```csharp
chart.ChartObject.Width = 400;
chart.ChartObject.Height = 300;
```

Grafiğin boyutlarını değiştirme zamanı geldi! Burada genişliği ayarlıyoruz `400` pikseller ve yükseklik `300` piksel. Boyutu ayarlamak, sanat eseriniz için mükemmel çerçeveyi seçmeye benzer; çok büyük veya çok küçük olursa odaya tam olarak uymaz.

## Adım 6: Grafiği Yeniden Konumlandırın

```csharp
chart.ChartObject.X = 250;
chart.ChartObject.Y = 150;
```

Artık doğru boyuta sahip olduğumuza göre, grafiği hareket ettirelim! `X` Ve `Y` özellikleri, aslında çalışma sayfasındaki tabloyu yeniden konumlandırıyoruz. Bunu, çerçeveli resminizi güzelliğini daha iyi sergilemek için duvardaki yeni bir noktaya sürüklemek gibi düşünün!

## Adım 7: Çalışma Kitabını Kaydedin

```csharp
workbook.Save(outputDir + "outputChangeChartSizeAndPosition.xlsx");
```

Son olarak, değişikliklerimizi yeni bir Excel dosyasına kaydediyoruz. Her şeyi düzenli tutmak için dışa aktarılan dosya için uygun bir ad belirtin. Bu, mobilyaları hareket ettirdikten sonra güzelce düzenlenmiş odanızın bir anlık görüntüsünü almak gibidir; yeni düzeni korur!

## Adım 8: Başarılı Olduğunu Onaylayın

```csharp
Console.WriteLine("ChangeChartSizeAndPosition executed successfully.");
```

İşleri düzgün bir şekilde toparlamak için, operasyonun başarıyla tamamlanıp tamamlanmadığına dair geri bildirim sağlıyoruz. Bu harika bir uygulamadır, görevinize dair net ve güvenli bir kapanış sağlar - tıpkı mobilyaları yeniden düzenledikten sonra yaptığınız işe hayranlık duymak gibi!

## Çözüm

Tebrikler! Aspose.Cells for .NET kullanarak Excel'deki grafiklerin boyutunu ve konumunu nasıl değiştireceğinizi öğrendiniz. Bu adımlarla, grafiklerinizin yalnızca daha iyi görünmesini değil, aynı zamanda elektronik tablolarınıza mükemmel şekilde uymasını sağlayabilir ve verilerinizin daha profesyonel bir şekilde sunulmasını sağlayabilirsiniz. Neden bir deneme yapmıyorsunuz ve bugün grafiklerinizi düzenlemeye başlamıyorsunuz? 

## SSS

### Aspose.Cells for .NET nedir?  
Aspose.Cells for .NET, geliştiricilerin .NET uygulamalarında Excel dosyaları oluşturmasına, düzenlemesine ve dönüştürmesine olanak tanıyan güçlü bir kütüphanedir.

### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?  
Aspose.Cells'i ücretsiz deneyebilirsiniz ancak üretim uygulamalarında sürekli kullanım için bir lisans gereklidir. Bir tane edinebilirsiniz [Burada](https://purchase.aspose.com/buy).

### Visual Studio olmadan Aspose.Cells'i kullanabilir miyim?  
Evet, Aspose.Cells'i herhangi bir .NET uyumlu IDE'de kullanabilirsiniz, ancak Visual Studio geliştirmeyi kolaylaştıran araçlar sunar.

### Aspose.Cells için nasıl destek alabilirim?  
Özel desteklerinden faydalanabilirsiniz [Destek Forumu](https://forum.aspose.com/c/cells/9).

### Geçici lisans var mı?  
Evet, Aspose.Cells'i kısa bir süreliğine değerlendirmek için geçici bir lisans edinebilirsiniz; bu lisans şu anda mevcuttur: [Burada](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}