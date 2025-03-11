---
title: Dừng chuyển đổi hoặc tải bằng cách sử dụng Interrupt Monitor
linktitle: Dừng chuyển đổi hoặc tải bằng cách sử dụng Interrupt Monitor
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách dừng chuyển đổi sổ làm việc trong Aspose.Cells cho .NET bằng Interrupt Monitor, với hướng dẫn chi tiết từng bước.
weight: 26
url: /vi/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dừng chuyển đổi hoặc tải bằng cách sử dụng Interrupt Monitor

## Giới thiệu
Làm việc với các tệp Excel lớn thường liên quan đến các quy trình dài có thể ngốn thời gian và tài nguyên. Nhưng nếu bạn có thể dừng quá trình chuyển đổi giữa chừng khi nhận ra có điều gì đó cần thay đổi thì sao? Aspose.Cells cho .NET có một tính năng gọi là Interrupt Monitor, cho phép bạn ngắt quá trình chuyển đổi sổ làm việc sang định dạng khác như PDF. Tính năng này có thể cứu cánh, đặc biệt là khi làm việc với các tệp dữ liệu lớn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách ngắt quá trình chuyển đổi bằng Interrupt Monitor trong Aspose.Cells cho .NET.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị những điều sau:
1.  Aspose.Cells cho .NET - Tải xuống[đây](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển .NET - Chẳng hạn như Visual Studio.
3. Kiến thức cơ bản về lập trình C# - Sự quen thuộc với cú pháp C# sẽ giúp bạn theo dõi.
## Nhập gói
Để bắt đầu, hãy nhập các gói cần thiết. Các gói nhập này bao gồm:
- Aspose.Cells: Thư viện chính để xử lý các tệp Excel.
- System.Threading: Để quản lý luồng, vì ví dụ này sẽ chạy hai tiến trình song song.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Hãy chia nhỏ quy trình thành các bước chi tiết. Mỗi bước sẽ giúp bạn hiểu được tầm quan trọng của việc thiết lập và sử dụng Interrupt Monitor để quản lý việc chuyển đổi sổ làm việc Excel.
## Bước 1: Tạo lớp và thiết lập thư mục đầu ra
Đầu tiên, chúng ta cần một lớp để đóng gói các hàm của mình, cùng với một thư mục nơi tệp đầu ra sẽ được lưu.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế mà bạn muốn lưu tệp PDF.
## Bước 2: Khởi tạo Trình giám sát ngắt
Tiếp theo, tạo một đối tượng InterruptMonitor. Màn hình này sẽ giúp kiểm soát quy trình bằng cách thiết lập khả năng ngắt quy trình tại bất kỳ thời điểm nào.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Trình giám sát ngắt này sẽ được đính kèm vào sổ làm việc của chúng ta, cho phép chúng ta quản lý quá trình chuyển đổi.
## Bước 3: Thiết lập sổ làm việc để chuyển đổi
Bây giờ, chúng ta hãy tạo một đối tượng sổ làm việc, gán InterruptMonitor cho đối tượng đó, sau đó truy cập vào bảng tính đầu tiên để chèn một số văn bản mẫu.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Đoạn mã trên tạo một bảng tính, thiết lập InterruptMonitor cho nó và đặt văn bản vào một ô xa (`J1000000`). Đặt văn bản tại vị trí ô này đảm bảo rằng việc xử lý sổ làm việc sẽ tốn nhiều thời gian hơn, giúp InterruptMonitor có đủ thời gian để can thiệp.
## Bước 4: Lưu Workbook dưới dạng PDF và Xử lý gián đoạn
 Bây giờ, chúng ta hãy thử lưu sổ làm việc dưới dạng PDF. Chúng ta sẽ sử dụng`try-catch` khối để xử lý bất kỳ sự gián đoạn nào có thể xảy ra.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Nếu quá trình bị gián đoạn, ngoại lệ sẽ bắt được và hiển thị thông báo phù hợp. Nếu không, sổ làm việc sẽ lưu dưới dạng PDF.
## Bước 5: Ngắt quá trình chuyển đổi
 Tính năng chính ở đây là khả năng ngắt quá trình. Chúng tôi sẽ thêm sự chậm trễ bằng cách sử dụng`Thread.Sleep` và sau đó gọi`Interrupt()` phương pháp dừng chuyển đổi sau 10 giây.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Sự chậm trễ này giúp sổ làm việc có thời gian bắt đầu chuyển đổi sang PDF trước khi tín hiệu ngắt được gửi đi.
## Bước 6: Thực hiện các luồng đồng thời
Để đưa mọi thứ lại với nhau, chúng ta cần bắt đầu cả hai hàm trong các luồng riêng biệt. Theo cách này, việc chuyển đổi sổ làm việc và chờ ngắt có thể xảy ra đồng thời.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 Mã ở trên chạy`CreateWorkbookAndConvertItToPdfFormat` Và`WaitForWhileAndThenInterrupt` trong các luồng song song, nối chúng lại sau khi cả hai tiến trình đã hoàn tất.
## Bước 7: Thực hiện cuối cùng
 Cuối cùng, chúng ta sẽ thêm một`Run()` phương pháp thực thi mã.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Cái này`Run` phương pháp là điểm vào để bắt đầu và quan sát sự gián đoạn trong hành động.
## Phần kết luận
Trong hướng dẫn này, chúng tôi đã khám phá cách ngắt quá trình chuyển đổi trong Aspose.Cells cho .NET. Interrupt Monitor là một công cụ hữu ích khi làm việc với các tệp Excel lớn, cho phép bạn dừng các quy trình mà không cần chờ chúng hoàn tất. Điều này đặc biệt hữu ích trong các tình huống mà thời gian và tài nguyên là quý giá và cần phản hồi nhanh.
## Câu hỏi thường gặp
### Interrupt Monitor trong Aspose.Cells dành cho .NET là gì?  
Interrupt Monitor cho phép bạn dừng quá trình chuyển đổi bảng tính hoặc tải giữa chừng.
### Tôi có thể sử dụng Interrupt Monitor cho các định dạng khác ngoài PDF không?  
Có, bạn cũng có thể ngắt quá trình chuyển đổi sang các định dạng được hỗ trợ khác.
### Thread.Sleep() ảnh hưởng đến thời gian ngắt như thế nào?  
Thread.Sleep() tạo ra độ trễ trước khi kích hoạt ngắt, cho thời gian để quá trình chuyển đổi bắt đầu.
### Tôi có thể ngắt quá trình trước 10 giây không?  
 Có, sửa đổi sự chậm trễ trong`WaitForWhileAndThenInterrupt()` đến một thời gian ngắn hơn.
### Quá trình ngắt có ảnh hưởng đến hiệu suất không?  
Tác động là rất nhỏ và rất có lợi cho việc quản lý các quy trình chạy lâu dài.
 Để biết thêm thông tin, hãy tham khảo[Tài liệu Aspose.Cells cho .NET](https://reference.aspose.com/cells/net/) . Nếu bạn cần trợ giúp, hãy kiểm tra[Diễn đàn hỗ trợ](https://forum.aspose.com/c/cells/9)hoặc nhận được một[Dùng thử miễn phí](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
