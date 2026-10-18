---
category: general
date: 2026-03-25
description: Cách viết mẫu bằng Smart Markers và học cách lặp lại các hàng, ràng buộc
  dữ liệu, tạo báo cáo và tạo mẫu một cách dễ dàng.
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: vi
og_description: Cách viết mẫu sử dụng Smart Markers. Khám phá cách lặp lại các hàng,
  ràng buộc dữ liệu, tạo báo cáo và tạo mẫu trong C#.
og_title: Cách viết mẫu với Smart Markers – Hướng dẫn đầy đủ
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: Cách viết mẫu với các dấu thông minh – Hướng dẫn từng bước
url: /vi/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách viết mẫu với Smart Markers – Hướng dẫn đầy đủ  

Bạn đã bao giờ tự hỏi **cách viết mẫu** mà tự động mở rộng dựa trên dữ liệu của mình chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi cần một báo cáo Excel động nhưng không biết tính năng API nào cần sử dụng. Tin tốt? Với Aspose.Cells Smart Markers, bạn có thể tạo một mẫu trong một ô duy nhất, ràng buộc dữ liệu phân cấp, và để thư viện tự lặp lại các hàng cho bạn. Trong hướng dẫn này, chúng tôi cũng sẽ đề cập đến **cách lặp lại các hàng**, **cách ràng buộc dữ liệu**, và thậm chí **cách tạo báo cáo** mà không cần tự viết vòng lặp qua các worksheet.

Khi kết thúc tutorial này, bạn sẽ có một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách tạo mẫu** cho các kịch bản master‑detail, cùng với các mẹo cho các trường hợp đặc biệt và thủ thuật hiệu năng. Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.

---

## Những gì bạn sẽ xây dựng

Chúng ta sẽ tạo một workbook Excel liệt kê các đơn hàng (master) và các mục chi tiết (detail). Mẫu nằm trong ô **A1**, và Smart Markers sẽ mở rộng nó thành một bảng được định dạng đẹp mắt. Trang cuối cùng sẽ trông như sau:

```
Order1
   A
   B
Order2
   C
```

Đây là một kịch bản “cách tạo báo cáo” cổ điển, và mã hoạt động với .NET 6+ và Aspose.Cells 23.x (hoặc phiên bản mới hơn).

---

## Yêu cầu trước

- .NET 6 SDK (hoặc bất kỳ phiên bản .NET gần đây nào)  
- Visual Studio 2022 hoặc VS Code  
- Aspose.Cells cho .NET (cài đặt qua NuGet: `Install-Package Aspose.Cells`)  

Nếu bạn đã có những thứ này, bạn đã sẵn sàng.

---

## Bước 1: Thiết lập dự án và thêm Aspose.Cells  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Tại sao điều này quan trọng*: Bắt đầu với một `Workbook` mới đảm bảo một canvas sạch sẽ. Đối tượng `Worksheet` là nơi chúng ta sẽ đặt mẫu của mình.

---

## Bước 2: Viết mẫu Smart Marker  

Mẫu sử dụng `${Master.Name}` cho tiêu đề đơn hàng và `${Detail:Repeat}` để lặp qua từng mục chi tiết.

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Mẹo chuyên nghiệp**: Giữ mẫu trong một ô duy nhất; Smart Markers sẽ tự động mở rộng nó qua các hàng.  

*Cách giải quyết vấn đề*: Bằng cách nhúng khối lặp trực tiếp trong ô, bạn tránh việc chèn hàng thủ công—Aspose sẽ xử lý thay bạn.

---

## Bước 3: Xây dựng dữ liệu phân cấp phù hợp với mẫu  

Dữ liệu của chúng ta phải phản ánh cấu trúc của mẫu: một collection `Master`, mỗi phần tử chứa một mảng `Detail`.

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Tại sao chúng ta ràng buộc dữ liệu theo cách này*: Smart Markers sử dụng ràng buộc kiểu reflection, vì vậy tên thuộc tính phải khớp chính xác với các placeholder. Đây là cốt lõi của **cách ràng buộc dữ liệu** cho các báo cáo động.

---

## Bước 4: Xử lý mẫu – Để Smart Markers làm công việc nặng  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

Sau khi xử lý, worksheet sẽ chứa các hàng đã được mở rộng. Không cần vòng lặp, không cần ghi ô thủ công.

---

## Bước 5: Lưu Workbook  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Mở file đã tạo và bạn sẽ thấy bố cục master‑detail chính xác như đã mô tả ở trên. Đó là **cách tạo báo cáo** chỉ với một dòng mã xử lý.

---

## Tổng quan trực quan  

![Báo cáo Excel được tạo bởi Smart Markers – cách viết mẫu](/images/smart-marker-report.png "cách viết mẫu")

*Văn bản thay thế*: "cách viết mẫu" – ảnh chụp màn hình của file Excel cuối cùng hiển thị các hàng được lặp lại cho mỗi đơn hàng.

---

## Đi sâu: Tại sao Smart Markers là một bước đột phá  

