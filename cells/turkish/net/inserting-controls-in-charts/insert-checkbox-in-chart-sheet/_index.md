---
title: Grafik Sayfasına Onay Kutusu Ekle
linktitle: Grafik Sayfasına Onay Kutusu Ekle
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım eğitimle Aspose.Cells for .NET kullanarak Excel grafik sayfasına nasıl kolayca onay kutusu ekleyeceğinizi öğrenin.
weight: 13
url: /tr/net/inserting-controls-in-charts/insert-checkbox-in-chart-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafik Sayfasına Onay Kutusu Ekle

## giriiş

Excel'de bir grafik oluşturduysanız, bunların verileri görselleştirmek için inanılmaz derecede güçlü olabileceğini biliyorsunuzdur. Peki ya bu etkileşimi, doğrudan grafiğe bir onay kutusu ekleyerek daha da artırabilirseniz? Bu biraz nüanslı gelebilir ancak .NET için Aspose.Cells kütüphanesiyle aslında oldukça basittir. Bu eğitimde, sizi adım adım süreç boyunca yönlendirerek basit ve takip etmesi kolay hale getireceğim.

## Ön koşullar

Eğitime dalmadan önce, her şeyin ayarlandığından emin olalım. İhtiyacınız olanlar şunlar:

### Visual Studio Yüklendi
- Öncelikle Visual Studio'ya ihtiyacınız olacak. Eğer henüz yüklemediyseniz, Microsoft sitesinden indirebilirsiniz.

