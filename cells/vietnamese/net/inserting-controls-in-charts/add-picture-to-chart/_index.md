---
title: Thêm hình ảnh vào biểu đồ
linktitle: Thêm hình ảnh vào biểu đồ
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách dễ dàng thêm hình ảnh vào biểu đồ Excel bằng Aspose.Cells cho .NET. Cải thiện biểu đồ và bài thuyết trình của bạn chỉ trong vài bước đơn giản.
weight: 11
url: /vi/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm hình ảnh vào biểu đồ

## Giới thiệu

Bạn có thấy chán những biểu đồ nhàm chán thiếu nét cá nhân không? Bạn có muốn tìm hiểu cách làm cho hình ảnh Excel của mình hấp dẫn hơn bằng cách thêm hình ảnh không? Vâng, bạn thật may mắn! Trong hướng dẫn này, chúng ta sẽ khám phá thế giới của Aspose.Cells dành cho .NET và tìm hiểu cách thêm hình ảnh vào biểu đồ trong Excel. Vậy thì, hãy lấy tách cà phê yêu thích của bạn và bắt đầu thôi!

## Điều kiện tiên quyết

Trước khi đi sâu vào phần cốt lõi của việc viết mã, bạn cần có một số điều kiện tiên quyết để có thể thực hiện suôn sẻ:

