---
category: general
date: 2026-10-01
description: Aspose.Cells kullanarak Excel'i HTML'ye dönüştürürken HTML'ye yazı tiplerini
  nasıl gömeceğinizi öğrenin. Birkaç adımda gömülü yazı tipleriyle Excel'i HTML olarak
  dışa aktarın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: tr
lastmod: 2026-10-01
og_description: Excel dosyalarını dışa aktarırken HTML'ye yazı tiplerini nasıl gömeceğinizi
  öğrenin. Yazı tipleri gömülü olarak Excel'i HTML'ye dönüştürmek için bu adım adım
  rehberi izleyin.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Excel'den HTML'ye Yazı Tipi Gömme – Aspose.Cells Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Aspose.Cells ile Excel'i HTML'ye dönüştürürken yazı tiplerini nasıl gömebilirsiniz?
url: /tr/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'i HTML'ye Dönüştürürken Fontları Nasıl Gömme

Excel çalışma kitabını HTML'ye dönüştürürken fontları gömmek, tarayıcılar arasında orijinal görünümün korunması için çok önemlidir. Özel fontları koruyarak Excel'i HTML'ye dönüştürmeniz gerekiyorsa, bu rehber tam süreci gösterir. Ayrıca Excel'i HTML olarak dışa aktarmayı ve HTML'de font gömme işleminin tutarlı render alımı için neden önemli olduğunu göreceksiniz.

Bu öğreticide ihtiyacınız olan her şey ele alınmaktadır: gerekli kütüphaneler, kod yapılandırması ve oluşturulan HTML dosyasının doğrulanması. Sonunda, sadece birkaç satır C# kodu ile gömülü fontlarla Excel'i HTML olarak dışa aktarabileceksiniz.

## Gerekenler

Başlamadan önce şunların olduğundan emin olun:

* **.NET 6.0 veya üzeri** – kod .NET 6 hedefli, ancak Aspose.Cells'i destekleyen herhangi bir .NET sürümü çalışır.
* **Aspose.Cells for .NET** – bir lisans edinin veya Aspose web sitesinden ücretsiz deneme sürümünü kullanın.
* **C# geliştirme ortamı** (Visual Studio, Rider veya VS Code) – .NET projelerini derleyebilen herhangi bir IDE.
* Özel fontları içeren bir Excel çalışma kitabı (`Styled.xlsx`) – korumak istediğiniz fontları içermeli.

## Adım 1: .NET projenizde Aspose.Cells'i kurun

İlk olarak, Aspose.Cells NuGet paketini projenize ekleyin:

```bash
dotnet add package Aspose.Cells
```

Ardından C# dosyanızın en üstüne namespace'i ekleyin:

```csharp
using Aspose.Cells;
```

Paketi eklemek, `Workbook`, `HtmlSaveOptions` ve ilgili sınıfları kullanılabilir hâle getirir.

## Adım 2: Excel çalışma kitabını yükleyin

Çalışma kitabını yüklemek, **Excel verilerini dışa aktarma** sürecinin ilk somut adımıdır. `Workbook` yapıcı (constructor) dosyayı diskteki konumundan okur:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Neden önemli:* Aspose.Cells, hücre stilleri, formüller ve font bilgileri dahil olmak üzere çalışma kitabını ayrıştırır. Dosya bulunamazsa bir istisna fırlatılır; bu yüzden yolun doğru olduğundan emin olun.

## Adım 3: Fontları gömmek için HTML kaydetme seçeneklerini yapılandırın

**HTML'de font gömme** işleminin çekirdeği `HtmlSaveOptions` sınıfıdır. `EmbedFonts` özelliğini `true` yaparak, çalışma kitabında kullanılan her font, HTML çıktısına Base64‑kodlu bir `@font-face` kuralı olarak yazılır.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Neden önemli:* Varsayılan olarak Aspose.Cells dış font dosyalarına referans verir; bu dosyalar istemci makinede bulunmayabilir. `EmbedFonts` etkinleştirildiğinde, render edilen HTML, izleyicinin yüklü fontlarından bağımsız olarak orijinal Excel sayfasıyla aynı görünür.

