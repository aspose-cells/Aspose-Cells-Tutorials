---
title: Thay đổi căn chỉnh ô Excel mà không làm mất định dạng
linktitle: Thay đổi căn chỉnh ô Excel mà không làm mất định dạng
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thay đổi căn chỉnh ô Excel mà không làm mất định dạng bằng Aspose.Cells for .NET. Làm theo hướng dẫn từng bước toàn diện của chúng tôi để kiểm soát liền mạch.
weight: 10
url: /vi/net/excel-data-alignment-formatting/change-cells-alignment-in-excel-without-losing-existing-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi căn chỉnh ô Excel mà không làm mất định dạng

## Giới thiệu

Quản lý các tệp Excel đôi khi có thể giống như đang điều hướng trong một mê cung, đặc biệt là khi nói đến việc duy trì định dạng trong khi thực hiện các điều chỉnh cần thiết như thay đổi căn chỉnh ô. Nếu bạn đã từng thử điều chỉnh căn chỉnh các ô trong Excel chỉ để thấy rằng định dạng bị xáo trộn, bạn không phải là người duy nhất! Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách thay đổi căn chỉnh các ô Excel mà không làm mất bất kỳ định dạng nào, bằng cách sử dụng Aspose.Cells cho .NET. Hãy xắn tay áo lên và bắt đầu!

## Điều kiện tiên quyết

Trước khi đi sâu vào mã hóa thực tế, điều quan trọng là phải đảm bảo rằng bạn đã thiết lập mọi thứ đúng cách. Sau đây là những gì bạn cần:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio (bất kỳ phiên bản nào hỗ trợ .NET) trên máy tính của mình.
2. Aspose.Cells cho .NET: Tải xuống và cài đặt thư viện Aspose.Cells từ[Trang web của Aspose](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Một chút quen thuộc với lập trình C# sẽ rất hữu ích vì chúng ta sẽ làm việc trong bối cảnh C#.
4.  Tệp Excel mẫu: Để minh họa, hãy chuẩn bị một tệp Excel mẫu (ví dụ:`sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx`) có chứa một số định dạng ô ban đầu.

## Nhập gói

Bước đầu tiên trong việc sử dụng Aspose.Cells cho .NET là đưa các không gian tên cần thiết vào dự án của bạn. Sau đây là cách thực hiện:

### Mở dự án của bạn

Mở Visual Studio và tạo một dự án C# mới (ứng dụng bảng điều khiển sẽ hoạt động tốt).

### Thêm tham chiếu đến Aspose.Cells

- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn "Quản lý gói NuGet".
-  Tìm kiếm`Aspose.Cells` và cài đặt nó.

### Nhập các không gian tên bắt buộc

Ở đầu tệp C# của bạn, hãy thêm lệnh using sau:

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Tables;
```

Điều này sẽ cho phép bạn sử dụng các lớp và phương thức do thư viện Aspose.Cells cung cấp một cách liền mạch.

Bây giờ chúng ta đã sắp xếp xong các điều kiện tiên quyết và nhập các gói, hãy cùng phân tích từng bước trong quy trình thay đổi căn chỉnh ô.

## Bước 1: Thiết lập thư mục nguồn và thư mục đầu ra của bạn

Để bắt đầu, bạn cần xác định nơi lưu trữ tệp Excel và nơi bạn muốn lưu tệp sau khi xử lý.

```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory\\"; // Thay thế bằng thư mục thực tế của bạn

// Thư mục đầu ra
string outputDir = "Your Document Directory\\"; // Thay thế bằng thư mục thực tế của bạn
```

 Mã này thiết lập đường dẫn cho các tệp đầu vào và đầu ra. Hãy chắc chắn thay thế`"Your Document Directory\\"` với đường dẫn thực tế trên máy tính của bạn.

## Bước 2: Tải tệp Excel mẫu

Tiếp theo, bạn sẽ muốn tải tệp Excel mẫu vào ứng dụng.

```csharp
// Tải tệp Excel mẫu có chứa các ô có định dạng.
Workbook wb = new Workbook(sourceDir + "sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx");
```

Dòng mã này sử dụng lớp Workbook để tải tệp Excel hiện có của bạn để chúng ta có thể thao tác với nội dung của tệp đó.

## Bước 3: Truy cập vào bảng tính mong muốn

Sau khi tải sổ làm việc, hãy truy cập vào trang tính bạn muốn thao tác. Tệp Excel có thể có nhiều trang tính, vì vậy hãy đảm bảo bạn đang nhắm đúng trang tính.

```csharp
// Truy cập vào bảng tính đầu tiên.
Worksheet ws = wb.Worksheets[0];
```

Ví dụ này truy cập vào trang tính đầu tiên. Nếu dữ liệu của bạn nằm trên một trang tính khác, hãy điều chỉnh chỉ mục cho phù hợp.

## Bước 4: Tạo một phạm vi ô

Xác định ô nào bạn muốn thay đổi bằng cách tạo một phạm vi. Lựa chọn này sẽ tập trung vào một phạm vi được chỉ định, chẳng hạn như “B2:D7”.

```csharp
//Tạo phạm vi ô.
Range rng = ws.Cells.CreateRange("B2:D7");
```

Phạm vi này sẽ cho phép chúng ta áp dụng các thiết lập căn chỉnh mới trực tiếp vào các ô đó.

## Bước 5: Tạo và tùy chỉnh đối tượng kiểu

Bây giờ, chúng ta cần xác định kiểu căn chỉnh mà chúng ta muốn áp dụng.

```csharp
// Tạo đối tượng kiểu.
Style st = wb.CreateStyle();

// Đặt căn chỉnh theo chiều ngang và chiều dọc vào giữa.
st.HorizontalAlignment = TextAlignmentType.Center;
st.VerticalAlignment = TextAlignmentType.Center;
```

Ở đây, một đối tượng Style mới được tạo ra và chúng ta đặt cả căn chỉnh ngang và dọc vào giữa. Đây là điều sẽ giúp căn chỉnh chính xác văn bản trong các ô đã chọn.

## Bước 6: Thiết lập Cờ Kiểu

Việc thiết lập cờ kiểu đóng vai trò quan trọng trong việc đảm bảo những thay đổi về kiểu của bạn được áp dụng. 

```csharp
// Tạo đối tượng cờ kiểu.
StyleFlag flag = new StyleFlag();

// Đặt kiểu cờ căn chỉnh là đúng. Đây là một tuyên bố quan trọng.
flag.Alignments = true;
```

 Bằng cách thiết lập`Alignments` thuộc tính của StyleFlag để`true`, bạn yêu cầu Aspose.Cells áp dụng các kiểu căn chỉnh một cách chính xác.

## Bước 7: Áp dụng Kiểu cho Phạm vi Ô

Sau khi đã thiết lập xong các kiểu và cờ, đã đến lúc áp dụng các kiểu đó vào phạm vi ô:

```csharp
//Áp dụng kiểu cho một phạm vi ô.
rng.ApplyStyle(st, flag);
```

Bước này có hiệu quả trong việc thay đổi cách căn chỉnh của tất cả các ô trong phạm vi đó trong khi vẫn giữ nguyên mọi định dạng hiện có.

## Bước 8: Lưu Workbook

Cuối cùng, bạn sẽ muốn lưu những thay đổi của mình vào một tệp mới để giữ nguyên bản gốc.

```csharp
// Lưu bảng tính ở định dạng XLSX.
wb.Save(outputDir + "outputChangeCellsAlignmentAndKeepExistingFormatting.xlsx", SaveFormat.Xlsx);
```

Dòng này lưu sổ làm việc, bao gồm cả những thay đổi về căn chỉnh, vào thư mục đầu ra đã chỉ định trước đó.

## Bước 9: Thông báo thành công

Sau khi lưu tệp, thật tuyệt khi phản hồi rằng mọi thứ đã hoạt động như mong đợi!

```csharp
Console.WriteLine("ChangeCellsAlignmentAndKeepExistingFormatting executed successfully.");
```

Thông báo này sẽ xuất hiện trong bảng điều khiển nếu thao tác của bạn hoàn tất mà không có vấn đề gì.

## Phần kết luận

Thay đổi căn chỉnh ô trong Excel trong khi vẫn giữ nguyên định dạng hiện tại là một quy trình liền mạch với Aspose.Cells for .NET. Bằng cách làm theo các bước này, bạn có thể đơn giản hóa thao tác Excel trong các ứng dụng của mình và tránh được sự đau đầu khi mất định dạng có giá trị. Cho dù bạn đang tạo báo cáo hay quản lý nguồn cấp dữ liệu, việc thành thạo kỹ năng này có thể thay đổi cuộc chơi!

## Câu hỏi thường gặp

### Aspose.Cells có thể xử lý các tệp Excel lớn không?
Chắc chắn rồi! Nó được tối ưu hóa về hiệu suất và có thể xử lý hiệu quả các tệp lớn.

### Có phiên bản dùng thử nào cho Aspose.Cells không?
 Có! Bạn có thể tải xuống bản dùng thử miễn phí từ trang web[Dùng thử miễn phí](https://releases.aspose.com/).

### Aspose.Cells hỗ trợ những ngôn ngữ lập trình nào?
Aspose.Cells chủ yếu hỗ trợ .NET, Java và một số ngôn ngữ khác thông qua các thư viện tương ứng.

### Tôi có thể nhận được hỗ trợ cho Aspose.Cells như thế nào?
 Đối với bất kỳ thắc mắc hoặc vấn đề liên quan đến hỗ trợ, hãy truy cập[diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9).

### Tôi có thể áp dụng nhiều kiểu cùng một lúc không?
Có, bạn có thể tạo nhiều đối tượng Style và áp dụng chúng theo trình tự hoặc có điều kiện tùy theo yêu cầu.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
