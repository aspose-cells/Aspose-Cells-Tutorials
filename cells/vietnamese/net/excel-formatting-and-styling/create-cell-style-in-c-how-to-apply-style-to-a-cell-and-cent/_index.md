---
category: general
date: 2026-02-21
description: Tạo kiểu ô trong C# nhanh chóng. Tìm hiểu cách áp dụng kiểu cho ô, căn
  giữa văn bản trong ô, thiết lập căn chỉnh ô và làm chủ định dạng ô.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: vi
og_description: Tạo kiểu ô trong C# và học cách áp dụng kiểu cho ô, căn giữa văn bản
  trong ô, và thiết lập căn chỉnh ô với hướng dẫn rõ ràng, từng bước.
og_title: Tạo kiểu ô trong C# – Áp dụng kiểu cho ô và căn giữa văn bản
tags:
- C#
- Aspose.Cells
- Excel automation
title: Tạo kiểu ô trong C# – Cách áp dụng kiểu cho ô và căn giữa văn bản
url: /vi/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo kiểu ô trong C# – Hướng dẫn đầy đủ về áp dụng kiểu và căn giữa văn bản

Bạn đã bao giờ cần **tạo kiểu ô** trong một bảng tính Excel nhưng không biết bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Trong nhiều dự án tự động hoá, khả năng **áp dụng kiểu cho ô** là sự khác biệt giữa một bảng tính nhạt nhẽo và một báo cáo được hoàn thiện.  

Trong tutorial này, chúng ta sẽ đi qua một ví dụ đầy đủ, có thể chạy được, cho thấy **cách căn giữa văn bản** trong ô, thiết lập căn chỉnh và thêm viền mỏng—tất cả chỉ trong vài dòng C#. Khi kết thúc, bạn sẽ hiểu rõ tại sao mỗi phần lại quan trọng và cách tùy chỉnh chúng cho các kịch bản của riêng mình.

## Những gì bạn sẽ thu được

- Hiểu rõ quy trình **tạo kiểu ô** bằng Aspose.Cells (hoặc bất kỳ thư viện tương tự nào).
- Đoạn mã chính xác mà bạn có thể sao chép‑dán vào một ứng dụng console để **áp dụng kiểu cho ô**.
- Kiến thức về **căn giữa văn bản trong ô**, **đặt căn chỉnh ô**, và xử lý các trường hợp đặc biệt như ô hợp nhất hoặc định dạng số tùy chỉnh.
- Mẹo mở rộng kiểu—phông chữ khác, màu nền, hoặc định dạng có điều kiện.

