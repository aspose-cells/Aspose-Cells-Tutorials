---
category: general
date: 2026-10-20
description: Aspose.Cells kullanarak özet tabloyu yeni bir çalışma kitabına kopyalayın
  ve tek bir rehberde düzenlenebilir bir şekli PowerPoint'e nasıl dışa aktaracağınızı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: tr
lastmod: 2026-10-20
og_description: Aspose.Cells kullanarak pivot tabloyu yeni bir çalışma kitabına kopyalayın
  ve düzenlenebilir bir şekli PowerPoint'e dışa aktarın—bugün çalıştırabileceğiniz
  adım adım kod.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Özet tabloyu yeni çalışma kitabına kopyala, şekli PowerPoint'e aktar
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Pivot tabloyu yeni çalışma kitabına kopyala, şekli PowerPoint'e dışa aktar
url: /tr/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tabloyu yeni çalışma kitabına kopyala, şekli PowerPoint'e dışa aktar

Pivot tabloyu işlevselliğini koruyarak **copy pivot table to new workbook** yapmanız gerekiyorsa, bu kılavuz Aspose.Cells ile bunu tam olarak nasıl yapacağınızı gösterir. Ayrıca **export an editable shape to PowerPoint**'in en hızlı yolunu da göreceksiniz, böylece metin kutusu dönüşümden sonra düzenlenebilir kalır.

Birçok geliştirici, pivot tablo içeren bir aralığı kopyalamanın pivot mantığını kaybedeceğini ya da şekillerin PPTX olarak kaydedildiğinde statik görüntülere dönüşeceğini varsayar. Bu öğretici bu mitleri çürütür ve size güvenilir, üretim‑hazır bir çözüm sunar.

Aşağıdaki bölümlerde şunları yapacaksınız:

* Kaynak bir çalışma kitabını yükleyin ve pivot tablo içeren bir aralığı kopyalayın.
* Aynı pivot tabloyu içeren bir hedef çalışma kitabı oluşturun.
* Bir metin kutusu şekli ekleyin, metnini değiştirin ve çalışma kitabını metin kutusunun düzenlenebilir kaldığı bir PowerPoint sunumu olarak kaydedin.
* Her API çağrısının neden gerekli olduğunu ve yaygın tuzaklardan nasıl kaçınılacağını anlayın.

**Prerequisites**

* .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).
* Aspose.Cells for .NET yüklü (`Install-Package Aspose.Cells`).
* C# ve Visual Studio (veya tercih ettiğiniz herhangi bir IDE) hakkında temel bilgi.

---

## Pivot tabloyu yeni çalışma kitabına kopyala

Bu adım‑adım bölümü, pivot tablo içeren bir aralığı nasıl kopyalayacağınızı ve yeni dosyada pivot tanımını koruyacağınızı gösterir.

### Adım 1 – Kaynak çalışma kitabını yükleyin ve ilk çalışma sayfasını seçin

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook`, Aspose.Cells içinde herhangi bir Excel işlemi için giriş noktasıdır. Doğru çalışma sayfasını seçmek, tam olarak pivot tablo konumuyla çalıştığımızı garanti eder.

### Adım 2 – Pivot tabloyu içeren hücre alanını tanımlayın

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
Pivot tablo belirli bir hücre bloğu içinde bulunur. Pivotu tamamen kapsayan bir `CellArea` belirleyerek, Aspose.Cells altındaki pivot önbelleğini de kopyalayacağını bilir.

### Adım 3 – Hedef çalışma kitabını oluşturun ve ilk çalışma sayfasını alın

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
Yeni bir çalışma kitabı, çakışan adlandırılmış aralıklar veya mevcut pivotların olmamasını sağlar ve kopyalama işlemini sorunsuz hâle getirir.

### Adım 4 – Kaynak alandan hedef sayfaya satırları kopyalayın

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows`, **Aspose.Cells copy rows** API'sinin bir parçasıdır. Hücre değerlerini ve gizli pivot önbelleğini birlikte kopyalar, böylece pivot tablo taşıma sonrası işlevsel kalır.

