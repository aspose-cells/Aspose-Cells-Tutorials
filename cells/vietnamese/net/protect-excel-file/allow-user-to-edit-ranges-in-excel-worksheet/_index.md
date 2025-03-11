---
title: Cho phép người dùng chỉnh sửa phạm vi trong bảng tính Excel
linktitle: Cho phép người dùng chỉnh sửa phạm vi trong bảng tính Excel
second_title: Tài liệu tham khảo API Aspose.Cells cho .NET
description: Cho phép người dùng chỉnh sửa các phạm vi cụ thể trong bảng tính Excel bằng Aspose.Cells cho .NET. Hướng dẫn từng bước với mã nguồn bằng C#.
weight: 10
url: /vi/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cho phép người dùng chỉnh sửa phạm vi trong bảng tính Excel

## Giới thiệu

Khi làm việc với các bảng tính Excel, tính linh hoạt thường là chìa khóa—đặc biệt là khi nhiều người dùng cần truy cập để chỉnh sửa các khu vực cụ thể mà không làm ảnh hưởng đến tính toàn vẹn dữ liệu của toàn bộ bảng tính. Đây chính là nơi Aspose.Cells for .NET tỏa sáng! Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách cho phép người dùng chỉnh sửa các phạm vi nhất định trong một bảng tính Excel trong khi vẫn bảo vệ phần còn lại của tài liệu. Đến cuối bài viết này, bạn sẽ không chỉ nắm được các khái niệm mà còn có một ví dụ cụ thể để làm việc. 

## Điều kiện tiên quyết

Trước khi đi sâu vào chi tiết, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:

