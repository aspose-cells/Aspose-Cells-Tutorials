---
date: '2026-03-15'
description: เรียนรู้วิธีแยกชื่อเป็นคอลัมน์แยกต่างหากและบันทึกไฟล์ workbook xlsx ด้วย
  Aspose.Cells Java ในบทเรียนแบบขั้นตอนต่อขั้นตอน.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – แบ่งชื่อเป็นคอลัมน์
url: /th/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การเชี่ยวชาญ **aspose cells java**: แบ่งชื่อเป็นคอลัมน์

ยินดีต้อนรับสู่บทเรียน **aspose cells java** ฉบับครอบคลุมของเรา ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีการแบ่งชื่อ** ที่เก็บอยู่ในคอลัมน์ Excel เดียวให้เป็นสองคอลัมน์แยกกัน—ชื่อจริงและนามสกุล—โดยใช้คุณสมบัติ text‑to‑columns ที่ทรงพลัง ไม่ว่าคุณจะทำความสะอาดรายการติดต่อ, เตรียมข้อมูลสำหรับการนำเข้า CRM, หรือแค่ต้องการวิธีเร็ว ๆ ในการจัดโครงสร้างสเปรดชีตใหม่ คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนการ **บันทึก workbook xlsx** หลังการแปลงอย่างชัดเจน

## คำตอบอย่างรวดเร็ว
- **บทเรียนนี้ครอบคลุมอะไร?** การแบ่งสตริงชื่อเต็มเป็นคอลัมน์ชื่อและนามสกุลด้วย Aspose.Cells for Java.  
- **ใช้เวอร์ชันไลบรารีใด?** รุ่นเสถียรล่าสุด (ณ ปี 2026).  
- **ต้องมีลิขสิทธิ์หรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการพัฒนา; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **สามารถแบ่งด้วยตัวคั่นอื่นได้หรือไม่?** ได้—แค่เปลี่ยนตัวคั่นใน `TxtLoadOptions`.  
- **ผลลัพธ์เป็นไฟล์ .xlsx หรือไม่?** แน่นอน, workbook จะถูกบันทึกในรูปแบบ XLSX.

## **aspose cells java** คืออะไร?
**Aspose.Cells java** เป็น API Java ที่มีประสิทธิภาพสูง ช่วยให้นักพัฒนาสร้าง, แก้ไข, แปลง, และแสดงผลไฟล์ Excel ได้โดยไม่ต้องใช้ Microsoft Office รองรับรูปแบบ Excel หลักทั้งหมดและให้คุณสมบัติเพิ่มเติมเช่นสูตร, แผนภูมิ, และการจัดการข้อมูลขั้นสูง

## ทำไมต้องใช้ **aspose cells java** สำหรับการแบ่งชื่อ?
- **Zero‑install**: ทำงานได้บนสภาพแวดล้อม Java ฝั่งเซิร์ฟเวอร์ใดก็ได้.  
- **Speed**: จัดการสเปรดชีตขนาดใหญ่ได้เร็วกว่า Excel native interop.  
- **Precision**: ควบคุมตัวคั่น, ช่วงคอลัมน์, และรูปแบบผลลัพธ์ได้เต็มที่.  
- **Reliability**: ไม่ต้องพึ่งพา COM หรือ Office ทำให้เหมาะกับการปรับใช้บนคลาวด์หรือคอนเทนเนอร์.

## ข้อกำหนดเบื้องต้น
- Java Development Kit (JDK) 8 หรือใหม่กว่า.  
- IDE เช่น IntelliJ IDEA หรือ Eclipse (ไม่บังคับแต่แนะนำ).  
- Maven หรือ Gradle สำหรับการจัดการ dependencies.  

