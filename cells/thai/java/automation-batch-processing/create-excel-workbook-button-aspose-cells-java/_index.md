---
date: '2026-06-02'
description: ค้นพบวิธีใช้ Aspose.Cells for Java เพื่อเพิ่มปุ่มใน Excel workbook –
  step‑by‑step setup, shape creation, and saving the file.
keywords:
- how to use aspose
- add button excel
- create excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-06-02'
  description: Discover how to use Aspose.Cells for Java to add a button to an Excel
    workbook – step‑by‑step setup, shape creation, and saving the file.
  headline: How to Use Aspose.Cells for Java – Add a Button to Excel
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java is a comprehensive API that enables creation, conversion,
      and manipulation of Excel files without Microsoft Office.
    question: What is Aspose.Cells for Java?
  - answer: Yes—Aspose.Cells runs on Windows, Linux, and macOS as long as a compatible
      JDK is installed.
    question: Can I use this on any operating system?
  - answer: There’s no hard‑coded limit; practical limits depend on workbook size
      and memory, but Aspose.Cells can handle thousands of button shapes efficiently.
    question: Is there a limit to the number of buttons I can add?
  - answer: Wrap workbook operations in try‑catch blocks, catching `com.aspose.cells.CellsException`
      to manage file‑related errors gracefully.
    question: How do I handle exceptions when working with Aspose.Cells?
  - answer: Yes—production deployments require a purchased license. A trial license
      is sufficient for development and testing.
    question: Do I need a license for commercial use?
  type: FAQPage
title: วิธีใช้ Aspose.Cells for Java – เพิ่มปุ่มใน Excel
url: /th/java/automation-batch-processing/create-excel-workbook-button-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose.Cells สำหรับ Java – เพิ่มปุ่มใน Excel

## บทนำ
หากคุณต้องการ **how to use Aspose** สำหรับสร้างสเปรดชีตแบบโต้ตอบ คุณมาถูกที่แล้ว บทเรียนนี้จะพาคุณผ่านขั้นตอนการสร้างสมุดงาน Excel พร้อมปุ่มโดยใช้ Aspose.Cells สำหรับ Java ซึ่งเป็นไลบรารีที่ไม่ต้องการ Microsoft Office บนเซิร์ฟเวอร์ คุณจะได้เรียนรู้วิธีตั้งค่า dependency, สร้างออบเจ็กต์หลัก, เพิ่มรูปทรงปุ่มที่คลิกได้, กำหนดลักษณะของมัน, แนบ hyperlink, และสุดท้ายบันทึกสมุดงาน เมื่อเสร็จคุณจะมีรูปแบบที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถฝังลงในเครื่องมือรายงาน, ฟอร์มการป้อนข้อมูล, หรือแดชบอร์ดอัตโนมัติ

**สิ่งที่คุณจะได้เรียนรู้**
- การติดตั้งและการให้ใบอนุญาต Aspose.Cells สำหรับ Java
- การสร้างสมุดงาน Excel ใหม่จากศูนย์
- การเพิ่มรูปทรงปุ่มและการปรับแต่งคำบรรยาย, การวางตำแหน่ง, และฟอนต์
- การเชื่อมโยงปุ่มกับ URL ภายนอก
- การบันทึกสมุดงาน Excel อย่างมีประสิทธิภาพ
- สถานการณ์จริงที่ปุ่มช่วยปรับปรุงกระบวนการทำงาน

ก่อนที่คุณจะเริ่ม โปรดตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณตรงตามข้อกำหนดเบื้องต้นที่ระบุด้านล่าง

## คำตอบสั้น
- **ขั้นตอนแรกคืออะไร?** เพิ่ม Aspose.Cells สำหรับ Java เป็น dependency ของ Maven หรือ Gradle  
- **ฉันจะสร้างปุ่มอย่างไร?** ใช้เมธอด `addShape` บนคอลเลกชัน `Shapes` ของ worksheet พร้อม `ShapeType.BUTTON`  
- **ฉันสามารถตั้งค่า hyperlink ได้หรือไม่?** ได้ — เรียก `setHyperlink` บนรูปทรงปุ่มและระบุ URL  
- **เมธอดใดบันทึกไฟล์?** `workbook.save("MyWorkbook.xlsx", SaveFormat.XLSX)`  
- **ฉันต้องการใบอนุญาตหรือไม่?** ใบอนุญาตทดลองใช้ได้สำหรับการประเมิน; ใบอนุญาตเต็มจำเป็นสำหรับการใช้งานในผลิตภัณฑ์

