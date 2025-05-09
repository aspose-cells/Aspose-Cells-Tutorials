---
"description": "Tìm hiểu cách lấy và liệt kê phông chữ từ bảng tính Excel bằng Aspose.Cells cho .NET với hướng dẫn dễ làm theo này."
"linktitle": "Lấy danh sách các phông chữ được sử dụng trong bảng tính"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Lấy danh sách các phông chữ được sử dụng trong bảng tính"
"url": "/vi/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lấy danh sách các phông chữ được sử dụng trong bảng tính

## Giới thiệu
Bạn đã bao giờ thấy mình đang cuộn qua một bảng tính Excel, tự hỏi về các phông chữ được sử dụng trong các ô khác nhau của nó chưa? Có thể bạn đã gặp một tài liệu cũ và muốn biết những lựa chọn về kiểu chữ nào đã được thực hiện? Vâng, bạn thật may mắn! Với Aspose.Cells dành cho .NET, nó giống như có một hộp công cụ cho phép bạn sàng lọc và khám phá những bí mật về phông chữ ẩn trong các bảng tính của mình. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn cách dễ dàng lấy danh sách tất cả các phông chữ được sử dụng trong một tệp Excel. Hãy thắt dây an toàn và cùng khám phá thế giới của các bảng tính!
## Điều kiện tiên quyết
Trước khi bắt đầu viết mã, có một vài thứ bạn cần để bắt đầu. Đừng lo lắng, nó thực sự đơn giản. Sau đây là danh sách kiểm tra những gì bạn cần:
1. Visual Studio: Đảm bảo bạn đã cài đặt phiên bản Visual Studio trên máy của mình. Đây là nơi chúng ta sẽ viết mã.
2. Aspose.Cells cho .NET: Bạn cần có thư viện Aspose.Cells. Nếu bạn chưa tải xuống, bạn có thể lấy nó từ [địa điểm](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Một chút hiểu biết về lập trình C# chắc chắn sẽ giúp bạn dễ dàng điều hướng qua mã.
4. Tệp Excel mẫu: Bạn sẽ cần một tệp Excel mẫu, như "sampleGetFonts.xlsx," để làm việc. Đây là nơi chúng ta sẽ áp dụng khám phá phông chữ của mình.
Khi bạn đã chuẩn bị mọi thứ xong xuôi, bạn đã sẵn sàng để bắt đầu viết mã!
## Nhập gói
Để bắt đầu, hãy nhập các không gian tên cần thiết. Trong .NET, việc nhập các gói cũng giống như việc mời đúng khách đến dự tiệc của bạn—nếu không có họ, mọi thứ sẽ không diễn ra suôn sẻ.
Sau đây là cách nhập Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Với dòng lệnh đơn giản này, chúng ta sẽ mời chức năng cốt lõi của Aspose.Cells vào dự án của mình. Bây giờ, hãy chuyển sang tải sổ làm việc.
## Bước 1: Thiết lập thư mục tài liệu
Trước tiên, trước khi đi sâu vào mã, bạn cần đặt đường dẫn đến thư mục tài liệu của mình. Đây là nơi lưu trữ tệp Excel của bạn. 
```csharp
string dataDir = "Your Document Directory";
```
Bạn sẽ thay thế “Your Document Directory” bằng đường dẫn thực tế nơi tệp Excel của bạn nằm. Hãy nghĩ về điều này như nói với chương trình, “Này, đây là nơi tôi đã cất tệp Excel của mình; hãy kiểm tra xem!”
## Bước 2: Tải Sổ làm việc nguồn
Đã đến lúc tải tệp Excel lên. Chúng ta sẽ tạo một phiên bản mới của `Workbook` lớp và truyền vào đường dẫn của tệp. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
Chuyện gì đang xảy ra ở đây? Về cơ bản chúng tôi đang mở cánh cửa đến bảng tính của mình. `Workbook` Lớp này cho phép chúng ta tương tác với nội dung của tệp Excel. 
## Bước 3: Lấy tất cả phông chữ
Bây giờ đến khoảnh khắc kỳ diệu—hãy thực sự lấy lại các phông chữ! `GetFonts()` phương pháp này chính là tấm vé vàng của chúng ta.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
Ở đây, chúng tôi yêu cầu sổ làm việc tiết lộ tất cả các phông chữ được sử dụng trong đó. `fnts` Mảng sẽ chứa đựng kho báu của chúng ta.
## Bước 4: In Phông chữ
Cuối cùng, hãy lấy những phông chữ đó và in chúng ra. Điều này sẽ giúp chúng ta xác minh những gì chúng ta đã tìm thấy.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
Vòng lặp này chạy qua từng phông chữ trong `fnts` mảng, xuất chúng ra bảng điều khiển từng cái một. Giống như việc thể hiện tất cả các lựa chọn kiểu chữ thú vị mà bạn có trong tệp Excel của mình vậy!
## Phần kết luận
Và bạn đã có nó! Chỉ với một vài dòng mã, bạn đã lấy và in thành công danh sách các phông chữ được sử dụng trong bảng tính Excel của mình bằng Aspose.Cells cho .NET. Đây không chỉ là về phông chữ; mà là về việc hiểu được những nét tinh tế trong tài liệu của bạn, cải thiện bài thuyết trình của bạn và làm chủ nghệ thuật sắp chữ trong bảng tính của bạn. Cho dù bạn là một nhà phát triển hay chỉ là người thích mày mò với Excel, đoạn mã nhỏ này có thể là một bước ngoặt. 
## Câu hỏi thường gặp
### Tôi có cần phải cài đặt Aspose.Cells riêng không?
Có, bạn cần tải xuống và tham chiếu thư viện trong dự án của mình. 
### Tôi có thể sử dụng Aspose.Cells cho các định dạng khác không?
Chắc chắn rồi! Aspose.Cells hoạt động với nhiều định dạng Excel như XLSX, XLS và CSV.
### Có bản dùng thử miễn phí không?
Vâng, bạn có thể lấy bản dùng thử miễn phí từ [liên kết tải xuống](https://releases.aspose.com/).
### Tôi có thể nhận được hỗ trợ kỹ thuật bằng cách nào?
Nếu bạn cần giúp đỡ, [Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) là một nguồn tài nguyên tuyệt vời.
### Aspose.Cells có tương thích với .NET Core không?
Có, Aspose.Cells cũng tương thích với các dự án .NET Core.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}