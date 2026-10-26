---
category: general
date: 2026-10-26
description: Tìm hiểu cách sử dụng WRAPCOLS trong C# để chia một phạm vi thành các
  cột, áp dụng WRAPROWS cho các hàng và lưu workbook dưới dạng XLSX một cách lập trình.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: vi
lastmod: 2026-10-26
og_description: Cách sử dụng WRAPCOLS trong C# để chia dữ liệu thành các cột, sử dụng
  WRAPROWS cho các hàng, và lưu workbook dưới dạng XLSX. Thực hiện theo hướng dẫn
  chi tiết từng bước.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Cách sử dụng WRAPCOLS trong C# – chia phạm vi và lưu dưới dạng XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cách sử dụng WRAPCOLS trong C# và lưu workbook dưới dạng XLSX
url: /vi/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng WRAPCOLS trong C# và lưu workbook dưới dạng XLSX

Nếu bạn cần **cách sử dụng WRAPCOLS** để tái tổ chức dữ liệu trong một tệp Excel, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, có thể chạy được. Bạn sẽ thấy một **ví dụ excel wrapcols**, học cách **chia phạm vi thành các hàng** bằng WRAPROWS, và kết thúc bằng **lưu workbook dưới dạng XLSX**—tất cả đều được thực hiện **bằng chương trình**.

Làm việc với Excel từ C# thường đồng nghĩa với việc tạo một workbook, áp dụng công thức, và lưu tệp. Đoạn mã dưới đây sử dụng thư viện Aspose.Cells, cho phép bạn thao tác các tệp Excel mà không cần cài đặt Microsoft Office. Khi kết thúc tutorial này, bạn sẽ có thể **tạo excel workbook bằng chương trình**, chia dữ liệu cả theo chiều ngang và chiều dọc, và tạo ra một tệp `.xlsx` sạch sẽ, sẵn sàng cho các quy trình xử lý tiếp theo.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.7+)
* Tham chiếu tới gói NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Kiến thức cơ bản về C# và công thức Excel

## Bước 1: Cách sử dụng WRAPCOLS để chia một phạm vi thành các cột

Hàm **WRAPCOLS** nhận một phạm vi một chiều và trải các giá trị của nó qua số cột được chỉ định. Trong ví dụ này, chúng ta bắt đầu với các giá trị trong `A1:A10` và yêu cầu WRAPCOLS tạo ba cột.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Kết quả:** Các ô `C1:E4` bây giờ chứa mười mục gốc được sắp xếp thành ba cột (cột cuối cùng giữ các mục còn lại).

![Ảnh chụp màn hình minh họa cách sử dụng WRAPCOLS để chia một phạm vi thành các cột trong Excel](image-url.png)

## Bước 2: Chia phạm vi thành các hàng với WRAPROWS

Trong khi **WRAPCOLS** hoạt động theo chiều ngang, **WRAPROWS** thực hiện ngược lại: nó trải một phạm vi qua một số hàng nhất định. Ở đây chúng ta lấy các giá trị từ `B1:B10` và sắp xếp chúng thành hai hàng bắt đầu tại `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Kết quả:** Công thức điền các ô `F1:K2` với mười giá trị được phân bố trên hai hàng.

## Bước 3: Lưu workbook dưới dạng XLSX

Sau khi áp dụng các công thức, bước cuối cùng là lưu tệp. Thao tác **save workbook as xlsx** ghi workbook đang ở trong bộ nhớ ra đĩa ở định dạng OpenXML hiện đại.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Hình dạng của tệp đã lưu

Khi bạn mở `wrapcols_wraprows_output.xlsx` trong Excel, bạn sẽ thấy:

| C | D | E |
|---|---|---|
| Mục 1 | Mục 4 | Mục 7 |
| Mục 2 | Mục 5 | Mục 8 |
| Mục 3 | Mục 6 | Mục 9 |
|        |        | Mục 10 |

và

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Giá trị 1 | Giá trị 3 | Giá trị 5 | Giá trị 7 | Giá trị 9 | |
| Giá trị 2 | Giá trị 4 | Giá trị 6 | Giá trị 8 | Giá trị 10 | |

Các công thức vẫn còn trong các ô, vì vậy bất kỳ thay đổi nào sau này đối với các phạm vi nguồn sẽ tự động được phản ánh.

## Bước 4: Các biến thể phổ biến và trường hợp đặc biệt

### Thay đổi số cột hoặc số hàng

* **Thêm cột:** Tăng đối số thứ hai của `WRAPCOLS`.  
  Ví dụ: `=WRAPCOLS(A1:A10,5)` tạo năm cột, để các ô trống khi dữ liệu hết.
* **Số cột động:** Sử dụng tham chiếu ô thay vì số cố định.  
  `=WRAPCOLS(A1:A10, G1)` trong đó `G1` chứa số cột mong muốn.

### Xử lý các ô trống hoặc không phải số

WRAPCOLS và WRAPROWS mặc định bỏ qua các ô trống, nhưng chúng giữ thứ tự của các giá trị không trống. Nếu bạn cần giữ lại các ô trống, hãy bao bọc phạm vi nguồn bằng các hàm `IFERROR` hoặc `TEXT` trước khi áp dụng WRAPCOLS.

### Lưu sang các định dạng khác

Mặc dù tutorial này tập trung vào **save workbook as xlsx**, Aspose.Cells hỗ trợ nhiều định dạng (`.xls`, `.csv`, `.pdf`, v.v.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Mẹo chuyên nghiệp và những lưu ý

* **Mẹo chuyên nghiệp:** Đặt `Workbook.Settings.CalcEngineEnabled = true` nếu bạn dự định tính toán các công thức ngay sau khi lưu.
* **Cẩn thận:** Các phạm vi nguồn lớn có thể tạo ra các khu vực tràn (spill) rất lớn, ảnh hưởng đến hiệu năng. Hạn chế kích thước phạm vi hoặc chia thao tác thành nhiều worksheet.
* **An toàn đa luồng:** Các đối tượng Aspose.Cells **không** an toàn cho đa luồng. Tạo một thể hiện `Workbook` riêng cho mỗi luồng nếu bạn xử lý tệp đồng thời.

## Kết luận

Bạn đã biết **cách sử dụng WRAPCOLS** để chia một phạm vi dọc thành nhiều cột, **cách chia phạm vi thành các hàng** bằng WRAPROWS, và **cách lưu workbook dưới dạng XLSX** sau khi thực hiện các chuyển đổi này. Bằng cách làm theo các bước trên, bạn có thể **tạo excel workbook bằng chương trình**, áp dụng các công thức tràn mạnh mẽ, và tạo ra các tệp Excel sẵn sàng chia sẻ mà không cần can thiệp thủ công.

### Tiếp theo là gì?

* Khám phá **định dạng có điều kiện** để làm nổi bật dữ liệu đã tràn.
* Kết hợp **WRAPCOLS** với **SORT** hoặc **FILTER** để xây dựng các bảng điều khiển động.
* Sử dụng **API vẽ biểu đồ** của Aspose.Cells để trực quan hoá dữ liệu đã sắp xếp ngay từ mã.

Chúc lập trình vui vẻ, và chúc bạn tự động hoá quy trình Excel một cách hiệu quả!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}