---
category: general
date: 2026-06-30
description: Thêm menu ngữ cảnh tùy chỉnh vào lưới Excel trong Python và ghi giá trị
  vào ô Excel khi lưu tệp đã cập nhật. Học cách tạo menu chuột phải và cập nhật giá
  trị ô theo phong cách Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: vi
og_description: Thêm menu ngữ cảnh tùy chỉnh trong Python để ghi giá trị vào ô Excel
  và lưu tệp Excel đã cập nhật. Hướng dẫn này sẽ chỉ cho bạn cách tạo menu nhấp chuột
  phải với GridJs.
og_title: Thêm Menu Ngữ Cảnh Tùy Chỉnh trong Python – Hướng Dẫn Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Thêm menu ngữ cảnh tùy chỉnh trong Python – Hướng dẫn chi tiết
url: /vi/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Menu Ngữ Cảnh Tùy Chỉnh trong Python – Hướng Dẫn Đầy Đủ

Bạn đã bao giờ tự hỏi làm thế nào để **thêm các mục menu ngữ cảnh tùy chỉnh** vào lưới bảng tính mà bạn đang phục vụ từ Python chưa? Có thể bạn cần một nút “Đánh dấu đã xem xét” nhanh chóng xuất hiện khi người dùng nhấp chuột phải vào một ô, ghi giá trị vào ô Excel, và sau đó lưu lại workbook đã cập nhật—tất cả mà không rời khỏi giao diện web.  

Trong tutorial này chúng ta sẽ xây dựng chính xác điều đó: một **menu chuột phải tùy chỉnh** được hỗ trợ bởi GridJs, một handler phía server **ghi giá trị vào ô excel**, và một bước cuối cùng **lưu file excel đã cập nhật** lên đĩa. Khi hoàn thành, bạn sẽ có một mẫu có thể tái sử dụng cho bất kỳ dự án Flask, FastAPI, hay Django nào.

> **Tại sao lại quan tâm?**  
> Thêm menu ngữ cảnh tùy chỉnh giúp hợp lý hoá quy trình xem xét dữ liệu, giảm thiểu việc sao chép‑dán thủ công, và mang lại trải nghiệm cảm giác “gốc” ngay trong lưới. Ngoài ra, bạn sẽ thấy cách **cập nhật giá trị ô python**‑style, một kỹ năng cốt lõi cho mọi tác vụ tự động hoá Excel.

## Các Điều Kiện Cần Có

- Python 3.9+ (code cũng chạy trên 3.10)  
- `openpyxl` để xử lý file Excel  
- `gridjs` wrapper cho Python (hoặc thư viện JS nếu bạn thích phía front‑end)  
- Một framework web cơ bản (ví dụ Flask)  
- Một file workbook tên `sample.xlsx` trong thư mục dự án của bạn  

Nếu bạn thiếu bất kỳ thành phần nào, chạy:

```bash
pip install openpyxl flask gridjs
```

Bây giờ chúng ta bắt đầu.

---

## Bước 1 – Thêm Menu Ngữ Cảnh Tùy Chỉnh: Khởi Tạo GridJs và Gắn Worksheet

Điều đầu tiên bạn cần làm là khởi tạo một instance `GridJs` và chỉ định worksheet mà bạn sẽ làm việc. Đây là nơi cụm từ **add custom context menu** xuất hiện lần đầu trong code, và nó đặt nền tảng cho mọi thứ tiếp theo.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Điều gì đang xảy ra?**  
`grid.set_worksheet(ws)` nói với GridJs sử dụng dữ liệu từ `ws` làm nguồn dữ liệu. Từ đây trở đi, bất kỳ thay đổi nào trong menu ngữ cảnh mà chúng ta thêm sẽ tự động nhắm tới cùng một worksheet, giữ cho UI và file luôn đồng bộ.

> **Mẹo chuyên nghiệp:** Giữ workbook mở ở chế độ đọc/ghi chỉ một lần. Mở lại nhiều lần trong một handler yêu cầu có thể gây ra vấn đề khóa file trên Windows.

---

## Bước 2 – Ghi Giá Trị Vào Ô Excel: Định Nghĩa Hành Động Cho Mục Menu

Giờ lưới đã sẵn sàng, chúng ta cần **write value to excel cell** khi người dùng chọn lệnh tùy chỉnh của chúng ta. Chúng ta sẽ thêm một mục menu có tên “Mark as Reviewed” và gán cho nó một định danh `markReviewed`. Định danh này là thứ mà JavaScript phía client sẽ gửi lại cho server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Tại sao lại dùng định danh tùy chỉnh?**  
Định danh tách biệt văn bản UI khỏi logic server, cho phép bạn thay đổi nhãn mà không cần chạm vào code backend. Nó cũng làm cho thao tác **create right‑click menu** trở nên rõ ràng và có thể tái sử dụng.

