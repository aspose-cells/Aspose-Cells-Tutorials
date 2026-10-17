---
date: '2026-04-05'
description: เรียนรู้วิธีเพิ่มกล่องข้อความในแผนภูมิ Excel ด้วย Aspose.Cells for Java
  รวมถึงการโหลดเวิร์กบุ๊กและการบันทึกไฟล์ Excel ด้วย Java
keywords:
- how to add textbox
- save excel file java
- excel chart textbox
- load excel workbook java
- Aspose.Cells Java
title: วิธีเพิ่มกล่องข้อความลงในแผนภูมิ Excel ด้วย Aspose.Cells Java
url: /th/java/charts-graphs/add-textbox-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่ม TextBox ลงในแผนภูมิ Excel ด้วย Aspose.Cells Java

## บทนำ

การสำรวจโลกของการแสดงผลข้อมูลอาจเป็นเรื่องท้าทาย โดยเฉพาะเมื่อคุณต้องการเพิ่มคำอธิบายข้อความหรือป้ายกำกับแบบกำหนดเองโดยตรงบนแผนภูมิในสเปรดชีต Excel ของคุณ บทเรียนนี้จะนำคุณผ่านการใช้ Aspose.Cells for Java—ไลบรารีที่แข็งแกร่งซึ่งทำให้ภารกิจเหล่านี้ง่ายขึ้น—เพื่อผสาน TextBox ลงในแผนภูมิ Excel อย่างราบรื่น.

**สิ่งที่คุณจะได้เรียนรู้:**
- โหลดและจัดการไฟล์ Excel ด้วย Aspose.Cells for Java.
- เข้าถึงและแก้ไขออบเจ็กต์แผนภูมิในเวิร์กบุ๊ก Excel.
- เพิ่มและปรับแต่งควบคุม TextBox บนแผนภูมิ.
- บันทึกการเปลี่ยนแปลงของคุณกลับไปยังไฟล์ Excel.

### คำตอบสั้น
- **คลาสหลักที่ใช้โหลดเวิร์กบุ๊กคืออะไร?** `Workbook` from `com.aspose.cells`.
- **เมธอดใดที่เพิ่ม TextBox ลงในแผนภูมิ?** `addTextBoxInChart` on the chart's shape collection.
- **ฉันสามารถเปลี่ยนสีเติมของ TextBox ได้หรือไม่?** Yes, via `FillFormat` and `SolidFill`.
- **ฉันจะบันทึกไฟล์ที่แก้ไขได้อย่างไร?** Use `workbook.save` with a chosen `SaveFormat`.
- **ฉันต้องการไลเซนส์สำหรับการผลิตหรือไม่?** Yes, a commercial license removes evaluation limits.

## วิธีเพิ่ม TextBox ลงในแผนภูมิ Excel

เมื่อคุณเข้าใจกระบวนการทำงานโดยรวมแล้ว ให้ดำดิ่งสู่การดำเนินการแบบขั้นตอนต่อขั้นตอน แต่ละขั้นตอนจะรวมโค้ดสั้น (คงเดิม) และคำอธิบายที่ชัดเจนว่ามันทำอะไร

## ข้อกำหนดเบื้องต้น

- **ไลบรารีที่ต้องการ:** Aspose.Cells for Java เวอร์ชัน 25.3 หรือใหม่กว่า บทเรียนนี้ใช้การตั้งค่า Maven และ Gradle.
- **การตั้งค่าสภาพแวดล้อม:** Java Development Kit (JDK) ที่เข้ากันได้ติดตั้งบนเครื่องของคุณ.
- **ข้อกำหนดความรู้:** ความเข้าใจพื้นฐานของการเขียนโปรแกรม Java และความคุ้นเคยกับโครงสร้างไฟล์ Excel.

## การตั้งค่า Aspose.Cells สำหรับ Java

เพื่อใช้ Aspose.Cells ในโปรเจกต์ของคุณ คุณต้องเพิ่มเป็น dependency ต่อไปนี้เป็นวิธีทำโดยใช้ Maven หรือ Gradle:

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### การรับไลเซนส์

Aspose.Cells มีการให้ทดลองใช้ฟรี, ไลเซนส์ชั่วคราวสำหรับการทดสอบต่อเนื่อง, และตัวเลือกการซื้อเชิงพาณิชย์:

