---
date: '2026-02-22'
description: เรียนรู้วิธีอัตโนมัติการรายงาน Excel ด้วย Aspose.Cells ใน Java โดยใช้
  CopyOptions และ PasteOptions เพื่อให้สูตรแม่นยำและวางเฉพาะค่าที่มองเห็นได้
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: อัตโนมัติการรายงาน Excel – เชี่ยวชาญ CopyOptions & PasteOptions ใน Java ด้วย
  Aspose.Cells
url: /th/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

 "**ทดสอบด้วย:**"

**Author:** => "**ผู้เขียน:**"

Now produce final content with all translations.

Check that we didn't translate code block placeholders. Keep them.

Check that we didn't translate URLs.

Check that we kept markdown formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# อัตโนมัติการรายงาน Excel ด้วย Aspose.Cells: CopyOptions & PasteOptions ใน Java

คุณกำลังมองหา **อัตโนมัติการรายงาน Excel** ด้วย Java หรือไม่? ด้วย Aspose.Cells คุณสามารถคัดลอก, วาง, และปรับสูตรโดยโปรแกรมได้เพื่อให้รายงานของคุณแม่นยำและส่งเฉพาะข้อมูลที่คุณต้องการ ในบทแนะนำนี้เราจะอธิบายคุณลักษณะสำคัญสองอย่าง—**CopyOptions.ReferToDestinationSheet** และ **PasteOptions**—ที่ช่วยให้คุณคงการอ้างอิงสูตรและวางค่าเฉพาะเซลล์ที่มองเห็นได้

## คำตอบด่วน
- **`CopyOptions.ReferToDestinationSheet` ทำอะไร?** ปรับสูตรให้ชี้ไปยังแผ่นงานปลายทางเมื่อคัดลอกข้อมูล.  
- **ฉันจะวางเฉพาะเซลล์ที่มองเห็นได้อย่างไร?** ตั้งค่า `PasteOptions.setOnlyVisibleCells(true)` พร้อมกับ `PasteType.VALUES`.  
- **ต้องการเวอร์ชันของไลบรารีใด?** Aspose.Cells 25.3 หรือใหม่กว่า.  
- **ต้องการไลเซนส์สำหรับการผลิตหรือไม่?** ใช่, ไลเซนส์ถาวรหรือชั่วคราวจะลบข้อจำกัดการประเมิน.  
- **ฉันสามารถใช้ Maven หรือ Gradle ได้หรือไม่?** ทั้งสองได้รับการสนับสนุน; ดูตัวอย่างการขึ้นต่อด้านล่าง.

## “การอัตโนมัติการรายงาน Excel” คืออะไร?
การอัตโนมัติการรายงาน Excel หมายถึงการสร้าง, รวมและจัดรูปแบบไฟล์ Excel อย่างโปรแกรมเมชัน เพื่อลดขั้นตอนคัดลอก‑วางด้วยมือและลดข้อผิดพลาด Aspose.Cells มี API ที่ครบถ้วนที่ช่วยให้นักพัฒนา Java จัดการสเปรดชีตในระดับใหญ่ได้

## ทำไมต้องใช้ CopyOptions และ PasteOptions สำหรับการรายงาน?
- **รักษาความสมบูรณ์ของสูตร** เมื่อย้ายข้อมูลระหว่างแผ่นงาน.  
- **ยกเว้นแถว/คอลัมน์ที่ซ่อน** เพื่อให้รายงานสะอาดและเน้นข้อมูล.  
- **เพิ่มประสิทธิภาพ** โดยคัดลอกเฉพาะข้อมูลที่จำเป็นแทนการคัดลอกช่วงทั้งหมด.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือสูงกว่า.  
- Maven หรือ Gradle สำหรับการจัดการ dependencies.  
- Aspose.Cells 25.3+ (รุ่นทดลอง, ไลเซนส์ชั่วคราว หรือไลเซนส์ถาวร).

## การตั้งค่า Aspose.Cells สำหรับ Java

