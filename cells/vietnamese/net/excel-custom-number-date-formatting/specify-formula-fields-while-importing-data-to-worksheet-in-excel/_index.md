---
title: Chỉ định các trường công thức khi nhập dữ liệu vào bảng tính Excel
linktitle: Chỉ định các trường công thức khi nhập dữ liệu vào bảng tính Excel
second_title: API xử lý Excel Aspose.Cells .NET
description: Tìm hiểu cách nhập dữ liệu vào các trang tính Excel có trường công thức được chỉ định bằng Aspose.Cells cho .NET trong hướng dẫn chi tiết này.
weight: 11
url: /vi/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chỉ định các trường công thức khi nhập dữ liệu vào bảng tính Excel

## Giới thiệu

Khi nói đến việc xử lý các tệp Excel theo chương trình, Aspose.Cells for .NET là một công cụ vô giá. Nó cung cấp chức năng mạnh mẽ để tạo, sửa đổi và thao tác các bảng tính Excel một cách dễ dàng. Một trong những tính năng thú vị mà nó cung cấp là khả năng chỉ định các trường công thức trong khi nhập dữ liệu vào một bảng tính Excel. Hãy tưởng tượng bạn đang làm việc trên một báo cáo tài chính và cần tự động tính tổng dựa trên đầu vào của người dùng. Hướng dẫn này sẽ hướng dẫn bạn từng bước để đạt được điều đó với một cách tiếp cận rõ ràng và đơn giản.

## Điều kiện tiên quyết

Trước khi tìm hiểu về mã, hãy đảm bảo rằng bạn có mọi thứ mình cần. 

