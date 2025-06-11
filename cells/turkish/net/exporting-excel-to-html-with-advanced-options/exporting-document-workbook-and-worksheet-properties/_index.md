---
"description": "Aspose.Cells for .NET kullanarak Excel belgesi, çalışma kitabı ve çalışma sayfası özelliklerini HTML'ye nasıl aktaracağınızı öğrenin. Kolay adım adım kılavuz dahildir."
"linktitle": "Belge Çalışma Kitabı ve Çalışma Sayfası Özelliklerini HTML'ye Aktarma"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Belge Çalışma Kitabı ve Çalışma Sayfası Özelliklerini HTML'ye Aktarma"
"url": "/tr/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Belge Çalışma Kitabı ve Çalışma Sayfası Özelliklerini HTML'ye Aktarma

## giriiş

E-tabloları işlemeye gelince, paylaşım, koruma veya sunum için Excel dosyalarını farklı biçimlere dönüştürmemiz gerektiğini sık sık görürüz. Yaygın görevlerden biri, çalışma kitabı ve çalışma sayfası özelliklerini HTML biçimine aktarmaktır. Bu makalede, bunu .NET için Aspose.Cells kullanarak nasıl başaracağınızı göstereceğiz. Kodlama veya Aspose kitaplığı konusunda yeniyseniz endişelenmeyin; takip etmeyi kolaylaştırmak için adım adım açıklayacağız!

## Ön koşullar

Koda dalmadan önce, başlamak için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:

1. .NET Framework: Geliştirme ortamınızın .NET Framework ile kurulduğundan emin olun. Aspose.Cells, .NET Framework'ün 4.8'e kadar olan sürümleriyle uyumludur.
   
2. .NET için Aspose.Cells: Aspose.Cells'in yüklü olması gerekir. Kütüphaneyi şuradan indirebilirsiniz: [indirme sayfası](https://releases.aspose.com/cells/net/). 

3. IDE: Visual Studio gibi uygun bir Entegre Geliştirme Ortamı (IDE) kodlama deneyiminizi basitleştirecektir.

4. Örnek Excel Dosyası: Test amaçlı olarak, adında bir Excel dosyanız olduğundan emin olun. `sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` çalışma dizininizde.

## Paketleri İçe Aktar

Artık ön koşulları ele aldığımıza göre, C# projemize gerekli paketleri içe aktararak başlayalım. Bunu nasıl yapabileceğinizi anlatalım:

### Yeni Bir Proje Oluştur

- IDE'nizi açın ve yeni bir C# projesi oluşturun. Bu tür görevleri çalıştırmak için mükemmel olan bir konsol uygulaması seçebilirsiniz.

### Aspose.Cells NuGet Paketini ekleyin

Aspose.Cells paketini eklemek için şu adımları izleyin:

- Çözüm Gezgini'nde projenize sağ tıklayın ve "NuGet Paketlerini Yönet" seçeneğini seçin.
- NuGet Paket Yöneticisi'nde "Aspose.Cells" ifadesini arayın ve yükleyin.
- Bu paket Excel dosyalarıyla çalışmak için gerekli sınıfları ve yöntemleri sağlayacaktır.

### Ad Alanlarını İçe Aktarma

Ana program dosyanızın en üstüne aşağıdaki ad alanlarını eklediğinizden emin olun:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Bu bize şuna erişim sağlayacak: `Workbook` Ve `HtmlSaveOptions` Örneğimizde kullanacağımız sınıflar.

Artık her şey hazır olduğuna göre, süreci basit adımlara bölelim.

## Adım 1: Dosya Dizinlerinizi Ayarlayın

İlk olarak, girdi ve çıktı dosyalarımızın nerede bulunacağını belirtmemiz gerekiyor. Kodunuzda, dizinleri şu şekilde başlatın:

```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory/";  // Gerçek yolunuzla güncelleyin

// Çıktı dizini
string outputDir = "Your Document Directory/";  // Gerçek yolunuzla güncelleyin
```