เพิ่มไลบรารีลงในโครงการของคุณด้วยวิธีใดวิธีหนึ่งต่อไปนี้:

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
implementation 'com.aspose:aspose-cells:25.3'
```

### การรับไลเซนส์
- **Free Trial** – ชุดฟีเจอร์เต็มสำหรับการประเมิน.  
- **Temporary License** – ลบข้อจำกัดของรุ่นทดลองขณะคุณทดสอบ.  
- **Permanent License** – แนะนำสำหรับการใช้งานในสภาพแวดล้อมการผลิต.

เริ่มต้น Aspose.Cells ในโค้ด Java ของคุณ:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## คู่มือขั้นตอนโดยละเอียด

### 1. CopyOptions กับ ReferToDestinationSheet

#### ภาพรวม
การตั้งค่า `CopyOptions.ReferToDestinationSheet` เป็น `true` จะเขียนทับการอ้างอิงสูตรให้ชี้ไปยังแผ่นงานใหม่หลังจากการคัดลอก

#### ขั้นตอนที่ 1: เริ่มต้น Workbook และ Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### ขั้นตอนที่ 2: กำหนดค่า CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### ขั้นตอนที่ 3: ดำเนินการคัดลอก
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*ทำไมเรื่องนี้สำคัญ*: สูตรที่เคยอ้างอิง `Sheet1` จะอ้างอิง `DestSheet` อย่างถูกต้อง ทำให้รายงานอัตโนมัติของคุณเชื่อถือได้

**เคล็ดลับการแก้ปัญหา**: หากสูตรยังอ้างอิงแผ่นงานเก่า ให้ตรวจสอบว่าได้เรียก `setReferToDestinationSheet(true)` **ก่อน** การคัดลอก

### 2. PasteOptions สำหรับค่าที่มาจากเซลล์ที่มองเห็นเท่านั้น

#### ภาพรวม
`PasteOptions` ให้คุณกำหนดสิ่งที่ต้องการวาง การใช้ `PasteType.VALUES` ร่วมกับ `onlyVisibleCells=true` จะคัดลอกเฉพาะค่าที่แสดงผลเท่านั้น ไม่รวมแถว/คอลัมน์ที่ซ่อนและการจัดรูปแบบ

#### ขั้นตอนที่ 1: เริ่มต้น Workbook และ Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### ขั้นตอนที่ 2: กำหนดค่า PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### ขั้นตอนที่ 3: ดำเนินการวาง
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*ทำไมเรื่องนี้สำคัญ*: เหมาะสำหรับการดึงข้อมูลที่กรองหรือสร้างรายงานที่สะอาดโดยไม่มีแถวที่ซ่อนหรือเสียงรบกวนจากการจัดรูปแบบ

**เคล็ดลับการแก้ปัญหา**: ตรวจสอบว่าแถว/คอลัมน์ถูกซ่อนจริงใน Excel ก่อนทำการคัดลอก; หากไม่เช่นนั้นจะถูกรวมอยู่

## การประยุกต์ใช้งานจริง
1. **Financial Consolidation** – รวมแผ่นงานรายเดือนเป็นเวิร์กบุ๊กหลักพร้อมคงสูตรทั้งหมดให้แม่นยำ.  
2. **Filtered Data Export** – ดึงเฉพาะแถวที่มองเห็นจากตารางที่กรองไปยังแผ่นสรุป.  
3. **Scheduled Report Generation** – อัตโนมัติการสร้างรายงาน Excel ทุกคืนด้วยค่าของเซลล์ที่แม่นยำและการอ้างอิงที่ถูกต้อง.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- **Dispose of Workbooks** เมื่อเสร็จ (`wb.dispose();`) เพื่อปล่อยทรัพยากรเนทีฟ.  
- **Batch Operations** – รวมหลายการเรียกคัดลอก/วางเพื่อ ลดภาระ.  
- **Monitor Memory** – เวิร์กบุ๊กขนาดใหญ่อาจต้องเพิ่ม heap (`-Xmx2g`).

## คำถามที่พบบ่อย

**Q1: `CopyOptions.ReferToDestinationSheet` ใช้ทำอะไร?**  
A: มันเขียนทับการอ้างอิงสูตรให้ชี้ไปยังแผ่นงานปลายทางหลังการคัดลอก เพื่อให้สูตรการรายงานยังคงถูกต้อง

**Q2: ฉันจะวางเฉพาะเซลล์ที่มองเห็นได้อย่างไร?**  
A: ตั้งค่า `PasteOptions.setOnlyVisibleCells(true)` และเลือก `PasteType.VALUES`.

**Q3: ฉันสามารถใช้ Aspose.Cells ได้โดยไม่ซื้อไลเซนส์หรือไม่?**  
A: ได้, มีรุ่นทดลองหรือไลเซนส์ชั่วคราวสำหรับการประเมิน, แต่ต้องมีไลเซนส์ถาวรสำหรับการผลิต.

**Q4: ทำไมบางการอ้างอิงยังผิดพลาดหลังการคัดลอก?**  
A: ตรวจสอบให้แน่ใจว่าได้เปิดใช้งาน `ReferToDestinationSheet` **ก่อน** การคัดลอกและสูตรต้นทางไม่มีลิงก์ไปยังเวิร์กบุ๊กภายนอก.

**Q5: ควรปฏิบัติตามแนวทางการจัดการหน่วยความจำอย่างไร?**  
A: ทำการ Dispose ของอ็อบเจ็กต์ `Workbook` เมื่อเสร็จ, ประมวลผลไฟล์ขนาดใหญ่เป็นชิ้นส่วน, และตรวจสอบการใช้ heap ของ JVM.

**Q6: สามารถรวม CopyOptions และ PasteOptions ในการดำเนินการเดียวได้หรือไม่?**  
A: ได้, คุณสามารถเชื่อมต่อโดยคัดลอกด้วย `CopyOptions` ก่อนแล้วจึงใช้ `PasteOptions` กับช่วงเป้าหมาย.

## แหล่งข้อมูล
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free Trial**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support Forum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**อัปเดตล่าสุด:** 2026-02-22  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose