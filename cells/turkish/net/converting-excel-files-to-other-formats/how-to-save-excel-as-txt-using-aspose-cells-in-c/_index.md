---
category: general
date: 2026-10-13
description: Aspose.Cells ile Excel’i TXT olarak kaydetmeyi öğrenin. Bu kılavuz, Excel’i
  TXT’ye dışa aktarmayı, hücreye değer yazmayı ve sadece birkaç adımda anlamlı basamakları
  ayarlamayı kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: tr
lastmod: 2026-10-13
og_description: Aspose.Cells ile Excel'i TXT olarak kaydedin. Excel'i TXT'ye nasıl
  dışa aktaracağınızı, hücreye değer yazmayı ve sadece birkaç C# satırıyla anlamlı
  basamakları nasıl ayarlayacağınızı öğrenin.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Excel'i TXT olarak kaydet – .NET geliştiricileri için adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Aspose.Cells ile C#'ta Excel'i TXT olarak kaydetme
url: /tr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i TXT olarak Kaydetme Aspose.Cells ile C#'ta

Eğer **Excel'i TXT olarak kaydetmek** istiyorsanız, bu öğretici beş dakikadan kısa sürede tam süreci gösterir. Excel'i TXT'ye nasıl dışa aktaracağınızı, hücreye değer nasıl yazılacağını ve anlamlı basamakları nasıl ayarlayacağınızı göreceksiniz, böylece metin dosyası tam olarak beklediğiniz verileri içerir.

Bir elektronik tabloyu TXT olarak dışa aktarmak, alt sistemlerin yalnızca düz metin girişi kabul ettiği, log oluşturmanız gerektiği veya hesaplamaların insan tarafından okunabilir bir dökümünü istediğiniz durumlarda faydalıdır. Aşağıdaki örnek Aspose.Cells v25.10 veya daha yeni sürümlerle çalışır ve herhangi bir .NET 6+ çalışma zamanında çalışır.

## Önkoşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

* **Aspose.Cells for .NET**'in lisanslı bir kopyası (ücretsiz deneme sürümü test için çalışır).
* .NET 6 SDK veya daha yeni bir sürüm yüklü.
* Visual Studio 2022, VS Code veya Rider gibi bir IDE.
* Temel C# bilgisi—gelişmiş Excel otomasyonu deneyimi gerekmez.

Aspose.Cells NuGet paketini şu şekilde kurabilirsiniz:

```bash
dotnet add package Aspose.Cells
```

## Adım 1: Bir çalışma kitabı oluşturun ve ilk çalışma sayfasına erişin (excel'i txt olarak kaydet)

**Excel'i TXT olarak kaydetmek** istediğinizde ilk yapmanız gereken bir `Workbook` nesnesi oluşturmaktır. Bu nesne, tüm Excel dosyasını bellekte temsil eder.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Neden önemli:** `Workbook` sınıfı tüm elektronik tablo işlemleri için giriş noktasıdır. Yeni bir çalışma kitabı ile başlayarak, düz metin çıktısını etkileyebilecek gizli biçimlendirmelerden kaçınırsınız.

## Adım 2: Hücreye yüksek hassasiyetli bir sayı yazın (write value to cell)

Şimdi **write value to cell** A1 yapmanız gerekiyor. `PutValue` yöntemi veri tipini otomatik olarak algılar ve sayısal bir değer olarak depolar.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **İpucu:** Daha sonra string, tarih veya formül yazmanız gerekirse, aynı `PutValue` yöntemi çalışır—sadece uygun .NET tipini geçirin.

## Adım 3: İhracat seçeneklerini yalnızca gerekli hassasiyeti tutacak şekilde yapılandırın (set significant digits)

Bir TXT dosyasına dışa aktarırken, dosya boyutunu küçük tutmak veya bir sonraki sistemin gereksinimlerine uymak için genellikle basamak sayısını sınırlamak istersiniz. `TxtSaveOptions` sınıfı bu amaçla bir `SignificantDigits` özelliği sunar.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Neden anlamlı basamakları ayarlamalısınız:** Bu ayar olmadan, Aspose.Cells tam çift hassasiyetli değeri yazar ve `12345.6789012345` gibi uzun dizgiler üretebilir. `SignificantDigits = 6` ayarlamak çıktıyı `12345.7`'ye kısaltır ve çoğu raporlama gereksinimiyle eşleşir.

## Adım 4: Çalışma kitabını TXT dosyası olarak dışa aktar (export excel to txt)