- Visual Studio: Đây là nơi bạn sẽ viết và chạy mã .NET của mình. Hãy đảm bảo rằng bạn đã cài đặt nó.
-  Aspose.Cells cho .NET: Bạn sẽ cần thư viện này để làm việc với các tệp Excel. Bạn có thể[tải xuống ở đây](https://releases.aspose.com/cells/net/).
- Hiểu biết cơ bản về C#: Mặc dù tôi sẽ hướng dẫn bạn viết mã, nhưng việc nắm được những kiến thức cơ bản về C# sẽ giúp bạn hiểu rõ hơn.

### Các bước cài đặt

1. Cài đặt Aspose.Cells: Bạn có thể thêm Aspose.Cells vào dự án Visual Studio của mình thông qua NuGet Package Manager. Thực hiện bằng cách điều hướng đến Tools > NuGet Package Manager > Manage NuGet Packages for Solution và tìm kiếm “Aspose.Cells.” Nhấp vào Install.
2. Thiết lập dự án của bạn: Tạo một dự án ứng dụng bảng điều khiển C# mới trong Visual Studio.

## Nhập gói

Sau khi bạn đã thiết lập mọi thứ, bước tiếp theo là nhập các gói cần thiết vào dự án của bạn. Sau đây là cách thực hiện:

### Nhập các không gian tên bắt buộc

Ở đầu tệp mã C#, bạn sẽ cần nhập các không gian tên sau:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Điều này cho chương trình của bạn biết, "Này! Tôi sẽ sử dụng những tính năng thú vị này từ Aspose.Cells."

Bây giờ chúng ta đã có đủ các điều kiện tiên quyết, hãy chia nhỏ quy trình thành các bước nhỏ hơn. 

## Bước 1: Xác định thư mục của bạn

Trước tiên, chúng ta cần thiết lập đường dẫn cho các tệp đầu vào và đầu ra. Bước này rất quan trọng vì chúng ta cần biết tìm tệp Excel hiện tại ở đâu và lưu tệp đã sửa đổi ở đâu.

```csharp
//Thư mục nguồn
string sourceDir = "Your Document Directory/";

//Thư mục đầu ra
string outputDir = "Your Output Directory/";
```

 Thay thế`Your Document Directory` Và`Your Output Directory` với đường dẫn thực tế trên máy tính của bạn. 

## Bước 2: Tải Workbook hiện có

Bây giờ, hãy tải tệp Excel hiện có mà chúng ta muốn thêm hình ảnh vào biểu đồ.

```csharp
// Mở tệp hiện có.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Mã này mở sổ làm việc, chuẩn bị sẵn sàng để chỉnh sửa.

## Bước 3: Chuẩn bị luồng hình ảnh

Trước khi thêm hình ảnh, chúng ta cần đọc hình ảnh mà chúng ta muốn chèn vào biểu đồ. 

```csharp
// Tải tệp hình ảnh vào luồng.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Hãy đảm bảo rằng bạn đã lưu ảnh vào thư mục đã chỉ định.

## Bước 4: Nhắm mục tiêu vào biểu đồ

Bây giờ, hãy chỉ định biểu đồ nào chúng ta sẽ thêm hình ảnh vào. Trong ví dụ này, chúng ta sẽ nhắm mục tiêu vào biểu đồ đầu tiên trên bảng tính đầu tiên.

```csharp
// Lấy biểu đồ thiết kế ở trang thứ hai.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Bạn có thể truy cập bất kỳ bảng tính nào bằng cách thay đổi mục lục cho phù hợp.

## Bước 5: Thêm hình ảnh vào biểu đồ

Sau khi đã chọn biểu đồ, đã đến lúc thêm hình ảnh! 

```csharp
// Thêm hình ảnh mới vào biểu đồ.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Đây,`50` Và`50` là tọa độ X và Y nơi hình ảnh sẽ được đặt và`200` là chiều rộng và chiều cao của hình ảnh.

## Bước 6: Tùy chỉnh Định dạng Dòng của Hình ảnh

Bạn muốn thêm chút phong cách cho bức ảnh của mình? Bạn có thể tùy chỉnh đường viền của bức ảnh! Sau đây là cách thực hiện:

```csharp
// Lấy kiểu định dạng dòng của hình ảnh.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Thiết lập kiểu gạch ngang.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Thiết lập độ dày của đường.
lineformat.Weight = 4;    
```

Đoạn mã này cho phép bạn chọn giao diện và độ dày của đường viền. Chọn bất kỳ kiểu nào phù hợp với bài thuyết trình của bạn!

## Bước 7: Lưu sổ làm việc đã sửa đổi

Sau tất cả những công sức bỏ ra, hãy lưu lại những sửa đổi của bạn bằng cách thực thi dòng mã sau:

```csharp
// Lưu tệp excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Bây giờ hình ảnh của bạn đã được tích hợp thành công vào biểu đồ và tệp đầu ra đã sẵn sàng để xem!

## Bước 8: Chỉ ra thành công

Cuối cùng, bạn có thể thêm một tin nhắn đơn giản để xác nhận rằng thao tác của bạn đã thành công:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Phần kết luận

Trong hướng dẫn này, chúng tôi đã khám phá cách thêm một chút cá tính vào biểu đồ Excel của bạn bằng cách thêm hình ảnh bằng Aspose.Cells cho .NET. Chỉ với một vài bước đơn giản, bạn có thể nâng tầm bài thuyết trình của mình từ tầm thường thành đáng nhớ. Vậy, bạn còn chờ gì nữa? Hãy thử và để biểu đồ của bạn tỏa sáng!

## Câu hỏi thường gặp

### Tôi có thể thêm nhiều hình ảnh vào một biểu đồ không?
 Vâng! Bạn có thể gọi`AddPictureInChart` phương pháp này nhiều lần để thêm nhiều hình ảnh tùy ý.

### Aspose.Cells hỗ trợ những định dạng hình ảnh nào?
Aspose.Cells hỗ trợ nhiều định dạng hình ảnh, bao gồm PNG, JPEG, BMP và GIF.

### Tôi có thể tùy chỉnh vị trí của hình ảnh không?
 Chắc chắn rồi! Tọa độ X và Y trong`AddPictureInChart` phương pháp cho phép định vị chính xác.

### Aspose.Cells có miễn phí sử dụng không?
Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để có đầy đủ tính năng, cần phải có giấy phép. Bạn có thể tìm thấy giá[đây](https://purchase.aspose.com/buy).

### Tôi có thể tìm thêm ví dụ ở đâu?
 Kiểm tra các[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để biết thêm ví dụ và chức năng chi tiết hơn.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
