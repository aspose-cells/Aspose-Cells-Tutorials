---
title: Triển khai Header và Footer trong Worksheet
linktitle: Triển khai Header và Footer trong Worksheet
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thiết lập tiêu đề và chân trang trong bảng tính Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước, ví dụ thực tế và mẹo hữu ích.
weight: 22
url: /vi/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Triển khai Header và Footer trong Worksheet

## Giới thiệu

Khi làm việc với bảng tính Excel, tiêu đề và chân trang đóng vai trò quan trọng trong việc cung cấp thông tin ngữ cảnh quan trọng, như tên tệp, ngày hoặc số trang, cho đối tượng của bạn. Cho dù bạn đang tự động hóa báo cáo hay tạo tệp động, Aspose.Cells for .NET giúp bạn dễ dàng tùy chỉnh tiêu đề và chân trang trong bảng tính theo chương trình. Hướng dẫn này đi sâu vào phương pháp tiếp cận toàn diện, từng bước để thêm tiêu đề và chân trang bằng Aspose.Cells for .NET, mang đến cho các tệp Excel của bạn sự trau chuốt và chuyên nghiệp hơn.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị những điều sau:

1.  Aspose.Cells cho .NET: Bạn cần cài đặt Aspose.Cells cho .NET.[Tải xuống tại đây](https://releases.aspose.com/cells/net/).
2. Thiết lập IDE: Visual Studio (hoặc IDE bạn thích) đã cài đặt .NET framework.
3.  Giấy phép: Mặc dù bạn có thể bắt đầu dùng thử miễn phí, nhưng việc mua giấy phép đầy đủ hoặc tạm thời sẽ mở khóa toàn bộ tiềm năng của Aspose.Cells.[Xin giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).

Tài liệu hướng dẫn cho Aspose.Cells là một nguồn tài nguyên hữu ích để tham khảo trong suốt quá trình này. Bạn có thể tìm thấy nó[đây](https://reference.aspose.com/cells/net/).

## Nhập gói

Trong dự án của bạn, hãy nhập các không gian tên cần thiết:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Bằng cách nhập gói này, bạn sẽ có quyền truy cập vào các lớp và phương thức cần thiết để làm việc với tiêu đề, chân trang và các chức năng Excel khác trong Aspose.Cells.

Trong hướng dẫn này, chúng tôi sẽ chia nhỏ từng bước để bạn có thể dễ dàng làm theo, ngay cả khi bạn mới sử dụng Aspose.Cells hoặc .NET.

## Bước 1: Thiết lập sổ làm việc và trang của bạn

Trước tiên: tạo một sổ làm việc mới và truy cập vào thiết lập trang của bảng tính. Điều này sẽ cung cấp cho bạn các công cụ bạn cần để sửa đổi tiêu đề và chân trang cho bảng tính.

```csharp
// Xác định đường dẫn để lưu tài liệu của bạn
string dataDir = "Your Document Directory";

// Khởi tạo một đối tượng Workbook
Workbook excel = new Workbook();
```

 Ở đây, chúng tôi đã tạo ra một`Workbook` đối tượng, đại diện cho tệp Excel của chúng tôi.`PageSetup` của bảng tính là nơi chúng ta có thể sửa đổi các tùy chọn đầu trang và chân trang.


## Bước 2: Truy cập Thuộc tính Worksheet và PageSetup

 Trong Aspose.Cells, mỗi trang tính có một`PageSetup`thuộc tính kiểm soát các tính năng bố trí, bao gồm cả tiêu đề và chân trang. Hãy lấy`PageSetup` đối tượng cho bài tập của chúng ta.

```csharp
// Lấy tham chiếu đến PageSetup của trang tính đầu tiên
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Với điều này,`pageSetup` hiện có tất cả các thiết lập cần thiết để tùy chỉnh đầu trang và chân trang.


## Bước 3: Đặt Phần Bên Trái của Tiêu Đề

Tiêu đề trong Excel được chia thành ba phần: trái, giữa và phải. Hãy bắt đầu bằng cách thiết lập phần bên trái để hiển thị tên bảng tính.

```csharp
// Đặt tên bảng tính ở phần bên trái của tiêu đề
pageSetup.SetHeader(0, "&A");
```

 Sử dụng`&A` cho phép bạn hiển thị động tên trang tính. Điều này đặc biệt hữu ích nếu bạn có nhiều trang tính trong một sổ làm việc và muốn mỗi tiêu đề phản ánh tiêu đề trang tính của nó.


## Bước 4: Thêm Ngày và Giờ vào Giữa Tiêu đề

Tiếp theo, chúng ta hãy thêm ngày và giờ hiện tại vào phần giữa của tiêu đề. Ngoài ra, chúng ta sẽ sử dụng phông chữ tùy chỉnh để tạo kiểu.

```csharp
// Đặt ngày và giờ ở phần giữa của tiêu đề với phông chữ đậm
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

Trong đoạn mã này:
- `&D`chèn ngày hiện tại.
- `&T` chèn thời gian hiện tại.
- `"Times New Roman,Bold"` áp dụng phông chữ Times New Roman in đậm cho các thành phần này.


## Bước 5: Hiển thị Tên Tệp ở Phần Bên Phải của Tiêu đề

Để hoàn thiện phần tiêu đề, hãy hiển thị tên tệp ở bên phải, cùng với phần điều chỉnh phông chữ.

```csharp
// Hiển thị tên tệp ở phần bên phải của tiêu đề với kích thước phông chữ tùy chỉnh
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` biểu thị tên tệp, giúp biết rõ các trang được in thuộc về tệp nào.
- `&12` thay đổi kích thước phông chữ thành 12 cho phần này.


## Bước 6: Thêm văn bản có phông chữ tùy chỉnh vào phần chân trang bên trái

Chuyển sang phần chân trang! Chúng ta sẽ bắt đầu bằng cách thiết lập phần chân trang bên trái với văn bản tùy chỉnh và kiểu phông chữ được chỉ định.

```csharp
// Thêm văn bản tùy chỉnh với kiểu phông chữ vào phần bên trái của chân trang
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 Các`&\"Courier New\"&14` thiết lập trong mã trên áp dụng phông chữ "Courier New" với kích thước 14 cho văn bản đã chỉ định (`123`). Phần còn lại của văn bản vẫn giữ nguyên phông chữ chân trang mặc định.


## Bước 7: Chèn số trang vào giữa chân trang

Đánh số trang ở chân trang là một cách tuyệt vời để giúp người đọc theo dõi các tài liệu nhiều trang.

```csharp
// Chèn số trang vào phần giữa của chân trang
pageSetup.SetFooter(1, "&P");
```

 Đây,`&P` thêm số trang hiện tại vào phần giữa của chân trang. Đây là một chi tiết nhỏ nhưng rất quan trọng đối với các tài liệu có giao diện chuyên nghiệp.


## Bước 8: Hiển thị Tổng số trang trong Phần chân trang bên phải

Cuối cùng, hãy hoàn thiện phần chân trang bằng cách hiển thị tổng số trang ở phần bên phải.

```csharp
// Hiển thị tổng số trang ở phần bên phải của chân trang
pageSetup.SetFooter(2, "&N");
```

- `&N` cung cấp tổng số trang, cho người đọc biết tài liệu dài bao nhiêu.


## Bước 9: Lưu sổ làm việc

Sau khi thiết lập xong header và footer, đã đến lúc lưu workbook. Đây là bước cuối cùng để tạo tệp Excel với header và footer được tùy chỉnh hoàn toàn.

```csharp
// Lưu sổ làm việc
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Dòng này lưu tệp vào thư mục được chỉ định của bạn với tiêu đề và chân trang tùy chỉnh đã có sẵn.


## Phần kết luận

Thêm tiêu đề và chân trang vào bảng tính Excel là một kỹ năng có giá trị để tạo các tài liệu chuyên nghiệp, có tổ chức. Với Aspose.Cells for .NET, bạn có toàn quyền kiểm soát tiêu đề và chân trang của tệp Excel, từ việc hiển thị tên bảng tính đến chèn văn bản tùy chỉnh, ngày, giờ và thậm chí là số trang động. Bây giờ bạn đã thấy từng bước thực hiện, bạn có thể đưa tính năng tự động hóa Excel của mình lên cấp độ tiếp theo.

## Câu hỏi thường gặp

### Tôi có thể sử dụng các phông chữ khác nhau cho các phần khác nhau của đầu trang và chân trang không?  
Có, Aspose.Cells for .NET cho phép bạn chỉ định phông chữ cho từng phần của đầu trang và chân trang bằng cách sử dụng các thẻ phông chữ cụ thể.

### Làm thế nào để xóa phần đầu trang và phần chân trang?  
 Bạn có thể xóa tiêu đề và chân trang bằng cách đặt văn bản tiêu đề hoặc chân trang thành một chuỗi trống với`SetHeader` hoặc`SetFooter`.

### Tôi có thể chèn hình ảnh vào đầu trang hoặc chân trang bằng Aspose.Cells cho .NET không?  
Hiện tại, Aspose.Cells chủ yếu hỗ trợ văn bản trong tiêu đề và chân trang. Hình ảnh có thể cần giải pháp thay thế, chẳng hạn như chèn hình ảnh vào chính trang tính.

### Aspose.Cells có hỗ trợ dữ liệu động ở phần đầu trang và chân trang không?  
 Có, bạn có thể sử dụng nhiều mã động khác nhau (như`&D` cho ngày hoặc`&P` để thêm số trang) để thêm nội dung động.

### Làm thế nào để điều chỉnh chiều cao của phần đầu trang hoặc phần chân trang?  
 Aspose.Cells cung cấp các tùy chọn trong`PageSetup` lớp để điều chỉnh lề đầu trang và chân trang, cho phép bạn kiểm soát khoảng cách.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
