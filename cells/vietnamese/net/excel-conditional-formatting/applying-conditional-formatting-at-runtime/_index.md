---
"description": "Tìm hiểu cách áp dụng định dạng có điều kiện khi chạy trong Excel với Aspose.Cells cho .NET trong hướng dẫn toàn diện, từng bước này."
"linktitle": "Áp dụng Định dạng có điều kiện tại Runtime trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Áp dụng Định dạng có điều kiện tại Runtime trong Excel"
"url": "/vi/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Áp dụng Định dạng có điều kiện tại Runtime trong Excel

## Giới thiệu

chúng là những công cụ mạnh mẽ để phân tích và trực quan hóa dữ liệu. Một trong những tính năng nổi bật của Excel là định dạng có điều kiện, cho phép người dùng áp dụng các kiểu định dạng cụ thể cho các ô dựa trên giá trị của chúng. Điều này có thể giúp xác định xu hướng dễ dàng hơn, làm nổi bật các điểm dữ liệu quan trọng hoặc đơn giản là làm cho dữ liệu dễ đọc hơn. Nếu bạn đang muốn triển khai định dạng có điều kiện trong các tệp Excel của mình theo chương trình, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách áp dụng định dạng có điều kiện khi chạy bằng Aspose.Cells cho .NET.

## Điều kiện tiên quyết
Trước khi tìm hiểu về mã, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:

