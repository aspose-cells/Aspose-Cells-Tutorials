---
"description": "Khám phá trong hướng dẫn này cách bảo vệ các hàng của bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước bằng C#."
"linktitle": "Bảo vệ hàng trong bảng tính Excel"
"second_title": "Tài liệu tham khảo API Aspose.Cells cho .NET"
"title": "Bảo vệ hàng trong bảng tính Excel"
"url": "/vi/net/protect-excel-file/protect-row-in-excel-worksheet/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bảo vệ hàng trong bảng tính Excel

## Giới thiệu

Khi làm việc với các trang tính Excel, thường cần phải bảo vệ các hàng cụ thể để duy trì tính toàn vẹn của dữ liệu. Cho dù bạn đang quản lý một dự án nhóm, giám sát báo cáo tài chính hay chia sẻ tài liệu, việc hạn chế quyền truy cập vào một số hàng nhất định có thể ngăn chặn những thay đổi không mong muốn. Trong hướng dẫn này, chúng ta sẽ khám phá cách tận dụng Aspose.Cells cho .NET để bảo vệ các hàng cụ thể trong một trang tính Excel. Vì vậy, hãy đội mũ lập trình của bạn và cùng khám phá thế giới thú vị của thao tác Excel bằng C#!

## Điều kiện tiên quyết

Trước khi bắt đầu phần thực hành, hãy đảm bảo bạn đã thiết lập mọi thứ. Sau đây là một số điều kiện tiên quyết:

