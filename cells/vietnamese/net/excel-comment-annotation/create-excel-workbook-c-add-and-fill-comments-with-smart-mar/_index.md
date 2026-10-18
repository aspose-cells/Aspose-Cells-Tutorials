---
category: general
date: 2026-03-21
description: Tạo workbook Excel bằng C# và học cách thêm nhận xét vào Excel, tự động
  điền nhận xét bằng Smart Markers. Hướng dẫn chi tiết từng bước cho các nhà phát
  triển.
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: vi
og_description: Tạo workbook Excel bằng C# và nhanh chóng thêm bình luận vào Excel,
  sau đó điền bình luận bằng Smart Markers. Hướng dẫn đầy đủ kèm mã nguồn.
og_title: Tạo sổ làm việc Excel C# – Thêm và điền bình luận
tags:
- C#
- Excel automation
- Aspose.Cells
title: Tạo Workbook Excel bằng C# – Thêm và Điền bình luận với các đánh dấu thông
  minh
url: /vi/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Workbook Excel C# – Thêm và Điền Bình luận bằng Smart Markers

Bạn đã bao giờ cần **tạo workbook Excel C#** và tự hỏi làm thế nào để nhúng một bình luận tự động cập nhật không? Bạn không phải là người duy nhất. Trong nhiều trường hợp báo cáo, bạn muốn một bình luận ô có nội dung *“Created by Alice on 2024‑07‑15”* mà không phải mã cứng tên hoặc ngày mỗi lần.  

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn **cách thêm bình luận vào Excel**, sau đó **cách điền bình luận** bằng Smart Markers của Aspose.Cells. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, tạo workbook, chèn bình luận động và lưu tệp—tất cả trong vài bước ngắn gọn.

> **Bạn sẽ nhận được:** một ứng dụng console C# đầy đủ, có thể biên dịch, giải thích từng dòng code, mẹo tránh các lỗi thường gặp, và ý tưởng mở rộng giải pháp.

## Yêu cầu trước

- .NET 6.0 SDK hoặc mới hơn (code cũng hoạt động với .NET Core và .NET Framework)  
- Visual Studio 2022 hoặc bất kỳ IDE nào bạn thích  
- **Aspose.Cells for .NET** gói NuGet (`Install-Package Aspose.Cells`) – thư viện này cung cấp các lớp `Workbook`, `Worksheet` và `SmartMarkerProcessor` được sử dụng bên dưới.  
- Kiến thức cơ bản về cú pháp C# – nếu bạn đã viết `Console.WriteLine`, bạn đã sẵn sàng.

Bây giờ nền tảng đã sẵn sàng, chúng ta cùng bắt đầu.

