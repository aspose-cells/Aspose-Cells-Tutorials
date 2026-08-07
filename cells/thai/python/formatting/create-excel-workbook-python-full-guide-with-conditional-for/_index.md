---
category: general
date: 2026-07-14
description: สร้างโค้ด Python เพื่อสร้างไฟล์ Excel ที่ตั้งค่าสีพื้นหลังของเซลล์, ไฮไลท์เซลล์ตามช่วงวันที่,
  และบันทึกเป็นไฟล์ XLSX ภายในไม่กี่นาที.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: th
lastmod: 2026-07-14
og_description: สร้างไฟล์ Excel ด้วย Python อย่างรวดเร็ว เรียนรู้การตั้งค่าสีพื้นหลังของเซลล์
  ไฮไลท์เซลล์ตามช่วงวันที่ และบันทึกไฟล์เป็น XLSX ด้วย Aspose.Cells
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: สร้างเวิร์กบุ๊ก Excel ด้วย Python – การจัดรูปแบบตามเงื่อนไขแบบทีละขั้นตอน
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
title: สร้างสมุดงาน Excel ด้วย Python – คู่มือเต็มพร้อมการจัดรูปแบบตามเงื่อนไข
url: /th/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel Workbook Python – คู่มือเต็มพร้อมการจัดรูปแบบตามเงื่อนไข

เคยสงสัยไหมว่า **create excel workbook python** สคริปต์ที่ดูเป็นมืออาชีพโดยไม่ต้องเปิด Excel ด้วยตนเอง? คุณไม่ได้เป็นคนเดียว ในหลายโครงการที่ขับเคลื่อนด้วยข้อมูล เราต้องสร้างสเปรดชีต, ทำสีเซลล์, และแม้กระทั่งทำเครื่องหมายวันที่อยู่ในช่วงที่กำหนด—ทั้งหมดจากโค้ด Python ธรรมดา

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และพร้อมรันที่ **creates an Excel workbook python** ด้วยไลบรารี Aspose.Cells, **sets cell background color**, ใช้ **conditional formatting based on date**, และสุดท้าย **saves workbook as xlsx**. เมื่อจบคุณจะได้สแนปช็อตที่นำกลับมาใช้ใหม่ได้ในพายป์ไลน์อัตโนมัติใด ๆ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการเริ่มต้น workbook และดึง worksheet แรกออกมา  
- ฟังก์ชันช่วยเหลือที่เพิ่ม collection ของ conditional‑formatting สำหรับช่วงเซลล์ใด ๆ  
- การใช้ **conditional formatting based on date** เพื่อไฮไลท์รายการของเมื่อวาน  
- การปรับความกว้างของคอลัมน์เพื่อให้เลย์เอาต์ดูเรียบร้อย  
- การบันทึกผลลัพธ์ด้วย **save workbook as xlsx**  

ไม่ต้องติดตั้ง Excel เพิ่มเติม—Aspose.Cells จัดการทุกอย่างในหน่วยความจำ

## ข้อกำหนดเบื้องต้น

- ติดตั้ง Python 3.8+  
- แพคเกจ `aspose-cells` (`pip install aspose-cells`)  
- ความคุ้นเคยพื้นฐานกับฟังก์ชัน Python และอ็อบเจ็กต์ datetime  

หากคุณยังไม่เคยใช้ Aspose.Cells มาก่อน คิดว่าเป็น API ที่ทรงพลังและเป็น Python‑pure ซึ่งจำลองโมเดลอ็อบเจ็กต์ของ Excel เหมือนจริง เหมาะสำหรับการสร้างไฟล์บนเซิร์ฟเวอร์ที่ไม่มีชุด Office

## ขั้นตอนที่ 1: เริ่มต้น Workbook (Create Excel Workbook Python)

ก่อนอื่นเราต้อง **create excel workbook python** แบบนี้ ขั้นตอนนี้จะสร้างอ็อบเจ็กต์ workbook ว่างเปล่าและชี้ไปที่ worksheet เริ่มต้น

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **ทำไมเรื่องนี้สำคัญ:** คลาส `Workbook` เป็นจุดเริ่มต้นของทุกการทำงานกับ Excel การสร้างมันโดยโปรแกรมทำให้หลีกเลี่ยงการจัดการไฟล์ด้วยมือ

## ขั้นตอนที่ 2: ตัวช่วยสำหรับเพิ่ม Conditional‑Formatting Collection (Set Cell Background Color)

Conditional formatting อยู่ภายใน *collection* ที่แนบกับช่วงเซลล์ เราจะห่อโค้ดซ้ำ ๆ นี้ในฟังก์ชันช่วยเหลือขนาดเล็กที่ยังให้เราสามารถ **set cell background color** ให้ทั้งช่วงได้

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

> **เคล็ดลับ:** การใช้ฟังก์ชันช่วยทำให้โฟลว์หลักของคุณสะอาดและง่ายต่อการนำกลับมาใช้กับหลายช่วง

## ขั้นตอนที่ 3: ใช้ Conditional Formatting ตามวันที่ (Highlight Cells Based on Date Range)

ตอนนี้เราจะ **highlight cells based on date range** จริง ๆ ตัวอย่างมุ่งเน้นที่ “เมื่อวาน” แต่คุณสามารถสลับ `TimePeriodType.YESTERDAY` เป็น `TODAY`, `LAST_WEEK` ฯลฯ

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

