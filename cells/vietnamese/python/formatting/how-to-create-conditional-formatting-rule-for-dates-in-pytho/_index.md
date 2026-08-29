---
category: general
date: 2026-08-24
description: Tạo quy tắc định dạng có điều kiện trong Python bằng Aspose.Cells để
  làm nổi bật các ngày, với tự động điều chỉnh độ rộng cột và định dạng màu nền.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: vi
lastmod: 2026-08-24
og_description: Tạo quy tắc định dạng có điều kiện trong Python với Aspose.Cells.
  Tìm hiểu cách làm nổi bật ngày tháng, đặt màu nền và tự động điều chỉnh độ rộng
  cột chỉ trong vài dòng mã.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Tạo quy tắc định dạng có điều kiện cho ngày trong Python – hướng dẫn chi
  tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Cách tạo quy tắc định dạng có điều kiện cho ngày trong Python
url: /vi/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo quy tắc định dạng có điều kiện cho ngày trong Python

Nếu bạn cần **tạo quy tắc định dạng có điều kiện** phản hồi với ngày tháng, hướng dẫn này sẽ chỉ cho bạn cách thực hiện bằng Aspose.Cells cho Python. Dù bạn đang xây dựng bảng điều khiển báo cáo hay một bảng tính tự động, bạn sẽ thấy cách làm nổi bật ngày hôm qua, áp dụng màu nền tùy chỉnh, và **tự động điều chỉnh độ rộng cột** để kết quả trông chuyên nghiệp.

Trong tutorial này, chúng ta sẽ đề cập tới **định dạng có điều kiện theo ngày**, trình bày **định dạng màu nền có điều kiện**, và kết thúc bằng việc lưu workbook dưới dạng file XLSX. Khi hoàn thành, bạn sẽ có một hàm trợ giúp có thể tái sử dụng cho bất kỳ **định dạng có điều kiện dựa trên ngày** nào bạn cần.

## Những gì bạn sẽ học

* Thiết lập workbook và worksheet bằng Aspose.Cells.  
* Viết một hàm trợ giúp để thêm **định dạng có điều kiện dựa trên ngày** vào bất kỳ phạm vi ô nào.  
* Điền dữ liệu mẫu ngày tháng để quy tắc có thể được đánh giá.  
* Áp dụng **tự động điều chỉnh độ rộng cột** để nội dung dễ đọc.  
* Lưu workbook và kiểm tra các ô được tô màu.

Điều kiện tiên quyết duy nhất là môi trường Python hoạt động với gói `aspose-cells` đã được cài đặt.

## Yêu cầu trước

| Yêu cầu | Chi tiết |
|---------|----------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Kiến thức cơ bản về Excel | worksheets, cells, formatting |
| Tùy chọn: IDE (VS Code, PyCharm, v.v.) | bất kỳ trình soạn thảo nào có thể chạy script Python |

## Bước 1: Tạo workbook và lấy worksheet đầu tiên

Bước đầu tiên là **tạo các đối tượng sẵn sàng cho quy tắc định dạng có điều kiện**: một `Workbook` và `Worksheet` mặc định của nó. Những đối tượng này là điểm khởi đầu cho mọi thao tác tiếp theo.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Tại sao điều này quan trọng:* `Workbook` chứa toàn bộ file Excel, trong khi `Worksheet` là nơi bạn áp dụng ô, kiểu dáng và **định dạng có điều kiện theo ngày**. Nếu không có các đối tượng này, phần còn lại của mã sẽ không có chỗ thực thi.

## Bước 2: Xây dựng hàm trợ giúp để thêm định dạng TIME_PERIOD

