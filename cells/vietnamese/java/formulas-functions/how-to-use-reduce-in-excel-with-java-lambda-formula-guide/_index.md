---
category: general
date: 2026-06-08
description: Cách sử dụng reduce trong Excel với Java bằng Aspose.Cells. Học công
  thức lambda trong Excel, mảng động Java, cách viết lambda và tính tổng bằng reduce
  trong một hướng dẫn chi tiết từng bước.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: vi
og_description: Cách sử dụng reduce trong Excel với Java. Thành thạo công thức lambda
  Excel, mảng động Java và tính tổng bằng reduce qua một ví dụ đầy đủ, có thể chạy
  được.
og_title: Cách Sử Dụng Reduce trong Excel với Java – Hướng Dẫn Công Thức Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Cách sử dụng Reduce trong Excel với Java – Hướng dẫn công thức Lambda
url: /vi/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng Reduce trong Excel với Java – Hướng Dẫn Công Thức Lambda

Bạn đã bao giờ tự hỏi **cách sử dụng reduce** trong Excel khi viết mã Java chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cố gắng kết hợp các hàm mảng động mới của Excel với tự động hoá dựa trên Java, và câu trả lời không phức tạp như ban đầu.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ cụ thể cho thấy **cách sử dụng reduce** cùng với một biểu thức **lambda formula Excel**, tất cả được hỗ trợ bởi thư viện Aspose.Cells for Java. Khi kết thúc, bạn sẽ có thể tạo các mảng động trong Java, viết các hàm lambda, và tính **tổng với reduce**—không cần can thiệp thủ công vào bảng tính.

---

## Những Gì Bạn Sẽ Xây Dựng

- Một workbook mới được tạo hoàn toàn từ Java.  
- Một mảng động **EXPAND** điền các ô A1:A5 với các số 1‑5.  
- Một công thức **REDUCE** tính tổng các số đó bằng **lambda formula Excel**.  
- Một tệp `.xlsx` đã lưu mà bạn có thể mở trong bất kỳ chương trình bảng tính nào để xác minh kết quả.

Không có macro bên ngoài, không VBA—chỉ mã Java thuần và các hàm hiện đại của Excel.

---

## Yêu Cầu Trước

- Java 17 (hoặc bất kỳ JDK gần đây nào) – các phiên bản cũ hơn vẫn hoạt động nhưng bạn sẽ bỏ lỡ cú pháp `var`.  
- Aspose.Cells for Java (bản dùng thử miễn phí hoạt động tốt cho bản demo này).  
- Kiến thức cơ bản về cú pháp Java và công thức Excel.  

Nếu bạn mới với **dynamic arrays java**, đừng lo—hướng dẫn này giải thích mọi phần.

---

## Bước 1: Thiết Lập Dự Án và Nhập Aspose.Cells

Đầu tiên, thêm phụ thuộc Aspose.Cells Maven vào tệp `pom.xml` của bạn (hoặc tải JAR thủ công).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Giữ các phụ thuộc luôn cập nhật; các phiên bản mới cải thiện tốc độ đánh giá công thức, điều này quan trọng khi bạn **cách sử dụng reduce** trong các bảng tính lớn.

---

## Bước 2: Tạo Workbook và Truy Cập vào Worksheet Đầu Tiên

Bây giờ chúng ta sẽ tạo một workbook mới hoàn toàn. Đây là nền tảng để học **cách sử dụng reduce** vì đối tượng workbook cung cấp một môi trường để chèn công thức.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Tại sao điều này quan trọng:* Lớp `Workbook` trừu tượng hoá toàn bộ tệp Excel, trong khi `Worksheet` đại diện cho một tab duy nhất. Bạn sẽ thấy sau này cách **dynamic arrays java** có thể lấp đầy nhiều ô từ một công thức duy nhất đặt ở A1.

---

## Bước 3: Tạo Mảng Dọc với EXPAND

Hàm `EXPAND` của Excel có thể truyền giá trị ra một phạm vi. Chúng ta sẽ dùng nó để tạo các số 1 đến 5 trong cột A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Nếu bạn mở workbook kết quả, các ô A1:A5 sẽ hiển thị 1, 2, 3, 4, 5. Đây là phần **dynamic arrays java**—một công thức lấp đầy toàn bộ phạm vi.

---

## Bước 4: Viết REDUCE Lambda để Tính Tổng Mảng

Đây là nơi chúng ta trả lời câu hỏi cốt lõi: **cách sử dụng reduce** trong Excel từ Java. Hàm `REDUCE` lặp qua một mảng, áp dụng một lambda mà bạn cung cấp. Trong trường hợp của chúng ta, chúng ta sẽ tính tổng các số.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Hãy phân tích từng phần:

- `0` – giá trị tích lũy ban đầu (`acc`).  
- `A1:A5` – mảng chúng ta tạo bằng **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel** cộng mỗi phần tử (`x`) vào tích lũy (`acc`).  

Khi công thức chạy, `B1` sẽ chứa **15**, là **tổng với reduce** của các số 1‑5.

> **Cách viết lambda** trong Excel? Hãy nghĩ nó như một hàm ẩn danh, trong đó các đối số đầu tiên là các tham số, và biểu thức cuối cùng là giá trị trả về. Trong Java chúng ta chỉ nhúng văn bản; engine của Excel thực hiện phần tính toán.

---

## Bước 5: Lưu Workbook

Cuối cùng, chúng ta lưu workbook vào đĩa để bạn có thể mở nó trong Excel, Google Sheets, hoặc bất kỳ trình xem nào hỗ trợ `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Mở tệp và bạn sẽ thấy:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**Tổng với reduce** xuất hiện ở B1, xác nhận rằng chúng ta đã thành công trong việc trình diễn **cách sử dụng reduce** cùng với **lambda formula Excel** từ Java.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là chương trình Java hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào IDE của bạn, điều chỉnh thư mục đầu ra, và nhấn **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Kết quả mong đợi** khi bạn mở `new-functions.xlsx`:

- Các ô **A1:A5** chứa `1, 2, 3, 4, 5`.  
- Ô **B1** hiển thị `15`, xác nhận **tổng với reduce**.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu tôi cần một mảng ngang thay vì dọc thì sao?

Đổi các đối số cột/hàng trong `EXPAND`. Đối với một truyền ngang qua B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Tôi có thể dùng REDUCE để nhân thay vì cộng không?

Chắc chắn. Chỉ cần thay đổi phần thân lambda:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Bây giờ B1 sẽ hiển thị `120` (5 ! = 120).

### Aspose.Cells có hỗ trợ các hàm LAMBDA tùy chỉnh không?

Có, bạn có thể định nghĩa các hàm LAMBDA có tên thông qua bộ sưu tập `Names` của workbook, sau đó gọi chúng như bất kỳ công thức tích hợp nào. Đó là một phần sâu hơn cho một hướng dẫn sau về **cách viết lambda** mà tồn tại vượt ra ngoài một ô duy nhất.

### Còn các phiên bản Excel cũ không nhận ra REDUCE thì sao?

Nếu bạn nhắm tới Excel 2019 hoặc phiên bản cũ hơn, engine sẽ trả về `#NAME?`. Trong những trường hợp như vậy

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}