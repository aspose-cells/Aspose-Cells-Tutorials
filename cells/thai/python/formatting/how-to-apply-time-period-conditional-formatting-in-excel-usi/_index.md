---
category: general
date: 2026-09-15
description: เรียนรู้วิธีใช้การจัดรูปแบบตามเงื่อนไขช่วงเวลาและบันทึกเวิร์กบุ๊กเป็นไฟล์
  XLSX ด้วย Aspose.Cells ใน Python พร้อมโค้ดขั้นตอนโดยละเอียด
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: th
lastmod: 2026-09-15
og_description: ใช้การจัดรูปแบบตามเงื่อนไขตามช่วงเวลาใน Excel ด้วย Python และบันทึกเวิร์กบุ๊กเป็นไฟล์
  XLSX. ตามคู่มือฉบับสมบูรณ์สำหรับ Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: ใช้การจัดรูปแบบตามเงื่อนไขตามช่วงเวลาใน Excel ด้วย Python
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
title: วิธีใช้การจัดรูปแบบตามเงื่อนไขตามช่วงเวลาใน Excel ด้วย Python
url: /th/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้การจัดรูปแบบตามเงื่อนไขช่วงเวลาใน Excel ด้วย Python

หากคุณต้องการ **time period conditional formatting** ในไฟล์ Excel, บทแนะนำนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าทำอย่างไรด้วย Python คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งสร้าง workbook, ไฮไลต์วันที่ของเมื่อวาน, และ **save workbook as XLSX** เพียงไม่กี่บรรทัดของโค้ด

การจัดรูปแบบตามเงื่อนไขเป็นวิธีที่ทรงพลังในการดึงความสนใจไปยังข้อมูลที่ตรงตามกฎเฉพาะ ในคู่มือนี้เราจะเน้นที่ช่วงเวลา “Yesterday” แต่รูปแบบเดียวกันก็ใช้ได้กับช่วงเวลาในตัวอื่น ๆ เช่น Today, LastWeek, และ NextMonth เมื่อจบบทแนะนำคุณจะสามารถสร้างสคริปต์ **how to create excel workbook python**‑style ที่พร้อมใช้งานในขั้นตอนการผลิต

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+  
- `aspose-cells` and `aspose-pydrawing` packages (`pip install aspose-cells aspose-pydrawing`)  
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ของ Python  

ไม่จำเป็นต้องติดตั้ง Office เพิ่มเติมใด ๆ เนื่องจาก Aspose.Cells จัดการการสร้างไฟล์ภายในเอง.

## การจัดรูปแบบตามเงื่อนไขช่วงเวลา ด้วย Aspose.Cells ใน Python

ส่วนนี้จะอธิบายทุกบรรทัดของโค้ดที่จำเป็นสำหรับงานหลัก โค้ดบล็อกด้านล่างเป็นสคริปต์เต็ม; คอมเมนต์อธิบายวัตถุประสงค์ของแต่ละขั้นตอน.

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

### ทำไมแต่ละขั้นตอนจึงสำคัญ

1. **Creating the workbook** ให้คุณได้ไฟล์ Excel ในหน่วยความจำที่สามารถจัดการได้โดยไม่ต้องเปิด Excel.  
2. **Defining the range** (`I19:K20`) บอก Aspose.Cells ว่ากฎจะใช้ที่ไหน ทำให้ตรรกะแยกออกจากกัน.  
3. **Adding a TIME_PERIOD condition** ใช้ enumeration ในตัวของ Aspose `TimePeriodType.YESTERDAY` ซึ่งช่วยหลีกเลี่ยงการคำนวณวันที่ด้วยตนเองและอัปเดตโดยอัตโนมัติเมื่อไฟล์เปิดในวันอื่น.  
4. **Setting the style** (`background_color` และ `pattern`) กำหนดลักษณะการแสดงของเซลล์ที่ไฮไลต์ การใช้ `Color.pink` ทำให้กฎง่ายต่อการมองเห็น.  
5. **Writing sample dates** ด้วยรูปแบบตัวเลข 30 ทำให้ Excel แสดงเป็นวันที่สั้นแทนเลขซีเรียล.  
6. **Auto‑fitting the column** ปรับความกว้างคอลัมน์อัตโนมัติเพื่อเพิ่มความอ่านง่ายสำหรับผู้ที่เปิดไฟล์ในภายหลัง.  
7. **Saving as XLSX** สร้างไฟล์ที่เข้ากันได้อย่างกว้างขวางซึ่งสามารถเปิดได้ใน Excel, Google Sheets หรือโปรแกรมสเปรดชีตสมัยใหม่ใด ๆ.

## วิธีสร้าง Excel workbook แบบ Python‑style ด้วย Aspose.Cells

สคริปต์ข้างต้นได้แสดงขั้นตอนขั้นต่ำเพื่อ **how to create excel workbook python** แล้ว ในการใช้งานจริงคุณอาจต้องการ:

- เพิ่มหลายแผ่นงาน (`workbook.worksheets.add("Report")`).  
- เติมตารางข้อมูลขนาดใหญ่ด้วยลูปหรือ pandas DataFrames (`worksheet.cells.import_data_table`).  
- ใช้การจัดรูปแบบเพิ่มเติม (ฟอนต์, เส้นขอบ) ด้วย `cell.get_style()`.

การกระทำทั้งหมดนี้ทำตามรูปแบบเดียวกัน: รับอ็อบเจ็กต์, แก้ไขคุณสมบัติ, และเรียก `set_style` หรือ `save`.

