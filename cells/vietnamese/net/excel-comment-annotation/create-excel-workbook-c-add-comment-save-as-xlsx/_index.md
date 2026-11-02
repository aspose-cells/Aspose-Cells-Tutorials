---
category: general
date: 2026-03-18
description: Tạo workbook Excel bằng C# có bình luận và lưu workbook dưới dạng XLSX.
  Tìm hiểu cách thêm bình luận, tạo bình luận trong Excel và tự động hoá các tệp Excel.
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: vi
og_description: Tạo workbook Excel bằng C# với một chú thích và lưu workbook dưới
  dạng XLSX. Hãy làm theo hướng dẫn từng bước này để thêm chú thích Excel và tạo chú
  thích Excel một cách lập trình.
og_title: Tạo Workbook Excel bằng C# – Thêm bình luận và lưu dưới dạng XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Tạo Workbook Excel bằng C# – Thêm bình luận và lưu dưới dạng XLSX
url: /vi/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel Workbook C# – Thêm Ghi chú & Lưu dưới dạng XLSX

Bạn đã bao giờ cần **tạo Excel workbook C#** và dán một ghi chú vào trong một ô, nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất—các nhà phát triển luôn hỏi *cách thêm comment* mà không cần mở Excel thủ công.  

Trong hướng dẫn này, bạn sẽ nhận được một giải pháp hoàn chỉnh, sẵn sàng chạy, cho thấy **cách thêm excel comment**, **tạo excel comment** bằng Smart Marker, và **lưu workbook dưới dạng xlsx** trong một quy trình liền mạch. Không có tham chiếu lơ lửng, chỉ có mã thuần túy mà bạn có thể dán vào Visual Studio và xem nó hoạt động.

## Những Điều Bạn Sẽ Học

- Khởi tạo một Excel workbook từ đầu bằng C#.
- Chèn một Smart Marker chuyển thành một Excel comment.
- Cung cấp dữ liệu JSON để biến marker thành một ghi chú thực tế.
- Lưu file dưới dạng workbook `.xlsx`.
- Các cách tiếp cận tùy chọn để thêm comment mà không dùng Smart Markers.

### Yêu cầu trước

- .NET 6 (hoặc .NET Framework 4.7+).  
- Gói NuGet **Aspose.Cells for .NET** – thư viện cung cấp tính năng Smart Marker.  
- Môi trường phát triển C# cơ bản (Visual Studio, VS Code, Rider…).

> **Mẹo:** Nếu bạn có ngân sách hạn hẹp, Aspose cung cấp bản dùng thử miễn phí, đầy đủ chức năng cho việc phát triển và kiểm thử.

---

## Bước 1: Tạo Excel Workbook C# – Thiết lập Dự án

Đầu tiên, hãy tạo một ứng dụng console mới và thêm gói Aspose.Cells.

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

Bây giờ mở `Program.cs`. Điều đầu tiên chúng ta làm là **tạo một workbook mới**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Tại sao bắt đầu với một workbook mới hoàn toàn? Nó đảm bảo một khởi đầu sạch sẽ, loại bỏ định dạng ẩn, và cho phép bạn kiểm soát mọi thứ từ đầu—hoàn hảo cho việc tạo báo cáo tự động.

---

## Bước 2: Cách Thêm Comment – Sử dụng Smart Marker

Smart Markers là các placeholder mà Aspose thay thế bằng dữ liệu tại thời gian chạy. Bằng cách nhúng một marker theo mẫu **`${Comment:UserComment}`**, chúng ta chỉ cho engine chuyển placeholder thành một comment thực tế.

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

Bạn có để ý tiền tố `Comment:` không? Đó là dấu hiệu cho bộ xử lý coi giá trị là một comment thay vì văn bản thường. Nếu bạn thắc mắc *“có hoạt động với các loại ô khác không?”*—có, bạn có thể áp dụng cùng marker cho bất kỳ ô nào, kể cả các vùng hợp nhất.

---

## Bước 3: Chuẩn bị Dữ liệu JSON – Nội dung của Comment

Phần tiếp theo là nguồn dữ liệu. Ở đây chúng ta dùng một chuỗi JSON đơn giản, nhưng bạn cũng có thể cung cấp một DataTable, List, hoặc thậm chí một đối tượng tùy chỉnh.

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

Bạn có thể thay `"Reviewed by QA"` bằng bất kỳ giá trị động nào—có thể là dấu thời gian, tên người dùng, hoặc liên kết tới hệ thống theo dõi lỗi. Tên khóa (`UserComment`) phải khớp với định danh của marker.

---

## Bước 4: Tạo Excel Comment – Xử lý Smart Marker

Bây giờ chúng ta đưa JSON cho bộ xử lý Smart Marker. Đây là thời điểm **generate excel comment** thực sự diễn ra.

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

