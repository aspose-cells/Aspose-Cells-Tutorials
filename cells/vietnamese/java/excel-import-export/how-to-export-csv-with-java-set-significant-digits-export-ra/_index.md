---
category: general
date: 2026-03-01
description: Tìm hiểu cách xuất csv từ một workbook Java đồng thời thiết lập chữ số
  có ý nghĩa và phạm vi xuất sang csv trong một hướng dẫn duy nhất, rõ ràng.
draft: false
keywords:
- how to export csv
- set significant digits
- export range to csv
- Java workbook export
- CSV formatting Java
language: vi
og_description: Nắm vững cách xuất CSV trong Java, thiết lập chữ số có nghĩa và xuất
  phạm vi ra CSV với mã thực tế và các mẹo hữu ích.
og_title: Cách xuất CSV bằng Java – Hướng dẫn chi tiết từng bước
tags:
- Java
- Aspose.Cells
- CSV
- Data Export
title: Cách xuất CSV bằng Java – Đặt số chữ số có nghĩa & Xuất phạm vi sang CSV
url: /vi/java/excel-import-export/how-to-export-csv-with-java-set-significant-digits-export-ra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách xuất CSV bằng Java – Đặt chữ số có nghĩa & Xuất phạm vi sang CSV

Bạn đã bao giờ tự hỏi **cách xuất csv** từ một workbook Java mà không mất độ chính xác số học chưa? Có thể bạn đã thử nhanh `toString()` và gặp rắc rối với lỗi làm tròn. Đó là một vấn đề phổ biến, đặc biệt khi bạn cần **đặt chữ số có nghĩa** cho dữ liệu tài chính hoặc kết quả khoa học.  

Trong tutorial này bạn sẽ thấy một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy **cách xuất csv**, cách **đặt chữ số có nghĩa**, và thậm chí cách **xuất phạm vi sang csv** trong khi giữ dữ liệu gọn gàng. Chúng tôi sẽ đi qua từng dòng, giải thích *tại sao* phía sau các lời gọi API, và đưa ra các mẹo để tránh những bẫy thường gặp. Không cần tài liệu bổ sung—chỉ một giải pháp tự chứa mà bạn có thể sao chép‑dán ngay hôm nay.

## Những gì bạn sẽ học

- Tạo một workbook và cấu hình độ chính xác số học bằng `setNumberSignificantDigits`.
- Xuất một phạm vi ô cụ thể dưới dạng chuỗi CSV được định dạng đẹp.
- Phân tích ngày theo thời đại Nhật Bản bằng `DateTimeFormatInfo`.
- Tính lại công thức để kết quả mảng động luôn cập nhật.
- Kết xuất một bảng pivot thành ảnh PNG.
- Sử dụng Smart Marker để chèn bình luận và cuối cùng lưu workbook.

Tất cả những điều này được thực hiện bằng thư viện Aspose.Cells for Java, phiên bản 23.12 (mới nhất tại thời điểm viết). Nếu bạn đã có JAR trong classpath, bạn đã sẵn sàng.

---

## Bước 1: Tạo một Workbook và **Đặt chữ số có nghĩa**

Trước khi chúng ta có thể xuất bất kỳ dữ liệu nào, chúng ta cần một đối tượng workbook. Điều đầu tiên mà nhiều nhà phát triển thường bỏ qua là độ chính xác số học. Theo mặc định Aspose.Cells sử dụng độ chính xác double đầy đủ, điều này có thể dẫn đến các chuỗi dài, khó xử lý trong CSV. Đặt số chữ số có nghĩa sẽ cắt ngắn đầu ra trong khi vẫn giữ lại các con số quan trọng nhất.

```java
import com.aspose.cells.*;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {

        // Step 1 – initialise workbook and limit numeric values to 5 significant digits
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        // This is the key call that **set significant digits** for all numeric cells
        settings.setNumberSignificantDigits(5);
```

