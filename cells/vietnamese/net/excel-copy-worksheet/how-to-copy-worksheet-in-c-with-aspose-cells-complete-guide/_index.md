---
category: general
date: 2026-03-30
description: Cách sao chép worksheet trong C# bằng Aspose.Cells – hướng dẫn từng bước
  bao gồm sao chép phạm vi ô, sao chép cột giữa các sheet, sao chép bảng pivot của
  worksheet và thêm mã tạo worksheet mới.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: vi
og_description: Tìm hiểu cách sao chép worksheet trong C# với Aspose.Cells. Hướng
  dẫn này chỉ ra cách sao chép phạm vi ô, bảo tồn bảng pivot, sao chép cột giữa các
  sheet và thêm mã tạo worksheet mới.
og_title: Cách sao chép Worksheet trong C# – Hướng dẫn đầy đủ Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cách sao chép Worksheet trong C# với Aspose.Cells – Hướng dẫn toàn diện
url: /vi/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sao Chép Worksheet trong C# với Aspose.Cells – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách sao chép worksheet** trong C# mà không mất bất kỳ pivot table hay công thức nào chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi cần nhân bản một sheet mà vẫn giữ nguyên mọi thứ. Trong tutorial này, chúng ta sẽ đi qua một giải pháp thực tế, từ đầu đến cuối, không chỉ sao chép dữ liệu mà còn bảo tồn **copy worksheet pivot table**, xử lý **copy cell range**, và hiển thị **add new worksheet code** mà bạn cần.

Chúng ta sẽ bao quát toàn bộ quá trình từ việc tải workbook nguồn tới lưu file đích, để bạn có thể sao chép cột giữa các sheet, bảo tồn các đối tượng, và giữ cho code của mình sạch sẽ. Không có những tham chiếu mơ hồ, chỉ có một ví dụ hoàn chỉnh, có thể chạy ngay trong dự án của bạn.

## Những Điều Tutorial Này Bao Quát

- Tải một file Excel hiện có bằng Aspose.Cells  
- Sử dụng **add new worksheet code** để tạo sheet đích  
- Định nghĩa một **copy cell range** bao gồm pivot table  
- Cấu hình **CopyOptions** để giữ nguyên biểu đồ, công thức và pivot table  
- Thực hiện **copy columns between sheets** với độ chính xác theo hàng  
- Lưu kết quả và xác minh rằng worksheet đã được sao chép đúng cách  

Kết thúc hướng dẫn, bạn sẽ tự tin trả lời câu hỏi “cách sao chép worksheet” dù đang tự động hoá báo cáo hay xây dựng UI dựa trên bảng tính.

---

## Cách Sao Chép Worksheet – Tổng Quan

Trước khi đi vào code, hãy phác thảo luồng công việc ở mức cao. Nghĩ nó như một công thức nấu ăn:

1. **Load** workbook nguồn (`Source.xlsx`).  
2. **Add** một worksheet mới để chứa bản sao (`add new worksheet code`).  
3. **Define** vùng bạn muốn nhân bản (`copy cell range`).  
4. **Configure** các tùy chọn sao chép để pivot table vẫn tồn tại (`copy worksheet pivot table`).  
5. **Copy** các hàng và cột (`copy columns between sheets`).  
6. **Save** workbook mới (`Destination.xlsx`).  

Đó là tất cả—sáu bước, không có phép màu. Mỗi bước sẽ được giải thích dưới đây kèm theo đoạn code và lý do thực hiện.

---

## Bước 1 – Tải Workbook Nguồn

Điều đầu tiên cần làm: tạo một thể hiện `Workbook` trỏ tới file bạn muốn sao chép. Bước này quan trọng vì Aspose.Cells làm việc trực tiếp với hệ thống file, không phải giao diện Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Lý do quan trọng:* Việc tải file tạo ra một biểu diễn trong bộ nhớ của mọi sheet, ô và đối tượng. Nếu không có bước này, sẽ không có gì để sao chép và bất kỳ cố gắng `add new worksheet code` nào sau này sẽ thất bại vì dữ liệu nguồn không tồn tại.

---

## Bước 2 – Thêm Worksheet Mới (add new worksheet code)

