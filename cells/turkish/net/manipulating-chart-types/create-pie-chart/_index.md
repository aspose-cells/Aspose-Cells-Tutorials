---
title: Pasta Grafiği Oluştur
linktitle: Pasta Grafiği Oluştur
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım kılavuzla Aspose.Cells for .NET kullanarak Excel'de pasta grafiği oluşturmayı öğrenin. Verilerinizi zahmetsizce görselleştirin.
weight: 12
url: /tr/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pasta Grafiği Oluştur

## giriiş

Grafikler oluşturmak, verileri görsel olarak temsil etmek için olmazsa olmazdır ve pasta grafikleri, parçaların bir bütünü nasıl oluşturduğunu göstermenin en popüler yollarından biridir. Aspose.Cells for .NET ile Excel dosyalarında pasta grafiklerinin oluşturulmasını kolayca otomatikleştirebilirsiniz. Bu eğitimde, Aspose.Cells for .NET kullanarak sıfırdan pasta grafiği oluşturmanın nasıl yapılacağına derinlemesine ineceğiz ve süreci sorunsuz ve basit hale getirmek için adım adım bir kılavuz sunacağız. İster araca yeni başlıyor olun, ister Excel otomasyon becerilerinizi geliştirmek istiyor olun, bu kılavuz tam size göre!

## Ön koşullar

Koda dalmadan önce aşağıdaki ayarların yapıldığından emin olun:

1.  Aspose.Cells for .NET Library: Projenizde Aspose.Cells'in yüklü olduğundan emin olun. Henüz yüklemediyseniz, şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/cells/net/).
2. .NET Geliştirme Ortamı: Projenizin .NET Framework veya .NET Core kullanacak şekilde ayarlandığından emin olun.
3. Temel C# Bilgisi: C# programlamada, özellikle nesne yönelimli programlamada (OOP) rahat olmalısınız.

 Gelişmiş kullanıcılar için, Aspose.Cells'in tüm özelliklerinin kilidini açmak için geçici bir lisans uygulanabilir. Bir tane talep edebilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).

## Paketleri İçe Aktar

Başlamak için, bu eğitim için gereken gerekli ad alanlarını ve paketleri içe aktarın. Bunlara temel G/Ç işlemleri ve Aspose.Cells paketi dahildir.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Adım 1: Yeni bir Çalışma Kitabı Oluşturun

 İlk olarak, bir örnek oluşturmamız gerekiyor`Workbook` Excel dosyasını temsil eden sınıf. Bir çalışma kitabı birden fazla sayfa içerir ve örneğimiz için iki sayfayla çalışacağız—biri veriler için, diğeri pasta grafiği için.

```csharp
Workbook workbook = new Workbook();
```

Bu yeni bir Excel çalışma kitabını başlatır. Peki veriler nereye gider? Bunu bir sonraki adımda halledelim.

## Adım 2: Çalışma Sayfasına Veri Ekleyin

Çalışma kitabı oluşturulduktan sonra, ilk çalışma sayfasına erişmemiz ve ona bir isim vermemiz gerekiyor. Pasta grafiği için gereken verileri buraya gireceğiz.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Şimdi farklı bölgeleri temsil eden bazı sahte satış verilerini girebiliriz:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Burada iki sütun ekliyoruz: biri bölgeler için, diğeri satış rakamları için. Bu veriler pasta grafiğinde gösterilecektir.

## Adım 3: Bir Grafik Sayfası Ekleyin

Daha sonra pasta grafiğini tutacak ayrı bir çalışma sayfası ekleyelim.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Bu yeni sayfa pasta grafiğini barındıracaktır. Buna "Grafik" gibi bir ad vermek, kullanıcıların dosyayı açtıklarında ne beklemeleri gerektiğini bilmelerini sağlar.

## Adım 4: Pasta Grafiğini Oluşturun

