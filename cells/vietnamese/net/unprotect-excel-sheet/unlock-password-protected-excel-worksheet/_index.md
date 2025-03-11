---
title: Mở khóa bảng tính Excel được bảo vệ bằng mật khẩu
linktitle: Mở khóa bảng tính Excel được bảo vệ bằng mật khẩu
second_title: Tài liệu tham khảo API Aspose.Cells cho .NET
description: Tìm hiểu cách mở khóa bảng tính Excel được bảo vệ bằng mật khẩu bằng Aspose.Cells cho .NET. Hướng dẫn từng bước bằng C#.
weight: 10
url: /vi/net/unprotect-excel-sheet/unlock-password-protected-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mở khóa bảng tính Excel được bảo vệ bằng mật khẩu

## Giới thiệu

Bạn đã bao giờ thấy mình bị khóa ngoài một bảng tính Excel, nhìn chằm chằm vào dữ liệu không thể chỉnh sửa và mong muốn có cách vào chưa? Tất cả chúng ta đều đã từng trải qua điều đó! Bảo vệ bằng mật khẩu có thể là con dao hai lưỡi: nó cung cấp tính bảo mật nhưng đôi khi lại giống như một nhà tù hơn. May mắn thay, nếu bạn là một nhà phát triển hoặc người thoải mái với lập trình .NET, Aspose.Cells sẽ hỗ trợ bạn, cho phép bạn mở khóa các bảng tính được bảo vệ đó một cách dễ dàng. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn các bước để mở khóa bảng tính Excel được bảo vệ bằng mật khẩu bằng Aspose.Cells cho .NET. 

## Điều kiện tiên quyết

Trước khi đi sâu vào chi tiết để mở khóa bảng tính này, bạn cần chuẩn bị một số thứ sau:

### Môi trường .NET

Bạn cần một môi trường .NET đang hoạt động. Nếu bạn chưa sẵn sàng, hãy cân nhắc cài đặt Visual Studio hoặc bất kỳ .NET IDE nào khác mà bạn thích. 

