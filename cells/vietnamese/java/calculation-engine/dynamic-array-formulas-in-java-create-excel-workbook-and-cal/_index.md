---
category: general
date: 2026-06-30
description: Công thức mảng động trong Java cho phép bạn xây dựng các bảng tính Excel
  mạnh mẽ. Học cách tạo workbook Excel bằng Java và tính toán nhanh tất cả các công
  thức.
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: vi
og_description: Công thức mảng động trong Java đơn giản hoá việc tự động hoá Excel.
  Hướng dẫn này chỉ cách tạo workbook Excel bằng Java, sử dụng hàm expand, công thức
  lambda và tính toán tất cả các công thức.
og_title: Công Thức Mảng Động trong Java – Tạo Sổ Làm Việc & Tính Toán Công Thức
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'Công thức mảng động trong Java: Tạo sổ làm việc Excel và tính toán tất cả
  các công thức'
url: /vi/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Công Thức Mảng Động trong Java: Tạo Workbook Excel và Tính Toán Tất Cả Công Thức

Bạn đã bao giờ tự hỏi **công thức mảng động** hoạt động như thế nào khi tự động hoá Excel từ Java chưa? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi cần đưa các công thức phức tạp như `EXPAND` hay `REDUCE` vào một workbook mà không mở Excel.

Tin tốt là gì? Chỉ với vài dòng mã Java, bạn có thể **tạo workbook Excel theo kiểu Java**, chèn các hàm mảng hiện đại, và sau đó **tính toán tất cả công thức** trong một lần. Trong hướng dẫn này, chúng tôi sẽ đi qua từng bước, giải thích *tại sao* mỗi phần quan trọng, và cung cấp cho bạn một ví dụ hoàn chỉnh, có thể chạy ngay, để sao chép‑dán vào dự án của mình.

## Những Điều Bạn Sẽ Học

- Cách tạo một workbook Excel mới bằng Java (đúng, không cần giao diện Excel).  
- Cơ chế phía sau hàm `EXPAND` và cách nó biến một phạm vi đơn giản thành một mảng động.  
- Cách **sử dụng cú pháp công thức lambda** với `REDUCE` để thực hiện các phép tổng hợp tùy chỉnh.  
- Thêm các hàm lượng giác và hyperbolic (`COT`, `COTH`) mà nhiều người quên tồn tại trong bộ công thức của Excel.  
- Dòng lệnh một‑lần bạn cần để **tính toán tất cả công thức** sao cho workbook phản ánh kết quả mới nhất.  

> **Yêu cầu trước:** Java 8+ (để hỗ trợ lambda), thư viện Aspose.Cells for Java, và hiểu biết cơ bản về công thức Excel. Không cần phụ thuộc khác.

---

## Công Thức Mảng Động: Thiết Lập Workbook

Đầu tiên, hãy tạo một đối tượng workbook. Lớp `Workbook` từ Aspose.Cells là điểm khởi đầu; nó giống như một tấm vải trắng, nơi mọi công thức mảng động sẽ sinh sống.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*Lý do quan trọng:* Khởi tạo workbook bằng chương trình cho phép bạn kiểm soát hoàn toàn định dạng tệp, cài đặt khu vực, và—quan trọng nhất—đánh giá công thức mà không cần chạm tới đĩa.

---

## Sử Dụng Hàm EXPAND Để Mở Rộng Phạm Vi

Hàm `EXPAND` là câu trả lời của Excel cho việc “tràn” (spill) một phạm vi vào khu vực lớn hơn dựa trên kích thước bạn chỉ định. Nó hoàn hảo khi dữ liệu nguồn có thể thay đổi độ dài trong thời gian chạy.

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*Giải thích:*  
- `B1:B3` là phạm vi nguồn.  
- `5` yêu cầu Excel tạo ra năm hàng, ngay cả khi nguồn ngắn hơn.  
- `1` buộc kết quả chỉ có một cột.  

Khi bạn **tính toán tất cả công thức** sau này, kết quả ở `A1` sẽ là một dải dọc gồm năm giá trị, lấp đầy bằng ô trống nếu cần.

---

## Áp Dụng Công Thức LAMBDA Với REDUCE

Nếu bạn muốn tính tổng một cột nhưng đồng thời cần một bộ tích lũy tùy chỉnh, `REDUCE` kết hợp với **công thức lambda** là cách thực hiện. Cú pháp có vẻ hơi lạ lúc đầu, nhưng đó chỉ là cách Java nhúng một hàm ẩn danh nhỏ vào công thức Excel.

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*Tại sao nên dùng?*  
- `0` là hạt giống ban đầu (tổng khởi đầu).  
- `B1:B5` là mảng chúng ta sẽ gập lại.  
- `LAMBDA(a,b,a+b)` nói “lấy bộ tích lũy `a` và phần tử tiếp theo `b`, trả về tổng của chúng”.  

