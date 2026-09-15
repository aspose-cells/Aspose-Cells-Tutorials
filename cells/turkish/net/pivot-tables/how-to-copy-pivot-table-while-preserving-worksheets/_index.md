---
category: general
date: 2026-09-15
description: Aspose.Cells kullanarak C#’ta pivot tabloyu kopyalamayı, pivotlu çalışma
  sayfasını kopyalamayı ve çalışma kitabını pptx olarak kaydetmeyi öğrenin. Tam adım
  adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: tr
lastmod: 2026-09-15
og_description: Aspose.Cells kullanarak özet tabloyu kopyalama, özet tablo içeren
  çalışma sayfasını kopyalama ve çalışma kitabını pptx olarak kaydetme. Tam, çalıştırılabilir
  C# örneklerini izleyin.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Pivot tabloyu kopyalama ve çalışma sayfalarını dışa aktarma – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Pivot tabloyu çalışma sayfalarını koruyarak nasıl kopyalarım?
url: /tr/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tabloyu kopyalarken çalışma sayfalarını koruma

Bir çalışma kitabından diğerine temel pivot önbelleğini kaybetmeden **how to copy pivot table** yapmanız gerekiyorsa, bu kılavuz hazır‑çalıştır çözüm sunar. Ayrıca **copy worksheet with pivot** ve **save workbook as pptx** işlemlerinin düzenlenebilir metin kutularını koruyarak nasıl yapılacağını göreceksiniz. Tüm örnekler en son Aspose.Cells for .NET kullanılarak hazırlanmıştır, böylece kodu herhangi bir C# projesine ekleyebilir ve anında sonuçları görebilirsiniz.

Excel dosyalarıyla programatik olarak çalışmak genellikle çalışma kitapları arasında veri taşıma, sunumlara dışa aktarma veya karmaşık Smart Marker'lar eklemeyi içerir. Aşağıdaki üç kod parçacığı bu yaygın senaryoları kapsar ve her adımın neden önemli olduğunu açıklar.

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm yüklü  
* Aspose.Cells for .NET (version 25.11 veya daha yeni) projenizde referans olarak eklenmiş  
* `YOUR_DIRECTORY` adlı bir klasör, örnek dosyaların okunup yazılacağı yer  

Ek bir NuGet paketi gerekmemektedir.

---

## Aspose.Cells ile pivot tabloyu kopyalama

Pivot tablo içeren bir aralığı, pivot önbelleğini koruyarak kopyalamak sık karşılaşılan bir gereksinimdir. Aşağıdaki adımlar, ihtiyacınız olan tam sıralamayı gösterir.

### Adım 1 – Pivot tabloyu içeren kaynak çalışma kitabını yükleyin

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Neden*: Aspose.Cells çalışma kitabını belleğe okur, böylece çalışma sayfalarına, hücrelere ve pivot tablolara erişim sağlar.

### Adım 2 – Boş bir hedef çalışma kitabı oluşturun

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Neden*: Boş bir çalışma kitabıyla başlamak, gizli stillerin veya adlandırılmış aralıkların kopyalama işleğine müdahale etmesini engeller.

### Adım 3 – Pivot tabloyu içeren satırları kopyalayın

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Neden*: `CopyRows` ham hücre değerlerini, biçimlendirmeleri ve temel pivot önbelleği referanslarını kopyalar. Aralık, tüm pivot tablo alanını içermelidir.

### Adım 4 – Pivot tabloyu içeren sütunları kopyalayın

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Neden*: Pivot tablolar hem satırları hem de sütunları kapsar; sütunları kopyalamak, tablo düzeninin tam olarak korunmasını sağlar.

### Adım 5 – Hazırlanan sayfayı hedef çalışma kitabına aktarın

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Neden*: `Copy` yöntemi, pivot önbelleği dahil çalışma sayfasını klonlar, böylece hedef çalışma kitabı aynı pivot tabloyu gösterir.

### Adım 6 – Sonucu kaydedin – pivot tablo bozulmadan kalır

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Neden*: Çalışma kitabını kalıcı hale getirmek, tüm iç yapıların kaydedilmesini sağlar ve pivotun daha sonra yenilenebileceğini garanti eder.

**Pro ipucu**: Kopyalama işleminden sonra, kaynak veri değiştiyse verileri güncellemek için `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` metodunu çağırabilirsiniz.

---

## Pivot ile çalışma sayfasını kopyalama – öz bir alternatif

Eğer zaten bir pivot tablo içeren bir çalışma sayfasını tamamen kopyalamanız gerekiyorsa, satır/sütun kopyalama adımlarını atlayabilir ve doğrudan çalışma sayfası düzeyindeki `Copy` metodunu kullanabilirsiniz.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Bu yaklaşım, çalışma sayfasının pivot alanının dışında ekstra veri içermediği durumlarda faydalıdır. **copy worksheet with pivot** işlemi tüm biçimlendirmeleri, adlandırılmış aralıkları ve pivot önbelleklerini otomatik olarak korur.

