---
title: Thay đổi dữ liệu nguồn của bảng Pivot theo chương trình trong .NET
linktitle: Thay đổi dữ liệu nguồn của bảng Pivot theo chương trình trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thay đổi dữ liệu nguồn bảng trục theo chương trình bằng Aspose.Cells cho .NET với hướng dẫn từng bước toàn diện của chúng tôi.
weight: 10
url: /vi/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi dữ liệu nguồn của bảng Pivot theo chương trình trong .NET

## Giới thiệu
Trong thế giới phân tích dữ liệu, ít công cụ nào tỏa sáng như Microsoft Excel. Hàng ngày, vô số người dùng phụ thuộc vào Excel để quản lý và phân tích dữ liệu, nhưng đằng sau hậu trường, nó phức tạp hơn nhiều so với việc chỉ nhấp và kéo. Nếu bạn từng muốn thao tác theo chương trình các tệp Excel—cụ thể là để thay đổi dữ liệu nguồn của bảng trục—bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng ta sẽ khám phá cách bạn có thể đạt được điều này bằng cách sử dụng Aspose.Cells cho .NET. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới dấn thân vào biển lập trình, bạn sẽ thấy hướng dẫn này chứa đầy thông tin có giá trị và dễ làm theo.
## Điều kiện tiên quyết
Trước khi bắt đầu hành trình thay đổi dữ liệu nguồn của bảng trục, hãy đảm bảo rằng bạn đã thiết lập mọi thứ và sẵn sàng thực hiện:
1. Visual Studio: Đảm bảo bạn đã cài đặt bản sao Microsoft Visual Studio vì chúng ta sẽ viết mã ở đây.
2. Thư viện Aspose.Cells: Bạn sẽ cần phải tải xuống và tham chiếu thư viện Aspose.Cells trong dự án của bạn. Bạn có thể tải xuống[đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Mặc dù hướng dẫn này được đơn giản hóa, nhưng việc nắm vững C# sẽ giúp bạn hiểu rõ hơn về mã.
4. Tệp Excel: Bạn nên có một tệp Excel mẫu (như "Book1.xlsx") chứa bảng tổng hợp mà chúng ta có thể thao tác.
Được rồi, sau khi đã kiểm tra xong các điều kiện tiên quyết này, chúng ta có thể tiến hành nhập các gói cần thiết và bắt đầu viết mã!
## Nhập gói
Trước tiên, hãy nhập các gói chúng ta cần. Mở dự án C# của bạn trong Visual Studio và thêm các chỉ thị using sau vào đầu tệp mã của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào các lớp thiết yếu cần thiết để làm việc với các tệp Excel và thao tác nội dung của chúng bằng Aspose.Cells.

Bây giờ, chúng ta hãy chia nhỏ quy trình thành các bước dễ quản lý. Chúng ta sẽ hướng dẫn mở tệp Excel, sửa đổi bảng tính, thay đổi nguồn dữ liệu của bảng trục và lưu kết quả.
## Bước 1: Xác định thư mục tài liệu của bạn
 Đầu tiên, bạn cần chỉ định vị trí tệp Excel của bạn. Sửa đổi`dataDir` biến để trỏ tới thư mục chứa "Book1.xlsx" của bạn.
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
Dòng này thiết lập thư mục lưu trữ tệp Excel của bạn, giúp bạn truy cập dễ dàng hơn sau này.
## Bước 2: Chỉ định Đường dẫn đầu vào
Tiếp theo, hãy tạo một chuỗi để chỉ định đường dẫn đầy đủ đến tệp Excel đầu vào của bạn:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Điều này giúp đơn giản hóa việc truy cập tệp của bạn; bạn sẽ không phải nhập cùng một đường dẫn nhiều lần trong toàn bộ mã của mình.
## Bước 3: Tạo luồng tệp
 Bây giờ là lúc mở tệp Excel. Chúng ta sẽ tạo một`FileStream` cho phép bạn đọc nội dung của tệp Excel:
```csharp
// Tạo luồng tệp chứa tệp Excel cần mở
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Dòng này mở tệp ở chế độ đọc, cho phép chúng ta truy cập dữ liệu trong tệp.
## Bước 4: Tải Workbook
Sau khi luồng tệp đã sẵn sàng, bước tiếp theo là tải sổ làm việc:
```csharp
// Mở tệp Excel thông qua luồng tệp
Workbook workbook = new Workbook(fstream);
```
 Lệnh này lấy tệp Excel của bạn và tải nó vào một`Workbook` đối tượng. Sau khi tải xong, bạn có thể thao tác với tệp theo nhu cầu.
## Bước 5: Truy cập vào Bảng tính
Đã đến lúc đi sâu vào chi tiết. Chúng ta sẽ truy cập vào bảng tính đầu tiên trong sổ làm việc:
```csharp
// Truy cập vào trang tính đầu tiên trong tệp Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Tính năng này cho phép bạn truy cập trực tiếp vào dữ liệu trong bảng tính đầu tiên, giúp bạn dễ dàng sửa đổi.
## Bước 6: Điền dữ liệu mới
Tiếp theo, chúng ta muốn chèn dữ liệu mới vào các ô. Trong ví dụ này, chúng ta sẽ thêm một số dữ liệu mẫu:
```csharp
// Điền dữ liệu mới vào các ô của bảng tính
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Ở đây, chúng tôi đang đưa các giá trị "Golf", "Qtr4" và`7000` vào các ô cụ thể. Bạn có thể thay đổi các giá trị này thành bất kỳ giá trị nào phù hợp với nhu cầu của bạn.
## Bước 7: Thay đổi phạm vi được đặt tên
Bây giờ, chúng ta sẽ thay đổi phạm vi được đặt tên mà bảng trục tham chiếu đến. Điều này bao gồm việc tạo hoặc cập nhật một phạm vi:
```csharp
// Thay đổi phạm vi được đặt tên "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Bằng cách xác định phạm vi mới, chúng tôi đảm bảo rằng bảng trục sẽ sử dụng dữ liệu mới này khi làm mới.
## Bước 8: Lưu tệp Excel đã sửa đổi
Sau tất cả các thay đổi, điều quan trọng là phải lưu công việc của bạn! Hãy lưu sổ làm việc đã sửa đổi:
```csharp
// Lưu tệp Excel đã sửa đổi
workbook.Save(dataDir + "output.xls");
```
Lệnh này lưu sổ làm việc vào một tệp mới để bạn không ghi đè lên tệp gốc trừ khi bạn muốn!
## Bước 9: Đóng luồng tập tin
Cuối cùng, điều cần thiết là đóng luồng tệp để giải phóng mọi tài nguyên bạn đang sử dụng:
```csharp
// Đóng luồng tệp để giải phóng tất cả tài nguyên
fstream.Close();
```
Bước này đảm bảo ứng dụng của bạn không bị rò rỉ bộ nhớ và vẫn hoạt động hiệu quả.
## Phần kết luận
Xin chúc mừng! Bạn vừa thay đổi thành công dữ liệu nguồn của bảng trục theo chương trình trong .NET bằng Aspose.Cells. Chức năng này mở ra nhiều khả năng để tự động hóa các tác vụ Excel và cải thiện quy trình làm việc của bạn. Cho dù bạn đang cập nhật báo cáo tài chính, theo dõi dữ liệu bán hàng hay thậm chí chỉ chơi đùa với các tập dữ liệu, khả năng thực hiện theo chương trình có thể giúp bạn tiết kiệm rất nhiều thời gian và giảm nguy cơ xảy ra lỗi.

## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ để làm việc với các tệp Excel, cho phép người dùng tạo, sửa đổi và thao tác các tài liệu Excel theo chương trình.
### Tôi có thể thay đổi dữ liệu nguồn của các bảng trục hiện có bằng phương pháp này không?
Hoàn toàn đúng! Phương pháp này cho phép bạn cập nhật nguồn dữ liệu cho các bảng trục hiện có trong bảng tính Excel của bạn.
### Tôi có cần cài đặt Office để sử dụng Aspose.Cells không?
Không! Aspose.Cells là một thư viện độc lập, nghĩa là bạn không cần cài đặt Microsoft Office để làm việc với các tệp Excel.
### Aspose.Cells có miễn phí sử dụng không?
Aspose.Cells cung cấp phiên bản dùng thử miễn phí, nhưng để có đầy đủ chức năng, bạn sẽ phải mua giấy phép. Bạn có thể tìm thấy thông tin chi tiết[đây](https://purchase.aspose.com/buy).
### Tôi có thể tìm thêm ví dụ và hỗ trợ ở đâu?
 Để biết thêm ví dụ và hỗ trợ, hãy xem[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) và diễn đàn cộng đồng của họ[đây](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