Bạn có thể thay `a+b` bằng bất kỳ logic tùy chỉnh nào—trung bình, max, hoặc thậm chí nối chuỗi—giúp `REDUCE` trở thành một khối xây dựng đa năng.

---

## Thêm Các Hàm Lượng Giác (COT, COTH)

Excel cung cấp một số hàm lượng giác ít được chú ý. Dưới đây là cách chèn một hàm cotangent đơn giản và hàm hyperbolic tương ứng vào bảng tính.

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*Mẹo:* Các hàm này tự động tuân theo chế độ tính toán của workbook, vì vậy bạn không cần mã bổ sung để chuyển độ sang radian—`PI()` đã làm phần việc nặng.

---

## Tính Toán Tất Cả Công Thức Trong Workbook

Bây giờ các công thức đã sẵn sàng, chúng ta cần **tính toán tất cả công thức** để các ô chứa giá trị thực thay vì chỉ là chuỗi công thức. Aspose.Cells thực hiện việc này bằng một lời gọi phương thức duy nhất.

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*Điều gì xảy ra phía sau?* Thư viện duyệt qua mọi ô, giải quyết các phụ thuộc, và tràn kết quả mảng ở những nơi cần thiết. Nếu bạn làm việc với các sheet khổng lồ, có thể tinh chỉnh tùy chọn tính toán để tối ưu hiệu năng, nhưng mặc định đã đủ tốt cho hầu hết các trường hợp.

---

## Ví Dụ Hoàn Chỉnh (Sẵn Sàng Sao Chép‑Dán)

Dưới đây là toàn bộ chương trình, sẵn sàng để bạn dán vào IDE. Nó bao gồm các import, phương thức `main`, và lời gọi `save` cuối cùng để bạn có thể mở tệp kết quả trong Excel và xem các dải tràn.

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**Kết quả mong đợi khi mở `DynamicArrayDemo.xlsx`:**

| A (Kết Quả) | B (Nguồn) |
|------------|-----------|
| 10         | 10 |
| 20         | 20 |
| 30         | 30 |
| (trống)    | 40 |
| (trống)    | 50 |
| 150 (tổng) |   |
| 1 (cot)    |   |
| 1.0373… (coth) | |

*Chú ý cách `A1` tràn ra năm hàng, mặc dù nguồn chỉ có ba giá trị. Đó là sức mạnh của **công thức mảng động**.*

---

## Những Sai Lầm Thường Gặp & Mẹo Chuyên Nghiệp

- **Đừng quên đặt chế độ tính toán** nếu bạn đã tắt tính toán tự động ở nơi khác; nếu không `calculateFormula()` sẽ không làm gì.  
- **Xung đột tràn mảng:** Nếu một ô khác đã chiếm vùng tràn, Excel sẽ trả về lỗi `#SPILL!`. Trong mã, bạn có thể xóa trước vùng đích bằng `worksheet.getCells().clear(0, 0, maxRow, maxColumn)`.  
- **Quirks cú pháp Lambda:** Hàm `LAMBDA` yêu cầu các tham số được ngăn cách bằng dấu phẩy, không phải dấu chấm phẩy. Thiếu dấu phẩy sẽ khiến toàn bộ công thức không phân tích được.  
- **Mẹo hiệu năng:** Khi làm việc với hàng ngàn dòng, gọi `workbook.getSettings().setCalculateFormulaOnOpen(false)` trước khi chèn dữ liệu hàng loạt, sau đó bật lại trước lời gọi `calculateFormula()` cuối cùng.

---

## Các Bước Tiếp Theo

Sau khi đã nắm vững **công thức mảng động**, bạn có thể khám phá:

- Các hàm **`FILTER`** và **`SORT`** để định hình dữ liệu ngay lập tức.  
- **`SEQUENCE`** để tạo mảng số mà không cần nguồn dữ liệu.  
- Sử dụng **các phạm vi đặt tên** kết hợp với `EXPAND` để có công thức sạch hơn, tái sử dụng được.  

Tất cả đều dựa trên cùng những khái niệm chúng ta đã đề cập—chỉ cần thay đổi chuỗi công thức và để Aspose.Cells thực hiện phần còn lại.

---

## Kết Luận

Trong hướng dẫn này, chúng tôi đã chỉ ra cách **tạo workbook Excel bằng Java**,


## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong bài viết này. Mỗi tài nguyên bao gồm các ví dụ mã đầy đủ, kèm theo giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Calculate Excel Formulas Java: Optimize with Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}