---

## Çalışma kitabını PPTX olarak düzenlenebilir metin kutuları ile kaydetme

Düzenlenebilir bir metin kutusu içeren bir Excel sayfasını PowerPoint'e dışa aktarmak, raporlama panoları için gerekli olabilir. Aşağıdaki kod, **save workbook as pptx** işlemini metin kutusunu düzenlenebilir tutarak gösterir.

### Adım 1 – Metin kutusunu içeren çalışma kitabını yükleyin

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Adım 2 – PPTX kaydetme seçeneklerini yapılandırın

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Neden*: `ExportEditableTextBox` ayarını yapmak, Aspose.Cells'in Excel metin kutusunu dışa aktarıldıktan sonra düzenlenebilir kalan bir PowerPoint şekline dönüştürmesini sağlar.

### Adım 3 – Çalışma kitabını PPTX olarak kaydedin

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Beklenen sonuç**: PowerPoint'te `Result.pptx` dosyasını açın, metin kutusunu seçin ve içeriğini yerel bir şekil gibi düzenleyin.

**Sık sorulan soru**: *Metin kutusunu kilitli tutmam gerekirse ne yapmalıyım?*  
`pptxOptions.ExportEditableTextBox = false` olarak ayarlayın; şekil bunun yerine statik bir görüntüye dönüştürülecektir.

---

## JSON dizisi içeren bir Smart Marker'ı tek hücre değeri olarak dışa aktarma

Smart Marker'lar, Excel şablonlarını karmaşık veri yapılarıyla doldurmanıza olanak tanır. Aşağıda, bir JSON dizisini tek bir hücreye eklerken **how to copy pivot table**‑stilinde veri işleme gösteren tam bir örnek bulunmaktadır.

### Adım 1 – SmartMarkerProcessor'ı hazırlayın

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Adım 2 – A1 hücresine bir Smart Marker ekleyin

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Adım 3 – JSON‑stilinde bir dizi ile veri kaynağını tanımlayın

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Adım 4 – Çalışma kitabını işleyin

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Adım 5 – Oluşan çalışma kitabını kaydedin

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Sonuç doğrulaması**: `JsonSingleCell.xlsx` dosyasını açın ve A1 hücresinin `A,B,C` okuduğunu doğrulayın. Bu, bir koleksiyonu tek bir hücre değeri olarak nasıl ele alacağınızı gösterir; bu desen, verileri alt sistemlere dışa aktarırken sıkça gereklidir.

---

## Tam çalışan örnek

Aşağıda, üç senaryoyu birleştiren tek bir program bulunmaktadır. Kodu bir konsol uygulamasına kopyalayabilir, dosya yollarını ayarlayabilir ve üç çıktıyı görmek için çalıştırabilirsiniz.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Running this program produces:

* `CopyWithPivot.xlsx` – orijinal pivot tablonun mükemmel bir kopyası.  
* `Result.pptx` – düzenlenebilir bir metin kutusu içeren bir PowerPoint slaytı.  
* `JsonSingleCell.xlsx` – JSON dizisinin tek bir hücrede göründüğü bir sayfa.

---

## Sonuç

Artık **how to copy pivot table** güvenli bir şekilde, **copy worksheet with pivot** tek bir çağrıyla ve **save workbook as pptx** düzenlenebilir metin kutularını koruyarak nasıl yapılacağını biliyorsunuz. Bu desenler, kurumsal otomasyon projelerinde karşılaşacağınız en yaygın Excel‑to‑PowerPoint ve Excel‑to‑JSON iş akışlarını kapsar.

Şimdi, aşağıdakileri keşfetmeyi düşünün:

* Kopyalanmış pivot tabloları programatik olarak yenileme (`PivotTable.Refresh()`)  
* PDF veya HTML gibi diğer formatlara dışa aktarma (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Özel fonksiyonlar veya koşullu biçimlendirme gibi gelişmiş Smart Marker seçeneklerini kullanma  

Farklı aralıklar, birden fazla çalışma sayfası veya daha büyük JSON yapılarıyla denemeler yapmaktan çekinmeyin. Aspose.Cells API size ayrıntılı kontrol sağlar, böylece bu örnekleri gerçek dünyadaki herhangi bir senaryoya uyarlayabilirsiniz. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Yeni Çalışma Kitabı Oluştur – Pivot Tablosu İçeren Çalışma Sayfasını Kopyalama](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [C# ile Pivot Tabloyu Kopyalama – Excel'i PPTX'e Dönüştürme, Aralık Kopyalama ve Metin Kutusu Oluşturma](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Aspose.Cells for .NET Kullanarak Çalışma Kitabı İçinde Sayfaları Kopyalama - Adım Adım Kılavuz](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}