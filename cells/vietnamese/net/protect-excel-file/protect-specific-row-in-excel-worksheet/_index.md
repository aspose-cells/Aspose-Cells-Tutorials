---
"description": "Tìm hiểu cách bảo vệ các hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước dành riêng cho nhà phát triển."
"linktitle": "Bảo vệ hàng cụ thể trong bảng tính Excel"
"second_title": "Tài liệu tham khảo API Aspose.Cells cho .NET"
"title": "Bảo vệ hàng cụ thể trong bảng tính Excel"
"url": "/vi/net/protect-excel-file/protect-specific-row-in-excel-worksheet/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bảo vệ hàng cụ thể trong bảng tính Excel

## Giới thiệu

Trong thế giới phát triển nhanh như ngày nay, việc quản lý bảng tính hiệu quả quan trọng hơn bao giờ hết. Microsoft Excel là một công cụ không thể thiếu trong nhiều ngành và nghề. Tuy nhiên, khi chúng ta chia sẻ những tài liệu này, đặc biệt là trong môi trường cộng tác, việc bảo vệ thông tin cụ thể trong bảng tính trở nên rất quan trọng. Vậy, làm thế nào bạn có thể niêm phong một hàng trong Excel để ngăn chặn các sửa đổi không mong muốn? Vâng, nếu bạn đang làm việc với .NET, bạn thật may mắn! Aspose.Cells là một thư viện tuyệt vời để xử lý các tệp Excel theo chương trình, cho phép chúng ta bảo vệ các hàng cụ thể một cách hiệu quả.

## Điều kiện tiên quyết

