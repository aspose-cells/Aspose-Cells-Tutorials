---
"date": "2025-04-08"
"description": "เรียนรู้วิธีใช้ Aspose.Cells สำหรับ Java เพื่อเพิ่มกล่องข้อความและกำหนดระยะห่างระหว่างบรรทัดในเวิร์กบุ๊ก Excel ปรับปรุงการนำเสนอเวิร์กบุ๊กของคุณด้วยรูปร่างข้อความที่มีสไตล์"
"title": "เพิ่มกล่องข้อความและกำหนดระยะห่างระหว่างบรรทัดใน Excel โดยใช้ Aspose.Cells สำหรับ Java"
"url": "/th/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# เพิ่มกล่องข้อความและกำหนดระยะห่างระหว่างบรรทัดใน Excel โดยใช้ Aspose.Cells สำหรับ Java

## การแนะนำ

การสร้างรายงาน Excel แบบไดนามิกมักต้องมีการจัดรูปแบบข้อความแบบกำหนดเอง เช่น การเพิ่มกล่องข้อความที่มีระยะห่างระหว่างบรรทัดเฉพาะ ด้วย Aspose.Cells สำหรับ Java จะทำให้เรื่องนี้กลายเป็นเรื่องง่ายและมีประสิทธิภาพ บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการปรับปรุงการนำเสนอเวิร์กบุ๊กของคุณโดยใช้ Aspose.Cells สำหรับ Java เพื่อเพิ่มรูปร่างข้อความที่มีสไตล์

เมื่ออ่านคู่มือนี้จบ คุณจะเรียนรู้วิธีการดังต่อไปนี้:
- สร้างเวิร์กบุ๊ก Excel ใหม่และเข้าถึงเวิร์กชีตของมัน
- เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
- กำหนดระยะห่างบรรทัดแบบกำหนดเองภายในรูปร่างข้อความ
- บันทึกสมุดงานของคุณในรูปแบบ XLSX

เริ่มต้นด้วยการตั้งค่าสภาพแวดล้อมของคุณกันก่อน

### ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:
- ติดตั้ง Java Development Kit (JDK) บนเครื่องของคุณ
- IDE หรือโปรแกรมแก้ไขสำหรับเขียนโค้ด Java
- ระบบสร้าง Maven หรือ Gradle ที่ถูกกำหนดค่าเพื่อจัดการการอ้างอิง

ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java และความคุ้นเคยกับโครงสร้างไฟล์ Excel จะเป็นประโยชน์

## การตั้งค่า Aspose.Cells สำหรับ Java

รวม Aspose.Cells ในการจัดการการอ้างอิงของโครงการของคุณโดยใช้ Maven หรือ Gradle:

**เมเวน**

เพิ่มบล็อกการอ้างอิงต่อไปนี้ลงในของคุณ `pom.xml` ไฟล์:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**แกรเดิล**

รวมสิ่งนี้ไว้ในของคุณ `build.gradle` ไฟล์:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

ขั้นตอนต่อไป คือการรับใบอนุญาตสำหรับ Aspose.Cells โดยเลือกทดลองใช้งานฟรี ขอใบอนุญาตชั่วคราว หรือซื้อใบอนุญาตแบบเต็มรูปแบบ

### การเริ่มต้น Aspose.Cells

เมื่อรวมไลบรารีไว้ในโครงการของคุณแล้ว ให้เริ่มต้นใช้งานภายในแอปพลิเคชัน Java ของคุณ:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // เริ่มต้นอินสแตนซ์ของเวิร์กบุ๊ก (แสดงถึงไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## คู่มือการใช้งาน

### สร้างสมุดงานและเข้าถึงแผ่นงาน

เริ่มต้นด้วยการสร้างเวิร์กบุ๊ก Excel ใหม่และเข้าถึงเวิร์กชีตแรก จากนั้นเพิ่มกล่องข้อความของคุณ

#### ภาพรวม

การสร้างเวิร์กบุ๊กใหม่จะจัดให้มีพื้นที่ว่างสำหรับผนวกข้อมูล รูปร่าง และการจัดรูปแบบตามต้องการ

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### เพิ่มกล่องข้อความลงในแผ่นงาน

ขั้นตอนต่อไป เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีตที่คุณเลือก รูปร่างนี้สามารถบรรจุเนื้อหาข้อความใดๆ ที่คุณต้องการได้

#### ภาพรวม

กล่องข้อความเป็นเครื่องมืออเนกประสงค์สำหรับการรวมข้อความที่กำหนดเอง เช่น หมายเหตุหรือคำแนะนำลงในแผ่นงาน Excel โดยตรง

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### ตั้งค่าข้อความในรูปร่าง

เมื่อกล่องข้อความของคุณพร้อมแล้ว ให้ตั้งค่าเนื้อหาและจัดรูปแบบข้อความภายในนั้น

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // กำหนดเนื้อหาข้อความภายในรูปร่าง
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### เข้าถึงย่อหน้าข้อความในรูปร่าง

คุณสามารถเข้าถึงแต่ละย่อหน้าภายในกล่องข้อความเพื่อใช้การจัดรูปแบบเฉพาะได้

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // กำหนดเนื้อหาข้อความภายในรูปร่าง
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // เข้าถึงย่อหน้าที่สองในรูป
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### ตั้งค่าระยะห่างระหว่างบรรทัดของย่อหน้า

การกำหนดระยะห่างระหว่างบรรทัดเองสามารถช่วยให้อ่านได้ง่ายขึ้น ดังต่อไปนี้คือวิธีตั้งค่า:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // กำหนดเนื้อหาข้อความภายในรูปร่าง
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // เข้าถึงย่อหน้าที่สองในรูป
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // กำหนดระยะห่างบรรทัดเป็น 20 จุด
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // กำหนดช่องว่างก่อนและหลังย่อหน้า
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### บันทึกสมุดงาน

สุดท้าย ให้บันทึกสมุดงานของคุณด้วยกล่องข้อความที่เพิ่มและจัดรูปแบบใหม่

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // สร้างสมุดงานใหม่ (ไฟล์ Excel)
        Workbook workbook = new Workbook();
        
        // เข้าถึงแผ่นงานแรก
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // เพิ่มรูปร่างกล่องข้อความลงในเวิร์กชีต
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // กำหนดเนื้อหาข้อความภายในรูปร่าง
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // เข้าถึงย่อหน้าที่สองในรูป
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // กำหนดระยะห่างบรรทัดเป็น 20 จุด
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // กำหนดช่องว่างก่อนและหลังย่อหน้า
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // บันทึกสมุดงาน
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## บทสรุป

คุณได้เรียนรู้วิธีการเพิ่มกล่องข้อความและกำหนดระยะห่างระหว่างบรรทัดในเวิร์กบุ๊ก Excel โดยใช้ Aspose.Cells สำหรับ Java สำเร็จแล้ว ซึ่งจะช่วยเพิ่มความสามารถในการสร้างรายงานแบบไดนามิกที่สวยงาม

## คำแนะนำคีย์เวิร์ด
- "Aspose.Cells สำหรับ Java"
- "เพิ่มกล่องข้อความใน Excel"
- "ตั้งค่าระยะห่างระหว่างบรรทัดใน Excel"
- "สมุดงาน Excel พร้อมข้อความที่มีสไตล์"
- “Java และ Aspose.Cells”


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}