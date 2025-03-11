---
title: Gửi hình dạng mặt trước hoặc mặt sau trong Excel
linktitle: Gửi hình dạng mặt trước hoặc mặt sau trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Khám phá cách gửi hình dạng ra phía trước hoặc phía sau trong Excel bằng Aspose.Cells cho .NET. Hướng dẫn này cung cấp hướng dẫn từng bước với các mẹo.
weight: 16
url: /vi/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gửi hình dạng mặt trước hoặc mặt sau trong Excel

## Giới thiệu
Khi làm việc với các tệp Excel, bạn có thể thấy mình cần kiểm soát nhiều hơn đối với các thành phần trực quan trong bảng tính của mình. Các hình dạng, như hình ảnh và đồ họa, có thể cải thiện cách trình bày dữ liệu của bạn. Nhưng điều gì xảy ra khi các hình dạng này chồng lên nhau hoặc cần được sắp xếp lại? Đây là nơi Aspose.Cells for .NET tỏa sáng. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn các bước để thao tác các hình dạng trong bảng tính Excel, cụ thể là gửi các hình dạng ra phía trước hoặc phía sau các hình dạng khác. Nếu bạn đã sẵn sàng để nâng cao trò chơi Excel của mình, hãy cùng bắt đầu ngay!
## Điều kiện tiên quyết
Trước khi bắt đầu, bạn cần chuẩn bị một số thứ sau:
1.  Cài đặt thư viện Aspose.Cells: Đảm bảo bạn đã cài đặt thư viện Aspose.Cells cho .NET. Bạn có thể tìm thấy nó[đây](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển: Đảm bảo bạn có môi trường phát triển được thiết lập hỗ trợ .NET, chẳng hạn như Visual Studio.
3. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn hiểu các đoạn mã tốt hơn.
Được rồi, bạn đã tích vào tất cả các ô trong danh sách điều kiện tiên quyết chưa? Tuyệt! Chúng ta hãy chuyển sang phần thú vị – viết một số mã!
## Nhập gói
Trước khi đi sâu vào mã hóa thực tế, hãy nhập các gói cần thiết. Chỉ cần thêm lệnh using sau vào đầu tệp C# của bạn:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Các không gian tên này rất quan trọng vì chúng chứa các lớp và phương thức mà chúng ta sẽ sử dụng để thao tác với các tệp và hình dạng Excel.
## Bước 1: Xác định đường dẫn tệp của bạn
Trong bước đầu tiên này, chúng ta cần thiết lập thư mục nguồn và thư mục đầu ra. Đây là nơi tệp Excel của bạn nằm và nơi bạn muốn lưu tệp đã sửa đổi.
```csharp
//Thư mục nguồn
string sourceDir = "Your Document Directory";
//Thư mục đầu ra
string outputDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế nơi lưu trữ các tệp Excel của bạn.
## Bước 2: Tải Workbook
Bây giờ chúng ta đã thiết lập xong các thư mục, hãy tải bảng tính (tệp Excel) có chứa các hình dạng mà chúng ta muốn thao tác.
```csharp
//Tải tệp Excel nguồn
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Dòng mã này khởi tạo một cái mới`Workbook` đối tượng, tải tệp Excel đã chỉ định vào bộ nhớ để chúng ta có thể làm việc với nó.
## Bước 3: Truy cập vào Bảng tính 
Tiếp theo, chúng ta cần truy cập vào worksheet cụ thể nơi chứa các hình dạng của chúng ta. Đối với ví dụ này, chúng ta sẽ sử dụng worksheet đầu tiên.
```csharp
//Truy cập bảng tính đầu tiên
Worksheet ws = wb.Worksheets[0];
```
 Bằng cách tham khảo`Worksheets[0]`, chúng tôi đang nhắm mục tiêu vào trang tính đầu tiên của sổ làm việc. Nếu hình dạng của bạn nằm trên một trang tính khác, hãy điều chỉnh chỉ mục cho phù hợp.
## Bước 4: Truy cập vào Hình dạng
Sau khi đã có bảng tính, hãy chọn các hình dạng mà chúng ta quan tâm. Trong ví dụ này, chúng ta sẽ chọn hình dạng thứ nhất và thứ tư.
```csharp
//Truy cập hình dạng đầu tiên và thứ tư
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Các đường này lấy hình dạng cụ thể từ bảng tính dựa trên chỉ mục của chúng.
## Bước 5: In Vị trí theo thứ tự Z của các hình dạng
Trước khi di chuyển bất kỳ hình dạng nào, hãy in ra vị trí Z-Order hiện tại của chúng. Điều này giúp chúng ta theo dõi vị trí của chúng trước khi thực hiện thay đổi.
```csharp
//In vị trí Z-Order của hình dạng
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Bằng cách gọi`ZOrderPosition`, chúng ta có thể thấy vị trí của từng hình dạng trong thứ tự bản vẽ.
## Bước 6: Gửi hình dạng đầu tiên lên phía trước
Bây giờ là lúc hành động! Hãy gửi hình dạng đầu tiên đến phía trước của Z-Order.
```csharp
//Gửi hình dạng này lên phía trước
sh1.ToFrontOrBack(2);
```
 Bằng cách đi qua`2` ĐẾN`ToFrontOrBack`, chúng tôi đang hướng dẫn Aspose.Cells đưa hình dạng này lên phía trước. 
## Bước 7: In Vị trí theo thứ tự Z của Hình thứ hai
Trước khi gửi hình dạng thứ hai ra phía sau, hãy kiểm tra vị trí của nó.
```csharp
//In vị trí Z-Order của hình dạng
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Điều này giúp chúng ta hiểu rõ hơn về vị trí của hình dạng thứ tư trước khi thực hiện bất kỳ thay đổi nào.
## Bước 8: Gửi hình dạng thứ tư ra phía sau
Cuối cùng, chúng ta sẽ gửi hình dạng thứ tư vào phía sau của ngăn xếp Z-Order.
```csharp
//Gửi hình dạng này trở lại
sh4.ToFrontOrBack(-2);
```
 Sử dụng`-2` vì tham số này sẽ gửi hình dạng về phía sau của ngăn xếp, đảm bảo nó không che khuất các hình dạng hoặc văn bản khác.
## Bước 9: Lưu sổ làm việc 
Bước cuối cùng là lưu bảng tính với các hình dạng vừa được định vị.
```csharp
//Lưu tệp Excel đầu ra
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Lệnh này lưu bảng tính đã sửa đổi vào thư mục đầu ra đã chỉ định.
## Bước 10: Tin nhắn xác nhận
Cuối cùng, hãy cung cấp một xác nhận đơn giản để cho chúng tôi biết rằng nhiệm vụ của chúng ta đã hoàn thành thành công.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Và như vậy là xong phần code cho hướng dẫn của chúng ta!
## Phần kết luận
Thao tác hình dạng trong Excel bằng Aspose.Cells for .NET không chỉ đơn giản mà còn mạnh mẽ. Bằng cách làm theo hướng dẫn này, giờ đây bạn có thể dễ dàng gửi hình dạng ra phía trước hoặc phía sau, cho phép kiểm soát tốt hơn các bài thuyết trình Excel của mình. Với các công cụ này, bạn đã sẵn sàng để tăng cường sức hấp dẫn trực quan cho bảng tính của mình.
## Câu hỏi thường gặp
### Tôi cần ngôn ngữ lập trình nào cho Aspose.Cells?  
Bạn cần sử dụng C# hoặc bất kỳ ngôn ngữ nào hỗ trợ .NET để làm việc với Aspose.Cells.
### Tôi có thể dùng thử Aspose.Cells miễn phí không?  
 Có, bạn có thể bắt đầu bằng bản dùng thử miễn phí Aspose.Cells[đây](https://releases.aspose.com/).
### Tôi có thể thao tác với những hình dạng nào trong Excel?  
Bạn có thể thao tác với nhiều hình dạng khác nhau như hình chữ nhật, hình tròn, đường thẳng và hình ảnh.
### Tôi có thể nhận được hỗ trợ cho Aspose.Cells như thế nào?  
 Bạn có thể truy cập diễn đàn cộng đồng của họ để được hỗ trợ hoặc giải đáp thắc mắc[đây](https://forum.aspose.com/c/cells/9).
### Có giấy phép tạm thời nào cho Aspose.Cells không?  
 Có, bạn có thể yêu cầu giấy phép tạm thời[đây](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
