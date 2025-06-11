---
"description": "Basit adım adım bir eğitimde, Aspose.Cells for .NET kullanarak Excel hücrelerindeki HTML dize değerlerini bir DataTable'a nasıl aktaracağınızı öğrenin."
"linktitle": "Excel'deki Hücrelerin HTML Dize Değerini DataTable'a Aktarma"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'deki Hücrelerin HTML Dize Değerini DataTable'a Aktarma"
"url": "/tr/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'deki Hücrelerin HTML Dize Değerini DataTable'a Aktarma

## giriiş

.NET ortamında Excel dosyalarıyla çalışırken, hücrelerden yalnızca düz metin olarak değil, HTML dizeleri olarak da bilgi çıkarmanız gerekebilir. Zengin metin verileriyle uğraşırken veya biçimlendirmeyi korumak istediğinizde bu oldukça kullanışlı olabilir. Bu kılavuzda, hücrelerin HTML dize değerini .NET için Aspose.Cells kullanarak bir DataTable'a aktarma konusunda size yol göstereceğim. 

## Ön koşullar

Koda dalmadan önce, ihtiyacınız olan her şeyin yerinde olduğundan emin olalım. İşte hızlı bir kontrol listesi:

1. C# ve .NET'in Temel Bilgileri: Kodlamaya başlamadan önce, C# programlamaya ve .NET framework'ünün temellerine aşina olduğunuzdan emin olun.
2. Aspose.Cells for .NET: Henüz yapmadıysanız, Aspose.Cells for .NET'i yüklemeniz gerekir. Ücretsiz deneme sürümünü şuradan indirebilirsiniz: [Burada](https://releases.aspose.com/).
3. Tercih ettiğiniz Visual Studio veya IDE: C# kodu yazmak için ortamınızı kurun. Visual Studio, geniş özellik yelpazesi ve kullanım kolaylığı nedeniyle önerilir.
4. Örnek Excel Dosyası: Bir örnek Excel dosyasına ihtiyacınız olacak (`sampleExportTableAsHtmlString.xlsx`) ile çalışmak için. Erişilebilir bir dizinde bulunduğundan emin olun.
5. NuGet Paket Yöneticisi: Aspose.Cells kütüphanesini kolayca eklemek için projenizde NuGet Paket Yöneticisine erişiminiz olduğundan emin olun.

Bu ön koşulları sağladıktan sonra, biraz kodlamaya girişelim!

## Paketleri İçe Aktar

Aspose.Cells ile çalışmaya başlamadan önce gerekli paketleri içe aktarmamız gerekir. Bu genellikle projenize Aspose.Cells NuGet paketini eklemeyi içerir. İşte nasıl yapılacağı:

### NuGet Paket Yöneticisini Açın

Visual Studio'da Çözüm Gezgini'nde projenize sağ tıklayın ve NuGet Paketlerini Yönet'i seçin.

### Aspose.Cells'i arayın

NuGet Paket Yöneticisi'nde şunu yazın: `Aspose.Cells` Arama çubuğunda.

### Paketi yükleyin

Aspose.Cells'i bulduğunuzda, Install butonuna tıklayın. Bu, kütüphaneyi projenize ekleyecek ve kodunuza içe aktarmanıza olanak tanıyacaktır.

### Ad Alanını İçe Aktar

Kod dosyanızın en üstüne aşağıdaki using yönergesini ekleyin:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Artık her şeyi ayarladığımıza göre, HTML dize değerlerini bir Excel dosyasından bir DataTable'a adım adım aktarma sürecine geçelim. 

## Adım 1: Kaynak Dizini Tanımlayın

Örnek Excel dosyanızın depolandığı dizini tanımlayarak başlayacaksınız. Bu, uygulamanıza dosyayı nerede bulacağını söylediği için önemlidir. İşte bunun için kod:

```csharp
string sourceDir = "Your Document Directory";
```

