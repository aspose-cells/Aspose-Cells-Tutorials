---
category: general
date: 2026-06-30
description: เพิ่มเมนูบริบทแบบกำหนดเองใน GridJs และเรียนรู้วิธีโหลดเวิร์กบุ๊ก Excel,
  อัปเดตค่าของเซลล์, เปิดใช้งานการตรวจสอบการสะกด, และลงทะเบียนคำสั่งแบบกำหนดเอง.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: th
og_description: เพิ่มเมนูคลิกขวาที่กำหนดเองใน GridJs พร้อมเรียนรู้การโหลดไฟล์ Excel,
  ปรับค่าเซลล์, เปิดใช้งานการตรวจสอบการสะกด, และลงทะเบียนคำสั่งที่กำหนดเอง
og_title: เพิ่มเมนูคอนเท็กซ์แบบกำหนดเองใน GridJs – สอน Python ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: เพิ่มเมนูคอนเท็กซ์แบบกำหนดเองใน GridJs – คู่มือ Python ฉบับสมบูรณ์
url: /th/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มเมนูบริบทแบบกำหนดเองใน GridJs – คู่มือ Python ฉบับสมบูรณ์

เคยสงสัยไหมว่า **เพิ่มรายการเมนูบริบทแบบกำหนดเอง** ลงในตาราง GridJs ที่เชื่อมต่อกับไฟล์ Excel workbook อย่างไร? คุณไม่ได้เป็นคนเดียวที่มีคำถามนี้ ในแอปที่มีข้อมูลจำนวนมากหลายแอปคุณต้องการเมนูคลิกขวาเพื่อให้ผู้ใช้ทำเครื่องหมายแถว, ระบุรายการว่าได้รับการตรวจสอบแล้ว, หรือเรียกการทำงานฝั่งเซิร์ฟเวอร์—โดยไม่ต้องออกจากกริด  

ในบทเรียนนี้เราจะพาคุณผ่านการโหลด Excel workbook, การเชื่อมต่อรายการเมนูบริบทแบบกำหนดเอง, การอัปเดตค่าเซลล์, การเปิดใช้งานการตรวจสอบการสะกด, และการลงทะเบียนคำสั่งแบบกำหนดเองที่บันทึกการเปลี่ยนแปลงกลับไปยังไฟล์ เมื่อเสร็จสิ้นคุณจะมีอินสแตนซ์ GridJs ที่ทำงานเต็มรูปแบบและเขียนกลับไปยังสเปรดชีตต้นฉบับโดยตรง

## ข้อกำหนดเบื้องต้น

- Python 3.9+ (โค้ดใช้ type hints แต่ทำงานได้กับเวอร์ชันล่าสุดใดก็ได้)  
- ไลบรารี `cells` (หรือ wrapper ใดก็ได้ที่จัดการ Excel แล้วให้วัตถุ `Workbook` และ `Worksheet`)  
- การผูก `gridjs` สำหรับ Python (โมเดลอ็อบเจกต์จะสะท้อน API ของ JavaScript)  
- ความเข้าใจพื้นฐานเกี่ยวกับ lambda และโครงสร้าง JSON  

ถ้าคุณมีทั้งหมดนี้แล้ว มาเริ่มกันเลย

## ขั้นตอนที่ 1: โหลด Excel Workbook และเลือก Worksheet

สิ่งแรกที่ต้องทำคือ **โหลด excel workbook** เพื่อให้ GridJs มีข้อมูลให้แสดง คลาส `cells.Workbook` จะจัดการไฟล์‑IO ให้คุณและให้เข้าถึงแถว, คอลัมน์, และเซลล์แต่ละเซลล์โดยตรง

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลด workbook ล่วงหน้าทำให้กริดสามารถดึงข้อมูลตามต้องการได้ และการแก้ไขใด ๆ ที่คุณทำต่อไป (เช่น **update cell value**) จะถูกบันทึกลงไฟล์เดียวกัน

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ GridJs และผูกกับ Worksheet

