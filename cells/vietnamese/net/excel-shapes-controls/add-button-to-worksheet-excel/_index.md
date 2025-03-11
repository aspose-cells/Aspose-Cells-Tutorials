---
title: Thêm nút vào trang tính trong Excel
linktitle: Thêm nút vào trang tính trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm nút vào bảng tính Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Cải thiện bảng tính Excel bằng các nút tương tác.
weight: 12
url: /vi/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm nút vào trang tính trong Excel

## Giới thiệu
Bảng tính Excel rất linh hoạt và thường được sử dụng để quản lý dữ liệu, nhưng đôi khi chúng cần thêm tính tương tác. Một trong những cách tốt nhất để nâng cao trải nghiệm của người dùng là thêm các nút vào bảng tính. Các nút này có thể kích hoạt macro hoặc điều hướng người dùng đến các liên kết hữu ích. Nếu bạn là nhà phát triển .NET làm việc với các tệp Excel, Aspose.Cells for .NET cung cấp một cách dễ dàng để thao tác sổ làm việc Excel theo chương trình, bao gồm cả việc thêm các nút.
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm nút vào bảng tính trong Excel bằng Aspose.Cells cho .NET. Chúng tôi sẽ đề cập đến mọi chi tiết, từ thiết lập các điều kiện tiên quyết đến hướng dẫn từng bước. Hãy cùng bắt đầu!
## Điều kiện tiên quyết
Trước khi bạn có thể làm theo hướng dẫn này, hãy đảm bảo rằng bạn đã cài đặt các công cụ và gói sau:
-  Thư viện Aspose.Cells cho .NET: Bạn có thể tải xuống từ[đây](https://releases.aspose.com/cells/net/).
- Môi trường phát triển .NET: Đảm bảo bạn đã cài đặt môi trường .NET đang hoạt động như Visual Studio.
- Hiểu biết cơ bản về C#: Bạn nên nắm rõ những kiến thức cơ bản về lập trình C#.
-  Giấy phép: Bạn sẽ cần một giấy phép hợp lệ. Nếu bạn không có, bạn có thể xin một[dùng thử miễn phí](https://releases.aspose.com/) hoặc nộp đơn xin[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
Chúng ta hãy chuyển sang nhập các gói cần thiết.
## Nhập gói
Trước khi bắt đầu viết mã, bạn sẽ cần nhập các gói cần thiết vào dự án .NET của mình. Sau đây là một đoạn mã đơn giản giúp bạn nhập Aspose.Cells vào dự án của mình:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Bây giờ chúng ta đã nhập các gói cần thiết, hãy chia nhỏ ví dụ thành hướng dẫn từng bước chi tiết.
## Bước 1: Thiết lập Sổ làm việc và Bảng tính
Ở bước đầu tiên này, chúng ta sẽ tạo một bảng tính Excel mới và tham chiếu đến bảng tính đầu tiên.
```csharp
// Xác định đường dẫn đến thư mục tài liệu của bạn.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Tạo một Workbook mới.
Workbook workbook = new Workbook();
// Lấy bài tập đầu tiên trong sổ làm việc.
Worksheet sheet = workbook.Worksheets[0];
```

-  Tạo sổ làm việc: Chúng tôi bắt đầu bằng cách tạo một sổ làm việc mới`Workbook` đối tượng, đại diện cho một tệp Excel.
-  Tài liệu tham khảo:`Worksheets[0]` lệnh này sẽ lấy trang tính đầu tiên trong sổ làm việc mà chúng ta sẽ sửa đổi.
Bước này đặt nền tảng bằng cách tạo một tệp Excel trống với một bảng tính duy nhất.
## Bước 2: Thêm nút vào trang tính
Tiếp theo, chúng ta sẽ thêm một nút vào bảng tính. Đây chính là nơi phép thuật xảy ra!
```csharp
// Thêm một nút mới vào bảng tính.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- Phương pháp AddButton: Phương pháp này thêm một nút vào vị trí được chỉ định trong bảng tính. Các tham số xác định vị trí của nút (hàng, cột, độ lệch x, độ lệch y) và kích thước (chiều cao, chiều rộng).
- Hàng và Cột: Nút được đặt ở hàng 2 và cột 0, không có khoảng bù bổ sung nào.
- Kích thước: Chiều cao của nút được đặt là 28 và chiều rộng là 80.
Bước này đã thêm thành công một nút vào bảng tính, nhưng chúng ta vẫn chưa hoàn thành, hãy tùy chỉnh nó.
## Bước 3: Thiết lập Thuộc tính Nút
Bây giờ là lúc tùy chỉnh giao diện của nút bằng cách thiết lập văn bản, phông chữ và vị trí của nút.
```csharp
// Đặt tiêu đề cho nút.
button.Text = "Aspose";
// Đặt Kiểu vị trí, cách Nút được gắn vào các ô.
button.Placement = PlacementType.FreeFloating;
```

- Văn bản: Chúng tôi đặt tiêu đề của nút là “Aspose”.
-  Vị trí: Chúng tôi xác định cách nút được định vị so với các ô trong bảng tính.`FreeFloating` cho phép nút di chuyển độc lập với các ô.
Bước này sẽ cá nhân hóa tiêu đề và vị trí của nút.
## Bước 4: Tùy chỉnh phông chữ của nút
Hãy làm cho nút này trở nên thú vị hơn bằng cách tùy chỉnh các thuộc tính phông chữ.
```csharp
// Đặt tên phông chữ.
button.Font.Name = "Tahoma";
// Đặt chữ in đậm cho chuỗi chú thích.
button.Font.IsBold = true;
// Đặt màu thành màu xanh.
button.Font.Color = Color.Blue;
```

- Tên phông chữ: Chúng tôi đổi phông chữ thành "Tahoma", đây là phông chữ sạch và hiện đại.
- In đậm: Chúng tôi in đậm chữ trên nút để nhấn mạnh.
- Màu sắc: Màu phông chữ được đặt thành màu xanh lam, làm nổi bật văn bản trên nút.
Bước này giúp cải thiện giao diện của nút, đảm bảo nút vừa có chức năng vừa đẹp mắt.
## Bước 5: Thêm siêu liên kết vào nút
Bạn có thể làm cho nút này hữu ích hơn bằng cách thêm siêu liên kết.
```csharp
// Đặt siêu liên kết cho nút.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink: Chúng tôi sử dụng phương pháp này để thêm siêu liên kết có thể nhấp vào nút. Khi nhấp vào, nút sẽ điều hướng đến trang web Aspose.
Bước này tăng thêm tính tương tác cho nút, giúp nút có chức năng hơn là chỉ mang tính thẩm mỹ.
## Bước 6: Lưu tệp Excel
Sau khi mọi thứ đã được thiết lập, đừng quên lưu lại thay đổi nhé!
```csharp
// Lưu tập tin.
workbook.Save(dataDir + "book1.out.xls");
```

-  Phương pháp lưu: Chúng tôi sử dụng`Save` phương pháp ghi sổ làm việc đã sửa đổi vào một tệp mới. Tệp sẽ được lưu trong thư mục đã chỉ định.
Xin chúc mừng! Bây giờ bạn đã thêm một nút tùy chỉnh hoàn toàn vào bảng tính Excel.
## Phần kết luận
Thêm nút vào bảng tính Excel có thể cải thiện đáng kể chức năng của bảng tính, giúp chúng tương tác và thân thiện với người dùng hơn. Với Aspose.Cells for .NET, bạn có thể đạt được điều này chỉ với một vài dòng mã, như chúng tôi đã trình bày trong hướng dẫn này.
Aspose.Cells for .NET là một thư viện mạnh mẽ cung cấp vô số khả năng thao tác Excel. Cho dù bạn đang tự động hóa các tác vụ hay thêm các tính năng mới vào bảng tính của mình, thư viện này là giải pháp dành cho bạn.
 Nếu bạn chưa làm,[tải xuống thư viện Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/) và bắt đầu cải thiện tệp Excel của bạn.
## Câu hỏi thường gặp
### Tôi có thể sử dụng các hình dạng khác ngoài các nút trong Aspose.Cells cho .NET không?
Có, Aspose.Cells cho phép bạn thêm nhiều hình dạng khác nhau, bao gồm hộp kiểm, nút radio, v.v.
### Tôi có thể kích hoạt macro từ nút được thêm thông qua Aspose.Cells không?
Có, bạn có thể liên kết nút với một macro, mặc dù bạn sẽ cần xử lý mã macro riêng biệt trong Excel.
### Làm thế nào để tôi có thể tự động thay đổi kích thước nút theo ô?
 Sử dụng`PlacementType.Move` thuộc tính cho phép nút thay đổi kích thước theo ô.
### Có thể thêm nhiều nút vào một bảng tính không?
 Chắc chắn rồi! Bạn có thể thêm bao nhiêu nút tùy thích bằng cách gọi`AddButton` phương pháp nhiều lần.
### Tôi có thể tùy chỉnh thêm giao diện của nút không?
Có, bạn có thể sửa đổi nhiều thuộc tính, bao gồm màu nền, kiểu đường viền, v.v.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
