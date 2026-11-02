---
category: general
date: 2026-06-05
description: C# kullanarak PowerPoint’ten grafiklerin nasıl dışa aktarılacağı. OLE
  nesnelerinin dışa aktarımını ve ortaya çıkan PPTX’te grafiklerin düzenlenebilir
  olmasını içerir – adım adım.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: tr
og_description: C# kullanarak PowerPoint’ten grafiklerin nasıl dışa aktarılacağını
  öğrenin. OLE nesnelerini dışa aktarmayı ve kaydedilen PPTX’te grafikleri düzenlenebilir
  hâle getirmeyi adım adım keşfedin.
og_title: Grafikleri Dışa Aktarma – Tam PowerPoint C# Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Grafikleri Dışa Aktarma – Tam PowerPoint C# Rehberi
url: /tr/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint C# ile Grafik Dışa Aktarma – Tam Rehber

PowerPoint sunumundan **grafikleri dışa aktarmanın** ardından daha sonra düzenleme yeteneğini kaybetmeden nasıl yapabileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama sürecinde grafik verileri PPTX içinde bulunur ve dosyayı birine gönderdiğinizde alıcı genellikle bir değeri değiştirmek ya da bir etiketi güncellemek zorunda kalır. İyi haber şu ki, birkaç satır C# kodu ile düzenlenebilirliği koruyabilir ve aynı anda gömülü OLE nesnelerini de dışa aktarabilirsiniz.

Bu öğreticide, **grafikleri nasıl dışa aktaracağınızı**, **OLE nesnelerini nasıl dışa aktaracağınızı** ve **grafikleri çıktı dosyasında düzenlenebilir hale getireceğinizi** gösteren, çalıştırmaya hazır bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, Aspose.Slides kütüphanesini kullanan herhangi bir .NET projesine ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

> **İpucu:** Aspose.Slides’a yeniyseniz, projenize `Aspose.Slides.NET` NuGet paketini eklediğinizden emin olun—aksi takdirde kod derlenmez.

## Gereksinimler

| Gereksinim | Neden Önemli |
|------------|--------------|
| .NET 6+ (veya .NET Framework 4.7+) | Modern çalışma zamanları daha iyi performans ve daha kolay paket yönetimi sağlar. |
| Aspose.Slides for .NET (en son sürüm) | Kullanacağımız `Presentation` ve `PptxSaveOptions` sınıflarını bu kütüphane sağlar. |
| En az bir grafik içeren örnek PowerPoint dosyası | Demo, bir grafik içeren herhangi bir `.pptx` dosyasında çalışır; dışa aktarma sonrası düzenlenebilirliği göreceksiniz. |
| Bir IDE (Visual Studio, Rider veya VS Code) | Hızlı hata ayıklama ve oluşturulan dosyayı görme açısından kullanışlıdır. |

Ek bir üçüncü‑taraf aracı gerekmez—her şey Aspose API’si tarafından yönetilir.

## Adım 1 – Kaynak Sunumu Yükleme

İlk olarak orijinal PPTX’i belleğe almamız gerekiyor. Bunu, Word’de bir belgeyi düzenlemeye başlamadan önce açmak gibi düşünün.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Neden önemli:** `Presentation` nesnesi, sonraki tüm işlemler için giriş noktasıdır. Dosyayı ayrıştırır, slaytlar, şekiller, grafikler ve OLE nesnelerinin bir nesne modelini oluşturur ve her şeyi değiştirilebilir bir durumda tutar.

## Adım 2 – Kaydetme Seçeneklerini Oluşturma ve Düzenlenebilir Grafikleri Etkinleştirme

Varsayılan olarak, `Save` metodunu çağırdığınızda kütüphane grafikleri statik görüntülere dönüştürür. Düzenlenebilir kalmalarını sağlamak için `ExportEditableCharts` bayrağını açmanız gerekir.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Nasıl çalışır:** `ExportEditableCharts` **true** olduğunda, kütüphane grafiğin XML tanımını (`chart.xml`) PPTX’e rasterleştirmek yerine yazar. PowerPoint bu XML’i okuyarak kullanıcıya grafik düzenleyicisini açma imkanı verir.

## Adım 3 – Gömülü OLE Nesnelerinin Dışa Aktarımını Açma

Birçok sunum, Excel sayfaları, Visio diyagramları veya hatta PDF dosyalarını OLE nesneleri olarak gömer. Bu nesnelerin dönüşüm sırasında korunmasını istiyorsanız `ExportOLEObjects` özelliğini etkinleştirin.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **“OLE nesnelerini dışa aktarmak” ne demek:** OLE paketi, PPTX içinde ikili bir veri bloğu olarak saklanır. Bu bayrağı ayarlamak, orijinal ikili veriyi korur ve alıcının nesneye çift‑tıklayarak yerel uygulamasında (ör. Excel) açmasını sağlar. Bu ayar olmadan OLE nesnesi çıkarılır, bağlantılar kırılır ve veri kaybolur.

## Adım 4 – Yapılandırılmış Seçeneklerle Sunumu Kaydetme

