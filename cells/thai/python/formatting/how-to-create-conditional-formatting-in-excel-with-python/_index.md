---
category: general
date: 2026-11-16
description: สร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Python. เรียนรู้การเพิ่มช่วงการจัดรูปแบบตามเงื่อนไข,
  ไฮไลท์วันที่, และสร้างเวิร์กบุ๊กโดยอัตโนมัติ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: th
lastmod: 2026-11-16
og_description: สร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Python บทเรียนนี้แสดงวิธีเพิ่มช่วงการจัดรูปแบบตามเงื่อนไข,
  เน้นวันที่ และสร้างเวิร์กบุ๊ก
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: สร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Python – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: วิธีสร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Python
url: /th/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างการจัดรูปแบบตามเงื่อนไขใน Excel ด้วย Python

หากคุณต้องการ **สร้างการจัดรูปแบบตามเงื่อนไข** ในไฟล์ Excel ขณะทำงานด้วย Python คำแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด คุณจะได้เรียนรู้การ **สร้าง excel workbook python**‑style, กำหนดช่วงการจัดรูปแบบ, และไฮไลต์วันที่โดยไม่ต้องออกจาก IDE

การจัดรูปแบบตามเงื่อนไขช่วยให้คุณทำเครื่องหมายเซลล์ที่ตรงตามเกณฑ์เฉพาะได้อย่างชัดเจน—เหมาะสำหรับแดชบอร์ด, รายงาน, หรือแผ่นตรวจสอบข้อมูล เมื่อจบบทเรียนนี้คุณจะมีเวิร์กบุ๊กที่ทำงานเต็มรูปแบบซึ่งเปลี่ยนสีเซลล์ที่มีวันที่ “เมื่อวาน” เป็นสีชมพู ส่วนช่วงอื่นคงเป็นสีเขียว

## สิ่งที่คุณจะทำสำเร็จ

* สร้างเวิร์กบุ๊กใหม่ตั้งแต่ต้น  
* เพิ่มคอลเลกชันการจัดรูปแบบตามเงื่อนไขสำหรับบล็อกเซลล์เฉพาะ  
* ใช้กฎ **TIME_PERIOD** ที่ไฮไลต์วันที่ (สถานการณ์ “วิธีไฮไลต์วันที่”)  
* บันทึกไฟล์เป็นเวิร์กบุ๊ก XLSX พร้อมใช้งานสำหรับการประมวลผลต่อไป

**ข้อกำหนดเบื้องต้น**  
* Python 3.8+  
* แพคเกจ Python `aspose-cells` (`pip install aspose-cells`)  
* ความคุ้นเคยพื้นฐานกับโมดูล `datetime` ของ Python  

---

## วิธีสร้างการจัดรูปแบบตามเงื่อนไขใน Python

ขั้นตอนแรกคือการตั้งค่าเวิร์กบุ๊กและเวิร์กชีตที่จะเป็นที่เก็บกฎการจัดรูปแบบ

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**ทำไมจึงสำคัญ** – `Workbook` เป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมดกับ Excel การสร้างเวิร์กบุ๊กโดยโปรแกรมแทนขั้นตอน “File → New” แบบแมนนวล ทำให้สามารถสร้างสายงานรายงานอัตโนมัติได้

---

## การเตรียมคอลเลกชันการจัดรูปแบบตามเงื่อนไข – เพิ่มช่วงการจัดรูปแบบตามเงื่อนไข

ต่อไปเราจะกำหนดบล็อกเซลล์ที่จะรับกฎ ในตัวอย่างนี้ช่วงคือ **I19:K20**

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**คำอธิบาย** – `conditional_formattings.add` ลงทะเบียนคอลเลกชันใหม่ที่เชื่อมโยงกับสตริงที่อยู่ เงื่อนไขแรก (`conds[0]`) ทำหน้าที่เป็นสไตล์ “ค่าเริ่มต้น”; กฎต่อมาจะทับซ้อนเมื่อเงื่อนไขของมันเป็นจริง

---

## การเพิ่มเงื่อนไข TIME_PERIOD – วิธีไฮไลต์วันที่

ตอนนี้เราจะเพิ่มตรรกะที่ระบุวันที่ “เมื่อวาน” และทาสีชมพูให้เซลล์นั้น

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**ทำไมต้องใช้ TIME_PERIOD?** – Aspose.Cells มี enumeration ที่สร้างไว้แล้วเช่น `YESTERDAY`, `TODAY` และ `LAST_WEEK` พวกมันเปรียบเทียบค่าที่อยู่ในเซลล์กับวันที่ระบบปัจจุบัน ทำให้ไม่ต้องเขียนสูตรกำหนดเอง

