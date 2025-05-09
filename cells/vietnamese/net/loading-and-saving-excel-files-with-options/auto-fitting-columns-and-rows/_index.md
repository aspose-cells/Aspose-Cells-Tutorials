---
"description": "Tìm hiểu cách tự động điều chỉnh cột và hàng khi tải HTML vào Excel bằng Aspose.Cells cho .NET. Có kèm hướng dẫn từng bước."
"linktitle": "Tự động điều chỉnh cột và hàng khi tải HTML trong sổ làm việc"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tự động điều chỉnh cột và hàng khi tải HTML trong sổ làm việc"
"url": "/vi/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tự động điều chỉnh cột và hàng khi tải HTML trong sổ làm việc

## Giới thiệu
Bạn đã bao giờ tự hỏi làm thế nào để tự động điều chỉnh kích thước cột và hàng khi tải nội dung HTML vào sổ làm việc Excel bằng Aspose.Cells cho .NET chưa? Vâng, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng ta sẽ đi sâu vào cách bạn có thể tải bảng HTML vào sổ làm việc và đảm bảo rằng các cột và hàng được tự động điều chỉnh để khớp với nội dung. Nếu bạn đang làm việc với dữ liệu động thay đổi thường xuyên, hướng dẫn này sẽ là lựa chọn của bạn để tạo các bảng tính Excel được định dạng tốt từ HTML.
### Điều kiện tiên quyết
Trước khi bắt đầu viết mã, có một vài thứ bạn cần thiết lập trên hệ thống của mình. Đừng lo lắng, nó rất đơn giản và dễ hiểu!
1. Đã cài đặt Visual Studio: Bạn sẽ cần Visual Studio hoặc bất kỳ môi trường phát triển .NET nào khác.
2. Aspose.Cells cho .NET: Bạn có thể [tải xuống phiên bản mới nhất](https://releases.aspose.com/cells/net/) hoặc sử dụng trình quản lý gói NuGet để cài đặt nó.
3. .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework 4.0 trở lên.
4. Hiểu biết cơ bản về C#: Có một số hiểu biết về C# sẽ giúp bạn hiểu hướng dẫn này dễ dàng hơn.
5. Dữ liệu bảng HTML: Chuẩn bị một số nội dung HTML (thậm chí là bảng cơ bản) mà bạn muốn tải vào Excel.
## Nhập gói
Trước tiên, hãy nhập các không gian tên cần thiết để bắt đầu. Sau đây là danh sách đơn giản những gì bạn cần nhập:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Các gói này cho phép bạn xử lý sổ làm việc, thao tác dữ liệu HTML và tải dữ liệu đó vào Excel một cách liền mạch.
Hãy chia nhỏ quy trình này thành các phần dễ quản lý để bạn có thể dễ dàng theo dõi. Đến cuối bài này, bạn sẽ có một ví dụ thực tế về cách tự động điều chỉnh cột và hàng khi tải HTML vào sổ làm việc bằng Aspose.Cells cho .NET.
## Bước 1: Thiết lập thư mục tài liệu
Để lưu và lấy lại tệp dễ dàng, chúng tôi sẽ chỉ định đường dẫn nơi tài liệu của bạn sẽ được lưu trữ. Bạn có thể thay thế đường dẫn thư mục bằng vị trí thư mục của riêng bạn.
```csharp
string dataDir = "Your Document Directory";
```
Dòng này thiết lập thư mục nơi các tệp Excel của bạn sẽ được lưu. Điều quan trọng là phải sắp xếp các tệp của bạn đúng cách khi làm việc trên nhiều dự án. Hãy tưởng tượng đây là tủ hồ sơ của dự án bạn!
## Bước 2: Tạo dữ liệu HTML dưới dạng chuỗi
Tiếp theo, chúng ta sẽ định nghĩa một số nội dung HTML cơ bản. Vì mục đích của ví dụ này, chúng ta sẽ sử dụng một bảng HTML đơn giản. Bạn có thể tùy chỉnh nó theo nhu cầu của dự án.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Chúng tôi đang định nghĩa một chuỗi HTML rất cơ bản ở đây. Nó chứa một bảng với một vài hàng và cột. Bạn có thể thêm nhiều hàng hoặc cột hơn tùy theo yêu cầu của mình. Hãy nghĩ về việc chuẩn bị nguyên liệu trước khi nấu một bữa ăn!
## Bước 3: Tải chuỗi HTML vào MemoryStream
Bây giờ chúng ta đã có nội dung HTML sẵn sàng, bước tiếp theo là tải nó vào bộ nhớ bằng cách sử dụng `MemoryStream`Điều này cho phép chúng ta thao tác nội dung HTML trong bộ nhớ mà không cần lưu vào đĩa trước.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
Bằng cách chuyển đổi chuỗi HTML thành một mảng byte và đưa nó vào một `MemoryStream`, chúng ta có thể làm việc với dữ liệu HTML trong bộ nhớ. Hãy tưởng tượng bước này giống như việc chuẩn bị món ăn trong nồi trước khi cho vào lò nướng!
## Bước 4: Tải MemoryStream vào một Workbook (Không có Auto-Fitting)
Khi chúng ta có nội dung HTML trong bộ nhớ, chúng ta tải nó vào Aspose `Workbook`. Tại thời điểm này, chúng tôi vẫn chưa tự động điều chỉnh các cột và hàng. Đây là kịch bản "trước" của chúng tôi, để so sánh với phiên bản tự động điều chỉnh sau.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Sổ làm việc được tải nội dung HTML, nhưng các cột và hàng vẫn chưa được tự động điều chỉnh cho phù hợp với văn bản. Hãy nghĩ đến việc nướng bánh nhưng quên kiểm tra nhiệt độ—nó hoạt động, nhưng có thể không hoàn hảo!
## Bước 5: Chỉ định Tùy chọn Tải HTML với Tự động Điều chỉnh được Bật
Bây giờ, đây là phép thuật! Chúng ta tạo ra một trường hợp `HtmlLoadOptions` và kích hoạt `AutoFitColsAndRows` thuộc tính. Điều này đảm bảo rằng khi nội dung HTML được tải, các cột và hàng sẽ điều chỉnh để phù hợp với nội dung bên trong chúng.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Bằng cách thiết lập tùy chọn này, chúng ta đang yêu cầu Aspose.Cells tự động thay đổi kích thước các hàng và cột. Hãy tưởng tượng điều này giống như việc thiết lập lò nướng ở nhiệt độ hoàn hảo để bánh nở vừa phải!
## Bước 6: Tải HTML vào Workbook với tính năng Tự động điều chỉnh được bật
Bây giờ chúng ta tải lại nội dung HTML, nhưng lần này với `AutoFitColsAndRows` tùy chọn được bật. Điều này sẽ điều chỉnh độ rộng cột và chiều cao hàng dựa trên nội dung bên trong chúng.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Bước này tải nội dung HTML vào một sổ làm việc mới và lưu dưới dạng tệp Excel, nhưng bây giờ các cột và hàng được tự động điều chỉnh! Hãy nghĩ về điều này như một chiếc bánh nướng hoàn hảo, trong đó mọi thứ đều có kích thước vừa phải.
## Phần kết luận
Bằng cách làm theo các bước đơn giản này, bạn đã học được cách tải nội dung HTML vào sổ làm việc bằng Aspose.Cells cho .NET và tự động điều chỉnh các cột và hàng. Điều này đảm bảo các trang tính Excel của bạn luôn trông gọn gàng, bất kể nội dung động như thế nào. Đây là một tính năng đơn giản nhưng mạnh mẽ có thể giúp bạn tiết kiệm rất nhiều thời gian trong việc định dạng và sắp xếp dữ liệu Excel của mình.
Bây giờ bạn đã được trang bị kiến thức này, bạn có thể thử nghiệm với nội dung HTML phức tạp hơn, thêm kiểu dáng và thậm chí tạo toàn bộ bảng tính Excel từ các trang web!
## Câu hỏi thường gặp
### Tôi có thể sử dụng phương pháp này để tải các bảng HTML lớn không?
Có, Aspose.Cells xử lý các bảng HTML lớn một cách hiệu quả, nhưng để có hiệu suất tối ưu, bạn nên thử nghiệm với kích thước dữ liệu của mình.
### Tôi có thể áp dụng chiều rộng cột và chiều cao hàng cụ thể theo cách thủ công sau khi tự động điều chỉnh không?
Chắc chắn rồi! Bạn vẫn có thể tùy chỉnh từng cột và hàng ngay cả sau khi sử dụng tính năng tự động điều chỉnh.
### Tôi có thể định dạng bảng như thế nào sau khi tải HTML?
Bạn có thể áp dụng kiểu bằng các tùy chọn kiểu mở rộng của Aspose.Cells sau khi tải HTML.
### Aspose.Cells cho .NET có tương thích với các phiên bản cũ hơn của .NET Framework không?
Có, Aspose.Cells cho .NET hỗ trợ .NET Framework 4.0 trở lên.
### Tôi có thể tải các loại nội dung khác ngoài HTML vào Excel bằng Aspose.Cells không?
Có, Aspose.Cells hỗ trợ tải nhiều định dạng khác nhau như CSV, JSON và XML vào Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}