### การตั้งค่า Maven
เพิ่ม dependency ของ Aspose.Cells ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### การตั้งค่า Gradle
เพิ่มไลบรารีลงใน `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **เคล็ดลับ:** ใช้ลิขสิทธิ์ชั่วคราวจากพอร์ทัล Aspose เพื่อเปิดใช้งานฟังก์ชันเต็มระหว่างการพัฒนา.

## การดำเนินการตามขั้นตอน

### ขั้นตอนที่ 1: สร้าง Workbook และเข้าถึง Worksheet แรก
แรกเริ่มให้ import คลาสหลักและสร้าง workbook ใหม่ ซึ่งจะให้ไฟล์ Excel ที่สะอาดพร้อมสำหรับการใส่ข้อมูล

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### ขั้นตอนที่ 2: เติมข้อมูลตัวอย่างชื่อลงใน Worksheet
ต่อไปให้เพิ่มสตริงชื่อเต็มหลายรายการลงในคอลัมน์ **A** ในโครงการจริงคุณอาจอ่านข้อมูลเหล่านี้จากฐานข้อมูลหรือไฟล์ CSV

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### ขั้นตอนที่ 3: ตั้งค่า Text Load Options สำหรับการแบ่งคอลัมน์
คลาส `TxtLoadOptions` บอก Aspose.Cells ว่าจะตีความข้อความอย่างไร ที่นี่เราใช้ช่องว่าง (`' '`) เป็นตัวคั่น

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### ขั้นตอนที่ 4: แบ่งข้อความเป็นสองคอลัมน์
จากนั้นเรียก `textToColumns()` บนพื้นที่เซลล์ที่มีชื่อ ตัวพารามิเตอร์ `(0, 0, 5, opts)` หมายถึง *เริ่มที่แถว 0, คอลัมน์ 0, ประมวลผล 5 แถว, ใช้ตัวเลือกที่เรากำหนดไว้*

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

หลังจากเรียกนี้แล้ว คอลัมน์ A จะเก็บชื่อแรกและคอลัมน์ B จะเก็บนามสกุล

### ขั้นตอนที่ 5: บันทึก Workbook เป็นไฟล์ XLSX
สุดท้ายให้เขียน workbook ที่แก้ไขแล้วลงดิสก์ `SaveFormat` enum จะทำให้ไฟล์ถูกจัดเก็บในรูปแบบ XLSX สมัยใหม่

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **ทำไมเรื่องนี้สำคัญ:** ด้วยการใช้ **save workbook xlsx** คุณรับประกันความเข้ากันได้กับ Excel รุ่นล่าสุด, Google Sheets, และเครื่องมือสเปรดชีตอื่น ๆ

## การประยุกต์ใช้ในเชิงปฏิบัติ
- **ทำความสะอาดข้อมูล:** แยกฟิลด์ที่ต่อเนื่องกันอย่างรวดเร็วก่อนโหลดเข้าสู่ pipeline การวิเคราะห์.  
- **การรวมกับ CRM:** แปลงรายการติดต่อแบบแบนให้เป็นตารางโครงสร้างสำหรับการนำเข้า.  
- **ระบบ HR:** แบ่งชื่อเต็มของพนักงานเพื่อการคำนวณเงินเดือนหรือการประมวลผลสวัสดิการ.

## พิจารณาด้านประสิทธิภาพ
เมื่อทำงานกับข้อมูลหลายพันแถว:

1. **อัปเดตเป็นชุด:** ใช้ `ws.getCells().setRowHeight()` หรือวิธี batch อื่นเพื่อลดภาระ.  
2. **การจัดการหน่วยความจำ:** เรียก `wb.calculateFormula()` เฉพาะเมื่อจำเป็นและทำลายอ็อบเจ็กต์ขนาดใหญ่โดยเร็ว.  
3. **Garbage Collection:** รัน JVM ด้วยการตั้งค่า heap ที่เหมาะสม (`-Xmx2g` สำหรับไฟล์ใหญ่) เพื่อหลีกเลี่ยงข้อผิดพลาด OutOfMemory.

## ปัญหาที่พบบ่อยและวิธีแก้
| ปัญหา | วิธีแก้ |
|-------|----------|
| **ชื่อมีอักษรย่อกลาง** (เช่น “John A. Doe”) | ปรับตัวคั่นหรือทำ post‑process คอลัมน์ที่สองเพื่อดึงนามสกุลออก. |
| **เซลล์ว่างที่ไม่คาดคิด** | ตรวจสอบว่าช่วงต้นทาง (`textToColumns` parameters) ตรงกับจำนวนแถวข้อมูลจริง. |
| **ไม่พบลิขสิทธิ์** | วางไฟล์ลิขสิทธิ์ชั่วคราว (`Aspose.Cells.lic`) ที่โฟลเดอร์รากของโครงการหรือกำหนดลิขสิทธิ์ผ่านโค้ด. |

## คำถามที่พบบ่อย

**ถาม: Aspose.Cells Java คืออะไร?**  
ตอบ: ไลบรารีที่ทรงพลังช่วยให้คุณสร้าง, แก้ไข, และแปลงไฟล์ Excel ด้วย Java อย่างโปรแกรมเมติก

**ถาม: สามารถแบ่งคอลัมน์โดยใช้ตัวคั่นอื่นนอกจากช่องว่างได้หรือไม่?**  
ตอบ: ได้, ปรับตัวคั่นใน `TxtLoadOptions` ตามความต้องการของข้อมูลของคุณ

**ถาม: จะจัดการชุดข้อมูลขนาดใหญ่กับ Aspose.Cells อย่างไร?**  
ตอบ: ปรับประสิทธิภาพโดยจัดการหน่วยความจำและลดการดำเนินการบน workbook ตามที่อธิบายข้างต้น

**ถาม: มีการสนับสนุนเมื่อเจอปัญหาหรือไม่?**  
ตอบ: เยี่ยมชม [Aspose Forum](https://forum.aspose.com/c/cells/9) เพื่อรับความช่วยเหลือจากชุมชนหรือ ติดต่อทีมสนับสนุนของ Aspose โดยตรง

**ถาม: Aspose.Cells สามารถบันทึก workbook ในรูปแบบใดบ้าง?**  
ตอบ: รองรับรูปแบบไฟล์ Excel หลากหลายรวมถึง XLSX, XLS, CSV, และอื่น ๆ

## แหล่งข้อมูล

- **เอกสาร**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **ดาวน์โหลด**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **ซื้อ**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **ทดลองใช้ฟรี**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **ลิขสิทธิ์ชั่วคราว**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

ขอให้สนุกกับการเขียนโค้ดและใช้พลังเต็มที่ของ **aspose cells java** ในโปรเจกต์ของคุณ!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**อัปเดตล่าสุด:** 2026-03-15  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose