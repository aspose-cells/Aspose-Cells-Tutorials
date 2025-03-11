---
title: Bỏ hợp nhất các ô đã hợp nhất trong Excel
linktitle: Bỏ hợp nhất các ô đã hợp nhất trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Dễ dàng hủy hợp nhất các ô đã hợp nhất trong Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để tạo bảng tính tốt hơn.
weight: 10
url: /vi/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bỏ hợp nhất các ô đã hợp nhất trong Excel

## Giới thiệu

Bạn có thấy mệt mỏi khi phải xử lý các ô đã hợp nhất trong bảng tính Excel của mình không? Bạn không phải là người duy nhất! Các ô đã hợp nhất có thể là một tính năng hữu ích để định dạng, nhưng chúng thường có thể gây đau đầu khi xử lý và phân tích dữ liệu. Nhưng đoán xem? Việc hủy hợp nhất các ô khó chịu đó dễ hơn bạn nghĩ, đặc biệt là khi bạn sử dụng Aspose.Cells cho .NET. Trong bài viết này, tôi sẽ hướng dẫn bạn cách hủy hợp nhất các ô đã hợp nhất từng bước, đảm bảo dữ liệu của bạn gọn gàng, ngăn nắp và sẵn sàng để sử dụng! Vì vậy, hãy đội mũ lập trình của bạn và cùng khám phá thế giới của Aspose.Cells.

## Điều kiện tiên quyết

Trước khi bắt tay vào thực hiện, bạn cần chuẩn bị một số điều cần thiết sau:

### Kiến thức cơ bản về C# và .NET Framework
Nếu bạn quen thuộc với lập trình C# và có hiểu biết cơ bản về .NET framework, bạn đã có một khởi đầu tuyệt vời. Nếu không, đừng lo lắng! Hướng dẫn này được thiết kế đơn giản, vì vậy bạn sẽ học được các khái niệm cần thiết trong quá trình học.

