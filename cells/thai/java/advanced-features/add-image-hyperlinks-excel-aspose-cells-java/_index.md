---
date: '2026-09-02'
description: เรียนรู้วิธีสร้างสมุดงาน Excel ที่มีภาพคลิกได้ด้วย Aspose.Cells for Java
  โดยเพิ่ม hyperlinks ไปยังรูปภาพเพื่อสร้างสเปรดชีตแบบโต้ตอบ
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: เรียนรู้วิธีสร้างสมุดงาน Excel ที่มีภาพคลิกได้ด้วย Aspose.Cells for
  Java โดยเพิ่ม hyperlinks, screen tips และการปรับประสิทธิภาพในไม่กี่บรรทัดของ code
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: สร้างภาพที่คลิกได้ใน Excel ด้วย Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: สร้างภาพที่คลิกได้ใน Excel ด้วย Aspose.Cells for Java
url: /th/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างภาพคลิกได้ใน Excel ด้วย Aspose.Cells for Java

## บทนำ

หากคุณต้องการ **สร้างภาพคลิกได้ใน Excel** workbook ที่ทำให้ผู้ใช้กระโดดไปยังเว็บไซต์ เอกสาร หรือแหล่งข้อมูลอื่น ๆ ด้วยการคลิกเดียว คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะอธิบายว่า Aspose.Cells for Java ทำให้คุณสามารถ **เพิ่มวัตถุรูปภาพ Excel ที่มีไฮเปอร์ลิงก์** กำหนด screen tip และทำให้สเปรดชีตของคุณสวยงามและใช้งานได้

### สิ่งที่คุณจะได้เรียนรู้
- การเริ่มต้น Aspose.Cells workbook ใน Java.  
- แทรกภาพและเปลี่ยนเป็นไฮเปอร์ลิงก์ที่คลิกได้.  
- เมธอดสำคัญเช่น `addHyperlink`, `setPlacement`, และ `setScreenTip`.  
- แนวปฏิบัติที่ดีที่สุดสำหรับประสิทธิภาพและการออกใบอนุญาต.

## คำตอบอย่างรวดเร็ว
- **ไลบรารีที่ต้องการคืออะไร?** Aspose.Cells for Java.  
- **ฉันสามารถใช้ไฟล์ .xlsx ได้หรือไม่?** ใช่ – API ทำงานกับทั้ง .xls และ .xlsx.  
- **ต้องการใบอนุญาตหรือไม่?** เวอร์ชันทดลองใช้สำหรับการประเมิน; ต้องมีใบอนุญาตถาวรสำหรับการใช้งานจริง.  
- **จำนวนบรรทัดของโค้ด?** ประมาณ 20 บรรทัดเพื่อเพิ่มภาพที่คลิกได้.  
- **ปลอดภัยต่อหลายเธรดหรือไม่?** วัตถุ Workbook ไม่ปลอดภัยต่อหลายเธรด; สร้างอินสแตนซ์แยกสำหรับแต่ละเธรด.  
- **ฉันสามารถเพิ่ม screen tip ใน Excel ได้หรือไม่?** ใช่ – ใช้ `Hyperlink.setScreenTip()` เพื่อแสดงข้อความช่วยเหลือเมื่อชี้เมาส์.

## วิธีสร้างภาพคลิกได้ใน Excel ด้วย Aspose.Cells for Java

คุณสร้าง workbook Excel ที่มีภาพคลิกได้โดยการโหลดหรือสร้าง `Workbook` แทรกวัตถุ `Picture` แนบ `Hyperlink` ไปยังรูปภาพนั้น ตั้งค่า screen tip หากต้องการ และสุดท้ายบันทึกไฟล์ API จะจัดการกับ XML ของ Excel ระดับต่ำทั้งหมด ดังนั้นคุณเพียงเขียนไม่กี่บรรทัดโค้ด Java ที่ง่าย

### ข้อกำหนดเบื้องต้น
- **Aspose.Cells for Java** (v25.3 หรือใหม่กว่า).  
- **JDK 8+** ติดตั้งแล้ว.  
- IDE (IntelliJ IDEA, Eclipse หรือ NetBeans) พร้อม Maven หรือ Gradle สำหรับการจัดการ dependencies.  

