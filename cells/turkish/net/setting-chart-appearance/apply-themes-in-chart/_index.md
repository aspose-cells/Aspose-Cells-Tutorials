---
title: Tabloda Temaları Uygula
linktitle: Tabloda Temaları Uygula
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET'i kullanarak Excel'deki grafiklere temaları nasıl uygulayacağınızı, kolay takip edilebilen adım adım kılavuzumuzla öğrenin. Veri sunumunuzu geliştirin.
weight: 10
url: /tr/net/setting-chart-appearance/apply-themes-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabloda Temaları Uygula

## giriiş

Excel'de görsel olarak çekici grafikler oluşturmak verilerinizi etkili bir şekilde iletmek için çok önemlidir. Temalar uygulayarak grafiklerinizin estetiğini artırabilir, bilgileri yalnızca erişilebilir değil, aynı zamanda ilgi çekici hale getirebilirsiniz. Bu kılavuzda, .NET için Aspose.Cells kullanarak temaların nasıl uygulanacağını keşfedeceğiz. O halde en sevdiğiniz atıştırmalığı alın ve grafiklerin yaratıcı dünyasına dalalım!

## Ön koşullar

Kodlama bölümüne geçmeden önce, yerine getirmeniz gereken birkaç ön koşul var.

### Gerekli Yazılım