1. Visual Studio: Đảm bảo rằng bạn đã cài đặt Visual Studio trên máy của mình. Bạn có thể sử dụng bất kỳ phiên bản nào hỗ trợ phát triển .NET.
2. Aspose.Cells cho .NET: Bạn sẽ cần phải cài đặt Aspose.Cells cho .NET. Bạn có thể tải xuống từ [Trang web Aspose](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
4. .NET Framework: Đảm bảo rằng dự án của bạn đang hướng tới phiên bản tương thích của .NET Framework.

Bây giờ chúng ta đã nắm được các điều kiện tiên quyết, hãy cùng bắt đầu phần thú vị nhé!

## Nhập gói
Để bắt đầu với Aspose.Cells, bạn sẽ cần nhập các không gian tên cần thiết vào dự án C# của mình. Sau đây là cách bạn có thể thực hiện:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào các lớp và phương thức cần thiết để thao tác với các tệp Excel và áp dụng định dạng có điều kiện.

Bây giờ, chúng ta hãy chia nhỏ quá trình áp dụng định dạng có điều kiện thành các bước dễ quản lý.

## Bước 1: Thiết lập dự án của bạn
Trước tiên, bạn cần tạo một dự án C# mới trong Visual Studio. Cách thực hiện như sau:

1. Mở Visual Studio và chọn File > New > Project.
2. Chọn Console App (.NET Framework) và đặt tên cho dự án của bạn.
3. Nhấp vào Tạo.

## Bước 2: Thêm tham chiếu Aspose.Cells
Sau khi thiết lập xong dự án, bạn cần thêm tham chiếu đến thư viện Aspose.Cells:

1. Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
2. Chọn Quản lý gói NuGet.
3. Tìm Aspose.Cells và cài đặt nó.

Điều này sẽ cho phép bạn sử dụng tất cả các chức năng được cung cấp bởi thư viện Aspose.Cells.

## Bước 3: Tạo một đối tượng Workbook
Tiếp theo, hãy tạo một sổ làm việc và một bảng tính mới. Đây là nơi mọi điều kỳ diệu xảy ra:

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

Ở bước này, chúng ta sẽ xác định thư mục lưu tệp Excel, tạo một bảng tính mới và truy cập vào bảng tính đầu tiên.

## Bước 4: Thêm Định dạng có điều kiện
Bây giờ, hãy thêm một số định dạng có điều kiện. Chúng ta sẽ bắt đầu bằng cách tạo một đối tượng định dạng có điều kiện trống:

```csharp
// Thêm định dạng có điều kiện trống
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Ở đây, chúng ta sẽ thêm một bộ sưu tập định dạng có điều kiện mới vào bảng tính của mình, bộ sưu tập này sẽ chứa các quy tắc định dạng.

## Bước 5: Xác định Phạm vi Định dạng
Tiếp theo, chúng ta cần chỉ định phạm vi ô mà định dạng có điều kiện sẽ áp dụng. Giả sử chúng ta muốn định dạng hàng đầu tiên và cột thứ hai:

```csharp
// Thiết lập phạm vi định dạng có điều kiện.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

Trong mã này, chúng tôi định nghĩa hai vùng để định dạng có điều kiện. Vùng đầu tiên dành cho ô tại (0,0) và vùng thứ hai dành cho (1,1). Hãy thoải mái điều chỉnh các phạm vi này dựa trên nhu cầu cụ thể của bạn!

## Bước 6: Thêm Điều kiện Định dạng Có điều kiện
Bây giờ là lúc xác định các điều kiện cho định dạng của chúng ta. Giả sử chúng ta muốn làm nổi bật các ô dựa trên giá trị của chúng:

```csharp
// Thêm điều kiện.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Thêm điều kiện.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

Trong bước này, chúng tôi sẽ thêm hai điều kiện: một cho các giá trị giữa `A2` Và `100`và một giá trị khác cho các giá trị giữa `50` Và `100`. Điều này cho phép bạn làm nổi bật các ô một cách linh hoạt dựa trên giá trị của chúng.

## Bước 7: Thiết lập Kiểu Định dạng
Với các điều kiện của chúng ta, bây giờ chúng ta có thể thiết lập các kiểu định dạng. Hãy thay đổi màu nền cho các điều kiện của chúng ta:

```csharp
// Đặt màu nền.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Ở đây, chúng ta đang thiết lập màu nền của điều kiện đầu tiên thành màu đỏ. Bạn có thể tùy chỉnh thêm bằng cách thay đổi màu phông chữ, đường viền và các kiểu khác khi cần!

## Bước 8: Lưu tệp Excel
Cuối cùng, đã đến lúc lưu công việc của chúng ta! Chúng ta sẽ lưu sổ làm việc vào thư mục đã chỉ định:

```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "output.xls");
```

Dòng mã này lưu tệp Excel với định dạng có điều kiện được áp dụng. Hãy đảm bảo kiểm tra thư mục được chỉ định cho tệp đầu ra của bạn!

## Phần kết luận
Và bạn đã có nó! Bạn đã áp dụng thành công định dạng có điều kiện khi chạy trong Excel bằng Aspose.Cells cho .NET. Thư viện mạnh mẽ này giúp bạn dễ dàng thao tác các tệp Excel theo chương trình, cho phép bạn tự động hóa các tác vụ tẻ nhạt và cải thiện các bản trình bày dữ liệu của mình. Cho dù bạn đang làm việc trên một dự án nhỏ hay một ứng dụng quy mô lớn, Aspose.Cells có thể giúp bạn hợp lý hóa quy trình làm việc và cải thiện năng suất của mình.

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là thư viện .NET cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel theo cách lập trình.

### Tôi có thể sử dụng Aspose.Cells với các ngôn ngữ lập trình khác không?
Có, Aspose.Cells hỗ trợ nhiều ngôn ngữ lập trình, bao gồm Java, Python, v.v.

### Có bản dùng thử miễn phí cho Aspose.Cells không?
Có, bạn có thể tải xuống bản dùng thử miễn phí từ [Trang web Aspose](https://releases.aspose.com/).

### Tôi có thể nhận được hỗ trợ cho Aspose.Cells như thế nào?
Bạn có thể nhận được hỗ trợ bằng cách truy cập [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
Có, cần có giấy phép để sử dụng cho mục đích thương mại, nhưng bạn có thể yêu cầu giấy phép tạm thời [đây](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}