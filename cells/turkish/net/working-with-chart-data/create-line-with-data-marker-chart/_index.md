---
title: Veri İşaretleyici Grafiği ile Çizgi Oluştur
linktitle: Veri İşaretleyici Grafiği ile Çizgi Oluştur
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de Veri İşaretleyicileri ile Çizgi grafiğinin nasıl oluşturulacağını öğrenin. Grafikleri kolayca oluşturmak ve özelleştirmek için bu adım adım kılavuzu izleyin.
weight: 10
url: /tr/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Veri İşaretleyici Grafiği ile Çizgi Oluştur

## giriiş

Excel'de programatik olarak çarpıcı grafikler oluşturmayı hiç merak ettiniz mi? Hadi, kemerlerinizi bağlayın çünkü bugün .NET için Aspose.Cells kullanarak Veri İşaretleyicili Çizgi Grafiği oluşturmaya dalacağız. Bu eğitim, Aspose.Cells'e yeni başlıyor olsanız bile, grafik oluşturma konusunda sağlam bir kavrayışa sahip olmanızı sağlayarak her adımda size rehberlik edecektir.

## Ön koşullar

Başlamadan önce, sorunsuz bir şekilde ilerleyebilmeniz için her şeyin yerli yerinde olduğundan emin olun.

1. Aspose.Cells for .NET Library – Bunu yüklemeniz gerekecek. Bunu alabilirsiniz[Burada](https://releases.aspose.com/cells/net/).
2. .NET Framework – Geliştirme ortamınızın en son .NET sürümüyle kurulduğundan emin olun.
3. IDE (Bütünleşik Geliştirme Ortamı) – Visual Studio önerilir.
4.  Geçerli bir Aspose.Cells lisansı – Eğer yoksa, bir tane talep edebilirsiniz[geçici lisans](https://purchase.aspose.com/temporary-license/) veya onlarınkine göz atın[ücretsiz deneme](https://releases.aspose.com/).

Hazır mısınız? Hadi parçalayalım!

## Gerekli Paketleri İçe Aktarma

Başlamak için, aşağıdaki ad alanlarını projenize aktardığınızdan emin olun. Bunlar, grafiğinizi oluşturmak için gerekli sınıfları ve yöntemleri sağlayacaktır.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Bunu hallettikten sonra kodlamaya başlayabiliriz!

## Adım 1: Çalışma Kitabınızı ve Çalışma Sayfanızı Ayarlayın

İlk önce yeni bir çalışma kitabı oluşturmanız ve ilk çalışma sayfasına erişmeniz gerekiyor.

```csharp
//Çıktı dizini
static string outputDir = "Your Document Directory";
		
// Bir çalışma kitabını örneklendirin
Workbook workbook = new Workbook();

// İlk çalışma sayfasına erişin
Worksheet worksheet = workbook.Worksheets[0];
```

Çalışma kitabını Excel dosyanız ve çalışma sayfasını da içindeki belirli sayfa olarak düşünün. Bu durumda, ilk sayfayla çalışıyoruz.

## Adım 2: Çalışma Sayfasını Verilerle Doldurun

Artık çalışma sayfamız olduğuna göre, onu biraz veriyle dolduralım. İki değer serisi için rastgele veri noktaları oluşturuyoruz.

```csharp
// Sütun başlıklarını ayarla
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Grafik oluşturmak için rastgele veriler
Random R = new Random();

// Rastgele veri oluştur ve hücrelere kaydet
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Burada, verileri simüle etmek için rastgele sayılar kullanıyoruz, ancak gerçek yaşam uygulamalarında, verileri veri kümenizdeki gerçek değerlerle doldurabilirsiniz.

## Adım 3: Tabloyu Çalışma Sayfasına Ekleyin

Daha sonra, grafiği çalışma sayfasına ekliyoruz ve türünü seçiyoruz; bu durumda, Veri İşaretleyicili Çizgi Grafiği.

```csharp
// Çalışma sayfasına bir grafik ekleyin
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Yeni oluşturulan grafiğe erişin
Chart chart = worksheet.Charts[idx];
```

Bu kod parçası, çalışma sayfasına veri işaretleyicileri içeren bir çizgi grafiği ekler ve onu belirli bir aralığa (1,3 ila 20,20) yerleştirir. Oldukça basit, değil mi?

## Adım 4: Grafiğin Görünümünü Özelleştirin

Grafik oluşturulduktan sonra, onu istediğiniz gibi biçimlendirebilirsiniz. Arkaplanı, başlığı ve grafik stilini değiştirelim.

```csharp
// Grafik stilini ayarla
chart.Style = 3;

// Otomatik ölçekleme değerini doğru olarak ayarlayın
chart.AutoScaling = true;

// Ön plan rengini beyaz olarak ayarla
chart.PlotArea.Area.ForegroundColor = Color.White;

//Grafik başlığı özelliklerini ayarla
chart.Title.Text = "Sample Chart";

// Grafik türünü ayarla
chart.Type = ChartType.LineWithDataMarkers;
```

Burada, beyaz bir arka plan ayarlayarak, otomatik ölçekleme yaparak ve anlamlı bir başlık vererek grafiğe temiz bir görünüm kazandırıyoruz.

## Adım 5: Serileri Tanımlayın ve Veri Noktalarını Çizin

Artık grafiğimiz güzel görünüyor, şimdi çizilecek veri serisini tanımlamamız gerekiyor.

```csharp
// Kategori ekseni başlığının Özelliklerini Ayarla
chart.CategoryAxis.Title.Text = "Units";

// Grafik için iki seri tanımlayın
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Bu seriler daha önce doldurduğumuz veri noktalarının aralıklarına karşılık gelmektedir.

## Adım 6: Renkleri Ekleyin ve Seri İşaretleyicilerini Özelleştirin

Veri işaretleyicilerimize özel renkler ekleyerek bu grafiği daha da çekici hale getirelim.

```csharp
// İlk seriyi özelleştir
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// İkinci seriyi özelleştir
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Renkleri özelleştirerek, tabloyu yalnızca işlevsel değil, aynı zamanda görsel olarak da ilgi çekici hale getirebilirsiniz!

## Adım 7: Her Seri için X ve Y Değerlerini Ayarlayın

Son olarak her bir serimize X ve Y değerlerini atayalım.

```csharp
// İlk serinin X ve Y değerlerini ayarlayın
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// İkinci serinin X ve Y değerlerini ayarlayın
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Değerler 2. adımda doldurduğumuz verilere dayanmaktadır.

## Adım 8: Çalışma Kitabını Kaydedin

Artık her şey ayarlandığına göre, çalışma kitabını kaydedelim, böylece grafiği çalışırken görebilelim.

```csharp
// Çalışma kitabını kaydet
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Ve işte bu kadar! Aspose.Cells for .NET kullanarak veri işaretleyicileriyle bir çizgi grafiği oluşturdunuz.

## Çözüm

Excel'de programatik olarak grafik oluşturmak göz korkutucu görünebilir, ancak .NET için Aspose.Cells ile adım adım bir tarifi takip etmek kadar kolaydır. Çalışma kitabınızı ayarlamaktan grafik görünümünü özelleştirmeye kadar, bu güçlü kütüphane her şeyi halleder. İster raporlar, ister panolar veya veri görselleştirmeleri oluşturun, Aspose.Cells bunu kolayca yapmanızı sağlar.

## SSS

### Tabloyu daha fazla özelleştirebilir miyim?  
Kesinlikle! Aspose.Cells, yazı tiplerinden kılavuz çizgilerine ve daha fazlasına kadar bir ton özelleştirme seçeneği sunuyor.

### Aspose.Cells'i kullanmak için lisansa ihtiyacım var mı?  
 Evet, tam işlevsellik için bir lisans gereklidir. Bir lisans alabilirsiniz.[geçici lisans](https://purchase.aspose.com/temporary-license/) veya bir ile başla[ücretsiz deneme](https://releases.aspose.com/).

### Daha fazla veri serisi nasıl ekleyebilirim?  
 Sadece kullanarak ek seriler ekleyin`NSeries.Add` Yeni veriler için hücre aralıklarını belirten yöntem.

### Tabloyu resim olarak dışarı aktarabilir miyim?  
 Evet, grafikleri doğrudan resim olarak dışa aktarabilirsiniz.`Chart.ToImage` yöntem.

### Aspose.Cells 3D grafikleri destekliyor mu?  
Evet, Aspose.Cells 3D grafikler de dahil olmak üzere çok çeşitli grafik türlerini destekler.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
