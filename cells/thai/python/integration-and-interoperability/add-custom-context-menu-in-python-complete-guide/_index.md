---
category: general
date: 2026-06-30
description: เพิ่มเมนูบริบทแบบกำหนดเองให้กับกริด Excel ใน Python และเขียนค่าลงในเซลล์
  Excel พร้อมบันทึกไฟล์ที่อัปเดต เรียนรู้การสร้างเมนูคลิกขวาและอัปเดตค่าของเซลล์ในสไตล์
  Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: th
og_description: เพิ่มเมนูบริบทแบบกำหนดเองใน Python เพื่อเขียนค่าลงในเซลล์ Excel และบันทึกไฟล์
  Excel ที่อัปเดต คู่มือฉบับนี้จะพาคุณผ่านขั้นตอนการสร้างเมนูคลิกขวาด้วย GridJs.
og_title: เพิ่มเมนูคอนเท็กซ์แบบกำหนดเองใน Python – บทเรียนขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: เพิ่มเมนูบริบทแบบกำหนดเองใน Python – คู่มือฉบับสมบูรณ์
url: /th/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มเมนูบริบทแบบกำหนดเองใน Python – คู่มือเต็ม

เคยสงสัยไหมว่าจะแนบรายการ **add custom context menu** ไปยังกริดสเปรดชีตที่คุณให้บริการจาก Python อย่างไร? บางทีคุณอาจต้องการปุ่ม “Mark as Reviewed” ที่ปรากฏเมื่อผู้ใช้คลิกขวาที่เซลล์, เขียนค่าลงในเซลล์ Excel, แล้วบันทึกเวิร์กบุ๊กที่อัปเดต—ทั้งหมดโดยไม่ต้องออกจาก web UI.  

ในบทแนะนำนี้เราจะสร้างสิ่งนั้นอย่างแม่นยำ: **custom right‑click menu** ที่ขับเคลื่อนโดย GridJs, ตัวจัดการฝั่งเซิร์ฟเวอร์ที่ **write(s) value to excel cell**, และขั้นตอนสุดท้ายที่ **save(s) updated excel file** บนดิสก์. เมื่อจบคุณจะมีรูปแบบที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถใส่ลงในโปรเจกต์ Flask, FastAPI หรือ Django ใดก็ได้.

> **Why care?**  
> การเพิ่มเมนูบริบทแบบกำหนดเองช่วยทำให้กระบวนการตรวจทานข้อมูลเป็นระเบียบ ลดการคัดลอก‑วางด้วยมือ และให้ผู้ใช้ปลายทางได้รับประสบการณ์ที่รู้สึกเป็นธรรมชาติโดยตรงในกริด นอกจากนี้คุณจะได้เห็นวิธี **update cell value python**‑style ซึ่งเป็นทักษะสำคัญสำหรับงานอัตโนมัติของ Excel ใด ๆ.

## ความต้องการเบื้องต้น

- Python 3.9+ (โค้ดทำงานบน 3.10 ด้วย)  
- `openpyxl` สำหรับการจัดการไฟล์ Excel  
- `gridjs` Python wrapper (หรือไลบรารี JS หากคุณต้องการฝั่งหน้า)  
- เว็บเฟรมเวิร์กพื้นฐาน (ตัวอย่าง Flask แสดง)  
- ไฟล์เวิร์กบุ๊กชื่อ `sample.xlsx` ในโฟลเดอร์โปรเจกต์ของคุณ  

หากคุณขาดส่วนใดส่วนหนึ่งเหล่านี้, ให้รัน:

```bash
pip install openpyxl flask gridjs
```

ตอนนี้มาเริ่มกันเลย.

---

## ขั้นตอนที่ 1 – Add Custom Context Menu: เริ่มต้น GridJs และผูก Worksheet

สิ่งแรกที่คุณต้องทำคือสร้างอินสแตนซ์ `GridJs` แล้วชี้ไปที่ worksheet ที่คุณตั้งใจจะทำงานด้วย นี่คือจุดที่วลี **add custom context menu** ปรากฏเป็นครั้งแรกในโค้ดของเราและเป็นการตั้งพื้นฐานสำหรับทุกอย่างต่อไป

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**What’s happening?**  
`grid.set_worksheet(ws)` บอก GridJs ให้ใช้ข้อมูลจาก `ws` เป็นแหล่งข้อมูล จากนี้ไป การแก้ไข context‑menu ใด ๆ ที่เราติดตั้งจะอัตโนมัติเชื่อมกับ worksheet เดียวกัน ทำให้ UI และไฟล์สอดคล้องกัน

> **Pro tip:** เปิดเวิร์กบุ๊กในโหมดอ่าน/เขียนเพียงครั้งเดียว การเปิดหลายครั้งภายใน request handler อาจทำให้เกิดปัญหา file‑locking บน Windows.

---

## ขั้นตอนที่ 2 – Write Value to Excel Cell: กำหนดการกระทำสำหรับรายการเมนู

เมื่อกริดพร้อมแล้ว, เราต้อง **write value to excel cell** เมื่อผู้ใช้เลือกคำสั่งที่กำหนดเองของเรา เราจะเพิ่มรายการเมนูชื่อ “Mark as Reviewed” และกำหนดตัวระบุ `markReviewed`. ตัวระบุนี้คือสิ่งที่ JavaScript ฝั่งไคลเอนต์จะส่งกลับไปยังเซิร์ฟเวอร์.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Why use a custom identifier?**  
ตัวระบุทำให้ข้อความ UI แยกจากตรรกะของเซิร์ฟเวอร์, ทำให้คุณสามารถเปลี่ยนป้ายชื่อโดยไม่ต้องแก้ไขโค้ดแบ็กเอนด์ นอกจากนี้ยังทำให้การดำเนินการ **create right‑click menu** ชัดเจนและนำกลับมาใช้ใหม่ได้

