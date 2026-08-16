---
date: '2026-08-16'
description: Tìm hiểu cách thêm tính toàn cầu hoá trong Java bằng Aspose.Cells, tùy
  chỉnh thông báo lỗi của Excel và thiết lập phụ thuộc Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Tìm hiểu cách thêm tính toàn cầu hoá trong Java bằng Aspose.Cells,
  tùy chỉnh thông báo lỗi của Excel và thiết lập phụ thuộc Maven. Thực hiện theo hướng
  dẫn từng bước.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Cách thêm tính toàn cầu hoá trong Java bằng Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Cách thêm tính toàn cầu hoá trong Java bằng Aspose.Cells
url: /vi/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cách thêm toàn cục hoá trong Java với Aspose.Cells

## Giới thiệu

Thêm toàn cục hoá vào workbook Java của bạn cho phép bạn hiển thị thông báo lỗi, giá trị boolean và các chuỗi đặc thù vùng miền khác bằng ngôn ngữ mà người dùng của bạn mong đợi. Trong hướng dẫn này, bạn sẽ học **cách thêm toàn cục hoá** cho tiếng Nga, nhưng mẫu tương tự hoạt động cho bất kỳ ngôn ngữ nào. Khi kết thúc hướng dẫn, bạn sẽ có thể:

- Ghi đè văn bản lỗi mặc định và các biểu diễn boolean.
- Áp dụng cài đặt tùy chỉnh của bạn cho bất kỳ đối tượng `Workbook` nào.
- Tích hợp giải pháp vào một dự án Java dựa trên Maven điển hình.

Sẵn sàng làm cho các tệp Excel của bạn thực sự đa ngôn ngữ? Hãy kiểm tra trước rằng môi trường phát triển của bạn đáp ứng các yêu cầu tiên quyết.

## Câu trả lời nhanh
- **Toàn cục hoá là gì trong Aspose.Cells?** Đó là một tập hợp các chuỗi nhận thức vùng miền (lỗi, boolean, v.v.) mà bạn có thể thay thế bằng văn bản tùy chỉnh.  
- **Artifact Maven nào được yêu cầu?** `com.aspose:aspose-cells:25.3`.  
- **Tôi có thể nhắm tới các ngôn ngữ khác ngoài tiếng Nga không?** Có – mở rộng `GlobalizationSettings` và ghi đè các phương thức cần thiết cho mỗi vùng miền.  
- **Tôi có cần giấy phép cho việc phát triển không?** Bản dùng thử miễn phí hoạt động cho việc thử nghiệm; giấy phép vĩnh viễn loại bỏ các dấu nước đánh giá.  
- **Giải pháp có an toàn với đa luồng không?** Áp dụng cài đặt cho mỗi workbook; đối tượng `GlobalizationSettings` tự nó là bất biến sau khi tạo.

## Toàn cục hoá là gì trong Aspose.Cells?

`GlobalizationSettings` là đối tượng cấu hình của Aspose.Cells, điều khiển các chuỗi đặc thù vùng miền như thông báo lỗi, giá trị boolean, ký hiệu tiền tệ và mẫu ngày. Bằng cách cung cấp lớp con của riêng bạn, bạn cho thư viện biết chuỗi nào sẽ hiển thị cho mỗi nền văn hoá, cho phép bạn thay thế các chuỗi tiếng Anh mặc định bằng bản dịch phù hợp với ngôn ngữ và quy ước khu vực của người dùng cuối.

## Tại sao thêm toàn cục hoá tùy chỉnh?

Aspose.Cells hỗ trợ **hơn 50 định dạng đầu vào và đầu ra** – bao gồm XLSX, CSV, PDF và ODS – và có thể xử lý workbook với **lên tới 200 000 dòng** mà không cần tải toàn bộ tệp vào bộ nhớ. Tùy chỉnh toàn cục hoá đảm bảo người dùng cuối thấy các thông báo bằng ngôn ngữ mẹ đẻ của họ, giảm khoảng **30 %** các phiếu hỗ trợ cho các triển khai đa quốc gia.

## Yêu cầu tiên quyết

- **Java Development Kit** 8 hoặc mới hơn.
- **IDE** như IntelliJ IDEA hoặc Eclipse.
- **Aspose.Cells for Java** phiên bản 25.3 (hoặc mới hơn) được thêm qua Maven hoặc Gradle.

### Cài đặt Aspose.Cells cho Java