---

## Bước 3 – Tạo Menu Chuột Phải: Đăng Ký Handler Phía Server

Với mục menu đã có, chúng ta cần chỉ cho GridJs biết phải làm gì khi người dùng nhấp vào. Đây là nơi chúng ta **create right‑click menu** thực sự gửi một yêu cầu trở lại Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Một vài lưu ý:

1. **`ws[cell_address] = "Reviewed"`** là cách đơn giản nhất để **update cell value python**. Ở mức độ bên dưới, `openpyxl` sẽ chuyển địa chỉ kiểu A1 thành chỉ số hàng/cột.  
2. Handler trả về một payload JSON nhỏ. GridJs mong đợi một chỉ báo trạng thái; bạn có thể mở rộng để bao gồm thông báo lỗi nếu cần.

Bây giờ chúng ta gắn định danh với handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Nếu ô trống hoặc được bảo vệ thì sao?**  
- Các ô trống không vấn đề—`openpyxl` sẽ tạo chúng ngay khi ghi.  
- Đối với sheet được bảo vệ, bạn cần bỏ bảo vệ trước (`ws.protection.sheet = False`) hoặc bắt `PermissionError`.

---

## Bước 4 – Cập Nhật Giá Trị Ô Python: Lưu Thay Đổi Bằng Cách Lưu Workbook

Ghi một giá trị chỉ là một nửa câu chuyện; bạn phải **save updated excel file** để thay đổi tồn tại sau phiên làm việc hiện tại. Đây là nơi chúng ta hoàn thiện vòng quay từ UI tới đĩa.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Tại sao lại lưu vào thư mục riêng?**  
Lưu vào thư mục `output/` giúp giữ nguyên mẫu gốc, hữu ích cho việc truy vết audit. Điều chỉnh đường dẫn cho phù hợp với môi trường triển khai của bạn.

> **Cảnh báo:** Nếu bạn phục vụ nhiều người dùng đồng thời, hãy cân nhắc sử dụng một lock an toàn đa luồng (`threading.Lock`) quanh `wb.save()` để tránh race conditions.

---

## Bước 5 – Tạo JSON Cấu Hình Client và Kết Nối Tất Cả Các Thành Phần

Cuối cùng, chúng ta cần tạo JSON mà instance GridJs phía front‑end sẽ tiêu thụ. JSON này chứa dữ liệu worksheet **và** định nghĩa menu tùy chỉnh.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Khi bạn nhúng `config_json` vào trang HTML, GridJs sẽ hiển thị lưới với mục “Mark as Reviewed” có thể nhấp chuột phải trên mọi ô.

### Ví Dụ Flask Đầy Đủ

Dưới đây là một ứng dụng Flask tối thiểu kết hợp tất cả các phần. Chạy nó, mở `http://localhost:5000` và nhấp chuột phải vào bất kỳ ô nào để thấy menu tùy chỉnh hoạt động.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Kết quả mong đợi:**  
- Nhấp chuột phải vào bất kỳ ô nào → hiện “Mark as Reviewed”.  
- Nhấp vào mục này → nội dung ô thay đổi thành “Reviewed”.  
- File workbook `output/sample-updated.xlsx` bây giờ chứa giá trị mới.

---

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

| Câu hỏi | Câu trả lời |
|----------|------------|
| *Nếu tôi cần nhiều hành động tùy chỉnh thì sao?* | Chỉ cần thêm nhiều đối tượng vào `grid.settings.context_menu.custom_items` và đăng ký mỗi cái với một định danh riêng. |
| *Có thể truyền dữ liệu phụ (ví dụ ID hàng) tới handler không?* | Có. Bao gồm các khóa phụ trong payload JSON phía client, sau đó đọc chúng từ `request` trong `on_custom_command`. |
| *Cách tiếp cận này có tương thích với các framework async không?* | Hoàn toàn tương thích—chỉ cần biến `on_custom_command` thành hàm async và dùng `await wb.save(...)` nếu bạn chuyển sang `aiofiles` hoặc tương tự. |
| *Làm sao để tạo kiểu cho biểu tượng menu?* | Cung cấp bất kỳ tên Material‑Icons nào (`"icon": "edit"`). Front‑end sẽ tự động tải font biểu tượng. |
| *Còn các workbook lớn thì sao?* | Chỉ tải sheet cần thiết, và cân nhắc streaming các hàng bằng `openpyxl.iter_rows()` để giảm mức tiêu thụ bộ nhớ. |

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoàn chỉnh cùng các giải thích từng bước, giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}