---

## ขั้นตอนที่ 3 – Create Right‑Click Menu: ลงทะเบียนตัวจัดการฝั่งเซิร์ฟเวอร์

เมื่อเมนูรายการพร้อมแล้ว, เราต้องบอก GridJs ว่าจะทำอะไรเมื่อผู้ใช้คลิก นี่คือจุดที่เราติดตั้งฟังก์ชัน **create right‑click menu** ที่ส่งคำขอกลับไปยัง Python จริง ๆ

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

สิ่งที่ควรทราบบางประการ:

1. **`ws[cell_address] = "Reviewed"`** เป็นวิธีที่ตรงที่สุดในการ **update cell value python**. ภายใต้การทำงาน, `openpyxl` จะแปลงที่อยู่รูปแบบ A1 ให้เป็นดัชนีแถว/คอลัมน์.
2. ตัวจัดการจะคืนค่า JSON เล็ก ๆ GridJs คาดหวังตัวบ่งชี้สถานะ; คุณสามารถขยายให้รวมข้อความข้อผิดพลาดได้หากต้องการ.

ตอนนี้เราผูกตัวระบุกับตัวจัดการ:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**What if the cell is empty or protected?**  
- เซลล์ว่างไม่มีปัญหา—`openpyxl` จะสร้างขึ้นโดยอัตโนมัติ.  
- สำหรับชีตที่ป้องกัน, คุณต้องยกเลิกการป้องกันก่อน (`ws.protection.sheet = False`) หรือจับ `PermissionError`.

---

## ขั้นตอนที่ 4 – Update Cell Value Python: บันทึกการเปลี่ยนแปลงโดยการบันทึกเวิร์กบุ๊ก

การเขียนค่ามีเพียงครึ่งหนึ่งของเรื่อง; คุณต้อง **save updated excel file** เพื่อให้การเปลี่ยนแปลงคงอยู่หลังเซสชันนี้ นี่คือจุดที่เราสรุปการเดินทางรอบจาก UI ไปยังดิสก์.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Why a separate folder?**  
การบันทึกลงในไดเรกทอรี `output/` ทำให้เทมเพลตต้นฉบับไม่ถูกแก้ไข ซึ่งเป็นประโยชน์สำหรับการตรวจสอบย้อนหลัง ปรับเส้นทางให้ตรงกับสภาพแวดล้อมการปรับใช้ของคุณ.

> **Watch out:** หากคุณให้บริการผู้ใช้หลายคนพร้อมกัน, ควรใช้ lock ที่ปลอดภัยต่อเธรด (`threading.Lock`) รอบ `wb.save()` เพื่อหลีกเลี่ยง race conditions.

---

## ขั้นตอนที่ 5 – Generate Client Configuration JSON and Wire It All Together

สุดท้าย, เราต้องสร้าง JSON ที่อินสแตนซ์ GridJs ฝั่งหน้าเว็บจะใช้ JSON นี้ประกอบด้วยข้อมูล worksheet **และ** คำจำกัดความของเมนูแบบกำหนดเอง.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

เมื่อคุณฝัง `config_json` ลงในหน้า HTML, GridJs จะเรนเดอร์กริดพร้อมรายการ “Mark as Reviewed” ที่สามารถคลิกขวาได้บนทุกเซลล์.

### ตัวอย่าง Flask เต็ม

ด้านล่างเป็นแอป Flask ขนาดเล็กที่รวมทุกส่วนเข้าด้วยกัน รันมัน, เปิด `http://localhost:5000` และคลิกขวาที่เซลล์ใดก็ได้เพื่อดูเมนูแบบกำหนดเองทำงาน.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Expected outcome:**  
- คลิกขวาที่เซลล์ใดก็ได้ → ปรากฏ “Mark as Reviewed”.  
- คลิกมัน → เนื้อหาเซลล์เปลี่ยนเป็น “Reviewed”.  
- เวิร์กบุ๊ก `output/sample-updated.xlsx` ตอนนี้มีค่าที่เพิ่มใหม่แล้ว.

---

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| *ถ้าฉันต้องการหลายการกระทำแบบกำหนดเอง?* | เพียงเพิ่มอ็อบเจกต์เพิ่มเติมใน `grid.settings.context_menu.custom_items` และลงทะเบียนแต่ละรายการด้วยตัวระบุของมันเอง. |
| *ฉันสามารถส่งข้อมูลเพิ่มเติม (เช่น row ID) ไปยังตัวจัดการได้หรือไม่?* | ได้. ใส่คีย์เพิ่มเติมใน payload JSON ฝั่งไคลเอนต์, แล้วอ่านจาก `request` ใน `on_custom_command`. |
| *วิธีนี้เข้ากันได้กับเฟรมเวิร์กแบบ async หรือไม่?* | แน่นอน—เพียงทำให้ `on_custom_command` เป็นฟังก์ชัน async และใช้ `await wb.save(...)` หากคุณเปลี่ยนไปใช้ `aiofiles` หรือคล้ายกัน. |
| *ฉันจะสไตล์ไอคอนเมนูอย่างไร?* | ระบุชื่อ Material‑Icons ใดก็ได้ (`"icon": "edit"`). ฝั่งหน้าเว็บจะโหลดฟอนต์ไอคอนโดยอัตโนมัติ. |
| *ทำอย่างไรกับเวิร์กบุ๊กขนาดใหญ่?* | โหลดเฉพาะชีตที่ต้องการเท่านั้น, และพิจารณา stream แถวด้วย `openpyxl.iter_rows()` เพื่อรักษาการใช้หน่วยความจำ |

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}