### Adım 5 – Yeni çalışma kitabını kaydedin

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
`CopyWithPivot.xlsx` dosyasını Excel'de açın. Pivot tablo, kaynak dosyadaki gibi tam olarak görünür ve normal şekilde yenileyebilir veya değiştirebilirsiniz.

---

## Düzenlenebilir şekli PowerPoint'e dışa aktar

Şimdi bir metin kutusu şekli ekleyecek, içeriğini değiştirecek ve çalışma kitabını PPTX dosyası olarak kaydedeceğiz. Şekil PowerPoint'te açıldığında tamamen düzenlenebilir kalır.

### Adım 1 – Yeni bir çalışma kitabı oluşturun ve ilk çalışma sayfasına erişin

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Adım 2 – Çalışma sayfasına bir metin kutusu şekli ekleyin

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox`, **PowerPoint** uyumlu **düzenlenebilir metin kutusu** şekli oluşturur. Koordinatlar puan (point) cinsindendir; düzeninize uyması için ayarlayın.

### Adım 3 – Şekli alın ve metnini değiştirin

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
`Shape` nesnesine doğrudan erişmek, `Text`, `Font` veya `Fill` gibi özellikleri değiştirmenizi sağlar. Bu adım, başlangıç içeriğini programlı olarak nasıl ayarlayacağınızı gösterir.

### Adım 4 – Çalışma kitabını PowerPoint sunumu olarak kaydedin

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
`Presentation.pptx` dosyasını Microsoft PowerPoint'te açın. Metin kutusu ilk slaytta görünür ve herhangi bir yerel PowerPoint şekli gibi metni düzenlemek için çift‑tıklayabilirsiniz.

## Beklenen çıktı

| Dosya | Ne göreceksiniz |
|------|-----------------|
| `CopyWithPivot.xlsx` | Orijinal pivot tabloyu içeren bir çalışma sayfası, tamamen işlevsel (yenileme çalışır). |
| `Presentation.pptx` | “Change me in PowerPoint” yazan düzenlenebilir bir metin kutusu içeren tek bir slayt. |

## Yaygın tuzaklar ve en iyi uygulama ipuçları

* **Pivot önbellek kaybı** – Yalnızca hücre değerlerini kopyalarsanız (ör. `CopyRows` ile `PasteOptions` bayrağı `PasteValues` olarak ayarlanmış), pivot önbelleği atlanır ve tablo statik hâle gelir. Her zaman gösterildiği gibi varsayılan `CopyRows` aşırı yüklemesini kullanın.
* **Şekil konumlandırma** – `AddTextBox` nokta birimlerini kullanır, Excel hücre indekslerini değil. Kaydırma dışı konumlamayı önlemek için koordinatları örnek bir dosyada test edin.
* **Dosya formatı uyumsuzluğu** – Çalışma kitabını `SaveFormat.Pptx` ile PPTX olarak kaydetmek, desteklenen tüm şekilleri otomatik olarak dönüştürür. `Pdf` olarak kaydetmeye çalışmak şekli rasterleştirir ve düzenlenemez hâle getirir.

## Sonuç

Artık Aspose.Cells for .NET kullanarak **copy pivot table to new workbook** ve **export an editable shape to PowerPoint** işlemlerinin nasıl yapılacağını biliyorsunuz. Tam, çalıştırılabilir kod örnekleri gerekli tüm API çağrılarını kapsar, her adımın neden önemli olduğunu açıklar ve beklenen sonuçları gösterir.

Sonraki adımda şunları keşfedebilirsiniz:

* **Grafiklerle çalışma** – pivot tablolarla birlikte grafikleri kopyalama (`Aspose.Cells copy rows between worksheets`).
* 

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım‑adım açıklamalar içeren tam çalışan kod örnekleri içerir.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}