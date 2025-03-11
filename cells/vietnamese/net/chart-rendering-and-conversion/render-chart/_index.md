---
title: Biểu đồ kết xuất
linktitle: Biểu đồ kết xuất
second_title: API xử lý Excel Aspose.Cells .NET
description: Khám phá cách tạo biểu đồ trong .NET bằng Aspose.Cells. Làm theo hướng dẫn từng bước của chúng tôi để tạo hình ảnh tuyệt đẹp một cách dễ dàng.
weight: 10
url: /vi/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Biểu đồ kết xuất

## Giới thiệu

Biểu đồ là một yếu tố thiết yếu trong việc trình bày và phân tích dữ liệu, giúp thông tin phức tạp dễ hiểu hơn. Nếu bạn đang làm việc với .NET và cần tạo biểu đồ theo chương trình, Aspose.Cells là một thư viện mạnh mẽ cung cấp các tính năng trực quan và nâng cao để xử lý các tệp và biểu đồ Excel. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình kết xuất biểu đồ bằng Aspose.Cells cho .NET. Hãy sẵn sàng để khám phá hướng dẫn chi tiết này, được thiết kế để hấp dẫn và dễ làm theo!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, hãy đảm bảo bạn đã chuẩn bị mọi thứ. Sau đây là những gì bạn cần:

