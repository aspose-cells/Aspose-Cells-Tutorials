---
category: general
date: 2026-07-14
description: Tạo mã Python để tạo workbook Excel, đặt màu nền cho ô, làm nổi bật các
  ô dựa trên khoảng thời gian ngày, và lưu workbook dưới dạng XLSX trong vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: vi
lastmod: 2026-07-14
og_description: Tạo nhanh workbook Excel bằng Python. Học cách đặt màu nền cho ô,
  làm nổi bật các ô dựa trên khoảng thời gian, và lưu workbook dưới dạng XLSX với
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Tạo Workbook Excel bằng Python – Định dạng có điều kiện từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Tạo Workbook Excel bằng Python – Hướng dẫn đầy đủ với Định dạng có điều kiện
url: /vi/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Excel Workbook Python – Hướng Dẫn Toàn Diện với Định Dạng Có Điều Kiện

Bạn đã bao giờ tự hỏi làm sao để **create excel workbook python** script trông chuyên nghiệp mà không cần mở Excel thủ công? Bạn không phải là người duy nhất. Trong nhiều dự án dựa trên dữ liệu, chúng ta cần tạo bảng tính, tô màu các ô, và thậm chí đánh dấu các ngày nằm trong một khoảng nhất định — tất cả chỉ bằng mã Python thuần.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, **creates an Excel workbook python** bằng thư viện Aspose.Cells, **sets cell background color**, áp dụng **conditional formatting based on date**, và cuối cùng **saves workbook as xlsx**. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ pipeline tự động nào.

## Những Điều Bạn Sẽ Học

- Cách khởi tạo một workbook và lấy worksheet đầu tiên.  
- Một hàm trợ giúp để thêm một collection định dạng có điều kiện cho bất kỳ phạm vi ô nào.  
- Sử dụng **conditional formatting based on date** để làm nổi bật các mục của ngày hôm qua.  
- Điều chỉnh độ rộng cột để có bố cục gọn gàng.  
- Lưu kết quả bằng **save workbook as xlsx**.  

Không cần cài đặt Excel bên ngoài — Aspose.Cells xử lý mọi thứ trong bộ nhớ.

## Yêu Cầu Trước

- Python 3.8+ đã được cài đặt.  
- `aspose-cells` package (`pip install aspose-cells`).  
- Kiến thức cơ bản về hàm Python và các đối tượng datetime.  

Nếu bạn chưa từng dùng Aspose.Cells, hãy nghĩ nó như một API mạnh mẽ, thuần Python mô phỏng mô hình đối tượng của Excel. Nó hoàn hảo cho việc tạo file phía máy chủ khi bộ Office không có sẵn.

## Bước 1: Khởi Tạo Workbook (Create Excel Workbook Python)

Đầu tiên, chúng ta cần **create excel workbook python** theo kiểu. Bước này tạo một đối tượng workbook trống và trỏ tới worksheet mặc định.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Tại sao điều này quan trọng:** Lớp `Workbook` là điểm vào cho mọi thao tác Excel. Bằng cách tạo nó bằng chương trình, chúng ta tránh việc xử lý file thủ công.

## Bước 2: Trợ Giúp Thêm Collection Định Dạng Có Điều Kiện (Set Cell Background Color)

Định dạng có điều kiện tồn tại trong một *collection* gắn vào một phạm vi. Hãy gói phần boilerplate này trong một hàm trợ giúp nhỏ, đồng thời cho phép chúng ta **set cell background color** cho toàn bộ phạm vi.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Mẹo chuyên nghiệp:** Sử dụng hàm trợ giúp giúp luồng chính của bạn sạch sẽ và dễ dàng tái sử dụng cùng một logic cho nhiều phạm vi.

## Bước 3: Áp Dụng Định Dạng Có Điều Kiện Dựa Trên Ngày (Highlight Cells Based on Date Range)

