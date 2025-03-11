---
title: .NET'te Çıktı HTML'de HTML CrossType'ı Programatik Olarak Belirleme
linktitle: .NET'te Çıktı HTML'de HTML CrossType'ı Programatik Olarak Belirleme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET'te HTML CrossType'ı nasıl belirleyeceğinizi öğrenin. Excel dosyalarını hassas bir şekilde HTML'ye dönüştürmek için adım adım öğreticimizi izleyin.
weight: 17
url: /tr/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Çıktı HTML'de HTML CrossType'ı Programatik Olarak Belirleme

## giriiş
.NET uygulamalarında Excel dosyalarını HTML'ye dönüştürmeye gelince, çıktıda çapraz referansların nasıl işleneceğini belirtmeniz gerekebilir. .NET için Aspose.Cells'deki HtmlSaveOptions sınıfı, dönüştürme sürecini kontrol etmek için çeşitli ayarlar sağlar ve bu seçeneklerden biri HtmlCrossType'tır. Bu eğitimde, Excel dosyalarını HTML biçimine aktarırken HTML çapraz türünü programlı olarak nasıl belirteceğimizi ele alacağız. 
## Ön koşullar
Koda dalmadan önce aşağıdakilerin mevcut olduğundan emin olun:
-  Aspose.Cells for .NET: Projenizde Aspose.Cells kütüphanesinin yüklü olduğundan emin olun. Bunu şuradan indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/cells/net/).
- Visual Studio: Visual Studio'nun veya herhangi bir .NET geliştirme ortamının çalışan bir kurulumu.
- Temel C# Bilgisi: C# programlamaya aşina olmak örnekleri daha iyi anlamanıza yardımcı olacaktır.
-  Örnek Excel Dosyası: Çalışmak için hazır bir örnek Excel dosyanız olsun. Bu örnek için şunu kullanacağız:`sampleHtmlCrossStringType.xlsx`.
## Paketleri İçe Aktar
Başlamak için gerekli Aspose.Cells ad alanlarını içe aktarmanız gerekir. Bunu şu şekilde yapabilirsiniz:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Bunu adım adım açıklayalım, böylece sizin için takip etmesi ve bu işlevselliği kendi projelerinize uygulaması kolay olsun.
## Adım 1: Kaynak ve Çıktı Dizinlerinizi Tanımlayın
Öncelikle kaynak Excel dosyanızın dizinlerini ve çıktı HTML dosyasını nereye kaydetmek istediğinizi ayarlamanız gerekir.
```csharp
// Kaynak dizini
string sourceDir = "Your Document Directory";
// Çıktı dizini
string outputDir = "Your Document Directory";
```
## Adım 2: Örnek Excel Dosyasını Yükleyin
 Ardından, örnek Excel dosyanızı bir`Workbook` nesne. İşte tüm sihir burada başlıyor.
```csharp
// Örnek Excel dosyasını yükleyin
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Burada, değiştirin`"Your Document Directory"` Excel dosyanızın bulunduğu gerçek yol ile. Bu satır Excel dosyasını belleğe okur, böylece onu düzenleyebilirsiniz.
## Adım 3: HTML Kaydetme Seçeneklerini Belirleyin
 Şimdi, bir örnek oluşturacağız`HtmlSaveOptions`Excel dosyasının HTML'ye nasıl dönüştürüleceğini yapılandırmanıza olanak tanır.
```csharp
// HTML Çapraz Tipini Belirleyin
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 Bu adımda, şunu ayarladık:`HtmlCrossStringType` ile`HtmlCrossType.Default`Çıkış HTML'inde çapraz referansları işlemek için kullanılabilen seçeneklerden biri olan .
## Adım 4: Gerektiğinde Çapraz Tipini Değiştirin
 Farklı türler belirleyebilirsiniz`HtmlCrossStringType` gereksinimlerinize göre. Kullanabileceğiniz çeşitli seçenekler şunlardır:
- `HtmlCrossType.Default`: Varsayılan çapraz tip.
- `HtmlCrossType.MSExport`: HTML'yi MS Excel benzeri davranışla dışa aktarır.
- `HtmlCrossType.Cross`: Çapraz referanslar oluşturur.
- `HtmlCrossType.FitToCell`: Çapraz referansları hücre boyutlarına uydurur.
 Şunu değiştirebilirsiniz:`HtmlCrossStringType` bunun gibi:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// veya
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// veya
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Adım 5: Çıktı HTML Dosyasını Kaydedin
 Seçeneklerinizi yapılandırdıktan sonra, dönüştürülen HTML dosyasını kaydetme zamanı geldi.`Save` yönteminiz`Workbook` nesne:
```csharp
// Çıktı Html
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Burada, çıktı dosyasını şu şekilde adlandırıyoruz:`HtmlCrossStringType` ayarladık. Bu şekilde, dönüşümde hangi çapraz türün kullanıldığını kolayca belirleyebilirsiniz.
## Adım 6: Başarılı Yürütmeyi Onaylayın
Son olarak, işleminizin başarılı olduğunu onaylamak her zaman iyi bir uygulamadır. Konsola bir mesaj yazdırabilirsiniz:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Bu, işlemin herhangi bir hata olmadan tamamlandığını bildirecektir.
## Çözüm
İşte oldu! Aspose.Cells kullanarak .NET'te Excel dışa aktarmanız için HTML çapraz türünü başarıyla belirttiniz. Bu işlevsellik, HTML çıktınızda belirli biçimlendirme veya referansları korumanız gerektiğinde özellikle yararlıdır ve dönüştürülen belgelerinizin gereksinimlerinizi karşılamasını sağlar.
## SSS
### Aspose.Cells'de HtmlCrossType nedir?  
HtmlCrossType, HTML dönüştürme sırasında Excel dosyasındaki çapraz referansların nasıl işleneceğini tanımlar. Default, MSExport, Cross ve FitToCell gibi seçenekleri seçebilirsiniz.
### Aspose.Cells'i ücretsiz kullanabilir miyim?  
 Aspose.Cells ücretsiz deneme sürümü sunuyor. Bunu şu adresten indirebilirsiniz:[web sitesi](https://releases.aspose.com/).
### Aspose.Cells'i .NET projeme nasıl yüklerim?  
 Visual Studio'da NuGet Paket Yöneticisi aracılığıyla Aspose.Cells'i şu komutu çalıştırarak yükleyebilirsiniz:`Install-Package Aspose.Cells`.
### Aspose.Cells'in dokümanlarını nerede bulabilirim?  
 Aspose.Cells'te kapsamlı belgeler bulabilirsiniz[Burada](https://reference.aspose.com/cells/net/).
### HTML dosyasını kaydederken bir hatayla karşılaşırsam ne yapmalıyım?  
Dizin yollarının doğru olduğundan ve çıktı dizini için yazma izinlerinizin olduğundan emin olun. Sorun devam ederse, yardım için Aspose destek forumunu kontrol edin.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
