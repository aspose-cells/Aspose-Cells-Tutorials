---
"description": "Học cách chèn các hàng DataTable vào Excel mà không dịch chuyển hàng đầu tiên xuống dưới bằng Aspose.Cells cho .NET. Hướng dẫn từng bước để tự động hóa dễ dàng."
"linktitle": "Chuyển hàng đầu tiên xuống dưới khi chèn hàng DataTable trong Excel"
"second_title": "API xử lý Excel Aspose.Cells .NET"
"title": "Chuyển hàng đầu tiên xuống dưới khi chèn hàng DataTable trong Excel"
"url": "/vi/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển hàng đầu tiên xuống dưới khi chèn hàng DataTable trong Excel

## Giới thiệu

Bạn có thấy mệt mỏi khi phải tự tay dịch chuyển các hàng khi chèn dữ liệu mới vào bảng tính Excel của mình không? Vâng, bạn thật may mắn! Trong bài viết này, chúng ta sẽ tìm hiểu cách tự động hóa quy trình này bằng Aspose.Cells cho .NET. Đến cuối hướng dẫn này, bạn sẽ không chỉ học cách làm việc với các bảng dữ liệu trong Excel mà còn biết cách tùy chỉnh các tùy chọn nhập để phù hợp hơn với nhu cầu của mình. Tin tôi đi; điều này có thể giúp bạn tiết kiệm rất nhiều thời gian và công sức! Vậy thì, hãy pha một tách cà phê và bắt đầu thôi!

## Điều kiện tiên quyết

Trước khi bắt đầu viết mã, hãy đảm bảo rằng bạn đã thiết lập mọi thứ:

1. Visual Studio: Đảm bảo bạn đã cài đặt Visual Studio (phiên bản 2017 trở lên sẽ hoạt động tốt).
2. Aspose.Cells cho .NET: Bạn cần có thư viện Aspose.Cells. Nếu bạn chưa thực hiện việc này, bạn có thể tải xuống [đây](https://releases.aspose.com/cells/net/).
3. Hiểu biết cơ bản về C# và Excel: Nắm vững kiến thức cơ bản về lập trình C# và cách thức hoạt động của Excel chắc chắn sẽ giúp bạn theo dõi hiệu quả hơn.

Bạn cũng sẽ muốn có một tệp Excel mẫu tiện dụng. Trong hướng dẫn này, chúng tôi sẽ sử dụng một mẫu có tên là `sampleImportTableOptionsShiftFirstRowDown.xlsx`. Bạn có thể tạo tệp này hoặc tìm mẫu phù hợp với nhu cầu của mình.

## Nhập gói

Trước khi đi sâu vào mã hóa, chúng ta cần đảm bảo rằng chúng ta đã nhập các gói cần thiết. Trong dự án C# của bạn, hãy bao gồm các không gian tên sau:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Các gói này rất cần thiết để làm việc với sổ làm việc, bảng tính và bảng biểu.

## Bước 1: Thiết lập dự án của bạn

### Tạo một dự án C# mới

Bắt đầu bằng cách tạo một ứng dụng C# Console mới trong Visual Studio. Đặt tên phù hợp cho dự án của bạn, như “ExcelDataImport”.

### Thêm gói NuGet Aspose.Cells

Để thêm gói Aspose.Cells, hãy nhấp chuột phải vào dự án của bạn trong Solution Explorer, chọn Manage NuGet Packages và tìm kiếm “Aspose.Cells”. Cài đặt gói để đảm bảo bạn có thể truy cập tất cả các chức năng chúng ta cần.

## Bước 2: Xác định Bảng dữ liệu

Tiếp theo, chúng ta sẽ thực hiện `ICellsDataTable` giao diện để tạo một lớp cung cấp dữ liệu được nhập. Sau đây là cách bạn có thể cấu trúc `CellsDataTable` lớp học:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Triển khai các thành viên khác ...
}
```

Tại đây, chúng ta sẽ xác định tên cột và dữ liệu cho mỗi cột, điều này sẽ tạo thuận lợi cho cấu trúc của bảng được nhập.

## Bước 3: Triển khai các thành viên giao diện ICellsDataTable

Trong vòng `CellsDataTable` lớp, bạn cần phải triển khai các thành viên của `ICellsDataTable` giao diện. Sau đây là phần triển khai cần thiết:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Phần này của lớp xử lý việc truy xuất dữ liệu, xác định có bao nhiêu hàng và cột, cũng như quản lý trạng thái chỉ mục hiện tại.

## Bước 4: Viết hàm chính

Bây giờ, chúng ta hãy tạo ra `Run` phương pháp để sắp xếp toàn bộ quá trình nhập bảng:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Bước 5: Thiết lập Tùy chọn Nhập

Để kiểm soát hành vi nhập, bạn nên tạo một phiên bản của `ImportTableOptions` và thiết lập các thuộc tính cho phù hợp. Cụ thể, chúng tôi muốn thiết lập `ShiftFirstRowDown` ĐẾN `false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Chúng tôi không muốn dịch chuyển hàng đầu tiên xuống dưới
```

## Bước 6: Nhập DataTable

Bây giờ chúng ta có thể nhập dữ liệu từ `CellsDataTable` vào bài tập.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

Lệnh này sẽ trực tiếp chèn bảng dữ liệu của bạn bắt đầu từ hàng và cột được chỉ định.

## Bước 7: Lưu sổ làm việc

Cuối cùng, chúng ta sẽ lưu bảng tính đã sửa đổi trở lại vào một tệp:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Phần kết luận

Và bạn đã có nó! Bạn đã học cách chèn các hàng DataTable vào một trang tính Excel mà không cần di chuyển hàng đầu tiên bằng cách sử dụng Aspose.Cells cho .NET. Quy trình này không chỉ hợp lý hóa thao tác dữ liệu trong Excel mà còn nâng cao hiệu suất ứng dụng của bạn bằng cách tự động hóa một tác vụ thường cồng kềnh. Với kiến thức này trong bộ công cụ của bạn, bạn được trang bị tốt hơn để xử lý các tác vụ tự động hóa Excel, giúp bạn tiết kiệm thời gian và công sức.

## Câu hỏi thường gặp

### Aspose.Cells dành cho .NET là gì?
Aspose.Cells for .NET là một thư viện lập trình cho phép các nhà phát triển tạo, thao tác và chuyển đổi các tệp Excel trong các ứng dụng .NET.

### Tôi có cần giấy phép để sử dụng Aspose.Cells không?
Có, bạn sẽ cần giấy phép hợp lệ để có đầy đủ tính năng. Tuy nhiên, có bản dùng thử miễn phí để thử nghiệm ban đầu.

### Tôi có thể sử dụng Aspose.Cells trong ứng dụng web không?
Hoàn toàn đúng! Aspose.Cells hoàn hảo cho các ứng dụng trên máy tính để bàn, web và đám mây được phát triển bằng .NET.

### Tôi có thể tạo những loại tệp Excel nào bằng Aspose.Cells?
Bạn có thể tạo nhiều định dạng tệp Excel khác nhau, bao gồm XLSX, XLS, CSV, v.v.

### Tôi có thể nhận hỗ trợ cho Aspose.Cells ở đâu?
Bạn có thể đặt câu hỏi hoặc tìm trợ giúp trong [Diễn đàn Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}