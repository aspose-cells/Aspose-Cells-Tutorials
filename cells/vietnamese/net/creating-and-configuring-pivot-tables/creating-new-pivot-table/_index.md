---
title: Tạo một bảng Pivot mới theo chương trình trong .NET
linktitle: Tạo một bảng Pivot mới theo chương trình trong .NET
second_title: API xử lý Excel Aspose.Cells .NET
description: Học cách tạo bảng trục theo chương trình trong .NET bằng Aspose.Cells với hướng dẫn từng bước của chúng tôi. Phân tích dữ liệu của bạn một cách hiệu quả.
weight: 13
url: /vi/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo một bảng Pivot mới theo chương trình trong .NET

## Giới thiệu
Việc tạo một bảng trục có vẻ như là một nhiệm vụ khó khăn, đặc biệt là khi bạn thực hiện theo chương trình. Nhưng đừng lo lắng! Với Aspose.Cells cho .NET, việc tạo một bảng trục không chỉ đơn giản mà còn khá mạnh mẽ để phân tích dữ liệu. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước về cách tạo một bảng trục mới trong ứng dụng .NET. Cho dù bạn đang thêm dữ liệu cho doanh số bán hàng, thể thao hay bất kỳ số liệu kinh doanh nào khác, hướng dẫn này sẽ giúp bạn thiết lập và chạy các bảng trục của mình chỉ trong thời gian ngắn.

## Điều kiện tiên quyết
Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị mọi thứ sẵn sàng. Sau đây là những gì bạn cần làm:

