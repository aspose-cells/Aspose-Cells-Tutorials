---
category: general
date: 2026-03-01
description: Cách tạo PDF và lưu workbook dưới dạng PDF, xuất Excel sang HTML, và
  sử dụng hàm expand với Aspose.Cells cho Java. Bao gồm mã từng bước.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: vi
og_description: Cách tạo PDF từ một workbook bằng Aspose.Cells cho Java. Tìm hiểu
  cách lưu workbook dưới dạng PDF, xuất Excel sang HTML và sử dụng hàm EXPAND.
og_title: Cách tạo PDF từ Workbook – Hướng dẫn Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Cách tạo PDF từ Workbook – Hướng dẫn Java toàn diện
url: /vi/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Tạo PDF từ Workbook – Hướng Dẫn Java Toàn Diện

Bạn đã bao giờ tự hỏi **cách tạo PDF** trực tiếp từ một workbook Excel mà không cần dùng các công cụ chuyển đổi bên thứ ba chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi họ cần xuất PDF nhanh, xem trước HTML, hoặc các công thức mảng phức tạp—tất cả trong một lần.  

Trong tutorial này chúng ta sẽ đi qua một chương trình Java độc lập duy nhất thực hiện đúng như vậy. Chúng ta sẽ **lưu workbook dưới dạng PDF**, cho bạn thấy cách **xuất Excel sang HTML** trong khi giữ các hàng cố định, và minh họa **cách sử dụng hàm expand** trong một worksheet. Khi kết thúc, bạn sẽ có một dự án có thể chạy được và có thể đưa vào bất kỳ build Maven hay Gradle nào.

> **Pro tip:** Tất cả mã dưới đây hoạt động với Aspose.Cells 23.10 (hoặc mới hơn). Nếu bạn đang dùng phiên bản cũ hơn, một số tên phương thức có thể hơi khác.

---

## Yêu Cầu Trước

- **Java 17** (hoặc bất kỳ phiên bản LTS nào) đã được cài đặt và cấu hình.  
- Thư viện **Aspose.Cells for Java**. Thêm phụ thuộc Maven sau vào file `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Một IDE hoặc trình soạn thảo văn bản mà bạn thích (IntelliJ IDEA, VS Code, Eclipse…).

Không có API bên ngoài, không có dịch vụ web—chỉ Java thuần và SDK Aspose.Cells.

---

## Tổng Quan Về Giải Pháp

Chúng ta sẽ chia việc triển khai thành **bảy bước logic**:

1. Tạo một workbook và minh họa hàm **EXPAND**.  
2. Bật tính năng chọn biến thể phông chữ và **lưu workbook dưới dạng PDF**.  
3. Xuất cùng một workbook sang HTML trong khi giữ nguyên các hàng cố định.  
4. Sử dụng Smart Marker với tham số `IF` để chèn văn bản có điều kiện.  
5. Áp dụng Smart Marker master‑detail cho dữ liệu phân cấp.  
6. Tải một file Markdown chứa các hình ảnh được mã hoá Base‑64.  
7. Cấu hình các tùy chọn GridJs cho căn chỉnh và viền, sau đó chèn dữ liệu.

Mỗi bước được đóng gói trong một phương thức riêng để giữ cho phương thức `main` gọn gàng và để minh họa **tại sao** chúng ta làm như vậy, không chỉ **cái gì** chúng ta gõ.

---

## Bước 1 – Tạo Workbook và Sử Dụng Hàm EXPAND

Hàm **EXPAND** là một công thức mảng động mới được giới thiệu trong Office 365. Nó cho phép bạn “tràn” một phạm vi vào một khu vực lớn hơn mà không cần sao chép ô thủ công.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Tại sao điều này quan trọng:**  
- `EXPAND` tự động bổ sung các ô trống vào kết quả, rất phù hợp khi bạn sau này **lưu workbook dưới dạng PDF**—PDF sẽ hiển thị một bảng hình chữ nhật sạch sẽ.  
- Gọi `calculateFormula()` đảm bảo công cụ tính công thức chạy trước khi chúng ta xuất bất kỳ thứ gì.

---

## Bước 2 – Bật Chọn Biến Thể Phông Chữ và **Lưu Workbook dưới dạng PDF**

Nếu bạn cần hỗ trợ kiểu chữ nâng cao (ví dụ: emoji hoặc các selector biến thể CJK), bạn phải bật tính năng này **trước** khi lưu.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Điểm then chốt:** Từ khóa chính **how to create pdf** được trả lời ở đây—bằng cách gọi `workbook.save(..., SaveFormat.PDF)` sau khi đã cấu hình các thiết lập.

---

## Bước 3 – **Xuất Excel sang HTML** Khi Giữ Các Hàng Cố Định

Thường thì các bên liên quan yêu cầu một bản xem trước web nhanh. Aspose.Cells có thể xuất sang HTML, và với `setPreserveFrozenRows(true)` chúng ta giữ được trải nghiệm cuộn giống như trong Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Tại sao bạn quan tâm:** Các hàng cố định là một tính năng tiện ích; nếu không có chúng, các hàng tiêu đề sẽ biến mất khi người dùng cuộn xuống trang.

---

## Bước 4 – Smart Marker với Tham Số IF

Smart Markers cho phép bạn hợp nhất dữ liệu vào mẫu mà không cần viết vòng lặp. Tham số `if` thêm logic điều kiện trực tiếp trong marker.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

File PDF đầu ra sẽ hiển thị **“VIP Customer: Acme Corp”** vì `IsVIP` là `true`. Thay đổi cờ thành `false` và bạn sẽ nhận được **“Regular Customer: Acme Corp”**—không cần viết mã thêm.

---

## Bước 5 – Master‑Detail Smart Marker Sử Dụng Dải Dữ Liệu Phân Cấp

Khi bạn có dữ liệu cha‑con (ví dụ: đơn hàng và các mục hàng), một master‑detail marker giúp bạn tránh việc chèn hàng thủ công.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Bạn sẽ nhận được gì:** Engine sẽ mở rộng các hàng master cho mỗi đơn hàng và tự động đặt các hàng detail dưới chúng—rất thích hợp cho hoá đơn hoặc báo cáo mua hàng.

---

## Bước 6 – Tải Tài Liệu Markdown với Hình Ảnh Base‑64 Nhúng

Nếu dữ liệu nguồn của bạn ở dạng Markdown (phổ biến trong quy trình tài liệu), Aspose.Cells có thể render trực tiếp vào workbook.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Lưu ý trường hợp đặc biệt:** Nếu chuỗi Base‑64 bị sai định dạng, Aspose sẽ bỏ qua hình ảnh nhưng vẫn tiếp tục xử lý phần còn lại của tài liệu—không gây crash.

---

## Bước 7 – Cấu Hình Các Tùy Chọn GridJs và Chèn Dữ Liệu

GridJs là một lưới JavaScript nhẹ mà Aspose có thể render thành HTML. Căn chỉnh số và áp dụng viền cải thiện khả năng đọc.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Tại sao chúng ta quan tâm:** Căn chỉnh đúng và viền làm cho HTML được tạo ra trông giống như một bảng tính được tinh chỉnh—rất hữu ích cho các dashboard.

---

## Tổng Hợp Tất Cả – Phương Thức `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}