---

## การใส่ข้อมูลตัวอย่าง – แสดงการทำงานของกฎ

เพื่อดูการจัดรูปแบบทำงาน เราจะใส่วันที่ที่ตรงกับกฎและอีกวันที่ไม่ตรง

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**หมายเหตุกรณีขอบ** – กฎ `TIME_PERIOD` ทำงานได้เฉพาะกับวันที่ *จริง* เท่านั้น หากเซลล์มีข้อความ (เช่น “N/A”) กฎจะถูกละเว้น ป้องกันการเปลี่ยนสีโดยไม่คาดคิด

---

## การบันทึกเวิร์กบุ๊ก – add conditional formatting python

สุดท้ายให้เขียนเวิร์กบุ๊กลงดิสก์ ไฟล์สามารถเปิดด้วยโปรแกรมสเปรดชีตใดก็ได้เพื่อยืนยันสีที่แสดง

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**ผลลัพธ์ที่คาดหวัง**  

| I19 (สีเขียว → สีชมพู) | J19 (สีเขียว) | K19 (สีเขียว) |
|--------------------------|---------------|---------------|
| 7/30/2008 (เมื่อวาน) | – | – |
| **I20**: ป้าย “Yesterday” | – | – |
| I21‑K21 (สีเขียว) | – | – |

เซลล์ **I19** จะปรากฏด้วยพื้นหลังสีชมพูเพราะวันที่ตรงกับช่วง “เมื่อวาน” ส่วน **K20** ยังคงสีเขียว

---

## คำถามที่พบบ่อยและเคล็ดลับปฏิบัติ

* **ฉันสามารถใช้ช่วงวันที่กำหนดเองแทนช่วงที่สร้างไว้ได้หรือไม่?**  
  ใช่. แทนที่ `condition.time_period` ด้วย `condition.formula1 = "TODAY()-1"` และตั้งค่า `condition.type = FormatConditionType.FORMULA`

* **ถ้าเวิร์กบุ๊กของฉันมีข้อมูลอยู่แล้วจะทำอย่างไร?**  
  ใช้ `worksheet.cells.import_data` เพื่อโหลดข้อมูลเป็นกลุ่มก่อนเพิ่มคอลเลกชันการจัดรูปแบบตามเงื่อนไข

* **ประสิทธิภาพกับชีตขนาดใหญ่เป็นอย่างไร?**  
  การเพิ่มเงื่อนไขหลาย ๆ ตัวอาจทำให้การแสดงผลช้าลง ให้รวมเซลล์ที่ใช้กฎเดียวกันเป็นช่วงเดียว (เช่น “A1:C1000”) เพื่อลดจำนวนเงื่อนไข

* **ความเข้ากันได้ข้ามแพลตฟอร์ม?**  
  ไฟล์ XLSX ที่สร้างขึ้นตามมาตรฐาน Office Open XML ทำงานได้บนแอปพลิเคชันสเปรดชีตของ Windows, macOS, และ Linux

---

## สรุป

ตอนนี้คุณรู้วิธี **สร้างการจัดรูปแบบตามเงื่อนไข** ในเวิร์กบุ๊ก Excel ด้วย Python แล้ว บทเรียนได้ครอบคลุมการสร้างเวิร์กบุ๊ก, การกำหนด **add conditional formatting range**, การใช้กฎ **how to highlight dates**, และการบันทึกไฟล์—ทั้งหมดด้วยวิธี **add conditional formatting python** ที่ Aspose.Cells จัดให้

ต่อจากนี้คุณสามารถ:

* ขยายชุดกฎด้วยค่า `TimePeriodType` อื่น ๆ (เช่น `TODAY`, `LAST_MONTH`)  
* รวมหลายเงื่อนไขในช่วงเดียวเพื่อให้ได้สัญญาณภาพที่หลากหลายขึ้น  
* ผสานกระบวนการนี้เข้ากับสายงานรายงานอัตโนมัติหรือเว็บเซอร์วิส

ขอให้สนุกกับการเขียนโค้ด และอย่ากลัวที่จะทดลองสี, ช่วง, และตรรกะวันที่ต่าง ๆ เพื่อให้ตรงกับความต้องการของรายงานของคุณ!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ ทุกแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}