## เพิ่มการจัดรูปแบบตามเงื่อนไขใน Python – รูปแบบที่เป็นประโยชน์อื่น ๆ

นอกเหนือจากตัวอย่าง “Yesterday”, Aspose.Cells รองรับหลายประเภทของการจัดรูปแบบตามเงื่อนไข:

| FormatConditionType | กรณีการใช้งานทั่วไป |
|---------------------|----------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | สูตรกำหนดเอง (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | การเปรียบเทียบง่าย (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | สเกลสีแบบไล่ระดับ |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | การแสดงผลบาร์ในเซลล์ |

เพื่อ **add conditional formatting python** สำหรับเกณฑ์เชิงตัวเลข คุณจะต้องแทนที่ `FormatConditionType.TIME_PERIOD` ด้วย `FormatConditionType.CELL_VALUE` และตั้งค่า `condition.operator_type` และ `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## บันทึก workbook เป็น XLSX – แนวทางปฏิบัติที่ดีที่สุด

เมื่อคุณ **save workbook as xlsx**, ควรพิจารณา:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) เพื่อหลีกเลี่ยงรูปแบบเก่า.  
- **Using a deterministic file name** หากสคริปต์ทำงานในลูป (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) ในบริการที่ทำงานต่อเนื่องเพื่อคืนหน่วยความจำเนทีฟ.

ตัวอย่างนี้ใช้ `SaveFormat.XLSX` อยู่แล้ว ซึ่งสร้าง workbook แบบ zip‑based สมัยใหม่ที่คงกฎการจัดรูปแบบตามเงื่อนไขทั้งหมด.

## ไฮไลต์ Yesterday ใน Excel – ขั้นตอนการตรวจสอบ

หลังจากรันสคริปต์, เปิดไฟล์ `TimePeriodExample.xlsx`:

1. เซลล์ `I19` และ `K20` มีวันที่ `30‑07‑2008` และ `03‑08‑2008`.  
2. เซลล์ `I20` แสดงข้อความ “Yesterday”.  
3. หากคุณเปลี่ยนวันที่ระบบเป็น **July 30 2008** และเปิดไฟล์ใหม่, เซลล์ที่ตรงกับวันที่จะถูกเติมสีชมพูโดยอัตโนมัติ.  
4. การเปลี่ยนวันที่ระบบเป็นวันอื่นใดจะลบการเติมสีชมพู, ยืนยันว่ากฎตอบสนองต่อตรรกะ **time period conditional formatting**.

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

- **Missing `aspose-pydrawing`** – คลาส `Color` อยู่ในแพ็กเกจนี้; การลืมติดตั้งจะทำให้เกิด `ImportError`.  
- **Incorrect number format** – การใช้รูปแบบ General เริ่มต้นจะแสดงเลขซีเรียล (เช่น 39822) ควรตั้งค่า `style.number = 30` เสมอสำหรับวันที่สั้น.  
- **Range mismatch** – ช่วงของการจัดรูปแบบตามเงื่อนไขต้องครอบคลุมเซลล์ที่ต้องการไฮไลต์; หากไม่เช่นนั้นกฎจะไม่มีผล.

## เคล็ดลับมืออาชีพ: ใช้ซ้ำ routine การจัดรูปแบบ

หากคุณต้องการกฎ “Yesterday” เดียวกันในหลาย workbook, ให้ห่อหุ้มตรรกะในฟังก์ชันช่วยเหลือ:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

เรียก `apply_yesterday_highlight(worksheet, "A1:A10")` ตามที่ต้องการ.

## สรุป

คู่มือนี้แสดงให้คุณเห็นวิธีทำ **time period conditional formatting** ใน Excel ด้วย Python, วิธี **save workbook as XLSX**, และวิธี **highlight yesterday in Excel** ด้วยสคริปต์เดียวที่สามารถใช้ซ้ำได้ ตอนนี้คุณมีพื้นฐานที่มั่นคงในการเพิ่มโค้ด **add conditional formatting python** ไปยังโครงการอัตโนมัติใด ๆ ไม่ว่าจะเป็นการสร้างรายงานประจำวัน, สร้างแดชบอร์ด, หรือเตรียมส่งออกข้อมูล

**Next steps**

- สำรวจค่า `TimePeriodType` อื่น ๆ เช่น `TODAY` หรือ `LAST_WEEK`.  
- รวมหลายกฎการจัดรูปแบบตามเงื่อนไขในช่วงเดียวกันเพื่อให้สัญญาณภาพที่หลากหลายขึ้น.  
- ผสานการสร้าง workbook เข้ากับเว็บเซอร์วิสหรืองานที่กำหนดเวลา.

ขอให้สนุกกับการเขียนโค้ด, และเพลิดเพลินกับความชัดเจนของภาพที่การจัดรูปแบบตามเงื่อนไขนำมาสู่การอัตโนมัติใน Excel ของคุณ!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ.

- [ทำความเข้าใจการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Aspose.Cells .NET : คู่มือเชิงลึก](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [ทำความเชี่ยวชาญ Aspose.Cells .NET : ใช้การจัดรูปแบบตามเงื่อนไขกับแถวสลับใน Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [ทำความเชี่ยวชาญการจัดรูปแบบตามเงื่อนไขด้วยฟอนต์กำหนดเองใน Excel โดยใช้ Aspose.Cells สำหรับ .NET และ C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}