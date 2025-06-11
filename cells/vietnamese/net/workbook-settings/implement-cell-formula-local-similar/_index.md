---
"description": "Khám phá cách triển khai công thức ô tương tự như chức năng cục bộ của công thức phạm vi trong Aspose.Cells cho .NET. Tìm hiểu cách tùy chỉnh tên hàm Excel tích hợp và nhiều hơn nữa."
"linktitle": "Thực hiện công thức ô cục bộ tương tự như công thức phạm vi cục bộ"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Thực hiện công thức ô cục bộ tương tự như công thức phạm vi cục bộ"
"url": "/vi/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện công thức ô cục bộ tương tự như công thức phạm vi cục bộ

## Giới thiệu
Aspose.Cells for .NET là API thao tác bảng tính mạnh mẽ và linh hoạt cho phép bạn tạo, thao tác và chuyển đổi các tệp Excel theo chương trình. Một trong nhiều tính năng được Aspose.Cells cung cấp là khả năng tùy chỉnh hành vi của các hàm Excel tích hợp, bao gồm khả năng tạo tên hàm cục bộ của riêng bạn. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn các bước để triển khai công thức ô tương tự như chức năng cục bộ của công thức phạm vi trong Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn có những điều sau:
1. Hệ thống của bạn phải được cài đặt Microsoft Visual Studio 2010 trở lên.
2. Phiên bản mới nhất của thư viện Aspose.Cells for .NET được cài đặt trong dự án của bạn. Bạn có thể tải xuống thư viện từ [Trang tải xuống Aspose.Cells cho .NET](https://releases.aspose.com/cells/net/).
## Nhập gói
Để bắt đầu, bạn sẽ cần nhập các gói cần thiết vào dự án C# của mình. Thêm các câu lệnh using sau vào đầu tệp mã của bạn:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Bước 1: Tạo lớp cài đặt toàn cầu hóa tùy chỉnh
Bước đầu tiên là tạo một tùy chỉnh `GlobalizationSettings` lớp cho phép bạn ghi đè hành vi mặc định của các hàm Excel. Trong ví dụ này, chúng ta sẽ thay đổi tên của `SUM` Và `AVERAGE` chức năng để `UserFormulaLocal_SUM` Và `UserFormulaLocal_AVERAGE`, tương ứng.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Thay đổi tên hàm SUM theo nhu cầu của bạn.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Thay đổi tên hàm AVERAGE theo nhu cầu của bạn.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Bước 2: Tạo một sổ làm việc mới và chỉ định cài đặt toàn cầu hóa tùy chỉnh
Tiếp theo, tạo một phiên bản Workbook mới và gán tùy chỉnh `GlobalizationSettings` lớp thực hiện cho Workbook `Settings.GlobalizationSettings` tài sản.
```csharp
//Tạo sổ làm việc
Workbook wb = new Workbook();
//Chỉ định lớp triển khai GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Bước 3: Truy cập trang tính đầu tiên và một ô
Bây giờ, chúng ta hãy truy cập vào trang tính đầu tiên trong sổ làm việc và một ô cụ thể trong trang tính đó.
```csharp
//Truy cập bảng tính đầu tiên
Worksheet ws = wb.Worksheets[0];
//Truy cập một số ô
Cell cell = ws.Cells["C4"];
```
## Bước 4: Gán công thức và in FormulaLocal
Cuối cùng, chúng ta hãy gán `SUM` Và `AVERAGE` công thức vào ô và in kết quả `FormulaLocal` giá trị.
```csharp
//Gán công thức SUM và in FormulaLocal của nó
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Gán công thức AVERAGE và in FormulaLocal của nó
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Phần kết luận
Trong hướng dẫn này, bạn đã học cách triển khai công thức ô tương tự như chức năng cục bộ của công thức phạm vi trong Aspose.Cells cho .NET. Bằng cách tạo một tùy chỉnh `GlobalizationSettings` class, bạn có thể ghi đè hành vi mặc định của các hàm Excel và tùy chỉnh tên hàm cục bộ để phù hợp với nhu cầu của bạn. Điều này có thể đặc biệt hữu ích khi làm việc với các tài liệu Excel được bản địa hóa hoặc quốc tế hóa.
## Câu hỏi thường gặp
### Mục đích của việc này là gì? `GlobalizationSettings` lớp trong Aspose.Cells?
Các `GlobalizationSettings` lớp trong Aspose.Cells cho phép bạn tùy chỉnh hành vi của các hàm Excel tích hợp, bao gồm khả năng thay đổi tên hàm cục bộ.
### Tôi có thể ghi đè hành vi của các chức năng khác ngoài `SUM` Và `AVERAGE`?
Có, bạn có thể ghi đè hành vi của bất kỳ hàm Excel tích hợp nào bằng cách sửa đổi `GetLocalFunctionName` phương pháp trong tùy chỉnh của bạn `GlobalizationSettings` lớp học.
### Có cách nào để thiết lập lại tên hàm về giá trị mặc định không?
Có, bạn có thể đặt lại tên hàm bằng cách xóa tùy chỉnh `GlobalizationSettings` lớp hoặc bằng cách trả về một chuỗi rỗng từ `GetLocalFunctionName` phương pháp.
### Tôi có thể sử dụng tính năng này để tạo các hàm tùy chỉnh trong Aspose.Cells không?
Không, `GlobalizationSettings` lớp được thiết kế để ghi đè hành vi của các hàm Excel tích hợp, không phải để tạo các hàm tùy chỉnh. Nếu bạn cần tạo các hàm tùy chỉnh, bạn có thể sử dụng `UserDefinedFunction` lớp trong Aspose.Cells.
### Tính năng này có sẵn trong mọi phiên bản Aspose.Cells cho .NET không?
Vâng, `GlobalizationSettings` lớp và khả năng tùy chỉnh tên hàm có sẵn trong mọi phiên bản Aspose.Cells cho .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}