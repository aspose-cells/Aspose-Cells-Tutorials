---
category: general
date: 2026-09-15
description: Tìm hiểu cách áp dụng định dạng có điều kiện theo khoảng thời gian và
  lưu workbook dưới dạng XLSX bằng Aspose.Cells trong Python. Bao gồm mã hướng dẫn
  chi tiết từng bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: vi
lastmod: 2026-09-15
og_description: Áp dụng định dạng có điều kiện theo khoảng thời gian trong Excel bằng
  Python và lưu sổ làm việc dưới dạng XLSX. Tham khảo hướng dẫn đầy đủ này cho Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Áp dụng định dạng có điều kiện theo khoảng thời gian trong Excel bằng Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Cách áp dụng định dạng có điều kiện theo khoảng thời gian trong Excel bằng
  Python
url: /vi/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách áp dụng định dạng có điều kiện theo khoảng thời gian trong Excel bằng Python

Nếu bạn cần **định dạng có điều kiện theo khoảng thời gian** trong một tệp Excel, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Python. Bạn sẽ thấy một ví dụ hoàn chỉnh, có thể chạy được, tạo một workbook, làm nổi bật các ngày của hôm qua, và **lưu workbook dưới dạng XLSX** chỉ trong vài dòng mã.

Định dạng có điều kiện là một cách mạnh mẽ để thu hút sự chú ý đến dữ liệu đáp ứng một quy tắc cụ thể. Trong hướng dẫn này, chúng tôi tập trung vào khoảng thời gian “Yesterday”, nhưng mẫu tương tự cũng hoạt động cho các khoảng thời gian tích hợp khác như Today, LastWeek và NextMonth. Khi kết thúc hướng dẫn, bạn sẽ có thể **how to create excel workbook python**‑style scripts sẵn sàng cho môi trường sản xuất.

## Yêu cầu trước

- Python 3.8+ đã được cài đặt  
- `aspose-cells` và `aspose-pydrawing` packages (`pip install aspose-cells aspose-pydrawing`)  
- Kiến thức cơ bản về cú pháp Python  

Không cần cài đặt Office bổ sung vì Aspose.Cells xử lý việc tạo tệp nội bộ.

## Định dạng có điều kiện theo khoảng thời gian với Aspose.Cells trong Python

Phần này sẽ hướng dẫn qua từng dòng mã cần thiết cho nhiệm vụ chính. Khối mã bên dưới là toàn bộ script; các chú thích giải thích mục đích của mỗi bước.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Tại sao mỗi bước lại quan trọng

1. **Creating the workbook** cung cấp cho bạn một tệp Excel trong bộ nhớ mà bạn có thể thao tác mà không cần mở Excel.  
2. **Defining the range** (`I19:K20`) cho Aspose.Cells biết quy tắc áp dụng ở đâu, giữ cho logic được cô lập.  
3. **Adding a TIME_PERIOD condition** sử dụng enumeration tích hợp sẵn của Aspose `TimePeriodType.YESTERDAY`. Điều này tránh việc tính toán ngày thủ công và tự động cập nhật khi tệp được mở vào ngày khác.  
4. **Setting the style** (`background_color` và `pattern`) xác định cách các ô được làm nổi bật sẽ hiển thị. Sử dụng `Color.pink` giúp quy tắc dễ nhận thấy.  
5. **Writing sample dates** với định dạng số 30 đảm bảo Excel hiển thị chúng dưới dạng ngày ngắn thay vì số sê-ri.  
6. **Auto‑fitting the column** cải thiện khả năng đọc cho bất kỳ ai mở tệp sau này.  
7. **Saving as XLSX** tạo ra một tệp tương thích rộng, có thể mở trong Excel, Google Sheets hoặc bất kỳ chương trình bảng tính hiện đại nào.

## Cách tạo Excel workbook theo phong cách Python với Aspose.Cells

Script ở trên đã minh họa các bước tối thiểu để **how to create excel workbook python**. Trong thực tế, bạn có thể muốn:

- Thêm nhiều worksheet (`workbook.worksheets.add("Report")`).  
- Điền các bảng dữ liệu lớn bằng vòng lặp hoặc pandas DataFrames (`worksheet.cells.import_data_table`).  
- Áp dụng định dạng bổ sung (phông chữ, viền) bằng cách sử dụng `cell.get_style()`.

Tất cả các hành động này đều theo cùng một mẫu: lấy đối tượng, sửa đổi các thuộc tính, và gọi `set_style` hoặc `save`.

