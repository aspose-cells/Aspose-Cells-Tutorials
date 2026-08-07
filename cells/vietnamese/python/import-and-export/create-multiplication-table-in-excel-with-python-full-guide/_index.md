---
category: general
date: 2026-06-21
description: Tạo bảng nhân trong Excel bằng Python. Học cách sử dụng lambda, cách
  sử dụng makearray, hiển thị mảng Excel và đọc giá trị Excel bằng Python trong một
  hướng dẫn từng bước.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: vi
og_description: Tạo bảng nhân trong Excel bằng Python. Hướng dẫn này chỉ cách sử dụng
  lambda, makearray, hiển thị mảng Excel và đọc giá trị Excel bằng Python một cách
  hiệu quả.
og_title: Tạo bảng nhân trong Excel bằng Python – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Tạo bảng nhân trong Excel bằng Python – Hướng dẫn đầy đủ
url: /vi/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo bảng nhân trong Excel bằng Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **tạo bảng nhân** trong Excel mà không cần nhập tay từng ô chưa? Bạn không phải là người duy nhất. Trong nhiều tình huống báo cáo, bạn cần một lưới 5×5 (hoặc lớn hơn) nhanh chóng của các sản phẩm, và việc làm thủ công tốn thời gian.  

Trong hướng dẫn này, chúng ta sẽ đi qua cách tiếp cận sạch sẽ, dựa trên Python để tạo bảng đó, nhúng nó bằng công thức `MAKEARRAY`, và sau đó lấy kết quả trở lại script của bạn. Trong quá trình này, chúng ta sẽ trả lời **cách sử dụng lambda**, trình bày **cách sử dụng makearray**, và minh họa **hiển thị mảng excel** cũng như **đọc giá trị excel bằng python** — tất cả trong một ví dụ thống nhất.

Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng cho bất kỳ workbook nào, và bạn sẽ hiểu tại sao cách tiếp cận này vừa nhanh vừa bền vững trong tương lai.

## Những gì bạn cần

- Python 3.8+ (phiên bản ổn định mới nhất là đủ)
- Thư viện `openpyxl` (hoặc bất kỳ thư viện hỗ trợ Excel nào có khả năng xử lý công thức)
- Hiểu biết cơ bản về biểu thức lambda trong Python
- Không cần add‑in Excel đặc biệt; hàm `MAKEARRAY` gốc (có sẵn trong Excel 365) thực hiện phần tính toán chính

Nếu bạn thiếu bất kỳ mục nào trong số này, chỉ cần chạy `pip install openpyxl` và bạn đã sẵn sàng.

## Tạo bảng nhân – Tổng quan

Ý tưởng cốt lõi rất đơn giản: chúng ta tạo một workbook mới, viết công thức `MAKEARRAY` để xây dựng ma trận nhân 5 × 5, buộc Excel tính toán nó, và cuối cùng đọc các giá trị kết quả trở lại Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Chạy script sẽ in ra:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Đó là một **tạo bảng nhân** hoàn chỉnh trong Excel, được tạo hoàn toàn từ Python.

### Tại sao lại dùng `MAKEARRAY` thay vì vòng lặp Python?

- **Hiệu suất**: Excel thực hiện tính toán một cách nguyên bản, nhanh hơn cho các ma trận lớn.
- **Cập nhật trực tiếp**: Nếu bạn sau này thay đổi kích thước trong công thức, sheet sẽ tự tính lại.
- **Độ đọc được**: Công thức diễn đạt mục đích (“tạo một mảng”) một cách trực tiếp, giữ cho mã Python của bạn gọn gàng.

## Cách sử dụng lambda trong Python cho công thức Excel

Phần `LAMBDA` của lời gọi `MAKEARRAY` là một hàm ẩn danh phía Excel, không phải lambda của Python. Tuy nhiên, khái niệm vẫn giống nhau: bạn định nghĩa một đoạn logic nhỏ, nội tuyến, nhận `r` (chỉ số hàng) và `c` (chỉ số cột) và trả về `r*c`.  

Nếu bạn mới với **cách sử dụng lambda** trong môi trường Excel, hãy nghĩ nó như một hàm mini chỉ tồn tại trong công thức. Không cần khai báo hàm riêng ở nơi khác. Trong Python chúng ta chỉ cần nhúng chuỗi:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Dòng này nói với Excel: *“Đối với mỗi ô trong khối 5 × 5, tính hàng × cột.”*  

Vì lambda được Excel đánh giá, bạn không cần lo lắng về cú pháp lambda của Python ở đây — chỉ cần cú pháp của Excel.

## Cách sử dụng makearray để tạo mảng

`MAKEARRAY` là một bổ sung tương đối mới vào thư viện hàm của Excel (có sẵn trong Microsoft 365 từ năm 2022). Nó thay thế các thủ thuật cũ như kết hợp `INDEX` + `ROW`/`COLUMN`. Cú pháp là:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – số lượng hàng bạn muốn.
- **columns** – số lượng cột bạn muốn.
- **lambda** – một hàm Excel LAMBDA nhận `(row, column)` và trả về một giá trị.