1. Môi trường phát triển .NET: Bạn nên thiết lập môi trường phát triển .NET đang hoạt động (có thể là Visual Studio hoặc bất kỳ IDE nào khác mà bạn chọn).
2.  Aspose.Cells cho Thư viện .NET: Tải xuống và cài đặt thư viện Aspose.Cells. Bạn có thể tìm thấy nó[đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn dễ dàng xem qua các ví dụ mã.
4. Hiểu những điều cơ bản về Excel: Biết cách Excel hoạt động sẽ cung cấp nền tảng cho các chức năng mà chúng ta sẽ thảo luận.

Sau khi đáp ứng được những điều kiện tiên quyết này, bạn đã sẵn sàng!

## Nhập gói

Trước khi bắt đầu mã hóa, chúng ta cần đảm bảo rằng dự án của chúng ta nhận ra không gian tên Aspose.Cells. Sau đây là cách nhập các gói cần thiết:

```csharp
using System.IO;
using Aspose.Cells;
```

Bây giờ chúng ta đã nhập những gì cần thiết, hãy cùng tìm hiểu từng bước trong hướng dẫn.

## Bước 1: Thiết lập thư mục tài liệu

Đối với bất kỳ hoạt động tệp nào, điều quan trọng là phải có một vị trí xác định nơi tài liệu của chúng ta sẽ được lưu. Hãy thiết lập thư mục làm việc của chúng ta để lưu trữ các tệp Excel.

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Đầu tiên, thay thế`"YOUR DOCUMENT DIRECTORY"` với đường dẫn mà bạn muốn lưu các tập tin của mình. Mã này kiểm tra xem thư mục có tồn tại không; nếu không, nó sẽ tạo một thư mục.

## Bước 2: Tạo một Workbook mới

Sau khi đã có thư mục làm việc, đã đến lúc tạo bảng tính Excel. 

```csharp
// Tạo một Workbook mới
Workbook book = new Workbook();
```

 Ở đây, chúng tôi đang tạo một phiên bản mới của`Workbook` lớp do Aspose.Cells cung cấp, cho phép chúng ta thao tác với tệp Excel.

## Bước 3: Truy cập Bảng tính mặc định

Mỗi sổ làm việc mới tạo đều có ít nhất một bảng tính. Hãy cùng truy cập vào đó.

```csharp
// Nhận bảng tính đầu tiên (mặc định)
Worksheet sheet = book.Worksheets[0];
```

Trong đoạn mã này, chúng ta sẽ truy cập vào trang tính đầu tiên của sổ làm việc, chúng ta sẽ thao tác ở các bước tiếp theo.

## Bước 4: Nhận Cho phép chỉnh sửa phạm vi

 Để cho phép các phạm vi cụ thể của bảng tính để chỉnh sửa, chúng ta cần truy cập`AllowEditRanges` tài sản.

```csharp
// Nhận được phạm vi chỉnh sửa cho phép
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Bộ sưu tập này sẽ cho phép chúng ta quản lý những phạm vi có thể chỉnh sửa trong bảng tính của mình.

## Bước 5: Xác định Phạm vi được Bảo vệ

Tiếp theo, hãy xác định phần nào của bảng tính mà chúng ta muốn bảo vệ trong khi vẫn cho phép chỉnh sửa trong phạm vi được chỉ định.

```csharp
// Định nghĩa ProtectedRange
ProtectedRange proteced_range;

// Tạo phạm vi
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Chỉ định mật khẩu
proteced_range.Password = "123";
```

Ở bước này, chúng tôi sẽ thêm một phạm vi có thể chỉnh sửa mới có tên là "r2" cho phép chỉnh sửa các ô từ hàng 1 cột 1 đến hàng 3 cột 3. Ngoài ra, chúng tôi sẽ đặt mật khẩu để bảo vệ phạm vi này, đảm bảo chỉ những người dùng được ủy quyền mới có thể sửa đổi.

## Bước 6: Bảo vệ bảng tính

Bây giờ chúng ta đã thiết lập phạm vi có thể chỉnh sửa, chúng ta cần bảo vệ bảng tính.

```csharp
// Bảo vệ tờ giấy
sheet.Protect(ProtectionType.All);
```

Mã này sẽ bảo vệ toàn bộ bảng tính khỏi mọi thay đổi không mong muốn, ngoại trừ phạm vi chúng ta vừa chỉ định.

## Bước 7: Lưu tệp Excel

Hãy lưu bảng tính để có thể thấy những thay đổi được phản ánh trong tệp Excel.

```csharp
// Lưu tệp Excel
book.Save(dataDir + "protectedrange.out.xls");
```

Đảm bảo điều chỉnh tên tệp khi cần thiết. Thao tác này sẽ tạo tệp Excel trong thư mục bạn chỉ định với các cài đặt chúng tôi đã định cấu hình.

## Phần kết luận

Vậy là xong! Bạn đã tạo thành công một bảng tính Excel giới hạn các chỉnh sửa trong phạm vi được chỉ định trong khi vẫn bảo vệ phần còn lại của bảng tính. Sử dụng Aspose.Cells cho .NET giúp quản lý các loại tác vụ này dễ dàng và hiệu quả hơn nhiều. Cho dù bạn đang phát triển một ứng dụng phức tạp hay chỉ cần quản lý dữ liệu một cách an toàn, những khả năng này có thể cải thiện đáng kể quy trình làm việc của bạn.

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ để xử lý các tệp Excel, cung cấp các chức năng như tạo, chỉnh sửa và chuyển đổi bảng tính theo chương trình.

### Tôi có thể áp dụng nhiều phạm vi có thể chỉnh sửa không?
 Chắc chắn rồi! Bạn có thể gọi`Add` phương pháp trên`allowRanges` thu thập nhiều lần để chỉ định nhiều phạm vi có thể chỉnh sửa.

### Điều gì xảy ra nếu tôi quên mật khẩu?
Thật không may, nếu bạn quên mật khẩu cho một phạm vi có thể chỉnh sửa, bạn sẽ cần phải xóa bảo vệ hoặc truy cập tệp theo cách được xác định trước có thể liên quan đến thông tin xác thực.

### Có phiên bản miễn phí của Aspose.Cells không?
Có, Aspose cung cấp bản dùng thử miễn phí mà bạn có thể sử dụng để khám phá các tính năng trước khi mua.

### Tôi có thể tìm thêm thông tin về Aspose.Cells ở đâu?
 Bạn có thể kiểm tra[tài liệu](https://reference.aspose.com/cells/net/)để có hướng dẫn và tài liệu tham khảo chi tiết.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
