---
date: '2026-10-28'
description: เรียนรู้วิธีวางค่าโดยใช้ตัวเลือกคัดลอกและวางของ Aspose.Cells ใน Java
  พร้อมโค้ดขั้นตอนต่อขั้นตอน การตั้งค่า Maven dependency และเคล็ดลับการใช้งานลิขสิทธิ์
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: เรียนรู้วิธีวางค่าโดยใช้ตัวเลือกคัดลอกและวางของ Aspose.Cells ใน Java
  พร้อมโค้ดขั้นตอนต่อขั้นตอน การตั้งค่า Maven dependency และเคล็ดลับการใช้งานลิขสิทธิ์
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: วิธีวางค่าโดยใช้ตัวเลือกคัดลอกและวางของ Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: วิธีวางค่าโดยใช้ตัวเลือกคัดลอกและวางของ Aspose.Cells
url: /th/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีวางค่าโดยใช้ตัวเลือกคัดลอกและวางของ Aspose.Cells

การทำงานอัตโนมัติของการรายงาน Excel ด้วย Java หมายความว่าคุณสามารถสร้าง รวม และจัดรูปแบบเวิร์กบุ๊กได้โดยไม่ต้องเปิด Excel ด้วยตนเอง ด้วย **Aspose.Cells** คุณจะได้การควบคุมเต็มรูปแบบเหนือสูตร แถวที่ซ่อนอยู่ และค่าของเซลล์ ทำให้รายงานของคุณแม่นยำและเบา ในบทแนะนำนี้คุณจะได้เรียนรู้วิธีใช้ **CopyOptions.ReferToDestinationSheet** เพื่อให้สูตรถูกต้องและ **PasteOptions** เพื่อวางเฉพาะค่าที่มองเห็นได้ที่คุณต้องการ

## คำตอบสั้น ๆ
- **`CopyOptions.ReferToDestinationSheet` ทำอะไร?** มันจะเขียนสูตรใหม่ให้ชี้ไปยังแผ่นงานปลายทางหลังจากการคัดลอก  
- **ฉันจะวางเฉพาะเซลล์ที่มองเห็นได้อย่างไร?** เรียก `PasteOptions.setOnlyVisibleCells(true)` พร้อมกับ `PasteType.VALUES`  
- **ต้องใช้เวอร์ชันไลบรารีใด?** Aspose.Cells 25.3 หรือใหม่กว่า  
- **ต้องมีลิขสิทธิ์สำหรับการใช้งานจริงหรือไม่?** ใช่ – ลิขสิทธิ์ถาวรหรือชั่วคราวจะลบข้อจำกัดการประเมินผล  
- **สามารถใช้ Maven หรือ Gradle ได้หรือไม่?** ทั้งสองสนับสนุน; ดูตัวอย่างการกำหนดค่าในส่วนด้านล่าง

## “การทำงานอัตโนมัติของการรายงาน Excel” คืออะไร?
การทำงานอัตโนมัติของการรายงาน Excel หมายถึงการสร้างและอัปเดตเวิร์กบุ๊ก Excel อย่างโปรแกรมเมติก ทำให้คุณสามารถสร้าง ผสาน และจัดรูปแบบรายงานได้โดยไม่ต้องคัดลอก‑วางด้วยมือ ซึ่งช่วยลดข้อผิดพลาดและประหยัดเวลาหลายชั่วโมงของงานซ้ำ ๆ วิธีนี้เหมาะสำหรับงานแบตช์ที่กำหนดเวลา, แดชบอร์ดที่ขับเคลื่อนด้วยข้อมูล, และกระบวนการรวมการเงิน

## ทำไมต้องใช้ CopyOptions และ PasteOptions สำหรับการรายงาน?
สองคลาสนี้ช่วยให้คุณคงการอ้างอิงสูตรไว้ครบถ้วนขณะคัดลอกข้อมูล **และ** ดึงเฉพาะเซลล์ที่มองเห็นได้หลังจากกรองหรือซ่อนแถว การใช้ร่วมกันช่วยลดปริมาณข้อมูลที่ถ่ายโอนได้สูงสุดถึง 80 % ในสถานการณ์ตารางที่กรองบ่อย และทำให้สูตรคำนวณได้อย่างถูกต้องในแผ่นงานปลายทาง

## ข้อกำหนดเบื้องต้น
- Java 8 หรือสูงกว่า  
- Maven หรือ Gradle สำหรับการจัดการการพึ่งพา  
- Aspose.Cells 25.3+ (รุ่นทดลอง, ชั่วคราว, หรือถาวร)

## การตั้งค่า Aspose.Cells สำหรับ Java

เพิ่มไลบรารีลงในโปรเจกต์ของคุณด้วยวิธีใดวิธีหนึ่งต่อไปนี้:

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

### การรับลิขสิทธิ์
- **ทดลองฟรี** – ชุดฟีเจอร์เต็มสำหรับการประเมินผล  
- **ลิขสิทธิ์ชั่วคราว** – ลบข้อจำกัดการทดลองขณะทดสอบ  
- **ลิขสิทธิ์ถาวร** – แนะนำสำหรับการใช้งานในสภาพแวดล้อมการผลิต

เริ่มต้น Aspose.Cells ในโค้ด Java ของคุณ:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## คำแนะนำแบบทีละขั้นตอน

### 1. copyOptions กับ referToDestinationSheet

#### ภาพรวม
`CopyOptions` คืออ็อบเจ็กต์การกำหนดค่าของ Aspose.Cells ที่ควบคุมวิธีการจัดการสูตรและการอ้างอิงเซลล์ระหว่างการคัดลอก การตั้งค่า `CopyOptions.ReferToDestinationSheet` เป็น `true` จะเขียนสูตรใหม่ให้ชี้ไปยังแผ่นงานใหม่หลังจากการคัดลอก