Trước khi bắt đầu, bạn cần chuẩn bị một số thứ sau:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình. Bạn có thể sử dụng bất kỳ phiên bản nào hỗ trợ phát triển .NET.
2. Aspose.Cells cho .NET: Bạn sẽ cần phải cài đặt thư viện Aspose.Cells. Truy cập [liên kết này để tải xuống](https://releases.aspose.com/cells/net/) bản phát hành mới nhất.
3. Kiến thức cơ bản về .NET: Sự quen thuộc với C# và các khái niệm lập trình cơ bản sẽ hữu ích vì chúng ta sẽ làm việc với các đoạn mã.

Khi bạn đã chuẩn bị mọi thứ xong xuôi, chúng ta hãy bắt tay vào làm thôi!

## Nhập gói

Trước khi viết mã, chúng ta phải nhập các không gian tên Aspose.Cells cần thiết. Điều này chuẩn bị cho ứng dụng của chúng ta sử dụng các lớp và phương thức do thư viện Aspose.Cells cung cấp. Sau đây là những gì bạn cần làm:

### Thiết lập dự án của bạn

1. Tạo một dự án mới:
   - Mở Visual Studio và tạo một dự án Console Application mới. Dự án này sẽ lưu trữ mã thao tác Excel của chúng tôi.

2. Thêm tham chiếu Aspose.Cells:
   - Nhấp chuột phải vào dự án trong Solution Explorer, đi tới "Manage NuGet Packages" và tìm kiếm "Aspose.Cells". Nhấp để cài đặt.

3. Bao gồm các không gian tên cần thiết trong mã của bạn:
```csharp
using System.IO;
using Aspose.Cells;
```

Bây giờ chúng ta đã thiết lập mọi thứ, hãy bảo vệ một hàng cụ thể trong bảng tính Excel của chúng ta từng bước. Ví dụ chúng ta sẽ sử dụng khóa hàng đầu tiên, nhưng bạn có thể điều chỉnh nó cho bất kỳ hàng nào bạn muốn.

## Bước 1: Xác định thư mục tài liệu

Đầu tiên, chúng ta cần xác định một thư mục nơi chúng ta sẽ lưu trữ tệp Excel của mình. Sau đây là cách bạn thực hiện:

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // thay đổi theo con đường bạn mong muốn.

// Tạo thư mục nếu thư mục đó chưa có.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Thay thế `"YOUR DOCUMENT DIRECTORY"` với đường dẫn thực tế mà bạn muốn lưu tệp Excel mới của mình.

## Bước 2: Tạo một Workbook mới

Tiếp theo, chúng ta sẽ tạo một sổ làm việc mới bằng Aspose.Cells. Đây là khung làm việc trống để tạo bảng tính.

```csharp
// Tạo một bảng tính mới.
Workbook wb = new Workbook();
```

## Bước 3: Tạo và truy cập bảng tính

Bây giờ, chúng ta hãy truy cập vào bảng tính đầu tiên trong sổ làm việc để thực hiện những thay đổi cần thiết.

```csharp
// Tạo một đối tượng bảng tính và lấy trang tính đầu tiên.
Worksheet sheet = wb.Worksheets[0];
```

## Bước 4: Mở khóa tất cả các cột

Trước khi khóa bất kỳ hàng nào, chúng ta cần đảm bảo rằng tất cả các cột đều được mở khóa. Điều này giúp chúng ta có thể linh hoạt chỉ bảo vệ hàng cụ thể mà chúng ta mong muốn.

```csharp
// Xác định đối tượng kiểu.
Style style;
// Xác định đối tượng styleflag.
StyleFlag flag;
// Lặp qua tất cả các cột trong bảng tính và mở khóa chúng.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false; // Mở khóa cột
    flag = new StyleFlag();
    flag.Locked = true; // Đặt cờ thành true để khóa
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag); // Áp dụng phong cách
}
```

## Bước 5: Khóa hàng mong muốn

Bây giờ, đã đến lúc khóa hàng bạn muốn bảo vệ. Trong trường hợp này, chúng ta đang khóa hàng đầu tiên.

```csharp
// Nhận kiểu hàng đầu tiên.
style = sheet.Cells.Rows[0].Style;
// Khóa nó lại.
style.IsLocked = true;
// Tạo cờ.
flag = new StyleFlag();
// Thiết lập cài đặt khóa.
flag.Locked = true;
// Áp dụng kiểu cho hàng đầu tiên.
sheet.Cells.ApplyRowStyle(0, style, flag);
```

## Bước 6: Bảo vệ bảng tính

Sau khi khóa hàng mong muốn, chúng ta cần bật chế độ bảo vệ trên bảng tính. Đây chính là nơi phép thuật xảy ra!

```csharp
// Bảo vệ tờ giấy.
sheet.Protect(ProtectionType.All);
```

## Bước 7: Lưu sổ làm việc

Cuối cùng, đã đến lúc lưu tệp Excel mới của bạn. Bạn có thể chọn định dạng bạn muốn cho tệp Excel của mình.

```csharp
// Lưu tệp excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```

## Phần kết luận

Và bạn đã có nó! Bạn đã bảo vệ thành công một hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Chức năng này cực kỳ hữu ích cho các nhà phát triển và người dùng cần đảm bảo tính toàn vẹn của dữ liệu trong khi vẫn chia sẻ các tệp Excel của họ. Bây giờ bạn có thể tự tin chia sẻ bảng tính của mình trong khi bảo vệ thông tin quan trọng trong đó.

## Câu hỏi thường gặp

### Tôi có thể bảo vệ nhiều hàng bằng cùng một phương pháp không?  
Có, bạn có thể lặp lại quy trình khóa cho bất kỳ hàng nào khác theo cách tương tự như bạn đã làm với hàng đầu tiên.

### Tôi phải làm sao nếu muốn bảo vệ và mở khóa các ô cụ thể thay vì các hàng?  
Bạn có thể chọn từng ô và áp dụng kiểu khóa, tương tự như cách bạn khóa một hàng.

### Aspose.Cells có miễn phí sử dụng không?  
Aspose.Cells là một sản phẩm thương mại, nhưng bạn có thể dùng thử miễn phí [đây](https://releases.aspose.com/).

### Tôi có cần kết nối Internet để sử dụng Aspose.Cells không?  
Không, Aspose.Cells là thư viện .NET và có thể hoạt động ngoại tuyến sau khi bạn đã cài đặt.

### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?  
Đối với bất kỳ thắc mắc hoặc hỗ trợ nào, bạn có thể truy cập [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}