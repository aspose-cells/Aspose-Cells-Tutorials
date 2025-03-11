---
title: Sao chép VBAMacro User Form Designer Storage vào Workbook bằng Aspose.Cells
linktitle: Sao chép VBAMacro User Form Designer Storage vào Workbook bằng Aspose.Cells
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách sao chép VBA Macro User Form Designer hiệu quả trong Aspose.Cells cho .NET với hướng dẫn từng bước toàn diện của chúng tôi! Mở khóa tiềm năng của Excel.
weight: 11
url: /vi/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sao chép VBAMacro User Form Designer Storage vào Workbook bằng Aspose.Cells

## Giới thiệu
Chào mừng! Nếu bạn đang muốn nâng cao trải nghiệm Excel của mình bằng macro VBA và biểu mẫu người dùng, bạn đã đến đúng nơi rồi! Trong hướng dẫn này, chúng tôi sẽ đi sâu vào cách bạn có thể sao chép liền mạch Macro VBA UserForm Designer từ sổ làm việc này sang sổ làm việc khác bằng Aspose.Cells for .NET. Cho dù bạn là một nhà phát triển dày dạn kinh nghiệm hay chỉ mới bắt đầu, chúng tôi sẽ hướng dẫn bạn từng bước quan trọng. Hãy coi đây là cẩm nang của bạn để thành thạo nghệ thuật xử lý các tệp Excel theo chương trình. Sẵn sàng để bắt đầu chưa? Bắt đầu thôi!
## Điều kiện tiên quyết
Trước khi đi sâu vào phần mã hóa, hãy đảm bảo rằng bạn có mọi thứ cần thiết:
1. Môi trường phát triển C#: Bạn nên có một môi trường làm việc sẵn sàng cho việc phát triển C#. Visual Studio được khuyến khích sử dụng.
2.  Aspose.Cells cho Thư viện .NET: Đảm bảo bạn đã tích hợp thư viện Aspose.Cells vào dự án của mình. Bạn có thể dễ dàng[tải xuống ở đây](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về VBA và Macro Excel: Hiểu rõ về VBA và cách thức hoạt động của macro Excel sẽ giúp bạn dễ dàng thực hiện hướng dẫn này.
4. Tệp Excel có Biểu mẫu Người dùng: Để thử nghiệm, hãy tạo hoặc lấy một sổ làm việc Excel có chứa Biểu mẫu Người dùng, tốt nhất là có bật macro (như`.xlsm` tập tin).
## Nhập gói
Trong dự án C# của bạn, bạn sẽ cần nhập một số không gian tên nhất định ở đầu tệp của mình để sử dụng các chức năng của Aspose.Cells. Sau đây là cách thực hiện:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Việc bao gồm các không gian tên này cho phép bạn truy cập tất cả các công cụ mạnh mẽ được nhúng trong thư viện Aspose.Cells. 
Bây giờ chúng ta đã có các điều kiện tiên quyết và các gói, đã đến lúc chuyển sang phần thú vị: mã hóa! Hãy cùng phân tích từng bước một.
## Bước 1: Xác định thư mục nguồn và thư mục đầu ra của bạn
Đầu tiên, bạn cần xác định vị trí lưu trữ các tập tin của mình:
```csharp
// Thư mục nguồn
string sourceDir = "Your Document Directory";
// Thư mục đầu ra
string outputDir = "Your Document Directory";
```
 Ở đây, thay thế`"Your Document Directory"` với đường dẫn thực tế nơi các tệp của bạn được lưu trữ. Đây là nơi sổ làm việc nguồn của chúng tôi (có UserForm) sẽ được lấy từ đó và nơi sổ làm việc mới sẽ được lưu.
## Bước 2: Tạo một Workbook mục tiêu trống
Tiếp theo, hãy tạo bảng tính mục tiêu để sao chép biểu mẫu người dùng và macro:
```csharp
// Tạo sổ làm việc mục tiêu trống
Workbook target = new Workbook();
```
Dòng mã này khởi tạo một sổ làm việc mới, trống để chúng ta điền dữ liệu. Hãy coi nó như một bức tranh vải trắng cho kiệt tác của bạn!
## Bước 3: Tải Sổ làm việc mẫu của bạn
Chúng ta cần tải lên bảng tính có chứa biểu mẫu người dùng và macro của bạn:
```csharp
// Tải tệp Excel có chứa VBA-Macro Designer User Form
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Hãy chắc chắn để thay đổi`"sampleDesignerForm.xlsm"` vào tên tệp thực tế của bạn. Sổ làm việc này giống như sổ công thức nấu ăn của bạn—đó là thứ chúng ta sẽ lấy nguyên liệu từ đó!
## Bước 4: Sao chép các trang tính vào sổ làm việc đích
Bây giờ, chúng ta hãy bắt đầu sao chép các bảng tính từ mẫu của mình sang bảng tính đích:
```csharp
// Sao chép tất cả các bảng tính mẫu vào sổ làm việc mục tiêu
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Đặt tin nhắn vào ô A2 của bảng tính mục tiêu
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
Trong bước này, chúng ta sẽ lặp qua từng bảng tính trong mẫu và sao chép chúng vào sổ làm việc mục tiêu của chúng ta. Nếu bạn nghĩ về điều đó, nó giống như việc chuyển những công thức nấu ăn ngon nhất của bạn từ một cuốn sách dạy nấu ăn sang một cuốn sách khác!
## Bước 5: Sao chép Macro VBA từ Mẫu
Tiếp theo, chúng ta sẽ sao chép các macro VBA, bao gồm các mô-đun UserForm Designer, vào bảng tính mới của mình:
```csharp
// Sao chép VBA-Macro Designer UserForm từ Mẫu đến Mục tiêu
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Sao chép mã mô-đun Workbook này
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Sao chép mã và dữ liệu của các mô-đun khác
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Lấy dữ liệu của biểu mẫu người dùng tức là lưu trữ thiết kế
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Thêm bộ lưu trữ thiết kế vào Dự án Vba mục tiêu
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Đoạn mã lớn này xử lý việc kiểm tra từng mô-đun VBA trong tệp mẫu. Chúng tôi đang sao chép thiết kế UserForm và các mã liên quan. Giống như đảm bảo bạn không chỉ có được công thức làm bánh nổi tiếng của Bà mà còn có cả kỹ thuật nướng bánh chính xác của bà!
## Bước 6: Lưu Workbook mục tiêu
Sau khi đã có đủ bản sao, đã đến lúc lưu lại công sức của chúng ta:
```csharp
// Lưu sổ làm việc mục tiêu
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Hãy đảm bảo sửa đổi tên tệp đầu ra khi cần thiết. Sau khi lưu, bạn thực sự đang tạo phiên bản sổ làm việc được thiết kế riêng của mình với đầy đủ các macro và biểu mẫu người dùng. Thật thú vị phải không?
## Bước 7: Xác nhận thành công
Cuối cùng, hãy in thông báo thành công ra bảng điều khiển:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Dòng nhỏ này đảm bảo với bạn rằng quá trình của bạn diễn ra suôn sẻ. Đây chính là điểm nhấn cho ly kem mã hóa của bạn!
## Phần kết luận
Xin chúc mừng! Bạn đã hoàn thành hướng dẫn từng bước để sao chép VBA Macro User Form Designer từ sổ làm việc này sang sổ làm việc khác bằng Aspose.Cells for .NET. Thoạt đầu có vẻ hơi khó khăn, nhưng khi thực hành, bạn sẽ xử lý được các thao tác trên sổ làm việc như một chuyên gia. Hãy nhớ rằng, mã hóa là tất cả về thực hành, vì vậy đừng ngại thử những điều khác nhau trong các tệp Excel của bạn. Nếu bạn có bất kỳ câu hỏi nào hoặc gặp phải bất kỳ sự cố nào, hãy thoải mái kiểm tra diễn đàn hoặc tài liệu của Aspose để được hỗ trợ!
## Câu hỏi thường gặp
### Aspose.Cells hỗ trợ những phiên bản Excel nào?
Aspose.Cells hỗ trợ nhiều định dạng Excel bao gồm XLSX, XLSM, CSV, v.v.
### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có! Bạn có thể bắt đầu bằng bản dùng thử miễn phí, cho phép bạn đánh giá thư viện:[Dùng thử miễn phí](https://releases.aspose.com/).
### Tôi có cần Visual Studio để chạy mã này không?
Mặc dù được khuyến khích sử dụng vì các tính năng thân thiện với người dùng, bất kỳ IDE C# nào cũng có thể sử dụng được miễn là nó hỗ trợ phát triển .NET.
### Tôi có thể tìm thêm ví dụ và tài liệu ở đâu?
 Bạn có thể khám phá[Tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/) để biết thêm ví dụ và giải thích chi tiết.
### Làm thế nào để giải quyết vấn đề khi sử dụng Aspose.Cells?
 Bạn nên ghé thăm[Diễn đàn hỗ trợ Aspose](https://forum.aspose.com/c/cells/9) để được cộng đồng và đội ngũ hỗ trợ của Aspose giúp đỡ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
