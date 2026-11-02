---
category: general
date: 2026-09-21
description: เรียนรู้วิธีสร้างไฟล์ Excel ใน Python ตั้งค่าสีพื้นหลังของเซลล์ และใช้การจัดรูปแบบตามเงื่อนไขโดยอิงวันที่ด้วย
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: th
lastmod: 2026-09-21
og_description: สร้างไฟล์ Excel ใน Python, ตั้งค่าสีพื้นหลังของเซลล์, และใช้การจัดรูปแบบตามเงื่อนไขตามวันที่ด้วย
  Aspose.Cells. ทำตามคู่มือแบบขั้นตอนต่อขั้นตอน.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: สร้างไฟล์ Excel ใน Python พร้อมการจัดรูปแบบตามเงื่อนไข
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: สร้างเวิร์กบุ๊ก Excel ด้วย Python โดยใช้การจัดรูปแบบตามเงื่อนไข
url: /th/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างไฟล์ Excel workbook ใน Python ด้วยการจัดรูปแบบตามเงื่อนไข

หากคุณต้องการ **สร้าง Excel workbook python** ที่ไฮไลต์วันที่โดยอัตโนมัติ คำแนะนำนี้จะแสดงวิธีทำอย่างละเอียด คุณจะได้เรียนรู้วิธี **ตั้งค่าสีพื้นหลังของเซลล์**, เพิ่มกฎ “Yesterday”, และบันทึกไฟล์—ทั้งหมดด้วย Aspose.Cells for Python

การทำงานกับไฟล์ Excel ผ่านโปรแกรมมักหมายถึงการใช้ตรรกะการจัดรูปแบบเดียวกันซ้ำหลายแผ่นงาน เมื่อจบบทเรียนนี้คุณจะมีรูปแบบที่นำกลับมาใช้ใหม่ได้สำหรับ **excel conditional formatting python** ที่สามารถใส่ลงในโปรเจกต์ใดก็ได้

## ข้อกำหนดเบื้องต้น

- Python 3.8+ ติดตั้งแล้ว  
- แพ็กเกจ `aspose-cells` (`pip install aspose-cells`)  
- ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และโมดูล datetime  

ไม่มีไลบรารีเพิ่มเติมที่จำเป็น; Aspose.Cells ดูแลการทำงานทั้งหมดของ Excel

## ขั้นตอนที่ 1: สร้าง workbook และเข้าถึง worksheet แรก

ขั้นตอนแรกคือ **สร้าง excel workbook python** แล้วดึง worksheet เริ่มต้นออกมา ซึ่งจะให้แคนวาสสะอาดสำหรับการจัดสไตล์ต่อไป

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*ทำไมจึงสำคัญ:* `Workbook()` สร้างไฟล์ Excel ในหน่วยความจำ การเข้าถึง `worksheets[0]` ช่วยหลีกเลี่ยงการกำหนดชื่อแผ่นงานแบบคงที่และทำงานได้แม้ชื่อเริ่มต้นจะเปลี่ยน

## ขั้นตอนที่ 2: ตัวช่วยสำหรับเพิ่มการจัดรูปแบบเงื่อนไข TIME_PERIOD

เพื่อให้โค้ดเป็นระเบียบ เราจะห่อการสร้าง conditional‑format ไว้ในฟังก์ชันช่วยเหลือ ฟังก์ชันนี้รับช่วงเซลล์, สีพื้นหลัง, และกฎช่วงเวลา ที่ต้องการ

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*ทำไมจึงสำคัญ:* ตัวช่วยนี้แยกขั้นตอนที่ทำซ้ำของการสร้าง conditional format ทำให้สามารถนำกลับมาใช้ซ้ำได้ง่ายสำหรับกฎที่อิงวันที่อื่น ๆ เช่น “Today” หรือ “Last Week”

## ขั้นตอนที่ 3: ใช้กฎ “Yesterday” กับช่วงเซลล์

