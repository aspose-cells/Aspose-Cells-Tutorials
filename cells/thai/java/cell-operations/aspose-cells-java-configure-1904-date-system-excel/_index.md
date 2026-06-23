---
date: '2026-02-22'
description: เรียนรู้วิธีเปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells for
  Java ตั้งค่ารูปแบบวันที่ของ Excel และแปลงระบบ 1904 ของ Excel อย่างมีประสิทธิภาพ
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells Java
url: /th/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

 "Managing historical data in Excel can be challenging because Excel supports two different date systems. **In this tutorial you'll learn how to change Excel date system to the 1904 format using Aspose.Cells for Java**, which makes handling legacy dates painless. We'll walk through initializing a workbook, enabling the 1904 date system, and persisting the change."

Translate.

Then "## Quick Answers" etc.

Translate bullet points.

Need to keep bold formatting.

Also code snippet placeholders remain.

Proceed.

Also note "## Set Excel date programmatically (secondary keyword)" etc.

Translate.

Make sure to keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนระบบวันที่ของ Excel เป็น 1904 ด้วย Aspose.Cells Java

การจัดการข้อมูลประวัติใน Excel อาจเป็นเรื่องท้าทายเนื่องจาก Excel รองรับสองระบบวันที่ที่แตกต่างกัน **ในบทเรียนนี้คุณจะได้เรียนรู้วิธีเปลี่ยนระบบวันที่ของ Excel ให้เป็นรูปแบบ 1904 ด้วย Aspose.Cells for Java** ซึ่งทำให้การจัดการวันที่เก่าเป็นเรื่องง่าย เราจะอธิบายขั้นตอนการสร้าง workbook, เปิดใช้งานระบบวันที่ 1904, และบันทึกการเปลี่ยนแปลง

## คำตอบอย่างรวดเร็ว
- **ระบบวันที่ 1904 ทำอะไร?** ระบบนี้เริ่มนับวันตั้งแต่ 1 มกราคม 1904 โดยเลื่อนวันที่ทั้งหมดไป 1462 วันเมื่อเทียบกับระบบเริ่มต้นปี 1900.  
- **ทำไมต้องใช้ Aspose.Cells เพื่อเปลี่ยนระบบวันที่?** มันมี API ที่ง่ายต่อการใช้งานโดยไม่ต้องติดตั้ง Excel และรองรับไฟล์ขนาดใหญ่.  
- **รองรับเวอร์ชัน Java ใดบ้าง?** JDK 8 หรือใหม่กว่า.  
- **ต้องมีลิขสิทธิ์หรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการประเมิน; ลิขสิทธิ์จะลบข้อจำกัดการใช้งาน.  
- **สามารถเปลี่ยนกลับเป็นระบบ 1900 ได้ภายหลังหรือไม่?** ได้, เพียงเรียก `setDate1904(false)`.

## ระบบวันที่ 1904 ใน Excel คืออะไร?
ระบบวันที่ 1904 ถูกใช้โดยเวอร์ชันแรกของ Excel บน Macintosh. ระบบนี้นับวันตั้งแต่ 1 มกราคม 1904 ซึ่งเป็นประโยชน์สำหรับความเข้ากันได้กับสเปรดชีตเก่าและโมเดลการเงินบางประเภท.

## ทำไมต้องเปลี่ยนระบบวันที่ของ Excel ด้วย Aspose.Cells?
- **ความเข้ากันได้ข้ามแพลตฟอร์ม** – ทำงานบน Windows, Linux, และ macOS.  
- **ไม่ต้องติดตั้ง Excel** – เหมาะสำหรับการประมวลผลบนเซิร์ฟเวอร์.  
- **ประสิทธิภาพสูง** – จัดการ workbook ขนาดใหญ่ด้วยการใช้หน่วยความจำน้อย.

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือสูงกว่า.  
- Maven หรือ Gradle สำหรับการจัดการ dependency.  
- ความรู้พื้นฐานการเขียนโปรแกรม Java.

## การตั้งค่า Aspose.Cells สำหรับ Java

