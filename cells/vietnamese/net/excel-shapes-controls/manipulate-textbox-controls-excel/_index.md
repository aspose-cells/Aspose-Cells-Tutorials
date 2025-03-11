---
title: Thao tác điều khiển TextBox trong Excel
linktitle: Thao tác điều khiển TextBox trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thao tác hộp văn bản trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước dễ làm theo này.
weight: 15
url: /vi/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thao tác điều khiển TextBox trong Excel

## Giới thiệu
Nếu bạn đã từng làm việc với Excel, có lẽ bạn đã từng bắt gặp những hộp văn bản nhỏ cho phép bạn thêm văn bản nổi vào bảng tính. Nhưng nếu bạn cần thao tác các hộp văn bản đó theo chương trình thì sao? Đó chính là lúc Aspose.Cells for .NET trở nên hữu ích. Với nó, bạn có thể truy cập và sửa đổi các hộp văn bản một cách dễ dàng, khiến nó trở nên hoàn hảo để tự động hóa các tác vụ hoặc tùy chỉnh báo cáo. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn quy trình thao tác các hộp văn bản trong Excel bằng Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi đi sâu vào mã thực tế, hãy đảm bảo rằng bạn đã thiết lập mọi thứ đúng cách:
1.  Aspose.Cells cho .NET: Bạn cần tải xuống thư viện Aspose.Cells cho .NET. Bạn có thể tìm thấy liên kết tải xuống[đây](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển .NET: Bất kỳ IDE nào hỗ trợ .NET, chẳng hạn như Visual Studio, đều có thể sử dụng được.
3. Kiến thức cơ bản về C#: Hướng dẫn này giả định rằng bạn đã quen thuộc với cú pháp C# cơ bản và cấu trúc của bảng tính Excel.
4.  Tệp Excel: Một tệp Excel hiện có với các hộp văn bản (chúng ta sẽ sử dụng`book1.xls`trong ví dụ này).
5.  Giấy phép Aspose: Nếu bạn không sử dụng phiên bản dùng thử miễn phí, bạn sẽ cần[mua](https://purchase.aspose.com/buy) giấy phép hoặc có được một[tạm thời một](https://purchase.aspose.com/temporary-license/).
Bây giờ, chúng ta hãy cùng tìm hiểu từng bước nhé!
## Nhập gói
Trước khi bạn có thể thao tác với sổ làm việc Excel và hộp văn bản bằng Aspose.Cells, bạn cần nhập các không gian tên cần thiết. Sau đây là đoạn mã bạn sẽ sử dụng ở đầu tệp C# của mình:
```csharp
using System.IO;
using Aspose.Cells;
```
Các gói này cung cấp cho bạn quyền truy cập vào thao tác trên sổ làm việc, trang tính và các đối tượng vẽ (như hộp văn bản).
Bây giờ chúng ta đã thiết lập mọi thứ, hãy chia nhỏ quá trình thao tác hộp văn bản thành các bước dễ thực hiện.
## Bước 1: Thiết lập thư mục sổ làm việc của bạn
 Bước đầu tiên là chỉ định vị trí các tệp Excel của bạn trên hệ thống. Bạn sẽ cần thay thế chỗ giữ chỗ`Your Document Directory` với đường dẫn thực tế đến tệp của bạn. Đường dẫn này được lưu trữ trong`dataDir` biến để dễ dàng tham khảo trong toàn bộ mã.
```csharp
string dataDir = "Your Document Directory";
```
Điều này cho phép chương trình của bạn biết nơi tìm tệp Excel đầu vào (`book1.xls`) và nơi lưu tệp đầu ra.
## Bước 2: Mở tệp Excel
Tiếp theo, bạn sẽ cần tải tệp Excel hiện có vào đối tượng Aspose.Cells Workbook. Workbook này hoạt động như một container cho dữ liệu Excel của bạn, cho phép bạn truy cập vào các trang tính và bất kỳ đối tượng vẽ nào (như hộp văn bản).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Các`Workbook` class từ Aspose.Cells sẽ tải tệp Excel được chỉ định từ thư mục của bạn. Nếu tệp không tồn tại trong thư mục được chỉ định, nó sẽ đưa ra ngoại lệ, vì vậy hãy đảm bảo đường dẫn là chính xác.
## Bước 3: Truy cập vào trang tính đầu tiên
Bây giờ bạn đã tải xong sổ làm việc, bạn có thể truy cập vào các trang tính của sổ làm việc đó. Trong ví dụ này, chúng ta đang truy cập vào trang tính đầu tiên trong sổ làm việc, được lưu trữ ở chỉ mục 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 Các`Worksheets` thuộc tính cho phép bạn truy cập vào tất cả các trang tính trong sổ làm việc. Ở đây, chúng tôi chỉ quan tâm đến trang tính đầu tiên, nhưng bạn có thể làm việc với bất kỳ trang tính nào bằng cách chỉ định chỉ mục chính xác.
## Bước 4: Lấy đối tượng TextBox đầu tiên
Hộp văn bản trong một trang tính Excel được coi là đối tượng vẽ. Lớp Aspose.Cells.Drawing.TextBox cung cấp các thuộc tính và phương thức để thao tác chúng. Để truy cập hộp văn bản đầu tiên trên trang tính, bạn chỉ cần tham chiếu đến`TextBoxes` bộ sưu tập theo chỉ mục.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Điều này lấy đối tượng hộp văn bản đầu tiên từ`TextBoxes` bộ sưu tập. Nếu bảng tính của bạn không có hộp văn bản ở chỉ mục đó, nó sẽ đưa ra ngoại lệ, vì vậy hãy luôn đảm bảo chỉ mục hợp lệ.
## Bước 5: Lấy văn bản từ hộp văn bản đầu tiên
 Sau khi truy cập vào hộp văn bản, bạn có thể trích xuất văn bản chứa trong đó bằng cách sử dụng`.Text` tài sản.
```csharp
string text0 = textbox0.Text;
```
 Điều này sẽ chụp văn bản từ hộp văn bản đầu tiên vào`text0` chuỗi. Bây giờ bạn có thể hiển thị, thao tác hoặc xử lý chuỗi đó trong ứng dụng của mình.
## Bước 6: Truy cập Đối tượng TextBox thứ hai
Để thao tác nhiều hộp văn bản, chúng ta có thể lấy thêm các hộp văn bản khác từ bảng tính. Ở đây, chúng ta sẽ truy cập hộp văn bản thứ hai theo cách tương tự như hộp văn bản đầu tiên:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Một lần nữa, chúng ta truy cập hộp văn bản thứ hai bằng cách sử dụng chỉ mục 1 từ`TextBoxes`bộ sưu tập.
## Bước 7: Lấy văn bản từ hộp văn bản thứ hai
Giống như hộp văn bản đầu tiên, bạn có thể lấy văn bản từ hộp văn bản thứ hai và lưu trữ nó trong một chuỗi:
```csharp
string text1 = textbox1.Text;
```
Thao tác này sẽ lấy văn bản hiện tại từ hộp văn bản thứ hai.
## Bước 8: Sửa đổi văn bản trong hộp văn bản thứ hai
 Bây giờ, giả sử bạn muốn sửa đổi văn bản bên trong hộp văn bản thứ hai. Bạn có thể dễ dàng thực hiện việc này bằng cách gán một chuỗi mới cho`.Text` thuộc tính của đối tượng hộp văn bản.
```csharp
textbox1.Text = "This is an alternative text";
```
Thao tác này sẽ thay đổi văn bản bên trong hộp văn bản thứ hai thành nội dung mới. Bạn có thể chèn bất kỳ văn bản nào vào đây tùy theo yêu cầu của bạn.
## Bước 9: Lưu tệp Excel đã cập nhật
 Cuối cùng, sau khi sửa đổi các hộp văn bản, đã đến lúc lưu các thay đổi của bạn. Aspose.Cells cho phép bạn lưu sổ làm việc đã sửa đổi bằng cách sử dụng`.Save()` phương pháp. Bạn có thể chỉ định tên tệp mới hoặc ghi đè lên tệp hiện có.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Thao tác này sẽ lưu tệp Excel đã sửa đổi vào đường dẫn đầu ra được chỉ định của bạn. Bây giờ, khi bạn mở tệp Excel, bạn sẽ thấy những thay đổi bạn đã thực hiện đối với hộp văn bản.
## Phần kết luận
Và bạn đã có nó! Bạn vừa học cách thao tác các hộp văn bản trong Excel bằng Aspose.Cells cho .NET. Cho dù bạn đang tự động tạo báo cáo, tùy chỉnh các trang tính Excel hay xây dựng nội dung động, Aspose.Cells giúp bạn dễ dàng kiểm soát mọi khía cạnh của tệp Excel theo chương trình. Từ việc trích xuất và sửa đổi văn bản đến lưu các tệp đã cập nhật, thư viện này là một công cụ mạnh mẽ dành cho các nhà phát triển làm việc với Excel trong môi trường .NET.
## Câu hỏi thường gặp
### Tôi có thể thao tác với các đối tượng vẽ khác bằng Aspose.Cells ngoài hộp văn bản không?
Có, Aspose.Cells cho phép bạn thao tác với các đối tượng vẽ khác như hình dạng, biểu đồ và hình ảnh.
### Điều gì xảy ra nếu tôi cố truy cập vào hộp văn bản không tồn tại?
 Nếu chỉ mục của hộp văn bản nằm ngoài phạm vi, một`IndexOutOfRangeException` sẽ được ném đi.
### Tôi có thể thêm hộp văn bản mới vào bảng tính Excel bằng Aspose.Cells không?
 Có, Aspose.Cells cho phép bạn thêm hộp văn bản mới bằng cách sử dụng`AddTextBox` phương pháp.
### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
 Có, bạn sẽ cần phải mua giấy phép, nhưng Aspose cũng cung cấp một[dùng thử miễn phí](https://releases.aspose.com/).
### Tôi có thể sử dụng Aspose.Cells với các ngôn ngữ lập trình khác ngoài C# không?
Có, Aspose.Cells có thể được sử dụng với bất kỳ ngôn ngữ nào hỗ trợ .NET, chẳng hạn như VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
