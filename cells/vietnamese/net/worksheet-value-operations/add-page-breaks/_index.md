---
title: Thêm ngắt trang trong trang tính bằng Aspose.Cells
linktitle: Thêm ngắt trang trong trang tính bằng Aspose.Cells
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thêm ngắt trang theo chiều ngang và chiều dọc trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Làm cho các tệp Excel của bạn thân thiện với máy in.
weight: 10
url: /vi/net/worksheet-value-operations/add-page-breaks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm ngắt trang trong trang tính bằng Aspose.Cells

## Giới thiệu
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thêm cả ngắt trang theo chiều ngang và chiều dọc vào bảng tính Excel của bạn. Bạn cũng sẽ thấy hướng dẫn từng bước về cách sử dụng Aspose.Cells cho .NET để dễ dàng thao tác ngắt trang và đến cuối hướng dẫn này, bạn sẽ thoải mái sử dụng các kỹ thuật này trong các dự án của riêng mình. Hãy bắt đầu nào!
## Điều kiện tiên quyết
Trước khi đi sâu vào mã, hãy đảm bảo rằng bạn đã sẵn sàng theo dõi hướng dẫn này. Sau đây là một số điều kiện tiên quyết:
- Visual Studio: Bạn cần cài đặt Visual Studio trên hệ thống của mình.
-  Aspose.Cells cho .NET: Bạn nên cài đặt thư viện Aspose.Cells. Nếu bạn chưa cài đặt, đừng lo lắng! Bạn có thể tải xuống phiên bản dùng thử miễn phí để bắt đầu. (Bạn có thể tải xuống[đây](https://releases.aspose.com/cells/net/)).
- .NET Framework: Hướng dẫn này giả định rằng bạn đang làm việc với .NET Framework hoặc .NET Core. Nếu bạn đang sử dụng một môi trường khác, quy trình có thể hơi khác một chút.
Ngoài ra, bạn nên có một số hiểu biết cơ bản về lập trình C# và khái niệm ngắt trang trong Excel.
## Nhập gói
Để bắt đầu làm việc với Aspose.Cells, chúng ta cần nhập các không gian tên có liên quan vào dự án của mình. Điều này cho phép chúng ta truy cập vào chức năng do Aspose.Cells cung cấp để thao tác với các tệp Excel.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Sau khi nhập các không gian tên này, bạn có thể bắt đầu tương tác với các tệp Excel và áp dụng nhiều sửa đổi khác nhau, bao gồm cả việc thêm ngắt trang.
Bây giờ bạn đã thiết lập xong, hãy cùng xem qua các bước để thêm ngắt trang vào bảng tính của bạn. Chúng tôi sẽ chia nhỏ từng phần của quy trình, giải thích chi tiết từng dòng mã.
## Bước 1: Thiết lập sổ làm việc của bạn
 Đầu tiên, bạn cần tạo một bảng tính mới.`Workbook` lớp trong Aspose.Cells biểu diễn một bảng tính Excel và là điểm khởi đầu để thao tác với các tệp Excel.
```csharp
// Xác định đường dẫn đến thư mục nơi tập tin của bạn sẽ được lưu
string dataDir = "Your Document Directory";
// Tạo một đối tượng Workbook mới
Workbook workbook = new Workbook();
```
Trong đoạn mã này:
- `dataDir` chỉ định nơi tệp của bạn sẽ được lưu.
-  Các`Workbook` đối tượng được tạo ra, sẽ được sử dụng để lưu trữ và thao tác với tệp Excel của bạn.
## Bước 2: Thêm Ngắt trang theo chiều ngang
Tiếp theo, chúng ta sẽ thêm ngắt trang theo chiều ngang vào worksheet. Ngắt trang theo chiều ngang sẽ chia worksheet thành hai phần theo chiều ngang, nghĩa là nó xác định vị trí nội dung sẽ ngắt sang trang mới theo chiều dọc khi in.
```csharp
//Thêm ngắt trang theo chiều ngang ở hàng 30
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
Trong ví dụ này:
- `Worksheets[0]` đề cập đến trang tính đầu tiên trong sổ làm việc (hãy nhớ rằng, các trang tính được đánh số từ 0).
- `HorizontalPageBreaks.Add("Y30")` thêm ngắt trang ở hàng 30. Điều này có nghĩa là nội dung trước hàng 30 sẽ xuất hiện trên một trang và mọi nội dung bên dưới sẽ bắt đầu trên một trang mới.
## Bước 3: Thêm ngắt trang theo chiều dọc
Tương tự, bạn có thể thêm ngắt trang theo chiều dọc. Thao tác này sẽ ngắt trang tính tại một cột cụ thể, đảm bảo rằng nội dung bên trái ngắt trang sẽ xuất hiện trên một trang và nội dung bên phải sẽ xuất hiện trên trang tiếp theo.
```csharp
// Thêm ngắt trang theo chiều dọc ở cột Y
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Đây:
-  Các`VerticalPageBreaks.Add("Y30")` phương pháp này thêm một ngắt trang theo chiều dọc tại cột Y (tức là sau cột thứ 25). Điều này sẽ tạo ra một ngắt trang giữa các cột X và Y.
## Bước 4: Lưu sổ làm việc
Sau khi thêm ngắt trang, bước cuối cùng là lưu sổ làm việc vào một tệp. Bạn có thể chỉ định đường dẫn nơi bạn muốn lưu tệp Excel.
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Thao tác này sẽ lưu sổ làm việc có các ngắt trang được thêm vào đường dẫn tệp đã chỉ định (`AddingPageBreaks_out.xls`).
## Phần kết luận
Thêm ngắt trang trong Excel là một tính năng quan trọng khi bạn làm việc với các tập dữ liệu lớn hoặc chuẩn bị tài liệu để in. Với Aspose.Cells for .NET, bạn có thể dễ dàng tự động hóa quy trình chèn ngắt trang theo chiều ngang và chiều dọc trong bảng tính Excel của mình, đảm bảo rằng tài liệu của bạn được sắp xếp hợp lý và dễ đọc.
## Câu hỏi thường gặp
### Làm thế nào để thêm nhiều ngắt trang trong Aspose.Cells cho .NET?
 Bạn có thể thêm nhiều ngắt trang bằng cách chỉ cần gọi`HorizontalPageBreaks.Add()` hoặc`VerticalPageBreaks.Add()` phương pháp nhiều lần với các tham chiếu ô khác nhau.
### Tôi có thể thêm ngắt trang vào một trang tính cụ thể của một sổ làm việc không?
 Có, bạn có thể chỉ định bảng tính bằng cách sử dụng`Worksheets[index]` tài sản nơi`index` là chỉ số bắt đầu từ số 0 của bảng tính.
### Làm thế nào để xóa ngắt trang trong Aspose.Cells cho .NET?
 Bạn có thể xóa ngắt trang bằng cách sử dụng`HorizontalPageBreaks.RemoveAt()` hoặc`VerticalPageBreaks.RemoveAt()` phương pháp bằng cách chỉ định chỉ mục ngắt trang mà bạn muốn xóa.
### Tôi phải làm sao nếu muốn tự động thêm ngắt trang dựa trên kích thước nội dung?
Aspose.Cells không cung cấp tính năng tự động thêm ngắt trang dựa trên kích thước nội dung, nhưng bạn có thể tính toán theo chương trình vị trí ngắt trang dựa trên số lượng hàng/cột.
### Tôi có thể thiết lập ngắt trang dựa trên phạm vi ô cụ thể không?
Có, bạn có thể chỉ định ngắt trang cho bất kỳ ô hoặc phạm vi nào bằng cách cung cấp tham chiếu ô tương ứng, chẳng hạn như "A1" hoặc "B15".

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
