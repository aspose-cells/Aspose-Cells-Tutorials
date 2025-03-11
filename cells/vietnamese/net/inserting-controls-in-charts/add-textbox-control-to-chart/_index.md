---
title: Thêm điều khiển TextBox vào biểu đồ
linktitle: Thêm điều khiển TextBox vào biểu đồ
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm TextBox vào biểu đồ trong Excel bằng Aspose.Cells cho .NET. Nâng cao khả năng trực quan hóa dữ liệu của bạn một cách dễ dàng.
weight: 12
url: /vi/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm điều khiển TextBox vào biểu đồ

## Giới thiệu

Tạo biểu đồ động và hấp dẫn trực quan trong Excel là một cách tuyệt vời để biểu diễn dữ liệu hiệu quả. Một tính năng tiện lợi mà bạn có thể sử dụng là thêm TextBox vào biểu đồ. Với Aspose.Cells cho .NET, nhiệm vụ này trở nên dễ dàng và thú vị! Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước trong quy trình tích hợp TextBox vào biểu đồ của mình. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, hướng dẫn này sẽ cung cấp cho bạn tất cả các công cụ bạn cần để cải thiện biểu đồ Excel của mình. Vậy, bạn đã sẵn sàng để bắt đầu chưa?

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, bạn cần chuẩn bị một số điều sau:

- Hiểu biết cơ bản về C#: Nắm vững cơ bản về lập trình C# sẽ hữu ích. Đừng lo lắng; bạn không cần phải là chuyên gia, chỉ cần thoải mái điều hướng cú pháp.
-  Thư viện Aspose.Cells đã cài đặt: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells for .NET. Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/) nếu bạn chưa làm như vậy.
- Visual Studio: Điều cần thiết là phải quen thuộc với Visual Studio hoặc bất kỳ IDE nào mà bạn muốn sử dụng cho .NET framework.
- Tệp Excel hiện có: Đối với ví dụ này, chúng ta sẽ làm việc với tệp Excel hiện có có tên "sampleAddingTextBoxControlInChart.xls". Bạn có thể tạo một tệp hoặc tải xuống mẫu.

Bây giờ chúng ta đã có mọi thứ, hãy bắt đầu phần viết mã!

## Nhập gói

Trước tiên, chúng ta cần import các namespace Aspose.Cells cần thiết vào dự án C# của mình. Bạn có thể dễ dàng thực hiện việc này bằng cách thêm các dòng sau vào đầu tệp mã của mình:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Bước 1: Xác định thư mục nguồn và thư mục đầu ra của bạn

Trước khi bắt đầu làm việc với tệp Excel, điều quan trọng là phải xác định tệp đầu vào của bạn nằm ở đâu và bạn muốn lưu tệp đầu ra ở đâu. Điều này giúp duy trì tổ chức cho dự án của bạn.

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";

// Thư mục đầu ra
string outputDir = "Your Output Directory";
```
 Thay thế`"Your Document Directory"` Và`"Your Output Directory"` với các đường dẫn thực tế trên hệ thống của bạn.

## Bước 2: Mở tệp Excel hiện có

Tiếp theo, chúng ta cần mở tệp Excel có chứa biểu đồ mà chúng ta muốn sửa đổi. Điều này sẽ cho phép chúng ta lấy biểu đồ và thực hiện thay đổi.

```csharp
// Mở tệp hiện có.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Dòng này khởi tạo một đối tượng Workbook mới với tệp được chỉ định của chúng ta.

## Bước 3: Truy cập Biểu đồ trong Bảng tính

Vì biểu đồ trong Excel được lưu trữ trong một bảng tính, trước tiên chúng ta cần truy cập vào bảng tính và sau đó lấy biểu đồ mong muốn. Đối với ví dụ này, chúng ta sẽ truy cập vào biểu đồ đầu tiên trong bảng tính đầu tiên.

```csharp
// Nhận biểu đồ thiết kế ở trang đầu tiên.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Bằng cách thay đổi giá trị chỉ mục, bạn có thể chọn các bảng tính hoặc biểu đồ khác nhau nếu tệp của bạn có nhiều hơn.

## Bước 4: Thêm một hộp văn bản mới vào biểu đồ

Bây giờ, chúng ta đã sẵn sàng để thêm TextBox. Chúng ta sẽ chỉ định vị trí và kích thước của nó khi tạo nó.

```csharp
// Thêm hộp văn bản mới vào biểu đồ.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Trong lệnh này, các tham số xác định vị trí (x, y) và kích thước (chiều rộng, chiều cao) của TextBox trong biểu đồ. Điều chỉnh các giá trị này dựa trên nhu cầu bố cục cụ thể của bạn.

