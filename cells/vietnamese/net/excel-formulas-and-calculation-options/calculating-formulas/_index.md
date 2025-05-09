---
"description": "Tự động hóa các tác vụ Excel của bạn với Aspose.Cells cho .NET. Học cách tính toán công thức theo chương trình trong hướng dẫn toàn diện này."
"linktitle": "Tính toán công thức trong Excel theo chương trình"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tính toán công thức trong Excel theo chương trình"
"url": "/vi/net/excel-formulas-and-calculation-options/calculating-formulas/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tính toán công thức trong Excel theo chương trình

## Giới thiệu
Trong thế giới dữ liệu ngày nay, việc tự động hóa các tác vụ có thể tiết kiệm thời gian và nâng cao hiệu quả, đặc biệt là khi xử lý bảng tính. Nếu bạn đã từng xử lý các công thức phức tạp trong Excel, bạn sẽ biết tầm quan trọng của việc xử lý đúng. Bằng cách sử dụng Aspose.Cells cho .NET, bạn có thể lập trình tính toán các công thức và quản lý các tệp Excel của mình một cách dễ dàng. Trong hướng dẫn này, chúng ta sẽ hướng dẫn từng bước liên quan đến việc tạo tệp Excel, thêm giá trị và công thức, sau đó tính toán các công thức đó bằng một chút C#. Hãy cùng tìm hiểu nhé!
## Điều kiện tiên quyết
Trước khi bắt đầu, bạn cần đảm bảo rằng mình đã chuẩn bị sẵn một số thứ:
1. Môi trường phát triển: Đảm bảo bạn có Visual Studio hoặc bất kỳ môi trường C# nào khác mà bạn có thể chạy các ứng dụng .NET.
2. Aspose.Cells cho .NET: Tải xuống và cài đặt thư viện Aspose.Cells. Bạn có thể lấy nó từ [Trang web Aspose](https://releases.aspose.com/cells/net/).
3. Hiểu biết cơ bản về C#: Kiến thức cơ bản về C# sẽ giúp bạn nắm bắt các khái niệm và đoạn mã chúng ta sẽ sử dụng.
4. .NET Framework: Đảm bảo phiên bản .NET Framework phù hợp được cài đặt trên máy của bạn.
5. Giấy phép Aspose.Cells: Nếu bạn muốn sử dụng nó sau thời gian dùng thử miễn phí, hãy cân nhắc việc mua [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
Bây giờ chúng ta đã chuẩn bị mọi thứ, hãy cùng tìm hiểu mã và phân tích từng bước nhé!
## Nhập gói
Trước khi viết bất kỳ mã nào, hãy đảm bảo bạn nhập các không gian tên cần thiết cho Aspose.Cells vào tệp C# của mình:
```csharp
using System.IO;
using Aspose.Cells;
```
Điều này cho phép bạn truy cập các chức năng do thư viện Aspose.Cells cung cấp để thao tác với các tệp Excel.
## Bước 1: Thiết lập thư mục tài liệu
Bắt đầu bằng cách xác định đường dẫn bạn muốn lưu tài liệu Excel. Điều quan trọng là phải đảm bảo thư mục này tồn tại hoặc tạo thư mục này nếu không.
```csharp
// Đường dẫn đến thư mục tài liệu
string dataDir = "Your Document Directory";
// Tạo thư mục nếu nó chưa có
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Trong bước này, bạn sẽ kiểm tra xem thư mục có tồn tại không. Nếu không, bạn sẽ tạo thư mục đó. Bước đơn giản này giúp tránh lỗi khi bạn cố gắng lưu tệp Excel sau này.
## Bước 2: Khởi tạo một đối tượng Workbook
## Tạo một Workbook mới
Bây giờ thư mục của bạn đã được thiết lập, hãy tạo một đối tượng Workbook đại diện cho tệp Excel của bạn:
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```
Dòng này chỉ đơn giản là tạo một sổ làm việc mới trong bộ nhớ. Hãy nghĩ về nó như việc mở một tệp Excel trống nơi bạn có thể bắt đầu thêm dữ liệu và công thức.
## Bước 3: Thêm một bảng tính mới
## Làm việc với các trang tính
Trong sổ làm việc của chúng tôi, chúng tôi muốn thêm một trang tính mới nơi chúng tôi có thể thao tác dữ liệu của mình. Sau đây là cách thực hiện:
```csharp
// Thêm một bảng tính mới vào đối tượng Excel
int sheetIndex = workbook.Worksheets.Add();
// Lấy tham chiếu của bảng tính mới được thêm vào bằng cách chuyển chỉ mục trang tính của nó
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Đầu tiên, bạn thêm một bảng tính mới, bảng tính này sẽ tự động cung cấp cho bạn chỉ mục của bảng tính đó. Tiếp theo, bạn lấy bảng tính đó theo chỉ mục của nó. Giống như mở một tab mới trong sổ làm việc Excel của bạn!
## Bước 4: Chèn giá trị vào ô
## Điền dữ liệu
Bây giờ chúng ta đã tạo xong bảng tính, chúng ta cần thêm một số dữ liệu vào đó:
```csharp
// Thêm giá trị vào ô "A1"
worksheet.Cells["A1"].PutValue(1);
// Thêm giá trị vào ô "A2"
worksheet.Cells["A2"].PutValue(2);
// Thêm giá trị vào ô "A3"
worksheet.Cells["A3"].PutValue(3);
```
Trong bước này, bạn chèn giá trị vào ba ô đầu tiên (A1, A2, A3) của trang tính. Thao tác này tương tự như nhập giá trị trực tiếp vào trang tính Excel. 
## Bước 5: Thêm công thức
## Tổng hợp các giá trị
Sau khi nhập giá trị, đã đến lúc thêm công thức tính tổng của các ô này. Thực hiện như sau:
```csharp
// Thêm công thức SUM vào ô "A4"
worksheet.Cells["A4"].Formula = "=SUM(A1:A3)";
```
Dòng mã này thêm công thức SUM vào ô A4, công thức này sẽ tính tổng các giá trị từ A1 đến A3. Giống như viết công thức trong Excel, nhưng theo chương trình!
## Bước 6: Tính công thức
## Thực hiện phép tính
Bây giờ đến lúc phải tính toán! Chúng ta cần tính toán kết quả của các công thức đã nhập:
```csharp
// Tính toán kết quả của công thức
workbook.CalculateFormula();
```
Bằng cách gọi `CalculateFormula()`, bạn đang yêu cầu Workbook xử lý tất cả các công thức trong đó. Điều này tương tự như việc nhấn "Enter" sau khi nhập công thức vào ô Excel.
## Bước 7: Lấy lại giá trị đã tính toán
## Đọc kết quả
Sau khi các công thức được tính toán, chúng ta có thể lấy giá trị từ A4:
```csharp
// Lấy giá trị tính toán của ô
string value = worksheet.Cells["A4"].Value.ToString();
```
Trong bước này, bạn sẽ lấy kết quả của công thức SUM của chúng tôi. Điều này sẽ cho bạn tổng là 1 + 2 + 3, tức là 6!
## Bước 8: Lưu tệp Excel
## Ghi ra đĩa
Cuối cùng, lưu sổ làm việc vào thư mục đã chỉ định để bạn có thể truy cập sau:
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "output.xls");
```
Mã này lưu tệp Excel của bạn với tên "output.xls" trong thư mục bạn chỉ định. Giống như nhấp vào "Lưu dưới dạng" trong Excel và chọn nơi lưu tệp của bạn.
## Phần kết luận
Trong hướng dẫn này, chúng tôi đã đề cập đến cách tạo tệp Excel theo chương trình với Aspose.Cells cho .NET. Từ việc thêm giá trị và công thức đến tính toán và lưu kết quả cuối cùng, chúng tôi đã hướng dẫn từng bước quan trọng, đảm bảo bạn có nền tảng vững chắc cho các hoạt động tự động hóa trong tương lai.
## Câu hỏi thường gặp
### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện cho phép các nhà phát triển thao tác các tài liệu Excel trong các ứng dụng .NET theo cách lập trình.
### Tôi có thể đánh giá các công thức trong Excel bằng Aspose.Cells không?
Có! Bạn có thể sử dụng Aspose.Cells để tính toán và đánh giá các công thức giống như bạn làm trong Excel.
### Có bản dùng thử miễn phí cho Aspose.Cells không?
Chắc chắn rồi! Bạn có thể dùng thử miễn phí [đây](https://releases.aspose.com/).
### Tôi có thể thao tác với các tệp Excel hiện có bằng Aspose.Cells không?
Có, Aspose.Cells cho phép bạn tải các tệp Excel hiện có và chỉnh sửa chúng khi cần.
### Tôi có thể tìm thêm tài liệu về Aspose.Cells cho .NET ở đâu?
Bạn có thể tìm thấy tài liệu toàn diện [đây](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}