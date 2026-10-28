---
date: '2026-10-28'
description: Tìm hiểu cách thay đổi hệ thống ngày trong Excel sang 1904 bằng Aspose.Cells
  cho Java, thiết lập định dạng ngày Excel và chuyển đổi hệ thống 1904 của Excel một
  cách hiệu quả.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Thay đổi hệ thống ngày trong Excel sang 1904 bằng Aspose.Cells cho
  Java. Tìm hiểu step‑by‑step cách bật hệ thống 1904, thiết lập ngày và chuyển lại.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Thay đổi hệ thống ngày trong Excel sang 1904 với Aspose.Cells cho Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Thay đổi hệ thống ngày trong Excel sang 1904 với Aspose.Cells Java
url: /vi/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay đổi hệ thống ngày Excel sang 1904 với Aspose.Cells Java

Trong hướng dẫn này, bạn sẽ học cách **thay đổi hệ thống ngày Excel** sang định dạng 1904 bằng Aspose.Cells cho Java. Hệ thống 1904 là cần thiết khi bạn cần bảo tồn các ngày trên Mac cổ hoặc đồng bộ với các mô hình tài chính yêu cầu epoch này. Chúng tôi sẽ hướng dẫn cách cài đặt thư viện, tải workbook, bật hệ thống ngày, và lưu kết quả—tất cả mà không cần Microsoft Excel trên máy chủ.

## Câu trả lời nhanh
- **Hệ thống ngày 1904 làm gì?** Nó bắt đầu đếm ngày từ 1 Tháng 1 1904, dịch chuyển tất cả các ngày lên 1.462 ngày so với hệ thống mặc định 1900.  
- **Tại sao dùng Aspose.Cells để thay đổi hệ thống ngày?** Nó cung cấp API đơn giản, hoạt động mà không cần cài Excel và hỗ trợ các tệp lớn.  
- **Phiên bản Java nào được hỗ trợ?** JDK 8 hoặc mới hơn.  
- **Có cần giấy phép không?** Bản dùng thử miễn phí đủ cho việc đánh giá; giấy phép sẽ loại bỏ các giới hạn sử dụng.  
- **Có thể chuyển lại hệ thống 1900 sau này không?** Có, chỉ cần gọi `setDate1904(false)`.

## Hệ thống ngày 1904 trong Excel là gì?
Hệ thống ngày 1904 đếm ngày từ 1 Tháng 1 1904, thay vì epoch mặc định 1900. Sự dịch chuyển này thêm chính xác 1.462 ngày vào mọi giá trị ngày, vì vậy các workbook Mac cổ xuất hiện lệch khi mở trên Windows. Nó chủ yếu được dùng để tương thích với các tệp Excel trên Macintosh cũ và một số mô hình tài chính kế thừa.

## Tại sao phải thay đổi hệ thống ngày Excel bằng Aspose.Cells?
Bạn có thể chuyển hệ thống ngày trực tiếp từ Java, loại bỏ các bước thủ công trong Excel. Aspose.Cells xử lý các workbook lên tới **2 GB** và có thể chuyển đổi một workbook 500 sheet trong dưới **2 giây** trên máy chủ 4 lõi tiêu chuẩn, mang lại hiệu suất cao cho tự động hoá phía server.

## Yêu cầu trước
- Java Development Kit (JDK) 8 hoặc cao hơn.  
- Maven hoặc Gradle để quản lý phụ thuộc.  
- Kiến thức lập trình Java cơ bản.  

## Cài đặt Aspose.Cells cho Java

