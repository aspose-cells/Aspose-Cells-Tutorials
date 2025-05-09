---
"description": "Tìm hiểu cách tạo biểu đồ hình tròn trong Excel bằng Aspose.Cells cho .NET với hướng dẫn từng bước này. Trực quan hóa dữ liệu của bạn một cách dễ dàng."
"linktitle": "Tạo biểu đồ hình tròn"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Tạo biểu đồ hình tròn"
"url": "/vi/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tạo biểu đồ hình tròn

## Giới thiệu

Tạo biểu đồ là điều cần thiết để biểu diễn dữ liệu trực quan và biểu đồ hình tròn là một trong những cách phổ biến nhất để minh họa cách các bộ phận tạo nên tổng thể. Với Aspose.Cells for .NET, bạn có thể dễ dàng tự động hóa việc tạo biểu đồ hình tròn trong các tệp Excel. Trong hướng dẫn này, chúng ta sẽ tìm hiểu cách tạo biểu đồ hình tròn từ đầu bằng Aspose.Cells for .NET, với hướng dẫn từng bước để giúp quá trình này diễn ra suôn sẻ và dễ dàng. Cho dù bạn mới sử dụng công cụ này hay muốn nâng cao kỹ năng tự động hóa Excel của mình, hướng dẫn này sẽ giúp bạn!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, hãy đảm bảo bạn đã thiết lập những thông tin sau:

