---
category: general
date: 2026-06-30
description: Đặt định dạng số tùy chỉnh trong Excel bằng Java. Tìm hiểu cách tạo workbook
  Excel bằng Java, lấy ngày‑giờ từ ô, tính toán công thức trong workbook và xuất giá
  trị ngày‑giờ.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: vi
og_description: Đặt định dạng số tùy chỉnh trong Excel bằng Java. Hướng dẫn này cho
  thấy cách tạo workbook Excel bằng Java, lấy ngày‑giờ từ ô, tính công thức trong
  workbook và xuất giá trị ngày‑giờ.
og_title: Đặt Định Dạng Số Tùy Chỉnh trong Excel bằng Java – Hướng Dẫn Đầy Đủ
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Đặt Định Dạng Số Tùy Chỉnh trong Excel bằng Java – Hướng Dẫn Toàn Diện
url: /vi/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Đặt Định Dạng Số Tùy Chỉnh trong Excel bằng Java – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **set custom number format** trong một bảng tính Excel khi làm việc với Java chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một engine báo cáo hay chỉ muốn hiển thị ngày theo thời kỳ Nhật Bản một cách chính xác, việc thành thạo thủ thuật này sẽ tiết kiệm cho bạn vô số giờ xử lý sau. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực tế mà **creates Excel workbook Java**, áp dụng định dạng theo vùng miền, tính lại công thức, và cuối cùng **gets DateTime from cell** để **output datetime value**.

Chúng tôi sẽ sử dụng thư viện Aspose.Cells for Java phổ biến vì nó xử lý định dạng số và ngày tháng dựa trên văn hoá ngay từ đầu. Khi kết thúc hướng dẫn, bạn sẽ có một chương trình tự chứa, có thể chạy được mà bạn có thể đưa vào bất kỳ dự án Maven hoặc Gradle nào. Không có các lối tắt mơ hồ “xem tài liệu”—chỉ có mã vững chắc và giải thích rõ ràng.

---

## Những Điều Bạn Sẽ Học

- Cách **create Excel workbook Java** một cách lập trình.
- Các bước chính xác để **set custom number format** cho ngày theo thời kỳ Nhật Bản.
- Tại sao việc gọi **calculate workbook formulas** là cần thiết trước khi trích xuất giá trị.
- Cách đúng để **get datetime from cell** và **output datetime value**.
- Những rủi ro phổ biến (thiếu locale, công thức lỗi thời) và cách khắc phục nhanh.

## Yêu Cầu Trước

- Java 8 hoặc mới hơn đã được cài đặt trên máy của bạn.  
- Aspose.Cells for Java 23.11 (hoặc bất kỳ phiên bản gần đây nào).  
- Một IDE hoặc trình soạn thảo cơ bản—IntelliJ IDEA, Eclipse, VS Code, bất kỳ công cụ nào bạn thích.  

Nếu bạn chưa thêm Aspose.Cells vào dự án, hãy dán đoạn mã Maven sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Người dùng Gradle có thể thêm:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Bây giờ môi trường đã sẵn sàng, hãy bắt đầu khám phá mã.

---

## Bước 1: Đặt Định Dạng Số Tùy Chỉnh – Tổng Quan

Trước khi viết bất kỳ mã Java nào, việc hình dung mục tiêu sẽ giúp ích. Hãy tưởng tượng một ô Excel cần hiển thị **“令和2年4月1日”** thay vì chuỗi ISO‑8601 “2020‑04‑01”. Giá trị bên trong vẫn là một ngày thực (để công thức vẫn hoạt động), nhưng *hiển thị* tuân theo định dạng thời kỳ Nhật Bản. Đây chính là mục đích của thao tác **set custom number format**.

Dưới đây là toàn bộ file nguồn. Bạn có thể sao chép‑dán nó vào `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Tại Sao Điều Này Hoạt Động

- **`setNumberFormat`** cho Excel biết cách *hiển thị* giá trị số nguyên. Chuỗi định dạng `[$-ja-JP]ggge年m月d日` là chìa khóa; `ggg` chọn tên thời kỳ, `e` là năm trong thời kỳ, tiếp theo là các ký tự tháng và ngày.
- **`calculateFormula`** buộc Aspose.Cells diễn giải chuỗi “R02-04-01” thành ngày dựa trên lịch Nhật Bản. Bỏ qua bước này ô sẽ còn lại dưới dạng văn bản, và `getDateTime()` sẽ ném ngoại lệ.
- **`getDateTime`** cuối cùng trích xuất đối tượng `java.util.Calendar` *thực tế*, cho phép bạn thao tác, định dạng hoặc lưu trữ ở nơi khác.

## Bước 2: Tạo Excel Workbook Java – Nhìn Sâu Hơn

Khi bạn **create Excel workbook Java**, bạn không chỉ cấp phát bộ nhớ; bạn còn thiết lập các kiểu mặc định, một worksheet mặc định, và một văn hoá mặc định (thường là locale của hệ thống). Nếu bạn cần một locale mặc định khác, bạn có thể truyền một đối tượng `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Trong hầu hết các trường hợp, constructor đơn giản là đủ, nhưng biết đến tùy chọn thay thế là tốt—đặc biệt khi bạn làm việc với nhiều locale trong cùng một ứng dụng.

