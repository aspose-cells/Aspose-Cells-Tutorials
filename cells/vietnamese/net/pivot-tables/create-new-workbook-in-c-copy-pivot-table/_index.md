---
category: general
date: 2026-06-24
description: Tạo workbook mới trong C# và sao chép bảng pivot trong khi giữ nguyên
  dữ liệu của nó. Tìm hiểu cách sao chép các hàng, xuất phạm vi đã chọn và giữ nguyên
  bảng pivot.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: vi
og_description: Tạo workbook mới trong C# và sao chép bảng pivot trong khi giữ nguyên
  dữ liệu của nó. Hướng dẫn chi tiết từng bước về cách sao chép các hàng và xuất phạm
  vi đã chọn.
og_title: Tạo Workbook mới trong C# – Sao chép Pivot Table
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Tạo sổ làm việc mới trong C# – Sao chép bảng Pivot
url: /vi/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Mới trong C# – Sao chép Pivot Table

Bạn đã bao giờ cần **create new workbook** trong C# chỉ để di chuyển một phần dữ liệu bao gồm pivot table chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình báo cáo, bạn lấy một vài hàng, có thể một vài cột, và bạn mong muốn pivot vẫn giữ nguyên như trước—không có tham chiếu bị phá vỡ, không có công thức thiếu.

Tin tốt là gì? Chỉ với vài dòng code Aspose.Cells, bạn có thể **copy pivot table**, giữ nguyên nó, và thậm chí **export selected range** mà không làm hỏng gì. Dưới đây bạn sẽ thấy một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy **how to copy rows**, bảo tồn pivot, và lưu kết quả thành một workbook hoàn toàn mới.

## Nội Dung Hướng Dẫn

- Thiết lập dự án C# với Aspose.Cells (thư viện cung cấp sức mạnh cho mã).
- Tải workbook nguồn chứa pivot gốc.
- Sử dụng các phương thức `CopyRows` và `CopyColumns` của thư viện để sao chép chính xác vùng dữ liệu bạn cần.
- Lưu vùng đã sao chép vào kịch bản **create new workbook** trong khi pivot vẫn hoạt động.
- Mẹo cho các trường hợp đặc biệt như nhiều pivot table, hàng ẩn, và bộ dữ liệu lớn.

Khi hoàn thành hướng dẫn này, bạn sẽ có thể **export selected range** từ bất kỳ tệp Excel nào, giữ cho logic pivot vẫn hoạt động, và lưu tệp mới ở bất kỳ vị trí nào bạn muốn.

> **Prerequisite**: Aspose.Cells for .NET (bản dùng thử miễn phí hoặc bản có giấy phép) đã được cài đặt qua NuGet. Nếu bạn chưa thêm, chạy `dotnet add package Aspose.Cells` trong thư mục dự án của bạn.

---

## Tạo Workbook Mới và Sao chép Pivot Table

Dưới đây là phần cốt lõi của giải pháp. Chúng tôi sẽ đi qua từng dòng, giải thích lý do quan trọng, và sau đó hiển thị toàn bộ chương trình.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Tại Sao Cách Này Hoạt Động

- **`CopyRows` / `CopyColumns`**: Các phương thức này sao chép dữ liệu ô nền tảng *và* các đối tượng liên quan (như pivot cache). Đó là lý do pivot vẫn hoạt động sau khi di chuyển.
- **Workbook đích riêng biệt**: Bằng cách tạo một thể hiện `Workbook` mới, chúng ta **create new workbook** mà không có bất kỳ định dạng hay sheet ẩn nào có thể gây cản trở.
- **Chỉ mục bắt đầu từ 0**: Aspose.Cells sử dụng chỉ mục bắt đầu từ 0, vì vậy `0` trỏ tới ô **A1**. Điều chỉnh `startRow`/`startColumn` nếu pivot của bạn không nằm ở góc trên‑trái.
- **Bảo tồn pivot table**: Cache của pivot nằm trong cùng một vùng, vì vậy sao chép vùng sẽ tự động sao chép cache. Không cần mã bổ sung.

---