### Thư viện Aspose.Cells
Đảm bảo bạn đã cài đặt thư viện Aspose.Cells trong môi trường .NET của mình. Bạn có thể dễ dàng tải xuống bằng cách truy cập[Trang Tải xuống Aspose.Cells](https://releases.aspose.com/cells/net/).

### Thiết lập IDE
Bạn nên thiết lập một môi trường phát triển, như Visual Studio, nơi bạn có thể viết và thực thi mã C# của mình.

### Tệp Excel mẫu
Lấy một tệp Excel mẫu có chứa một số ô đã hợp nhất—bạn sẽ sử dụng tệp này để thực hành hủy hợp nhất.

Khi đã đáp ứng được tất cả các điều kiện tiên quyết này, giờ chúng ta có thể bắt tay vào phần thú vị nhất—viết mã giải pháp!

## Nhập gói

Trước tiên, hãy nhập các gói cần thiết. Với Aspose.Cells, bạn sẽ tương tác với nhiều lớp khác nhau để quản lý các tệp Excel của mình một cách hiệu quả. Sau đây là những gì bạn cần đưa vào đầu tệp C# của mình:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Bằng cách sử dụng gói này, bạn sẽ có quyền truy cập vào tất cả các tính năng mà Aspose.Cells cung cấp.

Hãy chia nhỏ quá trình tách thành các bước dễ quản lý. Mỗi bước sẽ được định nghĩa rõ ràng để bạn có thể dễ dàng theo dõi.

## Bước 1: Xác định thư mục

Bước đầu tiên là xác định các thư mục nơi chứa tệp Excel đầu vào (tệp có các ô được hợp nhất) và tệp đầu ra (tệp lưu dữ liệu chưa hợp nhất). Sau đây là cách thiết lập:

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory"; 

// Thư mục đầu ra
string outputDir = "Your Document Directory"; 
```

 Hãy chắc chắn thay thế`"Your Document Directory"` với đường dẫn thực tế đến tập tin của bạn.

## Bước 2: Tạo một Workbook

Bây giờ bạn đã thiết lập các thư mục, đã đến lúc tạo một đối tượng Workbook. Đối tượng này sẽ cho phép bạn thao tác tệp Excel. Bạn có thể thực hiện việc này bằng mã sau:

```csharp
// Tạo một sổ làm việc
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Dòng mã này sẽ đọc tệp Excel mẫu của bạn và chuẩn bị để xử lý. 

## Bước 3: Truy cập vào Bảng tính

Mỗi sổ làm việc bao gồm các trang tính. Bạn cần truy cập vào trang tính cụ thể mà bạn muốn hủy hợp nhất các ô. Sau đây là cách thực hiện:

```csharp
// Tạo một bảng tính và lấy bảng tính đầu tiên
Worksheet worksheet = wbk.Worksheets[0];
```

Mã này lấy trang tính đầu tiên. Nếu các ô được hợp nhất của bạn nằm trên một trang tính khác, hãy cập nhật chỉ mục cho phù hợp.

## Bước 4: Truy cập các ô trong trang tính

Tiếp theo, bạn sẽ cần tham chiếu đến các ô trong bảng tính của mình. Bạn có thể thực hiện việc này bằng cách:

```csharp
//Tạo một đối tượng Cells để lấy tất cả các ô
Cells cells = worksheet.Cells;
```

Với dòng này, giờ bạn có thể truy cập vào tất cả các ô trên bảng tính, cho phép bạn thao tác chúng khi cần.

## Bước 5: Tách các ô

Đây là bước quan trọng—hủy hợp nhất các ô! Bạn sẽ muốn chỉ định phạm vi các ô đã hợp nhất mà bạn muốn hủy hợp nhất. Sử dụng mã sau:

```csharp
// Tách các ô
cells.UnMerge(5, 2, 2, 3);
```

 Trong ví dụ này,`UnMerge` phương pháp này sử dụng bốn tham số: chỉ số hàng bắt đầu (5), chỉ số cột bắt đầu (2), số hàng cần hủy hợp nhất (2) và số cột cần hủy hợp nhất (3). Điều chỉnh các tham số này để khớp với các ô đã hợp nhất cụ thể trong tệp Excel của bạn.

## Bước 6: Lưu sổ làm việc

Sau khi hủy hợp nhất, bạn sẽ muốn lưu các thay đổi của mình vào một tệp Excel mới. Sau đây là cách thực hiện:

```csharp
// Lưu tập tin
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Dòng này lưu dữ liệu chưa hợp nhất của bạn vào thư mục đầu ra đã chỉ định. Đơn giản vậy thôi!

## Bước 7: Xác nhận quy trình

Cuối cùng, bạn nên xác nhận mọi thứ diễn ra suôn sẻ. Bạn có thể in thông báo tới bảng điều khiển để cho bạn biết rằng thao tác đã được thực hiện thành công:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Và bạn đã hoàn thành! Bạn đã hủy hợp nhất các ô trong tệp Excel thành công bằng Aspose.Cells cho .NET.

## Phần kết luận

Việc hủy hợp nhất các ô có vẻ tẻ nhạt, đặc biệt là nếu bạn đang xử lý các bảng tính lớn, nhưng với Aspose.Cells cho .NET, việc này thật dễ dàng! Hướng dẫn này hướng dẫn bạn mọi thứ từ thiết lập môi trường của bạn đến thực thi mã cần thiết để hủy hợp nhất các ô một cách hiệu quả. Tính linh hoạt mà thư viện Aspose.Cells cung cấp cho phép bạn xử lý các bảng tính một cách hiệu quả, khiến nó trở thành lựa chọn lý tưởng cho các nhà phát triển làm việc với các tệp Excel. Vì vậy, hãy bắt đầu và tận hưởng các bảng tính sạch hơn, dễ quản lý hơn.

## Câu hỏi thường gặp

### Aspose.Cells là gì?  
Aspose.Cells là một thư viện mạnh mẽ để tạo, xử lý và chuyển đổi các tài liệu Excel trong các ứng dụng .NET.

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?  
 Trong khi Aspose.Cells cung cấp bản dùng thử miễn phí, bạn cần có giấy phép để sử dụng đầy đủ. Bạn có thể nhận được[giấy phép tạm thời ở đây](https://purchase.aspose.com/temporary-license/).

### Tôi có thể hủy nhập các ô trong nhiều trang tính cùng một lúc không?  
Có, bạn có thể lặp qua nhiều trang tính trong một bảng tính và hủy hợp nhất các ô khi cần.

### Aspose.Cells có tương thích với .NET Core không?  
Có, Aspose.Cells tương thích với .NET Core, khiến nó trở nên linh hoạt cho nhiều ứng dụng .NET khác nhau.

### Tôi có thể tìm thêm tài liệu về Aspose.Cells ở đâu?  
 Bạn có thể khám phá tài liệu đầy đủ về[Trang tham khảo Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
