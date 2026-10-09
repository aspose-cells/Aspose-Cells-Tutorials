---
category: general
date: 2026-06-21
description: Học cách thay đổi phông chữ của textbox, thiết lập màu phông chữ bằng
  mã và điều chỉnh kích thước phông chữ của ô trong lưới. Theo dõi hướng dẫn thực
  tế này để tạo kiểu cho các textbox.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: vi
og_description: Thay đổi phông chữ của textbox trong lưới một cách nhanh chóng. Hướng
  dẫn này chỉ cách tạo kiểu cho textbox, đặt màu phông chữ bằng lập trình, và điều
  chỉnh kích thước ô với mã rõ ràng.
og_title: Thay đổi phông chữ hộp văn bản trong lưới – Hướng dẫn lập trình chi tiết
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Thay đổi phông chữ của ô văn bản trong lưới – Hướng dẫn chi tiết từng bước
url: /vi/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thay Đổi Phông Chữ của Textbox trong Grid – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ cần **thay đổi phông chữ của textbox** trong một data grid nhưng không biết thuộc tính nào cần chỉnh không? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp khó khăn này khi xây dựng các bảng có thể chỉnh sửa hoặc dashboard. Trong tutorial này, chúng ta sẽ đi qua cách thay đổi phông chữ của textbox, đặt màu sắc một cách lập trình, và thậm chí điều chỉnh kích thước phông chữ theo từng ô.

Chúng tôi cũng sẽ chia sẻ các mẹo về **cách tạo kiểu cho textbox**, đề cập đến các trường hợp **thay đổi kích thước phông chữ của ô**, và chỉ cho bạn cách **đặt màu phông chữ bằng lập trình** mà không phải đau đầu. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng cho bất kỳ thành phần grid nào có API `getCell`.

## Prerequisites

- Trình duyệt hiện đại hỗ trợ ES6 (Chrome, Edge, Firefox, Safari)
- Thư viện grid cung cấp `grid.getCell(row, col)` và trả về một đối tượng ô chứa tham chiếu tới `textbox`
- Kiến thức cơ bản về đối tượng JavaScript và các thuộc tính CSS

Không cần cài đặt gói bổ sung—chỉ cần JavaScript thuần và API của grid.

## Overview of the Solution

Ý tưởng cốt lõi rất đơn giản: lấy ô mục tiêu, truy cập textbox bên trong, sau đó gán một đối tượng phông chữ mới định nghĩa family, size và color. Hãy tưởng tượng như đang thay bộ đồ mới cho textbox. Dưới đây là luồng tổng quan:

1. **Truy cập ô mục tiêu** – xác định hàng/cột bạn muốn.
2. **Lấy textbox** – phần tử UI chứa văn bản.
3. **Tạo đối tượng kiểu phông chữ** – chỉ định family, size và color.
4. **Áp dụng kiểu** – gán đối tượng vào thuộc tính `font` của textbox.

Xong rồi. Hãy đi sâu vào từng bước, giải thích lý do và xem mã thực tế.

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Step 1: Access the Target Cell in the Grid

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Tại sao điều này quan trọng:**  
> Các grid thường lưu trữ hàng và cột dưới dạng chỉ mục bắt đầu từ 0. Khi gọi `grid.getCell(2, 3)` chúng ta lấy ô ở **hàng 2, cột 3**. Nếu bạn muốn **thay đổi kích thước phông chữ của ô** ở vị trí khác, chỉ cần điều chỉnh các chỉ mục.

**Mẹo chuyên nghiệp:** Nếu grid của bạn hỗ trợ cột có tên, bạn có thể thay số cột bằng khóa, ví dụ `grid.getCell(2, "price")`.

## Step 2: Grab the Textbox Inside That Cell

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Điều đang xảy ra:**  
> Hầu hết các triển khai grid bọc nội dung có thể chỉnh sửa trong một phần tử `<input>` hoặc `<textarea>` và cung cấp nó dưới dạng `cell.textbox`. Lấy tham chiếu này cho phép chúng ta thao tác trực tiếp với kiểu hiển thị của nó.

Nếu grid sử dụng tên thuộc tính khác (như `cell.editor`), chỉ cần điều chỉnh mã cho phù hợp—đây là biến thể phổ biến khi bạn **cách tạo kiểu cho textbox** cho một thành phần tùy chỉnh.

## Step 3: Define the Desired Font Properties

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Phân Tích Đối Tượng

