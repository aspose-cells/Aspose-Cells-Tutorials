---
title: Xóa Name Range trong Excel
linktitle: Xóa Name Range trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách xóa các phạm vi được đặt tên trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước chi tiết.
weight: 11
url: /vi/net/excel-managing-named-ranges/remove-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xóa Name Range trong Excel

## Giới thiệu
Excel đã trở thành công cụ chính trong quản lý và phân tích dữ liệu cho nhiều cá nhân và tổ chức. Cho dù bạn là một nhà phân tích dữ liệu dày dạn kinh nghiệm hay chỉ là người thích sắp xếp dữ liệu của mình, thì việc thành thạo Excel là điều cần thiết. Hôm nay, chúng ta sẽ đi sâu vào một tính năng cụ thể nhưng mạnh mẽ: xóa các phạm vi được đặt tên bằng Aspose.Cells cho .NET. Hướng dẫn này sẽ hướng dẫn bạn từng bước để thực hiện điều này một cách hiệu quả. Vậy thì, hãy xắn tay áo lên và bắt đầu thôi!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã thực tế, bạn cần chuẩn bị một số thứ sau:

### Thiết lập môi trường .NET

Để làm việc với Aspose.Cells for .NET một cách liền mạch, hãy đảm bảo bạn có những điều sau:

