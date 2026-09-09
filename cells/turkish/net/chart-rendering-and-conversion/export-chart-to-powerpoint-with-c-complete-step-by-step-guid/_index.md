---
category: general
date: 2026-02-26
description: C# kullanarak Excel'den PowerPoint'e grafik dışa aktar. Excel'i PowerPoint'e
  nasıl dönüştüreceğinizi, Excel'i PowerPoint olarak nasıl kaydedeceğinizi ve şekilleri
  düzenlenebilir tutmayı öğrenin.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: tr
og_description: C# kullanarak Excel'den PowerPoint'e grafik dışa aktarın. Bu kılavuz,
  Excel'i PowerPoint'e nasıl dönüştüreceğinizi, çalışma kitabını PPTX olarak nasıl
  kaydedeceğinizi ve şekilleri düzenlenebilir tutmayı gösterir.
og_title: C# ile Grafiği PowerPoint'e Aktar – Tam Programlama Öğreticisi
tags:
- Aspose.Cells
- C#
- Office Automation
title: C# ile Grafiği PowerPoint'e Aktarma – Tam Adım Adım Kılavuz
url: /tr/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint'e Grafik Dışa Aktarma – Tam Programlama Öğreticisi

PowerPoint'e **grafik dışa aktarma** işlemini düzenlenebilirliğini kaybetmeden nasıl yapabileceğinizi hiç merak ettiniz mi? Birçok raporlama senaryosunda slayt setinde canlı bir grafik gerekir, ancak kopyala‑yapıştır manuel olarak zahmetlidir. İyi haber şu ki, bunu birkaç satır C# koduyla programatik olarak yapabilirsiniz.

Bu rehberde tüm süreci adım adım inceleyeceğiz: bir grafik ve metin kutusu içeren bir Excel çalışma kitabını yüklemek, dışa aktarımı metin kutuları ve şekillerin düzenlenebilir kalacak şekilde yapılandırmak ve sonunda sonucu bir **PowerPoint** dosyası olarak kaydetmek. Sonunda **Excel'i PowerPoint'e dönüştürme**, **Excel'i PowerPoint olarak kaydetme** ve kenar‑durum senaryoları için seçenekleri ayarlama konularında da bilgi sahibi olacaksınız.

## Gereksinimler

- **Aspose.Cells for .NET** (sürüm 23.10 veya daha yeni). Dönüşümü zahmetsiz hâle getiren kütüphane.
- **.NET 6+** çalışma zamanı – herhangi bir yeni SDK yeterli.
- En az bir grafik ve bir metin kutusu içeren basit bir Excel dosyası (`ChartWithTextbox.xlsx`).
- Visual Studio ya da tercih ettiğiniz IDE.

Ek bir NuGet paketi Aspose.Cells dışına gerek yok, ancak temel C# sözdizimini bilmek kesinlikle yardımcı olur.

## PowerPoint'e Grafik Dışa Aktarma – Adım Adım

Aşağıda çözümü ayrı, takip etmesi kolay adımlara bölüyoruz. Her adım, ihtiyacınız olan tam kodu ve neden bu şekilde yapmanız gerektiğini açıklayan kısa bir “neden” paragrafı içerir.

### Adım 1: Grafiği İçeren Excel Çalışma Kitabını Yükleyin

İlk olarak kaynak dosyayı belleğe almamız gerekiyor. Aspose.Cells'tan `Workbook` kullanmak, grafikleri, resimleri ve gömülü nesneleri içeren tüm çalışma sayfasını okur.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Bu neden önemli:* Çalışma kitabı yolu doğru belirtilmezse `FileNotFoundException` alırsınız. Hızlı bir kontrol, daha sonra boş bir slayt dışa aktarmanızı önler.

### Adım 2: Şekillerin Düzenlenebilir Kalması İçin Sunum Seçeneklerini Hazırlayın

Aspose.Cells, metin kutuları, şekiller ve hatta grafiğin kendisinin dışa aktarıldıktan sonra **düzenlenebilir** kalıp kalmayacağını belirlemenize izin verir. `ExportTextBoxes` ve `ExportShapes` özelliklerini `true` olarak ayarlamak, bu nesneleri statik bir görüntü yerine yerel PowerPoint öğeleri olarak korur.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Bu neden önemli:* Bu bayrakları varsayılan (`false`) bırakırsanız, ortaya çıkan slayt grafiğin bir bitmap'ini içerir ve serileri düzenlemek ya da başlığı değiştirmek mümkün olmaz. Her iki seçeneği de etkinleştirmek, manuel olarak çizdiğiniz bir PowerPoint grafiği gibi tam anlamıyla düzenlenebilir bir grafik elde etmenizi sağlar.

### Adım 3: Excel'i PowerPoint'e Dönüştürün ve Dosyayı Kaydedin

Şimdi `Save` metodunu, `SaveFormat.Pptx` enum'ını ve az önce yapılandırdığımız seçenekleri geçirerek çağırıyoruz. Kütüphane, Excel grafik nesnesini bir PowerPoint grafik şekline dönüştürmeyi üstlenir.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Bu neden önemli:* `Save` çağrısı tüm ağır işleri yapar—Excel serilerini PowerPoint serilerine eşleştirir, eksen biçimlendirmesini korur ve bağlı metin kutularını kopyalar. Bu satır çalıştıktan sonra, Microsoft PowerPoint'te açılmaya hazır tam‑düzenlenebilir bir `.pptx` dosyanız olur.

### Sonucu Doğrulayın

`Result.pptx` dosyasını PowerPoint'te açın. Şu öğeleri içeren bir slayt görmelisiniz:

