---
"date": "2025-04-08"
"description": "เรียนรู้วิธีการจัดการและแยกวัตถุ OLE ที่ฝังอยู่ในไฟล์ Excel อย่างมีประสิทธิภาพโดยใช้ Aspose.Cells สำหรับ Java ปฏิบัติตามคำแนะนำทีละขั้นตอนนี้เพื่อการบูรณาการที่ราบรื่น"
"title": "แยกและบันทึกวัตถุ OLE จาก Excel โดยใช้ Aspose.Cells Java&#58; คู่มือฉบับสมบูรณ์"
"url": "/th/java/ole-objects-embedded-content/aspose-cells-java-extract-save-ole-objects/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# แยกและบันทึกวัตถุ OLE จาก Excel โดยใช้ Aspose.Cells Java: คู่มือฉบับสมบูรณ์

## การแนะนำ

การจัดการอ็อบเจ็กต์ OLE (Object Linking and Embedding) ที่ฝังอยู่ภายในไฟล์ Excel ถือเป็นงานสำคัญสำหรับนักพัฒนาซอฟต์แวร์และนักวิเคราะห์ข้อมูล บทช่วยสอนนี้ให้คำแนะนำที่ครอบคลุมเกี่ยวกับการใช้ Aspose.Cells สำหรับ Java เพื่อแยกและบันทึกอ็อบเจ็กต์เหล่านี้อย่างมีประสิทธิภาพ และทำให้เวิร์กโฟลว์ของคุณราบรื่นขึ้นด้วยรูปแบบไฟล์ที่หลากหลาย

**สิ่งที่คุณจะได้เรียนรู้:**
- การเริ่มต้นเวิร์กบุ๊ก Excel ด้วย Aspose.Cells
- การแยกวัตถุ OLE จากแผ่นงาน
- บันทึกไฟล์ที่แยกออกมาในรูปแบบต่างๆ (DOCX, XLSX, PPTX, PDF)
- การจัดการกรณีเฉพาะเช่นการบันทึกเป็นไฟล์ Excel ใหม่

เมื่ออ่านคู่มือนี้จบ คุณจะพร้อมปรับปรุงแอปพลิเคชัน Java ของคุณด้วยความสามารถในการจัดการข้อมูลอันทรงพลัง

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการต่อ ให้แน่ใจว่าคุณมี:

**ห้องสมุดที่จำเป็น:**
- Aspose.Cells สำหรับ Java (เวอร์ชัน 25.3 หรือใหม่กว่า)
- ความเข้ากันได้กับ JDK เวอร์ชันที่เหมาะสำหรับการรัน Aspose.Cells

**ข้อกำหนดการตั้งค่าสภาพแวดล้อม:**
- ความเข้าใจพื้นฐานเกี่ยวกับเครื่องมือสร้าง Java และ Maven/Gradle
- สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น IntelliJ IDEA หรือ Eclipse

**ข้อกำหนดความรู้เบื้องต้น:**
- ความคุ้นเคยกับการจัดการไฟล์ใน Java
- ทำความเข้าใจวัตถุ OLE ใน Excel

## การตั้งค่า Aspose.Cells สำหรับ Java

ในการเริ่มต้น ให้รวม Aspose.Cells ในโครงการของคุณโดยใช้การกำหนดค่าต่อไปนี้:

**เมเวน:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**เกรเดิ้ล:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### การขอใบอนุญาต

Aspose.Cells นำเสนอตัวเลือกการออกใบอนุญาตต่างๆ:
- **ทดลองใช้งานฟรี**ดาวน์โหลดรุ่นทดลองใช้เพื่อทดสอบฟังก์ชั่นต่างๆ
- **ใบอนุญาตชั่วคราว**: การขอใบอนุญาตประเมินผลแบบขยายเวลา
- **ซื้อ**: รับใบอนุญาตใช้งานการผลิตแบบถาวร

เยี่ยมชม [หน้าการซื้อ](https://purchase.aspose.com/buy) หรือร้องขอ [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) ตามความต้องการของคุณ

### การเริ่มต้นขั้นพื้นฐาน

นี่คือวิธีการเริ่มต้น Aspose.Cells ในแอปพลิเคชัน Java ของคุณ:
```java
import com.aspose.cells.Workbook;

public class InitializeWorkbook {
    public static void main(String[] args) {
        Workbook workbook = new Workbook("path/to/excel/file.xlsx");
        // ดำเนินการใช้สมุดงานวัตถุตามต้องการ
    }
}
```

## คู่มือการใช้งาน

### คุณลักษณะที่ 1: แยกวัตถุ OLE จาก Excel

**ภาพรวม:** เริ่มต้นเวิร์กบุ๊กและแยกวัตถุที่ฝังตัวจากเวิร์กชีตแรก

#### ขั้นตอนที่ 1: เริ่มต้นเวิร์กบุ๊ก
ตั้งค่าเส้นทางไดเรกทอรีข้อมูลของคุณและสร้าง `Workbook` ตัวอย่าง:
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/oleFile.xlsx");
```

#### ขั้นตอนที่ 2: แยกวัตถุ OLE
เข้าถึงคอลเลกชันของวัตถุ OLE ในเวิร์กชีตแรก:
```java
import com.aspose.cells.OleObjectCollection;

OleObjectCollection oleObjects = workbook.getWorksheets().get(0).getOleObjects();
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    // ดำเนินการแต่ละวัตถุที่นี่
}
```

#### ขั้นตอนที่ 3: บันทึกวัตถุที่แยกออกมา
บันทึกวัตถุ OLE ที่ถูกแยกออกมาแต่ละรายการตามประเภทไฟล์:
```java
import com.aspose.cells.FileFormatType;
import java.io.FileOutputStream;

