---
"description": "Aspose.Cells for .NET ile Excel pivot tablolarını yönetmeyi öğrenin; veri güncellemeleri, uyumluluk ayarları ve hücre biçimlendirmesi dahil."
"linktitle": "Excel Dosyasının .NET'te Programatik Olarak Uyumluluğunu Belirleyin"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel Dosyasının .NET'te Programatik Olarak Uyumluluğunu Belirleyin"
"url": "/tr/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Dosyasının .NET'te Programatik Olarak Uyumluluğunu Belirleyin

## giriiş

Günümüzün veri odaklı dünyasında, Excel dosyalarını programatik olarak yönetmek ve düzenlemek birçok geliştirici için olmazsa olmaz hale geldi. .NET'te Excel ile çalışıyorsanız, Aspose.Cells Excel dosyalarını oluşturmayı, okumayı, değiştirmeyi ve kaydetmeyi kolaylaştıran güçlü bir kütüphanedir. Bu kütüphanenin önemli bir özelliği Excel dosyalarının uyumluluğunu programatik olarak belirlemenize olanak tanır. Bu eğitimde, özellikle .NET için Aspose.Cells kullanarak uyumluluğu yönetmeye odaklanarak Excel dosyalarını nasıl düzenleyeceğinizi inceleyeceğiz. Sonunda, verileri yenilerken ve yönetirken özellikle pivot tablolar için Excel dosyaları için uyumluluğu nasıl ayarlayacağınızı anlayacaksınız.

## Ön koşullar

Kodlama aşamasına geçmeden önce aşağıdakilere sahip olduğunuzdan emin olun:

