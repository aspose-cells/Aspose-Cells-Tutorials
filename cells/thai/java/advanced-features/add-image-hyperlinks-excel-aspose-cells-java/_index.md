---
date: '2026-02-16'
description: เรียนรู้วิธีสร้างไฟล์ Excel ที่มีรูปภาพคลิกได้ด้วย Aspose.Cells for Java
  โดยเพิ่มไฮเปอร์ลิงก์ให้กับรูปภาพสำหรับสเปรดชีตแบบโต้ตอบ.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: สร้างไฟล์ Excel ที่มีภาพคลิกได้โดยใช้ Aspose.Cells สำหรับ Java
url: /th/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Excel ที่มีรูปภาพคลิกได้โดยใช้ Aspose.Cells สำหรับ Java

## บทนำ

หากคุณต้องการ **สร้าง Excel ที่มีรูปภาพคลิกได้** ที่ทำให้ผู้ใช้กระโดดไปยังเว็บไซต์ เอกสาร หรือทรัพยากรอื่น ๆ เพียงคลิกเดียว คุณมาถูกที่แล้ว ในบทเรียนนี้เราจะอธิบายว่า Aspose.Cells สำหรับ Java ช่วยให้คุณ **เพิ่มวัตถุรูปภาพ Excel ที่เป็นไฮเปอร์ลิงก์** กำหนด screen tip และทำให้สเปรดชีตของคุณสวยงามและใช้งานได้อย่างเต็มที่

### สิ่งที่คุณจะได้เรียนรู้
- การเริ่มต้น workbook ของ Aspose.Cells ใน Java  
- การแทรกรูปภาพและเปลี่ยนให้เป็นไฮเปอร์ลิงก์ที่คลิกได้  
- เมธอดสำคัญเช่น `addHyperlink`, `setPlacement` และ `setScreenTip`  
- แนวทางปฏิบัติที่ดีที่สุดสำหรับประสิทธิภาพและการจัดการลิขสิทธิ์  

## คำตอบสั้น
- **ไลบรารีที่ต้องการคืออะไร?** Aspose.Cells for Java.  
- **ฉันสามารถใช้ไฟล์ .xlsx ได้หรือไม่?** ใช่ – API ทำงานกับทั้ง .xls และ .xlsx.  
- **ฉันต้องมีลิขสิทธิ์หรือไม่?** เวอร์ชันทดลองใช้สำหรับการประเมิน; ต้องมีลิขสิทธิ์ถาวรสำหรับการใช้งานจริง.  
- **ต้องใช้บรรทัดโค้ดกี่บรรทัด?** ประมาณ 20 บรรทัดเพื่อเพิ่มรูปภาพที่คลิกได้.  
- **ปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** วัตถุ Workbook ไม่ปลอดภัยต่อการทำงานหลายเธรด; ควรสร้างอินสแตนซ์แยกสำหรับแต่ละเธรด.  
- **ฉันสามารถเพิ่ม screen tip ใน Excel ได้หรือไม่?** ใช่ – ใช้ `Hyperlink.setScreenTip()` เพื่อแสดงข้อความช่วยเหลือเมื่อชี้เมาส์.  

## วิธีสร้าง Excel ที่มีรูปภาพคลิกได้ด้วย Aspose.Cells สำหรับ Java

### ข้อกำหนดเบื้องต้น
ก่อนเริ่มทำงาน ตรวจสอบให้แน่ใจว่าคุณมี:

- **Aspose.Cells for Java** (เวอร์ชัน 25.3 หรือใหม่กว่า).  
- **JDK 8+** ติดตั้งแล้ว.  
- IDE (IntelliJ IDEA, Eclipse หรือ NetBeans) พร้อม Maven หรือ Gradle สำหรับจัดการ dependencies.  

### ไลบรารีที่ต้องการ
เพิ่ม Aspose.Cells ลงในโปรเจกต์ของคุณ:

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

