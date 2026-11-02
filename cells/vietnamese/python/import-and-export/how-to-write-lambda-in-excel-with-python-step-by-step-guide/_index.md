---
category: general
date: 2026-06-21
description: Học cách viết lambda trong Excel bằng Python. Hướng dẫn này cũng bao
  gồm cách tạo workbook Excel bằng Python và cách đọc các ô bằng Aspose.Cells.
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: vi
og_description: Cách viết lambda trong Excel bằng Python được giải thích. Hãy làm
  theo các bước rõ ràng của chúng tôi để tạo workbook Excel bằng Python, áp dụng BYROW
  và đọc kết quả các ô.
og_title: Cách viết hàm Lambda trong Excel bằng Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: Cách viết Lambda trong Excel bằng Python – Hướng dẫn từng bước
url: /vi/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Viết Lambda trong Excel bằng Python – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi **cách viết lambda** trong công thức Excel khi tự động hoá bảng tính bằng Python chưa? Bạn không đơn độc. Nhiều nhà phát triển gặp khó khăn khi muốn kết hợp sức mạnh của các hàm mảng động mới của Excel với quy trình làm việc dựa trên Python. Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy chính xác cách thực hiện — cùng với các chủ đề **tạo workbook excel python**, **cách đọc ô**, và mẫu hữu ích **cách sử dụng byrow**.

Khi hoàn thành hướng dẫn này, bạn sẽ có một workbook mới, một công thức BYROW sử dụng lambda, và một cách đơn giản để lấy kết quả trở lại script Python của bạn. Không cần bất kỳ add‑in Excel nào, chỉ cần Aspose.Cells cho Python và một chút mã.

## Các Điều Kiện Cần Có

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Python 3.8 hoặc mới hơn được cài đặt.
- Gói `aspose-cells` (`pip install aspose-cells`).
- Kiến thức cơ bản về danh sách và hàm trong Python.
- (Tùy chọn) Một IDE hoặc trình soạn thảo văn bản mà bạn cảm thấy thoải mái.

Đó là tất cả. Nếu có bất kỳ mục nào bạn chưa quen, hãy tạm dừng và cài đặt gói trước; các bước còn lại sẽ hoạt động trên bất kỳ nền tảng nào chạy Python.

## Tạo Workbook Excel bằng Python

Điều đầu tiên chúng ta cần là một đối tượng workbook sạch sẽ. Aspose.Cells cung cấp lớp `Workbook` đại diện cho toàn bộ file Excel trong bộ nhớ.

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

Tại sao lại bắt đầu với một workbook mới? Vì nó đảm bảo môi trường xác định – không có công thức ẩn, không có định dạng lộn xộn, chỉ một canvas trống. Đây là nền tảng cho bất kỳ tutorial **tạo workbook excel python** nào.

## Điền Dữ Liệu vào Worksheet

Tiếp theo, chúng ta sẽ tạo một bảng số 5 × 3 bắt đầu từ ô **A1**. Dữ liệu được giữ đơn giản để bạn dễ nhìn thấy các phép tính.

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

Chú ý cách chúng ta dùng `put_value` với một danh sách lồng nhau trong Python; Aspose.Cells tự động ánh xạ các hàng và cột cho chúng ta. Nếu bạn cần nhập dữ liệu từ CSV hoặc cơ sở dữ liệu, chỉ cần thay thế `table_data` bằng nguồn dữ liệu đó – không cần thay đổi gì khác.

## Cách Viết Lambda trong Công Thức BYROW (Python)

Bây giờ đến phần hấp dẫn: **cách viết lambda** mà engine Excel sẽ đánh giá. Hàm `BYROW` của Excel lặp qua mỗi hàng của một phạm vi, truyền hàng đó vào một `LAMBDA` mà bạn cung cấp. Trong ví dụ này, chúng ta muốn tính trung bình của mỗi hàng.

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

Hãy phân tích:

- `BYROW(A1:C5, …)` yêu cầu Excel xem xét mọi hàng trong phạm vi A1:C5.
- `LAMBDA(r, AVERAGE(r))` định nghĩa một hàm ẩn danh (`r` là mảng hàng) trả về trung bình của hàng đó.
- Kết quả sẽ tự động tràn vào D1:D5 vì BYROW trả về một mảng.

