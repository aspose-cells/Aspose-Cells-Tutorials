---
category: general
date: 2026-06-30
description: Sắp xếp các giá trị duy nhất trong Excel bằng Java. Tìm hiểu cách đặt
  công thức, tính lại công thức và tạo danh sách duy nhất trong Excel với Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: vi
og_description: Sắp xếp các giá trị duy nhất trong Excel bằng Java. Hướng dẫn này
  chỉ cách thiết lập công thức, tính lại công thức và tạo danh sách duy nhất trong
  Excel chỉ trong vài phút.
og_title: Sắp xếp các giá trị duy nhất trong Excel – Hướng dẫn Java cho công thức
  mảng
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Sắp xếp các giá trị duy nhất trong Excel – Hướng dẫn Java toàn diện để thiết
  lập công thức mảng
url: /vi/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sắp Xếp Các Giá Trị Độc Nhất trong Excel – Hướng Dẫn Java Đầy Đủ Để Đặt Công Thức Mảng

Bạn đã bao giờ tự hỏi làm thế nào để **sắp xếp các giá trị độc nhất trong Excel** mà không phải kéo công thức khắp nơi? Bạn không phải là người duy nhất. Trong nhiều trường hợp báo cáo, bạn cần một danh sách sạch, được sắp xếp alphabetically của các mục riêng biệt, và việc làm thủ công thật là phiền phức.  

Tin tốt là gì? Chỉ với vài dòng code Java, bạn có thể **đặt công thức mảng** trên một worksheet, sau đó **tính lại các công thức** để phạm vi tràn (spilled range) tự động lấp đầy. Trong tutorial này, chúng ta sẽ đi qua mọi thứ—từ việc tạo workbook đến việc tạo danh sách độc nhất theo kiểu Excel—để bạn có thể nhúng giải pháp này trực tiếp vào ứng dụng của mình.

## Những Điều Hướng Dẫn Này Bao Quát

- Cài đặt dự án Java với Aspose.Cells (thư viện cung cấp đoạn code mẫu).  
- Sử dụng các hàm `SORT` và `UNIQUE` cùng nhau để **tạo danh sách độc nhất trong Excel**.  
- Áp dụng một **công thức mảng** vào ô một cách lập trình.  
- Kích hoạt một lần tính toán để bước **cách tính lại công thức** diễn ra ngay lập tức.  
- Kiểm tra đầu ra và tinh chỉnh giải pháp cho các trường hợp đặc biệt như ô trống hoặc phạm vi không liên tục.

Khi hoàn thành hướng dẫn này, bạn sẽ có thể chèn một phương thức sẵn sàng sử dụng vào bất kỳ dịch vụ Java nào cần xuất file Excel sạch sẽ.

> **Mẹo chuyên nghiệp:** Nếu bạn đã dùng Maven, việc thêm Aspose.Cells làm dependency sẽ giúp bạn tránh phải xử lý thủ công các file JAR.

---

## Yêu Cầu Trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Java 8 hoặc mới hơn | Aspose.Cells hỗ trợ Java 8+. |
| Maven (hoặc Gradle) | Đơn giản hoá việc quản lý dependency. |
| Aspose.Cells for Java | Cung cấp các API `Workbook`, `Worksheet`, và công thức mà chúng ta sẽ dùng. |
| Kiến thức cơ bản về các hàm Excel | Hiểu `SORT` và `UNIQUE` sẽ giúp bạn tùy biến code dễ dàng hơn. |

> *Nếu bạn chưa có Aspose.Cells, hãy thêm đoạn này vào `pom.xml` của bạn*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Bước 1: Tạo Workbook Mới (Bắt Đầu Đặt Công Thức)