Trong hậu trường, Aspose phân tích JSON, tìm trường `UserComment`, và chèn nó như một comment gắn vào ô **B2**. Giá trị hiển thị của ô vẫn là văn bản placeholder gốc, nhưng Excel sẽ hiển thị comment khi bạn di chuột qua.

---

## Bước 5: Lưu Workbook dưới dạng XLSX – Lưu Kết quả

Cuối cùng, chúng ta ghi workbook ra đĩa. Điều này đáp ứng yêu cầu **save workbook as xlsx**.

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Mở `output.xlsx` trong Excel, di chuột qua ô **B2**, và bạn sẽ thấy comment *“Reviewed by QA”* xuất hiện. Thế là xong—không có bước thủ công, không có COM interop, chỉ C# thuần.

---

## Thay thế: Cách Thêm Comment mà Không Dùng Smart Markers

Nếu bạn thích cách tiếp cận trực tiếp hơn, bạn có thể tự tạo một đối tượng comment:

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

Phương pháp này hữu ích khi nội dung comment đã biết tại thời điểm biên dịch, hoặc khi bạn cần đặt các thuộc tính bổ sung như tác giả, độ rộng, hoặc chiều cao. Tuy nhiên, **generate excel comment** bằng Smart Markers tỏa sáng khi bạn có kịch bản dựa trên dữ liệu với nhiều hàng và cột.

---

## Mẹo Chuyên Gia & Những Cạm Bẫy Thường Gặp

| Tình huống | Điều cần chú ý | Giải pháp đề xuất |
|-----------|-------------------|-----------------|
| Dữ liệu lớn (hơn 10k dòng) | Xử lý Smart Marker có thể tốn nhiều bộ nhớ | Sử dụng overload `SmartMarkerProcessor.Process` cho phép stream dữ liệu, hoặc chia workbook thành các phần |
| Cần tên tác giả tùy chỉnh | Tác giả mặc định để trống | `comment.Author = "MyApp";` sau khi tạo comment |
| Muốn comment hiển thị mặc định | Excel ẩn comment cho đến khi di chuột | Đặt `comment.Visible = true;` |
| Làm việc với phiên bản Excel cũ | `.xlsx` có thể không được hỗ trợ | Lưu dưới dạng `SaveFormat.Xls` thay thế, nhưng lưu ý một số tính năng comment sẽ khác |

---

## Kết Quả Mong Đợi

- **File workbook:** `output.xlsx` được đặt trong thư mục bin của dự án.  
- **Ô B2:** Hiển thị văn bản placeholder `${Comment:UserComment}` (bạn có thể ẩn nó bằng cách đặt màu phông chữ của ô thành trắng).  
- **Comment gắn vào B2:** Hiển thị “Reviewed by QA” khi di chuột.

![Tạo Excel workbook C# ví dụ hiển thị comment trong ô B2](https://example.com/placeholder-image.png "Tạo Excel workbook C# ví dụ hiển thị comment trong ô B2")

*Văn bản thay thế hình ảnh:* **Tạo Excel workbook C# ví dụ hiển thị comment trong ô B2**

---

## Tóm Tắt – Những Gì Chúng Ta Đã Đạt Được

Chúng ta **đã tạo một Excel workbook C#**, chèn một **Smart Marker** chuyển thành một **excel comment**, cung cấp JSON để **generate excel comment**, và cuối cùng **đã lưu workbook dưới dạng xlsx**. Toàn bộ quy trình được gói gọn trong vài chục dòng mã C# sạch sẽ, tự chứa.

---

## Bước Tiếp Theo? Mở Rộng Giải Pháp

- **Tạo comment hàng loạt:** Duyệt qua một DataTable và áp dụng Smart Marker cho mỗi hàng để thêm ghi chú riêng cho từng hàng.  
- **Định dạng comment:** Điều chỉnh kích thước phông chữ, màu sắc, hoặc thậm chí thêm văn bản định dạng bằng bộ sưu tập `Comment.RichText`.  
- **Xuất ra PDF:** Sử dụng `workbook.Save("output.pdf", SaveFormat.Pdf);` để chia sẻ báo cáo với comment được giữ nguyên.  

Nếu bạn muốn tìm hiểu về **add excel comment** một cách lập trình trong các ngữ cảnh khác—như sử dụng OpenXML SDK hoặc EPPlus—các thư viện đó cũng hỗ trợ tạo comment, mặc dù giao diện API khác nhau.

---

### Suy Nghĩ Cuối Cùng

Việc thêm comment vào file Excel từ C# không cần phải là một công việc vất vả. Bằng cách tận dụng engine Smart Marker của Aspose.Cells, bạn có được một cách ngắn gọn, dựa trên dữ liệu để **add excel comment**, **generate excel comment**, và **save workbook as xlsx** với tối thiểu mã lặp.  

Hãy thử nghiệm, điều chỉnh JSON, và xem bạn nhanh chóng biến dữ liệu thô thành một bảng tính tinh tế, đầy comment. Chúc lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}