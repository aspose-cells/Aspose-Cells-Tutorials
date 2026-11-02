---
category: general
date: 2026-10-10
description: Áp dụng định dạng số trong Excel nhanh chóng bằng cách nhập DataTable,
  thiết lập định dạng ngày và tiền tệ, và giữ nguyên hàng tiêu đề trong Excel trong
  một bước duy nhất.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: vi
lastmod: 2026-10-10
og_description: Áp dụng định dạng số trong Excel bằng C# sử dụng Aspose.Cells. Học
  cách đặt định dạng ngày trong Excel, đặt định dạng tiền tệ trong Excel và giữ nguyên
  hàng tiêu đề trong Excel khi nhập DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Áp dụng định dạng số Excel trong C# – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Cách áp dụng định dạng số trong Excel với Aspose.Cells
url: /vi/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách áp dụng định dạng số excel với Aspose.Cells

Nếu bạn cần **apply number format excel** khi tải dữ liệu từ một `DataTable`, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn cũng sẽ học cách **set date format excel**, **set currency format excel**, và **preserve header row excel** trong quá trình nhập, để bảng tính kết quả trông chuyên nghiệp mà không cần xử lý thêm.

Chúng tôi sẽ bao phủ mọi thứ từ cài đặt thư viện đến viết một đoạn mã hoàn chỉnh, có thể chạy được. Khi kết thúc, bạn sẽ có thể nhập bất kỳ `DataTable` nào vào một workbook Excel, tự động định dạng các cột số, và giữ nguyên hàng tiêu đề — tất cả chỉ trong vài dòng C#.

## Yêu cầu trước

