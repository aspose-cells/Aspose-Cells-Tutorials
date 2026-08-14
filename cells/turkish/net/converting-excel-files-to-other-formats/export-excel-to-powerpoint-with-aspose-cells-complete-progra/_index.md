---
category: general
date: 2026-08-14
description: Aspose.Cells kullanarak Excel'i PowerPoint'e aktarın ve kod içinde Excel
  formüllerini nasıl hesaplayacağınızı öğrenin. Tam kaynak kodlu adım adım C# örneği.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: tr
lastmod: 2026-08-14
og_description: Aspose.Cells ile Excel'i PowerPoint'e aktarın ve kodda Excel formüllerini
  hesaplayın. Çalışma kitaplarından düzenlenebilir PPTX dosyaları oluşturmak için
  bu kapsamlı rehberi izleyin.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Aspose.Cells ile Excel'i PowerPoint'e Aktarın – tam C# öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Aspose.Cells ile Excel'i PowerPoint'e Aktarma – Tam Programlama Rehberi
url: /tr/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PowerPoint'e Aktarma Aspose.Cells ile – tam programlama rehberi

Programatik olarak **Excel'i PowerPoint'e aktarmanız** gerekiyorsa, bu rehber Aspose.Cells for .NET ile bunu nasıl yapacağınızı tam olarak gösterir. Ayrıca **kod içinde Excel formüllerini hesaplamayı**, tanımları kaybetmeden pivot tabloları kopyalamayı ve dinamik diziler için yeni Office‑365 EXPAND işlevini kullanmayı öğreneceksiniz.

Aşağıdaki bölümlerde gerçek bir C# örneği üzerinden ilerleyecek, her satırın neden önemli olduğunu açıklayacak ve yaygın tuzakları ele alacağız, böylece çözümü kendi projelerinize uyarlayabilirsiniz.

## Bu öğreticide neler ele alınıyor

* Mevcut bir çalışma kitabını (`input.xlsx`) yükleme  
* Pivot tablo içeren bir aralığı tanımını koruyarak kopyalama  
* Çalışma kitabını düzenlenebilir metin kutuları ve şekiller içeren bir PowerPoint (`.pptx`) dosyasına aktarma  
* Özel mantık kullanarak bir hücre aralığını dize olarak dışa aktarma  
* Excel formüllerini kod içinde hesaplama, Office‑365 EXPAND işlevi dahil  
* Tüm değişiklikler uygulanmış final çalışma kitabını kaydetme  

