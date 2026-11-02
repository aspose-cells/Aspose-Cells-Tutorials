---
category: general
date: 2026-10-04
description: Tạo workbook Excel bằng Python sử dụng Aspose.Cells. Học cách định dạng
  có điều kiện trong Excel bằng Python, thay đổi màu nền ô bằng Python, và định dạng
  ngày cho ô bằng Python trong một ví dụ đầy đủ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: vi
lastmod: 2026-10-04
og_description: Tạo workbook Excel bằng Python với Aspose.Cells. Hướng dẫn này trình
  bày cách định dạng có điều kiện trong Excel bằng Python, thay đổi màu nền ô bằng
  Python và định dạng ngày cho các ô bằng Python một cách từng bước.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Tạo workbook Excel bằng Python – hướng dẫn đầy đủ với định dạng có điều
  kiện
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Tạo workbook Excel bằng Python với định dạng có điều kiện và màu nền ô
url: /vi/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel workbook python với conditional formatting và màu nền ô

Nếu bạn cần **create Excel workbook python** nhanh chóng, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy một ví dụ đầy đủ, có thể chạy được, trong đó thêm **excel conditional formatting python**, thay đổi **cell background color python**, và **format cells date python** để làm nổi bật “Yesterday”.  

Trong nhiều trường hợp báo cáo, dấu hiệu trực quan của một ô có màu giúp dữ liệu trở nên dễ hiểu ngay lập tức. Bài hướng dẫn này sẽ đưa bạn qua từng dòng mã, giải thích lý do mỗi bước quan trọng, và cung cấp cho bạn một script sẵn sàng chạy mà bạn có thể điều chỉnh cho dự án của mình.

## Những gì bạn sẽ đạt được

1. **create Excel workbook python** bằng thư viện Aspose.Cells.  
2. Áp dụng **excel conditional formatting python** tự động làm nổi bật các ngày thuộc “Yesterday”.  
3. Đặt **cell background color python** thành màu hồng (hoặc bất kỳ màu nào bạn muốn).  
4. **format cells date python** để các ngày hiển thị theo định dạng ngày chuẩn của Excel.  

Không cần kinh nghiệm trước với Aspose.Cells—chỉ cần môi trường Python 3 hoạt động và có quyền truy cập pip.

## Yêu cầu trước

- Python 3.8 hoặc mới hơn đã được cài đặt.  
- `aspose-cells` và `aspose-pydrawing` đã được cài đặt qua `pip install aspose-cells aspose-pydrawing`.  
- Hiểu biết cơ bản về cú pháp Python và các khái niệm Excel (workbooks, worksheets, cells).  

> **Mẹo:** Nếu bạn chạy script trong môi trường ảo, bạn sẽ tránh được xung đột phiên bản với các dự án khác.

## Bước 1: Thiết lập dự án và nhập các lớp cần thiết

Bước đầu tiên khi bạn **create Excel workbook python** là nhập các lớp Aspose.Cells cần thiết. Những lớp này cho phép bạn truy cập trực tiếp vào việc tạo workbook, conditional formatting và styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Tại sao điều này quan trọng:* Việc chỉ nhập các ký hiệu cần thiết giúp không gian tên gọn gàng và làm cho script dễ đọc hơn. `Workbook` là điểm vào cho **create Excel workbook python**, trong khi `FormatConditionType` và `TimePeriodType` là cần thiết cho **excel conditional formatting python**.

## Bước 2: Tạo một workbook mới và lấy worksheet đầu tiên

Bây giờ chúng ta thực sự **create Excel workbook python**. Hàm khởi tạo `Workbook()` cung cấp cho bạn một tệp Excel trống với một worksheet mặc định.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Giải thích:* Mỗi tệp Excel bắt đầu với ít nhất một worksheet. Mặc định Aspose.Cells đặt tên là “Sheet1”. Bạn có thể thêm nhiều sheet sau, nhưng trong ví dụ này một sheet duy nhất giúp tập trung vào nội dung.

## Bước 3: Xác định phạm vi mục tiêu cho conditional formatting

Conditional formatting hoạt động trên một phạm vi hình chữ nhật. Ở đây chúng ta chọn phạm vi `I19:K20`, cung cấp ba cột và hai hàng để làm việc.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Lý do chúng ta làm điều này:* Phương thức `get` trả về một đối tượng `ConditionalFormatting` gắn với phạm vi đã chỉ định. Nếu phạm vi chưa có bất kỳ định dạng nào, Aspose.Cells sẽ tự động tạo một bộ sưu tập mới.

