---
category: general
date: 2026-03-18
description: C# ile Aspose.Cells kullanarak pivot tabloyu kopyalayın. Excel aralığını
  nasıl kopyalayacağınızı, Excel pivotunu nasıl çoğaltacağınızı, aralığı yeni sayfaya
  nasıl kopyalayacağınızı ve pivotu sayfaya nasıl kopyalayacağınızı dakikalar içinde
  öğrenin.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: tr
og_description: Aspose.Cells kullanarak C#'ta pivot tablo kopyalama. Excel pivotunu
  çoğaltmayı, Excel aralığını yeni bir konuma kopyalamayı ve pivotu sayfaya kopyalamayı
  tam kod örnekleriyle öğrenin.
og_title: C#'de Pivot Tablosunu Kopyala – Tam Programlama Rehberi
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'de Pivot Tablosunu Kopyalama – Adım Adım Rehber
url: /tr/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Pivot Tablo Kopyalama – Tam Programlama Rehberi

Bir çalışma kitabının bir bölümünden diğerine **pivot tablo kopyalama** ihtiyacı hiç duydunuz mu, ancak temel veri bağlantılarını kaybetmeden nasıl yapılacağını bilemediniz mi? Tek başınıza değilsiniz. Birçok geliştirici, özellikle pivot büyük bir veri bloğu içinde yer aldığında Excel raporlarını otomatikleştirirken bu sorunu yaşıyor. İyi haber? Aspose.Cells ile pivot tabloyu **tam olarak göründüğü gibi** kopyalayabilirsiniz ve ayrıca **excel aralığını kopyalama**, **excel pivotunu çoğaltma** ve hatta **pivotu sayfaya kopyalama** işlemlerini sadece birkaç C# satırıyla öğrenebileceksiniz.

Bu öğreticide gerçek bir senaryoyu adım adım inceleyeceğiz: *A1:J20* aralığını kapsayan bir pivotu aynı çalışma sayfasında yeni bir alan *M1:V20*’ye taşımak. Sonunda çalıştırılabilir bir programınız olacak, her adımın neden önemli olduğunu anlayacaksınız ve kodu diğer aralıklar ya da ayrı çalışma sayfaları için nasıl uyarlayacağınızı bileceksiniz. Harici belgelere gerek yok—her şey burada.

---

## Önkoşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

- **Aspose.Cells for .NET** (sürüm 23.9 veya üzeri). NuGet üzerinden alabilirsiniz: `Install-Package Aspose.Cells`.
- Temel bir C# geliştirme ortamı (Visual Studio 2022, Rider veya C# uzantılı VS Code).
- *A1:J20* aralığında bir pivot tablo içeren bir Excel dosyası (`source.xlsx`).

Hepsi bu. Bir konsol uygulaması oluşturabiliyorsanız, hazırsınız.

---

## Aspose.Cells ile pivot tablo nasıl kopyalanır

Çözümün çekirdeği tek bir `Worksheet.Cells.CopyRange` çağrısıdır. Bu yöntem yalnızca hücre değerlerini kopyalamakla kalmaz, aynı zamanda pivot tabloları, grafikleri ve diğer zengin nesneleri otomatik olarak korur. Şimdi adımlara bakalım.

### Adım 1: Kaynak çalışma kitabını yükleyin

İlk olarak çalışma kitabını belleğe getirmemiz gerekiyor.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Neden önemli:** Çalışma kitabını yüklemek, Aspose.Cells’in Excel’i başlatmadan manipüle edebileceği bellek içi bir temsil oluşturur. Hızlıdır, çok iş parçacıklı güvenlidir ve sunucularda çalışır.

### Adım 2: İlk çalışma sayfasını alın

Çoğu örnek ilk sayfayı kullanır, ancak istediğiniz indeks ya da adı hedefleyebilirsiniz.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **İpucu:** Aynı sayfa yerine **pivotu sayfaya kopyalama** ihtiyacınız varsa, `worksheet` referansını başka bir `Worksheet` nesnesine değiştirmeniz yeterlidir.

### Adım 3: Kaynak ve hedef aralıkları tanımlayın

Taşıdığımız blokları tanımlamak için `CellArea` yapısını kullanacağız.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Açıklama:** Satır ve sütun indeksleri sıfır‑tabanlıdır. Sütun 0 = **A**, sütun 12 = **M** vb. Pivotunuz başka bir yerde ise bu sayıları ayarlayın.

### Adım 4: Kopyalama işlemini gerçekleştirin

Şimdi sihir gerçekleşir. Son boolean parametresini `true` olarak ayarlamak, Aspose.Cells’in tüm nesneleri—pivot dahil—kopyalamasını sağlar.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Neden `true`?** Bayrak “tüm nesneleri kopyala” anlamına gelir. `false` ayarlarsanız yalnızca düz hücre değerleri taşınır ve pivot kaybolur.

### Adım 5: Çalışma kitabını kaydedin

Son olarak, değiştirilmiş çalışma kitabını diske yazın.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Sonuç:** `copy-pivot.xlsx` artık orijinal pivotu *A1:J20* **ve** aynı pivotun bir kopyasını *M1:V20*’de içeriyor. Her iki pivotun da işlevsel olduğunu ve veri bağlantılarını koruduğunu doğrulamak için dosyayı Excel’de açın.