1. Môi trường .NET: Đảm bảo bạn đã thiết lập môi trường phát triển .NET. Bạn có thể sử dụng Visual Studio hoặc bất kỳ IDE nào khác hỗ trợ .NET.
2.  Aspose.Cells cho .NET: Bạn cần cài đặt thư viện Aspose.Cells. Bạn có thể tải xuống từ[Trang phát hành của Aspose](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Việc quen thuộc với lập trình C# sẽ giúp bạn hiểu các ví dụ tốt hơn, nhưng đừng lo nếu bạn là người mới—hướng dẫn này sẽ giải thích mọi thứ từng bước một!

## Nhập gói

Bước đầu tiên trong hành trình mã hóa của bạn là nhập các gói cần thiết. Mở dự án của bạn trong IDE và thêm không gian tên sau:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào chức năng do thư viện Aspose.Cells cung cấp, cho phép bạn tạo và thao tác biểu đồ một cách liền mạch.


Bây giờ chúng ta đã đề cập đến các điều kiện tiên quyết và nhập, hãy cùng đi sâu vào chi tiết của việc kết xuất biểu đồ! Chúng ta sẽ chia nhỏ thành các bước rõ ràng và dễ quản lý.

## Bước 1: Thiết lập thư mục đầu ra của bạn

Trước khi tạo sổ làm việc và biểu đồ, chúng ta cần thiết lập nơi lưu kết quả đầu ra. Theo cách này, khi biểu đồ được tạo, bạn sẽ biết chính xác nơi tìm thấy nó.

```csharp
string outputDir = "Your Output Directory"; // Chỉ định thư mục đầu ra ở đây.
```

Hãy thay thế "Thư mục đầu ra" bằng đường dẫn mà bạn muốn lưu hình ảnh biểu đồ của mình.

## Bước 2: Tạo một Workbook

Tiếp theo, chúng ta sẽ thiết lập một sổ làm việc mới. Đây chính là nơi mọi điều kỳ diệu xảy ra!

```csharp
Workbook workbook = new Workbook();
```

 Dòng này tạo ra một phiên bản mới của`Workbook` lớp cho phép chúng ta làm việc với các trang tính và biểu đồ.

## Bước 3: Thêm một bảng tính mới

Bây giờ chúng ta đã có sổ làm việc, đã đến lúc thêm một trang tính mới. Hãy nghĩ về các trang tính như các trang khác nhau trong sổ tay, nơi bạn có thể sắp xếp dữ liệu của mình.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Ở đây, chúng ta thêm một bảng tính mới và lấy tham chiếu đến bảng tính đó. Bạn sẽ làm việc với bảng tính này để nhập dữ liệu và biểu đồ của mình.

## Bước 4: Nhập giá trị mẫu

Với bảng tính đã tạo, hãy thêm một số dữ liệu mẫu vào các ô. Dữ liệu này là cơ sở để biểu đồ của bạn dựa vào, vì vậy hãy chọn các giá trị có ý nghĩa với loại biểu đồ của bạn!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

Trong đoạn mã này, chúng tôi sẽ điền một số giá trị số vào các ô "A1" đến "A3" và một số giá trị số khác vào các ô "B1" đến "B3". Hãy thoải mái tùy chỉnh các số này để phù hợp với nhu cầu của bạn!

## Bước 5: Tạo biểu đồ

Bây giờ là lúc tạo biểu đồ của bạn. Chúng ta sẽ thêm loại biểu đồ cột, rất phù hợp để so sánh các giá trị.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Ở đây, chúng ta sẽ thêm biểu đồ vào vị trí đã chỉ định bằng cách xác định bố cục của biểu đồ: tập hợp số đầu tiên biểu thị vị trí của biểu đồ trên lưới.

## Bước 6: Thêm Chuỗi Dữ Liệu vào Biểu Đồ

Sau khi tạo biểu đồ, bây giờ chúng ta cần liên kết biểu đồ đó với dữ liệu đã nhập ở các bước trước.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Dòng này kết nối chuỗi dữ liệu của biểu đồ với các giá trị trong ô "A1" đến "B3". Điều này có nghĩa là biểu đồ của bạn sẽ biểu diễn dữ liệu theo đúng ý định.

## Bước 7: Lưu biểu đồ dưới dạng hình ảnh

Bây giờ chúng ta hãy chuyển đổi biểu đồ sang định dạng hình ảnh để có thể dễ dàng chia sẻ và xem.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

Trong bước này, chúng ta lưu biểu đồ dưới dạng hình ảnh EMF (Enhanced Metafile) trong thư mục đầu ra đã chỉ định. Bạn cũng có thể lưu ở các định dạng khác nhau như BMP hoặc PNG.

## Bước 8: Chuyển đổi biểu đồ sang Bitmap

Nếu bạn thích làm việc với bitmap, sau đây là cách chuyển đổi biểu đồ sang định dạng Bitmap.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Thao tác này sẽ lưu biểu đồ của bạn dưới dạng ảnh BMP. Hãy nhớ rằng, tệp BMP thường lớn hơn nhưng có chất lượng cực cao!

## Bước 9: Kết xuất với Tùy chọn nâng cao

Chúng ta cũng có thể kết xuất biểu đồ với một số tùy chọn hình ảnh nâng cao để có chất lượng và độ phân giải tốt hơn. Hãy thiết lập một số tùy chọn:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Các tùy chọn này giúp cải thiện chất lượng hình ảnh bạn tạo ra, đặc biệt hữu ích cho các bài thuyết trình hoặc ấn phẩm.

## Bước 10: Chuyển đổi biểu đồ thành hình ảnh với tùy chọn nâng cao

Bây giờ chúng ta hãy chuyển đổi biểu đồ bằng các tùy chọn nâng cao mà chúng ta vừa thiết lập.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Thao tác này sẽ lưu biểu đồ của bạn dưới dạng tệp PNG với cài đặt chất lượng nâng cao.

## Bước 11: Xuất biểu đồ sang PDF

Cuối cùng, nếu bạn muốn có một tài liệu hoàn chỉnh, dễ chia sẻ, bạn có thể xuất biểu đồ trực tiếp sang định dạng PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Bước này sẽ tạo một tệp PDF chứa biểu đồ của bạn, rất phù hợp để tạo báo cáo kỹ thuật số hoặc chia sẻ với đồng nghiệp.

## Phần kết luận 

Xin chúc mừng! Bạn đã tạo thành công biểu đồ bằng Aspose.Cells cho .NET. Thư viện mạnh mẽ này đơn giản hóa việc tạo và thao tác các tệp và biểu đồ Excel, giúp dữ liệu của bạn dễ truy cập và hấp dẫn hơn về mặt trực quan. Cho dù bạn đang chuẩn bị báo cáo, phân tích hay bài thuyết trình, biểu đồ đều có tác động đáng kể và với Aspose, bạn có thể dễ dàng tạo biểu đồ theo chương trình.

## Câu hỏi thường gặp

### Tôi có thể tạo loại biểu đồ nào bằng Aspose.Cells cho .NET?
Bạn có thể tạo nhiều loại biểu đồ, bao gồm biểu đồ cột, biểu đồ đường, biểu đồ tròn và biểu đồ thanh, cùng nhiều loại biểu đồ khác.

### Tôi có thể tùy chỉnh giao diện của biểu đồ không?
Có, Aspose.Cells cho phép tùy chỉnh rộng rãi, bao gồm màu sắc, kiểu dáng và thành phần biểu đồ.

### Có bản dùng thử miễn phí không?
Chắc chắn rồi! Bạn có thể tải xuống phiên bản dùng thử miễn phí từ[đây](https://releases.aspose.com/).

### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
 Bạn có thể tìm thấy sự hỗ trợ và nguồn lực của cộng đồng tại[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
 Có, cần có giấy phép để tiếp tục sử dụng sau thời gian dùng thử, nhưng bạn có thể nộp đơn xin giấy phép tạm thời[đây](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
