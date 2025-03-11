---
title: Grafiğe TextBox Denetimi Ekle
linktitle: Grafiğe TextBox Denetimi Ekle
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak Excel'deki grafiklere TextBox eklemeyi öğrenin. Veri görselleştirmenizi zahmetsizce geliştirin.
weight: 12
url: /tr/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiğe TextBox Denetimi Ekle

## giriiş

Excel'de dinamik ve görsel olarak çekici grafikler oluşturmak, verileri etkili bir şekilde temsil etmenin harika bir yoludur. Kullanabileceğiniz şık bir özellik, bir grafiğe bir TextBox eklemektir. .NET için Aspose.Cells ile bu görev kolay ve eğlenceli hale gelir! Bu kılavuzda, bir TextBox'ı grafiğinize adım adım entegre etme sürecini adım adım anlatacağız. İster deneyimli bir geliştirici olun, ister yeni başlıyor olun, bu eğitim Excel grafiklerinizi geliştirmek için ihtiyacınız olan tüm araçları size verecektir. Peki, dalmaya hazır mısınız?

## Ön koşullar

Kodlamaya başlamadan önce, elinizde olması gereken birkaç şey var:

- C#'ın Temel Anlayışı: C# programlamanın temellerine hakim olmak faydalı olacaktır. Endişelenmeyin; uzman olmanıza gerek yok, sadece sözdiziminde gezinme konusunda rahat olmanız yeterli.
-  Yüklü Aspose.Cells Kütüphanesi: Aspose.Cells for .NET kütüphanesinin yüklü olduğundan emin olun. Buradan indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/) Eğer henüz yapmadıysanız.
- Visual Studio: .NET framework için kullanmayı tercih ettiğiniz Visual Studio veya herhangi bir IDE'ye aşinalık şarttır.
- Mevcut Bir Excel Dosyası: Bu örnek için, "sampleAddingTextBoxControlInChart.xls" adlı mevcut bir Excel dosyasıyla çalışacağız. Bir tane oluşturabilir veya bir örnek indirebilirsiniz.

Artık her şey yerli yerinde olduğuna göre kodlama kısmına geçebiliriz!

## Paketleri İçe Aktar

İlk önce, gerekli Aspose.Cells ad alanlarını C# projemize aktarmamız gerekiyor. Bunu kod dosyanızın en üstüne aşağıdaki satırları ekleyerek kolayca yapabilirsiniz:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Adım 1: Kaynak ve Çıktı Dizinlerinizi Tanımlayın

Excel dosyasıyla çalışmaya başlamadan önce, giriş dosyanızın nerede bulunduğunu ve çıktı dosyasını nereye kaydetmek istediğinizi tanımlamanız önemlidir. Bu, projenizi düzenli tutmanıza yardımcı olur.

```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";

// Çıktı dizini
string outputDir = "Your Output Directory";
```
 Yer değiştirmek`"Your Document Directory"` Ve`"Your Output Directory"` sisteminizdeki gerçek yollarla.

## Adım 2: Mevcut Excel Dosyasını Açın

Sonra, değiştirmek istediğimiz grafiği içeren Excel dosyasını açmamız gerekiyor. Bu, grafiği almamızı ve değişiklikler yapmamızı sağlayacaktır.

```csharp
// Mevcut dosyayı açın.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Bu satır, belirttiğimiz dosyayla yeni bir Çalışma Kitabı nesnesi başlatır.

## Adım 3: Çalışma Sayfasındaki Tabloya Erişim

Excel'deki grafikler bir çalışma sayfasında saklandığından, önce çalışma sayfasına erişmemiz ve ardından istenen grafiği almamız gerekir. Bu örnek için, ilk çalışma sayfasındaki ilk grafiğe erişeceğiz.

```csharp
// İlk sayfada tasarımcı şemasını alın.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Dizin değerini değiştirerek dosyanızda daha fazla varsa farklı çalışma sayfaları veya grafikler seçebilirsiniz.

## Adım 4: Grafiğe Yeni Bir Metin Kutusu Ekleyin