Son olarak, daha önce yapılandırılmış seçeneklerle `Workbook.Save` metodunu çağırarak **Excel'i TXT'ye dışa aktar**.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Kod tamamlandığında, `LimitedDigits.txt` şunları içerir:

```
12345.7
```

> **Sonuç doğrulama:** Dosyayı herhangi bir metin düzenleyicide (Notepad, VS Code) açarak yalnızca altı anlamlı basamağın bulunduğunu ve ekstra virgül ya da sekme ayırıcılarının olmadığını doğrulayın.

## Tam, çalıştırılabilir örnek

Aşağıda, kopyalayıp yapıştırarak hemen çalıştırabileceğiniz bağımsız bir konsol uygulaması bulunmaktadır.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Her bloğun açıklaması**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Aspose.Cells, `Workbook`, `Worksheet` ve `TxtSaveOptions` için gerekli olan Aspose.Cells ad alanını içe aktarır. |
| `Workbook workbook = new Workbook();` | Bellekte boş bir Excel çalışma kitabı oluşturur. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 hücresine çift hassasiyetli bir sayı yazar. |
| `TxtSaveOptions` | TXT dışa aktarımı için **set significant digits** davranışını yapılandırır. |
| `workbook.Save(..., txtOptions);` | **export excel to txt** işlemini yürütür ve düz metin dosyasını oluşturur. |

## Kenar durumları ve ek ipuçları

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | Unicode desteği gerekiyorsa `txtOptions.Encoding = Encoding.UTF8` kullanın ve yüksek bellek kullanımını önlemek için dosyayı `Workbook.Save(Stream, txtOptions)` ile akışa kaydetmeyi düşünün. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` ayrıca `Separator` özelliğini sunar—CSV‑stil çıktısı üretmek için `','` olarak ayarlayın, yine de TXT formatını kullanır. |
| **Preserving formulas** | Formülleri korumak için `txtOptions.ExportFormulas = true` ayarlayın; böylece hesaplanmış değer yerine formül metni yazılır. |
| **Locale‑specific decimal separators** | Avrupa yerel ayarları için `txtOptions.DecimalSeparator` değerini `','` olarak ayarlayın. |
| **Multiple worksheets** | `workbook.Worksheets` üzerinde döngü yapın ve her biri için `Save` çağırın, dosya adına çalışma sayfası adını ekleyin. |

## Sıkça Sorulan Sorular

**Q: `SignificantDigits` yuvarlar mı yoksa kırpar mı?**  
A: Belirtilen anlamlı basamak sayısına göre en yakın değere yuvarlar ve çıktı bu hassasiyete matematiksel olarak doğru olur.

**Q: Bellek akışına doğrudan dışa aktarabilir miyim?**  
A: Evet. Dosya yolunu bir `MemoryStream` örneğiyle değiştirin: `workbook.Save(stream, txtOptions);`. Bu, TXT içeriğini dosya sistemine dokunmadan döndürmesi gereken web API'leri için kullanışlıdır.

**Q: Orijinal biçimlendirmeyi (ör. tarih) korumam gerekirse ne yapmalıyım?**  
A: `txtOptions.ExportFormattedValues = true` kullanın. Bu, Aspose.Cells'in hücrenin gösterilen metnini ham değer yerine yazmasını sağlar.

## Sonuç

Artık **Excel'i TXT olarak kaydetme** konusunda hassasiyet, biçimlendirme ve çıktı konumu üzerinde tam kontrol sahibi olduğunuzu biliyorsunuz. Dört adımı izleyerek—bir çalışma kitabı oluşturun, **write value to cell**, **set significant digits**, ve **export Excel to TXT**—herhangi bir .NET uygulamasına düz metin dışa aktarımını entegre edebilirsiniz.

Sonra, **özel ayırıcılarla elektronik tabloyu TXT olarak dışa aktar**, **Excel'i CSV'ye dönüştür**, veya **Aspose.Cells ile JSON raporları oluştur** gibi ilgili konuları keşfedin. Bunların her biri burada gösterilen aynı temel kavramlara dayanır ve platformlar arası veri değişimi için çok yönlü bir araç seti sunar.

Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

İşte bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan öğreticiler. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Excel'i Metin Olarak Kaydet – C# ile Excel'i TXT'ye Dışa Aktarma Tam Kılavuzu](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Yeni Çalışma Kitabı Oluştur ve Hassasiyetle Excel'i TXT'ye Dışa Aktar](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Yeni çalışma kitabı oluştur – Tam Hassasiyetle Excel'i TXT'ye Dışa Aktar](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}