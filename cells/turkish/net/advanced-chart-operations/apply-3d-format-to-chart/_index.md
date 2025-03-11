---
title: 3D Formatını Tabloya Uygula
linktitle: 3D Formatını Tabloya Uygula
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'de çarpıcı 3D grafiklerin nasıl oluşturulacağını keşfedin. Basit adım adım kılavuzumuzu izleyin.
weight: 10
url: /tr/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 3D Formatını Tabloya Uygula

## giriiş

Veri görselleştirmenin çok önemli olduğu bir çağda, verilerimizi sunma şeklimiz temel grafiklerin ve çizelgelerin ötesine geçiyor. .NET için Aspose.Cells gibi araçlarla, yalnızca dikkat çekmekle kalmayıp aynı zamanda bilgileri etkili bir şekilde ileten çarpıcı 3B çizelgelerle veri sunumlarınızı yükseltebilirsiniz. Bu kılavuz, Aspose.Cells kullanarak bir çizelgeye 3B biçimi uygulamak için gereken adımlarda size yol gösterecek ve ham verilerinizi ilgi çekici bir gösterime dönüştürecektir.

## Ön koşullar

Bir grafiğe 3D formatının uygulanmasının inceliklerine dalmadan önce, ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım.

### Yazılım Gereksinimleri

- Visual Studio: .NET uygulamalarıyla çalışmak için Visual Studio'nun yüklü olduğundan emin olun.
-  .NET için Aspose.Cells: Eğer henüz yapmadıysanız, Aspose.Cells'i şu adresten indirin ve kurun:[Burada](https://releases.aspose.com/cells/net/).

### Kodlama Ortamı Kurulumu

1. Yeni bir .NET Projesi oluşturun: Visual Studio'yu açın, “Yeni proje oluştur” seçeneğini belirleyin ve bir Konsol Uygulaması seçin.
2. Aspose.Cells Referansını Ekleme: NuGet Paket Yöneticisi aracılığıyla, Aspose.Cells'i arayarak veya Paket Yöneticisi Konsolu aracılığıyla ekleyin:

```bash
Install-Package Aspose.Cells
```

3. Çıktı Dizinini Ayarlayın: Oluşturduğunuz dosyaların kaydedileceği bir çıktı dizini belirleyin; bu, masaüstünüzde bir klasör oluşturmak kadar basit olabilir.

Artık her şey hazır olduğuna göre, kodlara dalıp göz kamaştırıcı 3 boyutlu grafikler oluşturmanın zamanı geldi!

## Paketleri İçe Aktar

Başlamak için gerekli ad alanlarını içe aktarmanız gerekir. Bu, Aspose.Cells tarafından sağlanan sınıflara ve yöntemlere erişmenize yardımcı olacaktır. Bunu nasıl yapacağınız aşağıda açıklanmıştır:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Bu bölüm, süreci yönetilebilir adımlara bölerek her aşama hakkında net bir anlayış sağlayacaktır.

## Adım 1: Çalışma Kitabınızı Başlatın

 İlk olarak, bir örnek oluşturmanız gerekir`Workbook` sınıf. Bu nesne Excel belgenizin temelini oluşturacaktır.