## Thêm định dạng có điều kiện Python – các mẫu hữu ích khác

Ngoài ví dụ “Yesterday”, Aspose.Cells hỗ trợ một số loại định dạng có điều kiện:

| FormatConditionType | Trường hợp sử dụng điển hình |
|---------------------|------------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Công thức tùy chỉnh (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | So sánh đơn giản (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Thang màu gradient |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Biểu diễn thanh trong ô |

Để **add conditional formatting python** cho một ngưỡng số, bạn sẽ thay thế `FormatConditionType.TIME_PERIOD` bằng `FormatConditionType.CELL_VALUE` và thiết lập `condition.operator_type` và `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Lưu workbook dưới dạng XLSX – các thực hành tốt nhất

Khi bạn **save workbook as xlsx**, hãy cân nhắc:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) để tránh các định dạng cũ.  
- **Using a deterministic file name** nếu script chạy trong vòng lặp (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) trong các dịch vụ chạy lâu để giải phóng bộ nhớ gốc.

Ví dụ đã sử dụng `SaveFormat.XLSX`, tạo ra một workbook hiện đại dựa trên zip, giữ lại tất cả các quy tắc định dạng có điều kiện.

## Làm nổi bật ngày hôm qua trong Excel – các bước xác minh

Sau khi chạy script, mở `TimePeriodExample.xlsx`:

1. Các ô `I19` và `K20` chứa ngày `30‑07‑2008` và `03‑08‑2008`.  
2. Ô `I20` hiển thị văn bản “Yesterday”.  
3. Nếu bạn thay đổi ngày hệ thống thành **30 July 2008** và mở lại tệp, các ô có ngày trùng khớp sẽ tự động được tô màu hồng.  
4. Thay đổi ngày hệ thống sang bất kỳ ngày nào khác sẽ xóa màu hồng, xác nhận quy tắc phản hồi với logic **time period conditional formatting**.

## Những lỗi thường gặp và cách tránh chúng

- **Missing `aspose-pydrawing`** – lớp `Color` nằm trong gói này; quên cài đặt sẽ gây ra `ImportError`.  
- **Incorrect number format** – sử dụng định dạng General mặc định sẽ hiển thị số sê-ri (ví dụ, 39822). Luôn đặt `style.number = 30` cho ngày ngắn.  
- **Range mismatch** – phạm vi định dạng có điều kiện phải bao gồm các ô bạn muốn làm nổi bật; nếu không quy tắc sẽ không có hiệu lực.

## Mẹo chuyên nghiệp: tái sử dụng quy trình định dạng

Nếu bạn cần quy tắc “Yesterday” giống nhau trong nhiều workbook, hãy đóng gói logic vào một hàm trợ giúp:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Gọi `apply_yesterday_highlight(worksheet, "A1:A10")` ở bất kỳ nơi nào cần.

## Kết luận

Hướng dẫn này đã chỉ cho bạn cách triển khai **time period conditional formatting** trong Excel bằng Python, cách **save workbook as XLSX**, và cách **highlight yesterday in Excel** với một script duy nhất, có thể tái sử dụng. Giờ đây bạn có nền tảng vững chắc để **add conditional formatting python** vào bất kỳ dự án tự động hóa nào, dù bạn đang tạo báo cáo hàng ngày, xây dựng bảng điều khiển, hay chuẩn bị xuất dữ liệu.

**Các bước tiếp theo**

- Khám phá các giá trị `TimePeriodType` khác như `TODAY` hoặc `LAST_WEEK`.  
- Kết hợp nhiều quy tắc định dạng có điều kiện trên cùng một phạm vi để có các gợi ý trực quan phong phú hơn.  
- Tích hợp việc tạo workbook vào dịch vụ web hoặc công việc theo lịch.

Chúc lập trình vui vẻ, và tận hưởng sự rõ ràng trực quan mà định dạng có điều kiện mang lại cho việc tự động hóa Excel của bạn!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động được, kèm theo giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Thành thạo Định dạng có điều kiện trong Excel bằng Aspose.Cells .NET : Hướng dẫn toàn diện](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Thành thạo Aspose.Cells .NET : Áp dụng Định dạng có điều kiện cho các hàng xen kẽ trong Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Thành thạo Định dạng có điều kiện với Phông chữ tùy chỉnh trong Excel bằng Aspose.Cells cho .NET và C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}