Đầu tiên chúng ta cần một workbook trống. Hãy tưởng tượng nó như một canvas trắng, nơi chúng ta sẽ **đặt công thức mảng** vào ô `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Tại sao phải tạo workbook mới?*  
> Điều này đảm bảo môi trường sạch sẽ, tránh các công thức ẩn có thể gây xung đột với dữ liệu thử nghiệm của bạn.

---

## Bước 2: Điền Dữ Liệu Mẫu (Tùy Chọn Nhưng Hữu Ích)

Để thấy kết quả rõ ràng, hãy điền cột **B** với một số mục trùng lặp.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Tại sao dùng cột B?*  
> Công thức chúng ta sẽ viết sẽ tham chiếu tới `B1:B10`, vì vậy việc giữ dữ liệu ở đó giống với ví dụ Excel cổ điển.

---

## Bước 3: Đặt Công Thức Mảng **Sắp Xếp Các Giá Trị Độc Nhất trong Excel**

Bây giờ phép màu sẽ xảy ra. Chúng ta kết hợp `UNIQUE` (để loại bỏ trùng lặp) với `SORT` (để sắp xếp alphabetically). Biểu thức thu được là một **công thức mảng**, nghĩa là nó sẽ tràn sang các ô lân cận một cách tự động.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Cách Hoạt Động

- `UNIQUE(B1:B10)` quét phạm vi và trả về một mảng dọc các chuỗi riêng biệt.  
- `SORT(...)` nhận mảng đó và sắp xếp theo thứ tự tăng dần.  
- Đặt toàn bộ biểu thức trong `=` và gọi `setFormulaArray` báo cho Aspose.Cells xử lý kết quả như một **mảng tràn**, giống như trong Excel.

> **Lưu ý:** Nếu bạn đang dùng phiên bản Excel cũ hơn không hỗ trợ `SORT` hoặc `UNIQUE`, bạn có thể quay lại `SORT(UNIQUE(...))` kết hợp với hàm **LET** hoặc dùng các công thức mảng truyền thống (`=INDEX(...)`). Tutorial này tập trung vào cách tiếp cận mảng động hiện đại vì nó là cách sạch nhất để **tạo danh sách độc nhất trong Excel** ngày nay.

---

## Bước 4: Tính Lại Các Công Thức Để Phạm Vi Tràn Được Điền

Sau khi công thức đã được đặt, workbook sẽ không tự động tính toán nó. Đây là lúc bước **cách tính lại công thức** xuất hiện.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Gọi `calculateFormula()` buộc Aspose.Cells chạy engine Excel, lấp đầy các ô `A1`, `A2`, … với các giá trị đã sắp xếp và loại bỏ trùng lặp.

> *Tại sao không dựa vào tính toán lười biếng?*  
> Trong môi trường server‑side, bạn thường cần dữ liệu sẵn sàng để xuất (CSV, PDF, v.v.) ngay sau khi tính toán, vì vậy một lời gọi rõ ràng sẽ đảm bảo tính nhất quán.

---

## Bước 5: Kiểm Tra Kết Quả (Gỡ Rối Tùy Chọn)

Luôn luôn là ý tưởng tốt khi in các giá trị tràn ra console—đặc biệt khi bạn đang tự học một API mới.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Chạy chương trình sẽ in ra:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Mở file `SortedUniqueValues.xlsx` và bạn sẽ thấy cùng một dữ liệu tràn từ `A1` xuống dưới.

---

## Xử Lý Các Trường Hợp Đặc Biệt

### Ô Trống Trong Phạm Vi Nguồn

Nếu `B1:B10` chứa các ô trống, `UNIQUE` sẽ coi chúng là một mục riêng biệt. Để bỏ qua ô trống, hãy bao quanh phạm vi bằng `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Dữ Liệu Không Liên Tiếp

Khi dữ liệu của bạn nằm trong nhiều cột, bạn có thể ghép chúng bằng `CHOOSE` hoặc `TEXTJOIN` trước khi áp dụng `UNIQUE`. Ví dụ:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Những điều chỉnh này cho thấy tính linh hoạt của **cách đặt công thức** cho các kịch bản phức tạp hơn.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Bước Kết Hợp)

Dưới đây là chương trình Java đầy đủ, có thể chạy ngay. Sao chép‑dán vào IDE, thêm dependency Aspose.Cells, và nhấn *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Kết quả mong đợi** (hiển thị trong console) trùng với danh sách đã sắp xếp, loại bỏ trùng lặp mà chúng ta đã thảo luận. Mở file Excel được tạo ra sẽ hiển thị cùng các giá trị tràn từ `A1` xuống dưới.

---

## Câu Hỏi Thường Gặp

**H: Điều này có hoạt động với các phiên bản Excel cũ hơn (trước Office 365) không?**  
Đ: Các hàm `SORT` và `UNIQUE` là một phần của engine Mảng Động được giới thiệu trong Excel 365. Đối với các file legacy, bạn sẽ cần dùng các công thức mảng cổ điển như `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells vẫn có thể đánh giá chúng, nhưng cú pháp sẽ dài hơn.

**H: Tôi có thể đặt công thức mảng ở một phạm vi khác ngoài `A1` không?**  
Đ: Chắc chắn. Chỉ cần thay đổi địa chỉ trong `cells.get("A1")`. Mảng tràn sẽ luôn bắt đầu từ ô bạn chỉ định và mở rộng sang phải và xuống dưới tùy nhu cầu.

**H: Nếu dữ liệu nguồn của tôi lớn hơn `B1:B10` thì sao?**  
Đ: Thay thế phạm vi tĩnh bằng một phạm vi động, ví dụ `B:B` hoặc một named range. Công thức sẽ trở thành `=SORT(UNIQUE(B:B))`. Hãy cẩn thận khi dùng tham chiếu toàn cột trên các sheet rất lớn; chúng có thể ảnh hưởng đến hiệu năng.

---

## Kết Luận

Chúng ta vừa khám phá **cách đặt công thức** trong Java để **sắp xếp các giá trị độc nhất trong Excel**, cách **tính lại các công thức**, và cách **tạo danh sách độc nhất trong Excel** bằng API mạnh mẽ của Aspose.Cells. Các bước rất đơn giản: tạo workbook, điền dữ liệu, áp dụng công thức mảng, kích hoạt tính toán, và kiểm tra kết quả.  

Từ đây, bạn có thể mở rộng—thêm conditional formatting, xuất ra PDF, hoặc tích hợp phương thức vào một web service cung cấp báo cáo đã sẵn sàng. Ý tưởng cốt lõi vẫn giữ nguyên: để các hàm của Excel thực hiện phần việc nặng, và để Java điều phối quy trình.

Sẵn sàng nâng cấp tự động hoá Excel của bạn? Hãy thử thay `SORT` bằng `SORTBY` để sắp xếp theo cột phụ, hoặc thử `FILTER` để loại bỏ các hàng không đáp ứng quy tắc kinh doanh. Các khả năng gần như vô hạn.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}