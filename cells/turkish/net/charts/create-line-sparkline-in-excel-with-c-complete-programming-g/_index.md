---
category: general
date: 2026-06-30
description: C# ile Excel'de hızlıca çizgi sparkline oluşturun. Sparkline eklemeyi,
  C# ile Excel çalışma kitabı oluşturmayı ve birkaç adımda hücreye sparkline eklemeyi
  öğrenin.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: tr
og_description: C# ile Excel'de çizgi sparkline oluşturun. Bu öğreticide sparkline
  ekleme, C# ile Excel çalışma kitabı oluşturma ve sparkline'ı bir hücreye yerleştirme
  gösterilmektedir.
og_title: C# ile Excel’de Çizgi Sparkline Oluşturma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# ile Excel'de Çizgi Sparkline Oluşturma – Tam Programlama Rehberi
url: /tr/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel’de Çizgi Sparkline Oluşturma – Tam Programlama Rehberi

Hiç **çizgi sparkline** oluşturmayı C# kullanarak bir Excel dosyasında nasıl yapacağınızı merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli “Excel’i manuel olarak açmadan rapora sparkline eklemek nasıl olur?” diye soruyor. İyi haber şu ki, birkaç satır kodla çalışma kitabının içinde, UI olmadan şık bir çizgi sparkline oluşturabilirsiniz.

Bu öğreticide, **create Excel workbook C#** temellerinden, verileri doldurmaya, **add line sparkline** ve **add sparkline to cell** adımlarına kadar bilmeniz gereken her şeyi adım adım inceleyeceğiz. Sonunda, aylık satış trendlerini tek bakışta görselleştiren hazır bir *.xlsx* dosyanız olacak. Lafı uzatmadan, uygulanabilir ve çalıştırılabilir bir çözüm.

---

## Ne Oluşturacaksınız

- *KPI_Sparklines.xlsx* adlı yeni bir Excel çalışma kitabı  
- **KPI** adlı bir çalışma sayfası içinde örnek satış rakamları  
- **D2** hücresine yerleştirilen ve **B2:B13** veri aralığını referans alan bir **çizgi sparkline**  
- Sparkline’ı öne çıkaran temel biçimlendirme (renk, çizgi kalınlığı)  

Ön koşullar? Sadece .NET SDK (3.1+ veya .NET 6) ve ücretsiz Aspose.Cells for .NET kütüphanesi (NuGet üzerinden temin edilebilir). Aspose.Cells’i daha önce hiç kullanmadıysanız, koddan çağırabileceğiniz güçlü bir Excel motoru olarak düşünün—COM interop, Excel kurulumu gerekmez.

---