*Pro tip:* Luôn giữ workbook trong bộ nhớ cho đến khi bạn hoàn tất việc định dạng. Ghi ra đĩa sau mỗi thay đổi sẽ gây tốn I/O không cần thiết.

## Bước 3: Lấy DateTime từ Ô – Xử Lý Kết Quả

Dòng `java.util.Calendar dt = cellA1.getDateTime();` thực hiện phần công việc nặng. Ở phía sau, Aspose.Cells chuyển số serial nội bộ (số ngày kể từ 31‑12‑1899) thành một `Calendar`. Việc chuyển đổi này tôn trọng locale của workbook, vì vậy bạn nhận được ngày Gregorian chính xác mặc dù hiển thị dùng thời kỳ Nhật Bản.

Nếu bạn cần một `java.time.LocalDate` (API mới hơn), chuyển đổi như sau:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Điều này đáp ứng yêu cầu **output datetime value** đồng thời vẫn hiện đại.

## Bước 4: Tính Toán Công Thức Workbook – Khi Nó Quan Trọng

Bạn có thể tự hỏi: *“Tôi có thực sự cần gọi `calculateFormula()` không?”* Câu trả lời là có, trừ khi bạn đã cung cấp cho ô một đối tượng Java `Date` ngay từ đầu. Khi bạn **set custom number format** trên một chuỗi văn bản, Excel (và Aspose.Cells) coi nó như một biểu thức dạng công thức cần được đánh giá. Nếu không tính lại, `getDateTime()` sẽ trả về giá trị mặc định `1900‑01‑00` hoặc ném `CellValueException`.

Nếu workbook của bạn đã chứa các công thức phức tạp tham chiếu đến ô vừa định dạng, hãy gọi `calculateFormula()` *một lần* sau khi hoàn tất mọi thay đổi. Gọi lặp lại sẽ tốn kém.

## Bước 5: Xuất Giá Trị DateTime – Xác Nhận Kết Quả

Chạy demo sẽ in ra một dòng tương tự:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Dòng này xác nhận ba điều:

1. **set custom number format** đã được áp dụng (bạn có thể mở file `.xlsx` tạo ra trong Excel để thấy “令和2年4月1日”).
2. Bước **calculate workbook formulas** đã thành công, biến chuỗi thời kỳ thành ngày thực.
3. Lệnh **get datetime from cell** đã trả về một `Calendar` hợp lệ, sau đó chúng tôi **output datetime value** lên console.

Nếu bạn mở workbook bằng một chương trình bảng tính, bạn sẽ thấy văn bản đã được định dạng, nhưng giá trị thực tế của ô vẫn là số serial `43831` (đại diện cho ngày 2020‑04‑01 trong Excel). Sự kép này chính là sức mạnh của Excel.

## Những Rủi Ro Thông Thường & Trường Hợp Đặc Biệt

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | Ô vẫn là chuỗi vì `calculateFormula()` đã bị bỏ qua. | Luôn gọi `workbook.calculateFormula()` sau khi đặt ngày dạng văn bản cần chuyển đổi. |
| Japanese era not displayed correctly | Mã locale thiếu hoặc không đúng. | Sử dụng `[$-ja-JP]` trong chuỗi định dạng, hoặc đặt locale workbook qua `LoadOptions`. |
| Format shows “#VALUE!” in Excel | Chuỗi định dạng bị sai cấu trúc. | Kiểm tra lại dấu ngoặc và ký tự; mẫu `ggge年m月d日` là bắt buộc cho năm thời kỳ. |
| Time component appears (e.g., “00:00:00”) | Chuỗi nguồn có thời gian hoặc kiểu ô thêm nó. | Cắt bỏ phần thời gian trong chuỗi nguồn hoặc điều chỉnh định dạng thành `ggge年m月d日;@`. |

## Ví Dụ Hoàn Chỉnh – Chạy Một Lần

Nếu bạn muốn một file duy nhất không có bình luận thừa, đây là phiên bản tối thiểu:



## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo một Excel Workbook bằng Aspose.Cells trong Java: Hướng Dẫn Từng Bước](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Thành Thạo Trình Bày Dữ Liệu trong Excel: Định Dạng Số và Ngày Tùy Chỉnh với Aspose.Cells cho Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Cách Tạo & Định Dạng Các Ô Excel bằng Aspose.Cells cho Java: Hướng Dẫn Từng Bước](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}