### Aspose.Cells cho .NET

 Bạn cần có Aspose.Cells cho .NET. Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/) . Hãy đảm bảo rằng bạn đã làm quen với tài liệu, có thể tìm thấy[đây](https://reference.aspose.com/cells/net/).

### Kiến thức lập trình cơ bản

Một chút kiến thức lập trình cơ bản về C# hoặc VB.NET sẽ giúp ích rất nhiều. Nếu bạn đã nắm được, bạn đã sẵn sàng!

## Nhập gói

Trước tiên, chúng ta cần đưa các gói cần thiết vào dự án của mình. Hãy cùng phân tích từng bước một.

### Tạo một dự án mới

Để bắt đầu, hãy mở Visual Studio và tạo một dự án mới. 

1. Mở Visual Studio. 
2. Chọn "Tạo dự án mới".
3. Chọn "Thư viện lớp" hoặc "Ứng dụng bảng điều khiển" theo sở thích của bạn.
4. Thiết lập các thông tin cần thiết cho dự án và nhấp vào "Tạo".

### Thêm tham chiếu Aspose.Cells

Bây giờ, chúng ta cần tham chiếu Aspose.Cells trong dự án của mình.

1. Nhấp chuột phải vào "Tham khảo" trong Solution Explorer.
2. Chọn "Quản lý gói NuGet".
3. Tìm kiếm "Aspose.Cells" và cài đặt gói.

Và thế là xong! Bạn đã sẵn sàng để bắt đầu viết mã!

### Thêm Sử dụng Câu lệnh

Mở tệp C# của bạn và thêm lệnh sau vào đầu:

```csharp
using System.IO;
using System;
using Aspose.Cells;
```

Bây giờ, chúng ta hãy đi sâu vào trọng tâm của hướng dẫn này. Chúng ta sẽ sử dụng một đoạn mã đơn giản để mở khóa bảng tính khó chịu đó. Chúng ta sẽ chia nhỏ nó thành các bước dễ dàng hơn.

## Bước 1: Xác định Đường dẫn Tài liệu

Trước tiên, chúng ta cần thiết lập đường dẫn đến tài liệu Excel. Đây là nơi bạn sẽ chỉ định vị trí tệp Excel của mình. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 Mẹo: Thay thế`"YOUR DOCUMENT DIRECTORY"` với đường dẫn thực tế nơi tệp Excel của bạn (hãy gọi nó là`book1.xls`) nằm ở đâu. 

## Bước 2: Khởi tạo một đối tượng Workbook

Tiếp theo, chúng ta cần tạo một thể hiện của lớp Workbook. Đối tượng này biểu diễn tệp Excel trong mã của bạn.

```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

Dòng này đọc tệp Excel đã chỉ định và tải tệp đó vào bộ nhớ để chúng ta có thể tương tác với tệp đó.

## Bước 3: Truy cập vào Bảng tính

Mỗi bảng tính Excel đều chứa các trang tính và chúng ta muốn truy cập vào trang tính mà chúng ta muốn mở khóa. 

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

Ở đây, chúng ta đang truy cập vào trang tính đầu tiên trong sổ làm việc của mình. Nếu trang tính của bạn nằm ở nơi khác (ví dụ: chỉ mục trang tính 1), bạn có thể điều chỉnh chỉ mục cho phù hợp.

## Bước 4: Bỏ bảo vệ trang tính

Đây chính là phần kỳ diệu! 

```csharp
worksheet.Unprotect("");
```

 Nếu bảng tính của bạn được bảo vệ bằng mật khẩu và bạn biết mật khẩu, bạn sẽ thay thế chuỗi rỗng`""` bằng mật khẩu thực tế. Nếu bạn không biết, hãy để trống và chạy để xem nó có hoạt động không.

## Bước 5: Lưu sổ làm việc

Bây giờ chúng ta đã bỏ bảo vệ bảng tính, đã đến lúc lưu các thay đổi. 

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Dòng này lưu sổ làm việc với tên mới để đảm bảo chúng ta không ghi đè lên tệp gốc. 

## Bước 6: Xử lý ngoại lệ

Cuối cùng, hãy giải quyết mọi vấn đề tiềm ẩn có thể phát sinh. 

```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
    Console.ReadLine();
}
```

Khối catch này sẽ hiển thị bất kỳ lỗi nào bạn có thể gặp phải để bạn có thể gỡ lỗi dễ dàng. 

## Phần kết luận

Và bạn đã có nó! Bạn đã mở khóa thành công một bảng tính Excel được bảo vệ bằng mật khẩu bằng Aspose.Cells cho .NET. Chỉ với một vài dòng mã, bạn có thể lấy lại quyền truy cập vào dữ liệu quan trọng của mình. Sức mạnh và tính linh hoạt nằm trong tầm tay bạn với thư viện tuyệt vời này. Hoàn hảo cho các nhà phát triển muốn hợp lý hóa tương tác Microsoft Excel của họ, Aspose.Cells không chỉ là một công cụ hiệu quả — mà còn là một công cụ thiết yếu.

## Câu hỏi thường gặp

### Tôi có thể mở khóa bảng tính Excel mà không cần mật khẩu không?  
Có, bạn có thể thử mở khóa trang tính được bảo vệ mà không cần biết mật khẩu bằng cách để trống trường mật khẩu.

### Aspose.Cells có miễn phí sử dụng không?  
 Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để sử dụng lâu dài, bạn sẽ cần mua giấy phép. Kiểm tra[Mua trang](https://purchase.aspose.com/buy).

### Aspose.Cells hỗ trợ những định dạng nào?  
Aspose.Cells hỗ trợ nhiều định dạng Excel, bao gồm XLS, XLSX, CSV, v.v.

### Làm thế nào để cài đặt Aspose.Cells?  
 Bạn có thể cài đặt nó thông qua NuGet hoặc tải xuống trực tiếp từ[đây](https://releases.aspose.com/cells/net/).

### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?  
 Bạn có thể tìm thấy sự hỗ trợ từ cộng đồng trên[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
