---
title: Phát hiện tham chiếu vòng tròn trong Excel theo chương trình
linktitle: Phát hiện tham chiếu vòng tròn trong Excel theo chương trình
second_title: API xử lý Excel Aspose.Cells .NET
description: Dễ dàng phát hiện tham chiếu vòng tròn trong Excel bằng Aspose.Cells cho .NET. Làm theo hướng dẫn từng bước của chúng tôi để đảm bảo tính toán chính xác trong bảng tính của bạn.
weight: 13
url: /vi/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Phát hiện tham chiếu vòng tròn trong Excel theo chương trình

## Giới thiệu
Khi làm việc với các tệp Excel, một trong những vấn đề khó chịu nhất mà bạn có thể gặp phải là tham chiếu vòng tròn. Điều này xảy ra khi một công thức tham chiếu trở lại ô của chính nó, trực tiếp hoặc gián tiếp, tạo ra một vòng lặp có thể gây nhầm lẫn cho công cụ tính toán của Excel. Nhưng đừng lo! Với Aspose.Cells dành cho .NET, bạn có thể phát hiện các tham chiếu vòng tròn khó chịu này theo chương trình, đảm bảo bảng tính của bạn vẫn hoạt động và chính xác. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước trong quy trình, giúp mọi thứ trở nên đơn giản như ăn bánh.
## Điều kiện tiên quyết
Trước khi đi sâu vào cách phát hiện tham chiếu vòng, hãy đảm bảo rằng bạn có mọi thứ cần thiết để bắt đầu:
1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio trên máy của mình. Đây sẽ là môi trường phát triển của bạn.
2. .NET Framework: Đảm bảo rằng bạn đang sử dụng phiên bản .NET Framework tương thích (ít nhất là .NET Framework 4.0).
3.  Thư viện Aspose.Cells: Bạn cần có thư viện Aspose.Cells. Bạn có thể tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
4. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ có lợi vì chúng ta sẽ viết mã bằng ngôn ngữ này.
5. Tệp Excel: Chuẩn bị tệp Excel có chứa tham chiếu vòng tròn để thử nghiệm. Bạn có thể tạo một tệp đơn giản hoặc tải xuống mẫu.
Bây giờ chúng ta đã có đủ các điều kiện tiên quyết, hãy chuyển sang phần thú vị nhé!
## Nhập gói
Trước khi bạn có thể bắt đầu mã hóa, bạn cần nhập các gói cần thiết. Sau đây là cách thực hiện:
### Tạo một dự án mới
- Mở Visual Studio và tạo một dự án Ứng dụng bảng điều khiển C# mới.
### Thêm tham chiếu Aspose.Cells
- Nhấp chuột phải vào dự án của bạn trong Solution Explorer.
- Chọn "Quản lý gói NuGet".
- Tìm kiếm “Aspose.Cells” và cài đặt phiên bản mới nhất.
### Nhập không gian tên bắt buộc
 Ở đầu trang của bạn`Program.cs` tệp, nhập các không gian tên cần thiết:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Bây giờ chúng ta đã thiết lập mọi thứ, hãy cùng tìm hiểu mã để phát hiện tham chiếu vòng tròn trong tệp Excel.
## Bước 1: Xác định thư mục đầu vào
Đầu tiên, bạn cần chỉ định thư mục chứa tệp Excel của bạn. Đây là nơi bạn sẽ tải tệp Excel của mình.
```csharp
// Thư mục đầu vào
string sourceDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế đến tệp Excel của bạn.
## Bước 2: Tải Workbook bằng LoadOptions
Tiếp theo, bạn sẽ tải bảng tính Excel của mình. Đây chính là nơi phép thuật bắt đầu!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Ở đây, chúng ta đang tạo một phiên bản mới của`LoadOptions` và tải sổ làm việc từ đường dẫn đã chỉ định. Đảm bảo tên tệp Excel của bạn khớp!
## Bước 3: Bật Cài đặt Lặp lại
Để cho phép tham chiếu vòng tròn, bạn cần bật cài đặt lặp trong sổ làm việc.
```csharp
objWB.Settings.Iteration = true;
```
Điều này yêu cầu Aspose.Cells cho phép tham chiếu vòng trong quá trình tính toán.
## Bước 4: Tạo tùy chọn tính toán và màn hình tròn
Bây giờ, chúng ta hãy tạo các tùy chọn tính toán và màn hình tròn tùy chỉnh của mình.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Ở đây, chúng ta đang tạo một trường hợp của`CalculationOptions` và một phong tục`CircularMonitor`Màn hình này sẽ giúp theo dõi mọi tham chiếu vòng tròn được tìm thấy trong quá trình tính toán.
## Bước 5: Tính toán các công thức
Bây giờ là lúc tính toán các công thức trong bảng tính của bạn.
```csharp
objWB.CalculateFormula(copts);
```
Dòng này thực hiện phép tính và kiểm tra tham chiếu vòng tròn.
## Bước 6: Đếm tham chiếu vòng tròn
Sau khi tính toán, bạn có thể đếm được có bao nhiêu tham chiếu vòng được tìm thấy.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Thao tác này sẽ đưa ra số lượng tham chiếu vòng được phát hiện trong tệp Excel của bạn.
## Bước 7: Hiển thị kết quả
Cuối cùng, hãy hiển thị kết quả và xác nhận rằng phương pháp của chúng ta đã được thực hiện thành công.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Bước 8: Triển khai lớp CircularMonitor
 Để hoàn tất quá trình, bạn sẽ cần phải triển khai`CircularMonitor` lớp. Lớp này sẽ kế thừa từ`AbstractCalculationMonitor` và xử lý việc phát hiện các tham chiếu vòng tròn.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Lớp này ghi lại thông tin chi tiết của từng tham chiếu vòng được tìm thấy, bao gồm tên bảng tính và chỉ mục ô.
## Phần kết luận
Phát hiện tham chiếu vòng tròn trong Excel bằng Aspose.Cells cho .NET là một quy trình đơn giản khi bạn chia nhỏ thành các bước dễ quản lý. Bằng cách làm theo hướng dẫn này, bạn có thể dễ dàng xác định và xử lý tham chiếu vòng tròn trong bảng tính của mình, đảm bảo tính toán của bạn vẫn chính xác và đáng tin cậy. Cho dù bạn là nhà phát triển dày dạn kinh nghiệm hay mới bắt đầu, Aspose.Cells cung cấp các công cụ mạnh mẽ để nâng cao khả năng thao tác Excel của bạn. 
## Câu hỏi thường gặp
### Tham chiếu vòng tròn trong Excel là gì?
Tham chiếu vòng tròn xảy ra khi một công thức tham chiếu trở lại ô của chính nó, gây ra vòng lặp vô tận trong các phép tính.
### Làm thế nào tôi có thể phát hiện tham chiếu vòng tròn theo chương trình?
Bạn có thể sử dụng thư viện Aspose.Cells trong .NET để phát hiện tham chiếu vòng theo chương trình bằng cách triển khai trình giám sát tính toán tùy chỉnh.
### Điều kiện tiên quyết để sử dụng Aspose.Cells là gì?
Bạn cần cài đặt Visual Studio, .NET Framework và thư viện Aspose.Cells.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
Có, Aspose.Cells cung cấp bản dùng thử miễn phí mà bạn có thể sử dụng để khám phá các tính năng của nó.
### Tôi có thể tìm thêm thông tin về Aspose.Cells ở đâu?
 Bạn có thể ghé thăm[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để biết thông tin chi tiết và ví dụ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
