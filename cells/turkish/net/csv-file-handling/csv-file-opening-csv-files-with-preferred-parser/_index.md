---
title: CSV Dosyalarını Tercih Edilen Ayrıştırıcı ile Açma
linktitle: CSV Dosyalarını Tercih Edilen Ayrıştırıcı ile Açma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: .NET için Aspose.Cells'de özel ayrıştırıcılarla CSV dosyalarını nasıl açıp ayrıştıracağınızı öğrenin. Metin ve tarihleri zahmetsizce işleyin. Geliştiriciler için mükemmel.
weight: 11
url: /tr/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CSV Dosyalarını Tercih Edilen Ayrıştırıcı ile Açma

## giriiş
CSV dosyalarıyla uğraşırken, bazen farklı veri türlerini özel ayrıştırıcılarla işlemek istersiniz. Bu eğitim, .NET için Aspose.Cells kullanarak tercih edilen bir ayrıştırıcıyla CSV dosyalarını nasıl açacağınız konusunda size rehberlik edecektir. İster metin, ister tarih veya diğer özel biçimleri işlemek isteyin, bu kılavuz her adımda net bir açıklamayla size yol gösterecektir.
## Ön koşullar
Koda dalmadan önce, başlamak için ihtiyacınız olan temel öğeleri ele alalım.
1.  Aspose.Cells for .NET Kütüphanesi: Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. İndirebilirsiniz[Burada](https://releases.aspose.com/cells/net/) Ayrıca ücretsiz denemeyi de kullanabilirsiniz[Burada](https://releases.aspose.com/).
2. .NET Geliştirme Ortamı: Visual Studio önerilir, ancak herhangi bir .NET uyumlu IDE çalışacaktır.
3. Temel C# Bilgisi: Bu eğitimde C# ve nesne yönelimli programlamaya aşina olduğunuzu varsayıyoruz.
## Paketleri İçe Aktar
Aspose.Cells'i kullanmak için, C# dosyanızın en üstüne gerekli ad alanlarını aktarmanız gerekir:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Artık ortamı hazırladığımıza göre, metin ve tarih gibi farklı veri biçimlerini işleyen tercih edilen bir ayrıştırıcıyla bir CSV dosyasının nasıl açılacağını inceleyelim.
## Adım 1: Özel Ayrıştırıcıları Tanımlayın
 Metin veya belirli tarih biçimleri gibi farklı veri türlerini işlemek için özel ayrıştırıcılar tanımlamanız gerekir. Aspose.Cells'de özel ayrıştırıcılar şunları uygular:`ICustomParser` arayüz.
### 1.1 Bir Metin Ayrıştırıcısı Oluşturun
Bu ayrıştırıcı normal metin değerlerini işler. Biçimi değiştirmez, bu nedenle değer olduğu gibi döndürülür.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 The`ParseObject` method sadece girdi değerini döndürür. "Hiçbir şeyi değiştirme, sadece bana metni ver!" demek gibidir.
### 1.2 Bir Tarih Ayrıştırıcısı Oluşturun
 Tarihler için CSV verilerinin doğru şekilde ayrıştırıldığından emin olmak isteyeceksiniz`DateTime` nesneler. İşte bir tarih ayrıştırıcısı oluşturmanın yolu:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 Bu ayrıştırıcıda şunu kullanırız:`ParseExact` Tarihin önceden tanımlanmış bir biçime göre doğru şekilde yorumlanmasını sağlamak için (`"dd/MM/yyyy"`). Bu şekilde, CSV dosyanızdaki bu formatı izleyen herhangi bir tarih sorunsuz bir şekilde işlenecektir.
## Adım 2: Yükleme Seçeneklerini Yapılandırın
 Sonra, CSV dosyasının nasıl yükleneceğini yapılandırmanız gerekir. Bu, şu şekilde yapılır:`TxtLoadOptions` Kodlama ve özel ayrıştırıcılar da dahil olmak üzere ayrıştırma seçeneklerini belirtmenize olanak tanıyan sınıf.
### 2.1 Yükleme Seçeneklerini Ayarlayın
 Başlatma işlemiyle başlayacağız`TxtLoadOptions` ve ayırıcı ve kodlama gibi temel parametrelerin tanımlanması:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Ayırıcı: Bu, CSV dosyasındaki değerleri ayırmak için kullanılan karakteri tanımlar (bu durumda virgül).
- Kodlama: Geniş bir karakter yelpazesini işlemek için UTF-8 kodlamasını kullanıyoruz.
-  ConvertDateTimeData: Bunu true olarak ayarlamak, tarih değerlerinin otomatik olarak dönüştürülmesini sağlar`DateTime` Mümkün olduğunda nesneler.
### 2.2 Özel Ayrıştırıcıları Uygula
Daha sonra, daha önce oluşturduğumuz ayrıştırıcıları CSV'deki değerleri işlemek üzere atayacağız:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Bu, Aspose.Cells'e şunu kullanmasını söyler:`TextParser` genel metin değerleri ve`DateParser`CSV dosyasında karşılaştığı herhangi bir tarih alanı için.
## Adım 3: CSV Dosyasını Yükleyin ve Okuyun
 Artık yükleme seçenekleri yapılandırıldığına göre CSV dosyasını bir`Aspose.Cells.Workbook` nesne.
### 3.1 CSV Dosyasını Yükle
 CSV dosyasını dosya yolunu ve yapılandırılmış olanı geçirerek yüklüyoruz`TxtLoadOptions` için`Workbook` yapıcı:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Bu adım, CSV verilerinizi, her değerin tercih ettiğiniz kurallara göre ayrıştırıldığı, tam işlevli bir Excel çalışma kitabına dönüştürür.
## Adım 4: Hücre Verilerine Erişim ve Görüntüleme
CSV çalışma kitabına yüklendikten sonra verilerle çalışmaya başlayabilirsiniz. Örneğin, belirli hücrelerin türünü ve değerini yazdırmak isteyebilirsiniz.
### 4.1 A1 Hücresini Al ve Görüntüle
İlk hücreyi (A1) alalım ve değerini ve türünü görüntüleyelim:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Burada,`Type` özellik veri türünü gösterir (örneğin`String` veya`DateTime` ), Ve`DisplayStringValue` size biçimlendirilmiş değeri verir.
### 4.2 B1 Hücresini Al ve Görüntüle
Benzer şekilde, B1 gibi başka bir hücreyi alabilir ve görüntüleyebiliriz:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Bu işlem, incelemeniz gereken hücre sayısı kadar tekrarlanabilir.
## Adım 5: Çalışma Kitabını Kaydedin
 Verilerle çalıştıktan sonra çalışma kitabını yeni bir dosyaya kaydetmek isteyebilirsiniz. Aspose.Cells bunu basit bir şekilde kolaylaştırır`Save` yöntem:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Bu, çalışma kitabını Excel dosyası olarak kaydeder ve uyguladığınız tüm biçimlendirmeyi ve veri ayrıştırmayı korur.
## Çözüm
.NET için Aspose.Cells'de tercih edilen bir ayrıştırıcıyla CSV dosyalarını açmak, farklı veri türlerini işlemenin esnek ve güçlü bir yoludur. Özel ayrıştırıcılar oluşturarak ve yükleme seçeneklerini yapılandırarak, metin, tarih veya diğer özel biçimlerle uğraşıyor olun, CSV dosyalarınızın tam olarak ihtiyaç duyduğunuz şekilde ayrıştırılmasını sağlayabilirsiniz. Bu eğitimle, artık projelerinizde daha karmaşık veri ayrıştırma senaryolarını ele almaya hazırsınız.
## SSS
### Aspose.Cells for .NET'te özel ayrıştırıcıların amacı nedir?
Özel ayrıştırıcılar, CSV dosyası yüklenirken metin veya tarih gibi belirli veri türlerinin nasıl ayrıştırılacağını tanımlamanıza olanak tanır.
### CSV dosyasında farklı bir ayırıcı karakter kullanabilir miyim?
 Evet, ayırıcı olarak herhangi bir karakteri belirtebilirsiniz.`TxtLoadOptions.Separator` mülk.
### CSV yüklerken Aspose.Cells'de kodlamayı nasıl işlerim?
 Ayarlayabilirsiniz`Encoding` mülkiyeti`TxtLoadOptions` UTF-8, ASCII vb. gibi herhangi bir kodlama şemasına.
### CSV dosyasındaki tarih biçimi farklıysa ne olur?
Özel bir ayrıştırıcı kullanarak belirli tarih biçimini tanımlayabilir, böylece tarih değerlerinin doğru şekilde ayrıştırılmasını sağlayabilirsiniz.
### Çalışma kitabını başka formatlarda kaydedebilir miyim?
Evet, Aspose.Cells çalışma kitabını XLSX, CSV, PDF ve daha birçok formatta kaydetmenize olanak tanır.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
