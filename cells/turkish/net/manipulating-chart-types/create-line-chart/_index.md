---
title: Çizgi Grafiği Oluştur
linktitle: Çizgi Grafiği Oluştur
second_title: Aspose.Cells .NET Excel İşleme API'si
description: .NET için Aspose.Cells kullanarak çarpıcı çizgi grafikleri oluşturun. Verilerinizi etkili bir şekilde görselleştirmek için adım adım kılavuzumuzu izleyin.
weight: 11
url: /tr/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çizgi Grafiği Oluştur

## giriiş

Verilerinizi çarpıcı bir netlikle görselleştirmeye hazır mısınız? Çizgi grafikler, zaman içindeki eğilimleri veya iki değişken arasındaki ilişkiyi göstermenin harika bir yoludur. İster bir iş projesi için verileri yönetiyor olun, ister kişisel ölçümleri analiz ediyor olun, programatik olarak çizgi grafikler oluşturma yeteneği size zaman kazandırabilir ve daha fazla esneklik sağlayabilir. Bu kılavuzda, .NET için Aspose.Cells kullanarak bir çizgi grafik oluşturmanın her adımında size yol göstereceğiz. Başlamaya hazır mısınız? Hadi başlayalım!

## Ön koşullar

Çizgi grafiği oluşturmanın inceliklerine girmeden önce, aşağıdakileri takip edebilecek donanıma sahip olduğunuzdan emin olalım:

1. Visual Studio: .NET geliştirme için en popüler IDE'lerden biri olduğu için makinenizde Visual Studio'nun yüklü olduğundan emin olun.
2.  .NET için Aspose.Cells Kütüphanesi: Buradan indirebileceğiniz Aspose.Cells kütüphanesine ihtiyacınız olacak.[Burada](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: C# programlama diline aşina olmak, örnekleri ve kod parçacıklarını daha iyi anlamanıza yardımcı olacaktır.
4. .NET Framework veya .NET Core: Uygulamalarımızın temelini oluşturacağı için bu iki framework'ten birinin temel kurulumu.

Bu ön koşulları yerine getirdikten sonra, bazı grafikler oluşturmaya hazırsınız!

## Paketleri İçe Aktar

Ortamımızı kurduğumuza göre, C# kodumuza gerekli paketleri içe aktarmamız gerekiyor. Bir projeye başlamadan önce araçlarınızı nasıl topluyorsanız, paketleri içe aktarmak da ihtiyacınız olan her şeye sahip olduğunuzdan emin olmak için önemlidir.

İşte bunu nasıl yapacağınız:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Bu satır şunları içe aktarır:`Aspose.Cells` çizgi grafiğimizi oluşturmak için kullanacağımız tüm sınıfları ve metotları içeren namespace.

Şimdi, tüm süreci basit, sindirilebilir adımlara bölelim. Her adım, Aspose.Cells for .NET kullanarak bir çizgi grafiği oluşturmanın mantıksal akışında size rehberlik edecektir.

## Adım 1: Çıktı Dizinini Ayarlayın

İlk adım çıktı dosyanızı nereye kaydetmek istediğinizi tanımlamaktır. Ellerinizi kirletmeye başlamadan önce çalışma alanınızı ayarlamak gibidir. 

```csharp
// Çıktı dizini
string outputDir = "Your Output Directory";
```
 Yer değiştirmek`"Your Output Directory"`Oluşturulan Excel dosyasını kaydetmek istediğiniz gerçek yol ile.

## Adım 2: Çalışma Kitabı Nesnesini Örneklendirin

Sonra, yeni bir çalışma kitabı örneği oluşturmamız gerekiyor. Çalışma Kitabını yaratıcılığınızın akacağı tuval olarak düşünün. 

```csharp
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();
```
Bu satır tüm verilerinizi ve görsellerinizi tutacak yeni bir çalışma kitabı başlatır.

## Adım 3: Çalışma Sayfasına Erişim

Yeni oluşturduğumuz çalışma kitabımızda, verilerimizi gireceğimiz çalışma sayfasına bir referans edinmemiz gerekiyor. Çalışma kitabı tuvalimizse, çalışma sayfası paletimizdir.

```csharp
// Yeni eklenen çalışma sayfasının referansını sayfa indeksini geçirerek elde etme
Worksheet worksheet = workbook.Worksheets[0];
```
 Burada ilk çalışma sayfasına (indeks) erişiyoruz`0`).

## Adım 4: Hücrelere Örnek Değerler Ekleyin

