---
category: general
date: 2026-03-29
description: Tìm hiểu cách chèn hàng nhanh chóng trong GridJs. Hướng dẫn này cũng
  bao gồm cách thêm hàng và thêm nhiều hàng vào lưới bằng thao tác batch.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: vi
og_description: Tìm hiểu cách chèn hàng trong GridJs nhanh chóng. Hướng dẫn này chỉ
  cách thêm hàng, thêm nhiều hàng vào lưới và xử lý việc chèn hàng hàng loạt lớn.
og_title: Cách chèn hàng trong GridJs – Thêm nhiều hàng vào lưới một cách hiệu quả
tags:
- GridJs
- C#
- data‑grid
title: Cách chèn hàng trong GridJs – Thêm nhiều hàng vào Grid một cách hiệu quả
url: /vi/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chèn hàng trong GridJs – Thêm nhiều hàng vào lưới một cách hiệu quả

Bạn đã bao giờ tự hỏi **cách chèn hàng** vào một bảng GridJs khổng lồ mà không làm UI bị treo chưa? Có thể bạn đã gặp khó khăn khi **thêm hàng** từng cái một và hiệu năng nhanh chóng sụp đổ. Tin tốt là GridJs cung cấp một API batch cho phép bạn **thêm nhiều hàng vào lưới** trong một lần gọi, giữ cho mọi thứ luôn mượt mà ngay cả khi bạn phải xử lý hàng triệu mục dữ liệu.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy chính xác **cách chèn hàng** bằng `InsertRowsBatch`. Bạn sẽ hiểu vì sao việc batch quan trọng, cách kiểm chứng kết quả, và những lưu ý khi chỉ mục bạn muốn chèn rất lớn. Khi kết thúc, bạn sẽ tự tin thêm hàng nghìn bản ghi mới vào bất kỳ instance GridJs nào.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn đã có:

- .NET 6.0 trở lên (mã sẽ biên dịch với bất kỳ SDK mới nào)
- Tham chiếu tới gói NuGet `GridJs` (hoặc DLL nếu bạn dùng bản build tùy chỉnh)
- Kiến thức cơ bản về C# – không cần phải là chuyên gia, chỉ cần thoải mái với lớp và phương thức
- IDE hoặc trình soạn thảo mà bạn thích (Visual Studio, Rider, VS Code… đều được)

> **Mẹo chuyên nghiệp:** Nếu bạn dự định làm việc với các lưới thực sự khổng lồ (hàng chục triệu), bật `gridJs.EnableVirtualization = true;` để giảm tải việc render UI.

## Bước 1: Tạo và cấu hình đối tượng GridJs

Đầu tiên, bạn cần một đối tượng `GridJs` đang chạy. Hãy nghĩ nó như một canvas mà bạn sẽ vẽ các hàng lên.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Tại sao bước này quan trọng:** Khởi tạo lưới và (tùy chọn) nạp dữ liệu mẫu mô phỏng một kịch bản thực tế, nơi lưới đã chứa một lượng lớn thông tin. Việc batch insert chúng ta sẽ thực hiện sau phải tuân theo chỉ mục bắt đầu từ 0, vì vậy chúng ta tạo dữ liệu trước để minh họa điểm chèn chính xác.

## Bước 2: Sử dụng `InsertRowsBatch` để **thêm nhiều hàng vào lưới**

Đây là phần cốt lõi của tutorial – lời gọi thực sự **thêm hàng** hàng loạt. Chữ ký phương thức là `InsertRowsBatch(int startIndex, int count)`. Trong ví dụ, chúng ta sẽ bắt đầu tại chỉ mục 2 000 000 (tương ứng với hàng thứ 2 000 001) và thêm mười hàng.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Cách hoạt động:** `InsertRowsBatch` cấp phát số lượng hàng yêu cầu bên trong và đẩy các hàng hiện có xuống phía dưới. Vì thao tác được thực hiện trong một giao dịch duy nhất, UI chỉ được làm mới một lần, nên đây là cách được khuyến nghị để **thêm hàng** một cách hiệu quả.

