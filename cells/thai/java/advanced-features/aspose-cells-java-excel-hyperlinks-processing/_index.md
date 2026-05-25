---
date: '2026-02-24'
description: เรียนรู้วิธีดึงไฮเปอร์ลิงก์จาก Excel ด้วย Aspose.Cells สำหรับ Java รวมถึงการโหลดเวิร์กบุ๊ก
  การอ่านไฮเปอร์ลิงก์ใน Excel และการประมวลผลไฟล์ Excel เป็นชุด.
keywords:
- Aspose.Cells Java
- Excel Hyperlink Management
- Aspose.Cells for Java setup
title: ดึงไฮเปอร์ลิงก์จาก Excel – การโหลดเวิร์กบุ๊ก Aspose Cells
url: /th/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ดึงลิงก์ไฮเปอร์ลิงก์จาก Excel – การจัดการลิงก์ไฮเปอร์ลิงก์ขั้นสูงใน Excel

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน การ **ดึงลิงก์ไฮเปอร์ลิงก์จาก Excel** อย่างรวดเร็วและเชื่อถือได้เป็นความต้องการหลักสำหรับผู้ที่ทำอัตโนมัติการรายงานด้วย Excel ไม่ว่าคุณจะสร้างแดชบอร์ดการเงิน เครื่องมือการย้ายข้อมูล หรือบริการสร้างเอกสาร การจัดการเวิร์กบุ๊กที่เต็มไปด้วยไฮเปอร์ลิงก์อาจเป็นความท้าทายทั่วไป ในบทเรียนนี้คุณจะได้เรียนรู้วิธีโหลดเวิร์กบุ๊ก Excel, เข้าถึงแผ่นงานของมัน, และ **ดึงไฮเปอร์ลิงก์จาก Excel** ด้วย Aspose.Cells for Java เมื่อเสร็จแล้วคุณจะพร้อมผสานการประมวลผลไฮเปอร์ลิงก์เข้าไปในแอปพลิเคชันของคุณเองและแม้กระทั่ง **ประมวลผลไฟล์ Excel เป็นชุด** สำหรับสถานการณ์ขนาดใหญ่

## คำตอบสั้น
- **คลาสหลักที่ใช้เปิดเวิร์กบุ๊กคืออะไร?** `Workbook`
- **เมธอดใดที่คืนค่าทุกไฮเปอร์ลิงก์ในช่วง?** `Range.getHyperlinks()`
- **ต้องการไลเซนส์สำหรับการดึงไฮเปอร์ลิงก์พื้นฐานหรือไม่?** ทดลองใช้ฟรีได้ แต่ไลเซนส์จะลบข้อจำกัดการประเมินผล
- **สามารถประมวลผลไฟล์ขนาดใหญ่ได้อย่างมีประสิทธิภาพหรือไม่?** ใช่ — มุ่งเน้นที่แผ่นงานหรือช่วงที่ต้องการเท่านั้น
- **เวอร์ชัน Java ที่รองรับคืออะไร?** Java 8 และใหม่กว่า

## “ดึงไฮเปอร์ลิงก์จาก Excel” คืออะไร?
การดึงไฮเปอร์ลิงก์จาก Excel หมายถึงการอ่านข้อมูลลิงก์ที่เก็บไว้ในเซลล์ เช่น URL, เส้นทางไฟล์, ที่อยู่อีเมล, หรือการอ้างอิงเซลล์ภายใน Aspose.Cells มี API ที่ง่ายต่อการนับรายการลิงก์เหล่านี้โดยไม่ต้องเปิด Excel

