---
"description": "Tìm hiểu cách trích xuất văn bản từ SmartArt dạng bánh răng trong Excel bằng Aspose.Cells cho .NET. Có kèm hướng dẫn từng bước và ví dụ mã."
"linktitle": "Trích xuất văn bản từ Gear Type Smart Art trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Trích xuất văn bản từ Gear Type Smart Art trong Excel"
"url": "/vi/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ Gear Type Smart Art trong Excel

## Giới thiệu
Khi làm việc với Excel, bạn có thể gặp đồ họa SmartArt giúp truyền tải thông điệp của mình theo cách hấp dẫn về mặt thị giác. Trong số các đồ họa này, SmartArt dạng bánh răng là loại được ưa chuộng nhất vì các luồng phân cấp và định hướng của nó, thường được sử dụng trong quản lý dự án hoặc mô hình hóa hệ thống. Nhưng nếu bạn cần trích xuất văn bản từ các hình dạng này theo chương trình thì sao? Đây chính là lúc Aspose.Cells for .NET trở nên hữu ích! Trong bài đăng trên blog này, chúng tôi sẽ hướng dẫn bạn từng bước về cách trích xuất văn bản từ các hình dạng SmartArt dạng bánh răng trong Excel bằng Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi bắt đầu, có một số điều kiện tiên quyết thiết yếu mà bạn cần phải có. Đừng lo lắng; rất đơn giản và tôi sẽ hướng dẫn bạn.
### Môi trường .NET
Đảm bảo bạn đã thiết lập môi trường phát triển .NET trên máy tính của mình. Có thể là Visual Studio hoặc bất kỳ IDE nào bạn chọn hỗ trợ phát triển .NET.
### Aspose.Cells cho .NET
Tiếp theo, bạn sẽ cần cài đặt thư viện Aspose.Cells. Đây là công cụ mạnh mẽ cho phép bạn thao tác các tệp Excel một cách liền mạch. Bạn có thể tải xuống từ [Trang phát hành Aspose](https://releases.aspose.com/cells/net/). Nếu bạn muốn khám phá nó trước, hãy tận dụng [dùng thử miễn phí](https://releases.aspose.com/).
### Kiến thức cơ bản về C#
Hiểu biết cơ bản về lập trình C# chính là những gì bạn cần để làm theo hướng dẫn này. Nếu bạn mới làm quen, đừng lo lắng—tôi sẽ thiết kế các bước sao cho thân thiện với người mới bắt đầu nhất có thể.
### Tệp Excel mẫu
Đối với hướng dẫn này, bạn cũng sẽ cần một tệp Excel mẫu có chứa các hình dạng SmartArt loại bánh răng. Bạn có thể dễ dàng tạo một tệp hoặc tìm mẫu trực tuyến. Chỉ cần đảm bảo SmartArt bao gồm ít nhất một hình dạng bánh răng.
## Nhập gói
Để bắt đầu mã hóa, bạn sẽ cần nhập các gói cần thiết. Sau đây là cách thực hiện:
### Tạo một dự án mới
1. Mở .NET IDE của bạn.
2. Tạo một dự án mới. Ví dụ, chọn 'Console Application' trong tùy chọn .NET.
3. Đặt tên cho dự án và thiết lập khung mong muốn. 
### Thêm tài liệu tham khảo
Để sử dụng Aspose.Cells, bạn sẽ cần thêm tham chiếu thư viện vào dự án của mình:
1. Nhấp chuột phải vào tên dự án của bạn trong Solution Explorer.
2. Chọn “Quản lý gói NuGet”.
3. Tìm kiếm "Aspose.Cells" và cài đặt.
Sau khi cài đặt, bạn đã sẵn sàng để viết mã!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Bây giờ, chúng ta hãy phân tích mã bạn sẽ sử dụng để trích xuất văn bản. Chúng ta sẽ thực hiện từng bước một.
## Bước 1: Thiết lập thư mục nguồn
Bắt đầu bằng cách xác định thư mục chứa tệp Excel của bạn:
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
```
Hãy chắc chắn thay thế `"Your Document Directory"` với đường dẫn thực tế đến tệp Excel của bạn.
## Bước 2: Tải sổ làm việc Excel
Tiếp theo, chúng ta sẽ tải sổ làm việc Excel. Đây là cách chúng ta có thể truy cập nội dung của nó:
```csharp
// Tải tệp Excel mẫu có chứa hình dạng nghệ thuật thông minh loại bánh răng.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Phần này sẽ tải bảng tính Excel mẫu của bạn.
## Bước 3: Truy cập vào trang tính đầu tiên
Bây giờ chúng ta đã tải bảng tính, hãy truy cập vào bảng tính đầu tiên có SmartArt của chúng ta:
```csharp
// Truy cập bảng tính đầu tiên.
Worksheet ws = wb.Worksheets[0];
```
Thao tác này sẽ lấy lại bảng tính đầu tiên để thao tác thêm.
## Bước 4: Truy cập hình dạng đầu tiên
Tiếp theo, chúng ta cần truy cập hình dạng đầu tiên trong bảng tính của mình. Bằng cách này, chúng ta có thể điều hướng qua đồ họa SmartArt của mình:
```csharp
// Truy cập hình dạng đầu tiên.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Ở đây, chúng ta tập trung vào hình dạng đầu tiên, mà chúng ta cho là SmartArt mà chúng ta cần.
## Bước 5: Nhận hình dạng nhóm
Khi đã có hình dạng, đã đến lúc lấy kết quả biểu diễn SmartArt của chúng ta:
```csharp
// Nhận kết quả của hình dạng nghệ thuật thông minh loại bánh răng dưới dạng hình nhóm.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Thao tác này sẽ lấy SmartArt dạng bánh răng của chúng ta dưới dạng một hình dạng được nhóm lại.
## Bước 6: Trích xuất các hình dạng riêng lẻ
Bây giờ, chúng ta hãy trích xuất các hình dạng riêng lẻ tạo nên SmartArt của chúng ta:
```csharp
// Lấy danh sách các hình dạng riêng lẻ bao gồm hình dạng nhóm.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Mảng này sẽ chứa tất cả các hình dạng riêng lẻ mà chúng ta cần lặp qua.
## Bước 7: Trích xuất và in văn bản
Cuối cùng, chúng ta có thể lặp qua mảng hình dạng và trích xuất văn bản từ bất kỳ hình dạng bánh răng nào:
```csharp
// Trích xuất văn bản của các hình dạng loại bánh răng và in chúng trên bảng điều khiển.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Trong vòng lặp này, chúng ta kiểm tra loại hình dạng và in văn bản nếu đó là hình dạng bánh răng.
## Bước 8: Xác nhận thực hiện
Cuối cùng, bạn có thể muốn thêm tin nhắn xác nhận sau khi quá trình hoàn tất thành công:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Với thao tác này, quá trình trích xuất đã hoàn tất và bạn sẽ thấy văn bản đầu ra trong bảng điều khiển!
## Phần kết luận
Xin chúc mừng! Bạn vừa học cách trích xuất văn bản từ các hình dạng SmartArt dạng bánh răng trong Excel bằng Aspose.Cells cho .NET. Kỹ thuật tiện dụng này mở ra cánh cửa để tự động hóa các báo cáo hoặc tài liệu dựa trên biểu diễn dữ liệu trực quan. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, việc kiểm soát và trích xuất thông tin từ SmartArt có thể hợp lý hóa quy trình làm việc của bạn và giúp bạn hiệu quả hơn. Đừng quên khám phá chi tiết [Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để có thêm nhiều khả năng hơn.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là thư viện .NET cho phép các nhà phát triển tạo và thao tác các tệp Excel dễ dàng.
### Tôi có thể sử dụng Aspose.Cells với các ngôn ngữ khác không?
Có! Aspose.Cells có sẵn bằng nhiều ngôn ngữ lập trình, bao gồm Java và Python.
### Tôi có cần mua Aspose.Cells cho .NET không?
Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để sử dụng lâu dài, bạn cần phải mua. Bạn có thể tìm thấy các tùy chọn mua [đây](https://purchase.aspose.com/buy).
### Người dùng Aspose.Cells có được hỗ trợ không?
Chắc chắn rồi! Bạn có thể tìm thấy sự hỗ trợ của cộng đồng tại [Diễn đàn Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Tôi có thể trích xuất các loại SmartArt khác bằng phương pháp này không?
Có, chỉ cần một vài sửa đổi nhỏ, bạn có thể trích xuất văn bản từ nhiều hình dạng SmartArt khác nhau bằng cách thay đổi các điều kiện trong mã của mình.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}