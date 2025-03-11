---
title: Lưu sổ làm việc vào định dạng CSV văn bản
linktitle: Lưu sổ làm việc vào định dạng CSV văn bản
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách chuyển đổi sổ làm việc Excel sang định dạng CSV dễ dàng bằng Aspose.Cells trong hướng dẫn toàn diện, từng bước này được thiết kế dành cho các nhà phát triển .NET.
weight: 17
url: /vi/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lưu sổ làm việc vào định dạng CSV văn bản

## Giới thiệu
Khi xử lý dữ liệu, định dạng bạn chọn có thể thực sự quyết định mức độ dễ dàng bạn có thể làm việc với nó. Trong số các định dạng phổ biến nhất để xử lý dữ liệu dạng bảng là CSV (Giá trị phân cách bằng dấu phẩy). Nếu bạn là nhà phát triển làm việc với các tệp Excel và cần chuyển đổi sổ làm việc sang định dạng CSV, Aspose.Cells for .NET là một thư viện tuyệt vời giúp đơn giản hóa nhiệm vụ này. Trong hướng dẫn này, chúng tôi sẽ chia nhỏ các bước để chuyển đổi sổ làm việc Excel sang định dạng CSV văn bản một cách liền mạch.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị mọi thứ để bắt đầu:
1. Kiến thức cơ bản về C# và .NET: Vì chúng ta sẽ viết mã bằng C#, nên việc quen thuộc với ngôn ngữ này và nền tảng .NET là điều cần thiết.
2. Thư viện Aspose.Cells: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells for .NET trong môi trường phát triển của mình. Bạn có thể tải xuống[đây](https://releases.aspose.com/cells/net/).
3. Visual Studio hoặc bất kỳ IDE C# nào: Bạn sẽ cần một môi trường phát triển tích hợp (IDE) để viết và thực thi mã của mình. Visual Studio là một lựa chọn phổ biến.
4. Sổ làm việc Excel: Chuẩn bị một sổ làm việc Excel mẫu (ví dụ: "book1.xls") có chứa một số dữ liệu để kiểm tra chuyển đổi.
## Nhập gói
Bây giờ chúng ta đã có các điều kiện tiên quyết, bước đầu tiên trong quy trình là nhập các gói cần thiết. Trong dự án C# của bạn, bạn cần bao gồm không gian tên sau ở đầu tệp mã của mình:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Các không gian tên này sẽ cung cấp cho bạn quyền truy cập vào các lớp và phương thức cần thiết để làm việc với các tệp Excel và quản lý luồng bộ nhớ.
## Bước 1: Xác định đường dẫn đến thư mục tài liệu
Bước đầu tiên trong quy trình của chúng tôi là xác định nơi lưu trữ tài liệu (sổ làm việc Excel). Điều này rất cần thiết vì nó cho phép chương trình của chúng tôi biết nơi tìm các tệp cần xử lý. 
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Hãy chắc chắn thay thế`"Your Document Directory"` với đường dẫn thực tế nơi tệp "book1.xls" của bạn nằm. Đây có thể là một thư mục trên máy tính của bạn hoặc đường dẫn đến máy chủ.
## Bước 2: Tải sổ làm việc nguồn của bạn
Tiếp theo, chúng ta cần tải bảng tính Excel sẽ được chuyển đổi sang định dạng CSV.
```csharp
// Tải sổ làm việc nguồn của bạn
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Các`Workbook` lớp từ thư viện Aspose.Cells cho phép thao tác và truy cập vào sổ làm việc Excel. Bằng cách truyền đường dẫn tệp, chúng tôi đang tải sổ làm việc đã chỉ định để xử lý.
## Bước 3: Khởi tạo một mảng byte cho dữ liệu sổ làm việc
Trước khi bắt đầu chuyển đổi bảng tính sang CSV, chúng ta cần khởi tạo một mảng byte trống sẽ lưu trữ toàn bộ dữ liệu của bảng tính.
```csharp
// Mảng 0 byte
byte[] workbookData = new byte[0];
```
Mảng byte này sẽ kết hợp dữ liệu từ mỗi bảng tính thành một cấu trúc duy nhất mà chúng ta có thể ghi ra tệp sau.
## Bước 4: Thiết lập tùy chọn lưu văn bản
Bây giờ, hãy thiết lập các tùy chọn về cách chúng ta muốn lưu định dạng văn bản. Bạn có thể chọn các dấu phân cách tùy chỉnh hoặc sử dụng tab.
```csharp
// Tùy chọn lưu văn bản. Bạn có thể sử dụng bất kỳ loại dấu phân cách nào
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Thiết lập tab làm dấu phân cách
```
 Trong ví dụ này, chúng tôi sử dụng ký tự tab làm dấu phân cách. Bạn có thể thay thế`'\t'` với bất kỳ ký tự nào bạn muốn, như dấu phẩy (`,`), tùy thuộc vào cách bạn muốn định dạng tệp CSV.
## Bước 5: Lặp lại qua từng trang tính
 Tiếp theo, chúng ta sẽ lặp lại tất cả các bảng tính trong sổ làm việc, lưu từng bảng tính vào`workbookData` mảng, nhưng trước tiên bạn phải chọn bảng tính nào để làm việc.
```csharp
// Sao chép từng dữ liệu bảng tính ở định dạng văn bản bên trong mảng dữ liệu bảng tính
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Lưu bảng tính đang hoạt động ở định dạng văn bản
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 Vòng lặp chạy qua từng trang tính trong sổ làm việc.`ActiveSheetIndex` được thiết lập sao cho mỗi lần lặp lại, chúng ta sẽ lưu bảng tính hiện tại. Kết quả sẽ được lưu vào bộ nhớ bằng cách sử dụng`MemoryStream`.
## Bước 6: Lấy dữ liệu bảng tính
 Sau khi lưu một bảng tính vào luồng bộ nhớ, bước tiếp theo là lấy dữ liệu này và thêm nó vào`workbookData` mảng.
```csharp
    // Lưu dữ liệu bảng tính vào mảng dữ liệu bảng tính
    ms.Position = 0; // Đặt lại vị trí của luồng bộ nhớ
    byte[] sheetData = ms.ToArray(); // Lấy mảng byte
```
`ms.Position = 0;` đặt lại vị trí để đọc sau khi viết. Sau đó, chúng ta sử dụng`ToArray()` để chuyển đổi luồng bộ nhớ thành một mảng byte chứa dữ liệu bảng tính.
## Bước 7: Kết hợp dữ liệu bảng tính
 Bây giờ, chúng ta sẽ kết hợp dữ liệu từ mỗi bảng tính thành một bảng tính duy nhất.`workbookData` mảng được khởi tạo trước đó.
```csharp
    // Kết hợp dữ liệu bảng tính này vào mảng dữ liệu sổ làm việc
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Chúng tôi tạo một mảng mới đủ lớn để chứa cả dữ liệu sổ làm việc hiện có và dữ liệu trang tính mới. Sau đó, chúng tôi sao chép dữ liệu hiện có và dữ liệu mới vào mảng kết hợp này để sử dụng sau.
## Bước 8: Lưu toàn bộ dữ liệu bảng tính vào tệp
 Cuối cùng, với tất cả dữ liệu được kết hợp trong`workbookData` mảng, chúng ta có thể lưu mảng này vào một đường dẫn tệp được chỉ định.
```csharp
//Lưu toàn bộ dữ liệu bảng tính vào tệp
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` lấy mảng byte kết hợp và ghi nó vào tệp văn bản có tên "out.txt" trong thư mục được chỉ định.
## Phần kết luận
Và bạn đã có nó! Bạn đã chuyển đổi thành công một sổ làm việc Excel sang định dạng CSV bằng Aspose.Cells cho .NET. Quá trình này không chỉ hiệu quả mà còn cho phép dễ dàng thao tác dữ liệu Excel để phân tích hoặc báo cáo thêm. Bây giờ bạn có thể tự động hóa các tác vụ xử lý dữ liệu của mình hoặc thậm chí tích hợp chức năng này vào các ứng dụng lớn hơn.
## Câu hỏi thường gặp
### Tôi có thể sử dụng các ký tự phân cách khác nhau cho tệp CSV không?
 Vâng, bạn có thể thay đổi`opts.Separator` với bất kỳ ký tự nào bạn muốn, chẳng hạn như dấu phẩy hoặc dấu gạch ngang.
### Aspose.Cells có miễn phí sử dụng không?
 Aspose.Cells không miễn phí, nhưng bạn có thể dùng thử miễn phí[đây](https://releases.aspose.com/).
### Ngoài CSV, tôi có thể lưu ở những định dạng nào?
Aspose.Cells cho phép lưu thành nhiều định dạng bao gồm XLSX, PDF, v.v.
### Tôi có thể xử lý các tệp Excel lớn bằng Aspose.Cells không?
Có, Aspose.Cells được thiết kế để xử lý các tệp lớn một cách hiệu quả, nhưng hiệu suất có thể phụ thuộc vào tài nguyên hệ thống.
### Tôi có thể tìm tài liệu chi tiết hơn ở đâu?
Bạn có thể tìm thấy tài liệu và ví dụ toàn diện trên[trang web tham khảo](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