Şimdi gerçek grafiği oluşturma zamanı. Bir pasta grafiği istediğimizi belirteceğiz ve sayfadaki konumunu tanımlayacağız.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Yöntem`Add()`grafik türü için parametreleri kabul eder (bu durumda,`ChartType.Pie`), ve çalışma sayfasındaki konumu. Sayılar satır ve sütun konumlarını temsil eder.

## Adım 5: Grafik Görünümünü Özelleştirin

Bir pasta grafiği biraz özelleştirme olmadan tamamlanmış sayılmaz! Renkleri, etiketleri ve başlığı değiştirerek grafiğimizi görsel olarak çekici hale getirelim.

### Grafik Başlığını Ayarla
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Arsa Alanını Özelleştir
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Arsa alanının degrade dolgusunu ayarlıyoruz ve daha temiz bir görünüm için kenarlığı gizliyoruz.

## Adım 6: Grafik Verilerini Tanımlayın

 Grafiği verilerimize bağlamanın zamanı geldi.`NSeries` Grafik özelliği satış rakamlarını ve bölgeleri pasta grafiğine bağlar.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 İlk satır, hücrelerdeki satış verilerini kullandığımızı belirtir`B2:B8` Ayrıca grafiğe bölge adlarını kullanmasını da söylüyoruz.`A2:A8` kategori etiketleri olarak.

## Adım 7: Veri Etiketleri Ekleyin

Etiketleri doğrudan grafik segmentlerine eklemek, anlamayı kolaylaştırabilir. Bölge adlarını ve satış değerlerini pasta grafik dilimlerine dahil edelim.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Adım 8: Grafik Alanını ve Göstergeyi Özelleştirin

Son olarak, grafik alanına ve efsaneye son rötuşları yapalım. Bu, grafiğin genel sunumunu geliştirir.

### Grafik Alanı
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Efsane
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Adım 9: Çalışma Kitabını Kaydedin

Son olarak çalışma kitabını bir Excel dosyasına kaydediyoruz. Gerektiğinde çıktı dizinini ve dosya adını belirtebilirsiniz.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Çözüm

Aspose.Cells for .NET ile pasta grafiği oluşturmak basit ve özelleştirilebilir bir işlemdir. Bu kılavuzu izleyerek, sadece birkaç adımda değerli içgörüler ileten profesyonel görünümlü bir grafik oluşturabilirsiniz. İster iş raporlaması ister eğitim amaçlı olsun, grafik oluşturma konusunda uzmanlaşmak Excel otomasyon becerilerinizi geliştirecektir. Unutmayın, Aspose.Cells, çarpıcı, veri odaklı Excel dosyalarını zahmetsizce oluşturmanız için gereken esnekliği sağlar.

## SSS

### Aspose.Cells for .NET kullanarak başka tür grafikler oluşturabilir miyim?
Evet! Aspose.Cells çubuk grafikler, çizgi grafikler ve dağılım grafikleri dahil olmak üzere çeşitli grafik türlerini destekler.

### Aspose.Cells for .NET'i kullanmak için ücretli bir lisansa ihtiyacım var mı?
Ücretsiz sürümü bazı sınırlamalarla kullanabilirsiniz. Tam özellikler için satın alabileceğiniz bir lisansa ihtiyacınız olacak[Burada](https://purchase.aspose.com/buy).

### Tabloyu PDF veya resim gibi formatlara aktarabilir miyim?
Kesinlikle! Aspose.Cells, grafikleri PDF ve PNG dahil olmak üzere çeşitli formatlara aktarmanıza olanak tanır.

### Her pasta dilimini farklı renklerle şekillendirmek mümkün mü?
 Evet, her dilime farklı renkler uygulayabilirsiniz.`IsColorVaried` mülk`true`, eğitimde gösterildiği gibi.

### Tek bir çalışma kitabında birden fazla grafiğin oluşturulmasını otomatikleştirebilir miyim?
Evet, tek bir Excel dosyası içerisinde ihtiyacınız kadar çok grafik oluşturabilir ve özelleştirebilirsiniz.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