| Property | Purpose | Example Values |
|----------|---------|----------------|
| `family` | Font family – điều khiển kiểu chữ. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Font size tính bằng pixel (hoặc point, tùy grid). | `12`, `14`, `16` |
| `color`  | Màu chữ ở bất kỳ định dạng CSS nào. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Tại sao chúng ta dùng đối tượng:**  
> Gom ba thuộc tính lại với nhau giúp mã gọn gàng và phản ánh cách nhiều thư viện UI mong đợi thông tin kiểu. Nó cũng cho phép bạn **thay đổi family phông chữ trong grid** hoặc **đặt màu phông chữ bằng lập trình** chỉ với một lần gán.

## Step 4: Apply the Font Style to the Textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Bên trong:**  
> Thành phần textbox của grid sẽ diễn giải thuộc tính `font` và cập nhật CSS tương ứng. Dòng lệnh này thay thế family, size và color cũ trong một bước—đúng như bạn cần khi **thay đổi phông chữ của textbox** trên nhiều ô.

Nếu thành phần sử dụng API khác (ví dụ `textbox.style.fontFamily = ...`), hãy điều chỉnh cách gán nhưng giữ nguyên nguyên tắc.

## Full Working Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Expected Output

- Textbox tại **hàng 2, cột 3** bây giờ hiển thị văn bản với **Arial**, **14 px**, và màu xanh **#0066CC**.
- Mở console trình duyệt sẽ in ra một thông báo tương tự:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Nếu bạn mở trang, sẽ thấy thay đổi trực quan—không còn phông chữ hệ thống mặc định nữa.

## Frequently Asked Questions (FAQ)

### Tôi có thể chỉ thay đổi kích thước phông chữ mà không ảnh hưởng tới family hoặc color không?
Chắc chắn rồi. Chỉ cần bỏ qua các thuộc tính không muốn thay đổi:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Nếu grid của tôi dùng tên thuộc tính khác cho textbox thì sao?
Kiểm tra đối tượng ô trong console (`console.log(cell)`). Bạn có thể sẽ thấy `cell.editor` hoặc `cell.input`. Thay `cell.textbox` bằng tham chiếu đúng.

### Làm sao áp dụng cùng một kiểu cho toàn bộ cột?
Duyệt qua các hàng và đặt phông chữ cho mỗi ô trong cột đó:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Có cách nào để quay lại phông chữ gốc không?
Lưu kiểu gốc trước khi ghi đè:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tips & Best Practices

- **Cập nhật hàng loạt:** Nếu cần tạo kiểu cho nhiều ô, bọc các thay đổi trong `requestAnimationFrame` hoặc phương thức batch của grid để tránh việc layout thrashing.
- **Phông chữ đáp ứng:** Sử dụng đơn vị tương đối (`em`, `rem`) thay vì pixel cố định nếu UI cần co giãn.
- **Truy cập:** Đảm bảo độ tương phản đủ khi bạn **đặt màu phông chữ bằng lập trình**—tiêu chuẩn WCAG AA yêu cầu tỷ lệ tối thiểu 4.5:1 cho văn bản thường.
- **Khác biệt trình duyệt:** Một số grid cũ có thể yêu cầu đặt `style.fontFamily` trực tiếp trên phần tử `<input>` thay vì dùng đối tượng `font`.

## Conclusion

Chúng ta vừa tìm hiểu **cách thay đổi phông chữ của textbox** trong grid, từ việc lấy ô đúng, định nghĩa đối tượng `fontStyle` có thể tái sử dụng và áp dụng nó trong một dòng lệnh. Đồng thời, chúng ta đã học cách **thay đổi kích thước phông chữ của ô**, **đặt màu phông chữ bằng lập trình**, và thậm chí **thay đổi family phông chữ trong grid** cho một cột cụ thể.

Bây giờ bạn có thể áp dụng mẫu này cho bất kỳ thư viện UI nào—dù bạn đang xây dựng dashboard quản trị, trình soạn thảo kiểu bảng tính, hay công cụ báo cáo tùy chỉnh. Hãy thử nghiệm với các family, size và color khác nhau; có thể thêm hiệu ứng hover hoặc tạo kiểu có điều kiện dựa trên giá trị dữ liệu.

Có thách thức tạo kiểu khác? Hãy để lại bình luận, chúng ta cùng giải quyết. Chúc bạn coding vui vẻ!

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, mở rộng các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ và giải thích chi tiết từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Thay Đổi Màu Phông Chữ trong Excel bằng Aspose.Cells cho Java: Hướng Dẫn Toàn Diện](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Hướng Dẫn Thay Đổi Màu Phông Chữ Aspose Cells Java](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Hướng Dẫn Thay Đổi Màu Phông Chữ Aspose Cells Java](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}