### Kenar durumu: desteklenmeyen fontlar

Çalışma kitabı, sunucuda yüklü olmayan bir font kullanıyorsa, Aspose.Cells varsayılan sistem fontuna geri döner. Bunu önlemek için gerekli fontları sunucuya kurun veya dışa aktardıktan sonra manuel olarak gömün.

## Adım 4: Yapılandırılmış seçeneklerle çalışma kitabını HTML olarak kaydedin

Artık HTML dosyasını yazabilirsiniz. `Save` metodu, çıktı yolunu ve `HtmlSaveOptions` örneğini alır:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Çalıştırdıktan sonra `Styled.html`, elektronik tablo verilerini ve her özel font için Base64‑kodlu `@font-face` tanımlarını içeren bir `<style>` bloğu barındırır.

## Adım 5: Gömülü fontları doğrulayın

`Styled.html` dosyasını bir tarayıcıda açın. `<head>` bölümünü inceleyin; aşağıdakine benzer bir şey görmelisiniz:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Fontlar tabloda doğru şekilde görüntüleniyorsa gömme başarılı demektir. Eksik karakterler fark ederseniz, dönüşümü gerçekleştiren makinede kaynak font dosyalarının kurulu olduğundan tekrar kontrol edin.

## Yaygın varyasyonlar ve ek seçenekler

### Birden fazla çalışma sayfasını dönüştürme

Tüm çalışma sayfaları için **Excel'i HTML'ye dönüştürmek** istiyorsanız, `ExportActiveWorksheetOnly = false` (varsayılan) ayarını kullanın. Aspose.Cells, her sayfa için ayrı bir HTML dosyası oluşturur.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### CSS çıktısını kontrol etme

HTML boyutunu küçültmek için satır içi CSS'yi devre dışı bırakabilirsiniz:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Dosya yerine akış (stream) kullanma

Bir web API'ye entegre ederken, HTML'yi bir `MemoryStream`'e yazarak doğrudan dönebilirsiniz:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro ipucu: Değerlendirme filigranlarını kaldırmak için ürünü lisanslayın

Değerlendirme sürümünü kullanıyorsanız, oluşturulan HTML bir filigran yorumu içerebilir. Çalışma kitabını yüklemeden önce Aspose.Cells lisansınızı uygulayarak temiz bir çıktı elde edin:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Tam çalışan örnek

Aşağıda **fontları nasıl gömeceğinizi**, **excel'i html'ye nasıl dönüştüreceğinizi** ve **excel'i html olarak nasıl dışa aktaracağınızı** tek seferde gösteren eksiksiz, çalıştırılabilir bir program yer almaktadır:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Beklenen çıktı:** Programı çalıştırdıktan sonra `Styled.html`, `YOUR_DIRECTORY` içinde oluşur. Dosyayı modern bir tarayıcıda açtığınızda, orijinal Excel dosyasındaki aynı fontlarla tablo gösterilir; bu fontlar makinede yüklü olmasa bile aynı görünüm sağlanır.

## Sonuç

Artık Aspose.Cells kullanarak **Excel'i HTML'ye dönüştürürken fontları nasıl gömeceğinizi** biliyorsunuz ve çalışma kitabını yüklemekten gömülü fontları doğrulamaya kadar tam süreci gördünüz. Bu yaklaşım, Excel dosyalarınızın görsel bütünlüğünün oluşturulan HTML'de korunmasını sağlar; bu da web raporlaması, e‑posta bültenleri veya özel tipografi gerektiren herhangi bir senaryo için idealdir.

Sonraki adımda, **Excel'i PDF olarak dışa aktarma**, **HTML çıktısını özel CSS ile stil verme** veya **birden fazla çalışma kitabını toplu işleme** gibi ilgili konuları keşfedin. Bu konuların hepsi aynı `HtmlSaveOptions` desenine dayanır, böylece kodu minimum değişiklikle uyarlayabilirsiniz.

İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}