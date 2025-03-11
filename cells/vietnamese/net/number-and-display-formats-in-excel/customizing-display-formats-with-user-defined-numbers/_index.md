---
title: Tùy chỉnh định dạng hiển thị với số do người dùng xác định
linktitle: Tùy chỉnh định dạng hiển thị với số do người dùng xác định
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách tùy chỉnh định dạng hiển thị bằng Aspose.Cells cho .NET. Định dạng ngày tháng, phần trăm và tiền tệ bằng hướng dẫn từng bước này.
weight: 11
url: /vi/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tùy chỉnh định dạng hiển thị với số do người dùng xác định

## Giới thiệu
Làm việc với các tệp Excel thường yêu cầu định dạng tùy chỉnh các ô để trình bày dữ liệu theo cách có ý nghĩa hơn và thân thiện với người dùng hơn. Hãy tưởng tượng bạn đang xây dựng một tệp Excel cho một báo cáo. Bạn không chỉ muốn các con số thô. Bạn muốn ngày tháng, phần trăm và tiền tệ trông đẹp mắt và chuyên nghiệp, phải không? Đó là lúc các định dạng hiển thị tùy chỉnh phát huy tác dụng. Trong hướng dẫn này, chúng ta sẽ đi sâu vào Aspose.Cells cho .NET để chỉ cho bạn cách tùy chỉnh định dạng hiển thị của các con số bằng các thiết lập do người dùng xác định.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị mọi thứ để thực hiện theo hướng dẫn này. Sau đây là những gì bạn cần:
-  Đã cài đặt Aspose.Cells cho .NET.[Tải xuống tại đây](https://releases.aspose.com/cells/net/).
- Kiến thức cơ bản về C# và .NET framework.
-  Giấy phép hợp lệ cho Aspose.Cells. Nếu bạn không có, hãy lấy một[dùng thử miễn phí](https://releases.aspose.com/) hoặc yêu cầu một[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
- Một IDE như Visual Studio.
- .NET Framework 4.0 trở lên.
 Nếu bạn thiếu bất cứ điều gì, đừng lo lắng. Bạn luôn có thể truy cập lại các liên kết này để tải xuống các tệp cần thiết hoặc tìm kiếm sự trợ giúp từ[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9).
## Nhập không gian tên
Trước khi tìm hiểu mã, bạn cần nhập các không gian tên cần thiết để truy cập tất cả các chức năng cần thiết của Aspose.Cells.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Hai không gian tên này sẽ là công cụ cốt lõi của bạn trong hướng dẫn này. Bây giờ, chúng ta hãy chuyển sang phần thú vị:
## Bước 1: Thiết lập thư mục dự án
Trước tiên, bạn cần một nơi để lưu trữ các tệp của mình, đúng không? Hãy tạo một thư mục để lưu tệp Excel đầu ra. Trong bước này, chúng ta cũng sẽ đảm bảo thư mục tồn tại trước khi lưu bất kỳ thứ gì.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Chúng tôi đang định nghĩa một`dataDir` biến để lưu trữ đường dẫn tới tệp Excel đầu ra.
-  Sau đó chúng tôi kiểm tra xem thư mục có tồn tại hay không bằng cách sử dụng`System.IO.Directory.Exists()`.
-  Nếu thư mục không tồn tại, nó sẽ được tạo bằng cách sử dụng`System.IO.Directory.CreateDirectory()`.
## Bước 2: Tạo một bảng tính mới và thêm một trang tính
Bây giờ chúng ta đã có thư mục, hãy tạo một bảng tính Excel mới và thêm một bảng tính vào đó.
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
// Thêm một bảng tính mới vào đối tượng Excel
int i = workbook.Worksheets.Add();
// Lấy tham chiếu của bảng tính mới được thêm vào bằng cách chuyển chỉ mục trang tính của nó
Worksheet worksheet = workbook.Worksheets[i];
```
-  Đầu tiên, chúng ta tạo một cái mới`Workbook` đối tượng. Hãy nghĩ về điều này như tệp Excel của bạn.
-  Chúng tôi thêm một bảng tính mới vào sổ làm việc này bằng cách sử dụng`Add()`phương pháp và lưu trữ chỉ mục trong biến`i`.
-  Chúng tôi tham khảo bảng tính này bằng cách sử dụng`workbook.Worksheets[i]`.
## Bước 3: Thêm Ngày vào Ô và Tùy chỉnh Định dạng của Ô
 Bây giờ, hãy chèn ngày hiện tại vào một ô và định dạng nó để hiển thị theo cách tùy chỉnh. Thay vì định dạng ngày mặc định, chúng ta sẽ đặt định dạng tùy chỉnh như`d-mmm-yy`.
```csharp
// Thêm ngày hệ thống hiện tại vào ô "A1"
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Lấy kiểu của ô A1
Style style = worksheet.Cells["A1"].GetStyle();
// Thiết lập định dạng hiển thị tùy chỉnh để hiển thị ngày là "d-mmm-yy"
style.Custom = "d-mmm-yy";
// Áp dụng kiểu cho ô A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Chúng tôi thêm ngày hệ thống hiện tại vào ô`A1` sử dụng`PutValue(DateTime.Now)`.
-  Chúng tôi lấy lại kiểu hiện tại của ô`A1` sử dụng`GetStyle()`.
-  Chúng tôi sửa đổi kiểu của ô bằng cách thiết lập`style.Custom = "d-mmm-yy"`, định dạng ngày tháng để hiển thị ngày, tháng viết tắt và năm.
-  Cuối cùng, chúng tôi áp dụng kiểu mới cho ô với`SetStyle()`.
## Bước 4: Định dạng ô theo phần trăm
 Tiếp theo, chúng ta hãy làm việc với các con số. Chúng ta sẽ thêm một giá trị số vào một ô khác, chẳng hạn`A2`và định dạng nó theo phần trăm.
```csharp
//Thêm giá trị số vào ô "A2"
worksheet.Cells["A2"].PutValue(20);
// Nhận kiểu của ô A2
style = worksheet.Cells["A2"].GetStyle();
// Thiết lập định dạng hiển thị tùy chỉnh để hiển thị giá trị dưới dạng phần trăm
style.Custom = "0.0%";
// Áp dụng kiểu cho ô A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Chúng tôi thêm giá trị`20` đến tế bào`A2`.
-  Chúng tôi lấy lại phong cách của tế bào`A2` và thiết lập định dạng tùy chỉnh thành`0.0%` để hiển thị giá trị dưới dạng phần trăm (ví dụ: 20%).
-  Cuối cùng, chúng tôi áp dụng kiểu cho ô bằng cách sử dụng`SetStyle()`.
## Bước 5: Định dạng ô theo đơn vị tiền tệ
 Chúng ta hãy thêm một giá trị khác, ví dụ như vào ô`A3`và định dạng để hiển thị dưới dạng tiền tệ. Để làm cho mọi thứ thú vị hơn, chúng ta sẽ sử dụng định dạng hiển thị giá trị dương dưới dạng tiền tệ tính bằng pound và giá trị âm tính bằng đô la.
```csharp
// Thêm giá trị số vào ô "A3"
worksheet.Cells["A3"].PutValue(2546);
// Nhận kiểu ô A3
style = worksheet.Cells["A3"].GetStyle();
// Thiết lập định dạng hiển thị tùy chỉnh để hiển thị giá trị dưới dạng tiền tệ
style.Custom = "£#,##0;[Red]$-#,##0";
// Áp dụng kiểu cho ô A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Chúng tôi thêm giá trị`2546` đến tế bào`A3`.
-  Chúng tôi thiết lập một định dạng tùy chỉnh`£#,##0;[Red]$-#,##0`, hiển thị giá trị dương bằng dấu thăng và giá trị âm bằng màu đỏ bằng dấu đô la.
- Chúng tôi áp dụng kiểu cho ô bằng cách sử dụng`SetStyle()`.
## Bước 6: Lưu sổ làm việc
Bước cuối cùng là lưu sổ làm việc dưới dạng tệp Excel. Chúng tôi sẽ sử dụng định dạng Excel 97-2003 cho hướng dẫn này.
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  Các`Save()` phương pháp này lưu sổ làm việc vào thư mục được chỉ định.
-  Chúng tôi chọn`SaveFormat.Excel97To2003` để đảm bảo khả năng tương thích với các phiên bản Excel cũ hơn.
## Phần kết luận
Vậy là xong! Chúng tôi vừa tạo một tệp Excel, thêm định dạng ngày, phần trăm và tiền tệ tùy chỉnh vào các ô cụ thể bằng Aspose.Cells cho .NET và lưu tệp. Định dạng tùy chỉnh giúp tệp Excel của bạn dễ đọc và chuyên nghiệp hơn nhiều. Đừng quên khám phá các tùy chọn định dạng khác trong Aspose.Cells, như định dạng có điều kiện, để kiểm soát nhiều hơn nữa cách dữ liệu của bạn trông như thế nào.
## Câu hỏi thường gặp
### Làm thế nào tôi có thể áp dụng các tùy chọn định dạng phức tạp hơn trong Aspose.Cells?
Bạn có thể kết hợp nhiều kiểu định dạng khác nhau, chẳng hạn như màu phông chữ, đường viền và màu nền, với định dạng số tùy chỉnh.
### Tôi có thể áp dụng định dạng số tùy chỉnh cho một phạm vi ô không?
Có, Aspose.Cells cho phép bạn áp dụng một kiểu cho một phạm vi ô bằng cách sử dụng`Range.SetStyle()` phương pháp.
### Tôi có thể lưu sổ làm việc ở định dạng tệp nào khác?
 Aspose.Cells hỗ trợ nhiều định dạng, bao gồm XLSX, CSV và PDF. Chỉ cần thay đổi`SaveFormat` trong`Save()` phương pháp.
### Tôi có thể định dạng số âm theo cách khác không?
Hoàn toàn có thể! Bạn có thể sử dụng định dạng số tùy chỉnh để hiển thị số âm với nhiều màu sắc hoặc ký hiệu khác nhau.
### Aspose.Cells cho .NET có miễn phí không?
 Aspose.Cells cung cấp bản dùng thử miễn phí, nhưng để có đầy đủ chức năng, bạn sẽ cần một giấy phép hợp lệ. Bạn có thể nhận được[giấy phép tạm thời ở đây](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
