---
category: general
date: 2026-06-08
description: Thêm menu ngữ cảnh tùy chỉnh vào GridJs và xuất lưới ra CSV dưới dạng
  tệp blob có thể tải xuống. Hãy làm theo hướng dẫn từng bước này để có một ví dụ
  hoạt động đầy đủ.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: vi
og_description: Thêm menu ngữ cảnh tùy chỉnh vào GridJs và xuất lưới ra CSV bằng tệp
  blob tải xuống CSV. Tìm hiểu cách triển khai đầy đủ trong chưa đầy 10 phút.
og_title: Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs – Hướng Dẫn Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs – Hướng Dẫn Toàn Diện
url: /vi/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs – Hướng Dẫn Toàn Diện

Bạn muốn **thêm menu ngữ cảnh tùy chỉnh** vào một thành phần GridJs? Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách thực hiện điều đó, và cho bạn biết cách **xuất grid ra CSV** bằng cách sử dụng **download CSV file blob**. Dù bạn đang xây dựng một bảng điều khiển admin nhanh chóng hay một dashboard báo cáo đầy đủ, một menu chuột phải cho phép người dùng trích xuất dữ liệu dưới dạng CSV có thể tăng đáng kể năng suất làm việc.

Chúng tôi sẽ bao quát mọi thứ bạn cần: phần Python với Flask, trình xử lý JavaScript tạo Blob, và HTML/JS mà GridJs sinh ra. Khi kết thúc, bạn sẽ có một ví dụ tự chứa mà có thể đưa vào bất kỳ dự án nào.

---

## Những Gì Bạn Cần

- **Python 3.9+** và **Flask** đã được cài đặt (`pip install flask`).
- Bộ bao bọc Python **gridjs** (hoặc thư viện JavaScript trực tiếp) – trong hướng dẫn này chúng tôi sẽ giả sử một wrapper Python mỏng phản ánh API của JavaScript.
- Kiến thức cơ bản về **async JavaScript** (`fetch`, `Promise`) – nhưng đừng lo, chúng tôi sẽ giải thích từng dòng.
- Một trình soạn thảo mà bạn thích (VS Code, PyCharm, hoặc thậm chí một trình soạn thảo văn bản đơn giản).

Đó là tất cả. Không cần công cụ xây dựng front‑end bổ sung, không cần “dance” Node npm. Chỉ cần Flask đơn giản phục vụ HTML mà GridJs tạo ra.

---

## Thêm Menu Ngữ Cảnh Tùy Chỉnh vào GridJs

Điều đầu tiên bạn phải làm là thông báo cho GridJs biết bạn muốn một menu chuột phải tùy chỉnh. Mặc định GridJs đi kèm một bộ tối thiểu (copy, paste, v.v.), nhưng bạn có thể thay thế hoàn toàn.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Tại sao điều này quan trọng:**  
Việc thiết lập `CustomContextMenu` thay thế danh sách mặc định bằng danh sách bạn cung cấp. Chuỗi `"Export CSV"` chỉ là một nhãn – công việc thực sự diễn ra khi người dùng nhấp vào, và chúng tôi sẽ kết nối nó trong bước tiếp theo.

> *Mẹo:* Giữ danh sách ngắn. Một menu ngữ cảnh lộn xộn làm mất mục đích của các hành động nhanh.

---

## Xuất Grid ra CSV với Tải Xuống Blob

Bây giờ menu đã tồn tại, chúng ta cần một trình xử lý JavaScript giao tiếp với server, lấy CSV, chuyển nó thành một **Blob**, và buộc tải xuống. Đây là nơi cụm từ **download CSV file blob** xuất hiện.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Phân Tích Trình Xử Lý

| Dòng | Mô tả |
|------|------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Gọi một route Flask (`/export/csv`) và truyền tên sheet dưới dạng query string. |
| `.then(r => r.blob())` | Chuyển đổi phản hồi HTTP thành một **Blob** – về cơ bản là một container nhị phân cho dữ liệu CSV. |
| `URL.createObjectURL(b)` | Tạo một URL tạm thời mà trình duyệt có thể xem như một tệp. |
| `a.download = cell.sheetName + ".csv"` | Đặt tên tệp mà người dùng sẽ thấy trong hộp thoại tải xuống. |
| `a.click()` | Chương trình tự động click vào thẻ anchor ẩn, kích hoạt trình duyệt tải xuống Blob. |

> **Tại sao lại dùng Blob?**  
> Trình duyệt không thể tải trực tiếp văn bản thô trả về từ `fetch` mà không chuyển nó thành một đối tượng giống tệp. Thủ thuật Blob‑URL là cách đáng tin cậy nhất, hoạt động trên mọi trình duyệt, để kích hoạt **download CSV file blob** mà không cần làm mới trang.

---

## Cài Đặt Backend Flask

Trình xử lý front‑end mong đợi một endpoint tại `/export/csv`. Dưới đây là một view Flask tối thiểu lấy tên sheet, truy xuất dữ liệu từ workbook, và trả về CSV dưới dạng stream.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Các Điểm Chính

- `io.StringIO` cho phép chúng ta tạo CSV trong bộ nhớ mà không cần chạm tới hệ thống tệp.
- `Content‑Disposition` thông báo cho trình duyệt rằng tệp là một đính kèm và đề xuất một tên tệp. Mặc dù front‑end cũng đặt `a.download`, việc có nó ở phía server cung cấp một phương án dự phòng cho các client không hỗ trợ JS.
- Route này được thiết kế đơn giản; bạn có thể thêm xác thực, kiểm tra quyền, hoặc streaming cho các bộ dữ liệu lớn sau này.

---

## Render Grid trên Client

Với menu ngữ cảnh và backend đã sẵn sàng, phần cuối cùng là render thành phần GridJs và gửi HTML/JS tới trình duyệt.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Trong một view Flask, bạn thường sẽ làm như sau:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Khi trang tải, GridJs xây dựng bảng, chèn menu ngữ cảnh tùy chỉnh, và trình xử lý JavaScript chúng ta đã định nghĩa trước đó sẵn sàng hoạt động. Nhấp chuột phải vào bất kỳ ô nào, chọn **Export CSV**, và xem trình duyệt tải xuống một tệp có tên trùng với sheet.

---

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Tập Tin)

Dưới đây là mã hoàn chỉnh, có thể chạy được mà bạn có thể sao chép‑dán vào một thư mục mới. Cài đặt Flask (`pip install flask`) và chạy `python app.py`.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tải Các Tập Tin Csv Với Trình Phân Tích Tùy Chỉnh Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Mã Xuất Csv Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Xuất Excel Csv Các Dòng Trống Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}