## Bước 3: Xác minh việc chèn – Các hàng đã được chèn đúng vị trí chưa?

Sau khi batch hoàn thành, bạn sẽ muốn chắc chắn các hàng đã nằm ở nơi bạn mong đợi. Helper dưới đây đọc hàng đầu và cuối của khối mới thêm và in ra console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Kết quả mong đợi**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Các ô trống cho thấy các hàng là placeholder đang chờ dữ liệu. Bạn có thể điền dữ liệu cho chúng riêng lẻ hoặc thực hiện một batch update khác.

> **Lưu ý trường hợp biên:** Nếu `startIndex` vượt quá số hàng hiện tại, GridJs sẽ tự động thêm các hàng mới vào cuối. Ngược lại, một chỉ mục âm sẽ ném ra `ArgumentOutOfRangeException`, vì vậy luôn kiểm tra chỉ mục do người dùng cung cấp.

## Bước 4: Điền dữ liệu cho các hàng mới (Tùy chọn nhưng phổ biến)

Thường bạn không muốn chỉ có các hàng rỗng; bạn cần điền chúng bằng các giá trị có ý nghĩa. Bạn có thể lặp qua phạm vi vừa tạo và gọi `SetCell` hoặc API tương tự.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Bạn có thể gọi `PopulateNewRows(gridJs, startIndex, rowsToAdd);` ngay sau batch insert nếu muốn các hàng sẵn sàng hiển thị ngay lập tức.

## Bước 5: Mẹo hiệu năng cho lưới cực lớn

Khi bạn phải **thêm nhiều hàng vào lưới** lên tới hàng triệu, hãy nhớ những mẹo sau:

1. **Kích thước batch quan trọng** – Chèn 10 000 hàng một lần có thể nhanh hơn so với mười batch 1 000 hàng vì mỗi batch chỉ gây một lần refresh UI.
2. **Tắt cập nhật UI** – Một số phiên bản GridJs cung cấp `grid.SuspendLayout()` / `grid.ResumeLayout()`. Bao bọc batch của bạn bằng các lời gọi này nếu bạn cảm thấy chậm.
3. **Sử dụng virtualization** – Như đã đề cập, `EnableVirtualization` giảm đáng kể việc tiêu thụ bộ nhớ và thời gian render.
4. **Tránh sao chép sâu** – Truyền các kiểu giá trị đơn giản hoặc các đối tượng nhẹ vào lưới; các đối tượng nặng sẽ buộc lưới phải clone dữ liệu, làm giảm hiệu năng.

## Ví dụ đầy đủ hoạt động

Kết hợp mọi thứ lại, đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào một dự án console mới:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Chạy chương trình, bạn sẽ thấy output trên console xác nhận rằng mười hàng đã được chèn vào vị trí đúng và sau đó được điền dữ liệu.

## Kết luận

Chúng ta đã tìm hiểu **cách chèn hàng** trong GridJs bằng API batch, trình bày **cách thêm hàng** một cách hiệu quả, và khám phá cách **thêm nhiều hàng vào lưới** mà không làm UI bị nghẽn. Những điểm chính cần ghi nhớ:

- Sử dụng `InsertRowsBatch(startIndex, count)` cho bất kỳ thao tác bulk nào.
- Kiểm tra chỉ mục và cân nhắc bật virtualization cho các bộ dữ liệu khổng lồ.
- Điền dữ liệu cho các hàng sau batch nếu cần nội dung ngay lập tức.

Tiếp theo, bạn có thể khám phá **cách xóa hàng**, triển khai **undo/redo** cho các batch edit, hoặc tích hợp GridJs với dịch vụ back‑end truyền dữ liệu theo yêu cầu. Tất cả các chủ đề này dựa trên những khái niệm bạn vừa học.

Hãy thoải mái thử nghiệm—thay đổi kích thước batch, chèn ở đầu lưới, hoặc kết hợp nhiều batch trong một giao dịch. Càng thực hành, bạn sẽ càng tự tin với các lưới lớn.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}