---
"description": "Tự động định dạng số trong Excel bằng Aspose.Cells cho .NET. Tìm hiểu cách áp dụng định dạng ngày, phần trăm và tiền tệ theo chương trình."
"linktitle": "Sử dụng Định dạng Số tích hợp trong Excel theo Chương trình"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Sử dụng Định dạng Số tích hợp trong Excel theo Chương trình"
"url": "/vi/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sử dụng Định dạng Số tích hợp trong Excel theo Chương trình

## Giới thiệu
Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn cách sử dụng các định dạng số tích hợp trong Excel bằng Aspose.Cells cho .NET. Chúng tôi sẽ đề cập đến mọi thứ từ thiết lập môi trường của bạn đến áp dụng các định dạng khác nhau như ngày tháng, phần trăm và tiền tệ. Cho dù bạn là người chuyên nghiệp hay chỉ mới bắt đầu sử dụng hệ sinh thái .NET, hướng dẫn này sẽ giúp bạn định dạng các ô Excel một cách dễ dàng.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những thứ sau:
- Aspose.Cells cho thư viện .NET đã được cài đặt. Bạn có thể [tải xuống ở đây](https://releases.aspose.com/cells/net/).
- Kiến thức cơ bản về C# và lập trình .NET.
- Visual Studio hoặc bất kỳ .NET IDE nào được cài đặt trên máy của bạn.
- Giấy phép Aspose hợp lệ hoặc [giấy phép tạm thời](https://purchase.aspose.com/temporary-license/).
- Đã cài đặt .NET framework (phiên bản 4.0 trở lên).
  
Nếu bạn thiếu bất kỳ mục nào ở trên, hãy làm theo các liên kết được cung cấp để thiết lập mọi thứ. Sẵn sàng chưa? Hãy cùng bắt đầu phần thú vị nhé!
## Nhập gói
Trước khi bắt đầu hướng dẫn, hãy đảm bảo nhập các không gian tên cần thiết để làm việc với Aspose.Cells cho .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Sau khi nhập những thứ này, bạn đã sẵn sàng để thao tác các tệp Excel theo chương trình. Bây giờ, hãy cùng tìm hiểu hướng dẫn từng bước nhé!
## Bước 1: Tạo hoặc truy cập sổ làm việc Excel của bạn
Trong bước này, bạn sẽ tạo một sổ làm việc mới. Hãy nghĩ đến việc mở một tệp Excel mới, ngoại trừ việc bạn thực hiện thông qua mã!
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Tạo thư mục nếu thư mục đó chưa có.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```
Ở đây, chúng tôi chỉ đơn giản là tạo ra một cái mới `Workbook` đối tượng. Điều này hoạt động như tệp Excel của bạn, sẵn sàng để thao tác dữ liệu. Bạn cũng có thể tải tệp hiện có bằng cách cung cấp đường dẫn của tệp đó.
## Bước 2: Truy cập vào Bảng tính
Sổ làm việc Excel có thể chứa nhiều trang tính. Trong bước này, chúng ta sẽ truy cập trang tính đầu tiên trong sổ làm việc của bạn:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Bây giờ chúng ta đang truy cập trang tính đầu tiên trong sổ làm việc. Nếu bạn cần thao tác thêm các trang tính khác, bạn có thể tham chiếu chúng bằng chỉ mục hoặc tên của chúng.
## Bước 3: Thêm dữ liệu vào ô
Chúng ta hãy bắt đầu thêm một số dữ liệu vào các ô cụ thể. Đầu tiên, chúng ta sẽ chèn ngày hệ thống hiện tại vào ô "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Dòng này chèn ngày hiện tại vào ô A1. Thật tuyệt phải không? Hãy tưởng tượng làm điều này theo cách thủ công cho hàng trăm ô—sẽ là một cơn ác mộng. Bây giờ, chúng ta sẽ chuyển sang định dạng!
## Bước 4: Định dạng Ngày trong Ô "A1"
Tiếp theo, hãy định dạng ngày đó theo định dạng dễ đọc hơn, như "15-Oct-24". Đây là nơi Aspose.Cells thực sự tỏa sáng:
1. Lấy lại phong cách của Cell:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Ở đây, chúng ta sẽ lấy phong cách của ô A1. Hãy nghĩ về điều này như việc lấy "phong cách" của ô trước khi thực hiện bất kỳ thay đổi nào.
2. Thiết lập Định dạng Ngày:
```csharp
style.Number = 15;
```
Thiết lập `Number` thuộc tính 15 áp dụng định dạng ngày mong muốn. Đây là mã định dạng số tích hợp để hiển thị ngày theo định dạng "d-mmm-yy".
3. Áp dụng Kiểu cho Ô:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Dòng này áp dụng các thay đổi về kiểu cho ô. Bây giờ, thay vì định dạng ngày mặc định, bạn sẽ thấy thứ gì đó thân thiện với người dùng hơn nhiều như "15-Oct-24".
## Bước 5: Thêm và định dạng phần trăm trong ô "A2"
Hãy chuyển sang định dạng phần trăm. Hãy tưởng tượng bạn muốn chèn một giá trị và hiển thị nó dưới dạng phần trăm. Trong bước này, chúng ta sẽ thêm một giá trị số vào ô "A2" và định dạng nó dưới dạng phần trăm:
1. Chèn giá trị số:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Thao tác này sẽ chèn số 20 vào ô A2. Bạn có thể nghĩ rằng, "Đó chỉ là một con số thông thường—làm sao tôi có thể chuyển nó thành phần trăm?" Vâng, chúng ta sắp đến phần đó rồi.
2. Lấy lại Kiểu và Đặt Định dạng Phần trăm:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Định dạng theo phần trăm
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Ở đây, chúng ta thêm 2546 vào ô A3. Tiếp theo, chúng ta sẽ định dạng số này để hiển thị dưới dạng tiền tệ.
2. Lấy Kiểu và Thiết lập Định dạng Tiền tệ:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Định dạng như tiền tệ
worksheet.Cells["A3"].SetStyle(style);
```
Thiết lập `Number` thuộc tính 6 áp dụng định dạng tiền tệ. Bây giờ giá trị trong ô A3 sẽ hiển thị là "2,546.00", hoàn chỉnh với dấu phẩy và hai chữ số thập phân.
## Bước 7: Lưu tệp Excel
Bây giờ chúng ta đã áp dụng mọi phép định dạng, đã đến lúc lưu tệp:
```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Dòng này lưu tệp Excel ở định dạng Excel 97-2003. Bạn có thể thay đổi `SaveFormat` để phù hợp với nhu cầu của bạn. Và như vậy, bạn đã tạo và định dạng một tệp Excel theo chương trình!
## Phần kết luận
Xin chúc mừng! Bạn đã học thành công cách sử dụng Aspose.Cells cho .NET để áp dụng các định dạng số tích hợp vào các ô trong tệp Excel. Từ ngày tháng đến phần trăm và tiền tệ, chúng tôi đã đề cập đến một số nhu cầu định dạng phổ biến nhất để xử lý dữ liệu Excel. Bây giờ, thay vì định dạng thủ công các ô, bạn có thể tự động hóa toàn bộ quy trình—tiết kiệm thời gian và giảm lỗi.
## Câu hỏi thường gặp
### Tôi có thể áp dụng định dạng số tùy chỉnh bằng Aspose.Cells cho .NET không?
Có! Ngoài các định dạng tích hợp, Aspose.Cells cũng hỗ trợ các định dạng số tùy chỉnh. Bạn có thể tạo các định dạng rất cụ thể bằng cách sử dụng `Custom` tài sản trong `Style` lớp học.
### Làm thế nào để định dạng một ô thành loại tiền tệ bằng một ký hiệu cụ thể?
Để áp dụng một ký hiệu tiền tệ cụ thể, bạn có thể sử dụng định dạng tùy chỉnh bằng cách thiết lập `Style.Custom` tài sản.
### Tôi có thể định dạng toàn bộ hàng hoặc cột không?
Chắc chắn rồi! Bạn có thể áp dụng kiểu cho toàn bộ hàng hoặc cột bằng cách sử dụng `Rows` hoặc `Columns` bộ sưu tập trong `Worksheet` sự vật.
### Làm thế nào để định dạng nhiều ô cùng một lúc?
Bạn có thể sử dụng `Range` đối tượng để chọn nhiều ô và áp dụng kiểu cho tất cả cùng một lúc.
### Tôi có cần cài đặt Microsoft Excel để sử dụng Aspose.Cells không?
Không, Aspose.Cells hoạt động độc lập với Microsoft Excel, do đó bạn không cần cài đặt Excel trên máy.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}