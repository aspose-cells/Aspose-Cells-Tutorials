---
category: general
date: 2026-05-30
description: Thay đổi kích thước phông chữ của textbox trong Excel bằng C#. Tìm hiểu
  cách chỉnh sửa phông chữ textbox trong Excel nhanh chóng với mã hướng dẫn từng bước.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: vi
og_description: Thay đổi kích thước phông chữ của textbox trong Excel bằng C#. Hướng
  dẫn này cho thấy cách chỉnh sửa phông chữ textbox trong Excel một cách an toàn và
  hiệu quả.
og_title: Thay đổi kích thước phông chữ của Textbox trong Excel bằng C# – Hướng dẫn
  đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Thay đổi kích thước phông chữ của hộp văn bản trong Excel bằng C# – Hướng dẫn
  toàn diện
url: /vi/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay Đổi Kích Thước Phông Chữ của Hộp Văn Bản trong Excel bằng C# – Hướng Dẫn Đầy Đủ

Cần **thay đổi kích thước phông chữ của hộp văn bản** trong một worksheet Excel bằng C#? Bạn đang ở đúng nơi. Dù bạn đang tạo báo cáo, xây dựng bảng điều khiển, hay chỉ điều chỉnh một mẫu, việc thay đổi giao diện của hộp văn bản có thể làm cho bảng tính của bạn trông chuyên nghiệp hơn rất nhiều.

Trong hướng dẫn này, chúng ta sẽ **sửa đổi phông chữ hộp văn bản trong Excel** không chỉ giới hạn ở kích thước—cũng bao gồm họ phông, độ đậm và thậm chí xử lý nhiều hình dạng. Khi hoàn thành, bạn sẽ có một đoạn mã sẵn sàng chạy, bao quát mọi khía cạnh của quá trình, từ mở workbook đến dọn dẹp các đối tượng COM. Không có phần thừa, chỉ có mã thực tế mà bạn có thể đưa vào dự án ngay hôm nay.

## Yêu Cầu Trước — Bạn Cần Gì

Trước khi bắt đầu, hãy chắc chắn rằng máy của bạn đã có các thành phần sau:

| Yêu Cầu | Lý do quan trọng |
|-------------|----------------|
| **.NET 6+** (hoặc .NET Framework 4.7.2+) | Cung cấp trình biên dịch và môi trường chạy C#. |
| **Microsoft.Office.Interop.Excel** NuGet package | Cung cấp các kiểu interop COM cần thiết để giao tiếp với Excel. |
| **Excel installed** (any recent version) | Lớp Interop chỉ hoạt động khi ứng dụng Office có sẵn. |
| **Basic C# knowledge** | Bạn sẽ dễ dàng theo dõi, nhưng chúng tôi sẽ giải thích từng dòng. |

Nếu bất kỳ mục nào còn thiếu, hãy tạm dừng và cài đặt chúng; phần còn lại của hướng dẫn giả định rằng chúng đã sẵn sàng.

## Bước 1: Thiết Lập Dự Án và Nhập Các Namespace

First things first—create a new console app (or integrate into an existing one) and pull in the interop namespace.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Mẹo:** Nếu bạn đang nhắm tới .NET 6+, thêm gói `Microsoft.Office.Interop.Excel` bằng lệnh `dotnet add package Microsoft.Office.Interop.Excel`. Điều này đảm bảo bí danh `Excel` được giải quyết đúng.

## Bước 2: Mở Workbook và Lấy Worksheet Mục Tiêu

Now we need to launch Excel, open the file, and point to the sheet that holds the textbox. Wrapping this in a `try/finally` block guarantees the COM objects get released even if something goes wrong.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Tại sao điều này quan trọng

Opening the workbook via COM gives us a live object model—meaning any change we make reflects instantly in the file. Setting `Visible = false` speeds things up and avoids popping windows during automation.

## Bước 3: Lấy Đối Tượng Shape của Hộp Văn Bản

Excel treats textboxes as `Shape` objects under the `Shapes` collection, not as a dedicated `TextBox` collection. That’s why the code below looks a bit different from the snippet you may have seen online.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Cảnh báo:** The `Shapes` collection is 1‑based, so we add `+1` to the zero‑based `textboxIndex` you pass in. Forgetting this leads to “index out of range” errors that can be frustrating to debug.

## Bước 4: Thay Đổi Kích Thước Phông Chữ (và Tên) của Hộp Văn Bản

Here’s where we finally **change textbox font size**. The `TextFrame2` property gives us access to the rich‑text formatting options, which include `Font.Name` and `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Tại sao chúng ta dùng `TextFrame2`

`TextFrame2` is the newer object model introduced with Office 2007. It supports advanced typographic features and is generally more reliable than the older `TextFrame`. Using it ensures our **change textbox font size** operation works across modern Excel versions.

## Bước 5: Lưu, Dọn Dẹp và Kiểm Tra

After tweaking the font, we need to persist the changes and release every COM reference. Skipping cleanup can leave orphaned Excel processes lingering in the background.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Mẹo:** Nếu bạn cần **modify excel textbox font** trên nhiều worksheet, hãy bao bọc logic bên trong bằng một vòng lặp duyệt `Workbook.Worksheets`. Chỉ cần nhớ đặt lại `textboxIndex` cho mỗi sheet.

## Xử Lý Các Trường Hợp Đặc Biệt — Nhiều Hộp Văn Bản và Thiếu Shape

Real‑world spreadsheets rarely contain just one textbox. Below are two quick strategies you can adopt without rewriting the whole method.

### 1. Thay đổi *tất cả* các hộp văn bản trên một sheet

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Xác định hộp văn bản bằng **Tên** thay vì chỉ mục

If you gave your textbox a meaningful name (e.g., “TitleBox”), you can fetch it directly:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Both approaches let you **modify excel textbox font** with precision, no matter how the workbook is structured.

## Tổng Quan Hình Ảnh (Tùy Chọn)

If you prefer a quick visual cue, imagine the following diagram:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Alt text:* *thay đổi kích thước phông chữ hộp văn bản trong Excel – hộp văn bản được đánh dấu sẵn sàng cho việc chỉnh sửa phông.*

## Ví Dụ Hoàn Chỉnh Hoạt Động

Putting everything together, here’s a single file you can copy‑paste into a console project and run immediately (just update the file path and sheet name).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Bạn Nên Học Gì Tiếp Theo?

- [Thay đổi kích thước phông chữ trong Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Cách tùy chỉnh kích thước phông chữ trong ô Excel bằng Aspose.Cells .NET | Hướng dẫn đầy đủ](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Cách đặt kiểu phông chữ trong Excel bằng Aspose.Cells cho .NET (Hướng dẫn từng bước)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}