1. Aspose.Cells cho Thư viện .NET: Đảm bảo rằng bạn đã cài đặt Aspose.Cells trong dự án của mình. Nếu bạn chưa cài đặt, bạn có thể tải xuống từ [đây](https://releases.aspose.com/cells/net/).
2. Môi trường phát triển .NET: Đảm bảo dự án của bạn được thiết lập để sử dụng .NET Framework hoặc .NET Core.
3. Kiến thức cơ bản về C#: Bạn nên thành thạo lập trình C#, đặc biệt là lập trình hướng đối tượng (OOP).

Đối với người dùng nâng cao, có thể áp dụng giấy phép tạm thời để mở khóa tất cả các tính năng của Aspose.Cells. Bạn có thể yêu cầu một giấy phép từ [đây](https://purchase.aspose.com/temporary-license/).

## Nhập gói

Để bắt đầu, hãy nhập các không gian tên và gói cần thiết cho hướng dẫn này. Bao gồm các hoạt động I/O cơ bản và gói Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Bước 1: Tạo một Workbook mới

Đầu tiên, chúng ta cần tạo một phiên bản của `Workbook` lớp, biểu diễn tệp Excel. Một sổ làm việc chứa nhiều trang tính và trong ví dụ của chúng tôi, chúng tôi sẽ làm việc với hai trang tính—một trang tính cho dữ liệu và một trang tính cho biểu đồ hình tròn.

```csharp
Workbook workbook = new Workbook();
```

Thao tác này khởi tạo một bảng tính Excel mới. Nhưng dữ liệu sẽ đi đâu? Chúng ta hãy giải quyết vấn đề đó ở bước tiếp theo.

## Bước 2: Thêm dữ liệu vào trang tính

Sau khi tạo xong sổ làm việc, chúng ta cần truy cập vào trang tính đầu tiên và đặt tên cho nó. Đây là nơi chúng ta sẽ nhập dữ liệu cần thiết cho biểu đồ hình tròn.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Bây giờ, chúng ta có thể nhập một số dữ liệu bán hàng giả định đại diện cho các khu vực khác nhau:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Ở đây, chúng tôi sẽ thêm hai cột: một cột cho khu vực và một cột cho số liệu bán hàng. Dữ liệu này sẽ được thể hiện trong biểu đồ hình tròn.

## Bước 3: Thêm một bảng biểu đồ

Tiếp theo, chúng ta hãy thêm một bảng tính riêng để lưu biểu đồ hình tròn.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Trang tính mới này sẽ lưu trữ biểu đồ hình tròn. Đặt tên cho nó như "Biểu đồ" để đảm bảo người dùng biết những gì mong đợi khi họ mở tệp.

## Bước 4: Tạo biểu đồ hình tròn

Bây giờ là lúc tạo biểu đồ thực tế. Chúng ta sẽ chỉ định rằng chúng ta muốn có biểu đồ hình tròn và chúng ta sẽ xác định vị trí của nó trên trang tính.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

Phương pháp `Add()` chấp nhận các tham số cho loại biểu đồ (trong trường hợp này, `ChartType.Pie`), và vị trí của nó trên bảng tính. Các con số biểu thị vị trí hàng và cột.

## Bước 5: Tùy chỉnh giao diện biểu đồ

Biểu đồ hình tròn sẽ không hoàn chỉnh nếu không có một số tùy chỉnh! Hãy làm cho biểu đồ của chúng ta hấp dẫn về mặt thị giác bằng cách điều chỉnh màu sắc, nhãn và tiêu đề.

### Đặt tiêu đề biểu đồ
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Tùy chỉnh khu vực lô đất
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Chúng tôi thiết lập độ dốc cho vùng vẽ và ẩn đường viền để có giao diện rõ ràng hơn.

## Bước 6: Xác định dữ liệu biểu đồ

Đã đến lúc liên kết biểu đồ với dữ liệu của chúng tôi. `NSeries` Thuộc tính của biểu đồ liên kết số liệu bán hàng và khu vực với biểu đồ hình tròn.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

Dòng đầu tiên chỉ rõ rằng chúng ta đang sử dụng dữ liệu bán hàng từ các ô `B2:B8`. Chúng tôi cũng yêu cầu biểu đồ sử dụng tên vùng từ `A2:A8` như nhãn danh mục.

## Bước 7: Thêm nhãn dữ liệu

Thêm nhãn trực tiếp vào các phân đoạn biểu đồ có thể giúp bạn hiểu rõ hơn. Hãy đưa tên vùng và giá trị bán hàng vào các lát cắt biểu đồ hình tròn.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Bước 8: Tùy chỉnh Khu vực Biểu đồ và Chú giải

Cuối cùng, hãy hoàn thiện khu vực biểu đồ và chú giải. Điều này giúp nâng cao khả năng trình bày tổng thể của biểu đồ.

### Biểu đồ khu vực
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Huyền thoại
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Bước 9: Lưu Workbook

Cuối cùng, chúng ta lưu sổ làm việc vào một tệp Excel. Bạn có thể chỉ định thư mục đầu ra và tên tệp khi cần.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Phần kết luận

Tạo biểu đồ hình tròn bằng Aspose.Cells cho .NET là một quy trình đơn giản và có thể tùy chỉnh. Bằng cách làm theo hướng dẫn này, bạn có thể tạo biểu đồ trông chuyên nghiệp truyền tải những hiểu biết có giá trị chỉ trong vài bước. Cho dù là để báo cáo kinh doanh hay mục đích giáo dục, việc thành thạo việc tạo biểu đồ sẽ nâng cao kỹ năng tự động hóa Excel của bạn. Hãy nhớ rằng, Aspose.Cells cung cấp sự linh hoạt mà bạn cần để tạo các tệp Excel tuyệt đẹp, dựa trên dữ liệu một cách dễ dàng.

## Câu hỏi thường gặp

### Tôi có thể tạo các loại biểu đồ khác bằng Aspose.Cells cho .NET không?
Có! Aspose.Cells hỗ trợ nhiều loại biểu đồ khác nhau, bao gồm biểu đồ thanh, biểu đồ đường và biểu đồ phân tán.

### Tôi có cần giấy phép trả phí để sử dụng Aspose.Cells cho .NET không?
Bạn có thể sử dụng phiên bản miễn phí với một số hạn chế. Để có đầy đủ tính năng, bạn sẽ cần một giấy phép, bạn có thể mua [đây](https://purchase.aspose.com/buy).

### Tôi có thể xuất biểu đồ sang các định dạng như PDF hoặc hình ảnh không?
Chắc chắn rồi! Aspose.Cells cho phép bạn xuất biểu đồ sang nhiều định dạng khác nhau, bao gồm PDF và PNG.

### Có thể trang trí mỗi lát bánh bằng nhiều màu sắc khác nhau không?
Có, bạn có thể áp dụng các màu khác nhau cho mỗi lát cắt bằng cách thiết lập `IsColorVaried` tài sản để `true`, như được hiển thị trong hướng dẫn.

### Tôi có thể tự động tạo nhiều biểu đồ trong một bảng tính không?
Có, bạn có thể tạo và tùy chỉnh nhiều biểu đồ tùy theo nhu cầu trong một tệp Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}