1. Temel C# bilgisi: C# dilinde kod yazacağımız için, dile aşina olmanız eğitimi daha iyi anlamanıza yardımcı olacaktır.
2. Aspose.Cells for .NET kütüphanesi: Bunu şu adresten indirebilirsiniz: [Aspose Cells sürüm sayfası](https://releases.aspose.com/cells/net/). Eğer henüz yapmadıysanız, özelliklerini keşfetmek için ücretsiz deneme sürümünü almayı düşünebilirsiniz.
3. Visual Studio: C# kodlarınızı etkili bir şekilde yazıp test edebileceğiniz bir IDE.
4. Örnek Excel Dosyası: Bir örnek Excel dosyanız olduğundan emin olun, tercihen demo için bir pivot tablo içeren bir dosya. Örneğimiz için şunu kullanacağız: `sample-pivot-table.xlsx`.

Bu ön koşulları sağladıktan sonra kodlama sürecine başlayalım.

## Paketleri İçe Aktar

Uygulamanızı yazmaya başlamadan önce, Aspose.Cells kütüphanesini etkili bir şekilde kullanmak için gerekli ad alanlarını kodunuza eklemeniz gerekir. İşte bunu nasıl yapacağınız.

### Aspose.Cells Ad Alanını İçe Aktar

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Bu kod satırı, Aspose.Cells kütüphanesindeki tüm sınıflara ve yöntemlere erişebilmenizi sağlar.

Şimdi, her şeyin açık ve anlaşılır olduğundan emin olmak için süreci ayrıntılı olarak ele alalım.

## Adım 1: Dizininizi Ayarlayın

İlk önce, Excel dosyalarınızın bulunduğu dizini ayarlayın. Doğru dosya yolunu sağlamak önemlidir.

```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```

Burada, değiştirin `"Your Document Directory"` Excel dosyalarınızın gerçek yolu ile. Örnek pivot tablo dosyanızın bulunması gereken yer burasıdır.

## Adım 2: Kaynak Excel Dosyasını Yükleyin

Daha sonra örnek pivot tabloyu içeren Excel dosyasını yüklememiz gerekiyor. 

```csharp
// Örnek pivot tabloyu içeren kaynak excel dosyasını yükleyin
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

Bu adımda, bir örnek oluşturuyoruz `Workbook` Belirtilen Excel dosyasını yükleyen sınıf. 

## Adım 3: Çalışma Sayfalarına Erişim

Çalışma kitabı yüklendiğine göre, pivot tablo verilerini içeren çalışma sayfasına erişmeniz gerekiyor.

```csharp
// Pivot tablo verilerini içeren ilk çalışma sayfasına erişin
Worksheet dataSheet = wb.Worksheets[0];
```

Burada, pivot tablonun bulunduğu ilk çalışma sayfasına erişiyoruz. Ayrıca Excel yapınıza göre diğer çalışma sayfalarında dolaşabilir veya bunları belirtebilirsiniz.

## Adım 4: Hücre Verilerini İşleyin

Şimdi çalışma sayfanızdaki bazı hücre değerlerini değiştireceksiniz. 

### Adım 4.1: A3 Hücresini Değiştirin

Öncelikle A3 hücresine erişip değerini ayarlayalım.

```csharp
// A3 hücresine erişin ve verilerini ayarlayın
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Bu kod parçacığı A3 hücresini “FooBar” değeriyle günceller.

### Adım 4.2: B3 Hücresini Uzun Dize ile Değiştirin

Şimdi, B3 hücresine Excel'in standart karakter sınırlarını aşan uzun bir dize yerleştirelim.

```csharp
// B3 hücresine erişin, verilerini ayarlayın
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Bu kod önemlidir çünkü özellikle Excel'de uyumluluk ayarlarıyla çalışırken veri sınırlarına ilişkin beklentilerinizi belirler.

## Adım 5: B3 Hücresinin Uzunluğunu Kontrol Edin

Girdiğimiz dizenin uzunluğunu teyit etmemiz de önemlidir.

```csharp
// B3 hücresinin uzunluğunu yazdır dizesi
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Bu sadece hücrenizin kaç karakter tuttuğunu doğrulamak içindir.

## Adım 6: Diğer Hücre Değerlerini Ayarlayın

Şimdi daha fazla hücreye erişeceğiz ve bazı değerler belirleyeceğiz.

```csharp
// C3 hücresine erişin ve verilerini ayarlayın
cell = cells["C3"];
cell.PutValue("closed");

// D3 hücresine erişin ve verilerini ayarlayın
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Bu kod parçacıklarının her biri çalışma sayfasındaki birkaç ek hücreyi günceller.

## Adım 7: Pivot Tablosuna Erişim

Daha sonra pivot tablo verilerinden oluşan ikinci çalışma sayfasına erişeceksiniz.

```csharp
// Pivot tabloyu içeren ikinci çalışma sayfasına erişin
Worksheet pivotSheet = wb.Worksheets[1];

// Pivot tabloya erişin
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Bu kod parçası pivot tablonun uyumluluk ayarlarını değiştirmenize olanak tanır.

## Adım 8: Excel 2003 için Uyumluluğu Ayarlayın

Pivot tablonuzun Excel 2003 ile uyumlu olup olmadığını ayarlamanız çok önemlidir. 

```csharp
// IsExcel2003Compatible özelliği, PivotTable'ı yenilerken PivotTable'ın Excel2003 ile uyumlu olup olmadığını söyler
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Gerçek dönüşüm burada başlıyor. `IsExcel2003Compatible` ile `true`yenileme sırasında karakter uzunluklarını 255 ile sınırlandırırsınız.

## Adım 9: Uyumluluk Ayarından Sonra Uzunluğu Kontrol Edin

Uyumluluğu ayarladıktan sonra verileri nasıl etkilediğine bakalım.

```csharp
// Pivot tablonun B5 hücresinin değerini kontrol edin.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Başlangıç verileri 255 karakteri aşarsa, muhtemelen kesme etkisini doğrulayan bir çıktı göreceksiniz.

## Adım 10: Uyumluluk Ayarını Değiştirin

Şimdi uyumluluk ayarını değiştirip tekrar kontrol edelim.

```csharp
// Şimdi IsExcel2003Compatible özelliğini false olarak ayarlayın ve tekrar yenileyin
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Bu, verilerinizin önceki kısıtlamalar olmaksızın orijinal uzunluğunu yansıtmasını sağlar.

## Adım 11: Uzunluğu Tekrar Doğrulayın 

Verinin gerçek uzunluğunu doğru bir şekilde yansıttığını doğrulayalım.

```csharp
// Şimdi hücre verisinin orijinal uzunluğunu yazdıracak. Veriler artık kesilmedi.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Çıktının kesmenin kaldırıldığını doğruladığını görmelisiniz.

## Adım 12: Hücreleri Biçimlendirin

Görsel deneyimi geliştirmek için hücreleri biçimlendirmek isteyebilirsiniz. 

```csharp
// B5 hücresinin satır yüksekliğini ve sütun genişliğini ayarlayın ve ayrıca metnini sarın
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Bu kod satırları, hücre boyutlarını ayarlayarak ve metin kaydırmayı etkinleştirerek verilerin daha kolay okunmasını sağlar.

## Adım 13: Çalışma Kitabını Kaydedin

Son olarak çalışma kitabınızı yaptığınız değişikliklerle kaydedin.

```csharp
// Çalışma kitabını xlsx biçiminde kaydet
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Excel dosyalarını kaydederken uygun bir dosya biçimi seçmek çok önemlidir. `Xlsx` formatı yaygın olarak kullanılır ve birçok Excel sürümüyle uyumludur.

## Çözüm

Tebrikler! Artık Aspose.Cells for .NET kullanarak Excel dosya uyumluluk ayarlarını programladınız. Bu eğitimde, ortamınızı kurmaktan pivot tablolar için uyumluluk ayarlarını değiştirmeye kadar her adım özetlenmiştir. Belirli sınırlamalar veya uyumluluk gerektiren verilerle çalıştıysanız, bu göz ardı etmek istemeyeceğiniz bir beceridir.

## SSS

### Aspose.Cells Nedir?  
Aspose.Cells, geliştiricilerin Excel dosyalarını sorunsuz bir şekilde oluşturmalarına, düzenlemelerine ve dönüştürmelerine yardımcı olmak için tasarlanmış bir .NET kütüphanesidir.

### Excel uyumluluğu neden önemlidir?  
Excel uyumluluğu, özellikle önceki sürümlerde desteklenmeyen özellikler veya biçimler içeriyorsa, dosyaların istenen Excel sürümlerinde açılıp kullanılabilmesini sağlamak açısından çok önemlidir.

### Aspose.Cells ile programlı olarak Pivot Tablolar oluşturabilir miyim?  
Evet, Aspose.Cells kullanarak Pivot Tabloları programatik olarak oluşturabilir ve düzenleyebilirsiniz. Kütüphane, Pivot Tablolarla ilişkili veri kaynakları, alanlar ve özellikler eklemek için çeşitli yöntemler sunar.

### Excel hücresindeki bir dizenin uzunluğunu nasıl kontrol edebilirim?  
Kullanabilirsiniz `StringValue` birinin mülkü `Cell` hücrenin içeriğini almak ve ardından çağırmak için nesne `.Length` Dizenin uzunluğunu bulmak için özellik.

### Satır yüksekliği ve genişliğinin ötesinde hücre biçimlendirmesini özelleştirebilir miyim?  
Kesinlikle! Aspose.Cells kapsamlı hücre biçimlendirmesine izin verir. Yazı tipi stillerini, renkleri, kenarlıkları, sayı biçimlerini ve çok daha fazlasını şu şekilde değiştirebilirsiniz: `Style` sınıf.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}