#### ขั้นตอนที่ 1: เริ่มต้น workbook และ worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### ขั้นตอนที่ 2: กำหนดค่า copyOptions  
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
*ทำไมจึงสำคัญ*: สูตรที่เคยอ้างอิง `Sheet1` จะอ้างอิง `DestSheet` อย่างถูกต้อง ทำให้รายงานอัตโนมัติของคุณเชื่อถือได้

**เคล็ดลับการแก้ปัญหา**: หากสูตรยังอ้างอิงแผ่นงานเก่า ให้ตรวจสอบว่าได้เรียก `setReferToDestinationSheet(true)` **ก่อน** การคัดลอกหรือไม่

### 2. pasteOptions สำหรับค่าที่มองเห็นได้เท่านั้นจากเซลล์ที่มองเห็น

#### ภาพรวม
`PasteOptions` คืออ็อบเจ็กต์การตั้งค่าของ Aspose.Cells ที่กำหนดว่าจะวางอะไร การใช้ `PasteType.VALUES` ร่วมกับ `onlyVisibleCells=true` จะคัดลอกเฉพาะค่าที่แสดงผลเท่านั้น ไม่รวมแถว/คอลัมน์ที่ซ่อนและรูปแบบ

#### ขั้นตอนที่ 1: เริ่มต้น workbook และ worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### ขั้นตอนที่ 2: กำหนดค่า pasteOptions  
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
*ทำไมจึงสำคัญ*: เหมาะสำหรับการสกัดข้อมูลที่กรองหรือสร้างรายงานที่สะอาดโดยไม่มีแถวหรือรูปแบบที่ซ่อนอยู่

**เคล็ดลับการแก้ปัญหา**: ตรวจสอบว่าแถว/คอลัมน์ถูกซ่อนจริงใน Excel ก่อนคัดลอก; หากไม่ซ่อนจะถูกรวมอยู่ด้วย

## การประยุกต์ใช้ในเชิงปฏิบัติ
1. **การรวมการเงิน** – ผสานแผ่นงานรายเดือนเป็นเวิร์กบุ๊กหลักพร้อมคงสูตรทั้งหมดให้แม่นยำ  
2. **การส่งออกข้อมูลที่กรอง** – ดึงเฉพาะแถวที่มองเห็นจากตารางที่กรองไปยังแผ่นสรุป  
3. **การสร้างรายงานตามกำหนดเวลา** – ทำงานอัตโนมัติสร้างรายงาน Excel ทุกคืนด้วยค่าที่แม่นยำและการอ้างอิงที่ถูกต้อง

## พิจารณาด้านประสิทธิภาพ
- **ทำลาย workbook** เมื่อเสร็จ (`wb.dispose();`) เพื่อปล่อยทรัพยากรเนทีฟ  
- **การทำงานเป็นชุด** – รวมหลายคำสั่งคัดลอก/วางเพื่อ ลดค่าโอเวอร์เฮด  
- **ตรวจสอบหน่วยความจำ** – เวิร์กบุ๊กขนาดใหญ่อาจต้องเพิ่ม heap (`-Xmx2g`)  
- Aspose.Cells รองรับ **รูปแบบไฟล์เข้าและออกกว่า 50 แบบ** และสามารถประมวลผลเวิร์กบุ๊กที่มี **สูงสุด 2 ล้านแถว** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ให้ประสิทธิภาพสูงสำหรับงานระดับองค์กร

## คำถามที่พบบ่อย

**Q: `CopyOptions.ReferToDestinationSheet` ใช้ทำอะไร?**  
A: มันเขียนสูตรใหม่ให้ชี้ไปยังแผ่นงานปลายทางหลังจากการคัดลอก เพื่อให้สูตรรายงานยังคงถูกต้อง

**Q: ฉันจะวางเฉพาะเซลล์ที่มองเห็นได้อย่างไร?**  
A: ตั้งค่า `PasteOptions.setOnlyVisibleCells(true)` แล้วเลือก `PasteType.VALUES`

**Q: สามารถใช้ Aspose.Cells ได้โดยไม่ซื้อไลเซนส์หรือไม่?**  
A: ใช่, มีรุ่นทดลองหรือไลเซนส์ชั่วคราวสำหรับการประเมินผล แต่ต้องมีไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต

**Q: ทำไมบางการอ้างอิงยังผิดพลาดหลังการคัดลอก?**  
A: ตรวจสอบให้แน่ใจว่าเปิดใช้งาน `ReferToDestinationSheet` **ก่อน** การคัดลอกและสูตรต้นทางไม่มีลิงก์ไปยังเวิร์กบุ๊กภายนอก

**Q: ควรปฏิบัติตามแนวทางการจัดการหน่วยความจำอย่างไร?**  
A: ทำลายอ็อบเจ็กต์ `Workbook` เมื่อเสร็จ, แบ่งการประมวลผลไฟล์ขนาดใหญ่เป็นชิ้นส่วน, และตรวจสอบการใช้ heap ของ JVM

**Q: สามารถรวม CopyOptions และ PasteOptions ในการดำเนินการเดียวได้หรือไม่?**  
A: ได้, คุณสามารถทำตามลำดับโดยคัดลอกด้วย `CopyOptions` แล้วใช้ `PasteOptions` กับช่วงเป้าหมาย

## แหล่งข้อมูล
- **เอกสาร**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **ดาวน์โหลด**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **ซื้อ**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **ทดลองฟรี**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **ไลเซนส์ชั่วคราว**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **ฟอรั่มสนับสนุน**: [Aspose support](https://forum.aspose.com/c/cells)

---

**อัปเดตล่าสุด:** 2026-10-28  
**ทดสอบกับ:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}