Seçenekleri hazırladığımıza göre, Aspose’a dosyayı yazmasını söylemek yeterli.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Sonuç:** `editable.pptx`, `input.pptx` ile aynı slaytlara sahiptir, ancak herhangi bir grafik PowerPoint içinde doğrudan düzenlenebilir ve gömülü OLE nesneleri bozulmadan kalır.

### Tam Çalışan Örnek

Aşağıda, derleyip çalıştırabileceğiniz eksiksiz, bağımsız bir program yer alıyor. `using` ifadeleri, doğru kaynak yönetimi ve her satırı açıklayan yorumlar içerir.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Beklenen çıktı:** Programı çalıştırdıktan sonra `editable.pptx` dosyasını PowerPoint’te açın. Herhangi bir grafiğe sağ‑tıklayın → *Edit Data* → grafik düzenleyicisi açılır, bu da **grafikleri düzenlenebilir hâle getirme** işleminin başarılı olduğunu gösterir. Gömülü bir Excel sayfasına çift‑tıklayın, Excel’de açılır ve **OLE nesnelerini dışa aktarma** işleminin çalıştığını kanıtlar.

![grafikleri dışa aktarma diyagramı](https://example.com/images/export-charts.png "grafikleri dışa aktarma – PowerPoint dışa aktarma sonrası")

*(Alt metin: grafikleri dışa aktarma – düzenlenebilir grafik ve OLE nesnesi içeren PowerPoint ekran görüntüsü)*

## Yaygın Sorular & Kenar Durumlar

### Kaynak dosyada hiç grafik yoksa ne olur?

Kod hâlâ çalışır; `ExportEditableCharts` etkisiz kalır çünkü dönüştürülecek bir şey yoktur. Hata oluşmaz.

### Sadece belirli grafikleri dışa aktarmak mümkün mü?

Evet. Global `ExportEditableCharts` bayrağı yerine, `presentation.Slides` üzerinden döngü yapıp, kaydetmeden önce istediğiniz grafik nesnelerinde `Chart.IsEditable = true` ayarlayabilirsiniz. Bu, daha ince ayar kontrolü sağlar.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### OLE dışa aktarımını etkinleştirmek dosya boyutunu artırır mı?

Biraz. İkili OLE akışları olduğu gibi saklandığından, ortaya çıkan PPTX birkaç kilobayt daha büyük olabilir. Çoğu iş senaryosunda tam düzenlenebilirlik sağlanması bu küçük boyut artışına değerdir.

### Oluşturulan dosyayı hangi PowerPoint sürümleri açabilir?

OOXML standardını destekleyen herhangi bir sürüm (PowerPoint 2007 ve sonrası). Düzenlenebilir grafik özelliği, Office 2007’de tanıtılan yerel grafik düzenleyicisine dayanır; bu yüzden eski `.ppt` dosyaları bu avantajı elde etmez.

## Üretim‑Hazır Kod İçin İpuçları

| İpucu | Sebep |
|-------|-------|
| `using` bloklarını (gösterildiği gibi) kullanarak `Presentation` nesnelerini serbest bırakın. | Özellikle toplu dosya işleme sırasında bellek sızıntılarını önler. |
| Dosya yollarını yüklemeden önce doğrulayın. | Arka plan hizmetinin çökmesine neden olabilecek `FileNotFoundException` hatalarını engeller. |
| `ExportEditableCharts` ve `ExportOLEObjects` ayarlarını loglayın. | Kullanıcıların düzenlenemez grafik şikayetlerinde sorun giderme kolaylaşır. |
| `Aspose.Slides.Exception` hatasını ayrı ayrı yakalayın. | Kütüphaneden (ör. desteklenmeyen grafik tipleri) daha net hata mesajları almanızı sağlar. |
| Dosya boyutu önemliyse `PptxCompressionLevel`’ı değerlendirin. | Düzenlenebilirliği korurken çıktıyı sıkıştırabilirsiniz. |

## Özet – Ne Başardık?

Başlangıçta net bir soruya yanıt aradık: **PowerPoint dosyasından grafikleri dışa aktarmak** ve aynı zamanda düzenlenebilir kalmalarını ve gömülü OLE nesnelerinin korunmasını sağlamak. Sunumu yükleyip, `PptxSaveOptions` (`ExportEditableCharts = true` ve `ExportOLEObjects = true`) ayarlarını yapılandırıp, dosyayı kaydederek bu iki gereksinimi de karşılayan bir PPTX elde ettik. Aynı desen, toplu dönüşümler, CI pipeline’ları veya otomatik raporlama araçları için yeniden kullanılabilir.

## Sonraki Keşifleriniz Ne Olmalı?

- **Grafikleri resim olarak dışa aktarma** (statik raporlar için `saveOptions.ExportEditableCharts = false`).  
- **Vektör grafikleri koruyarak PPTX’i PDF’ye dönüştürme** (`PdfSaveOptions`).  
- **Grafik verilerini programatik olarak değiştirme** (ör. dışa aktarmadan önce seri değerlerini güncelleme).  
- **Azure Functions ile entegrasyon** yaparak talep üzerine grafik dışa aktarma API’si sağlama.

Denemeler yapın ve karşılaştığınız kenar durumlarını bizimle paylaşın. İyi kodlamalar, ve grafiğiniz her zaman düzenlenebilir olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakın konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Apply Themes to Excel Charts Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}