> **Điều kiện tiên quyết:** Visual Studio 2022 (hoặc bất kỳ IDE C# nào) và gói NuGet Aspose.Cells for .NET. Không cần phụ thuộc nào khác.

---

## Bước 1: Thiết lập dự án và nhập không gian tên

Trước khi chúng ta có thể **tạo kiểu ô**, chúng ta cần một dự án tham chiếu tới thư viện Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Lý do quan trọng:* Nhập `Aspose.Cells` cho phép chúng ta truy cập các lớp `Workbook`, `Worksheet`, `Style` và `Border`. Nếu bạn dùng thư viện khác (ví dụ EPPlus), tên lớp sẽ thay đổi nhưng khái niệm vẫn giống nhau.

---

## Bước 2: Tạo Workbook và lấy ô đầu tiên

Bây giờ chúng ta **tạo kiểu ô** bằng cách lấy tham chiếu tới ô muốn định dạng.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Lưu ý chúng ta dùng `Cell` thay vì `var` chung—việc khai báo kiểu rõ ràng giúp code dễ hiểu hơn cho người mới. Lệnh `PutValue` ghi một chuỗi để chúng ta có thể thấy hiệu ứng kiểu sau này.

---

## Bước 3: Định nghĩa kiểu – Căn giữa văn bản, Thêm viền mỏng

Đây là phần cốt lõi của thao tác **tạo kiểu ô**. Chúng ta sẽ đặt căn chỉnh ngang, viền mỏng và một vài tùy chọn phụ.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Tại sao chúng ta làm như vậy:*  
- **HorizontalAlignment** và **VerticalAlignment** cùng trả lời câu hỏi “**cách căn giữa văn bản** trong ô?”  
- Thêm bốn viền đảm bảo ô trông như một nhãn có khung, hữu ích cho tiêu đề.  
- Màu nền không bắt buộc, nhưng nó minh họa cách bạn có thể mở rộng kiểu sau này.

---

## Bước 4: Áp dụng kiểu đã định nghĩa cho ô đã chọn

Khi kiểu đã tồn tại, chúng ta **áp dụng kiểu cho ô** bằng một lời gọi phương thức duy nhất.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Xong rồi—Aspose.Cells sẽ sao chép kiểu vào bộ sưu tập kiểu nội bộ của ô. Nếu bạn cần cùng một định dạng cho một phạm vi, có thể dùng `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Bước 5: Lưu Workbook và kiểm tra kết quả

Một lần lưu nhanh sẽ cho phép bạn mở file trong Excel và xác nhận rằng văn bản thực sự được căn giữa và viền hiển thị.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Kết quả mong đợi:* Khi mở **StyledCell.xlsx**, ô **A1** chứa “Hello, styled world!” được căn giữa cả chiều ngang và chiều dọc, bao quanh bởi viền mỏng màu xám, và nền màu xám nhạt.

---

## Các biến thể phổ biến & Trường hợp đặc biệt

### 1. Căn giữa văn bản trong vùng hợp nhất

Nếu bạn hợp nhất các ô **A1:C1** và vẫn muốn văn bản được căn giữa, bạn phải áp dụng kiểu cho ô trên‑trái **sau** khi hợp nhất:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Sử dụng định dạng số

Đôi khi bạn cần **đặt căn chỉnh ô** *và* hiển thị số với định dạng cụ thể:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Căn chỉnh vẫn được giữ ở vị trí trung tâm trong khi số hiển thị dưới dạng `12,345.68`.

### 3. Tái sử dụng kiểu một cách hiệu quả

Tạo một `Style` mới cho mỗi ô có thể làm giảm hiệu năng. Thay vào đó, tạo một đối tượng kiểu duy nhất và tái sử dụng cho nhiều ô hoặc phạm vi. Lớp `StyleFlag` cho phép bạn chỉ áp dụng những phần cần thiết, tiết kiệm bộ nhớ.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Mẹo chuyên nghiệp & Những lỗi cần tránh

- **Đừng quên căn chỉnh dọc** – chỉ căn giữa ngang thường trông không đồng đều, đặc biệt với các hàng cao.
- **Kiểu viền**: `CellBorderType.Thin` phù hợp cho hầu hết báo cáo, nhưng bạn có thể chuyển sang `Medium` hoặc `Dashed` để tạo phân cấp trực quan.
- **Xử lý màu**: Khi nhắm tới .NET Core, sử dụng `System.Drawing.Color` từ gói `System.Drawing.Common`; nếu không sẽ gặp lỗi thời gian chạy.
- **Định dạng lưu**: Nếu cần tương thích với các phiên bản Excel cũ, đổi `SaveFormat.Xlsx` thành `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: ảnh chụp màn hình cho thấy một ô với văn bản được căn giữa và viền mỏng được tạo bởi tutorial tạo kiểu ô.*

---

## Ví dụ đầy đủ (Sẵn sàng sao chép‑dán)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Chạy chương trình này, mở **StyledCell.xlsx**, và bạn sẽ thấy kết quả chính xác như mô tả ở trên. Tự do thay đổi văn bản, kiểu viền, hoặc màu nền để phù hợp với thương hiệu của bạn.

---

## Kết luận

Chúng ta vừa **tạo kiểu ô** từ đầu, **áp dụng kiểu cho ô**, và minh họa **cách căn giữa văn bản** cả chiều ngang và chiều dọc. Khi nắm vững những khối xây dựng này, bạn có thể định dạng tiêu đề, làm nổi bật tổng cộng, hoặc xây dựng toàn bộ mẫu báo cáo mà không cần rời khỏi C#.  

Nếu bạn muốn khám phá các bước tiếp theo, hãy thử:

- **Áp dụng cùng một kiểu cho toàn bộ hàng** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Thêm định dạng có điều kiện** để thay đổi nền dựa trên giá trị ô.
- **Xuất ra PDF** trong khi giữ nguyên kiểu.

Nhớ rằng, việc tạo kiểu không chỉ về mặt thẩm mỹ mà còn về khả năng đọc hiểu. Hãy thử nghiệm, lặp lại, và sớm thôi các bảng tính của bạn sẽ trông chuyên nghiệp như code của bạn.

*Chúc lập trình vui vẻ!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}