## Bước 4: Thêm điều kiện TIME_PERIOD và đặt màu nền

Đây là phần cốt lõi của **excel conditional formatting python**. Chúng ta thêm một quy tắc `TIME_PERIOD` để làm nổi bật các ô chứa ngày thuộc “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Chi tiết sâu:*  
- `FormatConditionType.TIME_PERIOD` cho Excel đánh giá ngày dựa trên ngày hiện tại.  
- `TimePeriodType.YESTERDAY` là một enum tích hợp sẵn, tự động cập nhật mỗi ngày, vì vậy workbook luôn làm nổi bật “Yesterday” mới nhất.  
- Bằng cách đặt `background_color` thành `Color.pink` và mẫu thành `SOLID`, chúng ta đạt được hiệu ứng **cell background color python** mà không cần mã VBA bổ sung.

## Bước 5: Điền dữ liệu mẫu vào phạm vi và áp dụng định dạng ngày

Để thấy conditional formatting hoạt động, chúng ta cần các giá trị ngày thực. Chúng ta cũng cần **format cells date python** để Excel xử lý chúng như ngày chứ không phải số thuần.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Giải thích:*  
- Dòng `style.number = 30` là bước **format cells date python**. Mã định dạng 30 tương ứng với định dạng ngày ngắn (`m/d/yy`).  
- Sử dụng hàm trợ giúp giúp code DRY (Don’t Repeat Yourself) và dễ dàng thêm ngày mới sau này.

## Bước 6: Thêm nhãn mô tả

Một nhãn nhỏ giúp bất kỳ ai mở workbook hiểu lý do các ô được tô màu.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Bước 7: Lưu workbook vào đĩa

Cuối cùng, chúng ta **create Excel workbook python** trên đĩa bằng cách gọi `save`. Hằng số `SaveFormat.XLSX` đảm bảo tệp ở định dạng Office Open XML hiện đại.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Khi bạn mở `TimePeriodDemo.xlsx` trong Excel, bạn sẽ thấy:

- Các ô `I19` và `K20` chứa ngày.  
- Ô khớp với “Yesterday” (trong ví dụ tĩnh này, `I19`) được tô màu hồng.  
- Nhãn “Yesterday” xuất hiện ở `I20`.  

> **Mẹo:** Nếu bạn chạy script vào ngày khác, conditional formatting vẫn sẽ làm nổi bật ô có ngày chính xác một ngày trước ngày hệ thống hiện tại—không cần thay đổi mã.

## Toàn bộ script – sẵn sàng sao chép và chạy

Dưới đây là chương trình hoàn chỉnh, tự chứa, tích hợp tất cả các bước ở trên. Sao chép nó vào tệp có tên `conditional_format_demo.py`, điều chỉnh `YOUR_DIRECTORY`, và chạy bằng `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Kết quả mong đợi

Chạy script sẽ in ra một dòng xác nhận:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Mở tệp đã tạo sẽ hiển thị nền màu hồng trên ô khớp với quy tắc “Yesterday”, xác nhận rằng **excel conditional formatting python** và **cell background color python** đang hoạt động cùng nhau.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách điều chỉnh mã |
|-----------|-----------------------|
| **Màu nổi bật khác** | Thay `Color.pink` thành bất kỳ hằng số `Color` nào khác, ví dụ `Color.light_green`. |
| **Làm nổi bật “Today” thay vì “Yesterday”** | Đặt `condition.time_period = TimePeriodType.TODAY`. |
| **Áp dụng định dạng cho toàn bộ cột** | Sử dụng phạm vi như `"A:A"` và điều chỉnh biến `target_range` cho phù hợp. |
| **Sử dụng định dạng ngày tùy chỉnh** | Thay `style.number = 30` bằng `style.custom = "dd-mmm-yyyy"` để có định dạng dễ đọc hơn. |
| **Nhiều điều kiện trên cùng một phạm vi** |  |

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo Excel Workbook Python – Hướng dẫn đầy đủ với Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Tạo và Lưu Excel Workbook dưới dạng PDF trong ASP.NET sử dụng Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Cách tạo và lưu Excel Workbook dưới dạng ODS sử dụng Aspose.Cells cho .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}