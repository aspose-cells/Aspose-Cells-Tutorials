---
category: general
date: 2026-10-10
description: Học cách sử dụng hàm expand khi đọc và ghi tệp Excel trong Java. Hướng
  dẫn từng bước với mã đầy đủ và giải thích.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: vi
lastmod: 2026-10-10
og_description: Cách sử dụng hàm expand khi đọc và ghi tệp Excel trong Java. Theo
  dõi hướng dẫn đầy đủ này để thêm các phạm vi động với Aspose.Cells.
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: Cách sử dụng hàm expand trong xử lý Excel bằng Java – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: Cách sử dụng hàm expand trong xử lý Excel bằng Java
url: /vi/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng hàm EXPAND trong xử lý Excel bằng Java

Nếu bạn cần **cách sử dụng hàm EXPAND** khi làm việc với các tệp Excel trong Java, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Khi kết thúc tutorial, bạn sẽ có thể đọc và ghi tệp Excel trong các dự án Java mà động mở rộng phạm vi ô bằng công thức `EXPAND`.

Làm việc với bảng tính Excel thường đồng nghĩa với việc xử lý các công thức thích ứng với kích thước dữ liệu thay đổi. Hàm `EXPAND`, được giới thiệu trong các phiên bản Excel gần đây, cho phép bạn mở rộng một tham chiếu theo số hàng và cột xác định. Khi kết hợp với một thư viện Java mạnh mẽ, bạn có thể tự động hoá hành vi này mà không rời khỏi môi trường code của mình.

Trong tutorial này, bạn sẽ:

* Tải một workbook hiện có (`read and write excel file java` scenario)  
* Áp dụng công thức `EXPAND` vào một ô  
* Tính lại các công thức để giá trị mới xuất hiện  
* Lưu workbook đã cập nhật  

## Yêu cầu trước

* Java 17 hoặc mới hơn đã được cài đặt  
* Maven hoặc Gradle để quản lý phụ thuộc  
* Aspose.Cells for Java (thư viện cung cấp `Workbook`, `Worksheet`, …)  

> **Mẹo chuyên nghiệp:** Aspose.Cells hỗ trợ cả định dạng `.xlsx` và `.xls` và không yêu cầu Microsoft Office trên máy chủ.

## Những gì bạn cần

| Mục | Lý do |
|------|--------|
| JDK 17+ | Các tính năng ngôn ngữ hiện đại và hiệu năng tốt hơn |
| Maven/Gradle | Dễ dàng đưa thư viện vào dự án |
| Aspose.Cells for Java | Cung cấp `Workbook`, `Worksheet` và engine công thức |
| Một tệp Excel (`input.xlsx`) | Workbook nguồn để minh họa hàm `EXPAND` |

Thêm Aspose.Cells vào dự án bằng Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Hoặc bằng Gradle:

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## Bước 1: Tải workbook (cách sử dụng hàm EXPAND – khởi tạo)

Hoạt động đầu tiên là mở tệp Excel bạn muốn chỉnh sửa. `Workbook` đại diện cho toàn bộ tệp trong bộ nhớ.

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**Tại sao lại quan trọng:** Việc tải workbook cho phép bạn truy cập tất cả các worksheet, ô và engine công thức nội bộ. Nếu không có workbook đã tải, bạn không thể đọc hay ghi dữ liệu Excel trong Java.

## Bước 2: Truy cập worksheet mục tiêu

Hầu hết các workbook chứa nhiều sheet; ví dụ này sử dụng sheet đầu tiên (chỉ mục 0). Bạn cũng có thể lấy sheet theo tên.

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Giải thích:** Các đối tượng `Worksheet` cung cấp bộ sưu tập `Cells`, nơi bạn đặt công thức. Nếu muốn hướng tới một sheet khác, thay đổi chỉ mục hoặc gọi `get("SheetName")`.

## Bước 3: Đặt công thức EXPAND (cách sử dụng hàm EXPAND trong thực tế)