1. Cài đặt .NET Framework: Đảm bảo bạn đã cài đặt .NET Framework trên máy của mình. Aspose.Cells hỗ trợ nhiều phiên bản khác nhau, nhưng tốt nhất là bạn nên sử dụng phiên bản mới nhất.
2.  Thư viện Aspose.Cells: Bạn cần có thư viện Aspose.Cells. Bạn có thể[tải xuống ở đây](https://releases.aspose.com/cells/net/)hoặc nhận được một[giấy phép tạm thời](https://purchase.aspose.com/temporary-license/) để đánh giá.
3. Thiết lập IDE: Chuẩn bị một IDE tương thích với C#, như Visual Studio, nơi bạn có thể bắt đầu một dự án mới.
4. Kiến thức cơ bản về C#: Sự quen thuộc với lập trình C# sẽ giúp bạn theo dõi mà không bị bối rối.

Bạn đã sẵn sàng chưa? Tuyệt! Hãy bắt đầu nhập các gói cần thiết.

## Nhập gói
Trước tiên, bạn cần nhập các không gian tên cần thiết vào dự án C# của mình. Mở tệp C# của bạn và thêm các chỉ thị sau:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Các không gian tên này cung cấp cho bạn quyền truy cập vào các chức năng của sổ làm việc, bảng tính và bảng trục mà chúng ta sẽ sử dụng trong suốt hướng dẫn này.

## Bước 1: Tạo một đối tượng Workbook
Tạo một sổ làm việc là bước khởi đầu cho hành trình của bạn. Hãy bắt đầu bằng cách tạo một sổ làm việc mới và truy cập vào trang tính đầu tiên.

```csharp
// Đường dẫn đến thư mục tài liệu.
string dataDir = "Your Document Directory";
// Khởi tạo một đối tượng Workbook
Workbook workbook = new Workbook();

// Lấy tham chiếu của bảng tính mới được thêm vào
Worksheet sheet = workbook.Worksheets[0];
```

 Trong bước này, chúng ta tạo ra một`Workbook`trường hợp đại diện cho tệp Excel của chúng ta và lấy bảng tính đầu tiên, đây sẽ là sân chơi cho bảng trục.

## Bước 2: Chèn dữ liệu vào ô
Tiếp theo, hãy điền một số dữ liệu mẫu vào bảng tính của chúng ta. Chúng ta sẽ nhập các hàng cho các môn thể thao, quý và số liệu bán hàng khác nhau để cung cấp cho bảng trục của chúng ta một cái gì đó để tóm tắt.

```csharp
Cells cells = sheet.Cells;

// Thiết lập giá trị cho các ô
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Điền datacell = cells["A2"];
cell.PutValue("Golf");
// ... Thêm mục nhập dữ liệu
```

Ở đây, chúng ta sẽ định nghĩa tiêu đề cột và chèn giá trị vào mỗi tiêu đề. Dữ liệu này sẽ đóng vai trò là nguồn cho bảng trục của chúng ta, vì vậy hãy đảm bảo rằng nó được sắp xếp hợp lý! Thực hiện theo khối này và bạn sẽ tạo ra một tập dữ liệu toàn diện.

## Bước 3: Thêm Bảng Pivot
Khi dữ liệu đã sẵn sàng, đã đến lúc tạo bảng trục. Chúng ta sẽ sử dụng bộ sưu tập bảng trục từ bảng tính để thêm bảng trục mới.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Thêm PivotTable vào bảng tính
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Trong đoạn mã này, chúng ta thêm một bảng trục vào trang tính tham chiếu đến phạm vi dữ liệu của chúng ta (trong trường hợp này là các ô từ A1 đến C8). Chúng ta đặt bảng trục bắt đầu từ ô E3 và đặt tên là "PivotTable2". Khá đơn giản, phải không?

## Bước 4: Tùy chỉnh Bảng Pivot
Bây giờ chúng ta đã có bảng trục, hãy tùy chỉnh nó để hiển thị tóm tắt có ý nghĩa. Chúng ta có thể kiểm soát những gì xuất hiện trong các hàng, cột và vùng dữ liệu của bảng trục.

```csharp
// Truy cập vào phiên bản PivotTable mới được thêm vào
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Không hiển thị tổng số của các hàng.
pivotTable.RowGrand = false;

// Kéo trường đầu tiên vào vùng hàng.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Kéo trường thứ hai vào vùng cột.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Kéo trường thứ ba vào vùng dữ liệu.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Trong bước này, chúng tôi yêu cầu bảng trục ẩn tổng số cho các hàng và sau đó chỉ định trường nào sẽ đi vào hàng, cột và vùng dữ liệu. Tên môn thể thao sẽ điền vào các hàng, các quý sẽ điền vào các cột và số liệu bán hàng sẽ cung cấp tóm tắt.

## Bước 5: Lưu sổ làm việc
Cuối cùng, chúng ta muốn lưu bảng tính mới tạo để xem thành quả lao động của mình.

```csharp
// Lưu tệp Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Chỉ cần cung cấp đường dẫn thích hợp và kết quả bảng trục của bạn sẽ được lưu vào tệp Excel mà bạn có thể mở và xem lại.

## Phần kết luận
Tạo bảng trục theo chương trình bằng Aspose.Cells cho .NET có thể giúp bạn tiết kiệm đáng kể thời gian, đặc biệt là khi xử lý các tập dữ liệu lớn. Bạn đã học cách thiết lập dự án của mình, nhập các gói cần thiết, điền dữ liệu và tạo bảng trục tùy chỉnh từ đầu. Vì vậy, lần tới khi bạn bị chìm trong số liệu, hãy nhớ hướng dẫn này và để Aspose.Cells thực hiện công việc nặng nhọc thay bạn.

## Câu hỏi thường gặp
### Aspose.Cells là gì?
Aspose.Cells là một thư viện .NET mạnh mẽ để tạo và quản lý bảng tính Excel theo chương trình.

### Có bản dùng thử miễn phí Aspose.Cells không?
 Có, bạn có thể dùng thử miễn phí[đây](https://releases.aspose.com/).

### Tôi có thể tùy chỉnh giao diện của bảng trục không?
Chắc chắn rồi! Bạn có thể tùy chỉnh định dạng, bố cục và thậm chí cả kiểu của bảng trục theo nhu cầu của mình.

### Tôi có thể tìm thêm ví dụ và tài liệu về Aspose.Cells ở đâu?
 Bạn có thể kiểm tra[tài liệu](https://reference.aspose.com/cells/net/) để có hướng dẫn và ví dụ toàn diện.

### Làm thế nào để tôi nhận được hỗ trợ cho Aspose.Cells?
 Bạn có thể nhận được hỗ trợ thông qua[Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
