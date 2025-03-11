---
title: Xác thực dữ liệu thập phân trong Excel
linktitle: Xác thực dữ liệu thập phân trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Khám phá cách triển khai xác thực dữ liệu thập phân trong Excel bằng Aspose.Cells cho .NET với hướng dẫn dễ làm theo của chúng tôi. Nâng cao tính toàn vẹn của dữ liệu một cách dễ dàng.
weight: 11
url: /vi/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xác thực dữ liệu thập phân trong Excel

## Giới thiệu

Việc tạo bảng tính với dữ liệu chính xác là điều cần thiết để giao tiếp rõ ràng trong bất kỳ doanh nghiệp nào. Một cách để đảm bảo độ chính xác của dữ liệu là thông qua việc sử dụng xác thực dữ liệu trong Excel. Trong hướng dẫn này, chúng ta sẽ khai thác sức mạnh của Aspose.Cells cho .NET để tạo cơ chế xác thực dữ liệu thập phân giúp dữ liệu của bạn đáng tin cậy và sạch sẽ. Nếu bạn đang muốn nâng cao trò chơi Excel của mình, bạn đã đến đúng nơi rồi!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, hãy đảm bảo bạn đã thiết lập mọi thứ để có trải nghiệm suôn sẻ:

1. Visual Studio: Tải xuống và cài đặt Visual Studio nếu bạn chưa cài đặt. Đây là môi trường hoàn hảo để phát triển các ứng dụng .NET.
2.  Aspose.Cells cho .NET: Bạn sẽ cần phải thêm thư viện Aspose.Cells vào dự án của mình. Bạn có thể tải xuống qua[liên kết này](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Mặc dù chúng tôi sẽ giải thích mọi thứ theo từng bước, nhưng việc hiểu biết cơ bản về lập trình C# sẽ giúp bạn nắm bắt tốt hơn các khái niệm.
4. .NET Framework: Đảm bảo rằng bạn đã cài đặt .NET Framework cần thiết tương thích với Aspose.Cells.
5. Thư viện: Tham chiếu thư viện Aspose.Cells trong dự án của bạn để tránh lỗi biên dịch.

Bây giờ chúng ta đã nắm được những kiến thức cơ bản, hãy cùng đến với phần thú vị: lập trình.

## Nhập gói

Để bắt đầu, bạn cần nhập các gói cần thiết vào tệp C# của mình. Điều này cho phép bạn truy cập các chức năng của Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Bằng cách thêm dòng này vào đầu tệp, bạn đang yêu cầu C# tìm chức năng Aspose.Cells cho phép bạn thao tác với các tệp Excel.

Bây giờ chúng ta đã thiết lập xong bối cảnh, hãy cùng thực hiện các bước cần thiết để tạo xác thực dữ liệu thập phân trong bảng tính Excel.

## Bước 1: Thiết lập thư mục tài liệu của bạn

Trước khi bạn có thể lưu bất kỳ tệp nào, bạn cần đảm bảo rằng thư mục tài liệu của bạn được thiết lập chính xác:

```csharp
string dataDir = "Your Document Directory";
```

 Thay thế`"Your Document Directory"` bằng đường dẫn mà bạn muốn lưu các tệp Excel của mình.

## Bước 2: Kiểm tra sự tồn tại của thư mục

Đoạn mã này sẽ kiểm tra xem thư mục có tồn tại hay không và tạo thư mục nếu không:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Bước này giống như việc đảm bảo không gian làm việc của bạn đã sẵn sàng trước khi bắt đầu một dự án mới. Không lộn xộn, không căng thẳng!

## Bước 3: Tạo một đối tượng Workbook

Tiếp theo, chúng ta hãy tạo một đối tượng sổ làm việc mới, về cơ bản là một tệp Excel:

```csharp
Workbook workbook = new Workbook();
```

Hãy nghĩ về một sổ làm việc như một trang giấy trắng cho dữ liệu của bạn. Lúc này, nó không có nội dung nhưng đã sẵn sàng để được tô màu.

## Bước 4: Tạo và truy cập bảng tính


Bây giờ, chúng ta hãy tạo một bảng tính và truy cập vào trang tính đầu tiên trong sổ làm việc:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Giống như một cuốn sách có nhiều trang, một sổ làm việc có thể có nhiều bảng tính. Hiện tại chúng tôi đang tập trung vào bảng tính đầu tiên.

## Bước 5: Lấy Bộ sưu tập xác thực

Bây giờ, hãy kéo bộ sưu tập xác thực từ bảng tính vì đây là nơi chúng ta sẽ quản lý các quy tắc xác thực dữ liệu:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Bước này giống như việc kiểm tra hộp công cụ trước khi bạn bắt đầu một dự án.

## Bước 6: Xác định vùng ô để xác thực

Chúng ta cần xác định khu vực áp dụng xác thực:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Ở đây, chúng tôi quy định rằng xác thực dữ liệu sẽ được áp dụng cho một ô duy nhất, cụ thể là ô đầu tiên trong bảng tính (A1).

## Bước 7: Tạo và Thêm Xác thực

Hãy tạo đối tượng xác thực và thêm nó vào bộ sưu tập xác thực:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Bây giờ chúng ta có một đối tượng xác thực mà chúng ta sẽ cấu hình để thực thi các điều kiện thập phân.

## Bước 8: Đặt Loại xác thực

Tiếp theo, chúng ta sẽ chỉ định loại xác thực mà chúng ta muốn:

```csharp
validation.Type = ValidationType.Decimal;
```

Bằng cách đặt kiểu thành Thập phân, chúng ta đang hướng dẫn Excel mong đợi các giá trị thập phân trong ô được xác thực.

## Bước 9: Chỉ định toán tử

Bây giờ, chúng ta sẽ chỉ định điều kiện cho các giá trị được phép. Chúng ta muốn đảm bảo dữ liệu nhập vào nằm giữa hai phạm vi:

```csharp
validation.Operator = OperatorType.Between;
```

Hãy nghĩ về việc vẽ một đường ranh giới. Bất kỳ số nào nằm ngoài phạm vi này sẽ bị từ chối, giúp dữ liệu của bạn sạch sẽ!

## Bước 10: Thiết lập giới hạn cho việc xác thực

Tiếp theo, chúng ta sẽ thiết lập giới hạn dưới và giới hạn trên cho quá trình xác thực của mình:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Với những giới hạn này, mọi số thập phân, bất kể lớn hay nhỏ, đều được chấp nhận, miễn là nó hợp lệ!

## Bước 11: Tùy chỉnh thông báo lỗi

Hãy đảm bảo rằng người dùng biết lý do tại sao thông tin đầu vào của họ bị từ chối bằng cách thêm thông báo lỗi:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Điều này mang lại trải nghiệm thân thiện với người dùng vì nó cung cấp hướng dẫn về những gì cần nhập.

## Bước 12: Xác định vùng xác thực

Bây giờ, chúng ta hãy chỉ định các ô sẽ chịu xác thực này:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Trong cấu hình này, chúng ta đang nói rằng xác thực được áp dụng từ ô A1 đến ô A10.

## Bước 13: Thêm vùng xác thực

Bây giờ chúng ta đã xác định được vùng xác thực, hãy áp dụng nó:

```csharp
validation.AddArea(area);
```

Xác thực của bạn hiện đã được thiết lập chắc chắn, sẵn sàng phát hiện mọi dữ liệu đầu vào không phù hợp!

## Bước 14: Lưu sổ làm việc

Cuối cùng, hãy lưu bảng tính với xác thực dữ liệu thập phân tại chỗ:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Và thế là xong! Bạn đã tạo thành công một sổ làm việc có xác thực dữ liệu thập phân bằng Aspose.Cells cho .NET.

## Phần kết luận

Việc triển khai xác thực dữ liệu thập phân trong Excel bằng Aspose.Cells cho .NET thật dễ dàng khi bạn làm theo các bước đơn giản sau. Bạn không chỉ đảm bảo dữ liệu sạch và có cấu trúc mà còn cải thiện tính toàn vẹn dữ liệu tổng thể trong bảng tính của mình, giúp chúng đáng tin cậy và thân thiện với người dùng.
Cho dù bạn làm trong lĩnh vực tài chính, quản lý dự án hay bất kỳ lĩnh vực nào sử dụng báo cáo dữ liệu, việc thành thạo các kỹ năng này sẽ giúp tăng năng suất của bạn đáng kể. Vì vậy, hãy thử xem! Bảng tính của bạn sẽ cảm ơn bạn vì điều đó.

## Câu hỏi thường gặp

### Xác thực dữ liệu trong Excel là gì?
Xác thực dữ liệu trong Excel là tính năng hạn chế loại dữ liệu có thể nhập vào một ô hoặc phạm vi cụ thể, đảm bảo tính toàn vẹn của dữ liệu.

### Tôi có thể tùy chỉnh thông báo lỗi trong quá trình xác thực dữ liệu không?
Có! Bạn có thể cung cấp thông báo lỗi tùy chỉnh để hướng dẫn người dùng khi nhập dữ liệu không chính xác.

### Aspose.Cells có miễn phí sử dụng không?
 Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng bạn sẽ cần giấy phép để sử dụng lâu dài. Bạn có thể tìm thêm thông tin về việc mua giấy phép tạm thời[đây](https://purchase.aspose.com/temporary-license/).

### Tôi có thể xác thực những kiểu dữ liệu nào trong Excel?
Với Aspose.Cells, bạn có thể xác thực nhiều kiểu dữ liệu khác nhau bao gồm số nguyên, số thập phân, ngày tháng, danh sách và công thức tùy chỉnh.

### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?
 Bạn có thể khám phá tài liệu mở rộng[đây](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
