---
category: general
date: 2026-10-20
description: Sao chép bảng pivot sang sổ làm việc mới bằng Aspose.Cells và tìm hiểu
  cách xuất một hình dạng có thể chỉnh sửa sang PowerPoint trong một hướng dẫn duy
  nhất.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: vi
lastmod: 2026-10-20
og_description: Sao chép bảng pivot sang workbook mới bằng Aspose.Cells và xuất một
  shape có thể chỉnh sửa sang PowerPoint — mã từng bước bạn có thể chạy ngay hôm nay.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Sao chép bảng pivot sang sổ làm việc mới, xuất hình dạng sang PowerPoint
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
title: Sao chép bảng pivot sang sổ làm việc mới, xuất hình dạng sang PowerPoint
url: /vi/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sao chép bảng tổng hợp vào sổ làm việc mới, xuất hình dạng sang PowerPoint

Nếu bạn cần **copy pivot table to new workbook** trong khi giữ nguyên chức năng của nó, hướng dẫn này sẽ cho bạn thấy cách thực hiện chính xác với Aspose.Cells. Bạn cũng sẽ thấy cách nhanh nhất để **export an editable shape to PowerPoint**, để textbox vẫn có thể chỉnh sửa sau khi chuyển đổi.

Nhiều nhà phát triển cho rằng việc sao chép một vùng chứa bảng tổng hợp sẽ làm mất logic của pivot, hoặc các hình dạng sẽ trở thành hình ảnh tĩnh khi lưu dưới dạng PPTX. Bài hướng dẫn này bác bỏ những quan niệm sai lầm đó và cung cấp cho bạn một giải pháp đáng tin cậy, sẵn sàng cho môi trường sản xuất.

Trong các phần sau bạn sẽ:

* Tải một sổ làm việc nguồn và sao chép một vùng bao gồm bảng tổng hợp.
* Tạo một sổ làm việc đích chứa cùng một bảng tổng hợp.
* Thêm một hình dạng textbox, chỉnh sửa nội dung của nó, và lưu sổ làm việc dưới dạng bản trình bày PowerPoint mà textbox vẫn có thể chỉnh sửa.
* Hiểu tại sao mỗi lời gọi API cần thiết và cách tránh những cạm bẫy phổ biến.

**Prerequisites**

* .NET 6.0 hoặc phiên bản mới hơn (mã cũng hoạt động với .NET Framework 4.7+).
* Aspose.Cells for .NET đã được cài đặt (`Install-Package Aspose.Cells`).
* Kiến thức cơ bản về C# và Visual Studio (hoặc bất kỳ IDE nào bạn ưa thích).

---

## Sao chép bảng tổng hợp vào sổ làm việc mới

Phần hướng dẫn từng bước này minh họa cách sao chép một vùng chứa bảng tổng hợp và giữ lại định nghĩa pivot trong tệp mới.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` là điểm vào cho mọi thao tác Excel trong Aspose.Cells. Việc chọn đúng worksheet đảm bảo chúng ta làm việc với vị trí chính xác của bảng tổng hợp.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
Bảng tổng hợp nằm trong một khối ô cụ thể. Bằng cách chỉ định một `CellArea` bao trùm đầy đủ pivot, Aspose.Cells sẽ biết sao chép cả pivot cache ẩn bên dưới.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
Một workbook mới hoàn toàn đảm bảo không có các named range xung đột hay pivot đã tồn tại, giúp quá trình sao chép sạch sẽ.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` là một phần của **Aspose.Cells copy rows** API. Nó sao chép cả giá trị ô và pivot cache ẩn, vì vậy bảng tổng hợp vẫn hoạt động sau khi di chuyển.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Mở `CopyWithPivot.xlsx` trong Excel. Bảng tổng hợp xuất hiện chính xác như trong tệp nguồn, và bạn có thể làm mới hoặc chỉnh sửa nó một cách bình thường.

---

## Xuất hình dạng có thể chỉnh sửa sang PowerPoint

Bây giờ chúng ta sẽ thêm một hình dạng textbox, thay đổi nội dung của nó, và lưu workbook dưới dạng tệp PPTX. Hình dạng sẽ vẫn có thể chỉnh sửa hoàn toàn khi mở trong PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` tạo một **editable textbox in PowerPoint**‑compatible shape. Các tọa độ được tính bằng điểm; bạn có thể điều chỉnh chúng để phù hợp với bố cục của mình.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
Truy cập trực tiếp đối tượng `Shape` cho phép bạn thay đổi các thuộc tính như `Text`, `Font`, hoặc `Fill`. Bước này minh họa cách đặt nội dung ban đầu một cách lập trình.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Mở `Presentation.pptx` trong Microsoft PowerPoint. Textbox xuất hiện trên slide đầu tiên, và bạn có thể nhấp đúp vào để chỉnh sửa văn bản giống như bất kỳ hình dạng PowerPoint gốc nào.

## Kết quả mong đợi

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | Một worksheet chứa bảng tổng hợp gốc, hoàn toàn hoạt động (có thể làm mới). |
| `Presentation.pptx` | Một slide duy nhất với textbox có thể chỉnh sửa, hiển thị nội dung “Change me in PowerPoint”. |

---

## Những cạm bẫy thường gặp và mẹo thực hành tốt

* **Pivot cache loss** – Nếu bạn chỉ sao chép giá trị ô (ví dụ, sử dụng `CopyRows` với cờ `PasteOptions` được đặt thành `PasteValues`), pivot cache sẽ bị bỏ qua và bảng sẽ trở thành tĩnh. Luôn sử dụng overload mặc định của `CopyRows` như trong ví dụ.
* **Shape positioning** – `AddTextBox` sử dụng đơn vị điểm, không phải chỉ số ô Excel. Hãy thử nghiệm các tọa độ trên một tệp mẫu để tránh việc hình dạng bị đặt sai vị trí trên slide.
* **File format mismatch** – Lưu workbook dưới dạng PPTX với `SaveFormat.Pptx` sẽ tự động chuyển đổi tất cả các hình dạng được hỗ trợ. Cố gắng lưu dưới dạng `Pdf` sẽ raster hoá hình dạng, khiến chúng không thể chỉnh sửa được.

## Kết luận

Bạn giờ đã biết cách **copy pivot table to new workbook** và cách **export an editable shape to PowerPoint** bằng Aspose.Cells cho .NET. Các ví dụ mã đầy đủ, có thể chạy được, bao phủ mọi lời gọi API cần thiết, giải thích lý do mỗi bước quan trọng, và hiển thị kết quả mong đợi.

Tiếp theo, bạn có thể khám phá:

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`).
* **

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}