ต่อไปเราจะสร้างอ็อบเจกต์ `gridjs.GridJs` แล้วบอกให้มันเรนเดอร์ Worksheet ที่เลือกไว้ คิดว่าเป็นการให้ GridJs มีแหล่งข้อมูลสดที่มันสามารถ query ได้ทุกครั้งที่ต้องการเรนเดอร์หน้า หรือโหลดข้อมูลแบบ lazy‑load

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **เคล็ดลับ:** หากคุณทำงานกับหลายชีต เพียงเรียก `grid.set_worksheet(other_ws)` ภายหลัง—ไม่ต้องสร้างกริดใหม่

## ขั้นตอนที่ 3: เปิดใช้งานการตรวจสอบการสะกด (และฟีเจอร์อื่น ๆ)

แอปธุรกิจส่วนใหญ่ให้ผู้ใช้พิมพ์โน้ตแบบอิสระ การเปิด **spell checking** จะลดข้อผิดพลาดและปรับคุณภาพข้อมูล GridJs มีแฟล็กง่าย ๆ สำหรับการเปิดใช้งานนี้

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **ทำไมต้องเปิดการตรวจสอบการสะกด?** มันทำงานบนฝั่งไคลเอนต์ ให้ฟีดแบ็กทันทีโดยไม่ต้องเรียกเซิร์ฟเวอร์เพิ่ม—เหมาะกับชีตขนาดใหญ่

## ขั้นตอนที่ 4: เพิ่มรายการเมนูบริบทแบบกำหนดเอง

นี่คือหัวใจของบทเรียน: **add custom context menu** entries เราจะสร้างตัวเลือก “Mark as Reviewed” ที่เมื่อคลิกจะเรียกคำสั่งฝั่งเซิร์ฟเวอร์ที่เราจะกำหนดต่อไป

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **ภาพประกอบ**  
> ![ภาพหน้าจอเมนูบริบทแบบกำหนดเองที่แสดงตัวเลือกคลิกขวา](/images/add-custom-context-menu.png "ตัวอย่างเมนูบริบทแบบกำหนดเอง")

ข้อความ alt ด้านบนมีคีย์เวิร์ดหลักเพื่อให้สอดคล้องกับข้อกำหนด SEO

## ขั้นตอนที่ 5: ลงทะเบียนคำสั่งแบบกำหนดเองเพื่ออัปเดตค่าเซลล์

เมื่อผู้ใช้เลือก “Mark as Reviewed” เราต้อง **register custom command** ที่อัปเดตเซลล์ Excel ที่เกี่ยวข้องและบันทึกไฟล์ วิธี `grid.register_custom_command` จะผูกฟังก์ชัน Python กับตัวระบุการกระทำที่เราตั้งไว้ก่อนหน้า

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **ทำไมวิธีนี้ถึงได้ผล:** ตัวจัดการรับอ้างอิงเซลล์จากไคลเอนต์, ใช้ API ของ `Worksheet` เพื่อ **update cell value**, แล้วเขียน workbook ทั้งหมดกลับไปยังดิสก์ การตอบกลับบอกให้ฟรอนท์‑เอนด์ทราบว่าการดำเนินการสำเร็จ

### การจัดการกรณีขอบ

- **Missing cell reference:** หาก `req` ไม่มี `"cell"` ให้โยนข้อผิดพลาดที่ชัดเจนเพื่อให้ UI แสดง toast  
- **Concurrent edits:** สำหรับสถานการณ์ที่มีการแก้ไขพร้อมกันหลายคน ควรพิจารณาล็อก workbook หรือใช้ version‑stamp เพื่อหลีกเลี่ยง race condition

## ขั้นตอนที่ 6: เปิดใช้งาน Lazy Loading สำหรับชีตขนาดใหญ่

