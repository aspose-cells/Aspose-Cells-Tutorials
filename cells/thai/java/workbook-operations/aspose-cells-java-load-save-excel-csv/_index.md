---
"date": "2025-04-07"
"description": "เรียนรู้วิธีการแปลงไฟล์ Excel เป็นรูปแบบ CSV อย่างมีประสิทธิภาพโดยใช้ Aspose.Cells สำหรับ Java คู่มือนี้ครอบคลุมการโหลด การกำหนดค่า และการบันทึกเวิร์กบุ๊กพร้อมขั้นตอนโดยละเอียด"
"title": "วิธีโหลดและบันทึก Excel เป็น CSV โดยใช้ Aspose.Cells สำหรับ Java - คู่มือฉบับสมบูรณ์"
"url": "/th/java/workbook-operations/aspose-cells-java-load-save-excel-csv/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# วิธีการโหลดและบันทึก Excel เป็น CSV โดยใช้ Aspose.Cells สำหรับ Java
## การแนะนำ
การแปลงชุดข้อมูล Excel เป็นรูปแบบข้อความ เช่น CSV โดยยังคงรายละเอียดเฉพาะ เช่น ตัวคั่น อาจเป็นเรื่องท้าทาย คู่มือที่ครอบคลุมนี้สาธิตวิธีใช้ Aspose.Cells สำหรับ Java เพื่อการโหลด การกำหนดค่า และการบันทึกเวิร์กบุ๊ก Excel เป็นไฟล์ CSV อย่างมีประสิทธิภาพ เมื่ออ่านบทช่วยสอนนี้จบ คุณจะเชี่ยวชาญกระบวนการเหล่านี้ในแอปพลิเคชัน Java ของคุณ

**สิ่งที่คุณจะได้เรียนรู้:**
- การโหลดไฟล์ Excel ที่มีอยู่ลงในวัตถุเวิร์กบุ๊กโดยใช้ Aspose.Cells
- การกำหนดค่า TxtSaveOptions เพื่อจัดการตัวคั่นสำหรับแถวว่าง
- การบันทึกสมุดงานของคุณเป็นไฟล์ CSV ที่มีการกำหนดค่าเฉพาะ

## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มต้น ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- **สภาพแวดล้อมการพัฒนา Java:** ติดตั้งและกำหนดค่า JDK
- **Aspose.Cells สำหรับไลบรารี Java:** ต้องใช้เวอร์ชัน 25.3 ขึ้นไป
- **ไอดี:** ใช้ IntelliJ IDEA, Eclipse หรือสภาพแวดล้อมการพัฒนาอื่น ๆ ที่ต้องการ

