---
category: general
date: 2026-07-03
description: Hướng dẫn Aspose Cells GridJs cho thấy cách xuất dữ liệu Excel sang JSON
  và xuất worksheet sang JSON một cách hiệu quả bằng tải lười.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: vi
og_description: Hướng dẫn Aspose Cells GridJs giải thích cách xuất dữ liệu Excel sang
  JSON và xuất worksheet sang JSON với tải lười cho các bảng tính lớn.
og_title: Hướng dẫn Aspose Cells GridJs – Xuất dữ liệu Excel sang JSON
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Hướng dẫn Aspose Cells GridJs – Xuất dữ liệu Excel sang JSON với tải lười
url: /vi/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng dẫn Aspose Cells GridJs – Xuất dữ liệu Excel dưới dạng JSON với tải lười

Bạn đã bao giờ tự hỏi làm thế nào **xuất dữ liệu Excel dưới dạng JSON** từ một bảng tính khổng lồ mà không làm trình duyệt bị treo? Trong hướng dẫn Aspose Cells GridJs này, chúng ta sẽ đi qua một giải pháp hoàn chỉnh, sẵn sàng chạy, cho phép bạn **xuất worksheet thành JSON** bằng cách tải lười, vì vậy chỉ những hàng bạn cần mới được lấy khi yêu cầu.

Nếu bạn đã phải vật lộn với các tệp `.xlsx` rất lớn và phía client cứ bị đóng băng, bạn không phải là người duy nhất. Tin tốt? Cách tiếp cận chúng tôi trình bày ở đây vừa nhẹ nhàng vừa có khả năng mở rộng, và bạn có thể đưa nó vào bất kỳ dự án Python nào đã sử dụng thư viện Aspose.Cells.

## Những gì hướng dẫn này sẽ đề cập

Trong vài phút tới, bạn sẽ học được cách:

1. Tải một workbook lớn bằng Aspose.Cells.  
2. Bật tải lười cho GridJs để server truyền các hàng theo từng khối.  
3. Xuất cấu hình GridJs ra tệp JSON mà front‑end có thể tiêu thụ.  
4. Điều chỉnh kích thước khối để đạt hiệu năng tối ưu.  
5. Kiểm tra kết quả và tích hợp nó vào một trang HTML đơn giản.

Không có dịch vụ bên ngoài, không có phép thuật ẩn—chỉ có Python thuần và API Aspose.Cells. Khi kết thúc, bạn sẽ có một **pipeline xuất worksheet thành JSON** hoàn chỉnh mà có thể áp dụng cho dashboard, công cụ báo cáo, hoặc bất kỳ thành phần data‑grid nào.

### Yêu cầu trước

- Python 3.8+ đã được cài đặt trên máy.  
- Gói `asposecells` (bạn có thể `pip install aspose-cells`).  
- Một tệp Excel có kích thước đáng kể (ví dụ: `large-data.xlsx`) đặt trong thư mục đã biết.  
- Kiến thức cơ bản về Python và các khái niệm phát triển web.

Nếu bất kỳ mục nào trên còn lạ, đừng lo—mỗi bước đều có phần giải thích “tại sao” ngắn gọn để bạn hiểu lý do đằng sau mã.

---

## Bước 1: Cài đặt và import Aspose.Cells

Đầu tiên, chúng ta cần thư viện Aspose.Cells. Đây là sản phẩm thương mại, nhưng bản dùng thử miễn phí vẫn đủ cho việc phát triển.

```bash
pip install aspose-cells
```

Bây giờ import các lớp cần thiết vào script của bạn.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Tại sao điều này quan trọng:** Import `Workbook` cho phép bạn truy cập vào engine hiệu năng cao, đọc trực tiếp các tệp Excel vào bộ nhớ, bỏ qua cách tiếp cận chậm hơn của `openpyxl`.

## Bước 2: Tải workbook chứa bộ dữ liệu lớn

Với thư viện đã sẵn sàng, chỉ cần trỏ tới tệp Excel của bạn. Đường dẫn có thể là tuyệt đối hoặc tương đối; chỉ cần chắc chắn tệp tồn tại.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Mẹo chuyên nghiệp:** Nếu workbook của bạn lớn hơn vài trăm megabyte, hãy cân nhắc tăng giới hạn bộ nhớ của tiến trình Python hoặc dùng interpreter 64‑bit để tránh `MemoryError`.

## Bước 3: Bật tải lười cho GridJs

GridJs là thành phần lưới JavaScript của Aspose. Tải lười yêu cầu server chỉ gửi một phần nhỏ các hàng—hoàn hảo cho các sheet khổng lồ.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Tại sao cần tải lười?** Nếu không, toàn bộ worksheet sẽ được tuần tự hoá thành JSON một lần, dễ dàng vượt quá giới hạn bộ nhớ của trình duyệt. Khi đặt `LazyLoadingChunkSize` thành 500, mỗi yêu cầu chỉ mang một payload có thể quản lý được.