> **กำลังเกิดอะไรขึ้น?**  
> 1. เราให้ช่วงทั้งหมดมีพื้นหลังสีเขียวอ่อนเป็นค่าเริ่มต้น  
> 2. จากนั้นเพิ่มเงื่อนไข `TIME_PERIOD` ที่เปลี่ยนสีเติมเป็นสีชมพู **only** เมื่อวันที่ในเซลล์เท่ากับเมื่อวาน  
> 3. enum `TimePeriodType` จัดการคำนวณวันที่ให้โดยอัตโนมัติ ไม่ต้องเขียนโค้ดคำนวณเอง  

## ขั้นตอนที่ 4: เติมวันที่ตัวอย่าง (เพื่อให้กฎทำงานได้)

เพื่อดูกฎทำงาน เราจะใส่วันที่สองค่าลงในแผ่นงาน หนึ่งค่าจะอยู่ในช่วง “เมื่อวาน” อีกค่าหนึ่งไม่อยู่

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

> **หมายเหตุกรณีขอบ:** หาก workbook ของคุณจะเปิดในโลคัลต่าง ๆ ควรใช้ `date_style.custom = "dd‑mm‑yyyy"` เพื่อบังคับให้แสดงรูปแบบเดียวกัน

## ขั้นตอนที่ 5: จัดระเบียบเลย์เอาต์ (Auto‑Fit Columns)

สเปรดชีตที่แออัดดูไม่เป็นมืออาชีพ เรามา **adjust column width for a tidy output** กัน

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **ทำไมต้อง auto‑fit?** มันทำให้ป้ายชื่อหรือวันที่ยาวแสดงเต็มที่ ซึ่งสำคัญมากเมื่อคุณแชร์ไฟล์กับผู้ที่ไม่ใช่เทคนิค

## ขั้นตอนที่ 6: บันทึก Workbook (Save Workbook As XLSX)

สุดท้ายเราจะ **save workbook as xlsx** ไปยังตำแหน่งที่คุณเลือก ค่าคงที่ `SaveFormat.XLSX` บอก Aspose.Cells ให้เขียนเป็นรูปแบบ OpenXML สมัยใหม่

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **ผลลัพธ์ที่คุณควรเห็น:**  
> - เซลล์ I19 และ K20 มีวันที่  
> - I19 (เมื่อวาน) ถูกไฮไลท์เป็นสีชมพู ส่วน K20 ยังคงสีเขียว  
> - คอลัมน์ L ขยายอัตโนมัติเพื่อให้พอดีกับป้าย “Yesterday”  

หากคุณเปิดไฟล์ `TimePeriodDemo.xlsx` ใน Excel การจัดรูปแบบตามเงื่อนไขจะถูกนำไปใช้แล้ว—ไม่ต้องทำขั้นตอนเพิ่มใด ๆ

---

![แผ่น Excel แสดงวันที่ที่ไฮไลท์เป็นเมื่อวาน](https://example.com/images/excel-demo.png "ภาพหน้าจอของไฟล์ Excel ที่สร้างขึ้นพร้อมเซลล์ที่ไฮไลท์")

*ภาพด้านบนแสดง workbook สุดท้าย; สังเกตการไฮไลท์สีชมพูบนเซลล์ที่มีวันที่ของเมื่อวาน*

## สรุป: สิ่งที่เราบรรลุ

- **Created an Excel workbook python** ตั้งแต่ต้นด้วย Aspose.Cells  
- **Set cell background color** ให้ทั้งช่วงเพื่อให้แผ่นงานมีสัญญาณภาพ  
- ใช้ **conditional formatting based on date** เพื่อทำเครื่องหมายรายการของเมื่อวานโดยอัตโนมัติ  
- **Saved workbook as xlsx** พร้อมใช้งานหรือส่งต่อต่อไป  

ทั้งหมดนี้ทำได้ภายในไม่ถึง 60 บรรทัดของ Python และโค้ดทำงานบนแพลตฟอร์มใด ๆ ที่รองรับ runtime ของ Aspose.Cells

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

หากคุณพบว่าบทนี้มีประโยชน์ คุณอาจอยากสำรวจต่อ:

- **set cell background color** สำหรับแถวทั้งหมดตามค่าระดับสถานะ (เช่น “Completed”, “Pending”)  
- ใช้ **highlight cells based on date range** เพื่อสร้างหน้าต่างเวลาที่เคลื่อนที่ (7 วันล่าสุด, เดือนปัจจุบัน)  
- ส่งออกเป็นรูปแบบอื่นเช่น **CSV** หรือ **PDF** ด้วย `SaveFormat.CSV` หรือ `SaveFormat.PDF`  
- เพิ่ม **charts** ด้วยโปรแกรมเพื่อแสดงภาพข้อมูลที่คุณเพิ่งจัดรูปแบบ  

ปรับเปลี่ยนตรรกะของวันที่, สลับพาเล็ตสี, หรือขยายช่วงให้ครอบคลุมคอลัมน์ทั้งหมดได้ตามต้องการ รูปแบบยังคงเหมือนเดิม: สร้าง workbook, แนบ collection ของ conditional‑formatting, กำหนดกฎ, แล้วบันทึก

มีคำถามเกี่ยวกับกรณีการใช้งานเฉพาะ? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}