* .NET 6.0 hoặc mới hơn (mã cũng hoạt động với .NET Framework 4.6+)
* Visual Studio 2022 (hoặc bất kỳ IDE C# nào bạn thích)
* **Aspose.Cells for .NET** – cài đặt qua NuGet:

```bash
dotnet add package Aspose.Cells
```

* Một nguồn `DataTable` – ví dụ sử dụng phương thức trợ giúp `GetTable()` trả về dữ liệu mẫu.

> **Mẹo:** Aspose.Cells là một thư viện thương mại, nhưng nó cung cấp chế độ đánh giá miễn phí cho phép tắt watermark trong tối đa 30 ngày.

## Bước 1: Tạo workbook và truy cập worksheet đầu tiên

Đối tượng workbook là điểm vào cho mọi thao tác Excel. Tạo một workbook mới sẽ cung cấp cho bạn một worksheet mặc định ở chỉ mục 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Why this step?*  
`Workbook` quản lý định dạng tệp, engine tính toán và kho lưu style. Truy cập `Worksheet` sớm cho phép chúng ta truyền sheet mục tiêu vào phương thức nhập sau này.

## Bước 2: Lấy dữ liệu nguồn dưới dạng DataTable

Trong các dự án thực tế, dữ liệu thường đến từ truy vấn cơ sở dữ liệu, trình phân tích CSV, hoặc phản hồi API. Để minh họa, chúng ta tạo một `DataTable` đơn giản với ba cột: **Product**, **Price**, và **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Why this step?*  
`DataTable` cung cấp một biểu diễn dạng bảng trong bộ nhớ mà Aspose.Cells có thể nhập trực tiếp, giữ nguyên thứ tự cột và kiểu dữ liệu.

## Bước 3: Chuẩn bị mảng `Style` – một style cho mỗi cột

Aspose.Cells cho phép bạn áp dụng một style riêng cho mỗi cột trong quá trình nhập bằng cách truyền một mảng các đối tượng `Style`. Độ dài mảng phải khớp với số cột trong bảng nguồn.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Why this step?*  
Nếu bạn bỏ qua việc tạo rõ ràng (`CreateStyle()`), việc cố gắng đặt `Number` sẽ gây ra `NullReferenceException`. Khởi tạo mỗi `Style` đảm bảo các gán giá trị sau này thành công.

## Bước 4: Gán định dạng số – tiền tệ và ngày

Excel xác định các định dạng số tích hợp sẵn bằng ID.  
* **14** – Tiền tệ (ví dụ, `$1,234.00`)  
* **22** – Ngày ngắn (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Lưu ý:** Nếu bạn cần một định dạng tùy chỉnh (ví dụ, `"¥#,##0.00"`), sử dụng `Style.Custom = "¥#,##0.00"` thay vì ID tích hợp sẵn.

*Why this step?*  
Áp dụng **number format** đúng lúc nhập dữ liệu loại bỏ nhu cầu thực hiện một lượt thứ hai để duyệt qua các ô và thay đổi định dạng. Nó cũng đảm bảo rằng **format excel cells date** và **set currency format excel** nhất quán trên tất cả các hàng.

## Bước 5: Nhập DataTable trong khi giữ nguyên hàng tiêu đề

Phương thức `ImportDataTable` có thể sao chép dữ liệu, giữ hàng đầu tiên làm tiêu đề, và áp dụng các style cột mà chúng ta đã chuẩn bị.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Kết quả mong đợi** – Mở `FormattedReport.xlsx` và bạn sẽ thấy:

| Sản phẩm | Giá (tiền tệ) | Ngày phát hành (ngày) |
|----------|---------------|-----------------------|
| Widget A | $12.99        | 05/01/2023            |
| Widget B | $23.50        | 06/15/2023            |
| Widget C | $7.75         | 07/30/2023            |

Hàng tiêu đề vẫn nguyên vẹn, cột **Price** hiển thị ký hiệu tiền tệ, và cột **ReleaseDate** hiển thị định dạng ngày ngắn — tất cả mà không cần bất kỳ mã định dạng bổ sung nào.

### Xử lý các trường hợp đặc biệt phổ biến

| Tình huống                               | Giải pháp |
|----------------------------------------|----------|
| **Nhiều cột hơn số style**           | Đảm bảo `columnStyles.Length` bằng `sourceTable.Columns.Count`. Các mục thiếu sẽ mặc định sử dụng style mặc định của workbook. |
| **Giá trị null trong các cột số**     | Excel coi `null` là ô trống; định dạng số vẫn được áp dụng khi giá trị được nhập sau này. |
| **Tiền tệ tùy chỉnh theo địa phương**    | Sử dụng `columnStyles[i].Custom = "\"€\"#,##0.00"` và đặt `columnStyles[i].Number = -1` để tắt ID tích hợp sẵn. |
| **Bảng lớn ( > 100 000 hàng )**    | Xem xét sử dụng overload `ImportDataTable` với `ImportTableOptions` để truyền dữ liệu dạng stream và giảm áp lực bộ nhớ. |
| **Áp dụng cùng một style cho nhiều cột** | Tái sử dụng cùng một instance `Style` trong mảng (ví dụ, `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Thêm: Sử dụng chuỗi định dạng tùy chỉnh

Nếu các ID tích hợp sẵn không đáp ứng nhu cầu của bạn, bạn có thể định nghĩa một định dạng số tùy chỉnh:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Cách tiếp cận này cho phép bạn kiểm soát hoàn toàn **format excel cells date** và **set currency format excel** vượt qua các ID đã định sẵn.

## Kết luận

Bây giờ bạn đã biết cách **apply number format excel** một cách hiệu quả khi nhập một `DataTable` bằng Aspose.Cells. Bằng cách tạo một mảng `Style` cho từng cột, gán các ID số tích hợp sẵn hoặc tùy chỉnh, và sử dụng overload `ImportDataTable` mà **preserve header row excel**, bạn có thể tạo các worksheet sẵn sàng xuất bản trong một thao tác duy nhất.

### Tiếp theo là gì?

* Khám phá **set date format excel** với các mẫu tùy chỉnh như `"dddd, mmmm dd, yyyy"`.
* Kết hợp kỹ thuật này với **conditional formatting** để làm nổi bật các giá trị ngoài phạm vi.
* Sử dụng **format excel cells date** trong các pivot table hoặc biểu đồ để báo cáo động.

Bạn có thể thoải mái thử nghiệm các ID số khác nhau hoặc chuỗi tùy chỉnh để phù hợp với hướng dẫn phong cách của tổ chức. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động được kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [áp dụng định dạng số excel – Hướng dẫn từng bước để định dạng các cột](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Tạo Excel Workbook C# – Áp dụng định dạng tiền tệ và nhập DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Đặt định dạng ngày trong Excel bằng C# – Hướng dẫn định dạng nhập đầy đủ](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}