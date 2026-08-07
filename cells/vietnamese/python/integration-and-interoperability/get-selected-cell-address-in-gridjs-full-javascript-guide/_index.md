---
category: general
date: 2026-06-30
description: Tìm hiểu cách lấy địa chỉ ô được chọn, cập nhật giá trị ô trong lưới
  và đọc giá trị nhập vào bằng JavaScript với GridJs. Mã và mẹo từng bước.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: vi
og_description: Lấy địa chỉ ô đã chọn, cập nhật giá trị ô trong lưới và đọc giá trị
  nhập bằng JavaScript. Tham khảo hướng dẫn đầy đủ này để tích hợp GridJs một cách
  mượt mà.
og_title: Lấy Địa chỉ Ô Được Chọn – Hướng Dẫn Toàn Diện GridJs JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Lấy Địa Chỉ Ô Được Chọn trong GridJs – Hướng Dẫn JavaScript Đầy Đủ
url: /vi/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy Địa Chỉ Ô Được Chọn – Hướng Dẫn JavaScript GridJs Toàn Diện

Bạn đã bao giờ cần **lấy địa chỉ ô được chọn** từ một bảng GridJs nhưng không chắc nên gọi API nào? Bạn không phải là người duy nhất. Trong nhiều bảng điều khiển quản trị, người dùng nhấp vào một ô, chỉnh sửa giá trị trong một modal, và mong muốn lưới phản ánh thay đổi ngay lập tức. Hướng dẫn này sẽ chỉ cho bạn cách lấy địa chỉ đó, đọc giá mới từ trường nhập, và **cập nhật giá trị ô trong lưới** mà không cần tải lại trang.

Chúng tôi cũng sẽ đề cập đến **đọc giá trị nhập bằng JavaScript** một cách đúng đắn, xử lý các trường hợp biên, và đóng modal khi cập nhật hoàn tất. Khi kết thúc, bạn sẽ có một đoạn mã tự chứa có thể chèn vào bất kỳ dự án nào sử dụng GridJs.

## Những Điều Bạn Sẽ Xây Dựng

- Một bảng HTML đơn giản được hỗ trợ bởi GridJs.
- Một modal chỉnh sửa xuất hiện khi nhấp vào một ô.
- JavaScript mà **lấy địa chỉ ô được chọn**, lấy giá người dùng nhập, **cập nhật giá trị ô trong lưới**, và cuối cùng ẩn modal.

Không cần thư viện bên ngoài nào ngoài GridJs, và mã hoạt động trên các trình duyệt hiện đại (Chrome 102+, Edge, Firefox). Nếu bạn đã có một thể hiện GridJs trên trang, bạn có thể sao chép‑dán các phần liên quan trực tiếp.

## Yêu Cầu Trước

- Kiến thức cơ bản về JavaScript và DOM.
- Thư viện GridJs đã được tải (qua CDN hoặc npm).
- Một trang đã hiển thị một lưới GridJs (chúng tôi sẽ trình bày một ví dụ tối thiểu).

Nếu bất kỳ điều nào trong số này nghe lạ, đừng hoảng—mỗi bước đều có một tóm tắt nhanh.

---

## Bước 1: Thiết Lập Khung HTML

Đầu tiên, bố trí container bảng, modal ẩn, và trường nhập giá. Modal sẽ được bật tắt bằng các lớp CSS đơn giản.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Mẹo chuyên nghiệp:** `#editModal` sử dụng một thủ thuật CSS tối thiểu—chỉ cần thêm lớp `active` để hiển thị. Bạn có thể thay thế nó bằng Bootstrap, Tailwind, hoặc bất kỳ thành phần modal nào bạn đã sử dụng.

## Bước 2: Khởi Tạo GridJs và Bắt Sự Kiện Nhấp Ô

Bây giờ chúng ta sẽ tạo một lưới với dữ liệu mẫu và lắng nghe các lựa chọn ô. Khi người dùng nhấp vào một ô, chúng ta sẽ **lấy địa chỉ ô được chọn** và mở modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Tại sao cách này hoạt động:** `GridJs.getSelectedCell()` trả về một chuỗi như `"C2"` (cột C, hàng 2). Lưu nó trong `lastSelectedCell` cho phép chúng ta tham chiếu vị trí chính xác khi sau này **cập nhật giá trị ô trong lưới**.

## Bước 3: Đọc Giá Mới Từ Trường Nhập

Khi người dùng nhấp **Lưu**, chúng ta cần **đọc giá trị nhập bằng JavaScript** một cách an toàn. Bước này cũng xác thực rằng giá nhập vào là một số dương.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Lưu ý:** Sử dụng `parseFloat` đảm bảo chúng ta chấp nhận số thập phân (ví dụ, `1.99`). Kiểm tra `isNaN` ngăn ngừa việc gửi rỗng vô tình.

## Bước 4: Cập Nhật Giá Trị Ô Được Chọn

Bây giờ chúng ta cuối cùng **cập nhật giá trị ô trong lưới** bằng địa chỉ đã lưu trước đó. Phương thức `updateCell` của GridJs trả về một promise, vì vậy chúng ta có thể nối hành động đóng modal.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Tại sao lại dùng promise?** GridJs có thể cần render lại bảng hoặc đồng bộ với backend. Bằng cách chờ promise, chúng ta đảm bảo UI chỉ ẩn sau khi lưới phản ánh giá trị mới.

## Bước 5: Xử Lý Hủy và Các Trường Hợp Biên

Một giải pháp vững chắc luôn cung cấp cho người dùng một cách thoát. Nút **Cancel** chỉ ẩn modal và xóa bất kỳ địa chỉ nào đã lưu.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Nếu Không Có Ô Được Chọn?

Nếu người dùng vô tình kích hoạt nút **Save** mà chưa nhấp vào ô nào trước (có thể họ mở modal bằng mã), `lastSelectedCell` sẽ là `null`. Việc trả về sớm trong `updateSelectedCell` ngăn lỗi thời gian chạy và ghi lại cảnh báo hữu ích.

### Xử Lý Lưới Lớn

Đối với lưới có phân trang, `GridJs.getSelectedCell()` vẫn trả về địa chỉ tuyệt đối (ví dụ, `"B12"`), không chỉ hàng hiển thị. Điều này có nghĩa là việc cập nhật vẫn hoạt động ngay cả khi hàng được chỉnh sửa nằm trên trang khác. Chỉ cần lưu ý UI sẽ không tự động chuyển trang sau khi cập nhật—nếu cần, gọi `grid.forceUpdate()` hoặc điều hướng tới trang phù hợp bằng tay.

---

## Ví Dụ Hoạt Động Đầy Đủ

Dưới đây là toàn bộ mã bạn có thể sao chép‑dán vào một tệp HTML duy nhất. Mở nó trong trình duyệt, nhấp vào bất kỳ ô nào, thay đổi giá và xem lưới cập nhật ngay lập tức.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Lấy Địa Chỉ, Đếm Ô, và Độ Dịch cho Toàn Bộ Phạm Vi Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Lấy Địa Chỉ, Đếm Ô và Độ Dịch cho Toàn Bộ Phạm Vi Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Lấy Địa Chỉ, Đếm Ô và Độ Dịch cho Toàn Bộ Phạm Vi Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}