Şimdi eğlenceli kısma geliyoruz! Çalışma sayfamıza bazı örnek değerler gireceğiz. Bu veriler çizgi grafiğimizin temelini oluşturacak. 

```csharp
// Hücrelere örnek değerler ekleme
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
Bu kod parçacığında, A ve B sütunlarındaki hücrelere değerler ekliyoruz. A sütunu X eksenindeki değerleri, B sütunu ise Y eksenindeki değerleri temsil ediyor.

## Adım 5: Çalışma Sayfasına Bir Çizgi Grafiği Ekleyin

Sırada, çizgi grafiğimizi çalışma sayfasına tanıtacağız. Verilerinizin gerçekten canlanacağı yer burası!

```csharp
// Çalışma sayfasına bir grafik ekleme
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Burada, belirtilen konuma bir çizgi grafiği ekliyoruz. Parametreler (5, 0, 25, 10), grafiğin çalışma sayfasındaki konumunu ve boyutunu tanımlar.

## Adım 6: Yeni Grafik Örneğine Erişim

Grafiğimizi ekledikten sonra, yeni oluşturulan grafik nesnesine el atmamızın zamanı geldi. 

```csharp
// Yeni eklenen grafiğin örneğine erişim
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Bu kod bizi grafiğe bağlar, böylece onu daha fazla manipüle edebiliriz.

## Adım 7: SeriesCollection'ı Grafiğe Ekleyin

Şimdi grafiğimize hangi verilerin görüntüleneceğini söylememiz gerekiyor. Burada, bir SeriesCollection ekleyerek çizgi grafiğimiz için veri kaynağını tanımlıyoruz.

```csharp
// "A1" hücresinden "B3" hücresine kadar olan grafiğe SeriesCollection (grafik veri kaynağı) ekleniyor
chart.NSeries.Add("A1:B3", true);
```
Bu örnekte, grafiğe A1'den B3'e kadar olan hücrelerdeki değerleri kullanmasını söylüyoruz.

## Adım 8: Excel Dosyasını Kaydedin

Büyük final! Tüm sıkı çalışmanızın ardından, Excel dosyasını kaydetme ve çizgi grafiğinizi eylem halinde görme zamanı.

```csharp
// Excel dosyasını kaydetme
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Bu satır çalışma kitabınızı belirtilen çıktı dizinine şu adla kaydeder:`outputHowToCreateLineChart.xlsx`.

## Adım 9: Çalıştırın ve Doğrulayın

Son olarak, kodunuzu çalıştırabilir ve çizgi grafiğinin çıktı dizininizde başarıyla oluşturulduğunu doğrulayabilirsiniz! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Bu, konsolunuzda her şeyin düzgün çalıştığını bildiren bir mesaj görüntüleyecektir.

## Çözüm

.NET için Aspose.Cells kullanarak bir çizgi grafiği oluşturmak, verilerinizi canlandırmanın etkili bir yoludur. Bu adım adım kılavuzu izleyerek, veri kümelerinizdeki eğilimleri ve ilişkileri kolayca görselleştirebilirsiniz. İster deneyimli bir geliştirici olun, ister yeni başlıyor olun, Aspose.Cells size veri görselleştirme görevlerinizi otomatikleştirmek için esneklik ve güç sağlar. 

## SSS

### Aspose.Cells for .NET nedir?  
Aspose.Cells for .NET, Excel dosyalarını programlı bir şekilde yönetmek ve düzenlemek için tasarlanmış güçlü bir kütüphanedir ve geliştiricilerin elektronik tablolar oluşturmasına, düzenlemesine ve dönüştürmesine olanak tanır.

### Aspose.Cells grafikleri destekliyor mu?  
Evet, Aspose.Cells çizgi grafikler, pasta grafikler, çubuk grafikler ve daha fazlası dahil olmak üzere çeşitli grafik türleri için kapsamlı destek sağlar.

### Aspose.Cells'i ücretsiz kullanabilir miyim?  
Evet, özelliklerini keşfetmek için ücretsiz deneme sürümünü indirebilirsiniz. Uzun vadeli kullanım için bir lisans satın almayı düşünün.

### Destek için bir forum var mı?  
 Kesinlikle! Cevapları bulabilir ve sorular sorabilirsiniz[Aspose.Cells forumu](https://forum.aspose.com/c/cells/9).

### Lisans nasıl satın alabilirim?  
 Lisanslar şu adresten kolayca satın alınabilir:[satın alma sayfası](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