### Cách lặp lại các hàng mà không cần vòng lặp  

Tự động hoá Excel truyền thống buộc bạn phải tính hàng cuối cùng, chèn hàng mới và sao chép kiểu dáng—tất cả đều dễ gây lỗi. Smart Markers thay thế bằng một khối khai báo `${Detail:Repeat}`. Engine sẽ phân tích khối, sao chép hàng cho mỗi phần tử trong collection và chèn giá trị. Cách tiếp cận này là **cách lặp lại các hàng** một cách hiệu quả.

### Ràng buộc các đối tượng phức tạp  

Bạn có thể ràng buộc các đối tượng lồng nhau, collection, hoặc thậm chí DataTables. Miễn là tên thuộc tính khớp, bộ xử lý sẽ duyệt qua đồ thị đối tượng. Đây là bản chất của **cách ràng buộc dữ liệu**: bạn cung cấp cho bộ xử lý một đối tượng CLR thông thường (hoặc một kiểu ẩn danh, như chúng tôi đã làm) và để nó tự động ánh xạ.

### Tạo các định dạng khác nhau  

Mặc dù ví dụ của chúng tôi lưu dưới dạng XLSX, bạn có thể thay `SaveFormat.Pdf` hoặc `SaveFormat.Csv` chỉ bằng một dòng thay đổi. Đó là cách nhanh để **cách tạo báo cáo** ở nhiều định dạng mà không cần chỉnh sửa mẫu.

### Tái sử dụng mẫu  

Nếu bạn cần **cách tạo mẫu** cho các worksheet khác, chỉ cần sao chép nội dung ô sang sheet khác hoặc lưu nó trong một tài nguyên chuỗi. Lệnh gọi bộ xử lý giống nhau hoạt động ở mọi nơi, giúp mã của bạn DRY và dễ bảo trì.

---

## Các câu hỏi thường gặp & Trường hợp đặc biệt  

| Question | Answer |
|----------|--------|
| *Nếu master không có dòng chi tiết nào?* | Khối `${Detail:Repeat}` sẽ bị bỏ qua, chỉ để lại tên master. Không có hàng trống nào được tạo. |
| *Tôi có thể định dạng các hàng được lặp lại không?* | Có—áp dụng định dạng cho hàng mẫu (phông chữ, viền, v.v.) trước khi xử lý. Kiểu dáng sẽ được sao chép vào mỗi hàng được tạo. |
| *Có cần giải phóng workbook không?* | `Workbook` triển khai `IDisposable`. Bao bọc nó trong khối `using` cho mã sản xuất, nhưng đối với demo console ngắn thì không bắt buộc. |
| *Dữ liệu có thể lớn tới mức nào?* | Smart Markers tiết kiệm bộ nhớ, nhưng các collection cực lớn (hàng trăm nghìn) có thể cần phân trang hoặc streaming. |
| *Có thể dùng file JSON thay cho một đối tượng không?* | Chắc chắn—giải mã JSON thành một POCO phù hợp với mẫu, sau đó truyền nó vào `Process`. |

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Chạy chương trình (`dotnet run`) và mở *SmartMarkerReport.xlsx* – bạn sẽ thấy các hàng master‑detail được sắp xếp gọn gàng.

---

## Tóm tắt  

Chúng tôi đã trả lời **cách viết mẫu** bằng cách sử dụng Aspose.Cells Smart Markers, trình bày **cách lặp lại các hàng**, chỉ ra **cách ràng buộc dữ liệu** với các đối tượng phân cấp, và minh họa **cách tạo báo cáo** ở định dạng XLSX (hoặc bất kỳ định dạng nào được hỗ trợ). Mẫu tương tự cho phép bạn **cách tạo mẫu** cho hoá đơn, tồn kho, hoặc bất kỳ bố cục master‑detail nào bạn có thể tưởng tượng.

---

## Tiếp theo là gì?  

- **Định dạng đầu ra**: áp dụng kiểu ô cho hàng mẫu trước khi xử lý.  
- **Xuất ra PDF**: thay đổi `SaveFormat.Xlsx` thành `SaveFormat.Pdf` để tạo báo cáo có thể in.  
- **Tiêu đề động**: thêm placeholder `${Headers}` để tạo tiêu đề cột ngay lập tức.  
- **Nhiều sheet**: lặp lại quy trình trên các worksheet bổ sung cho các báo cáo đa phần.  

Hãy thoải mái thử nghiệm—đổi nguồn dữ liệu, thêm các cấp lồng nhau, hoặc kết hợp với công thức. Tính linh hoạt của Smart Markers có nghĩa là bạn dành ít thời gian viết vòng lặp hơn và nhiều thời gian hơn để mang lại giá trị.

*Chúc lập trình vui vẻ! Nếu bạn gặp bất kỳ khó khăn nào, hãy để lại bình luận bên dưới hoặc nhắn tin cho tôi trên Stack Overflow với thẻ `aspose-cells`. Hãy tiếp tục trao đổi nhé.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}