---

## Excel aralığını yeni bir konuma kopyalama – hızlı bir varyasyon

Bazen sadece **excel aralığını kopyalama** ihtiyacınız olur, pivotlarla uğraşmazsınız. Aynı `CopyRange` yöntemi iş görür; sadece son argümanı `false` yapın.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Ne zaman kullanılır:** Geçici bir hesaplama sayfası için ham veri taşıyorsanız, nesne kopyasını devre dışı bırakmak bellek tasarrufu sağlar ve işlemi hızlandırır.

---

## Excel pivotunu birden çok sayfada çoğaltma

Farklı bir çalışma sayfasında **excel pivotunu çoğaltma** ihtiyacınız varsa ne yapmalısınız? Desen aynı kalır; sadece hedef için başka bir `Worksheet` referansı verin.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Köşe durumu:** Kaynak pivot, orijinal sayfada bulunan bir tabloyu kullanıyorsa, Aspose.Cells aynı zamanda temel tablo tanımını da kopyalar, böylece yeni pivot kutudan çıkar çıkmaz çalışır.

---

## Yaygın tuzaklar ve nasıl önlenir

| Tuzak | Neden olur | Çözüm |
|---------|----------------|-----|
| **Pivot önbelleğini kaybeder** | `CopyRange`’i `false` ile kullanmak ya da nesneleri yok sayan özel bir kopyalama rutini. | Pivot gerektiğinde her zaman `true` geçin. |
| **Hedef hücrelerde zaten veri var** | Sessizce üzerine yazar, mevcut formülleri bozabilir. | Hedef alanı önce temizleyin: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Kaynak aralık pivotun tamamını içermiyor** | Pivot tabloları beklenenden daha fazla satır/sütun kapsar (ör. gizli satırlar). | `worksheet.PivotTables[0].DataRange` ile tam sınırları programatik olarak alın. |
| **Çalışma kitapları arasında kopyalama** | `CopyRange` yalnızca aynı çalışma kitabı içinde çalışır. | `sourceWorksheet.Cells.CopyRange` ile geçici bir aralığa kopyalayın, ardından `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` kullanın. |

---

## Beklenen çıktı ve doğrulama

Programı çalıştırdıktan sonra:

1. `copy-pivot.xlsx` dosyasını açın.
2. **A1:J20** ve **M1:V20** konumlarında iki aynı pivot tablo göreceksiniz.
3. Her iki pivotu da yenileyin; aynı temel veriyi yansıtmalı.
4. Başka bir sayfaya çoğalttıysanız, yeni sayfa da işlevsel bir kopya içermelidir.

Kod ile hızlı doğrulama:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro ipucu: Aralık tespiti otomasyonu

Statik raporlar için `CellArea` sabit kodlamak işe yarasa da, üretim kodunda pivotu dinamik olarak bulmak gerekir.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Neden?** Bu sayede çözümünüz düzen değişikliklerine karşı dayanıklı olur—“Pivot B2’ye taşındı” hataları ortadan kalkar.

---

![copy pivot table example](copy-pivot.png){alt="copy pivot table example"}

*Ekran görüntüsü (yer tutucu) sol tarafta orijinal pivotu, sağ tarafta ise kopyalanmış halini gösteriyor.*

---

## Özet

C#’ta Aspose.Cells kullanarak **pivot tablo kopyalama** yöntemini, **excel aralığını kopyalama**, **excel pivotunu çoğaltma** ve hatta **pivotu sayfaya kopyalama** tekniklerini inceledik. Temel çıkarımlar:

- Zengin nesneleri korumak için `Worksheet.Cells.CopyRange` metodunu `true` bayrağıyla kullanın.
- Sıfır‑tabanlı indekslerle kaynak ve hedef `CellArea` nesnelerini tanımlayın.
- Başka bir sayfaya **pivotu sayfaya kopyalama** ihtiyacınız varsa hedef çalışma sayfasını değiştirin.
- Mevcut veri, gizli satırlar ve çapraz‑çalışma kitabı senaryoları gibi kenar durumlarına dikkat edin.

---

## Sıradaki adımlar

- **Dinamik pivot keşfi**: Çalışma kitabındaki tüm pivotları tarayan ve otomatik olarak çoğaltan bir yardımcı oluşturun.
- **PDF/HTML’ye dışa aktarım**: Kopyalama sonrası sayfayı rapor formatına dönüştürmek isteyebilirsiniz—Aspose.Cells bunu da destekler.
- **Performans ayarı**: Büyük çalışma kitapları için kopyalamadan önce hesaplamayı devre dışı bırakıp ardından yeniden etkinleştirmeyi düşünün.

Denemeler yapın: hedef koordinatları değiştirin, tamamen yeni bir çalışma kitabına kopyalayın ya da birden çok sayfada döngü kurarak birleştirilmiş rapor oluşturun. Olanaklar sınırsızdır ve şimdi sahip olduğunuz temel sayesinde neredeyse her Excel otomasyon görevine uyum sağlayabilirsiniz.

Kodlamanın tadını çıkarın, pivotlarınız her zaman mükemmel senkronize olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}