**Tại sao điều này lại quan trọng?**  
Nếu bạn xuất một ô chứa `12345.6789` mà không giới hạn chữ số, CSV sẽ hiển thị giá trị đầy đủ, làm rối mắt báo cáo. Với `setNumberSignificantDigits(5)`, cùng một ô sẽ trở thành `12346`, thường là những gì người dùng doanh nghiệp mong đợi.

> **Mẹo chuyên nghiệp:** Nếu bạn cần độ chính xác khác nhau cho từng cột, bạn có thể áp dụng một `Style` tùy chỉnh thay vì cài đặt toàn cục.

---

## Bước 2: **Xuất phạm vi sang CSV** – Định dạng quan trọng

Bây giờ workbook đã sẵn sàng, hãy lấy một khối dữ liệu hình chữ nhật và chuyển nó thành chuỗi CSV. Chúng ta cũng sẽ áp dụng định dạng hai chữ số thập phân (`0.00`) để mọi số đều căn chỉnh đẹp mắt.

```java
        // Step 2 – define export options and pull the range B2:D10 as CSV
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // we want a string, not a file yet
        exportOptions.setNumberFormat("0.00");          // enforce two decimal places

        // Create a dummy range with some sample data for illustration
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // ... populate more rows as needed ...

        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);
```

Lời gọi `exportDataTable` thực hiện phần việc nặng. Vì chúng ta đã đặt `exportAsString`, phương thức trả về một `String` mà chúng ta có thể in ra, ghi vào file, hoặc gửi qua HTTP. Bước **export range to csv** cũng tuân theo cài đặt toàn cục `setNumberSignificantDigits` mà chúng ta đã định nghĩa trước, vì vậy các số vừa được làm tròn tới năm chữ số có nghĩa *và* hiển thị với hai chữ số thập phân.

**Kết quả mong đợi (được cắt ngắn):**

```
=== CSV Output ===
123.46,78.90,0.12
...
```

> **Câu hỏi thường gặp:** *Nếu tôi cần một dấu phân cách khác, chẳng hạn như dấu chấm phẩy?*  
> Chỉ cần gọi `exportOptions.setSeparator(";")` trước khi xuất.

---

## Bước 3: Phân tích ngày theo thời đại Nhật Bản (Tiện ích Bonus)

Mặc dù không liên quan trực tiếp đến CSV, nhiều bảng Excel chứa ngày định dạng theo địa phương. Dưới đây là cách bạn có thể chuyển một chuỗi thời đại Nhật Bản như `"R3/04/01"` thành một đối tượng `DateTime` chuẩn.

```java
        // Step 3 – parse Japanese era date (Reiwa 3)
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);
```

Kết quả:

```
Parsed Japanese date: 2021-04-01T00:00:00
```

**Tại sao lại đưa mục này vào?**  
Nếu việc xuất CSV của bạn cung cấp dữ liệu cho các hệ thống hạ nguồn yêu cầu ngày ở định dạng ISO‑8601, bạn sẽ cần chuẩn hoá bất kỳ định dạng địa phương nào trước. Đoạn mã này cho thấy *cách* và *tại sao* trong một nơi duy nhất.

---

## Bước 4: Tính lại công thức – Giữ kết quả mảng động luôn mới

Nếu workbook của bạn chứa công thức (ví dụ, `=SUM(A1:A10)`), chúng sẽ không tự động cập nhật sau khi chúng ta thay đổi cài đặt. Gọi `calculateFormula` buộc thực hiện tính toán lại toàn bộ, đảm bảo CSV xuất ra phản ánh các giá trị mới nhất.

```java
        // Step 4 – recalculate all formulas
        workbook.calculateFormula();
```

> **Cảnh báo:** Các workbook lớn có thể mất thời gian đáng kể để tính lại. Đối với các kịch bản yêu cầu hiệu năng cao, hãy xem xét `calculateFormula(FormulaCalculationOptions)` để giới hạn phạm vi tính toán.

---

## Bước 5: Kết xuất Pivot Table đầu tiên thành ảnh PNG

Đôi khi bạn cần một ảnh chụp nhanh của pivot table cùng với CSV. Đoạn mã dưới đây kết xuất pivot table đầu tiên trên worksheet đầu tiên thành một file PNG.

