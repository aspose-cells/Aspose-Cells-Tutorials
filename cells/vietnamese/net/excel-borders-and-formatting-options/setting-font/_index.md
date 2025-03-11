---
title: Thiết lập Font chữ theo chương trình trong Excel
linktitle: Thiết lập Font chữ theo chương trình trong Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách thiết lập phông chữ theo chương trình trong Excel bằng Aspose.Cells cho .NET. Nâng cao bảng tính của bạn bằng phông chữ thời trang.
weight: 11
url: /vi/net/excel-borders-and-formatting-options/setting-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thiết lập Font chữ theo chương trình trong Excel

## Giới thiệu
Bạn đang muốn thao tác các tệp Excel một cách tinh tế? Bạn đã đến đúng nơi rồi! Aspose.Cells for .NET là một thư viện đặc biệt cho phép các nhà phát triển làm việc với các bảng tính Excel một cách dễ dàng. Một tác vụ phổ biến trong Excel là điều chỉnh kiểu phông chữ của một số ô nhất định, đặc biệt là khi bạn đang xử lý định dạng có điều kiện. Hãy tưởng tượng bạn có thể tự động làm nổi bật dữ liệu quan trọng, giúp báo cáo của bạn không chỉ có chức năng mà còn hấp dẫn về mặt thị giác. Nghe có vẻ tuyệt vời, phải không? Hãy cùng tìm hiểu cách bạn có thể thiết lập kiểu phông chữ theo chương trình bằng Aspose.Cells for .NET.
## Điều kiện tiên quyết
Trước khi bắt tay vào viết mã, hãy đảm bảo bạn đã chuẩn bị mọi thứ. Sau đây là những gì bạn cần:
1. Visual Studio: Đảm bảo bạn đã cài đặt phiên bản Visual Studio (khuyến nghị phiên bản 2017 trở lên).
2.  Aspose.Cells cho .NET: Nếu bạn chưa tải xuống, hãy tải xuống thư viện Aspose.Cells. Bạn có thể tải xuống từ[Trang web Aspose](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với C# sẽ hữu ích vì chúng ta sẽ viết mã bằng ngôn ngữ này.
4. .NET Framework: Đảm bảo bạn đã cài đặt phiên bản .NET Framework tương thích.
Khi đã đáp ứng được những điều kiện tiên quyết này, bạn đã sẵn sàng bắt đầu viết mã!
## Nhập gói
Để bắt đầu với Aspose.Cells, bạn cần nhập các gói cần thiết vào dự án của mình. Sau đây là cách bạn có thể thực hiện:
1. Mở dự án Visual Studio của bạn.
2. Nhấp chuột phải vào dự án của bạn trong Solution Explorer và chọn “Quản lý gói NuGet”.
3. Tìm kiếm “Aspose.Cells” và cài đặt nó. Thao tác này sẽ tự động thêm các tham chiếu cần thiết vào dự án của bạn.
Sau khi cài đặt gói, bạn có thể bắt đầu viết mã để thao tác với các tệp Excel!
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Bây giờ, chúng ta hãy cùng tìm hiểu từng bước trong quy trình thiết lập kiểu phông chữ trong bảng tính Excel.
## Bước 1: Xác định thư mục tài liệu
Trước tiên, bạn cần xác định thư mục nơi bạn muốn lưu tệp Excel của mình. Đây là nơi lưu trữ tất cả công sức của bạn, vì vậy hãy lựa chọn một cách khôn ngoan! Sau đây là cách bạn có thể thực hiện:
```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
```
 Thay thế`"Your Document Directory"` với đường dẫn thực tế trên hệ thống của bạn. Điều này có thể giống như`@"C:\Documents\"` nếu bạn đang làm việc trên Windows.
## Bước 2: Khởi tạo một đối tượng Workbook
 Bây giờ chúng ta đã thiết lập xong thư mục, đã đến lúc tạo một sổ làm việc mới. Hãy nghĩ đến`Workbook` đối tượng như một khung vẽ trống nơi bạn sẽ tô màu dữ liệu của mình. Sau đây là cách khởi tạo nó:
```csharp
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();
```
## Bước 3: Truy cập vào trang tính đầu tiên
 Tiếp theo, chúng ta cần truy cập vào trang tính nơi chúng ta sẽ áp dụng định dạng của mình. Trong một sổ làm việc mới, trang tính đầu tiên thường nằm ở mục lục`0`. Sau đây là cách bạn có thể thực hiện điều đó:
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
## Bước 4: Thêm Định dạng có điều kiện
Bây giờ, hãy làm mọi thứ thú vị hơn một chút bằng cách thêm định dạng có điều kiện. Định dạng có điều kiện cho phép bạn chỉ áp dụng định dạng khi đáp ứng được một số điều kiện nhất định. Sau đây là cách thêm định dạng:
```csharp
// Thêm định dạng có điều kiện trống
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```
Bằng cách thêm định dạng có điều kiện, chúng ta đang thiết lập để áp dụng các kiểu dựa trên các tiêu chí cụ thể.
## Bước 5: Thiết lập Phạm vi Định dạng Có điều kiện
Tiếp theo, chúng ta sẽ xác định phạm vi ô mà chúng ta muốn áp dụng định dạng có điều kiện. Điều này giống như nói rằng, "Này, tôi muốn áp dụng các quy tắc của mình vào khu vực này." Sau đây là cách bạn có thể chỉ định phạm vi:
```csharp
// Thiết lập phạm vi định dạng có điều kiện.
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 5;
ca.StartColumn = 0;
ca.EndColumn = 3;
fcs.AddArea(ca);
```
Trong ví dụ này, chúng tôi định dạng các ô từ A1 đến D6 (có chỉ mục 0). Điều chỉnh các giá trị này khi cần cho trường hợp sử dụng cụ thể của bạn!
## Bước 6: Thêm điều kiện
Bây giờ, hãy chỉ định điều kiện mà định dạng sẽ được áp dụng. Trong trường hợp này, chúng ta muốn định dạng các ô có giá trị từ 50 đến 100. Sau đây là cách thêm điều kiện đó:
```csharp
// Thêm điều kiện.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```
Dòng này về cơ bản có nghĩa là "Nếu giá trị ô nằm trong khoảng từ 50 đến 100, thì áp dụng định dạng của tôi".
## Bước 7: Thiết lập Kiểu Phông chữ
Đây là phần thú vị! Bây giờ, chúng ta thực sự có thể xác định kiểu phông chữ mà chúng ta muốn áp dụng cho các ô của mình. Hãy làm cho phông chữ nghiêng, đậm, gạch ngang, gạch chân và thay đổi màu của nó. Đây là mã để thực hiện điều đó:
```csharp
// Đặt màu nền.
FormatCondition fc = fcs[conditionIndex];
// fc.Style.BackgroundColor = Color.Red; // Bỏ chú thích để thiết lập màu nền
fc.Style.Font.IsItalic = true;
fc.Style.Font.IsBold = true;
fc.Style.Font.IsStrikeout = true;
fc.Style.Font.Underline = FontUnderlineType.Double;
fc.Style.Font.Color = Color.Black;
```
Hãy thoải mái thử nghiệm những phong cách này! Có thể bạn muốn một nền sáng hoặc màu sắc khác? Hãy thử xem!
## Bước 8: Lưu Workbook
Cuối cùng, sau khi bạn đã hoàn thành tất cả công việc khó khăn này, đừng quên lưu kiệt tác của bạn! Sau đây là cách bạn có thể lưu sổ làm việc của mình:
```csharp
workbook.Save(dataDir + "output.xlsx");
```
 Dòng này lưu tệp Excel của bạn dưới dạng`output.xlsx` trong thư mục được chỉ định. Hãy đảm bảo bạn có quyền ghi ở vị trí đó!
## Phần kết luận
Và bạn đã có nó! Bạn vừa học cách thiết lập kiểu phông chữ theo chương trình trong Excel bằng Aspose.Cells cho .NET. Từ việc xác định thư mục tài liệu của bạn đến áp dụng định dạng có điều kiện và cuối cùng là lưu công việc của bạn, giờ đây bạn đã có các công cụ để làm cho các tệp Excel của mình hấp dẫn về mặt hình ảnh và chức năng.
Cho dù bạn đang tạo báo cáo, tự động hóa tác vụ hay tạo bảng thông tin, việc thành thạo nghệ thuật chỉnh sửa phông chữ có thể nâng cấp bảng tính của bạn từ cơ bản lên đẹp mắt.
## Câu hỏi thường gặp
### Tôi có thể áp dụng nhiều kiểu phông chữ khác nhau cho các điều kiện khác nhau không?  
Hoàn toàn có thể! Bạn có thể thêm nhiều điều kiện và chỉ định kiểu phông chữ khác nhau cho từng điều kiện.
### Tôi có thể sử dụng những loại điều kiện nào trong định dạng có điều kiện?  
Bạn có thể sử dụng nhiều loại điều kiện khác nhau, bao gồm giá trị ô, công thức, v.v. Aspose.Cells cung cấp nhiều tùy chọn phong phú.
### Aspose.Cells có miễn phí sử dụng không?  
 Aspose.Cells là một sản phẩm thương mại, nhưng bạn có thể dùng thử miễn phí với thời gian dùng thử có hạn[đây](https://releases.aspose.com/).
### Tôi có thể định dạng toàn bộ một hàng dựa trên giá trị của một ô không?  
Có! Bạn có thể thiết lập định dạng cho toàn bộ hàng hoặc cột dựa trên giá trị của một ô cụ thể bằng cách sử dụng định dạng có điều kiện.
### Tôi có thể tìm thêm thông tin về Aspose.Cells ở đâu?  
 Bạn có thể tìm thấy tài liệu và nguồn tài nguyên mở rộng trên[Trang tài liệu Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