1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. .NET uygulamaları geliştirmek için kullanıcı dostu bir ortam sağlar.
2. .NET Framework veya .NET Core: Tercihinize bağlı olarak, kodumuzu takip edecek şekilde .NET Framework veya .NET Core'un kurulu olması gerekir.
3.  Aspose.Cells for .NET: Bunu kaçıramazsınız! Başlamak için Aspose.Cells for .NET'i indirin. DLL'leri bulabilirsiniz[Burada](https://releases.aspose.com/cells/net/).
4. C# Temel Bilgisi: Kodu adım adım size anlatacağız ancak C# ile ilgili temel bilgilere sahip olmak kesinlikle yardımcı olacaktır.

## Paketleri İçe Aktar

Aspose.Cells for .NET ile çalışmak için ilk adım gerekli paketleri içe aktarmaktır. C# projenize aşağıdaki ad alanını ekleyin:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

Artık ön koşullarımızı tamamladığımıza göre, Excel'de bir grafiğe tema uygulama sürecini adım adım inceleyelim.

## Adım 1: Çıktı ve Kaynak Dizinlerinizi Ayarlayın

Yapmamız gereken ilk şey çıktı dizinimizi ve kaynak dizinimizi oluşturmaktır. Excel dosyalarınızı buradan yükleyeceksiniz ve değiştirilen dosyalar buraya kaydedilecektir.

```csharp
// Çıktı dizini
string outputDir = "Your Output Directory";

// Kaynak dizini
string sourceDir = "Your Document Directory";
```

 Burada, değiştirin`Your Output Directory` Ve`Your Document Directory` belirli yollarınızla. Bu dizinlerin açıkça tanımlanması iş akışınızı kolaylaştıracak ve ileride herhangi bir karışıklığın önüne geçecektir.

## Adım 2: Çalışma Kitabını Örneklendirin

 Sırada, değiştirmek istediğiniz grafiği içeren Excel dosyasını açma zamanı var. Bunu, bir örneğini oluşturarak yapıyoruz`Workbook` sınıfımızı oluşturuyoruz ve kaynak dosyamızı yüklüyoruz.

```csharp
// Bir grafik içeren dosyayı açmak için çalışma kitabını örneklendirin
Workbook workbook = new Workbook(sourceDir + "sampleApplyingThemesInChart.xlsx");
```

 Emin olun ki`sampleApplyingThemesInChart.xlsx` kaynak dizininizde mevcuttur.

## Adım 3: Çalışma Sayfasına Erişim

Artık çalışma kitabımız hazır olduğuna göre, bir sonraki adım grafiğimizi içeren belirli çalışma sayfasına erişmektir. 

```csharp
// İlk çalışma kağıdını al
Worksheet worksheet = workbook.Worksheets[0];
```

Bu durumda, bu örnek için yeterli olan ilk çalışma sayfasını alıyoruz. Birden fazla sayfanız varsa, gereksinimlerinize göre sayfa dizinini veya adını belirtebilirsiniz.

## Adım 4: Tabloyu Alın

Çalışma kağıdı elimizde olduğuna göre artık biçimlendirmek istediğimiz grafiğe ulaşabiliriz.

```csharp
// Sayfadaki ilk çizelgeyi alın
Chart chart = worksheet.Charts[0];
```

İşte ilk grafiği alıyoruz. Çalışma sayfanız birden fazla grafik içeriyorsa ve belirli bir grafik istiyorsanız, dizini buna göre değiştirmeniz yeterlidir.

## Adım 5: Seriye Katı Dolgu Uygulayın

Bir temayı uygulamadan önce, grafik serimizin sağlam bir dolguya sahip olduğundan emin olalım. Bunu nasıl ayarlayabileceğiniz aşağıda açıklanmıştır:

```csharp
// FillFormat'ın türünü ilk serinin Solid Fill'i olarak belirtin
chart.NSeries[0].Area.FillFormat.FillType = Aspose.Cells.Drawing.FillType.Solid;
```

Bu kod satırı, grafikteki ilk serinin düz dolgu kullanacak şekilde ayarlanmasını sağlar.

## Adım 6: Rengi Yapılandırın

 Artık dizimiz hazır olduğuna göre, rengini değiştirmemiz gerekiyor. Bu, bir dizi oluşturmayı içerir.`CellsColor` nesne ve bir tema rengi belirterek. Bu örnek için bir vurgu stili seçeceğiz.

```csharp
//SolidFill'in CellsColor'ını alın
CellsColor cc = chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor;

// Accent stilinde bir tema oluşturun
cc.ThemeColor = new ThemeColor(ThemeColorType.Accent6, 0.6);
```

İşte olanlar:
1. Katı dolgunun rengini elde ediyoruz.
2.  Kullanarak`ThemeColor` , katı dolgumuz için bir renk belirledik. Değiştirebilirsiniz`Accent6` İstediğiniz tema rengine göre başka bir tema rengine dönüştürebilirsiniz.

## Adım 7: Temayı Seriye Uygulayın

Rengi ayarladıktan sonra, sıra yeni temayı serimize uygulamaya geldi. 

```csharp
// Temayı diziye uygulayın
chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor = cc;
```

Bu çizgi grafikteki renkleri etkili bir şekilde günceller. 

## Adım 8: Çalışma Kitabını Kaydedin

Tüm bu zor çalışmalardan sonra, değişikliklerimizi yeni bir Excel dosyasına kaydetmemiz gerekiyor.

```csharp
// Excel dosyasını kaydedin
workbook.Save(outputDir + "outputApplyingThemesInChart.xlsx");
```

Burada, değiştirilmiş çalışma kitabını daha önce belirttiğiniz çıktı dizinine kaydediyoruz. 

## Adım 9: Onay Çıktısı

İşlemin başarıyla yürütüldüğünü kendimize bildirmek için bir onay mesajı yazdırabiliriz:

```csharp
Console.WriteLine("ApplyingThemesInChart executed successfully.");
```

Bu satır konsolda görevin tamamlandığını belirten bir mesaj çıktısı verecektir.

## Çözüm

Aspose.Cells for .NET kullanarak Excel'deki grafiklerinize temalar uygulamak, verilerinizin görüntülenme biçimini tamamen değiştirebilir. Grafiklerinizi estetik olarak hoş hale getirmekle kalmaz, aynı zamanda mesajınızı daha etkili bir şekilde iletmenize de yardımcı olur. Bu kılavuzda özetlenen adımları izleyerek grafiklerinizi kolayca özelleştirebilir ve verilerinizi hedef kitlenizin dikkatini çekecek şekilde sunabilirsiniz.

## SSS

### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Excel dosyalarını program aracılığıyla düzenlemelerine olanak tanıyan güçlü bir .NET kütüphanesidir.

### Satın almadan önce Aspose.Cells'i deneyebilir miyim?
 Evet, ücretsiz denemeyi indirebilirsiniz[Burada](https://releases.aspose.com/).

### Hangi tür grafik temalarını uygulayabilirim?
Aspose.Cells, Vurgu stilleri ve diğerleri de dahil olmak üzere çeşitli tema renklerini destekler.

### Birden fazla grafiğe tema uygulamak mümkün müdür?
Kesinlikle! Döngüye girebilirsin`worksheet.Charts` ve ihtiyaç halinde temaları uygulayın.

### Aspose.Cells için desteği nereden alabilirim?
 Destek alabilir ve kullanıcı topluluğuyla etkileşim kurabilirsiniz[Burada](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
