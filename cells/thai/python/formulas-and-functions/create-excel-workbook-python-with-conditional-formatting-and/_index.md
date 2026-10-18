---
category: general
date: 2026-10-04
description: สร้างไฟล์ Excel ด้วย Python โดยใช้ Aspose.Cells เรียนรู้การจัดรูปแบบตามเงื่อนไขใน
  Excel ด้วย Python, การตั้งค่าสีพื้นหลังของเซลล์ด้วย Python, และการจัดรูปแบบวันที่ของเซลล์ด้วย
  Python ในตัวอย่างเต็ม.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: th
lastmod: 2026-10-04
og_description: สร้างไฟล์ Excel ด้วย Python และ Aspose.Cells บทเรียนนี้แสดงการจัดรูปแบบตามเงื่อนไขใน
  Excel ด้วย Python, การเปลี่ยนสีพื้นหลังของเซลล์ด้วย Python, และการจัดรูปแบบวันที่ของเซลล์ด้วย
  Python อย่างเป็นขั้นตอน.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: สร้างเวิร์กบุ๊ก Excel ด้วย Python – คู่มือเต็มพร้อมการจัดรูปแบบตามเงื่อนไข
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
title: สร้างไฟล์ Excel ด้วย Python พร้อมการจัดรูปแบบตามเงื่อนไขและสีพื้นหลังของเซลล์
url: /th/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel workbook python พร้อมการจัดรูปแบบตามเงื่อนไขและสีพื้นหลังของเซลล์

หากคุณต้องการ **create Excel workbook python** อย่างรวดเร็ว คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน คุณจะได้เห็นตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งเพิ่ม **excel conditional formatting python**, เปลี่ยน **cell background color python**, และ **format cells date python** เพื่อไฮไลท์ “Yesterday”.

ในหลายสถานการณ์การรายงาน การใช้สัญญาณสีของเซลล์ทำให้ข้อมูลเข้าใจได้ทันที บทเรียนนี้จะพาคุณผ่านทุกบรรทัดของโค้ด อธิบายว่าทำไมแต่ละขั้นตอนจึงสำคัญ และให้สคริปต์พร้อมรันที่คุณสามารถปรับใช้กับโปรเจกต์ของคุณได้

## สิ่งที่คุณจะทำสำเร็จ

โดยตอนจบของบทความนี้คุณจะสามารถ:

1. **create Excel workbook python** ด้วยไลบรารี Aspose.Cells.  
2. ใช้ **excel conditional formatting python** ที่ทำการไฮไลท์วันที่เป็น “Yesterday” โดยอัตโนมัติ.  
3. ตั้งค่า **cell background color python** เป็นสีชมพู (หรือสีใดก็ได้ที่คุณต้องการ).  
4. **format cells date python** เพื่อให้วันที่แสดงในรูปแบบวันที่มาตรฐานของ Excel.  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose.Cells มาก่อน—เพียงแค่มีสภาพแวดล้อม Python 3 ที่ทำงานได้และสามารถใช้ pip

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8 หรือใหม่กว่า.  
- แพ็กเกจ `aspose-cells` และ `aspose-pydrawing` ติดตั้งผ่าน `pip install aspose-cells aspose-pydrawing`.  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ Python และแนวคิดของ Excel (workbooks, worksheets, cells).  

> **Pro tip:** หากคุณรันสคริปต์ใน virtual environment คุณจะหลีกเลี่ยงความขัดแย้งของเวอร์ชันกับโปรเจกต์อื่น ๆ.

## Step 1: Set up the project and import required classes

ขั้นตอนแรกเมื่อคุณ **create Excel workbook python** คือการนำเข้าคลาสของ Aspose.Cells ที่คุณต้องการ คลาสเหล่านี้ให้การเข้าถึงโดยตรงในการสร้าง workbook, การจัดรูปแบบตามเงื่อนไข, และการสไตลิง

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

*Why this matters:* การนำเข้าเฉพาะสัญลักษณ์ที่จำเป็นทำให้ namespace สะอาดและทำให้สคริปต์อ่านง่ายขึ้น `Workbook` เป็นจุดเริ่มต้นสำหรับ **create Excel workbook python**, ส่วน `FormatConditionType` และ `TimePeriodType` มีความสำคัญสำหรับ **excel conditional formatting python**.

## Step 2: Create a new workbook and obtain the first worksheet

ตอนนี้เราจะ **create Excel workbook python** จริง ๆ ตัวสร้าง `Workbook()` จะให้ไฟล์ Excel ว่างเปล่าพร้อม worksheet เริ่มต้น

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* ทุกไฟล์ Excel จะเริ่มต้นด้วยอย่างน้อยหนึ่ง worksheet โดยค่าเริ่มต้น Aspose.Cells ตั้งชื่อว่า “Sheet1”. คุณสามารถเพิ่ม sheet เพิ่มเติมได้ในภายหลัง แต่สำหรับการสาธิตนี้ sheet เดียวทำให้ตัวอย่างโฟกัสได้ดี

## Step 3: Define the target range for conditional formatting