## Cách Sao chép Hàng mà Không làm Hỏng Pivot

Nếu bạn chỉ quan tâm đến phần sao chép hàng, bạn có thể tách riêng phần này:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Khi sao chép các hàng giao nhau với pivot table, luôn sao chép *toàn bộ* vùng pivot (hàng + cột). Sao chép một phần có thể để lại pivot thiếu trường, gây lỗi `#REF!`.

---

## Xuất Vùng Được Chọn – Kịch Bản Thực Tế

Hãy tưởng tượng bạn có một workbook bán hàng khổng lồ, nhưng khách hàng chỉ muốn bản tóm tắt quý đầu tiên, nằm trong các hàng 1‑20 và cột A‑D. Đoạn mã trên đã **export selected range** cho bạn. Chỉ cần thay đổi các biến `totalRows` và `totalColumns` để phù hợp với yêu cầu của khách hàng, và bạn đã xong.

### Xử Lý Hàng Ẩn hoặc Bộ Lọc

Nếu sheet nguồn có các hàng ẩn (có thể do bộ lọc), bạn có thể muốn sao chép chỉ các hàng *hiển thị*. Aspose.Cells cung cấp các overload của `CopyRows` hỗ trợ tính năng này:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Đặt tham số boolean cuối cùng thành `true` để sao chép chỉ các hàng hiển thị—hoàn hảo cho “export selected range” khi người dùng đã áp dụng bộ lọc.

---

## Bảo Tồn Pivot Table – Những Sai Lầm Thường Gặp & Cách Khắc Phục

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Pivot cache not copied** | Sử dụng `Range.Copy` thông thường thay vì `Cells.CopyRows/CopyColumns`. | Dùng các phương thức `Cells` như đã minh họa. |
| **Destination sheet has existing pivot** | Ghi đè lên một workbook đã chứa pivot có cùng tên. | Bắt đầu với một `Workbook()` mới (như chúng tôi đã làm). |
| **Named ranges break** | Pivot nguồn tham chiếu một named range không tồn tại trong tệp mới. | Sao chép cả named range: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivot trỏ tới nguồn dữ liệu bên ngoài không khả dụng. | Sử dụng `PivotTable.RefreshData()` sau khi sao chép nếu cần. |

---

## Ví Dụ Toàn Diện Từ Đầu Đến Cuối (Sẵn Sàng Chạy)

Dưới đây là chương trình hoàn chỉnh, bao gồm các chỉ thị `using` và một giao diện console ngắn gọn. Sao chép‑dán vào một dự án Console App mới và nhấn **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Kết quả mong đợi** (trong console):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Mở `copy-pivot.xlsx` và bạn sẽ thấy cùng một pivot table như trong `source.xlsx`, hoàn toàn hoạt động và tham chiếu tới vùng dữ liệu đã sao chép.

---

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với nhiều pivot table trên cùng một sheet không?**  
A: Có, miễn là hình chữ nhật sao chép bao phủ mọi pivot bạn cần. Nếu chỉ muốn một pivot, điều chỉnh `rows`/`cols` để cô lập nó.

**Q: Nếu workbook nguồn sử dụng kết nối dữ liệu bên ngoài thì sao?**  
A: Pivot cache vẫn sẽ trỏ tới kết nối gốc. Gọi `pivotTable.RefreshData()` sau khi tải workbook đích nếu bạn muốn truy vấn lại nguồn.

**Q: Tôi có thể sao chép pivot sang một sheet khác trong cùng workbook không?**  
A: Chắc chắn. Thay `destinationWorkbook` bằng `sourceWorkbook` và chọn chỉ số worksheet khác.

**Q: Có cách sao chép chỉ định dạng không?**  
A: Sử dụng các overload của `CopyRows`/`CopyColumns` nhận đối tượng `CopyOptions`—đặt `CopyOptions.CopyType = CopyType.ValuesOnly` hoặc `CopyType.All` tùy nhu cầu.

---

## Kết Luận

Chúng ta vừa đi qua một kịch bản **create new workbook** mà **copy pivot table**, **preserve pivot table**, và **export selected range**—tất cả bằng C# thuần.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}