Bây giờ chúng ta ghi công thức `EXPAND` vào ô **B1**. Công thức sẽ mở rộng tham chiếu `A1` lên **5 hàng** và **1 cột**, tạo ra phạm vi `A1:A6` được dịch sang phải một cột.

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**Tại sao lại hoạt động:** `setFormula` lưu chuỗi công thức; Aspose.Cells không đánh giá ngay lập tức. Hàm `EXPAND` sẽ được tính khi chúng ta kích hoạt một lượt tính toán.

## Bước 4: Tính lại công thức (hoàn thiện hàm EXPAND)

Sau khi chèn công thức, yêu cầu workbook tính lại tất cả các ô phụ thuộc. Bước này đảm bảo giá trị mới xuất hiện trong worksheet.

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**Đi gì phía sau:** Engine tính toán phân tích biểu thức `EXPAND`, xác định phạm vi mới và ghi mảng giá trị kết quả trở lại sheet. Nếu `A1` chứa một số, phạm vi mở rộng sẽ lặp lại số đó trong các ô mới.

## Bước 5: Lưu workbook đã cập nhật

Cuối cùng, ghi workbook đã sửa lại vào đĩa (hoặc vào một luồng output). Điều này hoàn thành chu trình **read and write excel file java**.

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Chạy chương trình sẽ tạo ra `output.xlsx` trong đó ô **B1** bây giờ chứa một spill range phản ánh giá trị của `A1` trên năm hàng và một cột. Mở tệp trong Excel để xem mảng động hoạt động.

### Kết quả mong đợi

Giả sử `A1` ban đầu chứa số `42`, các ô kết quả sẽ là:

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

Nếu `A1` chứa chuỗi văn bản, cùng một chuỗi sẽ spill ra toàn bộ phạm vi mở rộng.

## Các biến thể phổ biến và trường hợp góc cạnh

| Kịch bản | Điều chỉnh |
|----------|------------|
| **Ô bắt đầu khác** | Thay `"B1"` bằng bất kỳ địa chỉ nào, ví dụ `"C3"` |
| **Chỉ mở rộng theo cột** | Dùng `=EXPAND(A1,0,3)` để mở rộng ba cột |
| **Số hàng động** | Thay `5` tĩnh bằng một tham chiếu ô như `D1` chứa số hàng mong muốn |
| **Sử dụng tên vùng** | Thay `A1` bằng tên đã định nghĩa, ví dụ `=EXPAND(MyRange,5,1)` |
| **Lỗi công thức** | Đảm bảo workbook được lưu ở định dạng hỗ trợ mảng động (`.xlsx`). Các tệp `.xls` cũ sẽ cắt bớt spill. |

### Xử lý bảng tính lớn

Khi làm việc với workbook rất lớn, gọi `workbook.calculateFormula(CalcOptions)` với một đối tượng `CalcOptions` tùy chỉnh để giới hạn bộ nhớ hoặc bật tính toán đa luồng.

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## Mã nguồn đầy đủ (sẵn sàng sao chép)

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Lưu ý:** Thay `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối tới các tệp Excel của bạn. Mã này chạy trên bất kỳ nền tảng nào được Java hỗ trợ (Windows, macOS, Linux).

## Kết luận

Bây giờ bạn đã biết **cách sử dụng hàm EXPAND** trong môi trường Java để động mở rộng tham chiếu ô, và bạn đã thấy quy trình **read and write excel file java** hoàn chỉnh bằng Aspose.Cells. Các bước — tải workbook, áp dụng công thức `EXPAND`, tính lại và lưu — bao phủ toàn bộ vòng đời tự động hoá Excel.

**Các bước tiếp theo** bạn có thể khám phá:

* Kết hợp `EXPAND` với các hàm mảng động khác như `FILTER` hoặc `SORT`.  
* Áp dụng cùng mẫu để **read and write excel file java** dữ liệu từ cơ sở dữ liệu hoặc API REST.  
* Thử nghiệm định dạng có điều kiện dựa trên phạm vi đã mở rộng.  

Hãy tự do điều chỉnh ví dụ cho dự án của mình, và để hàm `EXPAND` đơn giản hoá bất kỳ kịch bản nào mà kích thước dữ liệu thay đổi theo thời gian.

--- 

*Chúc lập trình vui vẻ!*


## Bạn nên học gì tiếp theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}