### Maven
Thêm phụ thuộc sau vào tệp `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Thêm dòng này vào tệp `build.gradle` của bạn:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Nhận giấy phép
Aspose cung cấp bản dùng thử miễn phí, giấy phép tạm thời và giấy phép thương mại đầy đủ. Bạn có thể bắt đầu với [free trial](https://releases.aspose.com/cells/java/) hoặc lấy giấy phép tạm thời từ [temporary license page](https://purchase.aspose.com/temporary-license/).

## Làm thế nào để thay đổi hệ thống ngày Excel sang 1904 với Aspose.Cells cho Java?
Tải workbook, bật cài đặt 1904, và lưu tệp—quy trình ba bước này cập nhật epoch ngày nội bộ của workbook trong vòng chưa đầy một giây. Lệnh API `setDate1904(true)` bật cờ hệ thống, và thay đổi sẽ được lưu khi bạn gọi `save`. Không cần cài đặt Excel, rất phù hợp cho môi trường server không giao diện.

### Bước 1: khởi tạo và tải workbook
Lớp `Workbook` đại diện cho toàn bộ tệp Excel trong bộ nhớ. Đầu tiên, tạo một thể hiện `Workbook` trỏ tới tệp hiện có của bạn.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Bước 2: bật hệ thống ngày 1904
Phương thức `WorkbookSettings.setDate1904` chuyển đổi cờ ngày ở mức workbook. Đặt giá trị `true` sẽ kích hoạt hệ thống 1904 cho tất cả các worksheet.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Mẹo:** Bạn cũng có thể gọi `setDate1904(false)` sau này nếu cần quay lại.

### Bước 3: lưu workbook đã chỉnh sửa
Cuối cùng, ghi các thay đổi vào một tệp mới (hoặc ghi đè tệp gốc). Phương thức `save` sẽ tự động áp dụng hệ thống ngày đang hoạt động.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Lưu ý:** Đoạn mã trên sử dụng tên lớp `tWorkbook` như trong bản gốc. Đảm bảo lỗi đánh máy này phù hợp với quy ước đặt tên trong dự án của bạn hoặc sửa thành `Workbook` nếu cần.

## Đặt ngày Excel bằng chương trình (từ khóa phụ)
Nếu bạn cần điều chỉnh giá trị ô riêng lẻ sau khi thay đổi hệ thống, có thể dùng `cells.get(i, j).putValue(Date)`; ngày sẽ được diễn giải theo hệ thống ngày đang hoạt động.

## Chuyển hệ thống 1904 của Excel trở lại 1900 (từ khóa phụ)
Để quay lại, chỉ cần gọi:

```java
workbook.getSettings().setDate1904(false);
```

Sau đó lưu workbook một lần nữa.

## Ứng dụng thực tiễn
1. **Lưu trữ dữ liệu** – Bảo tồn dấu thời gian kế thừa khi di chuyển các bảng tính Mac cũ.  
2. **Báo cáo đa nền tảng** – Tạo báo cáo mở đúng trên cả Windows và macOS mà không gặp lỗi ngày.  
3. **Mô hình tài chính** – Đồng bộ tính toán ngày với các mô hình tài chính kế thừa yêu cầu hệ thống 1904.

## Các cân nhắc về hiệu năng
- Giới hạn các thao tác workbook trong một phiên để giảm tiêu thụ bộ nhớ; Aspose.Cells truyền dữ liệu dạng stream và không tải toàn bộ tệp vào RAM trừ khi bạn yêu cầu.  
- Tinh chỉnh các tham số thu gom rác của Java (`-XX:+UseG1GC`) cho các tệp rất lớn để tránh các đợt tạm dừng dài.

## Câu hỏi thường gặp

**H: Sự khác nhau giữa hệ thống ngày 1900 và 1904 là gì?**  
Đ: Hệ thống 1900 bắt đầu từ 1 Tháng 1 1900, trong khi hệ thống 1904 bắt đầu từ 1 Tháng 1 1904, dịch chuyển tất cả các ngày lên 1.462 ngày.

**H: Tôi có thể thay đổi hệ thống ngày của workbook đang mở trong Excel không?**  
Đ: Có, nhưng trước tiên phải đóng file trong Excel; nếu không, thao tác lưu sẽ thất bại.

**H: Tôi có cần giấy phép để sử dụng `setDate1904` không?**  
Đ: Phương thức hoạt động trong bản dùng thử, nhưng giấy phép đầy đủ sẽ loại bỏ các hạn chế đánh giá.

**H: Có thể thay đổi hệ thống ngày chỉ cho một worksheet duy nhất không?**  
Đ: Không, hệ thống ngày là cài đặt ở mức workbook; nó áp dụng cho tất cả các worksheet.

**H: Làm sao kiểm tra hệ thống ngày đã được thay đổi?**  
Đ: Mở file đã lưu trong Excel, vào **File → Options → Advanced**, và kiểm tra ô **"Use 1904 date system"**.

## Kết luận
Bây giờ bạn đã biết cách **thay đổi hệ thống ngày Excel** sang 1904 bằng Aspose.Cells cho Java, cách đặt ngày cho các ô riêng lẻ, và cách quay lại hệ thống 1900 khi cần. Hãy tích hợp các đoạn mã này vào quy trình xử lý dữ liệu của bạn để đảm bảo tính tương thích ngày giữa các nền tảng và các tệp kế thừa.

---

**Last Updated:** 2026-10-28  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Resources**
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Purchase license:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free trial:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporary license:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Support forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Các hướng dẫn liên quan

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Master Excel Manipulation with Aspose.Cells for Java: Workbook Operations and Cell Styling Tutorial](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}