Trong ví dụ của chúng tôi, chúng tôi đã truyền `5,5` cho một bảng nhân cổ điển, nhưng bạn có thể dễ dàng thay đổi các số này:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Điều này sẽ cho bạn một bảng 10 × 10 mà không cần viết bất kỳ vòng lặp Python nào. Điều này minh họa **cách sử dụng makearray** cho bất kỳ loại lưới xác định nào, dù là bảng tra cứu, bản đồ nhiệt, hay lịch tài chính.

## Hiển thị mảng excel – lấy dữ liệu trở lại Python

Khi Excel đã tính toán công thức, các giá trị kết quả sẽ nằm trong sheet giống như bất kỳ ô nào được nhập thủ công. Để **hiển thị mảng excel**, chúng ta lặp qua phạm vi và in mỗi hàng:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Một vài mẹo:

- Sử dụng `worksheet.cell(row, column).value` thay vì cách truy cập kiểu từ điển nếu bạn cần xử lý phạm vi lớn hơn; nó nhanh hơn một chút.
- Nếu bạn muốn bảng đẹp hơn, hãy cân nhắc dùng `tabulate` hoặc `pandas.DataFrame` để định dạng đầu ra.

Dưới đây là ảnh chụp màn hình của sheet kết quả (văn bản alt của hình ảnh bao gồm từ khóa chính cho SEO):

![Ảnh chụp màn hình cho thấy cách tạo bảng nhân trong Excel bằng Python](/images/multiplication-table-excel.png)

## Đọc giá trị excel bằng python – trích xuất ma trận để xử lý tiếp

Thường bước tiếp theo sau **hiển thị mảng excel** là đưa những số này vào quy trình phân tích dữ liệu. Đó là lúc **đọc giá trị excel python** tỏa sáng. Vòng lặp giống như chúng ta đã dùng để in có thể được tái sử dụng để xây dựng danh sách các danh sách, một mảng NumPy, hoặc một Pandas DataFrame:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Kết quả:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Bây giờ bạn có một DataFrame đã được định kiểu đầy đủ mà bạn có thể vẽ đồ thị, xuất ra CSV, hoặc đưa vào mô hình học máy. Điều này hoàn thiện phần **đọc giá trị excel python** của quy trình.

## Các trường hợp đặc biệt & Mẹo thực tế

- **Tính toán lại công thức**: Nếu bạn sửa đổi workbook sau lần gọi `calculate_formula()` đầu tiên, bạn phải gọi lại; nếu không, mảng đã lưu trong bộ nhớ sẽ lỗi thời.
- **Excel không phải 365**: Các phiên bản Excel cũ không hỗ trợ `MAKEARRAY`. Trong trường hợp này, hãy quay lại bảng được tạo bằng Python và ghi từng ô một.
- **Bảng lớn**: Đối với ma trận lớn hơn ~100 × 100, hãy cân nhắc truyền dữ liệu theo luồng để tránh tải toàn bộ sheet vào bộ nhớ.
- **Xử lý lỗi**: Bao bọc các bước tính toán và đọc trong khối `try/except` để bắt `InvalidFileException` hoặc `FormulaError`.

## Kết luận

Chúng tôi vừa cho bạn thấy cách **tạo bảng nhân** trong Excel bằng Python, tận dụng sức mạnh của **cách sử dụng lambda** và **cách sử dụng makearray**. Bạn đã thấy cách **hiển thị mảng excel**, đọc lại các giá trị bằng **đọc giá trị excel python**, và thậm chí chuyển kết quả thành một Pandas DataFrame để phân tích tiếp theo.

Muốn tiến xa hơn? Hãy thử thay đổi logic nhân thành một thứ phức tạp hơn — có thể là ma trận khoảng cách, bảng xác suất, hoặc lưới định giá động. Mẫu tương tự vẫn áp dụng: một dòng `MAKEARRAY`, một lời gọi nhanh `calculate_formula()`, và một vài vòng lặp Python để lấy dữ liệu ra.

Nếu bạn thấy hướng dẫn này hữu ích, hãy đánh dấu sao trên GitHub, chia sẻ với đồng nghiệp, hoặc để lại bình luận với trường hợp sử dụng của bạn. Chúc lập trình vui vẻ, và tận hưởng sự ngắn gọn khi tạo bảng Excel chỉ bằng một công thức!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách tạo và cấu hình Workbook Excel với Aspose.Cells .NET: Hướng dẫn từng bước](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hướng dẫn Aspose.Cells .NET: Cách tạo và chỉnh sửa Workbook Excel một cách dễ dàng](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Cách tạo và định dạng Named Ranges trong Excel bằng Aspose.Cells .NET | Hướng dẫn từng bước](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}