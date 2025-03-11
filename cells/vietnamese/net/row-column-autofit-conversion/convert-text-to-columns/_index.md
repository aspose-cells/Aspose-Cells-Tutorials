---
title: Chuyển đổi văn bản thành cột trong Aspose.Cells .NET
linktitle: Chuyển đổi văn bản thành cột trong Aspose.Cells .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chuyển đổi văn bản thành cột dễ dàng bằng Aspose.Cells cho .NET trong hướng dẫn từng bước chi tiết này.
weight: 15
url: /vi/net/row-column-autofit-conversion/convert-text-to-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi văn bản thành cột trong Aspose.Cells .NET

## Giới thiệu
Trong thế giới quản lý dữ liệu nhịp độ nhanh ngày nay, hiệu quả là chìa khóa. Cho dù bạn là một nhà phân tích xử lý số liệu hay một chuyên gia kinh doanh chuẩn bị báo cáo, bạn thường thấy mình cần phải thao tác dữ liệu một cách nhanh chóng và chính xác. Nếu bạn đã từng phải xử lý các tên trong một ô duy nhất mà bạn cần chia thành các cột riêng biệt, bạn sẽ biết nó có thể tẻ nhạt như thế nào. Rất may, Aspose.Cells for .NET cung cấp một giải pháp tinh tế để chia văn bản thành các cột. Trong hướng dẫn này, chúng ta sẽ hướng dẫn quy trình chuyển đổi văn bản thành các cột bằng Aspose.Cells.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã thiết lập xong. Sau đây là những gì bạn cần:
1.  Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình. Nếu bạn chưa có, bạn có thể tải xuống từ[Trang web của Microsoft](https://visualstudio.microsoft.com/downloads/).
2. .NET Framework: Đảm bảo rằng bạn đang làm việc trong một dự án nhắm mục tiêu đến phiên bản tương thích của .NET Framework. Aspose.Cells tương thích với .NET Core, .NET Framework và các nền tảng khác.
3.  Thư viện Aspose.Cells: Bạn cần tải xuống và tham chiếu thư viện Aspose.Cells trong dự án của mình. Bạn có thể lấy nó từ[Trang Tải xuống Aspose](https://releases.aspose.com/cells/net/).
4. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu hướng dẫn này dễ dàng hơn.
## Nhập gói
Để mọi thứ bắt đầu, chúng ta cần nhập các gói Aspose.Cells cần thiết. Sau đây là cách bạn có thể thực hiện:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Điều này cho phép bạn truy cập tất cả các chức năng cần thiết của Aspose.Cells để xử lý dữ liệu.
Bây giờ chúng ta đã có mọi thứ cần thiết, hãy bắt đầu bằng cách chia nhỏ quá trình chuyển đổi văn bản thành cột thành nhiều bước dễ thực hiện.
## Bước 1: Thiết lập thư mục tài liệu
Trước tiên, bạn cần cấu hình thư mục nơi bạn sẽ lưu tệp đầu ra. Luôn là một ý tưởng hay khi cấu trúc các tệp của bạn một cách gọn gàng; điều này giúp quản lý chúng dễ dàng.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
-  Thay thế`"Your Document Directory"`với đường dẫn thực tế nơi bạn muốn lưu tệp của mình. Ví dụ, bạn có thể sử dụng`C:\\Documents\\AsposeOutput\\`.
## Bước 2: Tạo một phiên bản Workbook
Tiếp theo, hãy tạo sổ làm việc của chúng ta. Về cơ bản, đây là tệp mà tất cả dữ liệu của bạn sẽ được xử lý.
```csharp
// Tạo một phiên bản sổ làm việc.
Workbook wb = new Workbook();
```
- Hãy coi sổ làm việc như một tấm vải trắng. Bạn có thể vẽ bất cứ thứ gì bạn thích!
## Bước 3: Truy cập vào trang tính đầu tiên
Bây giờ chúng ta đã có bảng tính, chúng ta cần truy cập vào bảng tính đầu tiên để bắt đầu thêm dữ liệu.
```csharp
// Truy cập vào bảng tính đầu tiên.
Worksheet ws = wb.Worksheets[0];
```
- Phiếu bài tập giống như một trang trong sổ làm việc của bạn. Bạn có thể có nhiều trang, nhưng chúng tôi sẽ tập trung vào trang đầu tiên để đơn giản.
## Bước 4: Thêm dữ liệu vào trang tính
Hãy điền một số tên vào bảng tính của chúng ta. Chúng ta sẽ nhập một danh sách tên trong đó tên và họ được phân cách bằng một khoảng trắng.
```csharp
// Thêm tên người vào cột A. Tên và Họ được phân tách bằng dấu cách.
ws.Cells["A1"].PutValue("John Teal");
ws.Cells["A2"].PutValue("Peter Graham");
ws.Cells["A3"].PutValue("Brady Cortez");
ws.Cells["A4"].PutValue("Mack Nick");
ws.Cells["A5"].PutValue("Hsu Lee");
```
- Bạn có thể muốn điều chỉnh tên của mình nếu cần; có thể bạn muốn thử nghiệm với danh sách tên của riêng mình hoặc tạo một danh sách đa dạng hơn.
## Bước 5: Tạo tùy chọn tải văn bản
Trước khi tách tên, chúng ta phải xác định cách chúng ta muốn tách văn bản. Trong trường hợp này, chúng ta sẽ sử dụng khoảng trắng làm dấu phân cách.
```csharp
// Tạo tùy chọn tải văn bản với khoảng trắng làm dấu phân cách.
TxtLoadOptions opts = new TxtLoadOptions();
opts.Separator = ' ';
```
- Bằng cách xác định khoảng trắng làm dấu phân cách, chúng ta thông báo cho Aspose rằng đây là nơi cần phân tách tên.
## Bước 6: Chia cột thành nhiều cột
 Đây là phép thuật! Bây giờ chúng ta sẽ chia nội dung của cột A thành hai cột riêng biệt (tên ở cột A và họ ở cột B) bằng cách sử dụng`TextToColumns` phương pháp.
```csharp
// Chia cột A thành hai cột bằng phương thức TextToColumns().
// Bây giờ cột A sẽ có tên và cột B sẽ có họ.
ws.Cells.TextToColumns(0, 0, 5, opts);
```
- Bước này giúp bạn bớt đi mọi công sức. Giống như có một người trợ lý nhỏ siêng năng biết chính xác phải làm gì!
## Bước 7: Lưu sổ làm việc
Cuối cùng, hãy lưu sổ làm việc với những thay đổi đã thực hiện. Luôn cảm thấy thỏa mãn khi thấy công việc của mình được lưu sạch sẽ!
```csharp
// Lưu bảng tính ở định dạng xlsx.
wb.Save(dataDir + "outputTextToColumns.xlsx");
```
- Hãy đảm bảo bạn đặt tên cho tệp có ý nghĩa. Trong trường hợp này, chúng tôi sẽ lưu tệp dưới dạng`outputTextToColumns.xlsx`, nhưng bạn có thể đổi tên thành bất cứ tên nào bạn thấy phù hợp.
## Phần kết luận
 Và bạn đã có nó! Bạn vừa học cách chuyển đổi văn bản thành cột bằng Aspose.Cells cho .NET. Đây là một công cụ mạnh mẽ giúp đơn giản hóa việc xử lý dữ liệu, cho phép bạn thực hiện các thao tác từng mất hàng giờ chỉ bằng một vài dòng mã đơn giản. Bây giờ, lần sau khi bạn cần tách tên hoặc văn bản khác, bạn có thể thực hiện dễ dàng. Đừng quên khám phá[Tài liệu của Aspose](https://reference.aspose.com/cells/net/) để có thêm nhiều tính năng và tùy chỉnh nâng cao có thể nâng cao kỹ năng xử lý dữ liệu của bạn!
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ cho phép các nhà phát triển tạo, thao tác và chuyển đổi bảng tính Excel một cách hiệu quả mà không cần cài đặt Microsoft Excel.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có! Bạn có thể bắt đầu với bản dùng thử miễn phí có sẵn từ[Trang dùng thử của Aspose](https://releases.aspose.com/).
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?
 Đối với bất kỳ thắc mắc hoặc vấn đề nào, bạn có thể truy cập[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).
### Học Aspose.Cells có dễ không?
Chắc chắn rồi! Với các ví dụ trực quan và tài liệu hướng dẫn chi tiết, ngay cả người mới bắt đầu cũng có thể học nhanh chóng.
### Aspose.Cells còn cung cấp những tính năng nào khác?
Ngoài việc chỉnh sửa văn bản, Aspose.Cells còn hỗ trợ tạo biểu đồ, xác thực dữ liệu, tính toán công thức và nhiều chức năng khác!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