```java
        // Step 5 – render pivot table as PNG
        PivotTable pivot = sheet.getPivotTables().get(0); // assumes a pivot exists
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.Png);
        // The range that the pivot occupies is turned into an image
        pivot.getRange().toImage("output/pivot.png", imgOptions);
```

**Mẹo:** Nếu workbook chưa có pivot, bạn có thể tạo một pivot một cách lập trình—xem tài liệu Aspose.Cells để có ví dụ nhanh.

---

## Bước 6: Sử dụng Smart Marker để ghi chú và lưu Workbook

Smart Marker cho phép bạn chèn nội dung động vào các ô bằng các placeholder đơn giản. Ở đây chúng ta ghi một bình luận như “Reviewed by QA” vào một ô được chỉ định và sau đó lưu workbook.

```java
        // Step 6 – apply Smart Marker comment
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", java.util.Collections.singletonMap("Comment", "Reviewed by QA"));

        // Finally, save the workbook with the comment embedded
        workbook.save("output/commented.xlsx");
    }
}
```

Placeholder `${Comment}` có thể được đặt ở bất kỳ vị trí nào trong sheet (ví dụ, ô `A1`). Khi `apply` chạy, placeholder sẽ được thay thế bằng giá trị đã cung cấp.

**Kết quả:** Bạn sẽ tìm thấy file `output/commented.xlsx` chứa bình luận, cùng với `pivot.png` đã tạo trước đó và chuỗi CSV được in ra console.

---

## Ví dụ đầy đủ hoạt động

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh mà bạn có thể biên dịch và chạy:

```java
import com.aspose.cells.*;
import java.util.Collections;
import java.util.Locale;

public class CsvExportDemo {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Workbook & Significant Digits -----------
        Workbook workbook = new Workbook();
        WorkbookSettings settings = workbook.getSettings();
        settings.setNumberSignificantDigits(5); // **set significant digits**

        // ----------- Step 2: Populate Sample Data & Export CSV ----------
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
        cells.get("B2").putValue(123.456);
        cells.get("C2").putValue(78.9);
        cells.get("D2").putValue(0.12345);
        // (Add more rows if you like)

        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("0.00");
        Range dataRange = cells.createRange("B2:D10");
        String csvData = dataRange.exportDataTable(exportOptions).toString();

        System.out.println("=== CSV Output ===");
        System.out.println(csvData);

        // ----------- Step 3: Japanese Era Date ----------
        DateTime japaneseDate = DateTime.parse("R3/04/01", new DateTimeFormatInfo(Locale.JAPAN));
        System.out.println("Parsed Japanese date: " + japaneseDate);

        // ----------- Step 4: Recalculate Formulas ----------
        workbook.calculateFormula();

        // ----------- Step 5: Render Pivot Table ----------
        if (!sheet.getPivotTables().isEmpty()) {
            PivotTable pivot = sheet.getPivotTables().get(0);
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.Png);
            pivot.getRange().toImage("output/pivot.png", imgOptions);
        }

        // ----------- Step 6: Smart Marker Comment ----------
        SmartMarkerProcessor smartMarker = new SmartMarkerProcessor(workbook);
        smartMarker.apply("${Comment}", Collections.singletonMap("Comment", "Reviewed by QA"));
        workbook.save("output/commented.xlsx");
    }
}
```

### Kết quả mong đợi trên Console

```
=== CSV Output ===
123.46,78.90,0.12
...
Parsed Japanese date: 2021-04-01T00:00:00
```

Bạn cũng sẽ tìm thấy `output/pivot.png` (nếu có pivot) và `output/commented.xlsx` trên đĩa.

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

- **Tôi có thể xuất trực tiếp ra file CSV vật lý không?**  
  Có. Thay thế khối `exportAsString` bằng `dataRange.exportDataTable("output/data.csv", exportOptions);`.

- **Nếu sheet của tôi sử dụng một locale khác cho các số thì sao?**  
  Đặt `exportOptions.setCultureInfo(new CultureInfo("fr-FR"))` trước khi xuất; điều này sẽ hoán đổi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}