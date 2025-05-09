---
"date": "2025-04-07"
"description": "เรียนรู้วิธีการสร้าง จัดรูปแบบ และจัดการแผนภูมิ Excel โดยใช้ Aspose.Cells สำหรับ Java คู่มือนี้ครอบคลุมทุกอย่างตั้งแต่การตั้งค่าสภาพแวดล้อมจนถึงการใช้งานฟีเจอร์แผนภูมิขั้นสูง"
"title": "การสร้างและการจัดรูปแบบแผนภูมิ Excel ด้วย Aspose.Cells สำหรับ Java"
"url": "/th/java/charts-graphs/excel-charts-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# การสร้างและการจัดรูปแบบแผนภูมิ Excel ด้วย Aspose.Cells สำหรับ Java

## การแนะนำ

การจัดการข้อมูลที่ซับซ้อนในไฟล์ Excel อาจเป็นเรื่องท้าทาย แต่เครื่องมืออย่าง Aspose.Cells สำหรับ Java จะทำให้เรื่องนี้ง่ายขึ้น ไลบรารีอันทรงพลังนี้ช่วยให้คุณอ่าน เขียน และจัดการสเปรดชีตได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับการสร้างและจัดรูปแบบแผนภูมิโดยใช้ Aspose.Cells สำหรับ Java เพื่อให้แน่ใจว่าการนำเสนอข้อมูลของคุณถูกต้องและดึงดูดสายตา

**สิ่งที่คุณจะได้เรียนรู้:**
- แสดงเวอร์ชันของ Aspose.Cells สำหรับ Java
- โหลดและเข้าถึงไฟล์ Excel
- เพิ่มชุดข้อมูลลงในแผนภูมิและกำหนดรหัสรูปแบบ
- บันทึกไฟล์ Excel ที่ปรับเปลี่ยนอย่างมีประสิทธิภาพ

เริ่มต้นด้วยการตั้งค่าสภาพแวดล้อมของคุณและนำคุณลักษณะเหล่านี้ไปใช้

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม ให้แน่ใจว่าคุณมีสิ่งต่อไปนี้:

- **ชุดพัฒนา Java (JDK)**:แนะนำเวอร์ชัน 8 ขึ้นไป
- **สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE)**เช่น IntelliJ IDEA, Eclipse หรือ NetBeans
- **Aspose.Cells สำหรับ Java**:เราจะใช้ไลบรารีเวอร์ชัน 25.3 นี้

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม

ตรวจสอบให้แน่ใจว่า IDE ของคุณได้รับการกำหนดค่าด้วย JDK และคุณมีความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรม Java ความคุ้นเคยกับโครงสร้างไฟล์ Excel ก็จะเป็นประโยชน์เช่นกัน

## การตั้งค่า Aspose.Cells สำหรับ Java

หากต้องการเริ่มใช้ Aspose.Cells สำหรับ Java ให้รวมไว้ในโปรเจ็กต์ของคุณโดยใช้ Maven หรือ Gradle:

### เมเวน
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### แกรเดิล
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### การขอใบอนุญาต

