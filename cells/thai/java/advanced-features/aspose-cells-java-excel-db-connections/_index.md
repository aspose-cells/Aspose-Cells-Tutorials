---
date: '2025-12-16'
description: เรียนรู้วิธีจัดการการเชื่อมต่อฐานข้อมูล Excel ด้วย Aspose.Cells สำหรับ
  Java, แสดงรายการการเชื่อมต่อข้อมูล Excel, และรับรายละเอียดการเชื่อมต่อฐานข้อมูลอย่างมีประสิทธิภาพ.
keywords:
- Aspose.Cells Java
- manage Excel DB connections
- list Excel data connections
- get DB connection details
- load workbook Aspose Cells
title: จัดการการเชื่อมต่อฐานข้อมูล Excel ด้วย Aspose.Cells สำหรับ Java
url: /th/java/advanced-features/aspose-cells-java-excel-db-connections/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# จัดการการเชื่อมต่อ Excel DB ด้วย Aspose.Cells สำหรับ Java

ในแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน **การจัดการการเชื่อมต่อ excel db** เป็นทักษะสำคัญสำหรับผู้ที่ทำงานกับการอัตโนมัติของ Excel คู่มือนี้จะพาคุณผ่านการใช้ Aspose.Cells สำหรับ Java เพื่อ **แสดงรายการการเชื่อมต่อข้อมูล Excel**, ดึง **รายละเอียดการเชื่อมต่อ DB**, และโหลดอ็อบเจกต์ **workbook Aspose Cells** อย่างมีประสิทธิภาพ เมื่อเสร็จแล้วคุณจะสามารถตรวจสอบ, แก้ไข, และแก้ปัญหาการเชื่อมต่อฐานข้อมูลภายนอกที่ฝังอยู่ในไฟล์ Excel ใด ๆ ได้

## คำตอบสั้น ๆ
- **ไลบรารีที่จัดการการเชื่อมต่อ Excel DB คืออะไร?** Aspose.Cells สำหรับ Java.  
- **ฉันจะลิสต์การเชื่อมต่อข้อมูลทั้งหมดได้อย่างไร?** ใช้ `Workbook.getDataConnections()`.  
- **ฉันสามารถดึงพารามิเตอร์การเชื่อมต่อได้หรือไม่?** ได้, ผ่าน `DBConnection.getParameters()`.  
- **ต้องใช้ไลเซนส์หรือไม่?** จำเป็นต้องมีไลเซนส์ชั่วคราวหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **Maven รองรับหรือไม่?** แน่นอน – เพิ่ม dependency ของ Aspose.Cells ลงใน `pom.xml`.

## “การจัดการการเชื่อมต่อ excel db” คืออะไร?
การจัดการการเชื่อมต่อ Excel DB หมายถึงการเข้าถึง, นับจำนวน, และควบคุมแหล่งข้อมูลภายนอก (เช่นฐานข้อมูล SQL) ที่ workbook ของ Excel ใช้โดยโปรแกรม การทำเช่นนี้ช่วยให้สามารถสร้างรายงานอัตโนมัติ, ตรวจสอบความถูกต้องของข้อมูล, และอัปเดตแดชบอร์ดแบบไดนามิกโดยไม่ต้องมีการแทรกแซงของผู้ใช้

## ทำไมต้องใช้ Aspose.Cells สำหรับ Java?
Aspose.Cells ให้ API แบบ Java แท้ที่ทำงานได้โดยไม่ต้องติดตั้ง Microsoft Office มันให้คุณควบคุมอ็อบเจกต์ workbook ได้เต็มที่, รองรับคุณลักษณะของ Excel มากมาย, และช่วยให้คุณจัดการการเชื่อมต่อภายนอกได้อย่างปลอดภัยและมีประสิทธิภาพ

## ข้อกำหนดเบื้องต้น
1. **ไลบรารีที่ต้องการ:** Aspose.Cells สำหรับ Java (เวอร์ชันล่าสุด).  
2. **เครื่องมือสร้าง:** Maven หรือ Gradle.  
3. **ความรู้พื้นฐาน:** การเขียนโปรแกรม Java เบื้องต้นและความคุ้นเคยกับการเชื่อมต่อข้อมูลของ Excel.

## การตั้งค่า Aspose.Cells สำหรับ Java
เพื่อจัดการการเชื่อมต่อ Excel DB ให้เพิ่ม Aspose.Cells ลงในโปรเจกต์ของคุณ