- **ทดลองใช้ฟรี:** ดาวน์โหลดไลบรารีเพื่อเริ่มทดลองคุณสมบัติต่าง ๆ.
- **ไลเซนส์ชั่วคราว:** รับได้จาก [here](https://purchase.aspose.com/temporary-license/) เพื่อประเมินความสามารถเต็มรูปแบบโดยไม่มีข้อจำกัด.
- **การซื้อ:** สำหรับการใช้งานต่อเนื่องในสภาพแวดล้อมการผลิต ให้ซื้อไลเซนส์ที่ [Aspose Purchase](https://purchase.aspose.com/buy).

### การเริ่มต้นและตั้งค่าเบื้องต้น

Once you've added the library, initialize it with your license if available:

```java
License license = new License();
license.setLicense("path/to/your/license/file.lic");
```

## คู่มือการดำเนินการ

เราจะเดินผ่านการเพิ่ม TextBox ลงในแผนภูมิ Excel ด้วย Aspose.Cells for Java แต่ละฟีเจอร์จะอธิบายรายละเอียดในคู่มือนี้.

### การโหลดไฟล์ Excel

**ภาพรวม:** เราเริ่มด้วยการโหลดไฟล์ Excel ที่มีอยู่เข้าสู่แอปพลิเคชันของเรา เพื่อให้เราสามารถจัดการเนื้อหาโดยโปรแกรมได้

#### ขั้นตอนที่ 1: นำเข้าคลาสที่จำเป็น
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

#### ขั้นตอนที่ 2: โหลดเวิร์กบุ๊ก
```java
String dataDir = "YOUR_DATA_DIRECTORY";
String filePath = dataDir + "/chart.xls";
Workbook workbook = new Workbook(filePath);
Worksheet worksheet = workbook.getWorksheets().get(0);
```
**คำอธิบาย:** คลาส `Workbook` แทนไฟล์ Excel การโหลดมันทำให้เข้าถึงแผ่นงานและเนื้อหาทั้งหมดได้

### การเข้าถึงออบเจ็กต์แผนภูมิ

**ภาพรวม:** เมื่อไฟล์ถูกโหลดแล้ว เราต้องดึงออบเจ็กต์แผนภูมิจากแผ่นงานที่ระบุ

#### ขั้นตอนที่ 3: นำเข้าคลาส Chart
```java
import com.aspose.cells.Chart;
```

#### ขั้นตอนที่ 4: เข้าถึงแผนภูมิแรก
```java
Chart chart = worksheet.getCharts().get(0);
```
**คำอธิบาย:** สิ่งนี้ดึงแผนภูมิแรกในแผ่นงานที่ใช้งานของคุณเพื่อการจัดการต่อไป

### การเพิ่มควบคุม TextBox ลงในแผนภูมิ

**ภาพรวม:** ตอนนี้ให้เพิ่ม TextBox ที่กำหนดเองลงในแผนภูมิของเราเพื่อแสดงคำอธิบายข้อความใด ๆ ที่ต้องการ

#### ขั้นตอนที่ 5: นำเข้าคลาสที่จำเป็น
```java
import com.aspose.cells.TextBox;
import com.aspose.cells.FillFormat;
import com.aspose.cells.LineFormat;
import java.awt.Color;
import com.aspose.cells.MsoLineDashStyle;
```

#### ขั้นตอนที่ 6: เพิ่มและปรับแต่ง TextBox
```java
TextBox txt = chart.getShapes().addTextBoxInChart(100, 100, 850, 2500);
txt.setText("Aspose");
txt.getFont().setItalic(true);
txt.getFont().setSize(20);
txt.getFont().setBold(true);

// Set Fill Format
FillFormat fillformat = txt.getFill();
fillformat.setFillType(FillFormat.FillType.SOLID);
fillformat.getSolidFill().setColor(Color.getSilver());

// Configure Line Format
LineFormat lineformat = txt.getLine();
lineformat.setWeight(2);
lineformat.setDashStyle(MsoLineDashStyle.SOLID);
```
**คำอธิบาย:** สิ่งนี้เพิ่ม TextBox ที่พิกัดที่กำหนด ปรับลักษณะข้อความและใช้สไตล์การเติมและเส้น

### การบันทึกไฟล์ Excel

**ภาพรวม:** สุดท้ายบันทึกเวิร์กบุ๊กที่แก้ไขกลับเป็นรูปแบบไฟล์ Excel

#### ขั้นตอนที่ 7: นำเข้าคลาส SaveFormat
```java
import com.aspose.cells.SaveFormat;
```

#### ขั้นตอนที่ 8: บันทึกเวิร์กบุ๊ก
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATBoxControl_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
**คำอธิบาย:** เวิร์กบุ๊กจะถูกบันทึกในไดเรกทอรีที่ระบุ คงการเปลี่ยนแปลงที่ทำระหว่างการทำงาน

## การประยุกต์ใช้งานจริง

ต่อไปนี้เป็นสถานการณ์จริงที่การเพิ่ม TextBox ลงในแผนภูมิ Excel สามารถเป็นประโยชน์:

1. **คำอธิบายสำหรับรายงาน:** ใช้ TextBox เพื่อให้บริบทหรือเน้นผลลัพธ์สำคัญโดยตรงบนแผนภูมิ.
2. **คำอธิบายและป้ายกำกับแบบกำหนดเอง:** เพิ่มความเข้าใจด้วยข้อมูลหรือคำอธิบายเพิ่มเติมที่คำอธิบายมาตรฐานอาจไม่ครอบคลุม.
3. **การสร้างแบรนด์:** เพิ่มโลโก้หรือข้อความแบรนด์ของบริษัทภายในแผนภูมิสำหรับการนำเสนอ.

## การพิจารณาประสิทธิภาพ

เมื่อทำงานกับไฟล์ Excel ขนาดใหญ่ ให้พิจารณาข้อแนะนำต่อไปนี้:

- **เพิ่มประสิทธิภาพการใช้ทรัพยากร:** ลดจำนวนการจัดการแผนภูมิและการสร้างออบเจ็กต์เพื่อทำให้ใช้หน่วยความจำน้อยลง.
- **การจัดการหน่วยความจำใน Java:** ตรวจสอบการจัดการออบเจ็กต์ `Workbook` อย่างเหมาะสมโดยปิดหลังการใช้เพื่อปลดปล่อยทรัพยากรทันที.
- **การจัดการข้อมูลอย่างมีประสิทธิภาพ:** โหลดเฉพาะส่วนที่จำเป็นของเวิร์กบุ๊กเมื่อทำงานกับชุดข้อมูลขนาดใหญ่.

## วิธีบันทึกไฟล์ Excel ด้วย Java

ขั้นตอนสุดท้าย—การบันทึกเวิร์กบุ๊ก—แสดงกระบวนการ **save excel file java** โดยการระบุ `SaveFormat` ที่ต้องการ คุณสามารถส่งออกเป็นรูปแบบ `.xls` เก่า, `.xlsx` สมัยใหม่ หรือแม้กระทั่ง CSV ให้คุณควบคุมประเภทไฟล์ที่เหมาะกับกระบวนการต่อไปได้เต็มที่.

## วิธีโหลดเวิร์กบุ๊ก Excel ด้วย Java

การเริ่มต้น `Workbook` ก่อนหน้านี้แสดงรูปแบบ **load excel workbook java** Aspose.Cells แยกความซับซ้อนของการแยกโครงสร้าง Excel แบบไบนารี ทำให้คุณมุ่งเน้นที่ตรรกะธุรกิจแทนรายละเอียดการอ่าน/เขียนไฟล์.

## สรุป

เราได้อธิบายขั้นตอนการเพิ่ม TextBox ลงในแผนภูมิ Excel ด้วย Aspose.Cells for Java คู่มือนี้ครอบคลุมตั้งแต่การตั้งค่าสภาพแวดล้อมและการโหลดไฟล์, การเข้าถึงออบเจ็กต์แผนภูมิ, การปรับแต่ง TextBox, จนถึงการบันทึกเอกสารสุดท้าย.

**ขั้นตอนต่อไป:** ทดลองเพิ่มเติมโดยใช้สไตล์ต่าง ๆ หรือสำรวจประเภทแผนภูมิอื่น ๆ ที่มีใน Aspose.Cells ตรวจสอบเอกสารของพวกเขาที่ [Aspose Reference](https://reference.aspose.com/cells/java/) เพื่อฟังก์ชันขั้นสูงเพิ่มเติม.

## ส่วนคำถามที่พบบ่อย

1. **ฉันสามารถเพิ่ม TextBox หลายอันลงในแผนภูมิได้หรือไม่?**
   - ใช่ คุณสามารถเรียกเมธอด `addTextBoxInChart` ซ้ำตามต้องการด้วยพิกัดที่ต่างกัน.

2. **จะเกิดอะไรขึ้นหากไฟล์ Excel ของฉันไม่มีแผนภูมิ?**
   - การพยายามเข้าถึงแผนภูมิที่ไม่มีจะทำให้เกิดข้อยกเว้น ตรวจสอบว่าเวิร์กบุ๊กของคุณมีอย่างน้อยหนึ่งแผนภูมิก่อนดำเนินการต่อ.

3. **สามารถบันทึกไฟล์ในรูปแบบอื่นนอกจาก .xls ได้หรือไม่?**
   - ได้ คุณสามารถใช้ตัวเลือก `SaveFormat` ต่าง ๆ เช่น `XLSX` ตามความต้องการของคุณ.

4. **ฉันจะจัดการข้อยกเว้นระหว่างการดำเนินการไฟล์อย่างไร?**
   - ใช้บล็อก try‑catch รอบการโหลดและบันทึกไฟล์เพื่อจัดการข้อผิดพลาดอย่างราบรื่น.

5. **Aspose.Cells for Java สามารถใช้กับภาษาโปรแกรมอื่นได้หรือไม่?**
   - แม้ว่าคู่มือนี้มุ่งเน้นที่ Java, Aspose.Cells ยังมีให้สำหรับ .NET, C++ และอื่น ๆ ตรวจสอบ [documentation](https://reference.aspose.com/cells/java/) ของพวกเขาสำหรับคู่มือเฉพาะภาษา.

## คำถามที่พบบ่อย

**Q: การเพิ่ม TextBox มีผลต่อประสิทธิภาพของแผนภูมิหรือไม่?**  
A: ผลกระทบค่อนข้างน้อย; อย่างไรก็ตาม สำหรับเวิร์กบุ๊กขนาดใหญ่มาก ควรจำกัดจำนวนออบเจ็กต์รูปทรงเพื่อรักษาการใช้หน่วยความจำให้ต่ำ.

**Q: ฉันสามารถกำหนดตำแหน่ง TextBox ด้วยการอ้างอิงเซลล์แทนพิกเซลได้หรือไม่?**  
A: ได้ คุณสามารถคำนวณพิกัดพิกเซลจากดัชนีเซลล์หรือใช้เมธอด `addTextBox` บนแผ่นงานสำหรับการกำหนดตำแหน่งตามเซลล์.

**Q: มีวิธีใดที่จะผูกข้อความของ TextBox กับค่าของเซลล์หรือไม่?**  
A: Aspose.Cells ไม่ได้ให้การผูกข้อมูลโดยตรงสำหรับรูปทรง แต่คุณสามารถอัปเดตข้อความของ TextBox อย่างโปรแกรมเมติกหลังจากอ่านค่าจากเซลล์ได้.

**Q: ต้องการไลเซนส์อะไรสำหรับการใช้งานเชิงพาณิชย์?**  
A: ไลเซนส์ Aspose.Cells ที่ซื้อจะลบข้อจำกัดการประเมินทั้งหมดและจำเป็นสำหรับการใช้งานในผลิตภัณฑ์.

**Q: ฉันจะหา ตัวอย่างเพิ่มเติมของการจัดการแผนภูมิได้จากที่ไหน?**  
A: เอกสารอย่างเป็นทางการของ Aspose.Cells และคลังตัวอย่างมีหลายสถานการณ์ รวมถึงซีรีส์แบบไดนามิก, ประเภทแผนภูมิ, และการจัดสไตล์.

## แหล่งข้อมูล

- **เอกสาร:** สำรวจคู่มือที่ครอบคลุมที่ [Aspose Reference](https://reference.aspose.com/cells/java/).
- **ดาวน์โหลด:** เข้าถึงเวอร์ชันไลบรารีล่าสุดจาก [Releases](https://releases.aspose.com/cells/java/).
- **ตัวเลือกการซื้อและทดลอง:** รับไลเซนส์หรือเริ่มทดลองฟรีผ่าน [Purchase Aspose](https://purchase.aspose.com/buy) และ [Free Trial](https://releases.aspose.com/cells/java/).
- **สนับสนุน:** เข้าร่วมชุมชนที่ [Aspose Forum](https://forum.aspose.com/c/cells/9) เพื่อขอความช่วยเหลือ. 

โดยทำตามคู่มือนี้ คุณสามารถผสาน Aspose.Cells เข้ากับโปรเจกต์ Java ของคุณได้อย่างมีประสิทธิภาพเพื่อเพิ่มฟังก์ชันการทำงานของแผนภูมิ Excel ด้วยคำอธิบายข้อความแบบกำหนดเอง ขอให้เขียนโค้ดอย่างสนุก!

---

**อัปเดตล่าสุด:** 2026-04-05  
**ทดสอบด้วย:** Aspose.Cells Java 25.3  
**ผู้เขียน:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}