---
"description": "Tìm hiểu cách tắt các chú thích được hiển thị ở cấp độ thấp hơn khi lưu sổ làm việc Excel thành HTML bằng Aspose.Cells cho .NET với hướng dẫn từng bước chi tiết này."
"linktitle": "Tắt chế độ Downlevel Revealed Comments khi lưu vào HTML"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tắt chế độ Downlevel Revealed Comments khi lưu vào HTML"
"url": "/vi/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tắt chế độ Downlevel Revealed Comments khi lưu vào HTML

## Giới thiệu
Bạn đã bao giờ cần chuyển đổi sổ làm việc Excel sang HTML và muốn đảm bảo rằng bất kỳ chú thích không cần thiết hoặc nội dung ẩn nào không bị tiết lộ trong quá trình này chưa? Đó là lúc vô hiệu hóa các chú thích được tiết lộ ở cấp độ thấp trở nên hữu ích. Nếu bạn đang sử dụng Aspose.Cells cho .NET, bạn có toàn quyền kiểm soát cách sổ làm việc Excel của mình được hiển thị dưới dạng tệp HTML. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước đơn giản để giúp bạn vô hiệu hóa các chú thích được tiết lộ ở cấp độ thấp trong khi lưu sổ làm việc sang HTML. 
Đến cuối bài viết này, bạn sẽ hiểu rõ cách sử dụng tính năng này và đảm bảo đầu ra HTML của bạn sạch sẽ và không có bình luận.
## Điều kiện tiên quyết
Trước khi đi sâu vào hướng dẫn từng bước, chúng ta hãy cùng tìm hiểu một số điều bạn cần chuẩn bị để thực hiện suôn sẻ:
1. Aspose.Cells cho .NET: Bạn sẽ cần phải cài đặt thư viện Aspose.Cells. Nếu bạn chưa cài đặt, bạn có thể tải xuống [đây](https://releases.aspose.com/cells/net/).
2. IDE: Một môi trường phát triển như Visual Studio để viết và thực thi mã C# của bạn.
3. Kiến thức cơ bản về C#: Sự quen thuộc với cú pháp C# và lập trình hướng đối tượng sẽ giúp bạn theo dõi mã.
4. Phiên bản tạm thời hoặc có giấy phép: Bạn có thể sử dụng bản dùng thử miễn phí hoặc đăng ký giấy phép tạm thời từ [đây](https://purchase.aspose.com/temporary-license/). Điều này đảm bảo thư viện hoạt động mà không có bất kỳ hạn chế nào.
Bây giờ bạn đã sẵn sàng, chúng ta hãy bắt đầu ngay thôi!
## Nhập không gian tên
Trước khi đi vào các ví dụ về mã, điều cần thiết là phải bao gồm các không gian tên cần thiết cho Aspose.Cells. Nếu không có những không gian tên này, mã của bạn sẽ không thể truy cập các phương thức và thuộc tính cần thiết để thao tác với các tệp Excel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Đảm bảo đặt dòng này ở đầu tệp C# của bạn để nhập không gian tên Aspose.Cells.
## Bước 1: Thiết lập đường dẫn thư mục
Trước hết, chúng ta cần thiết lập thư mục nguồn (nơi lưu trữ tệp Excel của bạn) và thư mục đầu ra (nơi lưu tệp HTML của bạn). Điều này rất quan trọng vì Aspose.Cells yêu cầu đường dẫn tệp chính xác để truy cập và lưu tệp.
```csharp
// Thư mục nguồn nơi tệp Excel của bạn được lưu trữ
string sourceDir = "Your Document Directory";
// Thư mục đầu ra nơi tệp HTML kết quả sẽ được lưu
string outputDir = "Your Document Directory";
```
Trong bước này, thay thế `"Your Document Directory"` với đường dẫn tệp thực tế trên hệ thống của bạn. Bạn cũng có thể tạo thư mục tùy chỉnh để sắp xếp tốt hơn các tệp đầu vào và đầu ra của mình.
## Bước 2: Tải sổ làm việc Excel
Trong bước này, chúng ta sẽ tải sổ làm việc Excel vào bộ nhớ để có thể thao tác. Để trình bày, chúng ta sẽ sử dụng một tệp mẫu có tên `"sampleDisableDownlevelRevealedComments.xlsx"`. Bạn có thể sử dụng bất kỳ sổ làm việc nào bạn thích.
```csharp
// Tải sổ làm việc mẫu từ thư mục nguồn
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
Thao tác này tạo ra một đối tượng Workbook chứa tất cả dữ liệu và cấu trúc của tệp Excel của bạn. Từ đây, bạn có thể sửa đổi, áp dụng cài đặt và cuối cùng lưu ở định dạng khác.
## Bước 3: Thiết lập tùy chọn lưu HTML
Bây giờ, chúng ta cần cấu hình đối tượng HtmlSaveOptions để vô hiệu hóa các bình luận được tiết lộ ở cấp độ thấp hơn. Tùy chọn này đảm bảo rằng bất kỳ bình luận hoặc nội dung ẩn nào sẽ không được tiết lộ trong tệp HTML kết quả.
```csharp
// Tạo một đối tượng HtmlSaveOptions mới để cấu hình các tùy chọn lưu
HtmlSaveOptions opts = new HtmlSaveOptions();
// Tắt bình luận được tiết lộ ở cấp độ thấp hơn
opts.DisableDownlevelRevealedComments = true;
```
Bằng cách thiết lập `DisableDownlevelRevealedComments` ĐẾN `true`, bạn đảm bảo rằng khi bạn lưu sổ làm việc dưới dạng tệp HTML, mọi bình luận cấp dưới sẽ bị vô hiệu hóa.
## Bước 4: Lưu Workbook dưới dạng HTML
Sau khi đối tượng HtmlSaveOptions được cấu hình, bước tiếp theo là lưu sổ làm việc thành HTML bằng các tùy chọn đã chỉ định. Đây là nơi chuyển đổi tệp thực tế diễn ra.
```csharp
// Lưu sổ làm việc dưới dạng tệp HTML với các tùy chọn lưu được chỉ định
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
Trong dòng mã này, chúng tôi lưu sổ làm việc vào thư mục đầu ra mà bạn đã chỉ định trước đó và áp dụng cài đặt DisableDownlevelRevealedComments. Kết quả sẽ là một tệp HTML sạch không có bất kỳ chú thích không mong muốn nào.
## Bước 5: Xác minh và thực hiện
Cuối cùng, để đảm bảo mọi thứ hoạt động như mong đợi, bạn có thể xuất thông báo thành công ra bảng điều khiển.
```csharp
// Xuất thông báo thành công ra bảng điều khiển
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
Điều này cho bạn biết rằng thao tác đã hoàn tất mà không có lỗi.
## Phần kết luận
Và bạn đã có nó! Bạn đã học thành công cách vô hiệu hóa các bình luận được tiết lộ ở cấp độ thấp trong khi lưu sổ làm việc Excel thành HTML bằng Aspose.Cells cho .NET. Với tính năng này, giờ đây bạn có thể kiểm soát cách sổ làm việc của mình được hiển thị dưới dạng HTML và tránh tiết lộ bất kỳ nội dung không cần thiết nào. Cho dù bạn đang phát triển ứng dụng web hay chỉ cần đầu ra HTML sạch, phương pháp này đảm bảo việc chuyển đổi sổ làm việc của bạn chính xác và an toàn.
Nếu bạn thấy hướng dẫn này hữu ích, hãy cân nhắc khám phá các tính năng khác của Aspose.Cells để nâng cao hơn nữa khả năng xử lý Excel của bạn.
## Câu hỏi thường gặp
### Bình luận được tiết lộ ở cấp độ thấp là gì?
Bình luận tiết lộ cấp độ thấp thường được sử dụng trong phát triển web để cung cấp thêm thông tin cho các trình duyệt cũ không hỗ trợ một số tính năng HTML nhất định. Trong quá trình chuyển đổi Excel sang HTML, đôi khi chúng có thể tiết lộ nội dung hoặc bình luận ẩn, đó là lý do tại sao việc vô hiệu hóa chúng có thể hữu ích.
### Tôi có thể bật chế độ bình luận cấp thấp hơn nếu cần không?
Vâng, chỉ cần thiết lập `DisableDownlevelRevealedComments` tài sản để `false` nếu bạn muốn bật bình luận cấp thấp hơn khi lưu sổ làm việc của mình dưới dạng HTML.
### Làm thế nào để tôi có được giấy phép tạm thời cho Aspose.Cells?
Bạn có thể dễ dàng nộp đơn xin cấp giấy phép tạm thời bằng cách truy cập [Trang web Aspose](https://purchase.aspose.com/temporary-license/).
### Việc tắt bình luận cấp thấp có ảnh hưởng đến giao diện của HTML không?
Không, việc vô hiệu hóa các bình luận được tiết lộ ở cấp độ thấp không ảnh hưởng đến giao diện trực quan của đầu ra HTML. Nó chỉ ngăn chặn việc tiết lộ thông tin bổ sung dành cho các trình duyệt cũ hơn.
### Tôi có thể lưu bảng tính ở định dạng khác ngoài HTML không?
Có, Aspose.Cells hỗ trợ nhiều định dạng đầu ra như PDF, CSV và TXT. Bạn có thể khám phá thêm các tùy chọn trong [tài liệu](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}