## Aspose.Cells สำหรับ Java คืออะไร?
**Aspose.Cells for Java** เป็น API ที่มีประสิทธิภาพสูงที่ช่วยให้นักพัฒนาสร้าง, แก้ไข, แปลง, และแสดงผลไฟล์ Excel โดยไม่ต้องติดตั้ง Microsoft Excel รองรับ **50+** รูปแบบการนำเข้าและส่งออก, ประมวลผลสมุดงานหลายร้อยหน้าในโหมดประหยัดหน่วยความจำ, และทำงานบนระบบปฏิบัติการใด ๆ ที่รองรับ Java 8+

## ทำไมต้องใช้ Aspose.Cells เพื่อเพิ่มปุ่มใน Excel?
การเพิ่มปุ่มโดยตรงจาก Java ช่วยขจัดการประมวลผลหลังจากใน Excel, ลดข้อผิดพลาดของมนุษย์, และเปิดใช้งานกระบวนการทำงานอัตโนมัติ Aspose.Cells สามารถแทรกรูปทรงปุ่มได้ถึง **10,000** รูปต่อสมุดงานพร้อมคงขนาดไฟล์ไม่เกิน **5 MB** สำหรับการใช้งานทั่วไป ด้วยการจัดการไบนารีที่ปรับแต่งมาเป็นพิเศษ ความสามารถนี้ทำให้คุณสร้างเทมเพลตแบบโต้ตอบได้ในระดับใหญ่โดยไม่เสียประสิทธิภาพ

## ข้อกำหนดเบื้องต้น
- **Java Development Kit (JDK) 8 หรือสูงกว่า** – เพื่อให้เข้ากันได้กับไลบรารี
- **Maven หรือ Gradle** – สำหรับการจัดการ dependency
- **Aspose.Cells สำหรับ Java** – แนะนำเวอร์ชันล่าสุด (≥ 25.3)
- **ใบอนุญาตที่ถูกต้อง** – ทดลองใช้สำหรับการทดสอบ, ใบอนุญาตเต็มสำหรับการผลิต

## การตั้งค่า Aspose.Cells สำหรับ Java
การรวม Aspose.Cells เข้าในโปรเจกต์ของคุณทำได้ง่าย เลือกเครื่องมือสร้างที่คุณชอบ

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
compile group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