### Aspose.Cells Kütüphanesi
-  Bir sonraki temel araç .NET için Aspose.Cells kütüphanesidir. Bunu şuradan kolayca edinebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/cells/net/) indirmek için. Satın almadan önce test etmeyi tercih ederseniz, ayrıca bir[ücretsiz deneme mevcut](https://releases.aspose.com/).

### C#'ın Temel Anlayışı
- Biraz kod yazacağımız için, C# hakkında temel bir anlayış faydalı olacaktır. Endişelenmeyin; ilerledikçe her şeyi açıklayacağım!

### Çıktı Dizini
- Çıktı Excel dosyalarınızın kaydedileceği bir dizine ihtiyacınız olacak. Bunu elinizin altında bulundurduğunuzdan emin olun.

Bu ön koşulları tamamladığınızda, artık aksiyona geçmeye hazırız!

## Paketleri İçe Aktar

Başlamak için, projemizi Visual Studio'da kuralım ve gerekli paketleri içe aktaralım. İşte basit bir adım adım kılavuz:

### Yeni Bir Proje Oluşturun

Visual Studio'yu açın ve yeni bir Konsol Uygulaması projesi oluşturun. Sadece şu basit adımları izleyin:
- “Yeni proje oluştur”a tıklayın.
- Seçeneklerden “Konsol Uygulaması (.NET Framework)” seçeneğini seçin.
- Projenize "CheckboxInChart" gibi bir isim verin.

### NuGet aracılığıyla Aspose.Cells'i yükleyin

Projeniz kurulduktan sonra, Aspose.Cells kütüphanesini ekleme zamanı geldi. Bunu NuGet Paket Yöneticisi aracılığıyla yapabilirsiniz:
- Çözüm Gezgini’nde projenize sağ tıklayın ve “NuGet Paketlerini Yönet” seçeneğini seçin.
- “Aspose.Cells”i arayın ve “Yükle”ye tıklayın.
- Bu, ihtiyacınız olan tüm bağımlılıkları çekerek kütüphaneyi kullanmaya başlamanızı kolaylaştıracaktır.

### Gerekli Kullanım Yönergelerini Ekleyin

 En üstte`Program.cs` dosyasına, Aspose.Cells işlevlerini kullanılabilir hale getirmek için aşağıdaki using yönergelerini ekleyin:
```csharp
using Aspose.Cells.Charts;
using System;
using Aspose.Cells.Drawing;
```

Artık kurulumu tamamladınız! Bu, bir ev inşa etmeden önce sağlam bir temel atmak gibidir - istikrarlı bir yapı için çok önemlidir.

Artık her şey hazır olduğuna göre, kodlama kısmına geçelim! İşte Aspose.Cells kullanarak bir grafik sayfasına onay kutusu eklemenin ayrıntılı bir dökümü.

## Adım 1: Çıktı Dizininizi Tanımlayın

Heyecan verici kısma geçmeden önce, dosyamızın nereye kaydedilmesini istediğimizi tanımlamamız gerekiyor. Bir çıktı dizin yolu sağlamak isteyeceksiniz.
```csharp
string outputDir = "C:\\YourOutputDirectory\\"; // Belirtilen dizine geçin
```
 Değiştirdiğinizden emin olun`"C:\\YourOutputDirectory\\"`dosyanızın kaydedilmesini istediğiniz yol ile. Bunu çalışma alanınızı ayarlamak gibi düşünün; araçlarınızı (veya bu durumda Excel dosyanızı) nereye koyduğunuzu bilmeniz gerekir.

## Adım 2: Bir Çalışma Kitabı Nesnesi Oluşturma

 Sonra, bir örnek oluşturuyoruz`Workbook` sınıf. Bütün çalışmalarımız burada gerçekleşecek.
```csharp
Workbook workbook = new Workbook();
```
Bu kod satırı boş bir tuvali açmak gibidir. Boyamaya (veya bizim durumumuzda kodlamaya) başlamaya hazırsınız!

## Adım 3: Çalışma Sayfasına Grafik Ekleme

Şimdi, çalışma kitabınıza bir grafik ekleme zamanı. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
int index = workbook.Worksheets.Add(SheetType.Chart);
Worksheet sheet = workbook.Worksheets[index];
sheet.Charts.AddFloatingChart(ChartType.Column, 0, 0, 1024, 960);
```
Bu kodda:
- Çalışma kitabına yeni bir grafik sayfası ekleniyor.
- Grafik türünü seçme. Burada basit bir sütun grafiği seçiyoruz.
- Grafiğinizin boyutlarını belirleme.

Bu adımı, sanat eserinizi çerçevenin içine yerleştirmeden önce ne tür bir çerçeve istediğinize karar vermek olarak düşünün.

## Adım 4: Grafiğinize Veri Serileri Ekleme

Bu noktada, grafiği bazı veri serileriyle dolduralım. Örnek veri eklemek için:
```csharp
sheet.Charts[0].NSeries.Add("{1,2,3}", false);
```
Bu satır çok önemli! Tuvalinize boya sürmek gibi. Sayılar, grafiğiniz için bazı örnek veri noktalarını temsil ediyor.

## Adım 5: Grafiğe Onay Kutusu Ekleme

Şimdi eğlenceli kısma geliyoruz — grafiğimize bir onay kutusu eklemek. İşte nasıl:
```csharp
sheet.Charts[0].Shapes.AddShapeInChart(MsoDrawingType.CheckBox, PlacementType.Move, 400, 400, 1000, 600);
sheet.Charts[0].Shapes[0].Text = "CheckBox 1";
```
Bu kodda:
- Eklemek istediğimiz şeklin türünü belirtiyoruz; bu durumda bir onay kutusu.
- `PlacementType.Move` grafik hareket ederse onay kutusunun da hareket edeceği anlamına gelir.
- Ayrıca grafik alanındaki onay kutusunun konumunu ve boyutunu ayarlıyoruz ve son olarak onay kutusunun metin etiketini ayarlıyoruz.

Bir onay kutusu eklemek, dondurmanızın üzerine kiraz koymak gibidir; tüm sunumunuzu zenginleştirir!

## Adım 6: Excel Dosyasını Kaydetme

Son olarak çalışmamızı kaydedelim. İşte bulmacanın son parçası:
```csharp
workbook.Save(outputDir + "InsertCheckboxInChartSheet_out.xlsx");
```
Bu satır, yeni oluşturduğunuz Excel dosyanızı onay kutusuyla tanımlanmış çıktı dizinine kaydeder. Bu, sanat eserinizi koruyucu bir kılıf içinde mühürlemeye benzer!

## Çözüm

İşte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasındaki grafik sayfasına başarıyla bir onay kutusu eklediniz. Bu adımları izleyerek, harika işlevsellik sunan etkileşimli ve dinamik Excel sayfaları oluşturabilir, veri görselleştirmelerinizi daha da ilgi çekici hale getirebilirsiniz.

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, .NET uygulamalarında Excel dosyaları oluşturmak ve düzenlemek için güçlü bir kütüphanedir.

### Aspose.Cells'i ücretsiz kullanabilir miyim?  
 Evet, Aspose ücretsiz deneme sunuyor. Mevcut deneme sürümüyle başlayabilirsiniz[Burada](https://releases.aspose.com/).

### Bir grafik sayfasına onay kutusu eklemek karmaşık mıdır?  
Hayır, hayır! Bu eğitimde gösterildiği gibi, bu sadece birkaç basit kod satırıyla yapılabilir.

### Aspose.Cells'i nereden satın alabilirim?  
 Aspose.Cells'i şu adresten satın alabilirsiniz:[satın alma bağlantısı](https://purchase.aspose.com/buy).

### Sorun yaşarsam nasıl destek alabilirim?  
 Aspose, sorular sorabileceğiniz ve çözümler bulabileceğiniz bir destek forumu sunar. Şuraya göz atın:[destek sayfası](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