- Kaynak Dizini: Giriş Excel dosyanızın (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) saklanır.
- Çıktı Dizini: Bu, çıktı HTML dosyasının kaydedilmesini istediğiniz yoldur.

## Adım 2: Excel Dosyanızı Yükleyin

Şimdi Excel dosyasını şunu kullanarak yüklememiz gerekiyor: `Workbook` sınıf:

```csharp
// Örnek Excel dosyasını yükleyin
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

- Çalışma Kitabı Örneği: `Workbook` constructor, Excel dosyanızın yolunu alır ve üzerinde değişiklik yapabileceğiniz yeni bir örnek oluşturur.

## Adım 3: HTML Kaydetme Seçeneklerini Ayarlayın

Daha sonra Excel verilerimizi HTML'e nasıl kaydetmek istediğimizi belirtiyoruz:

```csharp
// Html Kaydetme Seçeneklerini Belirleyin
HtmlSaveOptions options = new HtmlSaveOptions();

// Belge, çalışma kitabı ve çalışma sayfası özelliklerinin dışa aktarılmasını engelle
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: Bu sınıf, Excel dosyasının HTML'ye nasıl dönüştürüleceğini yönetmeye yardımcı olur.
- Birkaç seçeneği ayarladık `false` çünkü HTML çıktımıza çalışma kitabı ve çalışma sayfası özelliklerini dahil etmek istemiyoruz.

## Adım 4: Her Şeyi HTML'ye Aktar

Artık çalışma kitabımızı HTML formatına kaydetmeye hazırız:

```csharp
// Excel dosyasını Html Kaydetme Seçenekleri ile Html'ye aktarın
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

- The `Save` method iki parametre alır: çıktı HTML dosyası için dosya yolu ve kurduğumuz seçenekler. Bunu çalıştırmak HTML dosyanızı belirlenen çıktı dizininde oluşturacaktır.

## Adım 5: Konsol Geri Bildirimi

Son olarak, işlemin başarıyla tamamlandığını bildirmek için konsolda biraz geri bildirim sağlayalım:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## Çözüm

Ve işte böyle, Aspose.Cells for .NET kullanarak çalışma kitabı ve çalışma sayfası özelliklerini HTML'ye başarıyla aktardınız! Ortamınızı kurmaktan Excel verilerinizi aktarmaya kadar basit bir süreci takip ettiniz. Aspose.Cells gibi kütüphaneleri kullanmanın güzelliği, karmaşık görevleri kolaylaştırması ve geliştiricilerin hayatını kolaylaştırmasıdır. Artık, tıpkı tüm kitabı onlara vermeden çalışma kitaplarınıza göz atmasına izin verdiğiniz gibi, elektronik tablolarınızı HTML ile daha geniş bir şekilde paylaşabilirsiniz.

## SSS

### Aspose.Cells for .NET'i nasıl kurarım?  
NuGet Paket Yöneticisi aracılığıyla Visual Studio projenize Aspose.Cells kütüphanesini kurabilirsiniz.

### HTML çıktısını özelleştirebilir miyim?  
Evet, Aspose.Cells çeşitli seçenekler sunar `HtmlSaveOptions` Excel dosyanızın HTML'ye nasıl dönüştürüleceğini özelleştirmek için.

### HTML dışa aktarımına belge özelliklerini eklemenin bir yolu var mı?  
Ayarlayabilirsiniz `ExportDocumentProperties`, `ExportWorkbookProperties`, Ve `ExportWorksheetProperties` ile `true` içinde `HtmlSaveOptions` eğer bunları dahil etmek isterseniz.

### Excel dosyamı HTML dışında hangi formatlara aktarabilirim?  
Aspose.Cells, PDF, CSV, XML ve diğerleri dahil olmak üzere çeşitli formatları destekler.

### Deneme sürümü mevcut mu?  
Evet, Aspose.Cells'in ücretsiz deneme sürümünü şu adresten edinebilirsiniz: [web sitesi](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}