ตอนนี้เราจะใช้ตัวช่วยเพื่อไฮไลต์เซลล์ที่มีค่าวันที่ของ “Yesterday” ช่วง `I19:K20` จะเปลี่ยนเป็น **medium sea green** เมื่อเงื่อนไขเป็นจริง

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*ทำไมจึงสำคัญ:* `TimePeriodType.YESTERDAY` เป็นส่วนหนึ่งของ enumeration ที่มาพร้อมกับ Aspose.Cells ดังนั้นคุณไม่ต้องคำนวณวันที่ด้วยตนเอง ไลบรารีจะประเมินกฎทุกครั้งที่เปิด workbook

## ขั้นตอนที่ 4: เติมค่าช่วงด้วยตัวอย่างวันที่

เพื่อดูกฎทำงาน เราจะเขียนวันที่สองค่า—หนึ่งที่ตรงกับ “Yesterday” และอีกหนึ่งที่ไม่ตรง สไตล์ `number` `30` สอดคล้องกับรูปแบบวันที่ที่มีอยู่ใน Excel

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*ทำไมจึงสำคัญ:* การใส่วันที่จริงช่วยให้คุณตรวจสอบว่า conditional formatting ทำงานได้โดยไม่ต้องเปิดไฟล์ในวันเฉพาะ

## ขั้นตอนที่ 5: เพิ่มป้ายอธิบายและปรับขนาดคอลัมน์อัตโนมัติ

ป้ายเล็ก ๆ จะอธิบายวัตถุประสงค์ของช่วงที่จัดรูปแบบ และ `auto_fit_column` ทำให้แผ่นงานอ่านง่ายขึ้น

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## ขั้นตอนที่ 6: บันทึก workbook

สุดท้ายให้เขียน workbook ลงดิสก์ คำสั่ง `os.makedirs` จะสร้างโฟลเดอร์เป้าหมายหากยังไม่มี

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

เมื่อคุณเปิดไฟล์ *TimePeriodDemo.xlsx* คุณจะเห็น:

- เซลล์ **I19** มีสี **medium sea green** เพราะค่าตรงกับกฎ “Yesterday”  
- เซลล์ **K20** ยังคงพื้นหลังค่าเริ่มต้น เนื่องจากวันที่ไม่ตรงกับเงื่อนไข  

นี่คือการ **format cells by date** ด้วยบรรทัดโค้ด Python เพียงบรรทัดเดียว

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกส่วนเข้าด้วยกัน นี่คือสคริปต์เต็มที่คุณสามารถคัดลอก‑วางและรันได้

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

รันสคริปต์ เปิดไฟล์ที่ได้และคุณจะเห็น conditional formatting ทำงาน

## ความแตกต่างทั่วไปและกรณีขอบ

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY` | Real‑time dashboards |
| **Multiple ranges** | Call `add_time_period` for each range, passing different colors | Complex reports |
| **Dynamic date range** | Use `TimePeriodType.LAST_7_DAYS` or `TimePeriodType.NEXT_MONTH` | Rolling reports |
| **Custom color** | Use `Color.from_argb(255, r, g, b)` to create any shade | Brand‑consistent styling |

**Pro tip:** Always set `condition.style.pattern = BackgroundType.SOLID` when you want a solid fill; otherwise Excel may display a gradient that looks inconsistent across versions.

## สรุป

ตอนนี้คุณรู้วิธี **สร้าง Excel workbook python** ที่ **ตั้งค่าสีพื้นหลังของเซลล์**, ใช้ **excel conditional formatting python**, และ **format cells by date** ด้วย Aspose.Cells ตัวอย่างนี้ครอบคลุมสถานการณ์ **date based conditional formatting** แต่รูปแบบเดียวกันสามารถใช้กับกฎช่วงเวลาอื่น ๆ ได้

ต่อไปคุณอาจสำรวจ:

- เพิ่ม data bars หรือ icon sets (`FormatConditionType.DATA_BAR`)  
- รวมหลายกฎ conditional บนช่วงเดียวกัน  
- ส่งออก workbook เป็น PDF (`SaveFormat.PDF`) เพื่อการรายงาน  

ลองเล่นกับสี, ช่วง, และประเภทช่วงเวลาเพื่อให้ตรงกับความต้องการของการรายงานของคุณเอง ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}