String outDir = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    String fileName = outDir + "/object" + i + ".";

    switch (object.getFileFormatType()) {
        case FileFormatType.DOCX:
            fileName += "docx";
            break;
        case FileFormatType.XLSX:
            fileName += "xlsx";
            break;
        // เพิ่มรูปแบบอื่น ๆ ตามต้องการ
    }

    if (object.getFileFormatType() == FileFormatType.XLSX) {
        byte[] bytes = object.getObjectData();
        Workbook oleBook = new Workbook(new java.io.ByteArrayInputStream(bytes));
        oleBook.getSettings().setHidden(false);
        oleBook.save(fileName);
    } else {
        try (FileOutputStream fos = new FileOutputStream(fileName)) {
            fos.write(object.getObjectData());
        }
    }
}
```

### คุณสมบัติ 2: บันทึกวัตถุ OLE เป็นไฟล์ Excel
**ภาพรวม:** สาธิตการบันทึกวัตถุ OLE ที่ถูกแยกออกมาเป็นไฟล์ Excel โดยเฉพาะ

#### ขั้นตอนที่ 1: ดึงข้อมูล OLE
สมมติว่าคุณมี `byte[] bytes` จาก `OleObject`-
```java
import com.aspose.cells.Workbook;
import java.io.ByteArrayInputStream;

Workbook oleBook = new Workbook(new ByteArrayInputStream(bytes));
oleBook.getSettings().setHidden(false);
oleBook.save("YOUR_OUTPUT_DIRECTORY/object.xlsx");
```

## การประยุกต์ใช้งานจริง

- **การรวมข้อมูล:** แยกประเภทเอกสารต่างๆ จาก Excel เพื่อจัดเก็บข้อมูลส่วนกลาง
- **การสร้างรายงานอัตโนมัติ:** บูรณาการและบันทึกรายงานในรูปแบบต่างๆ โดยตรงจากแอปพลิเคชันของคุณ
- **เครื่องมือย้ายข้อมูล:** ใช้ข้อมูลที่แยกออกมาเพื่อกระบวนการย้ายข้อมูลระหว่างระบบ

## การพิจารณาประสิทธิภาพ

- เพิ่มประสิทธิภาพการใช้หน่วยความจำด้วยการจัดการวัตถุขนาดใหญ่อย่างมีประสิทธิภาพ โดยอาจใช้วิธีการสตรีมมิ่ง
- ใช้การตั้งค่า Aspose.Cells เพื่อจัดการการมองเห็นและขนาดของเวิร์กบุ๊กแบบไดนามิก
- ใช้แนวทางปฏิบัติในการจัดการไฟล์ที่มีประสิทธิภาพเพื่อป้องกันการรั่วไหลของทรัพยากร

## บทสรุป

หากปฏิบัติตามคู่มือนี้ คุณจะสามารถแยกและบันทึกวัตถุ OLE ได้อย่างมีประสิทธิภาพโดยใช้ Aspose.Cells สำหรับ Java ความสามารถเหล่านี้จะช่วยปรับปรุงกระบวนการจัดการข้อมูลของคุณได้อย่างมาก

**ขั้นตอนต่อไป:**
ลองพิจารณาสำรวจฟีเจอร์เพิ่มเติมของ Aspose.Cells เช่น การจัดการแผนภูมิหรือการแปลงไฟล์ Excel ขั้นสูง เพื่อขยายแอปพลิเคชัน Java ของคุณเพิ่มเติม

## ส่วนคำถามที่พบบ่อย

1. **ฉันจะจัดการรูปแบบวัตถุ OLE ที่ไม่รองรับได้อย่างไร**
   - ใช้รูปแบบเริ่มต้น (เช่น JPG) สำหรับวัตถุที่ไม่รู้จัก
2. **ฉันสามารถแยกวัตถุ OLE จากหลายชีตได้หรือไม่**
   - ใช่ ทำซ้ำผ่านแต่ละเวิร์กชีตในเวิร์กบุ๊กและทำซ้ำขั้นตอนการแยกข้อมูล
3. **จะเกิดอะไรขึ้นถ้าวัตถุ OLE ไม่สามารถบันทึกได้อย่างถูกต้อง?**
   - ตรวจสอบสิทธิ์ของไฟล์และให้แน่ใจว่าเส้นทางไดเร็กทอรีเอาต์พุตถูกต้อง
4. **Aspose.Cells รองรับ Excel ทุกเวอร์ชันหรือไม่**
   - Aspose.Cells รองรับรูปแบบ Excel หลากหลาย รวมถึงรูปแบบเดิมๆ เช่น XLS
5. **ฉันจะเพิ่มประสิทธิภาพการทำงานเมื่อต้องจัดการกับไฟล์ขนาดใหญ่ได้อย่างไร**
   - พิจารณาการประมวลผลเป็นส่วนๆ หรือใช้เทคนิคการสตรีมไฟล์เพื่อจัดการการใช้หน่วยความจำอย่างมีประสิทธิภาพ

## ทรัพยากร
- [เอกสารประกอบ](https://reference.aspose.com/cells/java/)
- [ดาวน์โหลด Aspose.Cells](https://releases.aspose.com/cells/java/)
- [การซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ดาวน์โหลดทดลองใช้งานฟรี](https://releases.aspose.com/cells/java/)
- [การขอใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มการสนับสนุนชุมชน](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}