### การตั้งค่า Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### การตั้งค่า Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

หลังจากเพิ่ม dependency แล้ว ให้รับไลเซนส์จาก [official site](https://purchase.aspose.com/temporary-license/). ไลเซนส์นี้จะเปิดใช้งานคุณสมบัติเต็มรูปแบบสำหรับการทดลองและการใช้งานในสภาพแวดล้อมการผลิต

### การเริ่มต้นพื้นฐาน
```java
import com.aspose.cells.Workbook;

public class ExcelDbConnections {
    public static void main(String[] args) throws Exception {
        // Initialize a Workbook object with the path to an Excel file containing external connections.
        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/sampleRetrievingSQLConnectionData.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## คู่มือการดำเนินการ
ต่อไปนี้เป็นขั้นตอนที่จำเป็นสำหรับการ **แสดงรายการการเชื่อมต่อข้อมูล excel** และ **ดึงรายละเอียดการเชื่อมต่อ db**

### โหลด Workbook และเข้าถึงการเชื่อมต่อภายนอก
**ภาพรวม:** โหลด workbook และดึง `ExternalConnectionCollection` ของมัน  
```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/sampleRetrievingSQLConnectionData.xlsx");
externalConnectionCollection connections = workbook.getDataConnections();
int connectionCount = connections.getCount();

// Print the number of connections found
System.out.println("Total External Connections: " + connectionCount);
```
*คำอธิบาย:* `getDataConnections()` จะคืนค่าทุกแหล่งข้อมูลภายนอกที่แนบกับ workbook, ให้คุณเห็นจำนวนการเชื่อมต่อที่มีอยู่โดยเร็ว

### วนลูปการเชื่อมต่อภายนอกเพื่อระบุการเชื่อมต่อ DB
**ภาพรวม:** วนลูปแต่ละการเชื่อมต่อและตรวจสอบว่ามันเป็นการเชื่อมต่อฐานข้อมูล (SQL) หรือไม่  
```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;

for (int i = 0; i < connectionCount; i++) {
    ExternalConnection connection = connections.get(i);
    
    if (connection instanceof DBConnection) {
        // This block processes each DB Connection found
        System.out.println("DB Connection Found: " + ((DBConnection) connection).getName());
    }
}
```
*คำอธิบาย:* การตรวจสอบ `instanceof DBConnection` แยกการเชื่อมต่อฐานข้อมูลออกจากประเภทอื่น (เช่น OLEDB หรือเว็บคิวรี), ทำให้สามารถประมวลผลได้ตามเป้าหมาย

### ดึงคุณสมบัติของการเชื่อมต่อ DB
**ภาพรวม:** เมื่อพบการเชื่อมต่อ DB แล้ว ให้ดึงคุณสมบัติหลัก เช่น คำสั่ง SQL, คำอธิบาย, และโหมดการตรวจสอบสิทธิ์  
```java
import com.aspose.cells.ConnectionParameterCollection;

for (int i = 0; i < connectionCount; i++) {
    ExternalConnection connection = connections.get(i);
    
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        
        System.out.println("Command: " + dbConn.getCommand());
        System.out.println("Description: " + dbConn.getConnectionDescription());
        // Add more properties as needed
    }
}
```
*คำอธิบาย:* การเข้าถึงคุณสมบัติเหล่านี้ช่วยให้คุณเข้าใจว่า workbook สื่อสารกับฐานข้อมูลอย่างไรและเป็นฐานข้อมูลสำหรับการปรับแต่งเพิ่มเติม

### เข้าถึงและวนลูปพารามิเตอร์ของการเชื่อมต่อ DB
**ภาพรวม:** การเชื่อมต่อ DB มักมีคอลเลกชันของพารามิเตอร์ (คู่คีย์‑ค่า) ที่ปรับแต่งการเชื่อมต่อให้ละเอียดขึ้น  
```java
for (int i = 0; i < connectionCount; i++) {
    ExternalConnection connection = connections.get(i);
    
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        ConnectionParameterCollection parameterCollection = dbConn.getParameters();
        
        for (int j = 0; j < parameterCollection.getCount(); j++) {
            com.aspose.cells.ConnectionParameter param = parameterCollection.get(j);
            
            System.out.println("Parameter Name: " + param.getName());
            System.out.println("Param Value: " + param.getValue());
        }
    }
}
```
*คำอธิบาย:* พารามิเตอร์อาจรวมถึงชื่อเซิร์ฟเวอร์, ชื่อฐานข้อมูล, หรือออปชันการคิวรีแบบกำหนดเอง การวนลูปพารามิเตอร์เหล่านี้ทำให้คุณมองเห็นการตั้งค่าการเชื่อมต่อทั้งหมดได้อย่างครบถ้วน

## การประยุกต์ใช้งานจริง
การจัดการการเชื่อมต่อ Excel DB ด้วย Aspose.Cells เปิดโอกาสหลายประการ:

1. **การรายงานข้อมูลอัตโนมัติ** – ดึงข้อมูลสดจากเซิร์ฟเวอร์ SQL ไปยัง workbook ตามกำหนดเวลา  
2. **การตรวจสอบความถูกต้องของข้อมูล** – เปรียบเทียบค่าบน worksheet กับบันทึกในฐานข้อมูลแบบเรียลไทม์เพื่อค้นหาความไม่สอดคล้อง  
3. **แดชบอร์ดไดนามิก** – สร้างแดชบอร์ดที่รีเฟรชอัตโนมัติเมื่อข้อมูลในตารางฐานข้อมูลเปลี่ยนแปลง

## พิจารณาด้านประสิทธิภาพ
เมื่อทำงานกับ workbook ขนาดใหญ่หรือการเชื่อมต่อจำนวนมาก:

- **เพิ่มประสิทธิภาพการใช้หน่วยความจำ:** ทำลายอ็อบเจกต์ `Workbook` หลังการประมวลผลเสร็จ  
- **การประมวลผลแบบแบตช์:** รวมหลายไฟล์ในรอบเดียวเพื่อลดค่าโอเวอร์เฮด  
- **คิวรีที่มีประสิทธิภาพ:** ทำให้คำสั่ง SQL กระชับเพื่อให้เวลาโหลดสั้นลง

## สรุป
คุณมีวิธีการแบบครบถ้วนและเป็นขั้นตอนเพื่อ **จัดการการเชื่อมต่อ excel db** ด้วย Aspose.Cells สำหรับ Java แล้ว โหลด workbook, **แสดงรายการการเชื่อมต่อข้อมูล excel**, ดึง **รายละเอียดการเชื่อมต่อ db**, และตรวจสอบพารามิเตอร์ของแต่ละการเชื่อมต่อ เทคนิคเหล่านี้ทำให้คุณสร้างโซลูชันอัตโนมัติของ Excel ที่ขับเคลื่อนด้วยข้อมูลได้อย่างมั่นคง

**ขั้นตอนต่อไป**

- ทดลองโค้ดกับไฟล์ workbook ต่าง ๆ ที่มีการเชื่อมต่อ OLEDB หรือเว็บคิวรี  
- สำรวจเมธอดทั้งหมดของ `DBConnection` ใน [Aspose.Cells documentation](https://reference.aspose.com/cells/java/)  
- นำตรรกะนี้รวมเข้าไปใน pipeline ETL หรือบริการรายงานขนาดใหญ่

## คำถามที่พบบ่อย

**Q: ไลเซนส์ชั่วคราวของ Aspose.Cells คืออะไร?**  
A: ไลเซนส์ชั่วคราวให้คุณประเมินคุณสมบัติเต็มรูปแบบของ Aspose.Cells โดยไม่มีข้อจำกัดในช่วงเวลาที่กำหนด

**Q: สามารถแก้ไข connection string ระหว่างรันได้หรือไม่?**  
A: ได้, คุณสามารถอัปเดตพารามิเตอร์ผ่าน `ConnectionParameter.setValue()` แล้วบันทึก workbook

**Q: Aspose.Cells รองรับไฟล์ Excel ที่เข้ารหัสหรือไม่?**  
A: แน่นอน – เพียงระบุรหัสผ่านเมื่อติดตั้ง workbook: `new Workbook(path, password)`

**Q: จะจัดการกับการเชื่อมต่อที่ใช้ Windows authentication อย่างไร?**  
A: ตั้งค่า property `IntegratedSecurity` บนวัตถุ `DBConnection` หรือปรับพารามิเตอร์ที่เกี่ยวข้องตามความเหมาะสม

**Q: สามารถลบการเชื่อมต่อ DB ออกจาก workbook ได้หรือไม่?**  
A: ได้, เรียก `connections.remove(index)` หลังจากระบุตำแหน่งของการเชื่อมต่อที่ต้องการลบ

---

**Last Updated:** 2025-12-16  
**Tested With:** Aspose.Cells for Java 25.3  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}