```csharp
//Çıktı dizini
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Bunu düşünün`Workbook` Boş bir tuval olarak—renkli veriler ve etkili görselleştirmelerle doldurmanız için hazır.

## Adım 2: İlk Çalışma Sayfasını Yeniden Adlandırın

Şimdi, ilk çalışma sayfasını yeniden adlandıralım. Bu, hangi verilerle çalıştığımız konusunda netlik sağlar.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

İsimler sezgisel olmalıdır. Bu durumda, verilerimizin nerede yaşadığını bilmek için ona "DataSheet" adını veriyoruz.

## Adım 3: Grafik için Veri Oluşturun

Şimdi "Veri Sayfamıza" biraz veri ekleyelim. Bunu grafiğimizin kullanacağı değerlerle dolduralım.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Bir tarifin malzemelere bağlı olması gibi, grafiğinizin etkinliği de girdiğiniz verilerin kalitesine ve organizasyonuna bağlıdır.

## Adım 4: Yeni Bir Grafik Çalışma Sayfası Ayarlayın

Grafik için yeni bir çalışma sayfası oluşturmanın zamanı geldi. Bu, veri görselleştirmenizi düzenli tutmanıza yardımcı olur.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Bu çalışma sayfasını, verilerinizin performansının ortaya çıktığı bir sahne olarak düşünün.

## Adım 5: Bir Grafik Ekleyin

Burada yeni oluşturulan çalışma sayfasına bir sütun grafiği ekleyeceğiz.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Tablomuz için bir alan tanımlıyoruz ve ne tür olduğunu belirtiyoruz. Bunu, sanat eseriniz için çerçeve türünü seçmek olarak düşünün.

## Adım 6: Grafik Görünümünü Özelleştirin

Şimdi, arka plan renklerini ayarlayarak grafiğimizin görünümünü özelleştirelim. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Temiz beyaz bir arka plan genellikle verilerinizin renklerinin öne çıkmasını sağlayarak görünürlüğü artırır.

## Adım 7: Grafiğe Veri Serileri Ekleyin

Grafiğimize veriyi beslemenin zamanı geldi. Grafiğimizin ihtiyaç duyduğumuz verileri yansıttığından emin olmak için "Veri Sayfamızdan" bir veri dizisi ekleyeceğiz.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Bu, bir şefin belirli malzemelerle bir yemek hazırlamasına benzer. Her veri noktası önemlidir!

## Adım 8: Veri Serisine Erişim ve Biçimlendirme

Artık verilerimiz birbirine bağlı olduğuna göre, veri serisini alıp bazı 3 boyutlu efektler uygulamaya başlayalım.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Yemeğimize biraz lezzet katmaya hazırlanıyoruz; bunu, genel lezzeti artıracak bir baharat olarak düşünün.

## Adım 9: 3D Eğim Efektlerini Uygula

Daha sonra grafiğimize boyut kazandırmak için bir eğim efekti ekleyeceğiz.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Bir heykeltıraşın taşa şekil vermesi gibi, biz de grafiğimizin canlanmasını sağlayacak derinlik yaratıyoruz!

## Adım 10: Yüzey Malzemesini ve Aydınlatmayı Özelleştirin

Tablomuzu parlak hale getirelim! Yüzey malzemesini ve ışık ayarlarını ayarlayacağız.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Uygun aydınlatma ve malzeme düz bir nesneyi büyüleyici bir görsele dönüştürebilir. Her sahneyi geliştirmek için ustaca aydınlatılmış bir film setini düşünün.

## Adım 11: Dizi Görünümünde Son Rötuşlar

Şimdi veri serimizin rengini ayarlayarak görünümünü sonlandıralım.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Doğru renk, belirli hisleri ve tepkileri uyandırabilir; bordo, zarafet ve incelik katar.

## Adım 12: Çalışma Kitabınızı Kaydedin

Son olarak, şaheserinizi kaydetme zamanı geldi! Onu saklamak istediğiniz yeri belirtmeyi unutmayın.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Eserinizi kaydetmek, sanatınızı bir galeriye koymak gibidir; değer verilecek ve paylaşılacak bir andır.

## Çözüm

Tebrikler! Aspose.Cells for .NET kullanarak görsel olarak çekici bir 3D grafik oluşturmayı başardınız. Bu adımları izleyerek, artık veri sunumlarınızı geliştirmek, onları yalnızca bilgilendirici değil aynı zamanda görsel olarak da ilgi çekici hale getirmek için güçlü bir araca sahipsiniz. Grafiklerinizi geliştirirken, her görselleştirmenin bir hikaye olduğunu unutmayın; ilgi çekici, net ve etkili hale getirin!

## SSS

### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, geliştiricilerin Excel belgelerini programlı bir şekilde düzenlemelerine, grafikler ve diyagramlar oluşturmalarına olanak tanıyan güçlü bir kütüphanedir.

### Aspose.Cells'de grafik türlerini özelleştirebilir miyim?
Evet! Aspose.Cells, Sütun, Çizgi, Pasta ve daha birçok farklı grafik türünü destekler ve bunlar kolayca özelleştirilebilir.

### Aspose.Cells için ücretsiz deneme sürümü mevcut mu?
 Kesinlikle! Ücretsiz deneme sürümünü şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/).

### Grafiklere 3D formatların dışında başka efektler uygulayabilir miyim?
Evet, grafiklerinizi 3B'nin ötesine taşımak için gölgeler, degradeler ve farklı stiller gibi çeşitli efektler uygulayabilirsiniz.

### Aspose.Cells için desteği nerede bulabilirim?
 Destek için şu adresi ziyaret edebilirsiniz:[Aspose Forum](https://forum.aspose.com/c/cells/9) Toplum desteği ve yardımı için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