![Ảnh chụp màn hình ví dụ tạo workbook Excel C#](excel-workbook.png "Ví dụ tạo workbook Excel C#")

## Bước 1: Khởi tạo Workbook mới – Kiến thức cơ bản về tạo workbook Excel C#

Đầu tiên chúng ta cần một đối tượng workbook sạch. Hãy nghĩ `Workbook` như một bảng vẽ trống; nếu không có nó, bạn không thể đặt ô, hàng hay bình luận nào.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**Tại sao lại quan trọng:** `Workbook` tự động tạo một worksheet mặc định, vì vậy bạn không cần gọi `Add` trừ khi muốn thêm các tab khác. Truy cập `Worksheets[0]` là cách nhanh nhất để bắt đầu điền dữ liệu.

## Bước 2: Chèn bình luận Smart Marker – Cách thêm bình luận với token

Tiếp theo chúng ta đặt một bình luận ở ô **B2** chứa các token Smart Marker (`«UserName»` và `«CreatedDate»`). Các token này sẽ được thay thế sau bằng giá trị thực.

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**Giải thích:**  
- `CreateComment()` tạo đối tượng bình luận nếu chưa tồn tại; nếu đã có thì trả về đối tượng hiện có.  
- Thuộc tính `Note` chứa văn bản hiển thị. Bằng cách bao quanh các placeholder bằng `« »` chúng ta báo cho Aspose.Cells biết chúng là **Smart Markers** – các placeholder có thể được thay thế đồng loạt.

> **Mẹo:** Nếu bạn cần bình luận đa dòng, dùng `\n` trong chuỗi, ví dụ `"Line1\nLine2"`.

## Bước 3: Chuẩn bị đối tượng dữ liệu – Cách điền bình luận một cách động

Smart Markers cần một nguồn dữ liệu. Trong C# cách đơn giản nhất là sử dụng kiểu ẩn danh (anonymous type) có các thuộc tính trùng với tên placeholder.

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**Tại sao lại dùng kiểu ẩn danh?**  
Nó nhẹ, không cần tạo file lớp riêng, và các tên thuộc tính (`UserName`, `CreatedDate`) khớp chính xác với tên token. Nếu bạn muốn mô hình có kiểu mạnh, chỉ cần tạo một lớp với các thuộc tính tương tự.

## Bước 4: Xử lý Smart Markers – Cách điền bình luận bằng đối tượng dữ liệu

Bây giờ phép màu xảy ra. `SmartMarkerProcessor` sẽ quét workbook tìm mọi token `«…»` và thay chúng bằng giá trị từ `markerData`.

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**Bên trong cơ chế:**  
`SmartMarkerProcessor` duyệt qua từng ô, bình luận, header, v.v., tìm mẫu `«Token»`. Khi phát hiện, nó dùng reflection để đọc thuộc tính tương ứng từ `markerData` và ghi giá trị trở lại. Không cần vòng lặp thủ công.

## Bước 5: Lưu Workbook – Điền bình luận Excel và lưu tệp

Cuối cùng chúng ta ghi workbook ra đĩa. Bình luận bây giờ sẽ hiển thị như *“Created by Alice on 03/21/2026 10:15 AM”*.

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Xác nhận kết quả:** Mở `CommentFilled.xlsx` trong Excel, di chuột lên ô **B2**, bạn sẽ thấy bình luận với tên người dùng và thời gian thực. Không cần thay đổi code nào cho các lần chạy tiếp theo—chỉ cần thay đổi giá trị trong `markerData`.

---

## Các biến thể thường gặp & Trường hợp đặc biệt

### Sử dụng định dạng ngày tùy chỉnh

Nếu muốn ngày ở định dạng `yyyy‑MM‑dd`, chỉnh sửa đối tượng dữ liệu:

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### Thêm nhiều bình luận

Bạn có thể lặp lại **Bước 2** cho các ô khác. Mỗi bình luận có thể có tập token riêng, hoặc chia sẻ cùng một tập nếu thông tin chung.

### Làm việc với Workbook đã tồn tại

Thay vì `new Workbook()`, tải một tệp hiện có:

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

Các bước còn lại giữ nguyên—Smart Markers hoạt động trên cả file mới và file đã có.

### Xử lý giá trị null

Nếu một token có thể thiếu, bao bọc thuộc tính trong kiểu nullable hoặc cung cấp giá trị dự phòng:

```csharp
UserName = user?.Name ?? "Unknown"
```

Bộ xử lý sẽ chèn *“Unknown”* khi nguồn dữ liệu là `null`.

---

## Ví dụ đầy đủ (Sẵn sàng sao chép‑dán)

Dưới đây là **toàn bộ chương trình** bạn có thể dán vào dự án console và chạy ngay (chỉ cần thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực).

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Chạy chương trình, mở file đã tạo, và bạn sẽ thấy bình luận động ở ô **B2**. Thật dễ dàng, phải không?

---

## Câu hỏi thường gặp (FAQ)

**Hỏi: Có hoạt động với .NET Framework 4.7 không?**  
Đáp: Hoàn toàn có. Aspose.Cells hỗ trợ .NET Framework 4.0+ và .NET Core/5/6/7. Chỉ cần tham chiếu DLL hoặc gói NuGet phù hợp.

**Hỏi: Tôi có thể dùng cách này cho kiểm tra dữ liệu hoặc định dạng có điều kiện không?**  
Đáp: Smart Markers chủ yếu dùng để chèn giá trị vào ô, bình luận, header và footer. Đối với định dạng có điều kiện, bạn vẫn cần dùng API `Style` thông thường.

**Hỏi: Nếu muốn thêm bình luận vào **worksheet** khác thì sao?**  
Đáp: Lấy worksheet mục tiêu (`workbook.Worksheets["MySheet"]`) và lặp lại **Bước 2** trên các ô của worksheet đó.

---

## Các bước tiếp theo & Chủ đề liên quan

- **Cách thêm bình luận vào Excel** một cách lập trình cho nhiều ô (vòng lặp qua một vùng).  
- **Điền bình luận Excel** từ dữ liệu cơ sở dữ liệu (sử dụng `DataTable` làm nguồn dữ liệu cho Smart Markers).  
- Khám phá **mảng Smart Marker** để tự động tạo bảng.  
- Tìm hiểu về **định dạng Aspose.Cells** để tùy chỉnh phông chữ, màu sắc và kích thước của bình luận.

Hãy thử các đoạn code, thay đổi nguồn dữ liệu, và bạn sẽ nhanh chóng thành thạo **cách điền bình luận** trong bất kỳ kịch bản tự động hoá Excel nào.

---

### Kết luận

Chúng ta vừa đi qua toàn bộ quy trình **tạo workbook Excel C#**, **thêm bình luận vào Excel**, và **điền bình luận Excel** bằng Smart Markers. Giải pháp ngắn gọn, tái sử dụng được và sẵn sàng cho môi trường production.  

Hãy thử, tùy chỉnh các placeholder, và để thư viện lo phần còn lại. Nếu gặp khó khăn, hãy để lại bình luận bên dưới—chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}