การจัดรูปแบบตามเงื่อนไขทำงานบนช่วงสี่เหลี่ยม เราเลือกช่วง `I19:K20` ซึ่งให้สามคอลัมน์และสองแถวให้เล่น

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* เมธอด `get` คืนค่าออบเจ็กต์ `ConditionalFormatting` ที่เชื่อมโยงกับช่วงที่ระบุ หากช่วงนั้นยังไม่มีการจัดรูปแบบใด ๆ Aspose.Cells จะสร้างคอลเลกชันใหม่โดยอัตโนมัติ

## Step 4: Add a TIME_PERIOD condition and set the background color

นี่คือหัวใจของ **excel conditional formatting python** เราเพิ่มกฎ `TIME_PERIOD` ที่ไฮไลท์เซลล์ที่มีวันที่เป็น “Yesterday”

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

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` บอก Excel ให้ประเมินวันที่สัมพันธ์กับวันที่ปัจจุบัน.  
- `TimePeriodType.YESTERDAY` เป็น enum ที่สร้างไว้แล้วซึ่งอัปเดตโดยอัตโนมัติทุกวัน ทำให้ workbook ไฮไลท์ “Yesterday” ล่าสุดเสมอ.  
- โดยการตั้งค่า `background_color` เป็น `Color.pink` และ pattern เป็น `SOLID` เราจะได้ผลลัพธ์ **cell background color python** โดยไม่ต้องใช้โค้ด VBA เพิ่มเติม.

## Step 5: Populate the range with sample dates and apply date formatting

เพื่อดูการจัดรูปแบบตามเงื่อนไขทำงาน เราต้องมีค่าที่เป็นวันที่จริง และต้อง **format cells date python** เพื่อให้ Excel จัดการเป็นวันที่ไม่ใช่ตัวเลขธรรมดา

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

*Explanation:*  
- บรรทัด `style.number = 30` คือขั้นตอน **format cells date python**. รหัสรูปแบบ 30 ตรงกับรูปแบบวันที่สั้น (`m/d/yy`).  
- การใช้ฟังก์ชันช่วยเหลือทำให้โค้ดเป็น DRY (Don’t Repeat Yourself) และง่ายต่อการเพิ่มวันที่เพิ่มเติมในภายหลัง.

## Step 6: Add a descriptive label

ป้ายกำกับเล็ก ๆ ช่วยให้ผู้เปิด workbook เข้าใจว่าทำไมเซลล์ถึงมีสี

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Step 7: Save the workbook to disk

สุดท้าย เรา **create Excel workbook python** บนดิสก์โดยเรียก `save`. ค่าคงที่ `SaveFormat.XLSX` ทำให้ไฟล์อยู่ในรูปแบบ Office Open XML สมัยใหม่

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

เมื่อคุณเปิด `TimePeriodDemo.xlsx` ใน Excel คุณจะเห็น:

- เซลล์ `I19` และ `K20` มีวันที่.  
- เซลล์ที่ตรงกับ “Yesterday” (ในตัวอย่างคงที่นี้คือ `I19`) จะถูกไฮไลท์เป็นสีชมพู.  
- ป้าย “Yesterday” ปรากฏใน `I20`.  

> **Tip:** หากคุณรันสคริปต์ในวันอื่น การจัดรูปแบบตามเงื่อนไขยังคงไฮไลท์เซลล์ที่มีวันที่เท่ากับหนึ่งวันก่อนวันที่ระบบปัจจุบัน—ไม่ต้องแก้ไขโค้ดใด ๆ.

## Full script – ready to copy and run

ด้านล่างเป็นโปรแกรมครบชุดที่รวมทุกขั้นตอนข้างต้น คัดลอกไปไฟล์ชื่อ `conditional_format_demo.py`, ปรับ `YOUR_DIRECTORY`, แล้วรันด้วย `python conditional_format_demo.py`

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

### Expected output

การรันสคริปต์จะแสดงบรรทัดยืนยัน:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

การเปิดไฟล์ที่สร้างขึ้นจะแสดงพื้นหลังสีชมพูบนเซลล์ที่ตรงกับกฎ “Yesterday”, ยืนยันว่า **excel conditional formatting python** และ **cell background color python** ทำงานร่วมกันอย่างถูกต้อง

## Common variations and edge cases

| สถานการณ์ | วิธีปรับโค้ด |
|-----------|-----------------------|
| **สีไฮไลท์ที่ต่างกัน** | เปลี่ยน `Color.pink` เป็นค่าสี `Color` อื่น ๆ เช่น `Color.light_green`. |
| **ไฮไลท์ “Today” แทน “Yesterday”** | ตั้งค่า `condition.time_period = TimePeriodType.TODAY`. |
| **ใช้การจัดรูปแบบกับคอลัมน์ทั้งหมด** | ใช้ช่วงเช่น `"A:A"` และปรับตัวแปร `target_range` ให้สอดคล้อง. |
| **ใช้รูปแบบวันที่แบบกำหนดเอง** | แทนที่ `style.number = 30` ด้วย `style.custom = "dd-mmm-yyyy"` เพื่อรูปแบบที่อ่านง่ายขึ้น. |
| **หลายเงื่อนไขบนช่วงเดียวกัน** |  |

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [สร้าง Excel Workbook Python – คู่มือเต็มด้วย Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [สร้างและบันทึก Excel Workbook เป็น PDF ใน ASP.NET ด้วย Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [วิธีสร้างและบันทึก Excel Workbook เป็น ODS ด้วย Aspose.Cells สำหรับ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}