Bây giờ chúng ta sẽ thực sự **highlight cells based on date range**. Ví dụ tập trung vào “yesterday” nhưng bạn có thể thay `TimePeriodType.YESTERDAY` bằng `TODAY`, `LAST_WEEK`, v.v.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Điều gì đang xảy ra?**  
> 1. Đầu tiên chúng ta đặt nền xanh lá cây trung tính cho toàn bộ phạm vi.  
> 2. Sau đó chúng ta thêm một điều kiện `TIME_PERIOD` ghi đè màu nền thành màu hồng **chỉ** khi ngày của ô bằng ngày hôm qua.  
> 3. Enum `TimePeriodType` trừu tượng hoá việc tính toán ngày, vì vậy bạn không cần viết logic tùy chỉnh.

## Bước 4: Điền Các Ngày Mẫu (Để Quy Tắc Có Thể Được Đánh Giá)

Để thấy quy tắc hoạt động, chúng ta sẽ đưa một vài ngày vào sheet. Một ngày nằm trong khoảng “yesterday”, còn lại không.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Lưu ý trường hợp biên:** Nếu workbook của bạn sẽ được mở trong các locale khác nhau, hãy cân nhắc sử dụng `date_style.custom = "dd‑mm‑yyyy"` để đảm bảo hiển thị nhất quán.

## Bước 5: Sắp Xếp Gọn Gàng Bố Cục (Auto‑Fit Columns)

Một bảng tính chật chội trông không chuyên nghiệp. Hãy **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Tại sao auto‑fit?** Nó đảm bảo bất kỳ nhãn hoặc ngày nào dài đều hiển thị đầy đủ, điều này đặc biệt quan trọng khi bạn chia sẻ file với các bên liên quan không chuyên môn.

## Bước 6: Lưu Workbook (Save Workbook As XLSX)

Cuối cùng, chúng ta **save workbook as xlsx** tới vị trí bạn chọn. Hằng số `SaveFormat.XLSX` cho Aspose.Cells biết ghi dưới định dạng OpenXML hiện đại.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Kết quả bạn sẽ thấy:**  
> - Các ô I19 và K20 chứa ngày.  
> - I19 (yesterday) được tô màu hồng, trong khi K20 vẫn xanh lá.  
> - Cột L tự động mở rộng để vừa nhãn “Yesterday”.  

Nếu bạn mở `TimePeriodDemo.xlsx` trong Excel, định dạng có điều kiện đã được áp dụng — không cần bước nào thêm.

---

![Bảng tính Excel hiển thị ngày hôm qua được tô sáng](https://example.com/images/excel-demo.png "Ảnh chụp màn hình file Excel đã tạo với các ô được tô sáng")

*Hình ảnh trên minh họa workbook cuối cùng; chú ý màu hồng nổi bật trên ô chứa ngày hôm qua.*

## Tóm Tắt: Những Gì Chúng Ta Đã Đạt Được

- **Created an Excel workbook python** từ đầu bằng Aspose.Cells.  
- **Set cell background color** cho toàn bộ phạm vi để cung cấp gợi ý trực quan cho sheet.  
- Áp dụng **conditional formatting based on date** để tự động đánh dấu các mục của ngày hôm qua.  
- **Saved workbook as xlsx**, sẵn sàng cho việc phân phối hoặc xử lý tiếp theo.  

Tất cả đều được thực hiện trong dưới 60 dòng Python, và mã chạy trên bất kỳ nền tảng nào hỗ trợ runtime của Aspose.Cells.

## Các Bước Tiếp Theo & Chủ Đề Liên Quan

Nếu bạn thấy hữu ích, bạn cũng có thể muốn khám phá:

- **set cell background color** cho toàn bộ hàng dựa trên giá trị trạng thái (ví dụ: “Completed”, “Pending”).  
- sử dụng **highlight cells based on date range** để tạo cửa sổ trượt (7 ngày gần nhất, tháng hiện tại).  
- xuất ra các định dạng khác như **CSV** hoặc **PDF** với `SaveFormat.CSV` hoặc `SaveFormat.PDF`.  
- thêm **charts** bằng chương trình để trực quan hoá dữ liệu bạn vừa định dạng.  

Bạn có thể tự do điều chỉnh logic ngày, thay đổi bảng màu, hoặc mở rộng phạm vi để bao phủ toàn cột. Mẫu vẫn giống nhau: tạo workbook, đính kèm collection định dạng có điều kiện, xác định quy tắc, và lưu.

Có câu hỏi về trường hợp sử dụng cụ thể? Để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}