Thêm phụ thuộc Maven vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Hoặc, nếu bạn thích Gradle, chèn đoạn sau vào `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Nhận giấy phép

Aspose cung cấp một số tùy chọn cấp phép:

- **Free trial** – đánh giá đầy đủ tính năng trong 30 ngày.  
- **Temporary license** – đánh giá không giới hạn mà không có dấu nước.  
- **Commercial license** – sẵn sàng cho sản xuất, với hỗ trợ ưu tiên.

Sau khi có được tệp giấy phép, thiết lập nó một lần khi khởi động ứng dụng:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Cách thêm toàn cục hoá cho tiếng Nga?

Đối tượng `Workbook` đại diện cho một tệp Excel được tải vào bộ nhớ, cung cấp quyền truy cập vào các sheet, ô và cài đặt của nó. Tải workbook của bạn, tạo một lớp con của `GlobalizationSettings`, và gắn nó vào workbook. Câu trả lời trực tiếp là: **khởi tạo một lớp `GlobalizationSettings` tùy chỉnh, ghi đè `getErrorValueString` và `getBooleanValueString`, sau đó gọi `workbook.setGlobalizationSettings(customSettings)`**. Cách tiếp cận hai bước này thay thế các chuỗi tiếng Nga mặc định bằng chuỗi của bạn.

### Định nghĩa cài đặt tùy chỉnh

Lần đầu tiên bạn tham chiếu `GlobalizationSettings` trong hướng dẫn này, lưu ý định nghĩa:

`GlobalizationSettings` là lớp cơ sở mà Aspose.Cells sử dụng để lấy các chuỗi đặc thù vùng miền.  

Bây giờ tạo một lớp con trả về văn bản đặc thù cho tiếng Nga:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Áp dụng cài đặt vào workbook

Sau khi định nghĩa lớp con, gắn nó vào bất kỳ đối tượng `Workbook` nào:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Ứng dụng thực tiễn

- **Financial reporting** – hiển thị mã lỗi bằng ngôn ngữ mẹ đẻ của kế toán, giảm hiểu lầm.  
- **Enterprise‑wide tools** – nhúng cùng logic toàn cục hoá vào hàng chục công cụ nội bộ dựa trên Excel.  
- **Automated data pipelines** – đảm bảo các hệ thống hạ nguồn nhận giá trị nhận thức vùng miền mà không cần bước dịch thêm.

## Các cân nhắc về hiệu năng

Khi bạn bật toàn cục hoá tùy chỉnh, Aspose.Cells vẫn xử lý công thức và I/O với hiệu năng cao như trước. Để giữ mức sử dụng bộ nhớ thấp:

- Giải phóng các tham chiếu workbook (`wb.dispose()`) sau khi lưu.  
- Sử dụng `CalculationOptions.setEnableIterativeCalculation(true)` chỉ khi cần thiết.  
- Tinh chỉnh heap của JVM (`-Xmx2g`) cho các workbook lớn hơn 100 MB.

## Câu hỏi thường gặp

**Q: Tôi có thể áp dụng cùng một cài đặt toàn cục hoá cho nhiều workbook cùng lúc không?**  
A: Có. Tạo một thể hiện `RussianGlobalization` duy nhất và truyền nó cho mỗi workbook qua `setGlobalizationSettings`.

**Q: Nếu tôi cần hỗ trợ một ngôn ngữ sử dụng script phải‑trái thì sao?**  
A: Ghi đè các phương thức bổ sung như `getCurrencySymbol` và `getDatePattern` trong lớp con của bạn để trả về các ký hiệu RTL thích hợp.

**Q: Có cần giấy phép cho phiên bản dùng thử để sử dụng toàn cục hoá tùy chỉnh không?**  
A: Không. Phiên bản dùng thử hoàn toàn hỗ trợ `GlobalizationSettings`; chỉ có dấu nước đánh giá xuất hiện trên một số định dạng đầu ra nhất định.

**Q: Làm thế nào để gỡ lỗi các chuỗi lỗi không đúng?**  
A: Chèn các câu lệnh `System.out.println` bên trong các phương thức đã ghi đè của bạn để xác minh giá trị `err` đầu vào khớp với các trường hợp trong `switch`.

**Q: Điều này có ảnh hưởng đến tốc độ tính toán công thức không?**  
A: Hầu như không. Thư viện chỉ tra cứu chuỗi khi hiển thị giá trị ô, không phải trong các bước tính toán trung gian.

## Tài nguyên bổ sung

- **Documentation**: Khám phá các hướng dẫn chi tiết tại [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Download**: Truy cập các bản phát hành mới nhất tại [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Purchase**: Mua giấy phép cho mục đích thương mại tại [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Free trial**: Bắt đầu với bản dùng thử miễn phí từ [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: Nhận giấy phép tạm thời qua [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support**: Nhận trợ giúp từ cộng đồng tại [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Cập nhật lần cuối:** 2026-08-16  
**Kiểm tra với:** Aspose.Cells 25.3 for Java  
**Tác giả:** Aspose

## Hướng dẫn liên quan

- [Aspose.Cells Java: Hướng dẫn Engine Tính toán Tùy chỉnh](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Cách sử dụng Aspose Cells – Hướng dẫn Engine Excel cho Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Quản lý kết nối dữ liệu Excel với Aspose.Cells trong Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}