หากคุณต้องจัดการกับแถวหลายพันแถว Lazy Loading จะทำให้ UI ตอบสนองเร็วขึ้น ตั้งค่า page size ให้เหมาะสม—เช่น 500 แถว ทำงานได้ดีในเบราว์เซอร์ส่วนใหญ่

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **ถ้าคุณมี 10 000 แถว?** กริดจะร้องขอข้อมูลเป็นหน้า ๆ ลดความกดดันของหน่วยความจำทั้งบนไคลเอนต์และเซิร์ฟเวอร์

## ขั้นตอนที่ 7: (ทางเลือก) เพิ่ม Modal แบบกำหนดเองสำหรับการแก้ไขแถว

บางครั้งคุณต้องการ UI ที่ซับซ้อนกว่าตัวแก้ไขแบบอินไลน์ GridJs ให้คุณเปิด Modal ที่คุณสามารถโฮสต์ได้ทุกที่—อาจเป็นคอมโพเนนต์ React หรือฟอร์ม HTML ธรรมดา

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **ทำไมต้องใช้ Modal?** มันแยกตรรกะการตรวจสอบที่ซับซ้อนออกจากกริดและให้คุณควบคุมเลย์เอาต์ได้เต็มที่ ในขณะเดียวกันยังสามารถเรียกจากกริดได้

## ขั้นตอนที่ 8: ดึง JSON การตั้งค่าฝั่งไคลเอนต์

สุดท้ายคุณต้องส่งการตั้งค่าไปยังเบราว์เซอร์ วิธี `get_client_config` จะทำการซีเรียลไลซ์ทุกอย่างเป็น JSON blob ที่ไลบรารี GridJs ฝั่งฟรอนท์‑เอนด์สามารถใช้ได้

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

ผลลัพธ์ที่ได้จะคล้ายกับนี้ (ตัดให้สั้นเพื่อความกระชับ):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### ผลลัพธ์ที่คาดหวัง

- คลิกขวาที่เซลล์ใดก็เปิดเมนูที่มี **Mark as Reviewed**  
- การเลือกเมนูจะส่งคำขอไปยังเซิร์ฟเวอร์ ซึ่ง **updates the cell value** เป็น “Reviewed” และบันทึก `example‑updated.xlsx`  
- การตรวจสอบการสะกดจะไฮไลท์คำที่พิมพ์ผิดขณะผู้ใช้พิมพ์  

ทั้งหมดนี้ทำงานโดยไม่ต้องรีเฟรชหน้าเต็ม ๆ ด้วย Lazy Loading และ JSON payload ที่เบา

## คำถามที่พบบ่อย & เคล็ดลับระดับมืออาชีพ

| Question | Answer |
|----------|--------|
| *What if the workbook is read‑only?* | ตรวจสอบให้แน่ใจว่าไฟล์มีสิทธิ์เขียน, หรือเปิด workbook ด้วย `mode="rw"` หากไลบรารีรองรับ |
| *Can I add more than one custom menu item?* | แน่นอน—เพียงเพิ่ม dict เพิ่มเติมลงใน `grid.settings.context_menu.custom_items` |
| *Do I need to reload the grid after a cell update?* | GridJs จะรีเฟรชแถวที่ได้รับผลกระทบอัตโนมัติถ้าคุณคืนค่า `{status:"ok"}`; มิฉะนั้นเรียก `grid.refresh()` จากไคลเอนต์ |
| *How do I make spell checking language‑specific?* | ตั้งค่า `grid.settings.spell_check.language = "en-US"` (หรือ locale ที่รองรับอื่น) |
| *Is lazy loading compatible with server‑side filtering?* | ใช่—ผสาน `grid.settings.filter.enabled = True` แล้วทำการกรองในคำสั่งแบบกำหนดเองของคุณ |

## ตัวอย่างทำงานเต็มรูปแบบ (รวมทุกขั้นตอน)

ด้านล่างเป็นสคริปต์เดียวที่คุณสามารถวางลงใน route ของ Flask หรือรันเป็นโปรเซสสแตนด์อโลน แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงบนเซิร์ฟเวอร์ของคุณ

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## What Should You Learn Next?


บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}