![C# kullanarak Excel’de çizgi sparkline oluşturma](https://example.com/images/create-line-sparkline.png "C# ile Excel’de çizgi sparkline oluşturma")

*Image alt text: C# kod örneğiyle Excel’de çizgi sparkline oluşturma*

---

## Adım 1: **Create Excel workbook C#** – Dosya ve çalışma sayfasını ayarlama

İlk işimiz bir çalışma kitabı nesnesi ve verilerin yer alacağı bir çalışma sayfası oluşturmak. Bu, **add line sparkline** ekleseniz de formül yazsanız da her Excel otomasyonunun temelidir.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Neden önemli:** `Workbook` sınıfı tüm dosyayı temsil ederken, `Worksheet` satır, sütun ve sonunda sparkline’ımız için bir tuvaldir. Sayfayı erken adlandırmak dosyanın düzenli ve kendini belgeleyen olmasını sağlar.

---

## Adım 2: Verileri doldurma – Sparkline için kaynak aralık

Bir sparkline’ın çizmesi için veriye ihtiyacı vardır. 12 aylık satış rakamlarını simüle edelim. Bunları bir veritabanından çekebilirsiniz, ancak açıklık açısından burada anında oluşturacağız.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **İpucu:** `PutValue` veri tipini otomatik algılar, bu yüzden `double` ya da `int`’e dönüştürmeye gerek yoktur. Hücreleri (para birimi, binlik ayırıcı) biçimlendirmeniz gerekirse, daha sonra bir `Style` nesnesi uygulayabilirsiniz.

---

## Adım 3: **Create line sparkline** – Sparkline’ı belirli bir hücreye ekleme

Şimdi gösterinin yıldızı: **çizgi sparkline**. Aspose.Cells sparkline’ları gruplar, bu yüzden önce `Line` tipinde bir `SparklineGroup` oluşturur, ardından görselin nerede görüneceğini belirtiriz.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Nasıl çalışır:**  
> - `firstRow/firstColumn` ve `lastRow/lastColumn` *hedef hücreyi* (sparkline’ın görüneceği yeri) tanımlar.  
> - `firstDataRow/lastDataRow` kaynak aralığı gösterir.  
> **çizgi sparkline** kullandığımız için görsel, sayıların trendini izleyen basit ince bir çizgi olacaktır.

### Opsiyonel: **How to add sparkline** – Özel stil ile

Sparkline’ın öne çıkmasını istiyorsanız, birkaç özelliği ayarlayın:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Neden stil vermelisiniz?** Beyaz arka plan üzerinde koyu mavi bir çizgi göz yormaz, işaretçiler ise bireysel veri noktalarına hızlı bir bakış sağlar—sunumlar için çok kullanışlıdır.

---

## Adım 4: Çalışma kitabını kaydet – Sonucu doğrulama

Sparkline yerleştirildiğine göre, dosyayı diske yazmamız yeterli. Yazma izniniz olan bir klasör seçin; örnek, değiştirilmesi gereken bir yer tutucu yol kullanıyor.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Doğrulama:** Oluşturulan dosyayı Excel’de (veya .xlsx destekleyen herhangi bir görüntüleyicide) açın. **D2** hücresinde **çizgi sparkline**’ın **B** sütunundaki artan satış rakamlarını yansıttığını görmelisiniz. Sparkline üzerine gelindiğinde alt değerleri gösteren bir araç ipucu (tooltip) çıkar.

---

## Adım 5: **add sparkline to cell** sırasında sıkça karşılaşılan sorunlar

Basit bir örnek bile yeni başlayanları şaşırtabilir. Dikkat etmeniz gereken birkaç nokta:

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Yanlış hücre koordinatları | Sparkline hedefi sıfır‑tabanlı sütun indeksi, ancak bir‑tabanlı satır indeksi kullanır. | `Cells[row, column]`’de `row` ve `column` ikisinin de sıfır‑tabanlı olduğunu unutmayın. `SparklineGroup.Add` içinde satır ve sütun **1‑tabanlı**dır. |
| Veri gösterilmiyor | Kaynak aralık boş ya da sayısal olmayan değerler içeriyor. | Aralığın (ör. `B2:B13`) sayılar içerdiğinden emin olun. Sayısal tiplerle `PutValue` kullanın. |
| Sparkline kaydedildikten sonra kayboluyor | Kütüphane sürüm uyuşmazlığı veya lisans eksikliği. | En yeni Aspose.Cells paketini kullanın ve değerlendirme sınırlarını aştıysanız geçerli bir lisans sağlayın. |
| Biçimlendirme uygulanmadı | Stil değişiklikleri sparkline eklenmeden önce yapıldı. | Stil **sparkline grubunu oluşturduktan** sonra ayarlayın, yukarıda gösterildiği gibi. |

---

## Tam Kaynak Kodu – Tek‑tık kopyala‑yapıştır

Aşağıda, tamamen çalıştırılabilir program yer alıyor. Yeni bir konsol projesine yapıştırın, Aspose.Cells NuGet paketini ekleyin ve **F5** tuşuna basın.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** *KPI_Sparklines.xlsx* dosyasını açtığınızda **B** sütununda on iki sayı (5.000 → 13.250) listelenecek ve **D2** hücresinde, artan bir trendi gösteren koyu‑mavi bir çizgi sparkline bulunacak. `ShowMarkers` etkinleştirildiyse işaretçiler küçük turuncu‑kırmızı noktalar olarak görünecek.

---

## Sıradaki Adım? Sparkline Yetkinliğinizi Genişletin

Artık Aspose.Cells ile **create line sparkline** konusunu kavradığınıza göre, aşağıdaki ilgili konuları keşfetmeyi düşünün:

- **Add column sparkline** – yığılmış verileri göstermek için ideal.  
- **Create multi‑sparkline groups** – aynı sayfada yan yana karşılaştırma için birden fazla grup oluşturma.  
- **Export to PDF** – sparklineları koruyarak PDF’ye dönüştürme (Aspose.Cells PDF dönüşümünü destekler).  
- **Dynamic data sources** – sabit değerler yerine gerçek satış rakamlarını bir SQL veritabanından çekme.  

Bu konuların her biri aynı temel kavramlar üzerine kurulu: **create Excel workbook C#**, verileri doldur, ve **add sparkline to cell** istediğiniz stil ile ekle.

---

### TL;DR

C# kullanarak bir Excel çalışma kitabında **çizgi sparkline** oluşturmayı gösterdik. Adımlar—*çalışma kitabı oluştur, verileri doldur, sparkline ekle, stil ver ve kaydet*—tek bir, bağımsız programda birleştirildi. Raporlama ihtiyaçlarınıza göre renkleri, çizgi kalınlığını veya kaynak aralığını özgürce değiştirin.

Paylaşmak istediğiniz bir farklılık var mı? Aşağıya yorum bırakın, kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}