1.  Visual Studio: Tải xuống và cài đặt Visual Studio (Phiên bản cộng đồng hoàn toàn ổn) mà bạn có thể tìm thấy trên[Trang web Visual Studio](https://visualstudio.microsoft.com/).
2. .NET Framework: Đảm bảo bạn đang sử dụng phiên bản .NET Framework phù hợp. Aspose.Cells hỗ trợ .NET Framework 4.0 trở lên.
3. Thư viện Aspose.Cells: Bạn cần tải xuống và tham chiếu thư viện Aspose.Cells cho .NET trong ứng dụng của mình. Bạn có thể tìm thấy gói có thể tải xuống[đây](https://releases.aspose.com/cells/net/).

### Hiểu biết cơ bản về C#

Bạn sẽ cần hiểu biết cơ bản về lập trình C#. Điều này sẽ giúp bạn nắm bắt được các đoạn mã mà chúng ta sẽ thảo luận.

### Truy cập vào các tập tin Excel

Đảm bảo bạn có tệp Excel để thử nghiệm. Nếu không, bạn có thể tạo tệp nhanh bằng Microsoft Excel.

## Nhập gói

Bây giờ chúng ta đã có các điều kiện tiên quyết, hãy nhập các gói chúng ta cần vào dự án của mình. Mở Visual Studio và tạo một ứng dụng bảng điều khiển mới. Sau đó, bao gồm không gian tên sau vào chương trình của bạn:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Thiết lập này cho phép bạn khai thác các chức năng do Aspose.Cells cung cấp để thao tác trên các bảng tính Excel một cách dễ dàng.

## Bước 1: Thiết lập thư mục đầu ra

Trước hết, chúng ta cần xác định nơi lưu tệp đầu ra. Điều này rất quan trọng vì nó tránh nhầm lẫn về nơi lưu tệp của bạn sau này.

```csharp
// Thư mục đầu ra
string outputDir = "Your Document Directory Here\\";
```

 Thay thế`"Your Document Directory Here\\"`bằng đường dẫn trên máy tính nơi bạn muốn lưu tệp của mình.

## Bước 2: Khởi tạo một Workbook mới

Làm thế nào để bắt đầu với một bảng mới? Tất nhiên là bằng cách tạo một bảng tính mới! Bảng tính này sẽ đóng vai trò như một trang giấy trắng của chúng ta.

```csharp
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
```

Dòng mã này tạo ra một bảng tính mới mà chúng ta có thể thao tác.

## Bước 3: Truy cập Bộ sưu tập bảng tính

Mỗi sổ làm việc bao gồm một hoặc nhiều trang tính. Để làm việc trong một trang tính cụ thể, chúng ta cần truy cập vào bộ sưu tập này.

```csharp
// Lấy tất cả các bài tập trong sách.
WorksheetCollection worksheets = workbook.Worksheets;
```

Ở đây, chúng tôi đã lấy lại tất cả các bài tập có trong sổ làm việc mới của mình.

## Bước 4: Chọn trang tính đầu tiên

Tiếp theo, chúng ta muốn hoạt động trong bảng tính đầu tiên—điểm bắt đầu mặc định trong nhiều trường hợp.

```csharp
// Nhận bài tập đầu tiên trong bộ sưu tập bài tập.
Worksheet worksheet = workbook.Worksheets[0];
```

Đoạn mã này cho phép chúng ta chọn trang tính đầu tiên một cách dễ dàng.

## Bước 5: Tạo phạm vi được đặt tên

Bây giờ, chúng ta hãy tạo một phạm vi được đặt tên, đây là một phần thiết yếu của hướng dẫn này. Điều này sẽ cho phép chúng ta minh họa cách xóa một phạm vi được đặt tên sau này.

```csharp
// Tạo một dãy ô.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Đặt tên cho phạm vi.
range1.Name = "FirstRange";
```

Tại đây, chúng ta xác định một phạm vi từ ô E12 đến I12 và đặt tên là “FirstRange”.

## Bước 6: Định dạng phạm vi được đặt tên

Để chứng minh Aspose.Cells linh hoạt như thế nào, chúng ta hãy thêm một số định dạng vào phạm vi được đặt tên của mình.

```csharp
// Đặt đường viền phác thảo theo phạm vi.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

Chúng tôi đang thêm đường viền màu xanh navy trung bình xung quanh sản phẩm để tăng tính hấp dẫn về mặt thị giác.

## Bước 7: Chèn dữ liệu vào phạm vi

Tiếp theo, chúng ta có thể điền một số dữ liệu vào ô để nó hoạt động.

```csharp
// Nhập một số dữ liệu với một số định dạng vào một số ô trong phạm vi.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

Ở bước này, chúng ta đặt từ "Test" vào ô E12 và số 123 vào ô I12.

## Bước 8: Tạo một phạm vi được đặt tên khác

Để minh họa rõ hơn quan điểm của mình, chúng ta sẽ tạo một phạm vi được đặt tên khác tương tự như phạm vi đầu tiên.

```csharp
//Tạo một dãy ô khác.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Đặt tên cho phạm vi.
range2.Name = "SecondRange";
```

Bây giờ chúng ta có một phạm vi tên khác có tên là "SecondRange" có thể sử dụng.

## Bước 9: Sao chép Phạm vi đầu tiên vào Phạm vi thứ hai

Chúng ta hãy cùng xem cách sử dụng phạm vi thứ hai bằng cách sao chép dữ liệu từ phạm vi đầu tiên.

```csharp
// Sao chép phạm vi đầu tiên vào phạm vi thứ hai.
range2.Copy(range1);
```

Với bước này, chúng ta đã sao chép dữ liệu từ "FirstRange" thành "SecondRange" một cách hiệu quả.

## Bước 10: Xóa phạm vi được đặt tên

Bây giờ đến phần nổi bật của hướng dẫn của chúng tôi: xóa phạm vi được đặt tên. Đây là nơi mọi thứ kết hợp lại với nhau.

```csharp
// Xóa phạm vi được đặt tên trước đó (range1) cùng với nội dung của nó.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Dòng này xóa nội dung của phạm vi chúng ta muốn xóa, đảm bảo rằng chúng ta không để lại dấu vết nào!

## Bước 11: Xóa phạm vi được đặt tên khỏi trang tính

Bước cuối cùng quan trọng là xóa phạm vi được đặt tên khỏi bộ sưu tập tên của bảng tính.

```csharp
worksheets.Names.RemoveAt(0);
```

Thao tác này sẽ xóa vùng có tên “FirstRange” khỏi bảng tính.

## Bước 12: Lưu sổ làm việc

Cuối cùng nhưng không kém phần quan trọng, hãy lưu lại công việc của mình. 

```csharp
// Lưu tệp Excel.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Lệnh này lưu sổ làm việc của bạn với những thay đổi chúng ta đã thực hiện—đây là nơi lưu giữ mọi công sức của bạn!

## Bước 13: Xác nhận thực hiện thành công

Để kết thúc mọi việc một cách gọn gàng, bạn có thể muốn đưa ra thông báo thành công vào bảng điều khiển.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Điều này thông báo cho bạn rằng toàn bộ hoạt động đã hoàn tất mà không có trục trặc nào!

## Phần kết luận

Bằng cách làm theo hướng dẫn này, bạn đã học cách thao tác các phạm vi được đặt tên trong Excel bằng Aspose.Cells cho .NET. Bạn đã tạo các phạm vi, điền dữ liệu vào chúng, sao chép nội dung của chúng và cuối cùng xóa chúng trong khi đảm bảo tệp Excel của bạn vẫn được sắp xếp và sạch sẽ. Excel, giống như một quán cà phê nhộn nhịp, phát triển mạnh mẽ nhờ sự sắp xếp. Vì vậy, cho dù bạn đang quản lý dữ liệu cho báo cáo hay làm đẹp bảng ngân sách cá nhân của mình, việc thành thạo các phạm vi được đặt tên có thể giúp bạn pha chế một số giải pháp hiệu quả. 

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET được thiết kế để xử lý các tệp Excel theo chương trình.

### Tôi có thể xóa nhiều phạm vi được đặt tên cùng một lúc không?
Có, bạn có thể lặp qua bộ sưu tập các phạm vi được đặt tên và xóa chúng khi cần.

### Có phiên bản dùng thử không?
 Có, bạn có thể tải xuống bản dùng thử miễn phí của Aspose.Cells[đây](https://releases.aspose.com/).

### Aspose.Cells hỗ trợ những ngôn ngữ lập trình nào?
Nó chủ yếu hỗ trợ các ngôn ngữ .NET như C# và VB.NET, cùng nhiều ngôn ngữ khác.

### Tôi có thể tìm kiếm sự hỗ trợ ở đâu nếu gặp vấn đề?
 Bạn có thể ghé thăm[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để được trợ giúp giải đáp mọi thắc mắc.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