1. Visual Studio hoặc bất kỳ môi trường phát triển tích hợp (IDE) .NET nào: Đảm bảo bạn có IDE phù hợp để viết và chạy mã C#.
2.  Aspose.Cells cho .NET: Bạn sẽ cần tải xuống và tham chiếu thư viện Aspose.Cells trong dự án của mình. Bạn có thể tải xuống từ[Aspose phát hành](https://releases.aspose.com/cells/net/).
3. Kiến thức cơ bản về C#: Sự quen thuộc với C# và các khái niệm lập trình hướng đối tượng sẽ giúp bạn hiểu các ví dụ tốt hơn.
4. .NET Framework: Hướng dẫn này giả định rằng bạn đang sử dụng .NET Framework 4.5 trở lên.

Sau khi đã sắp xếp xong các điều kiện tiên quyết, chúng ta hãy tiến hành nhập một số dữ liệu vào bảng tính Excel với các trường công thức được chỉ định.

## Nhập gói

Trước khi bắt đầu viết mã, bạn sẽ cần nhập không gian tên Aspose.Cells cần thiết. Điều này thường được thực hiện ở đầu tệp C# của bạn:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Điều này cho phép bạn sử dụng các lớp và phương thức do thư viện Aspose.Cells cung cấp mà không cần phải thêm tiền tố không gian tên vào mỗi lần.

Chúng ta hãy chia nhỏ toàn bộ quá trình thành các bước dễ quản lý:

## Bước 1: Xác định thư mục đầu ra

Trước tiên, bạn cần thiết lập nơi bạn muốn lưu tệp Excel của mình. Sau đây là cách bạn có thể thực hiện:

```csharp
static string outputDir = "Your Document Directory"; // chỉ định thư mục tài liệu của bạn ở đây
```

 Thay thế`"Your Document Directory"` với đường dẫn tệp thực tế của bạn. Đây là nơi tệp Excel được tạo sẽ được lưu.

## Bước 2: Tạo một lớp do người dùng định nghĩa cho các mục dữ liệu

Tiếp theo, chúng ta sẽ định nghĩa một lớp để cấu trúc dữ liệu mà chúng ta dự định nhập.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Cái này`DataItems` Lớp này sẽ lưu trữ các số nguyên thô và các công thức mà chúng ta sẽ ghi vào bảng tính Excel. 

## Bước 3: Khởi tạo danh sách để lưu trữ các mục dữ liệu

 Chúng tôi sẽ sử dụng một danh sách để lưu trữ nhiều trường hợp của chúng tôi`DataItems` lớp học.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Bước 4: Thêm mục dữ liệu vào danh sách

Bây giờ, hãy thêm một số mục vào danh sách của chúng ta. Mỗi mục sẽ chứa hai số và hai công thức.

```csharp
// Xác định và thêm từng mục dữ liệu
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Trang web Aspose\")";
dis.Add(di);

// Lặp lại cho các mục dữ liệu bổ sung
```

 Hãy chắc chắn tùy chỉnh từng cái`DataItems` trường hợp có giá trị và công thức duy nhất.

## Bước 5: Tạo Workbook và Access Worksheet

Tiếp theo, hãy tạo bảng tính và truy cập vào trang tính đầu tiên nơi chúng ta sẽ nhập dữ liệu.

```csharp
Workbook wb = new Workbook(); // tạo một bảng tính mới
Worksheet ws = wb.Worksheets[0]; // truy cập vào bảng tính đầu tiên
```

## Bước 6: Chỉ định Tùy chọn Bảng Nhập

Đây là nơi phép thuật xảy ra. Bạn cần chỉ định trường nào trong dữ liệu của bạn tương ứng với công thức. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 Trong ví dụ này, hai trường cuối cùng chứa công thức, được biểu thị bằng`true` , trong khi hai trường đầu tiên được đặt thành`false`.

## Bước 7: Nhập Đối tượng Tùy chỉnh

Bây giờ mọi thứ đã được thiết lập, hãy nhập danh sách các mục dữ liệu vào bảng tính.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Dòng này thực sự nhập dữ liệu bắt đầu từ ô A1.

## Bước 8: Tính toán công thức

Vì chúng ta đã nhập một số công thức nên việc tính toán chúng là rất quan trọng.

```csharp
wb.CalculateFormula();
```

Phương pháp này đảm bảo rằng các công thức của bạn được đánh giá dựa trên sự phụ thuộc của chúng.

## Bước 9: Tự động điều chỉnh cột

Để đảm bảo dữ liệu của bạn thân thiện với màn hình, bạn có thể tự động điều chỉnh các cột dựa trên nội dung.

```csharp
ws.AutoFitColumns();
```

Bước này tối ưu hóa bố cục của tệp Excel. 

## Bước 10: Lưu tệp Excel của bạn

Cuối cùng, đã đến lúc lưu tệp Excel mới tạo của bạn. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Hãy đảm bảo tên tệp đầu ra của bạn có liên quan và mô tả rõ ràng!

## Bước 11: Kiểm tra thực hiện

Một cách đơn giản để xác nhận mọi thứ đã chạy đúng, bạn có thể muốn in một tin nhắn.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Điều này cung cấp cho bạn phản hồi ngay lập tức rằng mã đã hoạt động mà không có bất kỳ vấn đề nào.

## Phần kết luận

Và bạn đã có nó! Bạn đã nhập dữ liệu thành công vào một bảng tính Excel bằng Aspose.Cells cho .NET và các trường công thức đã chỉ định. Bằng cách làm theo các bước này, bạn có thể áp dụng các kỹ thuật tương tự để tự động hóa các tác vụ xử lý dữ liệu phù hợp với nhu cầu của mình. Cho dù bạn đang xử lý số liệu cho báo cáo hay chỉ đơn giản là duy trì dữ liệu, việc thành thạo nghệ thuật thao tác Excel với Aspose là một kỹ năng đáng có.

## Câu hỏi thường gặp

### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET được thiết kế để tạo, thao tác và chuyển đổi các tệp Excel theo cách lập trình.

### Làm thế nào để cài đặt Aspose.Cells cho .NET?
 Bạn có thể tải nó xuống từ[Aspose phát hành](https://releases.aspose.com/cells/net/) và tham chiếu nó trong dự án của bạn.

### Tôi có thể sử dụng Aspose.Cells miễn phí không?
 Có, Aspose cung cấp bản dùng thử miễn phí có sẵn tại[liên kết này](https://releases.aspose.com/).

### Tôi có thể tìm thêm ví dụ ở đâu?
 Các ví dụ và tài liệu bổ sung có thể được tìm thấy tại[Trang tài liệu Aspose](https://reference.aspose.com/cells/net/).

### Tôi phải làm sao nếu gặp sự cố khi sử dụng Aspose?
 Bạn có thể tìm kiếm sự trợ giúp từ diễn đàn hỗ trợ Aspose[đây](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