**Önkoşullar**  
* .NET 6.0 veya üzeri (kod .NET Framework 4.7.2+ ile de çalışır)  
* Aspose.Cells for .NET v25.11 veya daha yeni (`CopyPivotTable` seçeneği v25.11'de tanıtıldı)  
* C# ve Excel kavramları (aralıklar, pivot tablolar, formüller) hakkında temel bilgi  

> **Pro ipucu:** Projenizi en yeni özelliklerle güncel tutmak için Aspose.Cells'i NuGet üzerinden kurun (`Install-Package Aspose.Cells`).

## Excel'i PowerPoint'e Aktarma Aspose.Cells ile

İlk büyük görev, çalışma kitabını tüm görsel öğeleri düzenlenebilir tutarak bir PowerPoint sunumuna dönüştürmektir. Bu, finansal raporlar veya panolar üzerinden otomatik olarak slayt desteleri oluşturmak istediğinizde çok önemlidir.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Neden bu şekilde çalışır

* **`Workbook`** tüm Excel dosyasını belleğe yükler, size tam API erişimi sağlar.  
* **`CopyRange`** ile `CopyPivotTable = true` ayarı, pivot tablonun veri kaynağını, önbelleğini ve düzenini tam olarak kopyalar—eski Aspose.Cells sürümlerinin yapamadığı bir şey.  
* Yeni bir çalışma sayfası (`Copy`) eklemek, orijinal sayfayı dokunulmaz tutar; bu, denetim izleri için faydalıdır.  

## Çalışma kitabını düzenlenebilir nesnelerle PowerPoint'e Aktarma

Şimdi çalışma kitabını bir PowerPoint dosyasına dönüştürüyoruz. `ExportEditableObjects` özelliğini etkinleştirerek, her grafik, şekil veya metin kutusu, dışa aktarıldıktan sonra kullanıcıların doğrudan düzenleyebileceği yerel bir PowerPoint nesnesi haline gelir.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Açıklama

* **`WorkbookDesigner`** çalışma kitabını dışa aktarmaya hazırlayan yüksek seviyeli bir yardımcıdır; Smart Markers, adlandırılmış aralıklar ve düzen ayarlamalarıyla ilgilenir.  
* `ExportEditableObjects = true` ayarı, Aspose.Cells'in Excel çizimlerini resim olarak düzleştirmek yerine PowerPoint şekillerine dönüştürmesini sağlar. Bu, **tamamen düzenlenebilir** bir slayt destesi ortaya çıkarır.  

> **Köşe durumu:** Çalışma kitabınız dış veri bağlantılarından oluşturulmuş karmaşık grafikler içeriyorsa, `ExportToPptx` çağrısından önce bu bağlantıların çözülmüş olduğundan emin olun; aksi takdirde grafik boş görünebilir.

## Özel mantık kullanarak bir aralığı dize olarak dışa aktarma

Bazen sonraki işleme (ör. bir CSV ayrıştırıcıya besleme) için ham dize değerlerine ihtiyaç duyarsınız. `ExportTableOptions` sınıfı, her hücrenin nasıl dönüştürüleceğini kontrol etmenizi sağlar.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Neden bunu kullanabilirsiniz

* **Tek tip veri türü:** Dize olarak dışa aktarmak, tüketicinin metin beklediği durumlarda tip uyuşmazlığı hatalarını önler.  
* **Özel biçimlendirme:** `value.ToString()` ifadesini istediğiniz herhangi bir biçimlendiriciyle değiştirin (ör. tarih için `value.ToString("yyyy-MM-dd")`).  

## Excel formüllerini kod içinde hesaplama

Sık karşılaşılan bir gereksinim, **Excel formüllerini kod içinde hesaplamaktır**; Excel'i açmadan. Aspose.Cells, çevrimdışı çalışan ve en yeni Office‑365 işlevlerini (`EXPAND` dahil) destekleyen yerleşik bir hesaplama motoru sunar.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Hesaplama motoru nasıl çalışır

* `Formula` özelliği, ifadeyi Excel'de yazacağınız gibi tam olarak saklar.  
* `CalculateFormula()` tam bir çalışma kitabı yeniden hesaplamasını tetikler, hücreler arasındaki bağımlılıkları dikkate alır.  
* `EXPAND` işlevi (Excel 365'te mevcut) kaynak hücre (`B1`) ve belirtilen satır (`5`) ve sütun (`3`) sayısına göre bir dökülen aralık döndürür.  

> **İpucu:** Sadece çalışma kitabının bir alt kümesini hesaplamanız gerekiyorsa, kapsamı sınırlamak ve performansı artırmak için `Worksheet.CalculateFormula()` kullanın.

## Tüm değişiklikler uygulanmış şekilde çalışma kitabını kaydetme

Son olarak, değiştirilmiş çalışma kitabını diske yazın. Dosya uzantısını değiştirerek (`.xlsx`, `.xls`, `.csv` vb.) desteklenen herhangi bir formatta kaydedebilirsiniz.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Kontrol edilmesi gerekenler

* `result.xlsx` dosyasını Excel'de açarak pivot tablo kopyasını, `EXPAND` formül sonucunu ve özel dışa aktarılmış dizeleri doğrulayın.  
* `output.pptx` dosyasını PowerPoint'te açın; Excel düzenini yansıtan bir slayt görmeli ve tüm grafikler/metin kutuları düzenlenebilir olmalıdır.  

## Yaygın sorular ve sorun giderme

| Soru | Cevap |
|----------|--------|
| **Aspose.Cells kullanmak için lisansa ihtiyacım var mı?** | Evet. Değerlendirme için bir deneme sürümü çalışır, ancak tam lisans değerlendirme filigranlarını kaldırır ve `CopyPivotTable` özelliğinin kilidini açar. |
| **Dışa aktarılan PPTX boş şekiller gösteriyorsa ne yapmalıyım?** | Çalışma kitabının çizim nesnelerinin gizli olmadığını (`Visible = true`) ve dış görüntü bağlantılarının dışa aktarmadan önce gömülü olduğunu doğrulayın. |
| **Birden fazla çalışma sayfasını ayrı PPTX slaytlarına dışa aktarabilir miyim?** | Her çalışma sayfası için farklı bir `ExportOptions` belirterek bir döngü içinde `WorkbookDesigner.ExportToPptx` kullanın veya Aspose.Slides ile slaytları manuel olarak ekleyerek tek bir sunumda birleştirin. |
| **`CalculateFormula` çoklu iş parçacığında güvenli mi?** | Hayır. Hesaplamaları tek bir iş parçacığında yapın veya her iş parçacığı için çalışma kitabını klonlayarak yarış koşullarını önleyin. |

## Sonuç

Artık Aspose.Cells kullanarak **Excel'i PowerPoint'e tamamen uçtan uca aktarma** çözümüne sahipsiniz ve **kod içinde Excel formüllerini hesaplamayı**—modern `EXPAND` işlevi dahil—anladınız. Öğreticide bir çalışma kitabını yükleme, pivot tabloları kopyalama, düzenlenebilir PowerPoint'e dışa aktarma, özel dize dışa aktarımı, formül hesaplama ve son kaydetme adımları ele alındı.

Bundan sonra şunları yapabilirsiniz:

* Dışa aktarmayı, çalışma sayfası başına birden fazla slayt içerecek şekilde genişletin (ikincil anahtar kelime: *calculate Excel formulas in code* grafik verileri oluştururken yeniden kullanılabilir).  
* Animasyonlar veya ana slayt düzenleri eklemek için Aspose.Slides entegrasyonu yapın.  
* Basit `CustomExport` temsilcisini, uluslararası projeler için yerel duyarlı biçimlendirme ile değiştirin.  

Farklı aralıklarla denemeler yapmaktan, diğer Office‑365 işlevlerini (ör. `FILTER`, `SORT`) keşfetmekten ve bu iş akışını tam otomatik raporlama hatları için otomatik e‑posta gönderimiyle birleştirmekten çekinmeyin.

---


## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells for .NET ile Excel Veri Dışa Aktarımını Otomatikleştirme: Adım Adım Rehber](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel Grafiklerini PDF'ye Dışa Aktarma: Adım Adım Rehber](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET ile Excel Hücrelerini Görüntüye Dışa Aktarma: Adım Adım Rehber](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}