Şimdi TextBox'ımızı eklemeye hazırız. Oluştururken konumunu ve boyutunu belirteceğiz.

```csharp
// Grafiğe yeni bir metin kutusu ekleyin.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Bu komutta, parametreler grafikteki TextBox'ın konumunu (x, y) ve boyutunu (genişlik, yükseklik) tanımlar. Bu değerleri belirli düzen ihtiyaçlarınıza göre ayarlayın.

## Adım 5: TextBox için Metni Ayarlayın

TextBox yerleştirildikten sonra, onu içerikle doldurma zamanı geldi. Grafiğiniz için gerekli gördüğünüz herhangi bir metni ekleyebilirsiniz.

```csharp
// Metni doldurun.
textbox0.Text = "Sales By Region";
```
"Bölgeye Göre Satışlar" kısmını verilerinizle ilgili herhangi bir metinle değiştirmekten çekinmeyin.

## Adım 6: TextBox Özelliklerini Ayarlayın

Şimdi TextBox'ımızı güzel gösterelim! Yazı tipi rengi, boyutu ve stili gibi çeşitli özellikleri özelleştirebilirsiniz.

```csharp
// Yazı rengini ayarlayın.
textbox0.Font.Color = Color.Maroon; // İstediğiniz renge değiştirin

// Yazı tipini kalın olarak ayarlayın.
textbox0.Font.IsBold = true;

// Yazı tipi boyutunu ayarlayın.
textbox0.Font.Size = 14;

// Yazı tipi özelliğini italik olarak ayarlayın.
textbox0.Font.IsItalic = true;
```

Bu satırların her biri TextBox'ınızın içindeki metnin görünümünü değiştirerek görünürlüğünü ve çekiciliğini artırır.

## Adım 7: TextBox Görünümünü Biçimlendirin

TextBox'ın arkaplanını ve kenarlığını biçimlendirmek de önemlidir. Bu, onu grafikte öne çıkarır.

```csharp
// Metin kutusunun doldurma biçimini alın.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Metin kutusunun satır biçim türünü alın.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Çizgi kalınlığını ayarlayın.
lineformat.Weight = 2;

// Çizgi stilini düz olarak ayarlayın.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Bu seçenekler TextBox'ın arka plan dolgusunu ayarlamanıza ve kenarlığını özelleştirmenize olanak tanır.

## Adım 8: Değiştirilen Excel Dosyasını Kaydedin

Son adım, yaptığınız değişiklikleri yeni bir Excel dosyasına kaydetmektir. Bu, orijinal dosyanızın dokunulmadan kalmasını sağlayacaktır.

```csharp
// Excel dosyasını kaydedin.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Yer değiştirmek`"outputAddingTextBoxControlInChart.xls"` istediğiniz dosya adıyla.

## Çözüm

Tebrikler! Aspose.Cells for .NET kullanarak bir grafiğe başarıyla bir TextBox denetimi eklediniz. Bu basit ancak etkili değişiklik, grafiklerinizi daha bilgilendirici ve görsel olarak çekici hale getirebilir. Veri gösterimi etkili iletişimin anahtarıdır ve Aspose gibi araçlarla bu sunumu en az çabayla geliştirme gücüne sahipsiniz.

## SSS

### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, Microsoft Excel'e güvenmeye gerek kalmadan Excel dosyaları oluşturmak, düzenlemek ve dönüştürmek için güçlü bir kütüphanedir.

### Tek bir grafiğe birden fazla TextBox ekleyebilir miyim?
Evet! TextBox oluşturma adımlarını farklı pozisyonlarda tekrarlayarak ihtiyacınız kadar TextBox ekleyebilirsiniz.

### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ücretli bir kütüphanedir, ancak ücretsiz deneme sürümünü şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?
 Kapsamlı belgelere erişebilirsiniz[Burada](https://reference.aspose.com/cells/net/).

### Sorun yaşarsam nasıl destek alabilirim?
 Aspose destek forumundan yardım isteyebilirsiniz[Burada](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