## การตั้งค่า Aspose.Cells สำหรับ Java
### การพึ่งพา Maven
หากต้องการรวม Aspose.Cells ในโครงการ Maven ของคุณ ให้เพิ่มสิ่งนี้ลงใน `pom.xml`-
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
### การอ้างอิงของ Gradle
สำหรับผู้ใช้ Gradle ให้เพิ่มสิ่งนี้ลงใน `build.gradle`-
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
## การขอใบอนุญาต
Aspose.Cells สำหรับ Java มีทั้งใบอนุญาตทดลองใช้งานและใบอนุญาตเชิงพาณิชย์ เริ่มต้นด้วย [ทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/) เพื่อสำรวจความสามารถหรือซื้อใบอนุญาตหากเหมาะสม สำหรับใบอนุญาตชั่วคราว โปรดไปที่ [หน้าใบอนุญาตชั่วคราว](https://purchase-aspose.com/temporary-license/).
## คู่มือการใช้งาน
### การโหลดสมุดงาน Excel
**ภาพรวม:**
การโหลดไฟล์ Excel ลงใน Aspose.Cells เป็นเรื่องง่ายและจำเป็นสำหรับการดำเนินการในภายหลัง
#### ทีละขั้นตอน:
1. **นำเข้าคลาสที่จำเป็น**
   นำเข้า `Workbook` คลาสจากแพ็กเกจ Aspose.Cells:
   ```java
   import com.aspose.cells.Workbook;
   ```
2. **โหลดไฟล์ Excel**
   สร้างอินสแตนซ์เวิร์กบุ๊กด้วยเส้นทางไฟล์ของคุณ:
   ```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/KeepSeparatorsForBlankRow.xlsx");
   ```
### การกำหนดค่า TxtSaveOptions สำหรับการจัดการตัวคั่น
**ภาพรวม:**
ปรับแต่งวิธีการบันทึกไฟล์ข้อความ รวมถึงการรักษาตัวคั่นในแถวว่างด้วย `TxtSaveOptions`-
#### ทีละขั้นตอน:
1. **นำเข้าคลาส TxtSaveOptions**
   นำเข้าคลาสที่จำเป็นสำหรับการกำหนดค่าตัวเลือกการบันทึก:
   ```java
   import com.aspose.cells.TxtSaveOptions;
   ```
2. **ตั้งค่าตัวเลือกเพื่อเก็บตัวคั่น**
   การกำหนดค่า `TxtSaveOptions` เพื่อรักษาตัวคั่นในแถวว่าง:
   ```java
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   ```
### การบันทึกสมุดงานเป็นไฟล์ CSV พร้อมตัวเลือก
**ภาพรวม:**
ขั้นตอนนี้เกี่ยวข้องกับการบันทึกเวิร์กบุ๊กของคุณเป็นไฟล์ข้อความ โดยเฉพาะ CSV ในตัวอย่างนี้
#### ทีละขั้นตอน:
1. **ตั้งค่าเส้นทางการบันทึก**
   กำหนดตำแหน่งบันทึกเอาท์พุต:
   ```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   ```
2. **บันทึกสมุดงานด้วยตัวเลือกที่กำหนดค่าไว้**
   ใช้ `save` วิธีการเขียนสมุดงานของคุณเป็นไฟล์ CSV โดยใช้ตัวเลือกที่กำหนดค่าไว้:
   ```java
   Workbook workbook = new Workbook("YOUR_DATA_DIRECTORY/KeepSeparatorsForBlankRow.xlsx");
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   workbook.save(outDir + "/KeepSeparatorsForBlankRow.out.csv", options);
   ```
## การประยุกต์ใช้งานจริง
1. **การส่งออกข้อมูลเพื่อการรายงาน:** แปลงข้อมูล Excel เป็นรูปแบบ CSV สำหรับเครื่องมือสร้างรายงาน
2. **สคริปต์การประมวลผลแบบแบตช์:** การแปลงไฟล์ Excel หลายไฟล์ภายในไดเร็กทอรีแบบอัตโนมัติ
3. **การบูรณาการกับฐานข้อมูล:** เตรียมและส่งออกข้อมูล Excel เป็น CSV เพื่อนำเข้าฐานข้อมูล
## การพิจารณาประสิทธิภาพ
สำหรับการจัดการชุดข้อมูลขนาดใหญ่อย่างมีประสิทธิภาพ:
- เพิ่มประสิทธิภาพการใช้หน่วยความจำโดยปล่อยทรัพยากรทันทีโดยใช้ `workbook-dispose()`.
- ใช้ประโยชน์จากการรวบรวมขยะของ Java เพื่อจัดการหน่วยความจำอย่างมีประสิทธิภาพในแอปพลิเคชันที่ทำงานในระยะยาว
- สร้างโปรไฟล์แอปพลิเคชันของคุณเพื่อแก้ไขปัญหาคอขวด I/O ของไฟล์
## บทสรุป
ตอนนี้คุณเข้าใจวิธีการโหลด กำหนดค่า และบันทึกเวิร์กบุ๊ก Excel เป็นไฟล์ CSV โดยใช้ Aspose.Cells สำหรับ Java แล้ว คู่มือนี้ทำหน้าที่เป็นพื้นฐานสำหรับการผสานรวมความสามารถเหล่านี้เข้ากับแอปพลิเคชันของคุณ
**ขั้นตอนต่อไป:**
สำรวจคุณลักษณะเพิ่มเติมของ Aspose.Cells เช่น การจัดการข้อมูลและการจัดรูปแบบขั้นสูงเพื่อเพิ่มประสิทธิภาพการทำงาน
## ส่วนคำถามที่พบบ่อย
1. **ฉันจะจัดการไฟล์ขนาดใหญ่ด้วย Aspose.Cells ได้อย่างไร**
   - ใช้ API สตรีมมิ่งและเพิ่มประสิทธิภาพการใช้หน่วยความจำด้วยการจัดการทรัพยากรอย่างทันท่วงที
2. **ฉันสามารถใช้ Aspose.Cells ได้โดยไม่ต้องมีใบอนุญาตสำหรับการใช้งานจริงหรือไม่?**
   - ต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการผลิต เริ่มต้นด้วยการทดลองใช้เพื่อสำรวจขีดความสามารถ
3. **ฉันจะจัดการตัวแบ่ง CSV ที่แตกต่างกันได้อย่างไร**
   - การกำหนดค่า `TxtSaveOptions` โดยใช้วิธีการเช่น `setSeparator(';')`-
4. **จะเกิดอะไรขึ้นถ้าสมุดงานของฉันมีสูตร?**
   - Aspose.Cells จะคำนวณและส่งออกผลลัพธ์ของสูตรเมื่อบันทึกเป็นรูปแบบข้อความ
5. **ฉันสามารถปรับแต่งการจัดรูปแบบเซลล์ระหว่างการแปลงได้หรือไม่**
   - ใช่ สำรวจตัวเลือกเพิ่มเติมภายใน Aspose.Cells สำหรับการจัดรูปแบบและการนำเสนอข้อมูล
## ทรัพยากร
- [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/java/)
- [ดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/java/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/)
- [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}