---
title: PDF Kaydetme Seçenekleri için Varsayılan Yazı Tipini Ayarla
linktitle: PDF Kaydetme Seçenekleri için Varsayılan Yazı Tipini Ayarla
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET kullanarak PDF kaydetme seçenekleri için varsayılan yazı tiplerini nasıl ayarlayacağınızı öğrenin; böylece belgelerinizin her zaman mükemmel görünmesini sağlayın.
weight: 11
url: /tr/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Kaydetme Seçenekleri için Varsayılan Yazı Tipini Ayarla

## giriiş
Raporları, faturaları veya diğer belgeleri PDF formatında oluştururken, içeriğinizin tam olarak doğru görünmesini sağlamak çok önemlidir. Yazı tipleri, belgelerinizin görsel çekiciliğini ve okunabilirliğini korumada hayati bir rol oynar. Ancak, Excel dosyanızda kullandığınız yazı tipi PDF'nizi oluşturduğunuz sistemde mevcut olmadığında ne olur? İşte tam bu noktada Aspose.Cells for .NET işe yarar. Bu güçlü kitaplık, PDF kaydetme seçenekleriniz için varsayılan yazı tiplerini ayarlamanıza olanak tanır ve belgelerinizin nerede açılırsa açılsın profesyonel ve tutarlı görünmesini sağlar.
## Ön koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1. Visual Studio: Kodunuzu yazmak ve çalıştırmak için Visual Studio gibi bir geliştirme ortamına ihtiyacınız olacak.
2.  Aspose.Cells for .NET: En son sürümü şu adresten indirebilirsiniz:[bu bağlantı](https://releases.aspose.com/cells/net/)Alternatif olarak, Visual Studio'daki NuGet Paket Yöneticisi aracılığıyla da yükleyebilirsiniz.
3. Temel C# Bilgisi: C# temellerini anlamak, kod örneklerini takip etmenize yardımcı olacaktır.
4. Örnek Excel Dosyası: Test için hazır bir örnek Excel dosyası bulundurun. Aspose.Cells'in eksik fontları nasıl işlediğini görmek için çeşitli fontlar ve stillerle bir tane oluşturabilirsiniz.
## Paketleri İçe Aktar
Projenizde Aspose.Cells'i kullanabilmeniz için gerekli paketleri içe aktarmanız gerekir. İşte bunu nasıl yapacağınız:
1. Projenizi Açın: Visual Studio'yu başlatın ve mevcut projenizi açın veya yeni bir proje oluşturun.
2. Referans Ekleme: Çözüm Gezgini'nde projenize sağ tıklayın ve "NuGet Paketlerini Yönet" seçeneğini seçin.
3. Aspose.Cells'i yükleyin: "Aspose.Cells"i arayın ve "Yükle" butonuna tıklayın.
4. Yönergeleri Kullanarak Ekleyin: C# dosyanızın en üstüne aşağıdaki ad alanlarını ekleyin:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Adım 1: Dizinlerinizi Ayarlayın
Dosyalarla çalışmaya başlamadan önce kaynak ve çıktı dizinlerini tanımlamak önemlidir. Bu, giriş Excel dosyanızı bulmanızı ve oluşturulan çıktı dosyalarını kaydetmenizi kolaylaştıracaktır.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// Çıktı dizini
string outputDir = "Your Document Directory";
```
 Yer değiştirmek`"Your Document Directory"` dizinlerinize giden gerçek yol ile.
## Adım 2: Excel Dosyasını Açın
 Artık dizinlerimizi ayarladığımıza göre, çalışmak istediğiniz Excel dosyasını açalım.`Workbook` Aspose.Cells'deki sınıf Excel belgesini yüklemek için kullanılır.
```csharp
// Bir Excel dosyası açın
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Dosya adını gerçek dosya adınızla değiştirdiğinizden emin olun.
## Adım 3: Görüntü İşleme Seçeneklerini Ayarlayın
Sonra, Excel sayfamızı bir resim biçimine dönüştürmek için işleme seçeneklerini yapılandırmamız gerekiyor. Bir örnek oluşturacağız`ImageOrPrintOptions`, resim türünü ve varsayılan yazı tipini belirterek.
```csharp
// PNG dosya biçimine dönüştürme
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 Bu kod parçacığında, şunu ayarlıyoruz:`CheckWorkbookDefaultFont` mülk`false`Bu, herhangi bir yazı tipinin eksik olması durumunda belirtilen varsayılan yazı tipinin (“Times New Roman”) kullanılacağı anlamına gelir.
## Adım 4: Sayfayı Bir Görüntü Olarak İşleyin
 Şimdi, çalışma kitabının ilk sayfasını PNG resmi olarak işleyelim.`SheetRender` Bunu başarmak için sınıf.
```csharp
// İlk çalışma sayfasını bir görüntüye dönüştürün
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Adım 5: Görüntü Türünü Değiştirin ve TIFF'e Dönüştürün
 Aynı sayfayı TIFF gibi farklı bir görüntü biçimine dönüştürmek istiyorsanız, basitçe`ImageType` özelliği ve işleme sürecini tekrarlayın.
```csharp
// TIFF formatına ayarlayın
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Adım 6: PDF Kaydetme Seçeneklerini Yapılandırın
 Şimdi, PDF kaydetme seçeneklerini ayarlayalım. Bir örnek oluşturacağız`PdfSaveOptions`varsayılan yazı tipini ayarlayalım ve eksik yazı tiplerini kontrol etmek istediğimizi belirtelim.
```csharp
// PDF kaydetme seçeneklerini yapılandırın
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Adım 7: Çalışma Kitabını PDF olarak kaydedin
Kaydetme seçeneklerini yapılandırdıktan sonra Excel çalışma kitabımızı PDF dosyası olarak kaydetmenin zamanı geldi. 
```csharp
// Çalışma kitabını PDF'ye kaydet
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Adım 8: Uygulamayı Onaylayın
Son olarak, kullanıcıya işlemin başarıyla tamamlandığını bildirmek iyi bir uygulamadır. Bunu basit bir konsol mesajı kullanarak başarabilirsiniz.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Çözüm
Aspose.Cells, Excel dosya düzenlemelerini yönetmek için esnek ve sağlam bir yol sunarak geliştiricilerin biçimlendirmelerini koruyan görsel olarak çekici belgeler oluşturmasını kolaylaştırır. İster raporlar, ister finansal belgeler veya başka bir veri sunumu biçimi üzerinde çalışıyor olun, yazı tipi oluşturma üzerinde kontrol sahibi olmak çıktı kalitenizi önemli ölçüde artırabilir.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, geliştiricilerin Microsoft Excel'in yüklenmesine gerek kalmadan Excel dosyalarını düzenlemelerine olanak tanıyan güçlü bir .NET kütüphanesidir. Çeşitli dosya biçimlerini destekler ve elektronik tablolarla çalışmak için zengin özellikler sunar.
### Excel dosyalarım için varsayılan yazı tipini nasıl ayarlayabilirim?
 Varsayılan bir yazı tipi ayarlamak için şunu kullanabilirsiniz:`PdfSaveOptions` sınıfını seçin ve istediğiniz yazı tipi adını belirtin. Bu, bir yazı tipi eksik olsa bile belgenizin belirttiğiniz varsayılan yazı tipini kullanmasını sağlar.
### Excel dosyalarını PDF dışındaki formatlara dönüştürebilir miyim?
Kesinlikle! Aspose.Cells, Excel dosyalarını resim (PNG, TIFF), HTML, CSV ve daha fazlası dahil olmak üzere çeşitli formatlara dönüştürmenize olanak tanır.
### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ticari bir üründür, ancak sınırlı deneme sürümüyle ücretsiz deneyebilirsiniz. Tam işlevsellik için bir lisans satın almanız gerekir.
### Aspose.Cells için desteği nerede bulabilirim?
 Aspose.Cells için destek almak için şu adresi ziyaret edebilirsiniz:[Aspose forumu](https://forum.aspose.com/c/cells/9)Diğer kullanıcılar ve geliştiricilerle soru sorabileceğiniz ve fikirlerinizi paylaşabileceğiniz bir yer.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