Thay vì lặp lại cùng một đoạn mã cho mỗi phạm vi, chúng ta gói logic vào một hàm trợ giúp. Hàm này gắn **định dạng màu nền có điều kiện** mà tô màu các ô dựa trên `TimePeriodType` (ví dụ: Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Tại sao chúng ta dùng hàm trợ giúp:* Nó tách biệt logic **định dạng có điều kiện dựa trên ngày**, giúp mã dễ đọc, dễ kiểm thử và tái sử dụng trên nhiều sheet hoặc dự án.

## Bước 3: Áp dụng quy tắc định dạng có điều kiện cho một phạm vi cụ thể

Bây giờ chúng ta dùng hàm trợ giúp để làm nổi bật các ô chứa “Yesterday”. Đây là phần cốt lõi của thao tác **tạo quy tắc định dạng có điều kiện**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Khi workbook được mở, bất kỳ ô nào trong `I19:K20` có ngày bằng ngày hôm qua sẽ hiển thị nền màu hồng (kiểu chúng ta đã thiết lập trong hàm trợ giúp). Tham số `bg_color` cho thấy cách bạn có thể đặt nền mặc định phía sau màu điều kiện nếu muốn.

## Bước 4: Điền dữ liệu mẫu ngày tháng vào phạm vi

Một quy tắc có điều kiện chỉ hiển thị sau khi worksheet chứa dữ liệu thỏa mãn điều kiện. Chúng ta sẽ chèn hai ngày: một ngày khớp “Yesterday” và một ngày nằm ngoài khoảng thời gian.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Tại sao điều này quan trọng:* Bằng cách sử dụng đối tượng `datetime`, chúng ta đảm bảo Excel xử lý giá trị là ngày thực, điều này cần thiết để **định dạng có điều kiện theo ngày** hoạt động đúng. Định dạng số (`30`) bảo đảm các ô hiển thị dưới dạng ngày dễ nhận biết.

## Bước 5: Tự động điều chỉnh độ rộng cột và lưu workbook

Sau khi dữ liệu và định dạng đã sẵn sàng, bước cuối cùng là **tự động điều chỉnh độ rộng cột** để ngày tháng hiển thị đầy đủ. Sau đó ghi file ra đĩa.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Lệnh `auto_fit_column` kiểm tra nội dung dài nhất ở cột 12 (tương ứng với cột **L** trong Excel) và mở rộng độ rộng cho phù hợp. Bước nhỏ này ngăn ngày bị cắt ngắn và làm cho **định dạng màu nền có điều kiện** hiển thị rõ ràng.

### Kết quả mong đợi

Khi bạn mở `TimePeriodDemo.out.xlsx`:

| I19 (ngày) | I20 (nhãn) | K20 (ngày) |
|------------|------------|------------|
| 30‑Jul‑2008 (được tô hồng) | Yesterday | 03‑Aug‑2008 (không tô) |

* Ô chứa ngày hôm qua hiển thị nền màu hồng vì **tạo quy tắc định dạng có điều kiện** đã khớp với khoảng `YESTERDAY`.  
* Các ô còn lại giữ nền mặc định (hoặc `medium_sea_green` tùy chọn bạn đã cung cấp).  
* Cột L được tự động mở rộng, vì vậy các ngày hiển thị đầy đủ và dễ đọc.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Cách điều chỉnh mã |
|-----------|--------------------|
| **Làm nổi bật “Today” thay vì “Yesterday”** | Thay `TimePeriodType.YESTERDAY` bằng `TimePeriodType.TODAY`. |
| **Sử dụng màu nền khác** | Thay `condition.style.background_color = Color.pink` bằng bất kỳ `Color` nào khác (ví dụ: `Color.light_sky_blue`). |
| **Áp dụng quy tắc cho phạm vi không liên tiếp** | Gọi `add_time_period_condition` nhiều lần với các chuỗi `cell_range` khác nhau (ví dụ: `"A1:A10", "C1:C10"`). |
| **Làm việc với workbook đã tồn tại** | Tải file bằng `Workbook("myfile.xlsx")` thay vì tạo mới. |
| **Nhiều điều kiện dựa trên ngày cho cùng một phạm vi** | Sau lần gọi `add_time_period_condition` đầu tiên, thêm một điều kiện khác bằng `conditions.add_condition(FormatConditionType.TIME_PERIOD)` và đặt `time_period` khác. |

## Kết luận

Bạn đã biết cách **tạo quy tắc định dạng có điều kiện** phản hồi với ngày tháng, áp dụng **định dạng màu nền có điều kiện**, và **tự động điều chỉnh độ rộng cột** bằng Aspose.Cells cho Python. Hàm trợ giúp trừu tượng hoá logic, cho phép bạn tái sử dụng cùng một mẫu cho bất kỳ **định dạng có điều kiện theo ngày** nào—dù là “Yesterday”, “LastWeek”, hay một khoảng tùy chỉnh.

Tiếp theo, bạn có thể khám phá:

* Thêm **icon sets** hoặc **data bars** cùng với các quy tắc ngày.  
* Tạo báo cáo động lấy ngày từ cơ sở dữ liệu.  
* Kết hợp nhiều **định dạng có điều kiện dựa trên ngày** trên một sheet.

Hãy tự do thử nghiệm các màu, khoảng thời gian và phạm vi khác nhau để phù hợp với nhu cầu dự án của bạn. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}