Dòng duy nhất này là câu trả lời cho **cách viết lambda** cho các phép tính theo hàng. Bạn có thể thay `AVERAGE` bằng `SUM`, `MAX`, hoặc bất kỳ hàm tổng hợp nào khác – chỉ cần thay đổi phần thân của lambda.

## Buộc Tính Tính Toán Công Thức

Aspose.Cells không tự động tính toán công thức khi bạn đặt chúng, vì vậy chúng ta phải yêu cầu nó tính lại.

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

Nếu bỏ qua bước này, các ô trong cột D sẽ vẫn chứa văn bản công thức, không phải các số đã tính. Đây là một lỗi phổ biến khi mọi người **cách sử dụng byrow** mà không kích hoạt một lượt tính toán.

## Cách Đọc Ô Sau Khi Tính Toán

Cuối cùng, hãy lấy kết quả trở lại Python. Điều này minh họa **cách đọc ô** theo cách hoạt động với bất kỳ đầu ra công thức nào.

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Một list‑comprehension nhanh lặp qua năm hàng, lấy giá trị `.value` của mỗi ô, và lưu vào `row_averages`. Danh sách được in ra xác nhận rằng lambda của chúng ta đã hoạt động đúng như mong đợi.

### Mẹo chuyên nghiệp
Nếu bạn cần đọc một khối kết quả lớn, hãy dùng `worksheet.cells.get_range("D1:D5").value` để lấy toàn bộ mảng trong một lần gọi – nhanh hơn rất nhiều cho các sheet lớn.

## Sử Dụng Hàm Lambda trong Excel để Tính Trung Bình Theo Hàng (Script Đầy Đủ)

Kết hợp mọi thứ lại, đây là script hoàn chỉnh, sẵn sàng chạy:

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

Chạy script này sẽ in ra:

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Đó là toàn bộ vòng đời: **tạo workbook excel python**, điền dữ liệu, **cách sử dụng byrow**, **cách viết lambda**, và cuối cùng **cách đọc ô**.

## Các Trường Hợp Cạnh & Câu Hỏi Thường Gặp

- **Nếu dữ liệu của tôi không liên tiếp thì sao?**  
  BYROW hoạt động trên bất kỳ phạm vi hình chữ nhật nào. Nếu có khoảng trống, chỉ cần tham chiếu một phạm vi lớn hơn và để lambda bỏ qua các ô trống (`AVERAGEIF(r, "<>")`).

- **Tôi có thể truyền hơn một đối số vào lambda không?**  
  Có. Đối số đầu tiên luôn là hàng (hoặc cột cho `BYCOL`). Các đối số bổ sung có thể được cung cấp sau phạm vi, như `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`.

- **Liệu điều này có tương thích với các phiên bản Excel cũ không?**  
  BYROW và LAMBDA chỉ có từ Excel 365 (mảng động). Nếu bạn cần hỗ trợ legacy, sẽ phải mô phỏng logic bằng VBA hoặc nhiều cột trợ giúp.

- **Có cần lưu workbook ra đĩa không?**  
  Không cho demo này, nhưng bạn có thể gọi `workbook.save("output.xlsx")` nếu muốn tạo file thực.

## Kết Luận

Chúng ta đã khám phá **cách viết lambda** trong công thức BYROW của Excel từ Python, trình diễn một quy trình **tạo workbook excel python** đầy đủ, và chỉ ra cách **cách đọc ô** sau khi tính toán. Bằng cách sử dụng Aspose.Cells, bạn tránh được các rắc rối COM interop, và mẫu này có thể mở rộng lên hàng nghìn dòng với ít thay đổi mã.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay `AVERAGE` bằng `MEDIAN`, thêm logic điều kiện vào lambda, hoặc tự động tạo một bộ báo cáo hoàn chỉnh. Sự kết hợp giữa Python và các hàm hiện đại của Excel mở ra một thế giới khả năng cho tự động hoá dựa trên dữ liệu.

Có câu hỏi hoặc muốn chia sẻ mẹo lambda của bạn? Để lại bình luận bên dưới, và chúc bạn coding vui vẻ!  

![cách viết lambda trong Excel bằng Python](image.png){alt="cách viết lambda trong Excel bằng Python"}

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, kèm theo giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Load an Excel Workbook Without Defined Names Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}