## Bước 5: Thiết lập Văn bản cho Hộp văn bản

Khi TextBox đã vào đúng vị trí, đã đến lúc điền nội dung vào đó. Bạn có thể thêm bất kỳ văn bản nào mà bạn cho là cần thiết cho biểu đồ của mình.

```csharp
// Điền vào văn bản.
textbox0.Text = "Sales By Region";
```
Bạn có thể thay thế "Doanh số theo khu vực" bằng bất kỳ văn bản nào có liên quan đến dữ liệu của bạn.

## Bước 6: Điều chỉnh Thuộc tính TextBox

Bây giờ, hãy làm cho TextBox của chúng ta trông đẹp mắt! Bạn có thể tùy chỉnh nhiều thuộc tính khác nhau như màu phông chữ, kích thước và kiểu chữ.

```csharp
// Đặt màu phông chữ.
textbox0.Font.Color = Color.Maroon; // Thay đổi sang màu bạn mong muốn

// Đặt phông chữ thành chữ đậm.
textbox0.Font.IsBold = true;

// Đặt kích thước phông chữ.
textbox0.Font.Size = 14;

// Đặt thuộc tính phông chữ thành in nghiêng.
textbox0.Font.IsItalic = true;
```

Mỗi dòng này sẽ thay đổi giao diện của văn bản bên trong TextBox của bạn, tăng khả năng hiển thị và hấp dẫn.

## Bước 7: Định dạng giao diện hộp văn bản

Việc định dạng nền và đường viền của TextBox cũng rất quan trọng. Điều này làm cho nó nổi bật trên biểu đồ.

```csharp
// Lấy định dạng điền của hộp văn bản.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Lấy kiểu định dạng dòng của hộp văn bản.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Thiết lập độ dày của đường.
lineformat.Weight = 2;

// Đặt kiểu gạch ngang thành dạng liền.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Các tùy chọn này cho phép bạn thiết lập phần nền của TextBox và tùy chỉnh đường viền của nó.

## Bước 8: Lưu tệp Excel đã sửa đổi

Bước cuối cùng là lưu các thay đổi bạn đã thực hiện vào một tệp Excel mới. Điều này sẽ đảm bảo tệp gốc của bạn không bị thay đổi.

```csharp
// Lưu tệp excel.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Thay thế`"outputAddingTextBoxControlInChart.xls"` với bất kỳ tên tệp nào bạn thích.

## Phần kết luận

Xin chúc mừng! Bạn đã thêm thành công điều khiển TextBox vào biểu đồ bằng Aspose.Cells cho .NET. Thay đổi đơn giản nhưng hiệu quả này có thể giúp biểu đồ của bạn nhiều thông tin hơn và hấp dẫn hơn về mặt thị giác. Biểu diễn dữ liệu là chìa khóa để giao tiếp hiệu quả và với các công cụ như Aspose, bạn có khả năng nâng cao bản trình bày đó với nỗ lực tối thiểu.

## Câu hỏi thường gặp

### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện mạnh mẽ để tạo, thao tác và chuyển đổi các tệp Excel mà không cần phải dựa vào Microsoft Excel.

### Tôi có thể thêm nhiều TextBox vào một biểu đồ không?
Có! Bạn có thể thêm bao nhiêu TextBox tùy ý bằng cách lặp lại các bước tạo TextBox với các vị trí khác nhau.

### Aspose.Cells có miễn phí sử dụng không?
Aspose.Cells là một thư viện trả phí, nhưng bạn có thể tải xuống phiên bản dùng thử miễn phí từ[đây](https://releases.aspose.com/).

### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?
 Bạn có thể truy cập tài liệu toàn diện[đây](https://reference.aspose.com/cells/net/).

### Tôi có thể nhận được hỗ trợ như thế nào nếu gặp vấn đề?
 Bạn có thể tìm kiếm sự hỗ trợ thông qua diễn đàn hỗ trợ Aspose[đây](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