## ทำไมต้องดึงไฮเปอร์ลิงก์จาก Excel?
ไฮเปอร์ลิงก์มักชี้ไปยังแหล่งข้อมูลภายนอก, เอกสาร, หรือการอ้างอิงภายใน การดึงข้อมูลเหล่านี้ทำให้คุณสามารถ:
- ตรวจสอบสุขภาพของลิงก์โดยอัตโนมัติ
- ย้ายหรือเขียนทับ URL ระหว่างการย้ายข้อมูล
- สร้างรายงานสรุปของทรัพยากรที่เชื่อมโยงทั้งหมด
- สร้างดัชนีที่ค้นหาได้สำหรับการบูรณาการฐานความรู้

## ข้อกำหนดเบื้องต้น

- ไลบรารี **Aspose.Cells for Java** (เวอร์ชัน 25.3 หรือใหม่กว่า)
- Java 8 + และ IDE (IntelliJ IDEA, Eclipse, ฯลฯ)
- Maven หรือ Gradle สำหรับการจัดการ dependencies
- ไลเซนส์ Aspose.Cells ที่ถูกต้อง (ไม่บังคับสำหรับรุ่นทดลอง)

### การตั้งค่า Aspose.Cells for Java

เพิ่มไลบรารีลงในโปรเจกต์ของคุณด้วย Maven หรือ Gradle

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **เคล็ดลับ:** รักษาเวอร์ชันของไลบรารีให้เป็นปัจจุบันเพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพและคุณสมบัติการจัดการไฮเปอร์ลิงก์ใหม่

#### การเริ่มต้นพื้นฐาน

เมื่อ dependencies พร้อมแล้ว สร้างคลาส Java ง่าย ๆ เพื่อตรวจสอบว่าเวิร์กบุ๊กสามารถโหลดได้หรือไม่

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

### การดำเนินการแบบขั้นตอน

ด้านล่างนี้เราจะพาคุณผ่านสามคุณลักษณะหลัก: โหลดเวิร์กบุ๊ก, เข้าถึงแผ่นงานและช่วง, และสุดท้ายดึงและประมวลผลไฮเปอร์ลิงก์

## วิธีดึงไฮเปอร์ลิงก์จาก Excel – การโหลดเวิร์กบุ๊ก

### โหลดเวิร์กบุ๊ก (คุณลักษณะ 1)

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## วิธีดึงไฮเปอร์ลิงก์จาก Excel – การเข้าถึงแผ่นงานและช่วง

### เข้าถึงแผ่นงานและช่วง (คุณลักษณะ 2)

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## วิธีดึงไฮเปอร์ลิงก์จาก Excel – การดึงและประมวลผลไฮเปอร์ลิงก์

### ดึงและประมวลผลไฮเปอร์ลิงก์ (คุณลักษณะ 3)

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

### การประยุกต์ใช้งานจริง

| กรณีการใช้ | ประโยชน์ |
|------------|----------|
| **การตรวจสอบข้อมูล** | ตรวจสอบโดยอัตโนมัติว่าทุกไฮเปอร์ลิงก์ชี้ไปยัง URL ที่เข้าถึงได้ก่อนเผยแพร่รายงาน |
| **อัตโนมัติ** | ดึงลิงก์ระหว่างการย้ายไปยังคลังข้อมูลใหม่, ปรับปรุงการอ้างอิงแบบเรียลไทม์ |
| **การรายงาน** | สร้างแผ่นสรุปที่แสดงรายการทรัพยากรภายนอกทั้งหมดที่อ้างอิงในเวิร์กบุ๊ก |

### พิจารณาด้านประสิทธิภาพ

