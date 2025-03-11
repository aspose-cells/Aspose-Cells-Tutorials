---
title: Điều chỉnh mức độ nén trong Workbook
linktitle: Điều chỉnh mức độ nén trong Workbook
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách điều chỉnh mức độ nén của sổ làm việc Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Tối ưu hóa việc quản lý tệp của bạn.
weight: 14
url: /vi/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Điều chỉnh mức độ nén trong Workbook

## Giới thiệu
Khi nói đến việc quản lý các tệp Excel lớn, nén là một công cụ thay đổi cuộc chơi. Nó không chỉ tiết kiệm dung lượng lưu trữ mà còn giúp truyền tệp nhanh hơn và hiệu quả hơn. Nếu bạn đang làm việc với Aspose.Cells cho .NET, bạn có thể dễ dàng điều chỉnh mức độ nén của sổ làm việc. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước trong quy trình, đảm bảo rằng bạn hiểu từng phần của mã và cách thức hoạt động của nó.
## Điều kiện tiên quyết
Trước khi bắt đầu viết mã, bạn cần phải có một số điều kiện tiên quyết sau:
1. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
2.  Thư viện Aspose.Cells: Bạn cần cài đặt thư viện Aspose.Cells. Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/).
3. Visual Studio: Cần có môi trường phát triển như Visual Studio để chạy mã.
4. .NET Framework: Đảm bảo rằng dự án của bạn được thiết lập với phiên bản .NET Framework tương thích.
## Nhập gói
Để bắt đầu, bạn cần nhập các gói cần thiết vào dự án C# của mình. Sau đây là cách bạn có thể thực hiện:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Các gói này rất cần thiết để làm việc với các tệp Excel bằng thư viện Aspose.Cells.`Aspose.Cells` không gian tên chứa tất cả các lớp bạn cần để thao tác các tệp Excel, trong khi`Aspose.Cells.Xlsb` cung cấp các tùy chọn để lưu tệp theo định dạng XLSB.
Bây giờ, chúng ta hãy chia nhỏ quá trình điều chỉnh mức độ nén trong bảng tính thành các bước dễ quản lý.
## Bước 1: Xác định thư mục nguồn và thư mục đầu ra
Đầu tiên, bạn cần chỉ định nơi lưu trữ các tệp nguồn và nơi bạn muốn lưu các tệp đầu ra. Điều này rất quan trọng để đảm bảo chương trình của bạn biết nơi tìm các tệp cần thiết để làm việc.
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế đến thư mục của bạn. Điều này sẽ giúp chương trình xác định vị trí các tệp bạn muốn nén.
## Bước 2: Tải Workbook
Tiếp theo, bạn sẽ tải sổ làm việc mà bạn muốn nén. Đây chính là nơi phép thuật bắt đầu!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
Trong dòng này, chúng ta tạo một phiên bản mới của`Workbook` lớp và tải tệp Excel hiện có. Đảm bảo rằng tên tệp khớp với tên bạn có trong thư mục nguồn.
## Bước 3: Thiết lập tùy chọn lưu
Bây giờ là lúc cấu hình các tùy chọn lưu. Chúng ta sẽ thiết lập loại nén cho tệp đầu ra. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 Các`XlsbSaveOptions` lớp này cho phép bạn chỉ định nhiều tùy chọn khác nhau khi lưu sổ làm việc của mình ở định dạng XLSB, bao gồm cả mức độ nén.
## Bước 4: Đo thời gian nén cho cấp độ 1
Chúng ta hãy bắt đầu với mức nén đầu tiên. Chúng ta sẽ đo thời gian cần thiết để lưu sổ làm việc với mức nén này.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Ở đây, chúng tôi đặt loại nén thành Mức 1, lưu sổ làm việc và sau đó đo thời gian trôi qua. Điều này cho chúng tôi biết quá trình này mất bao lâu.
## Bước 5: Đo thời gian nén cho cấp độ 6
Tiếp theo, chúng ta hãy xem hiệu suất nén Cấp độ 6 như thế nào.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Bước này tương tự như bước trước, nhưng chúng ta thay đổi mức nén thành Mức 6. Bạn sẽ nhận thấy rằng thời gian thực hiện có thể thay đổi tùy theo độ phức tạp của bảng tính.
## Bước 6: Đo thời gian nén cho cấp độ 9
Cuối cùng, chúng ta hãy kiểm tra hiệu suất ở mức nén cao nhất.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
Ở bước này, chúng tôi đặt mức nén thành Mức 9. Đây là mức mà bạn thường thấy kích thước tệp giảm đáng kể nhất, nhưng có thể mất nhiều thời gian hơn để xử lý.
## Bước 7: Đầu ra cuối cùng
Sau khi chạy tất cả các mức nén, bạn có thể đưa ra thông báo cho biết quá trình đã hoàn tất thành công.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Dòng mã đơn giản này xác nhận rằng chương trình của bạn đã hoàn tất thực thi mà không có bất kỳ trục trặc nào.
## Phần kết luận
Điều chỉnh mức độ nén của sổ làm việc của bạn bằng Aspose.Cells cho .NET là một quá trình đơn giản có thể mang lại lợi ích đáng kể về kích thước tệp và hiệu suất. Bằng cách làm theo các bước được nêu trong hướng dẫn này, bạn có thể dễ dàng triển khai nén trong các ứng dụng của mình và cải thiện hiệu quả quản lý tệp Excel.
## Câu hỏi thường gặp
### Aspose.Cells là gì?  
Aspose.Cells là một thư viện mạnh mẽ dành cho .NET cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel mà không cần đến Microsoft Excel.
### Làm thế nào để cài đặt Aspose.Cells?  
 Bạn có thể tải xuống và cài đặt Aspose.Cells từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
### Có những mức độ nén nào?  
Aspose.Cells hỗ trợ nhiều mức nén khác nhau, từ Mức 1 (nén thấp nhất) đến Mức 9 (nén cao nhất).
### Tôi có thể dùng thử Aspose.Cells miễn phí không?  
 Có! Bạn có thể dùng thử miễn phí Aspose.Cells[đây](https://releases.aspose.com/).
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?  
 Đối với bất kỳ thắc mắc hoặc hỗ trợ nào, bạn có thể truy cập diễn đàn hỗ trợ Aspose[đây](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