1. Aspose.Cells cho .NET: Tải xuống thư viện từ [Trang web Aspose](https://releases.aspose.com/cells/net/). Đảm bảo bạn có phiên bản mới nhất cho tất cả các tính năng mới và sửa lỗi.
2. Visual Studio: Môi trường phát triển tích hợp (IDE) như Visual Studio (Community, Professional hoặc Enterprise) sẽ giúp bạn biên dịch và chạy mã C# hiệu quả.
3. .NET Framework: Bạn sẽ cần phiên bản .NET Framework tương thích. Aspose.Cells hỗ trợ nhiều phiên bản, vì vậy hãy đảm bảo phiên bản của bạn được cập nhật. 
4. Kiến thức cơ bản về C#: Hiểu biết cơ bản về C# sẽ có lợi khi chúng ta viết mã trong hướng dẫn này.
5. Tài liệu tham khảo: Làm quen với [Aspose.Cells cho tài liệu .NET](https://reference.aspose.com/cells/net/) để biết thêm chi tiết về các phương pháp và lớp được sử dụng.

## Nhập gói

Bước đầu tiên trong hành trình của chúng ta là nhập các gói cần thiết vào dự án C# của chúng ta. Aspose.Cells hoạt động thông qua một tập hợp các lớp mà chúng ta cần đưa vào:

```csharp
using System.IO;
using Aspose.Cells;
```

Bây giờ chúng ta đã nhập các gói cần thiết, hãy cùng thực hiện các bước để tạo một bảng tính Excel và bảo vệ một hàng cụ thể. 

## Bước 1: Xác định thư mục

Trong bước này, chúng ta sẽ chỉ định vị trí lưu tệp Excel của mình. Điều quan trọng là phải đảm bảo rằng thư mục này tồn tại, nếu không, chúng ta sẽ tạo nó theo chương trình nếu cần.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Thay thế bằng đường dẫn tài liệu của bạn
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Trong mã này, thay thế `YOUR DOCUMENT DIRECTORY` bằng đường dẫn thực tế mà bạn muốn lưu tệp Excel của mình.

## Bước 2: Tạo một Workbook mới

Tiếp theo, chúng ta sẽ tạo một sổ làm việc mới, nơi diễn ra mọi thao tác. Đây là bước cơ bản, giống như đặt nền móng trước khi xây dựng ngôi nhà mơ ước của bạn.

```csharp
Workbook wb = new Workbook();
```
Dòng này khởi tạo một phiên bản mới của `Workbook` lớp, tạo ra một bài tập mới để chúng ta thực hiện.

## Bước 3: Truy cập vào Bảng tính

Sau khi tạo xong sổ làm việc, chúng ta hãy bắt tay vào làm bảng tính đầu tiên. Hãy nhớ rằng, một tệp Excel có thể chứa nhiều trang tính, vì vậy việc chọn đúng trang tính là rất quan trọng.

```csharp
Worksheet sheet = wb.Worksheets[0]; // Truy cập trang tính đầu tiên
```

## Bước 4: Mở khóa tất cả các cột

Trước khi khóa một hàng cụ thể, tốt nhất là mở khóa tất cả các cột trước. Điều này cho phép chúng ta kiểm soát dữ liệu nào vẫn có thể chỉnh sửa sau này.

```csharp
Style style;
StyleFlag flag;

// Lặp qua tất cả các cột và mở khóa chúng
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
Vòng lặp này lặp qua 256 cột đầu tiên, mở khóa từng cột để đảm bảo quyền chỉnh sửa mặc định.

## Bước 5: Khóa hàng cụ thể

Bây giờ, chúng ta sẽ nhắm mục tiêu vào hàng đầu tiên của bảng tính để khóa. Bước này đảm bảo rằng người dùng không thể thực hiện các thay đổi trái phép đối với dữ liệu quan trọng có trong hàng này.

```csharp
style = sheet.Cells.Rows[0].Style; // Lấy kiểu của hàng đầu tiên
style.IsLocked = true; // Khóa hàng
flag = new StyleFlag();
flag.Locked = true; // Đặt cờ khóa
sheet.Cells.ApplyRowStyle(0, style, flag); // Áp dụng kiểu cho hàng đầu tiên
```
Ở đây, chúng ta lấy kiểu cho hàng đầu tiên, đánh dấu là đã khóa và áp dụng kiểu khóa. Điều này tương tự như việc khóa một ngăn kéo quan trọng—điều cần thiết để bảo mật thông tin nhạy cảm!

## Bước 6: Bảo vệ tờ giấy

Với hàng của chúng ta bị khóa, hãy thực hiện thêm bước đó và bảo vệ hoàn toàn bảng tính. Điều này sẽ thực thi khóa trên tất cả các chức năng được xác định trong `ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); // Bảo vệ tờ giấy với tất cả các tính năng
```
Bằng cách áp dụng biện pháp bảo vệ này, người dùng không thể chỉnh sửa hàng đã khóa hoặc thực hiện bất kỳ thay đổi nào có thể ảnh hưởng đến các khu vực bị khóa.

## Bước 7: Lưu sổ làm việc

Bước cuối cùng là lưu sổ làm việc. Đây là nơi mọi công sức của chúng ta được đền đáp, và chúng ta có thể thấy bảng tính được bảo vệ tuyệt đẹp của mình trở nên sống động!

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Đảm bảo tên tệp đã lưu và định dạng phù hợp với yêu cầu của bạn. Trong trường hợp này, chúng tôi sẽ lưu dưới dạng định dạng Excel cũ hơn (Excel 97-2003).

## Phần kết luận

Và bạn đã có nó! Bạn đã học thành công cách bảo vệ một hàng cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Chỉ với một vài dòng mã, bạn không chỉ tạo được một sổ làm việc mà còn quản lý để bảo mật thông tin nhạy cảm, đảm bảo rằng các tệp Excel của bạn vẫn nguyên vẹn và đáng tin cậy. Cho dù đó là báo cáo tài chính, bảng điểm danh hay kế hoạch dự án hợp tác, việc bảo vệ dữ liệu quan trọng là điều cần thiết. 

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là một thư viện mạnh mẽ dành cho .NET cho phép người dùng tạo, thao tác và chuyển đổi các tệp Excel theo chương trình.

### Tôi có thể bảo vệ nhiều hàng cùng lúc bằng Aspose.Cells không?
Có, bạn có thể mở rộng kỹ thuật khóa bằng cách lặp qua nhiều hàng và áp dụng các thay đổi kiểu tương tự cho từng hàng.

### Có cách nào để mở khóa các hàng sau khi bảo vệ không?
Có, trước tiên bạn có thể bỏ bảo vệ trang tính rồi sau đó điều chỉnh `IsLocked` thuộc tính của các hàng mong muốn, sau đó áp dụng lại biện pháp bảo vệ.

### Aspose.Cells có hỗ trợ các định dạng khác ngoài Excel không?
Chắc chắn rồi! Aspose.Cells có thể chuyển đổi và lưu sổ làm việc thành nhiều định dạng khác nhau, bao gồm CSV, PDF và HTML.

### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
Bạn có thể ghé thăm [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để được hỗ trợ và hướng dẫn cộng đồng.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}