Bây giờ chúng ta cần một nơi để dán dữ liệu đã sao chép. Đây là lúc **add new worksheet code** tỏa sáng. Bạn có thể đặt tên sheet tùy ý; ở đây chúng ta gọi nó là `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Mẹo chuyên nghiệp:* Nếu bạn dự định sao chép nhiều sheet, hãy gọi `Worksheets.Add` trong một vòng lặp và đặt tên duy nhất cho mỗi sheet. Như vậy bạn tránh được xung đột tên và giữ workbook gọn gàng.

---

## Bước 3 – Định Nghĩa Copy Cell Range

Một **copy cell range** cho Aspose.Cells biết chính xác những hàng và cột nào cần nhân bản. Trong nhiều trường hợp thực tế, phạm vi này bao gồm một pivot table, vì vậy chúng ta phải rất chính xác.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Tại sao cần bước này:* Bằng cách chỉ định rõ phạm vi, bạn tránh việc sao chép toàn bộ sheet (điều này có thể lãng phí) và đảm bảo pivot table nằm trong khu vực đã sao chép. Đây là cốt lõi của **how to copy worksheet** khi bạn chỉ cần một phần của sheet.

---

## Bước 4 – Cài Đặt Copy Options (preserve copy worksheet pivot table)

Aspose.Cells cung cấp một đối tượng `CopyOptions` để kiểm soát những gì sẽ được dán. Để giữ pivot table, biểu đồ và công thức, chúng ta đặt `PasteType.All` và bật `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Giải thích:* `PasteType.All` là tùy chọn bao quát nhất, trong khi `PasteSpecial` yêu cầu engine xử lý đúng các đối tượng phức tạp—như pivot table. Bỏ qua bước này là một sai lầm phổ biến; sheet sao chép sẽ mất các tính năng tương tác.

---

## Bước 5 – Sao Chép Hàng và Cột (copy columns between sheets)

Tiếp theo là công việc nặng: thực sự di chuyển dữ liệu. Chúng ta sẽ dùng `CopyRows` và `CopyColumns` để thực hiện **copy columns between sheets**. Thực hiện cả hai đảm bảo rằng các ô hợp nhất và độ rộng cột được bảo tồn.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Điều đang xảy ra:* `CopyRows` di chuyển dữ liệu theo hàng, trong khi `CopyColumns` làm tương tự theo cột. Chạy cả hai đảm bảo khối hình chữ nhật đầy đủ được sao chép, điều này rất quan trọng khi bạn cần **copy columns between sheets** có độ rộng cột khác nhau hoặc có cột ẩn.

---

## Bước 6 – Lưu Workbook

Cuối cùng, ghi các thay đổi ra đĩa. Bước này hoàn thiện quy trình **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Mẹo kiểm tra:* Mở `Destination.xlsx` và xác nhận rằng sheet `"Copy"` trông giống hệt bản gốc, pivot table hoạt động, và độ rộng cột khớp. Nếu có gì không ổn, hãy xem lại cài đặt `CopyOptions`.

---

## Các Trường Hợp Đặc Biệt & Biến Thể Thông Thường

### Sao Chép Nhiều Worksheet

Nếu cần nhân bản nhiều sheet, hãy bao bọc logic trên trong một vòng `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Bảo Tồn Công Thức Khi Đổi Workbook

Khi workbook nguồn và đích có các named range khác nhau, đặt `copyOptions` thành `PasteType.Formulas` cộng với `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Phạm Vi Lớn và Hiệu Suất

Đối với dữ liệu khổng lồ (hàng hàng trăm ngàn), cân nhắc chỉ dùng `CopyRows` và bỏ qua `CopyColumns` nếu độ rộng cột không quan trọng. Điều này có thể tiết kiệm vài giây.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy, thể hiện mọi gì chúng ta đã thảo luận. Dán vào một console app, điều chỉnh đường dẫn file, và nhấn **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Kết quả mong đợi:** Mở `Destination.xlsx` sẽ hiển thị một sheet tên **Copy** phản chiếu sheet đầu tiên của `Source.xlsx`—bao gồm mọi pivot table, định dạng và độ rộng cột. File gốc vẫn không bị thay đổi.

---

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với file .xlsx được tạo bằng Excel 2019 không?**  
A: Hoàn toàn có. Aspose.Cells hỗ trợ tất cả các định dạng Excel hiện đại, vì vậy cùng một đoạn code hoạt động cho `.xlsx`, `.xlsm`, và thậm chí các file `.xls` cũ hơn.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}