**การรับใบอนุญาต:** Aspose.Cells ใช้โมเดลการให้ใบอนุญาต คุณสามารถรับใบอนุญาตทดลองฟรี, ขอใบอนุญาตชั่วคราวเพื่อการประเมิน, หรือซื้อใบอนุญาตเต็มสำหรับการใช้งานในผลิตภัณฑ์ เยี่ยมชม [เว็บไซต์ Aspose](https://purchase.aspose.com/buy) เพื่อดูข้อมูลเพิ่มเติม

## วิธีใช้ Aspose.Cells เพื่อเพิ่มปุ่มใน Excel

โหลดไฟล์ PDF ของคุณด้วย `new Document("file.pdf")` แล้วเรียก `doc.Save("output.docx", SaveFormat.DocX)` — นั่นคือการแปลงครบถ้วนในสองบรรทัด Aspose.Cells สำหรับ Java มี API ที่ไหลลื่นทำให้คุณสร้างสมุดงาน, เพิ่มปุ่ม, และบันทึก — ทั้งหมดโดยไม่ต้องเปิด Excel

### การสร้างสมุดงาน Excel ใหม่
คลาส `Workbook` เป็นออบเจ็กต์ระดับบนของ Aspose.Cells ที่แทนไฟล์ Excel หนึ่งไฟล์ในหน่วยความจำ การสร้างอินสแตนซ์ให้คุณมีผืนผ้าเปล่าสำหรับเพิ่มชีต, ข้อมูล, และรูปทรง

```java
import com.aspose.cells.Workbook;
// Initialize a new workbook
Workbook workbook = new Workbook();
```

### การเข้าถึง Worksheet แรก
สมุดงานใหม่ทุกไฟล์จะมีอย่างน้อยหนึ่ง worksheet ชื่อ “Sheet1” คอลเลกชัน `Worksheets` ให้คุณดึงมันโดยใช้ดัชนีหรือชื่อ

```java
import com.aspose.cells.Workbook;
// Create a new instance of Workbook, representing an Excel file
Workbook workbook = new Workbook();
```

### การเพิ่มรูปทรงปุ่ม
คลาส `Shape` แทนวัตถุที่วาดได้บน worksheet รวมถึงปุ่ม ใช้เมธอด `addShape` พร้อม `ShapeType.BUTTON` เพื่อแทรกคอนโทรลที่คลิกได้  
`addShape` จะเพิ่มรูปทรงใหม่ลงในคอลเลกชัน Shapes ของ worksheet

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.Worksheets;
// Get the collection of worksheets and access the first one
Worksheet sheet = workbook.getWorksheets().get(0);
```

### การตั้งค่าคุณสมบัติปุ่ม
คุณสามารถปรับแต่งคำบรรยาย, การวางตำแหน่ง, และฟอนต์ของปุ่มให้สอดคล้องกับแนวทาง UI ของคุณ เมธอด `setText`, `setPlacement`, และ `getFont` เปิดให้เข้าถึงตัวเลือกเหล่านี้

```java
import com.aspose.cells.Button;
import com.aspose.cells.MsoDrawingType;
// Add a button shape to the worksheet
Button button = (Button) sheet.getShapes().addShape(
    MsoDrawingType.BUTTON, 2, 2, 2, 0, 20, 80);
```

### การเพิ่ม Hyperlink ให้กับปุ่ม
เมื่อคุณแนบ hyperlink ปุ่มจะกลายเป็นแบบโต้ตอบ เมธอด `setHyperlink` รับออบเจ็กต์ `Hyperlink` ที่ชี้ไปยังที่อยู่เว็บใด ๆ หรือตำแหน่งภายในสมุดงาน

```java
import com.aspose.cells.Color;
import com.aspose.cells.PlacementType;
// Set the caption of the button.
button.setPlacement(PlacementType.FREE_FLOATING); // Determine how the button is attached to cells.
button.getFont().setName("Tahoma"); // Define font name.
button.getFont().setBold(true); // Make text bold.
button.getFont().setColor(Color.getBlue()); // Change font color to blue.
```

### การบันทึกสมุดงาน
บันทึกการเปลี่ยนแปลงโดยเรียก `save` พร้อมรูปแบบที่ต้องการ `save` จะเขียนสมุดงานลงไฟล์ในรูปแบบที่ระบุ  
Aspose.Cells รองรับ **XLSX**, **XLS**, **CSV**, **PDF**, และรูปแบบอื่น ๆ อีกมากมาย

```java
// Add hyperlink to the button
button.addHyperlink("http://www.aspose.com/");
```

## การประยุกต์ใช้งานจริง
- **รายงานอัตโนมัติ:** แนบปุ่ม “Refresh Data” ที่ทำงานคล้ายแมโครเมื่อผู้ใช้คลิก  
- **การส่งฟอร์ม:** ฝังปุ่ม “Submit” ที่เปิด URL ฟอร์มเว็บ ช่วยเร่งกระบวนการเก็บข้อมูล  
- **แดชบอร์ดโต้ตอบ:** วางปุ่มนำทางที่กระโดดไปยังส่วนต่าง ๆ ของ worksheet เพื่อเพิ่มประสบการณ์ผู้ใช้สำหรับนักวิเคราะห์ธุรกิจ

## พิจารณาด้านประสิทธิภาพ
เพื่อให้แอปพลิเคชันของคุณตอบสนองได้ดีเมื่อจัดการสมุดงานขนาดใหญ่ ให้ปฏิบัติตามแนวทางต่อไปนี้:
- **การจัดการหน่วยความจำ:** ปล่อยออบเจ็กต์ขนาดใหญ่ (`Workbook`, `Worksheet`) โดยตั้งค่าเป็น `null` หลังบันทึก  
- **การประมวลผลเป็นชุด:** ประมวลผลหลายไฟล์ใน thread pool เดียวเพื่อ ลดภาระ JVM  
- **การใช้คุณลักษณะเลือก:** ใช้ `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` เพื่อลดการใช้หน่วยความจำเมื่อเพียงแค่เพิ่มรูปทรง

## ปัญหาทั่วไปและวิธีแก้
- **ปุ่มไม่ปรากฏ:** ตรวจสอบให้แน่ใจว่าการวางตำแหน่งของปุ่มตั้งเป็น `PlacementType.FREE_FLOATING`  
- **Hyperlink ไม่ทำงาน:** ยืนยันว่า URL มีโปรโตคอล (`http://` หรือ `https://`)  
- **License Exception:** หากพบข้อผิดพลาดเกี่ยวกับใบอนุญาต ตรวจสอบว่าไฟล์ใบอนุญาตถูกโหลดก่อนเรียกใช้ Aspose.Cells ใด ๆ

## คำถามที่พบบ่อย

**Q: Aspose.Cells สำหรับ Java คืออะไร?**  
A: Aspose.Cells สำหรับ Java เป็น API ครบวงจรที่ช่วยสร้าง, แปลง, และจัดการไฟล์ Excel โดยไม่ต้องใช้ Microsoft Office

**Q: ฉันสามารถใช้บนระบบปฏิบัติการใดก็ได้หรือไม่?**  
A: ใช่ — Aspose.Cells ทำงานบน Windows, Linux, และ macOS ตราบใดที่ติดตั้ง JDK ที่รองรับ

**Q: มีขีดจำกัดจำนวนปุ่มที่สามารถเพิ่มได้หรือไม่?**  
A: ไม่มีขีดจำกัดที่กำหนดไว้ในโค้ด; ขีดจำกัดจริงขึ้นอยู่กับขนาดสมุดงานและหน่วยความจำ แต่ Aspose.Cells สามารถจัดการรูปทรงปุ่มหลายพันได้อย่างมีประสิทธิภาพ

**Q: ฉันจะจัดการกับข้อยกเว้นเมื่อทำงานกับ Aspose.Cells อย่างไร?**  
A: ห่อการดำเนินการของสมุดงานในบล็อก try‑catch และจับ `com.aspose.cells.CellsException` เพื่อจัดการข้อผิดพลาดที่เกี่ยวกับไฟล์อย่างเหมาะสม

**Q: ฉันต้องมีใบอนุญาตสำหรับการใช้งานเชิงพาณิชย์หรือไม่?**  
A: ใช่ — การใช้งานในสภาพแวดล้อมการผลิตต้องมีใบอนุญาตที่ซื้อแล้ว ใบอนุญาตทดลองใช้เพียงพอสำหรับการพัฒนาและทดสอบ

## แหล่งข้อมูล
- [เอกสาร](https://reference.aspose.com/cells/java/)
- [ดาวน์โหลด](https://releases.aspose.com/cells/java/)
- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- [ทดลองใช้ฟรี](https://releases.aspose.com/cells/java/)
- [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน](https://forum.aspose.com/c/cells/9)

Feel free to explore these resources for additional guidance, sample projects, and community support. Happy coding!

---

**อัปเดตล่าสุด:** 2026-06-02  
**ทดสอบกับ:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

```java
import com.aspose.cells.SaveFormat;
// Define output path and save the workbook
String dataDir = "YOUR_DATA_DIRECTORY"; // Replace with actual directory path.
workbook.save(dataDir + "/AddingButtonControl_out.xls", SaveFormat.AUTO);
```

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง

- [วิธีสร้างสมุดงาน Excel ด้วย Aspose.Cells สำหรับ Java - การเพิ่มรูปทรงป้าย](/cells/java/automation-batch-processing/aspose-cells-java-excel-label-shape-automation/)
- [สร้างสมุดงาน Excel ด้วย Aspose.Cells ใน Java: คู่มือขั้นตอน](/cells/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [วิธีเพิ่ม Checkbox ใน Excel ด้วย Aspose.Cells สำหรับ Java: คู่มือขั้นตอน](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}