- Orijinal grafik, hâlâ verisine bağlı (serileri düzenlemek için çift‑tıklayabilirsiniz).
- Excel sayfasındaki metin kutusu, artık yerel bir PowerPoint metin kutusu.
- Slayt düzeni otomatik olarak seçilir (genellikle boş bir slayt).

Eksik bir öğe fark ederseniz, kaynak çalışma kitabının gerçekten görünür nesneler içerdiğini ve `ExportTextBoxes` / `ExportShapes` değerlerinin `true` olduğundan emin olun.

### Excel'i PowerPoint'e Dönüştürme: Birden Çok Çalışma Sayfasını İşleme

Çoğu zaman bir çalışma kitabı birden fazla sayfa ve her sayfada ayrı bir grafik bulunur. Varsayılan olarak Aspose.Cells, **tüm** çalışma sayfalarındaki **tüm** grafikleri ayrı slaytlara dışa aktarır. Sadece bir kısmına ihtiyacınız varsa, kaydetmeden önce filtreleyebilirsiniz:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Pro tip:* `chart.IsVisible = false` ayarı, grafiği tamamen kaldırmaktan daha ucuzdur ve kaynağı değiştirmeden dahil etmeyi açıp kapamanıza olanak tanır.

### Excel'i PowerPoint Olarak Kaydet – Slayt Boyutunu Özelleştirme

PowerPoint varsayılan olarak 10 inç × 5.63 inç bir slayt kullanır. Grafik sıkışık görünüyorsa, `PresentationOptions` nesnesi üzerinden slayt boyutlarını değiştirebilirsiniz:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Artık dışa aktarılan grafik daha geniş bir alana sahip olur ve metin kutuları orijinal yerleşimlerini korur.

### Excel'i PPT'ye Dönüştürme: Gizli Nesnelerle Baş Etme

Gizli satırlar, sütunlar veya şekiller bazen dışa aktarımda ortaya çıkabilir. Bunları temizlemek için kaydetmeden önce hızlı bir temizlik yapın:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Bu adım her zaman gerekli değildir, ancak final slayt setinizde beklenmedik boşlukların oluşmasını engeller.

### Çalışma Kitabını PPTX Olarak Kaydet – Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, tüm akışı gösteren hazır bir konsol programı aşağıdadır:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Bu programı çalıştırdığınızda, **çalışma kitabını pptx olarak kaydet** işleminin tam karşılığı olan düzenlenebilir bir grafik ve metin kutusu içeren `Result.pptx` dosyası oluşturulur.

![PowerPoint'e grafik dışa aktarım örneği](/images/export-chart-to-powerpoint.png "PowerPoint'e grafik dışa aktarım – düzenlenebilir slayt")

## Yaygın Sorular & Özel Durumlar

**Excel dosyası harici bir veri kaynağına bağlı bir grafik içeriyorsa ne olur?**  
Aspose.Cells, *mevcut* veri değerlerini PowerPoint grafiğine kopyalar. Harici bağlantıyı **korumaz**, çünkü PowerPoint aynı şekilde bir Excel veri bağlantısını referans gösteremez. Canlı güncellemeler gerekiyorsa, orijinal Excel dosyasını PPTX içinde bir OLE nesnesi olarak gömmeyi düşünün.

**Özel bir tema kullanan bir grafiği dışa aktarabilir miyim?**  
Evet. Kütüphane, Excel tema renklerini PowerPoint tema slotlarına eşlemeye çalışır. Çok özel paletler için dışa aktardıktan sonra PowerPoint API'si (ör. Aspose.Slides) ile renkleri ayarlamanız gerekebilir.

**Grafik sayısı için bir sınırlama var mı?**  
Pratikte yoktur—Aspose.Cells veriyi akış (stream) olarak işler, bu yüzden onlarca grafik içeren bir çalışma kitabı da dışa aktarılır; ancak ortaya çıkan PPTX dosyasının boyutu lineer olarak artar.

**Aspose.Cells için bir lisansa ihtiyacım var mı?**  
Ücretsiz deneme sürümü çalışır, ancak ilk slayta bir filigran ekler. Üretim ortamında filigranı kaldırmak ve tam performansı elde etmek için uygun bir lisans temin edin.

## Özet

C# kullanarak **grafik dışa aktarma** işlemini nasıl yapacağınızı, bir Excel çalışma kitabını nasıl yükleyeceğinizi, metin kutuları ve şekillerin düzenlenebilir kalması için `PresentationOptions` nasıl yapılandırılacağını ve son olarak sonucu bir `.pptx` olarak nasıl kaydedeceğinizi adım adım gösterdik. Ayrıca **Excel'i PowerPoint'e dönüştürme**, **Excel'i PowerPoint olarak kaydetme** ve “**Excel'i ppt'ye nasıl dönüştürürüm**” sorusuna tam, çalıştırılabilir bir örnekle yanıt verdik.

## Sıradaki Adımlar

- **Çalışma kitabını PPTX olarak kaydet** ve birden çok slayt: her çalışma sayfası için `Save` metodunu `PresentationOptions` ile döngü içinde çağırın.
- Oluşturulan PPTX'i daha da özelleştirmeniz gerekiyorsa **Aspose.Slides**'ı keşfedin (geçişler, konuşmacı notları vb. ekleyin).
- **Pivot grafikleri** veya **3‑D grafikler** dışa aktarın—aynı seçenekler geçerli, ancak eksen biçimlendirmesini sonradan ayarlamanız gerekebilir.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da en yeni API değişiklikleri için resmi Aspose.Cells belgelerine göz atın. Kodlamanın tadını çıkarın ve sadece birkaç C# satırıyla Excel grafiklerinizi şık PowerPoint sunumlarına dönüştürmenin keyfini yaşayın!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}