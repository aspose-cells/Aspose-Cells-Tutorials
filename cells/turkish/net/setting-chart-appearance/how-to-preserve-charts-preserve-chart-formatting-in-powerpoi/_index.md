---
category: general
date: 2026-07-03
description: Aspose.Slides kullanarak C#'ta grafik biçimlendirmesini korurken grafikleri
  nasıl koruyacağınızı öğrenin. Bu adım adım kılavuzu izleyin.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: tr
og_description: Aspose.Slides ile C#’ta grafikleri ve grafik biçimlendirmesini koruma
  nasıl yapılır? Kodlu tam rehber.
og_title: grafikleri koruma – PowerPoint’te grafik biçimlendirmesini koruma (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Grafikleri koruma – PowerPoint C#'ta grafik biçimlendirmesini koruma
url: /tr/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# grafiklerin nasıl korunacağı – PowerPoint C#'ta grafik biçimlendirmesini koruma

Programlı olarak bir PowerPoint dosyasını dışa aktarmanız veya değiştirmeniz gerektiğinde **grafiklerin nasıl korunacağını** hiç merak ettiniz mi? Belki hızlı bir kaydetme denediniz ve grafik statik bir görüntüye dönüştü, beklediğiniz düzenlenebilirliği bozdu.  

Bu öğreticide **grafiklerin nasıl korunacağını** **ve** **grafik biçimlendirmesini koruma**'yı Aspose.Slides for .NET kullanarak nasıl koruyacağınızı göstereceğiz. Sonunda, her grafiğin düzenlenebilir bir OOXML nesnesi olarak kaldığı bir PPTX üreten, çalıştırmaya hazır bir C# kod parçasına sahip olacaksınız—artık düzleştirilmiş resimler yok.

## Öğrenecekleriniz

- Sunumu yükleme, dışa aktarma seçeneklerini yapılandırma ve **grafik biçimlendirmesini koruma** sırasında kaydetme adımlarını tam olarak öğrenin.  
- `ExportEditableObjects` bayrağının neden önemli olduğunu ve grafiklerin rasterleştirilmesini nasıl engellediğini öğrenin.  
- Yaygın tuzaklar (ör. eski PPT formatları, eksik yazı tipleri) ve hızlı çözümler.  

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok; sadece temel bir C# ortamı ve grafik dostu tutmak istediğiniz bir PowerPoint dosyası yeterli.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).  
- Aspose.Slides for .NET NuGet paketi (`Install-Package Aspose.Slides.NET`).  
- En az bir grafik içeren örnek bir `input.pptx` dosyası.  
- Visual Studio, Rider veya tercih ettiğiniz herhangi bir editör.

---

## Adım 1: Aspose.Slides'ı kurun ve yeni bir konsol projesi oluşturun

Başlamak için yeni bir konsol uygulaması oluşturun ve kütüphaneyi ekleyin:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro ipucu:** Kurumsal bir proxy'nin arkasındaysanız, `--no-restore` bayrağını ekleyin ve daha sonra proxy ayarlarınızla geri yükleyin.

## Adım 2: Kaynak sunumu yükleyin – **grafiklerin nasıl korunacağını** uygulamanın ilk yeri

`Presentation` sınıfını kullanarak PPTX dosyanızı açın. **Grafiklerin nasıl korunacağını** öğrenme yolculuğunun gerçekten başladığı yer burası.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Henüz herhangi bir grafik nesnesine dokunmadığımızı fark edin—bu kasıtlıdır. Dosyayı olduğu gibi yüklemek, orijinal XML yapısını korumamızı sağlar ve bu da daha sonra **grafik biçimlendirmesini koruma** için kritiktir.

## Adım 3: Dışa aktarma seçeneklerini yapılandırın – **grafiklerin nasıl korunacağını** kalbi

Aspose.Slides bir `PresentationExportOptions` sınıfı sunar. `ExportEditableObjects` özelliğini `true` olarak ayarlamak, motorun grafikleri, tabloları ve SmartArt'ı düzleştirmek yerine yerel OOXML parçaları olarak tutmasını sağlar.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Bu neden çalışıyor? `ExportEditableObjects` `false` (varsayılan) olduğunda, kütüphane uyumluluk için karmaşık nesneleri rasterleştirir, bu da **grafik biçimlendirmesini koruma**'yı yok eder. Özelliği açmak, orijinal grafik XML'ini korur ve son kullanıcıların PPTX'i açıp hâlâ grafik verilerini düzenlemesine izin verir.

## Adım 4: Yapılandırılmış seçenekleri kullanarak sunumu kaydedin

Şimdi çıktı dosyasını yazıyoruz. `SaveFormat` ve `exportOptions` parametrelerini kabul eden aynı `Save` aşırı yüklemesi, grafiğin düzenlenebilir kalmasını garanti eder.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Bu programı çalıştırdığınızda `EditableCharts.pptx` oluşur. PowerPoint'te açın, bir grafiğe sağ‑tıklayın ve alışılmış “Verileri Düzenle” seçeneğini göreceksiniz—bu da **grafiklerin nasıl korunacağını** ve **grafik biçimlendirmesini koruma**'yı başarıyla başardığımızın kanıtıdır.

## Adım 5: Sonucu doğrulayın ve yaygın sorunları giderin

### Doğrulama

1. `EditableCharts.pptx` dosyasını PowerPoint'te açın.  
2. Herhangi bir grafiğe tıklayın → “Verileri Düzenle”.  
3. Excel benzeri veri sayfası görünmeli ve seri değerlerini değiştirmenize izin vermelidir.

Eğer sadece statik bir görüntü görüyorsanız, şunları iki kez kontrol edin:

- Aspose.Slides'ın son sürümünü kullanıyorsunuz (eski sürümlerde `ExportEditableObjects` ile ilgili hatalar vardı).  
- Kaynak PPTX gerçekten grafik nesneleri içeriyor (grafik resimleri değil).  
- Özel bir tema veya yazı tipi ikamesi grafiğin görüntü olarak render edilmesine neden olmamalı.

### Kenar Durumları

- **Eski PPT (ikili) dosyalar:** Dışa aktarma seçeneklerini uygulamadan önce önce PPTX'e dönüştürün (`pres.Save("temp.pptx", SaveFormat.Pptx)`).  
- **Büyük sunumlar:** Bellek kullanımı artabilir; büyük dosyalar için `Presentation` sınıfının `Dispose` desenini veya akış API'lerini düşünün.  
- **Gömülü yazı tipleri:** Hedef ortam orijinal yazı tiplerine sahip değilse, PowerPoint geri dönüş yaparak grafiği görüntü olarak render edebilir. Yazı tiplerini kaynak dosyaya gömün veya uygulamanızla birlikte dağıtın.

## Sıkça Sorulan Sorular (SSS)

**S: Bu, PowerPoint 2003 (PPT) dosyalarıyla çalışır mı?**  
C: Doğrudan hayır—`ExportEditableObjects` yalnızca PPTX formatına uygulanır. Önce dönüştürün, ardından dışa aktarın.

**S: SmartArt gibi diğer nesneleri de koruyabilir miyim?**  
C: Kesinlikle. Aynı `ExportEditableObjects` bayrağı SmartArt, tablolar ve diyagramları düzenlenebilir tutar.

**S: Orijinal slayt boyutunu korumam gerekirse ne olur?**  
C: Slayt boyutu sunum meta verilerinde saklanır ve bu seçeneklerden etkilenmez. Ek bir koda gerek yok.

## Sonraki Adımlar – İlerlemeyi Sürdürün

Artık **grafiklerin nasıl korunacağını** kavradığınıza göre, şunları keşfetmeye çalışın:

- Belirli grafik türleri için **grafik biçimlendirmesini koruma** (ör. yığılmış çubuk vs. radar).  
- Kaydetmeden önce verileri programlı olarak değiştirmek için `Chart` API'sini kullanma.  
- Diğer formatlara (PDF, HTML) dışa aktarırken kaynak PPTX'teki grafiklerin düzenlenebilir kalmasını sağlama.  

Bunların her biri aynı ilkeye dayanır: temel OOXML'i bozulmadan tutmak.

## Sonuç

Aspose.Slides for .NET kullanarak bir PowerPoint dosyasında **grafiklerin nasıl korunacağını** adım adım inceledik ve bu grafiklerin tamamen düzenlenebilir kalması için gereken tam **grafik biçimlendirmesini koruma** adımlarını gösterdik. Yukarıdaki tam kod parçacığı herhangi bir C# projesine eklenmeye hazır ve açıklamalar her satırın *neden*ini kapsar—sadece kopyala‑yapıştırmak yerine anlayacaksınız.

Deneyin, dışa aktarma seçeneklerini ayarlayın ve yakında grafik verilerini ince ayar yapma yeteneğini kaybetmeden sunum güncellemelerini otomatikleştireceksiniz. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Excel Grafiklerini PDF'ye Dışa Aktarma: Adım Adım Kılavuz](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells for .NET Kullanarak Excel Grafiklerini SVG'ye Dönüştürme (Adım Adım Kılavuz)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel'de Grafik Oluşturma: Geliştirici Kılavuzu](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}