คุณสามารถรับใบอนุญาตทดลองใช้งานฟรีหรือซื้อใบอนุญาตเต็มรูปแบบเพื่อปลดล็อกฟีเจอร์ทั้งหมดของ Aspose.Cells สำหรับ Java เยี่ยมชม [หน้าการซื้อ](https://purchase.aspose.com/buy) เพื่อดูรายละเอียดเพิ่มเติมเกี่ยวกับตัวเลือกใบอนุญาต

### การเริ่มต้นและการตั้งค่าเบื้องต้น

เมื่อคุณเพิ่มการอ้างอิงแล้ว ให้เริ่มต้น Aspose.Cells ในโปรเจ็กต์ของคุณ:

```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // กำหนดใบอนุญาตหากมี
        License license = new License();
        license.setLicense("path_to_your_license.lic");

        // แสดงเวอร์ชันของ Aspose.Cells สำหรับ Java ที่กำลังใช้งานอยู่
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## คู่มือการใช้งาน

### แสดงเวอร์ชัน Aspose.Cells

ฟีเจอร์นี้ช่วยให้คุณตรวจสอบว่าใช้ Aspose.Cells เวอร์ชันใดอยู่ เพื่อให้แน่ใจถึงความเข้ากันได้และการเข้าถึงฟีเจอร์ล่าสุด

```java
import com.aspose.cells.*;

public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // ส่งออกเวอร์ชันของ Aspose.Cells สำหรับ Java ที่กำลังใช้อยู่
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

### โหลดและเข้าถึงไฟล์ Excel

การโหลดไฟล์ Excel เป็นเรื่องง่ายด้วย Aspose.Cells นี่คือวิธีเข้าถึงเวิร์กชีตที่ต้องการ:

```java
import com.aspose.cells.*;

public class LoadAndAccessExcelFile {
    public static void main(String[] args) throws Exception {
        // กำหนดไดเรกทอรีข้อมูลตามเส้นทางของคุณ
        String dataDir = "YOUR_DATA_DIRECTORY";

        // โหลดไฟล์ Excel ต้นฉบับจากไดเร็กทอรีที่ระบุ
        Workbook wb = new Workbook(dataDir + "/sampleSeries_ValuesFormatCode.xlsx");

        // เข้าถึงแผ่นงานแรกในสมุดงาน
        Worksheet worksheet = wb.getWorksheets().get(0);
    }
}
```

### การเข้าถึงและเพิ่มซีรีส์ลงในแผนภูมิ

การเพิ่มชุดข้อมูลลงในแผนภูมิถือเป็นสิ่งสำคัญสำหรับการแสดงข้อมูลแบบภาพ คุณสามารถทำได้ดังนี้:

```java
import com.aspose.cells.*;

public class AccessAndAddSeriesToChart {
    public static void main(String[] args) throws Exception {
        // กำหนดไดเรกทอรีข้อมูลตามเส้นทางของคุณ
        String dataDir = "YOUR_DATA_DIRECTORY";

        // โหลดไฟล์ Excel
        Workbook wb = new Workbook(dataDir + "/sampleSeries_ValuesFormatCode.xlsx");

        // เข้าถึงแผ่นงานแรก
        Worksheet worksheet = wb.getWorksheets().get(0);

        // เข้าถึงแผนภูมิแรกในเวิร์กชีต
        Chart ch = worksheet.getCharts().get(0);

        // เพิ่มซีรีส์ลงในแผนภูมิโดยใช้ค่าเป็นอาร์เรย์
        ch.getNSeries().add("{10000, 20000, 30000, 40000}", true);
    }
}
```

### ตั้งค่ารูปแบบรหัสสำหรับชุดแผนภูมิ

การจัดรูปแบบข้อมูลแผนภูมิเป็นสิ่งสำคัญสำหรับการอ่านได้ ต่อไปนี้คือวิธีการตั้งค่ารูปแบบสกุลเงิน:

```java
import com.aspose.cells.*;

public class SetValuesFormatCodeForChartSeries {
    public static void main(String[] args) throws Exception {
        // กำหนดไดเรกทอรีข้อมูลตามเส้นทางของคุณ
        String dataDir = "YOUR_DATA_DIRECTORY";

        // โหลดไฟล์ Excel
        Workbook wb = new Workbook(dataDir + "/sampleSeries_ValuesFormatCode.xlsx");

        // เข้าถึงแผ่นงานแรก
        Worksheet worksheet = wb.getWorksheets().get(0);

        // เข้าถึงแผนภูมิแรกในเวิร์กชีต
        Chart ch = worksheet.getCharts().get(0);

        // เข้าถึงซีรีย์และตั้งค่ารหัสรูปแบบเป็นรูปแบบสกุลเงิน
        Series srs = ch.getNSeries().get(0);
        srs.setValuesFormatCode("$#,##0");
    }
}
```

### บันทึกไฟล์ Excel

หลังจากทำการเปลี่ยนแปลงแล้ว ให้บันทึกสมุดงานของคุณเพื่อเก็บรักษาการอัปเดต:

```java
import com.aspose.cells.*;

public class SaveExcelFile {
    public static void main(String[] args) throws Exception {
        // กำหนดไดเรกทอรีเอาท์พุตโดยใช้เส้นทางของคุณ
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // โหลดไฟล์ Excel
        Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSeries_ValuesFormatCode.xlsx");

        // บันทึกสมุดงานไปยังไดเร็กทอรีเอาท์พุตที่ระบุ
        wb.save(outDir + "/outputSeries_ValuesFormatCode.xlsx");
    }
}
```

## การประยุกต์ใช้งานจริง

Aspose.Cells สำหรับ Java สามารถใช้ได้ในสถานการณ์ต่างๆ:

1. **การรายงานทางการเงิน**:สร้างและจัดรูปแบบแผนภูมิทางการเงินสำหรับรายงานรายไตรมาส
2. **การวิเคราะห์ข้อมูล**:แสดงภาพแนวโน้มข้อมูลโดยใช้แผนภูมิแบบไดนามิกใน Excel
3. **การจัดการสินค้าคงคลัง**ติดตามระดับสต๊อกสินค้าด้วยแผนภูมิที่มีการจัดรูปแบบ

การรวม Aspose.Cells เข้ากับระบบอื่นๆ เช่น ฐานข้อมูลหรือแอปพลิเคชันเว็บ อาจช่วยเพิ่มความสามารถของระบบได้

## การพิจารณาประสิทธิภาพ

เพื่อเพิ่มประสิทธิภาพการทำงานเมื่อทำงานกับชุดข้อมูลขนาดใหญ่:

- ใช้วิธีการใช้หน่วยความจำอย่างมีประสิทธิภาพที่จัดทำโดย Aspose.Cells
- จัดการทรัพยากรอย่างรอบคอบเพื่อหลีกเลี่ยงการรั่วไหล
- ปฏิบัติตามแนวทางปฏิบัติที่ดีที่สุดของ Java สำหรับการจัดการหน่วยความจำ

## บทสรุป

ในบทช่วยสอนนี้ เราจะมาเรียนรู้วิธีนำแผนภูมิและการจัดรูปแบบของ Excel ไปใช้โดยใช้ Aspose.Cells สำหรับ Java โดยทำตามขั้นตอนเหล่านี้ คุณสามารถปรับปรุงการนำเสนอข้อมูลและปรับปรุงเวิร์กโฟลว์ของคุณให้มีประสิทธิภาพยิ่งขึ้น

**ขั้นตอนต่อไป:**
- ทดลองใช้แผนภูมิประเภทและรูปแบบที่แตกต่างกัน
- สำรวจคุณสมบัติเพิ่มเติมของ Aspose.Cells โดยปรึกษา [เอกสารประกอบ](https://reference-aspose.com/cells/java/).

พร้อมที่จะพัฒนาทักษะ Excel ของคุณไปสู่อีกระดับหรือยัง ลองนำโซลูชันเหล่านี้ไปใช้ในโครงการของคุณวันนี้!

## ส่วนคำถามที่พบบ่อย

1. **ฉันจะติดตั้ง Aspose.Cells สำหรับ Java ได้อย่างไร?**
   - ใช้การอ้างอิง Maven หรือ Gradle ดังที่แสดงด้านบน

2. **ฉันสามารถใช้ Aspose.Cells โดยไม่ต้องมีใบอนุญาตได้หรือไม่?**
   - ใช่ แต่มีข้อจำกัด ควรพิจารณาขอใบอนุญาตชั่วคราวเพื่อเข้าถึงแบบเต็มรูปแบบ

3. **Java เวอร์ชันใดบ้างที่เข้ากันได้กับ Aspose.Cells?**
   - ขอแนะนำเวอร์ชัน 8 ขึ้นไป

4. **ฉันจะจัดรูปแบบข้อมูลแผนภูมิใน Excel โดยใช้ Aspose.Cells ได้อย่างไร**
   - ใช้ `setValuesFormatCode` วิธีการใช้รูปแบบเฉพาะเจาะจง

5. **ฉันสามารถหาทรัพยากรเพิ่มเติมเกี่ยวกับ Aspose.Cells สำหรับ Java ได้ที่ไหน**
   - เยี่ยมชม [เอกสารอย่างเป็นทางการ](https://reference.aspose.com/cells/java/) และ [ฟอรั่มสนับสนุน](https://forum-aspose.com/c/cells/9).

## ทรัพยากร

- **เอกสารประกอบ**- [อ้างอิง Aspose.Cells สำหรับ Java](https://reference.aspose.com/cells/java/)
- **ดาวน์โหลด**- [หน้าดาวน์โหลด Aspose.Cells สำหรับ Java](https://downloads.aspose.com/cells/java)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}