### Maven
เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
ใส่บรรทัดนี้ในไฟล์ `build.gradle` ของคุณ:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### การรับลิขสิทธิ์
Aspose มีรุ่นทดลองฟรี, ลิขสิทธิ์ชั่วคราว, และลิขสิทธิ์เชิงพาณิชย์เต็มรูปแบบ คุณสามารถเริ่มต้นด้วย [free trial](https://releases.aspose.com/cells/java/) หรือรับลิขสิทธิ์ชั่วคราวจาก [temporary license page](https://purchase.aspose.com/temporary-license/).

## เปลี่ยนระบบวันที่ของ Excel ด้วย Aspose.Cells Java

ด้านล่างเป็นคำแนะนำแบบขั้นตอนที่ **เปลี่ยนระบบวันที่ของ Excel** จริง ๆ แต่ละขั้นตอนมีคำอธิบายสั้น ๆ ตามด้วยโค้ดที่ต้องใช้

### ขั้นตอน 1: เริ่มต้นและโหลด workbook
แรกเริ่มสร้างอินสแตนซ์ `Workbook` ที่ชี้ไปยังไฟล์ Excel ที่มีอยู่ของคุณ

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### ขั้นตอน 2: เปิดใช้งานระบบวันที่ 1904
ใช้การตั้งค่า workbook เพื่อสลับระบบวันที่

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**เคล็ดลับ:** คุณสามารถเรียก `setDate1904(false)` ภายหลังได้หากต้องการย้อนกลับ

### ขั้นตอน 3: บันทึก workbook ที่แก้ไขแล้ว
สุดท้ายให้เขียนการเปลี่ยนแปลงลงไฟล์ใหม่ (หรือเขียนทับไฟล์เดิม)

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **หมายเหตุ:** โค้ดข้างต้นใช้ชื่อคลาส `tWorkbook` ตามที่ให้มาเดิม ตรวจสอบให้แน่ใจว่าชื่อพิมพ์ผิดนี้ตรงกับแนวปฏิบัติของโปรเจกต์คุณหรือแก้เป็น `Workbook` หากจำเป็น

## ตั้งค่าวันที่ Excel ผ่านโปรแกรม (secondary keyword)
หากต้องการปรับค่าที่เซลล์แต่ละเซลล์หลังจากเปลี่ยนระบบ, สามารถใช้ `Cells.get(i, j).putValue(Date)` ซึ่งวันที่จะถูกตีความตามระบบวันที่ที่ใช้งานอยู่

## แปลงระบบวันที่ Excel 1904 กลับเป็น 1900 (secondary keyword)
เพื่อย้อนกลับ, เพียงเรียก:

```java
workbook.getSettings().setDate1904(false);
```

แล้วบันทึก workbook อีกครั้ง

## การใช้งานจริง
1. **การเก็บข้อมูลเก่า** – รักษา timestamp เก่าเมื่อย้ายสเปรดชีตจาก Mac รุ่นเก่า.  
2. **การรายงานข้ามแพลตฟอร์ม** – สร้างรายงานที่เปิดได้ทั้งบน Windows และ macOS โดยไม่มีความไม่ตรงกันของวันที่.  
3. **การสร้างโมเดลการเงิน** – ปรับการคำนวณวันที่ให้สอดคล้องกับโมเดลการเงินเก่าที่คาดหวังระบบ 1904.

## พิจารณาด้านประสิทธิภาพ
- จำกัดการดำเนินการกับ workbook ในเซสชันเดียวเพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- ใช้การปรับแต่ง garbage‑collection ของ Java สำหรับไฟล์ขนาดใหญ่มาก.

## คำถามที่พบบ่อย

**ถาม: ความแตกต่างระหว่างระบบวันที่ 1900 และ 1904 คืออะไร?**  
ตอบ: ระบบ 1900 เริ่มที่ 1 มกราคม 1900, ส่วนระบบ 1904 เริ่มที่ 1 มกราคม 1904, ทำให้วันที่ทั้งหมดเลื่อนออกไป 1462 วัน

**ถาม: สามารถเปลี่ยนระบบวันที่ของ workbook ที่เปิดอยู่ใน Excel ได้หรือไม่?**  
ตอบ: ได้, แต่ต้องปิดไฟล์ใน Excel ก่อน; มิฉะนั้นการบันทึกจะล้มเหลว

**ถาม: ต้องมีลิขสิทธิ์เพื่อใช้ `setDate1904` หรือไม่?**  
ตอบ: วิธีนี้ทำงานในรุ่นทดลองฟรี, แต่ลิขสิทธิ์เต็มจะลบข้อจำกัดการประเมิน

**ถาม: สามารถเปลี่ยนระบบวันที่ได้เฉพาะ worksheet เดียวหรือไม่?**  
ตอบ: ไม่ได้, ระบบวันที่เป็นการตั้งค่าระดับ workbook; มีผลกับทุก worksheet

**ถาม: จะตรวจสอบว่าระบบวันที่ถูกเปลี่ยนหรือไม่อย่างไร?**  
ตอบ: เปิดไฟล์ที่บันทึกใน Excel, ไปที่ **File → Options → Advanced**, แล้วตรวจสอบช่อง **"Use 1904 date system"**

## สรุป
คุณได้เรียนรู้วิธี **เปลี่ยนระบบวันที่ของ Excel** เป็น 1904 ด้วย Aspose.Cells for Java, วิธีตั้งค่าฟอร์แมตวันที่ใน Excel, และวิธีแปลงกลับหากต้องการ นำโค้ดเหล่านี้ไปใช้ใน pipeline การประมวลผลข้อมูลของคุณเพื่อรับประกันความเข้ากันได้ของวันที่ข้ามแพลตฟอร์ม

---

**อัปเดตล่าสุด:** 2026-02-22  
**ทดสอบกับ:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

**แหล่งข้อมูล**
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Purchase License:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free Trial:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporary License:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Support Forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}