- **ประมวลผลเฉพาะช่วงที่ต้องการ** — จำกัดขอบเขตช่วยลดการใช้หน่วยความจำ
- **ทำลายออบเจ็กต์** — ตั้งค่า `workbook = null;` หลังการใช้งานและให้ Garbage Collector ของ JVM ทำงานคืนหน่วยความจำ
- **การประมวลผลเป็นชุด** — เมื่อจัดการหลายไฟล์ ให้ใช้อินสแตนซ์ `Workbook` เดียวซ้ำได้เมื่อเป็นไปได้ ซึ่งช่วยให้คุณ **ประมวลผลไฟล์ Excel เป็นชุด** อย่างมีประสิทธิภาพ

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | วิธีแก้ |
|-------|--------|
| **`range` เป็น Null** | ตรวจสอบให้แน่ใจว่าช่วงถูกสร้างก่อนเรียก `getHyperlinks()` |
| **ไม่มีไลเซนส์** | รุ่นทดลองใช้ได้สำหรับการพัฒนา แต่ไลเซนส์เต็มจะลบข้อจำกัดการประเมินผลและเพิ่มประสิทธิภาพ |
| **ประเภทไฮเปอร์ลิงก์ที่ไม่รองรับ** | ใช้ค่าคงที่ `TargetModeType` เพื่อจัดการประเภทใหม่เมื่อ Aspose ปล่อยอัปเดต |

## คำถามที่พบบ่อย

**ถาม: เวอร์ชัน Java ใดที่เข้ากันได้กับ Aspose.Cells?**  
ตอบ: Aspose.Cells for Java รองรับ Java 8 และใหม่กว่า ตรวจสอบให้แน่ใจว่า JDK ของคุณตรงตามข้อกำหนดนี้

**ถาม: สามารถดึงไฮเปอร์ลิงก์จากไฟล์ Excel ขนาดใหญ่มากโดยไม่หมดหน่วยความจำได้หรือไม่?**  
ตอบ: ใช่ โหลดเฉพาะแผ่นงานหรือช่วงที่ต้องการและหลีกเลี่ยงการโหลดเวิร์กบุ๊กทั้งหมดเมื่อเป็นไปได้

**ถาม: จำเป็นต้องมีไลเซนส์สำหรับการดึงไฮเปอร์ลิงก์ในสภาพแวดล้อมการผลิตหรือไม่?**  
ตอบ: รุ่นทดลองให้คุณทดลองใช้ได้ แต่ไลเซนส์เชิงพาณิชย์จะลบข้อจำกัดการประเมินผลและให้การสนับสนุนเต็มรูปแบบ

**ถาม: จะจัดการกับไฮเปอร์ลิงก์ที่ชี้ไปยังที่อยู่อีเมลอย่างไร?**  
ตอบ: ค่าคงที่ `TargetModeType.EMAIL` ระบุลิงก์อีเมล; คุณสามารถประมวลผลแยกต่างหากได้ตามต้องการ

**ถาม: Aspose.Cells รักษาการจัดรูปแบบของไฮเปอร์ลิงก์เมื่อบันทึกหรือไม่?**  
ตอบ: แน่นอน คุณสมบัติของไฮเปอร์ลิงก์ทั้งหมด (ข้อความแสดง, tooltip, ที่อยู่) จะคงอยู่เมื่อบันทึกเวิร์กบุ๊ก

**ถาม: สามารถใช้ Aspose.Cells เพื่อ **อ่านไฮเปอร์ลิงก์จาก Excel** ในงานแบบแบตช์ได้หรือไม่?**  
ตอบ: ใช่ — ผสาน API กับลูปที่วนไฟล์เพื่ออ่านไฮเปอร์ลิงก์จากหลายเวิร์กบุ๊ก

**ถาม: วิธีที่ดีที่สุดในการ **โหลดเวิร์กบุ๊ก Excel ด้วย Java** สำหรับสถานการณ์ที่ต้องการประมวลผลสูงคืออะไร?**  
ตอบ: ใช้อินสแตนซ์ `Workbook` เดียวซ้ำได้เมื่อเป็นไปได้และปิดสตรีมอย่างรวดเร็วเพื่อคืนทรัพยากร

---

**อัปเดตล่าสุด:** 2026-02-24  
**ทดสอบด้วย:** Aspose.Cells 25.3 for Java  
**ผู้เขียน:** Aspose  

หากคุณมีคำถามเพิ่มเติม โปรดเยี่ยมชม [ฟอรั่มสนับสนุนของ Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}