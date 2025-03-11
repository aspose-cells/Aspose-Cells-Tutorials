---
title: Theo dõi tiến trình chuyển đổi tài liệu theo chương trình trong .NET
linktitle: Theo dõi tiến trình chuyển đổi tài liệu theo chương trình trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách theo dõi tiến trình chuyển đổi tài liệu theo chương trình bằng Aspose.Cells cho .NET trong hướng dẫn chi tiết này.
weight: 20
url: /vi/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Theo dõi tiến trình chuyển đổi tài liệu theo chương trình trong .NET

## Giới thiệu
Bạn có muốn cải thiện quy trình chuyển đổi tài liệu của mình bằng Aspose.Cells cho .NET không? Nếu vậy, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng ta sẽ đi sâu vào việc theo dõi tiến trình chuyển đổi của các tài liệu Excel khi chúng được chuyển đổi sang định dạng PDF. Chúng tôi không chỉ hướng dẫn bạn qua các bước cần thiết để đạt được điều này mà còn cung cấp một số thông tin chi tiết hữu ích trong suốt quá trình. Vậy, hãy bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi đi sâu vào chi tiết về việc theo dõi quá trình chuyển đổi tài liệu, bạn cần phải có một số điều kiện tiên quyết sau:
1. Kiến thức cơ bản về C#: Vì chúng ta sẽ sử dụng C# để viết mã, nên hiểu biết cơ bản về ngôn ngữ lập trình này sẽ rất hữu ích.
2. Visual Studio đã cài đặt: Đây sẽ là môi trường phát triển của chúng tôi. Bạn có thể sử dụng bất kỳ phiên bản nào bạn thích, nhưng phiên bản mới nhất luôn là lựa chọn tốt.
3.  Aspose.Cells cho .NET: Đảm bảo bạn đã cài đặt Aspose.Cells. Bạn có thể tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
4.  Tệp Excel: Chuẩn bị một tệp Excel mẫu để chuyển đổi. Bạn có thể tạo một tệp đơn giản`.xlsx` tập tin để theo dõi.
## Nhập gói
Bây giờ chúng ta đã có đủ các điều kiện tiên quyết, đã đến lúc nhập các gói cần thiết vào dự án C# của bạn. Sau đây là cách thực hiện:
### Tạo một dự án mới
1. Mở Visual Studio và tạo một dự án mới. Chọn mẫu Console App để đơn giản hơn.
### Thêm tham chiếu đến Aspose.Cells
2. Nhấp chuột phải vào References trong Solution Explorer, chọn Add Reference và điều hướng đến Aspose.Cells assembly nếu nó không được thêm tự động. Bạn cũng có thể sử dụng NuGet Package Manager bằng cách chạy lệnh sau trong Package Manager Console:
```bash
Install-Package Aspose.Cells
```
### Nhập không gian tên
3.  Ở đầu trang của bạn`Program.cs` tệp, thêm lệnh sau bằng cách sử dụng:
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Bây giờ chúng ta đã hoàn tất việc thiết lập dự án!

Sau khi đã có nền tảng, chúng ta hãy chia nhỏ quy trình theo dõi chuyển đổi tài liệu thực tế thành các bước dễ hiểu. 
## Bước 1: Xác định thư mục của bạn
Bắt đầu bằng cách chỉ định các thư mục nơi chứa các tệp nguồn và tệp đầu ra của bạn. Sau đây là cách thực hiện:
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Document Directory";
```
 Hãy chắc chắn thay thế`"Your Document Directory"` với đường dẫn thực tế trên hệ thống của bạn. Điều này sẽ giúp định vị tệp của bạn dễ dàng.
## Bước 2: Tải Workbook
 Tiếp theo, bạn cần tải sổ làm việc Excel của mình bằng cách sử dụng`Workbook` lớp. Đây là cách thực hiện:
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
 Dòng mã này tạo ra một`Workbook` đối tượng cho phép chúng ta tương tác với tệp Excel mà chúng ta đã chỉ định.
## Bước 3: Thiết lập tùy chọn lưu PDF
Bây giờ, hãy thiết lập tùy chọn lưu PDF. Đây là nơi phép thuật theo dõi tiến trình bắt đầu. Bạn sẽ tạo một phiên bản`PdfSaveOptions` và gán lệnh gọi lại cho nó.
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
Bằng cách chỉ định một lệnh gọi lại tùy chỉnh (`TestPageSavingCallback`), chúng ta có thể triển khai logic riêng của mình để theo dõi tiến trình chuyển đổi trang.
## Bước 4: Lưu Workbook dưới dạng PDF
 Khi mọi thứ đã được thiết lập, đã đến lúc lưu sổ làm việc của bạn dưới dạng PDF. Sử dụng`Save` phương pháp của`Workbook` lớp như thế này:
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
Dòng này sẽ kích hoạt quá trình chuyển đổi và gọi phương thức gọi lại của chúng tôi khi các trang đang được xử lý.
## Bước 5: Triển khai lớp Callback
 Bây giờ chúng ta hãy tạo ra`TestPageSavingCallback` lớp. Đây là nơi bạn xác định những gì xảy ra khi bắt đầu và kết thúc việc lưu mỗi trang.
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Không xuất trang trước trang chỉ mục 2.
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // Không xuất trang sau trang chỉ mục 8.
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`Phương pháp này được gọi ngay trước khi một trang bắt đầu lưu. Ở đây, chúng tôi ghi lại quá trình bắt đầu lưu cho mỗi trang. Ngoài ra, chúng tôi có thể kiểm soát việc có xuất trang hay không. Trong trường hợp này, các trang trước chỉ mục 2 sẽ bị bỏ qua.
- `PageEndSaving`: Phương pháp này được gọi sau khi một trang đã được lưu. Nó cho phép bạn ghi lại thời điểm kết thúc lưu cho mỗi trang và kiểm soát xem có nên xử lý thêm các trang khác hay không. Trong ví dụ này, chúng tôi dừng sau chỉ mục trang 8.
## Phần kết luận
Xin chúc mừng! Bạn đã triển khai thành công hệ thống theo dõi tiến trình chuyển đổi tài liệu bằng Aspose.Cells cho .NET. Phương pháp này không chỉ cho phép bạn theo dõi quá trình chuyển đổi mà còn cho phép bạn kiểm soát những trang nào cần đưa vào hoặc loại trừ, giúp việc quản lý tài liệu của bạn hiệu quả hơn nhiều.
## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel theo cách lập trình.
### Làm thế nào tôi có thể nhận được bản dùng thử miễn phí Aspose.Cells?
 Bạn có thể tải xuống bản dùng thử miễn phí từ[Trang web Aspose](https://releases.aspose.com/).
### Có thể tùy chỉnh quá trình chuyển đổi không?
Có, khi sử dụng lệnh gọi lại, bạn có thể tùy chỉnh cách xử lý các trang trong quá trình chuyển đổi.
### Tôi có thể kiểm soát tên tập tin đầu ra không?
Hoàn toàn được! Bạn có thể chỉ định bất kỳ tên nào cho tệp đầu ra khi lưu sổ làm việc.
### Tôi có thể tìm thấy hỗ trợ cho Aspose.Cells ở đâu?
 Bạn có thể nhận được hỗ trợ bằng cách truy cập[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