### ไลบรารีที่จำเป็น
Add Aspose.Cells to your project:

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### การรับใบอนุญาต
- เวอร์ชันทดลอง: ดาวน์โหลดจาก [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- ใบอนุญาตชั่วคราว: ขอผ่าน [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- ซื้อ: สำหรับการใช้งานระยะยาว เยี่ยมชม [Aspose Purchase](https://purchase.aspose.com/buy).  

### การเริ่มต้นพื้นฐาน
`Workbook` คลาสแสดงไฟล์ Excel ทั้งหมดในหน่วยความจำ คุณสร้างอินสแตนซ์แล้วรับอ้างอิงไปยัง worksheet แรก `Worksheet` แสดงแผ่นงานเดียวภายใน workbook.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## การดำเนินการแบบขั้นตอน

### ขั้นตอนที่ 1: เตรียม workbook ของคุณ
เราเริ่มด้วยการสร้าง workbook ใหม่และเลือกแผ่นแรก.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### ขั้นตอนที่ 2: แทรกป้ายและปรับขนาดเซลล์
เพิ่มป้ายอธิบายและให้เซลล์มีพื้นที่เพียงพอสำหรับรูปภาพ.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### ขั้นตอนที่ 3: เพิ่มรูปภาพ
`Picture` แสดงวัตถุภาพที่วางบน worksheet.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*เคล็ดลับ*: แทนที่ `"path/to/aspose-logo.jpg"` ด้วยเส้นทางจริงของไฟล์รูปภาพของคุณ.

### ขั้นตอนที่ 4: กำหนดตำแหน่งและเพิ่มไฮเปอร์ลิงก์
`Hyperlink` กำหนดลิงก์ที่เชื่อมกับเซลล์ รูปร่าง หรือรูปภาพ ทำให้สามารถนำทางเมื่อคลิก.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### ขั้นตอนที่ 5: ตั้งค่า screen tip และบันทึก workbook
ให้ tooltip ที่เป็นประโยชน์และเขียน workbook ลงดิสก์.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## ทำไมต้องเพิ่มไฮเปอร์ลิงก์ให้รูปภาพใน Excel?
การฝังรูปภาพที่คลิกได้ทำให้คุณเปลี่ยนองค์ประกอบแบรนด์ ไอคอน หรือแผนภาพให้เป็นจุดนำทางโดยตรง ลดจำนวนคลิกที่ต้องใช้เพื่อเข้าถึงเนื้อหาที่เกี่ยวข้อง วิธีนี้เพิ่มประสิทธิภาพของผู้ใช้ในแดชบอร์ดการตลาด คู่มือเทคนิค และแผ่นงานการศึกษา.

## วิธีเพิ่ม screen tip ใน Excel
คุณเพิ่ม screen tip โดยเรียก `hyperlink.setScreenTip("Your tip here")` บนวัตถุ `Hyperlink` ที่แนบกับรูปภาพ tip จะปรากฏเมื่อเคอร์เซอร์ชี้เหนือรูปภาพ ให้คำแนะนำตามบริบทแก่ผู้ใช้โดยไม่ทำให้แผ่นงานรก.

## เคล็ดลับการแก้ไขปัญหา
- **ข้อผิดพลาดของเส้นทางรูปภาพ** – ตรวจสอบตำแหน่งไฟล์อีกครั้งและให้แน่ใจว่าแอปพลิเคชันมีสิทธิ์อ่าน.  
- **ใบอนุญาตไม่ได้ใช้** – หากเวอร์ชันทดลองหมดอายุ ไฮเปอร์ลิงก์อาจหยุดทำงาน; ใช้ใบอนุญาตที่ถูกต้องด้วย `License.setLicense`.  
- **ไฮเปอร์ลิงก์ไม่คลิกได้** – ตรวจสอบว่า `PlacementType` ของรูปภาพตั้งเป็น `FREE_FLOATING`.

## การประยุกต์ใช้งานจริง
การฝังรูปภาพที่คลิกได้มีประโยชน์ในหลายสถานการณ์:
1. **รายงานการตลาด** – ลิงก์โลโก้แบรนด์ไปยังหน้าผลิตภัณฑ์.  
2. **เอกสารเทคนิค** – แนบแผนภาพที่เปิดสเคมาติคละเอียด.  
3. **แผ่นงานการศึกษา** – แปลงไอคอนเป็นทางลัดสำหรับวิดีโอเสริม.  
4. **แดชบอร์ดโครงการ** – ทำให้ไอคอนสถานะเปิดตัวติดตามงานที่เกี่ยวข้อง.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- รักษาขนาดไฟล์รูปภาพให้เหมาะสม; รูปภาพขนาดใหญ่เพิ่มการใช้หน่วยความจำของ workbook.  
- ทำลายวัตถุที่ไม่ได้ใช้ (`workbook.dispose()`) เมื่อประมวลผลไฟล์หลายไฟล์ในลูป.  
- อัปเกรดเป็นเวอร์ชันล่าสุดของ Aspose.Cells เพื่อปรับปรุงประสิทธิภาพและแก้บั๊ก.

## สรุป
ตอนนี้คุณรู้วิธีเพิ่มไฮเปอร์ลิงก์ให้กับรูปภาพใน Excel ด้วย Aspose.Cells for Java ทำให้คุณสามารถ **สร้างภาพคลิกได้ใน Excel** workbook ที่มีความสมบูรณ์และโต้ตอบมากขึ้น ทดลองใช้ URL ต่าง ๆ, screen tip, และตำแหน่งรูปภาพเพื่อให้ตรงกับความต้องการรายงานของคุณ ขั้นต่อไปคุณอาจสำรวจการเพิ่มไฮเปอร์ลิงก์ให้กับรูปร่างหรืออัตโนมัติการแทรกรูปภาพจำนวนมากในหลาย worksheet.

## คำถามที่พบบ่อย

**Q:** ขนาดภาพสูงสุดที่รองรับโดย Aspose.Cells for Java คือเท่าไหร่?  
**A:** ไม่มีขีดจำกัดที่เข้มงวด แต่ภาพขนาดใหญ่มากอาจส่งผลต่อประสิทธิภาพและเพิ่มขนาดไฟล์.

**Q:** ฉันสามารถใช้คุณลักษณะนี้กับไฟล์ .xlsx ได้หรือไม่?  
**A:** ใช่, API ทำงานกับทั้งรูปแบบ `.xls` และ `.xlsx`.

**Q:** ฉันควรจัดการกับข้อยกเว้นอย่างไรเมื่อเพิ่มไฮเปอร์ลิงก์?  
**A:** ห่อโค้ดด้วยบล็อก try‑catch และบันทึกรายละเอียดของ `Exception` เพื่อวินิจฉัยปัญหาเส้นทางหรือใบอนุญาต.

**Q:** สามารถลบไฮเปอร์ลิงก์จากรูปภาพหลังจากที่เพิ่มแล้วได้หรือไม่?  
**A:** ได้ – ดึงวัตถุ `Picture` แล้วเรียก `pic.getHyperlink().remove()` หรือทำการลบรูปภาพจากคอลเลกชัน.

**Q:** ทำไมไฮเปอร์ลิงก์ของฉันอาจไม่ทำงานตามที่คาดหวัง?  
**A:** สาเหตุทั่วไปรวมถึงสตริง URL ไม่ถูกต้อง, ขาดคำนำหน้า `http://`/`https://`, หรือเวอร์ชันทดลองที่ไม่มีใบอนุญาตซึ่งปิดการทำงานของฟีเจอร์บางอย่าง.

## แหล่งข้อมูลเพิ่มเติม
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Purchase and trial:** Visit [Aspose Purchase](https://purchase.aspose.com/buy) or [Temporary License Page](https://purchase.aspose.com/temporary-license/) for licensing options.  
- **Support forum:** For assistance, check out the [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**อัปเดตล่าสุด:** 2026-09-02  
**ทดสอบด้วย:** Aspose.Cells for Java 25.3  
**ผู้เขียน:** Aspose

## บทเรียนที่เกี่ยวข้อง

- [วิธีสร้างไฮเปอร์ลิงก์ใน Excel ด้วย Aspose.Cells for Java - คู่มือขั้นตอน](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [วิธีจัดรูปแบบเซลล์ Excel และเพิ่มไฮเปอร์ลิงก์ด้วย Aspose.Cells for Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [เพิ่มรูปภาพในคอมเมนต์ Excel ด้วย Aspose.Cells for Java: คู่มือฉบับสมบูรณ์](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}