### การรับลิขสิทธิ์
Aspose.Cells เป็นผลิตภัณฑ์เชิงพาณิชย์ แต่คุณสามารถเริ่มต้นด้วยเวอร์ชันทดลองฟรีหรือขอรับลิขสิทธิ์ชั่วคราว:

- เวอร์ชันทดลอง: ดาวน์โหลดจาก [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- ลิขสิทธิ์ชั่วคราว: ขอผ่าน [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- ซื้อ: สำหรับการใช้งานระยะยาว เยี่ยมชม [Aspose Purchase](https://purchase.aspose.com/buy).  

### การเริ่มต้นพื้นฐาน
สร้าง workbook และดึง worksheet แรก:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## การดำเนินการแบบขั้นตอน

### ขั้นตอนที่ 1: เตรียม Workbook ของคุณ
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
โหลดไฟล์รูปภาพและวางลงบนแผ่นงาน.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*เคล็ดลับ*: แทนที่ `"path/to/aspose-logo.jpg"` ด้วยพาธจริงของไฟล์รูปภาพของคุณ.

### ขั้นตอนที่ 4: กำหนดตำแหน่งและเพิ่มไฮเปอร์ลิงก์
ทำให้รูปภาพเป็นแบบ floating และแนบไฮเปอร์ลิงก์เข้ากับมัน.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### ขั้นตอนที่ 5: ตั้งค่า Screen Tip และบันทึก Workbook
ให้ tooltip ที่เป็นประโยชน์และบันทึก workbook ลงดิสก์.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## ทำไมต้องเพิ่มไฮเปอร์ลิงก์ให้รูปภาพใน Excel?
การฝังรูปภาพที่คลิกได้ทำให้คุณเปลี่ยนองค์ประกอบแบรนด์ ไอคอน หรือแผนภาพให้เป็นจุดนำทางโดยตรง ซึ่งช่วยปรับปรุงประสบการณ์ผู้ใช้ในแดชบอร์ดการตลาด คู่มือเทคนิค และแบบฝึกหัดการศึกษาโดยลดจำนวนคลิกที่ต้องใช้เพื่อเข้าถึงเนื้อหาที่เกี่ยวข้อง.

## วิธีเพิ่ม screen tip ใน Excel
เมธอด `setScreenTip` ให้คุณกำหนดข้อความที่แสดงเมื่อผู้ใช้วางเคอร์เซอร์เหนือรูปภาพ ซึ่งเหมาะสำหรับให้ข้อมูลเพิ่มเติม เช่น “ดูรายละเอียดสินค้า” หรือ “เปิดวิดีโอสอน”.

## เคล็ดลับการแก้ไขปัญหา
- **ข้อผิดพลาดของพาธรูปภาพ** – ตรวจสอบตำแหน่งไฟล์อีกครั้งและให้แน่ใจว่าแอปพลิเคชันมีสิทธิ์อ่าน.  
- **ลิขสิทธิ์ไม่ได้ถูกนำมาใช้** – หากเวอร์ชันทดลองหมดอายุ ไฮเปอร์ลิงก์อาจหยุดทำงาน; ให้ตั้งลิขสิทธิ์ที่ถูกต้องด้วย `License.setLicense`.  
- **ไฮเปอร์ลิงก์ไม่คลิกได้** – ตรวจสอบว่า `PlacementType` ของรูปภาพตั้งเป็น `FREE_FLOATING`.  

## การประยุกต์ใช้ในเชิงปฏิบัติ
การฝังรูปภาพที่คลิกได้มีประโยชน์ในหลายสถานการณ์:

1. **รายงานการตลาด** – ลิงก์โลโก้แบรนด์ไปยังหน้าผลิตภัณฑ์.  
2. **เอกสารเทคนิค** – แนบแผนภาพที่เปิดสเก็มาติกละเอียด.  
3. **แบบฝึกหัดการศึกษา** – แปลงไอคอนเป็นทางลัดสำหรับวิดีโอเสริม.  
4. **แดชบอร์ดโครงการ** – ทำให้ไอคอนสถานะเปิดตัวติดตามงานที่เกี่ยวข้อง.  

## ข้อควรพิจารณาด้านประสิทธิภาพ
- รักษาขนาดไฟล์รูปภาพให้เหมาะสม; รูปขนาดใหญ่จะเพิ่มการใช้หน่วยความจำของ workbook.  
- ทำลายวัตถุที่ไม่ได้ใช้ (`workbook.dispose()`) เมื่อประมวลผลไฟล์หลายไฟล์ในลูป.  
- อัปเกรดเป็นเวอร์ชันล่าสุดของ Aspose.Cells เพื่อปรับปรุงประสิทธิภาพและแก้ไขบั๊ก.  

## สรุป
ตอนนี้คุณรู้แล้วว่า **วิธีเพิ่มไฮเปอร์ลิงก์** ให้กับรูปภาพใน Excel ด้วย Aspose.Cells สำหรับ Java ซึ่งทำให้คุณสามารถ **สร้าง Excel ที่มีรูปภาพคลิกได้** ที่มีความสมบูรณ์และโต้ตอบมากขึ้น ลองทดลองใช้ URL, screen tip, และตำแหน่งรูปภาพต่าง ๆ เพื่อให้ตรงกับความต้องการของรายงานของคุณ ต่อไปคุณอาจสำรวจการเพิ่มไฮเปอร์ลิงก์ให้กับรูปทรงหรือการทำอัตโนมัติการแทรกรูปภาพจำนวนมากในหลาย ๆ worksheet.  

## คำถามที่พบบ่อย

**Q:** ขนาดรูปภาพสูงสุดที่ Aspose.Cells สำหรับ Java รองรับคือเท่าไหร่?  
**A:** ไม่มีขีดจำกัดที่เข้มงวด แต่รูปภาพขนาดใหญ่มากอาจส่งผลต่อประสิทธิภาพและเพิ่มขนาดไฟล์.

**Q:** ฉันสามารถใช้ฟีเจอร์นี้กับไฟล์ .xlsx ได้หรือไม่?  
**A:** ใช่, API ทำงานกับทั้งรูปแบบ `.xls` และ `.xlsx`.

**Q:** ฉันควรจัดการกับข้อยกเว้นอย่างไรเมื่อเพิ่มไฮเปอร์ลิงก์?  
**A:** ห่อโค้ดด้วยบล็อก try‑catch และบันทึกรายละเอียด `Exception` เพื่อวินิจฉัยปัญหาพาธหรือลิขสิทธิ์.

**Q:** สามารถลบไฮเปอร์ลิงก์จากรูปภาพหลังจากที่เพิ่มแล้วได้หรือไม่?  
**A:** ได้ – ดึงวัตถุ `Picture` แล้วเรียก `pic.getHyperlink().remove()` หรือทำการลบรูปภาพจากคอลเลกชัน.

**Q:** ทำไมไฮเปอร์ลิงก์ของฉันอาจไม่ทำงานตามที่คาดหวัง?  
**A:** สาเหตุทั่วไปรวมถึงสตริง URL ไม่ถูกต้อง, ขาดคำนำหน้า `http://`/`https://`, หรือเวอร์ชันทดลองที่ไม่มีลิขสิทธิ์ซึ่งปิดการทำงานของฟีเจอร์บางอย่าง.

## แหล่งข้อมูลเพิ่มเติม
- **เอกสาร:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **ดาวน์โหลด:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **การซื้อและทดลอง:** เยี่ยมชม [Aspose Purchase](https://purchase.aspose.com/buy) หรือ [Temporary License Page](https://purchase.aspose.com/temporary-license/) สำหรับตัวเลือกลิขสิทธิ์.  
- **ฟอรั่มสนับสนุน:** หากต้องการความช่วยเหลือ ดูที่ [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**อัปเดตล่าสุด:** 2026-02-16  
**ทดสอบกับ:** Aspose.Cells for Java 25.3  
**ผู้เขียน:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}