Değiştirdiğinizden emin olun `"Your Document Directory"` Excel dosyanızın gerçek yolunu belirtin.

## Adım 2: Örnek Excel Dosyasını Yükleyin

Bir sonraki adım Excel çalışma kitabını yüklemektir. `Workbook` Bunu yapmak için Aspose.Cells'den bir sınıf kullanın. Dosyayı şu şekilde yükleyebilirsiniz:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Bu basit kod satırı çalışma kitabını başlatır ve belirtilen Excel dosyasını yükler.

## Adım 3: İlk Çalışma Sayfasına Erişim

Çalışma kitabı yüklendikten sonra, ilgilendiğiniz verileri içeren belirli çalışma sayfasına erişmek isteyeceksiniz. Genellikle, ilk çalışma sayfasıyla başlayacaksınız:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Burada ilk çalışma sayfasıyla (indeks 0) çalışıyoruz. Verilerinizin doğru sayfada olduğundan emin olun.

## Adım 4: Dışa Aktarma Tablosu Seçeneklerini Belirleyin

Verilerin nasıl dışa aktarılacağını kontrol etmek için şunları ayarlamanız gerekir: `ExportTableOptions`Bu durumda, sütun adlarının dışa aktarılmamasını ve hücre verilerinin HTML dizeleri olarak dışa aktarılmasını istersiniz:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Bu yapılandırma, hücre verilerinizi dışa aktarırken zengin biçimlendirmeyi korumanıza olanak tanır.

## Adım 5: Hücreleri DataTable'a Aktar

Şimdi verileri gerçekten dışa aktardığınız kritik kısım geliyor. `ExportDataTable` yöntemi, verileri çalışma sayfasından bir `DataTable`Bunu nasıl yapacağınız aşağıda açıklanmıştır:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Bu kod, daha önce belirtilen seçenekleri kullanarak belirtilen bir hücre aralığını (satır 0, sütun 0'dan satır 3, sütun 3'e kadar) bir DataTable'a aktarır.

## Adım 6: HTML Dize Değerini Yazdırın

Son olarak, DataTable'daki belirli bir hücreden HTML dize değerini yazdırıp neyi dışa aktarabildiğimizi görelim. Örneğin, üçüncü satır ve ikinci sütundaki değeri yazdırmak istiyorsanız, şunları yaparsınız:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Bu satır DataTable'daki istenilen HTML dizesini konsola yazdırır. 

## Çözüm 

Ve işte oldu! Aspose.Cells for .NET kullanarak bir Excel dosyasındaki hücrelerden HTML dize değerlerini bir DataTable'a başarıyla aktardınız. Bu yetenek yalnızca veri işleme becerilerinizi zenginleştirmekle kalmaz, aynı zamanda Excel dosyalarından doğrudan biçimlendirilmiş içerikle uğraşırken seçeneklerinizi de genişletir. 

## SSS

### Aspose.Cells'i Excel dışında başka dosya formatlarında da kullanabilir miyim?  
Evet, Aspose.Cells öncelikli olarak Excel içindir, ancak Aspose farklı formatlar için başka kütüphaneler de sunmaktadır.

### Aspose.Cells için lisansa ihtiyacım var mı?  
Evet, üretim kullanımı için geçerli bir lisans gereklidir. Geçici bir lisans alabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).

### Excel dosyam formüller içeriyorsa ne olur? Bunlar doğru şekilde dışa aktarılır mı?  
Evet, Aspose.Cells formülleri işleyebilir ve dışa aktarıldığında, bunlar sonuç değerlerine göre değerlendirilir.

### İhracat seçeneklerini değiştirmek mümkün mü?  
Kesinlikle! Özelleştirebilirsiniz `ExportTableOptions` özel ihtiyaçlarınıza uyacak şekilde.

### Aspose.Cells için daha detaylı dokümantasyonu nerede bulabilirim?  
Kapsamlı dokümanları bulabilirsiniz [Burada](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}