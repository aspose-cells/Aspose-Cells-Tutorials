---
category: general
date: 2026-08-14
description: Nhúng phông chữ trong SVG khi xuất Excel sang SVG bằng Aspose.Cells.
  Tìm hiểu cách đặt vùng in, thiết lập tùy chọn in và sử dụng hàm WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: vi
lastmod: 2026-08-14
og_description: Nhúng phông chữ vào SVG khi xuất Excel sang SVG bằng Aspose.Cells.
  Hướng dẫn này chỉ cho bạn cách thiết lập khu vực in, cấu hình tùy chọn in và áp
  dụng hàm WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Nhúng phông chữ vào SVG khi xuất Excel sang SVG – từng bước
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Nhúng phông chữ vào SVG khi xuất Excel sang SVG
url: /vi/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhúng phông chữ vào SVG khi xuất Excel sang SVG

Nếu bạn cần **nhúng phông chữ vào SVG khi xuất Excel sang SVG**, hướng dẫn này sẽ chỉ cho bạn cách thực hiện chính xác bằng Aspose.Cells for Java. Chúng tôi cũng sẽ đề cập đến cách **đặt vùng in**, **đặt tùy chọn in**, và **sử dụng hàm WRAPCOLS** để định dạng dữ liệu mà không làm mất bố cục.

Bạn sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, tải một workbook hiện có, áp dụng công thức `WRAPCOLS`, cấu hình các tùy chọn ảnh đặc thù cho SVG, định nghĩa vùng in, và cuối cùng lưu file dưới dạng SVG với phông chữ được nhúng. Không cần tài liệu bên ngoài—chỉ cần sao chép mã, chạy nó, và kiểm tra SVG kết quả.

## Nhúng phông chữ vào SVG – cấu hình ImageOrPrintOptions

Việc nhúng phông chữ đảm bảo rằng SVG hiển thị chính xác như trong Excel, ngay cả trên các máy không có phông chữ gốc được cài đặt.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Tại sao điều này quan trọng*: Khi `setEmbedFonts(true)` được bật, Aspose.Cells ghi dữ liệu phông chữ trực tiếp vào phần `<defs>` của SVG. Kết quả là một file tự chứa, trông giống hệt trên mọi trình duyệt và nền tảng.

## Xuất Excel sang SVG – quy trình đầy đủ

Các bước sau minh họa quá trình từ đầu đến cuối, từ việc tải workbook đến lưu file SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Kết quả mong đợi**: `output.svg` xuất hiện trong `YOUR_DIRECTORY`. Mở nó trong trình duyệt sẽ hiển thị worksheet với mọi phông chữ đã được nhúng, dữ liệu được gói thành ba cột (nhờ `WRAPCOLS`), và chỉ các ô trong `A1:H30` được hiển thị.

## Đặt vùng in cho worksheet

Xác định vùng in giới hạn SVG xuất ra một phạm vi cụ thể, giảm kích thước file và tập trung người xem vào dữ liệu liên quan.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Mẹo*: Phạm vi tuân theo ký hiệu A1 của Excel. Nếu bạn cần một phạm vi động, có thể tính toán nó bằng mã với `ws.getCells().getMaxDisplayRange()`.

## Đặt tùy chọn in cho đầu ra SVG

Các tùy chọn in kiểm soát cách Aspose.Cells chuyển đổi worksheet thành ảnh. Ngoài việc nhúng phông chữ, bạn có thể điều chỉnh độ phân giải, tỉ lệ phóng đại và bố cục trang.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Tại sao bạn nên đặt tùy chọn in*: Nếu không chỉ định rõ, Aspose.Cells sẽ dùng các giá trị mặc định có thể bỏ qua việc nhúng phông chữ hoặc áp dụng tỉ lệ phóng đại không mong muốn, dẫn đến SVG mờ hoặc định dạng sai.

## Sử dụng hàm WRAPCOLS để gói dữ liệu cột

`WRAPCOLS` là công thức Excel phân phối một dải dọc thành một số cột xác định. Thực tế hữu ích khi bạn muốn hiển thị một danh sách dài trong một lưới gọn gàng.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Khi workbook được lưu, Aspose.Cells sẽ tính toán công thức, tạo ra bố cục ba cột bên trong vùng in đã định. Kỹ thuật này hoạt động với bất kỳ dải dữ liệu nào—chỉ cần điều chỉnh đối số thứ hai thành số cột mong muốn.

## Ví dụ đầy đủ có thể chạy

Dưới đây là chương trình Java hoàn chỉnh mà bạn có thể dán vào bất kỳ IDE nào. Đảm bảo đã thêm thư viện Aspose.Cells for Java vào classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Các bước xác minh**

1. Chạy chương trình.  
2. Mở `output.svg` trong trình duyệt web.  
3. Xác nhận rằng văn bản sử dụng cùng phông chữ như file Excel gốc (phông chữ đã được nhúng).  
4. Kiểm tra rằng chỉ các ô trong `A1:H30` xuất hiện và dữ liệu từ `A2:A10` được hiển thị trong ba cột.

## Những vấn đề thường gặp và cách tránh chúng

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| Phông chữ bị thiếu trong SVG | `setEmbedFonts(false)` hoặc file phông không truy cập được | Đảm bảo `setEmbedFonts(true)` và phông chữ đã được cài đặt trên máy chạy mã |
| WRAPCOLS không tính toán | Engine tính toán bị tắt | Gọi `workbook.calculateFormula()` trước khi xuất, hoặc để Aspose.Cells tự tính trong quá trình lưu |
| SVG xuất ra rỗng | Vùng in không bao gồm dữ liệu nào | Kiểm tra lại phạm vi truyền vào `setPrintArea` |
| File SVG quá lớn | Không áp dụng tỉ lệ, độ phân giải ảnh cao | Điều chỉnh `imgOptions.setResolution(96)` hoặc giá trị tương tự để kiểm soát DPI |

## Mẹo chuyên nghiệp: tái sử dụng ImageOrPrintOptions cho nhiều worksheet

Nếu workbook của bạn có nhiều sheet cần cùng thiết lập SVG, hãy tạo một thể hiện `ImageOrPrintOptions` duy nhất và gán nó cho `PageSetup` của mỗi worksheet. Điều này giảm tiêu thụ bộ nhớ và đảm bảo việc nhúng phông chữ nhất quán cho tất cả các file xuất.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Các bước tiếp theo

* **Xuất sang các định dạng vector khác** – Thay `ImageFormat.SVG` bằng `ImageFormat.PDF` để tạo PDF chất lượng cao.  
* **Xử lý hàng loạt** – Duyệt qua một thư mục chứa các file `.xlsx` và tự động tạo SVG.  
* **Xử lý phông chữ tùy chỉnh** – Sử dụng `FontSettings` để tải phông từ thư mục cụ thể khi hệ thống không có đủ phông cần thiết.  

Bằng cách thành thạo **nhúng phông chữ vào SVG**, **xuất excel sang svg**, **đặt vùng in**, **đặt tùy chọn in**, và **sử dụng hàm WRAPCOLS**, bạn có thể tự động tạo SVG độ chính xác cao cho báo cáo, bảng điều khiển và trực quan hoá web trực tiếp từ dữ liệu Excel. Chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Đặt Vùng In trong Excel Sử dụng Aspose.Cells cho .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}