## Bước 4: Xuất cấu hình GridJs ra JSON

Bây giờ chúng ta yêu cầu Aspose tạo ra JSON mà thành phần GridJs phía front‑end mong đợi. Đây là phần cốt lõi của thao tác **export excel data json**.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Phương thức `ExportGridJsJson` trả về một đối tượng `bytes` chứa biểu diễn JSON của worksheet, sẵn sàng để lưu hoặc stream.

## Bước 5: Ghi JSON vào tệp (hoặc stream)

Để kiểm tra nhanh, ghi JSON ra đĩa. Trong một API production, bạn sẽ trả về trực tiếp từ endpoint Flask/Django.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Bạn sẽ thấy gì:** Mở `lazygrid.json` sẽ hiển thị cấu trúc có `columns`, `rows`, và siêu dữ liệu phân trang. Mảng `rows` ban đầu sẽ rỗng; GridJs sẽ yêu cầu khối đầu tiên khi trang tải.

## Bước 6: Kết nối JSON vào một trang HTML đơn giản (tùy chọn)

Nếu muốn xem lưới hoạt động, tạo một tệp HTML nhỏ tải GridJs từ CDN và trỏ tới JSON đã tạo.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Tại sao đưa mục này vào?** Nó minh họa vòng tròn đầy đủ: Python tạo JSON, trình duyệt tải nó, và GridJs render dữ liệu từng khối. Bạn có thể thử các giá trị `LazyLoadingChunkSize` khác nhau để tìm “sweet spot” cho mạng của mình.

## Bước 7: Kiểm tra và khắc phục sự cố

Chạy script Python:

```bash
python export_lazy_grid.py
```

Bạn sẽ thấy thông báo thành công và một tệp `lazygrid.json`. Mở tệp HTML trong trình duyệt; lưới sẽ hiển thị ngay 500 hàng đầu tiên, với các điều khiển phân trang để tải thêm.

Nếu lưới hiện ra trống:

- **Kiểm tra kích thước tệp JSON** – tệp 0 byte thường nghĩa là đường dẫn workbook sai.  
- **Xác nhận tải lười đã được bật** – cờ `LazyLoading` phải là `True`.  
- **Kiểm tra console của trình duyệt** – bất kỳ lỗi CORS hoặc 404 nào đều cho thấy JSON không được phục vụ đúng cách.

---

## Các biến thể phổ biến và trường hợp góc

### Xuất một worksheet cụ thể

Ví dụ trên luôn dùng worksheet đầu tiên (`Worksheets[0]`). Để xuất một sheet khác, chỉ cần thay đổi chỉ số hoặc dùng tên sheet:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Thay đổi kích thước khối cho tệp siêu lớn

Đối với các tệp có hàng triệu dòng, kích thước khối 500 có thể vẫn quá nhỏ, gây nhiều vòng truy vấn. Bạn có thể tăng lên 2000 hoặc hơn, nhưng nhớ rằng khối lớn hơn sẽ tiêu tốn băng thông nhiều hơn cho mỗi yêu cầu.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Xuất ra stream thay vì tệp

Nếu API của bạn trả về JSON trực tiếp, không cần ghi ra đĩa:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Xử lý công thức và định dạng

Mặc định, `ExportGridJsJson` bao gồm giá trị đã tính của công thức. Nếu bạn cần công thức thô, đặt:

```python
grid_options.ExportFormulas = True
```

---

## Kết luận

Trong **hướng dẫn Aspose Cells GridJs** này, chúng ta đã bao quát mọi thứ cần thiết để **export Excel data JSON** và **export worksheet to JSON** với tải lười. Từ việc cài đặt Aspose.Cells, bật tải lười, tạo JSON, đến việc kết nối nó với một trang HTML đơn giản, bạn giờ đã có một mẫu full‑stack có thể mở rộng một cách nhẹ nhàng với các bảng tính khổng lồ.

Hãy thử nghiệm—điều chỉnh kích thước khối, trỏ tới các worksheet khác, hoặc tích hợp endpoint vào ứng dụng Flask hoặc Django. Khả năng là vô hạn, và lợi ích về hiệu năng là ngay lập tức.

Sẵn sàng bước tiếp? Hãy thử thêm tính năng sắp xếp cột, renderer ô tùy chỉnh, hoặc thậm chí lọc phía server để làm cho lưới GridJs của bạn thực sự tương tác. Nếu gặp khó khăn, hãy để lại bình luận bên dưới; chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu hoàn chỉnh cùng giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}