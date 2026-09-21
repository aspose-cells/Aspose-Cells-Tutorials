---
date: '2026-03-17'
description: เรียนรู้วิธีจัดการการเชื่อมต่อฐานข้อมูล Excel สำหรับแดชบอร์ด Excel แบบไดนามิกโดยใช้
  Aspose.Cells for Java, แสดงรายการการเชื่อมต่อข้อมูล Excel, แก้ไขการเชื่อมต่อฐานข้อมูล
  Excel, และรับข้อมูลการเชื่อมต่อ SQL อย่างมีประสิทธิภาพ.
keywords:
- Aspose.Cells Java
- manage Excel DB connections
- list Excel data connections
- get DB connection details
- load workbook Aspose Cells
title: จัดการการเชื่อมต่อฐานข้อมูล Excel สำหรับแดชบอร์ด Excel แบบไดนามิกด้วย Aspose.Cells
  สำหรับ Java
url: /th/java/advanced-features/aspose-cells-java-excel-db-connections/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# จัดการการเชื่อมต่อ Excel DB สำหรับแดชบอร์ด Excel แบบไดนามิกด้วย Aspose.Cells for Java

ในแอปพลิเคชันที่ขับเคลื่อนด้วยข้อมูลในยุคปัจจุบัน **การจัดการการเชื่อมต่อ Excel DB** เป็นทักษะสำคัญ โดยเฉพาะเมื่อคุณต้องการสร้าง **แดชบอร์ด Excel แบบไดนามิก** ที่รีเฟรชโดยอัตโนมัติจากฐานข้อมูลสด บทเรียนนี้จะพาคุณผ่านการใช้ Aspose.Cells for Java เพื่อ **แสดงรายการการเชื่อมต่อข้อมูล Excel**, ดึง **รายละเอียดการเชื่อมต่อ DB**, และ **แก้ไขพารามิเตอร์การเชื่อมต่อ Excel DB** เพื่อให้แดชบอร์ดของคุณอัปเดตอยู่เสมอโดยไม่ต้องทำด้วยตนเอง

## คำตอบสั้น
- **ไลบรารีที่จัดการการเชื่อมต่อ Excel DB คืออะไร?** Aspose.Cells for Java.  
- **ฉันจะลิสต์การเชื่อมต่อข้อมูลทั้งหมดได้อย่างไร?** ใช้ `Workbook.getDataConnections()`.  
- **ฉันสามารถดึงพารามิเตอร์การเชื่อมต่อได้หรือไม่?** ได้, ผ่าน `DBConnection.getParameters()`.  
- **ต้องมีลิขสิทธิ์หรือไม่?** จำเป็นต้องมีลิขสิทธิ์ชั่วคราวหรือเต็มสำหรับการใช้งานในผลิตภัณฑ์.  
- **Maven รองรับหรือไม่?** รองรับแน่นอน – เพิ่ม dependency ของ Aspose.Cells ไปที่ `pom.xml`.  
- **วิธีนี้ช่วยแดชบอร์ด Excel แบบไดนามิกอย่างไร?** ทำให้คุณสามารถรีเฟรชแหล่งข้อมูลแบบโปรแกรมและทำให้การแสดงผลเป็นปัจจุบันอยู่เสมอ.  

## “แดชบอร์ด Excel แบบไดนามิก” คืออะไร?
**แดชบอร์ด Excel แบบไดนามิก** คือไฟล์ Excel ที่ดึงข้อมูลสดจากแหล่งภายนอก (เช่นฐานข้อมูล SQL) และอัปเดตแผนภูมิ ตาราง และ KPI โดยอัตโนมัติเมื่อข้อมูลพื้นฐานมีการเปลี่ยนแปลง การจัดการการเชื่อมต่อ DB ของเวิร์กบุ๊กทำให้แดชบอร์ดแสดงข้อมูลล่าสุดโดยไม่ต้องผู้ใช้ทำการอัปเดตเอง

## ทำไมต้องใช้ Aspose.Cells for Java?
Aspose.Cells ให้ API แบบ Java แท้ที่ทำงานได้โดยไม่ต้องติดตั้ง Microsoft Office ให้คุณควบคุมออบเจ็กต์เวิร์กบุ๊กได้เต็มที่ รองรับคุณสมบัติของ Excel หลากหลาย และจัดการการเชื่อมต่อภายนอกอย่างปลอดภัยและมีประสิทธิภาพ – เหมาะอย่างยิ่งสำหรับการอัตโนมัติการรายงานข้อมูล Excel และการสร้างแดชบอร์ดแบบไดนามิก

## ข้อกำหนดเบื้องต้น
1. **ไลบรารีที่ต้องการ:** Aspose.Cells for Java (เวอร์ชันล่าสุด).  
2. **เครื่องมือสร้าง:** Maven หรือ Gradle.  
3. **ความรู้พื้นฐาน:** การเขียนโปรแกรม Java เบื้องต้นและความคุ้นเคยกับการเชื่อมต่อข้อมูลของ Excel.

## การตั้งค่า Aspose.Cells for Java
เพื่อจัดการการเชื่อมต่อ Excel DB ให้เพิ่ม Aspose.Cells เข้าไปในโปรเจกต์ของคุณ

### การตั้งค่า Maven *(aspose cells maven setup)*
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

หลังจากเพิ่ม dependency แล้ว ให้รับลิขสิทธิ์จาก [official site](https://purchase.aspose.com/temporary-license/). ลิขสิทธิ์นี้จะเปิดใช้งานฟีเจอร์เต็มสำหรับการทดลองและการใช้งานในผลิตภัณฑ์

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

## คู่มือการทำงาน
ต่อไปนี้เป็นขั้นตอนที่จำเป็นสำหรับ **การแสดงรายการการเชื่อมต่อข้อมูล Excel**, **ดึงข้อมูลการเชื่อมต่อ SQL**, และ **แก้ไขการตั้งค่าการเชื่อมต่อ Excel DB**.

### โหลดเวิร์กบุ๊กและเข้าถึงการเชื่อมต่อภายนอก
**ภาพรวม:** โหลดเวิร์กบุ๊กและดึง `ExternalConnectionCollection` ของมัน.  
```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/sampleRetrievingSQLConnectionData.xlsx");
externalConnectionCollection connections = workbook.getDataConnections();
int connectionCount = connections.getCount();

// Print the number of connections found
System.out.println("Total External Connections: " + connectionCount);
```
*คำอธิบาย:* `getDataConnections()` จะคืนค่าการเชื่อมต่อข้อมูลภายนอกทั้งหมดที่แนบกับเวิร์กบุ๊ก ทำให้คุณทราบจำนวนการเชื่อมต่อที่มีอยู่ได้อย่างรวดเร็ว.

### วนลูปการเชื่อมต่อภายนอกเพื่อระบุการเชื่อมต่อ DB
**ภาพรวม:** ทำลูปผ่านแต่ละการเชื่อมต่อและตรวจสอบว่าเป็นการเชื่อมต่อฐานข้อมูล (SQL) หรือไม่.  
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
*คำอธิบาย:* การตรวจสอบ `instanceof DBConnection` จะคัดแยกการเชื่อมต่อฐานข้อมูลออกจากประเภทอื่น (เช่น OLEDB หรือเว็บคิวรี) เพื่อให้สามารถประมวลผลได้อย่างตรงจุด.

### ดึงคุณสมบัติของการเชื่อมต่อ DB
**ภาพรวม:** เมื่อพบการเชื่อมต่อ DB แล้ว ให้ดึงคุณสมบัติหลัก เช่น คำสั่ง SQL, คำอธิบาย, และโหมดการยืนยันตัวตน.  
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
*คำอธิบาย:* การเข้าถึงคุณสมบัติเหล่านี้ช่วยให้คุณเข้าใจว่าเวิร์กบุ๊กสื่อสารกับฐานข้อมูลอย่างไรและเป็นฐานข้อมูลสำหรับการปรับแต่งต่อไป.

### เข้าถึงและวนลูปพารามิเตอร์ของการเชื่อมต่อ DB
**ภาพรวม:** การเชื่อมต่อ DB มักมีคอลเลกชันของพารามิเตอร์ (คู่คีย์‑ค่า) ที่ปรับแต่งการเชื่อมต่อ.  
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
*คำอธิบาย:* พารามิเตอร์อาจรวมถึงชื่อเซิร์ฟเวอร์, ชื่อฐานข้อมูล, หรือออปชันของคิวรีแบบกำหนดเอง การวนลูปพารามิเตอร์ทำให้คุณเห็นการกำหนดค่าการเชื่อมต่อทั้งหมด.

## การประยุกต์ใช้ในเชิงปฏิบัติ
การจัดการการเชื่อมต่อ Excel DB ด้วย Aspose.Cells เปิดโอกาสหลายอย่างสำหรับ **แดชบอร์ด Excel แบบไดนามิก**:

1. **การรายงานข้อมูล Excel อัตโนมัติ** – ดึงข้อมูลสดจากเซิร์ฟเวอร์ SQL ไปยังไฟล์ Excel ตามกำหนดเวลา.  
2. **การตรวจสอบความถูกต้องของข้อมูล** – เปรียบเทียบค่าบนชีตกับบันทึกในฐานข้อมูลสดเพื่อค้นหาความไม่สอดคล้อง.  
3. **แดชบอร์ดไดนามิก** – สร้างแดชบอร์ดที่รีเฟรชอัตโนมัติเมื่อเทเบิลฐานข้อมูลที่อ้างอิงมีการเปลี่ยนแปลง.  
4. **แก้ไขการเชื่อมต่อ Excel DB** – เปลี่ยนชื่อเซิร์ฟเวอร์หรือฐานข้อมูลโดยโปรแกรมโดยไม่ต้องเปิดไฟล์ด้วยตนเอง.

## ข้อควรพิจารณาด้านประสิทธิภาพ
เมื่อทำงานกับเวิร์กบุ๊กขนาดใหญ่หรือการเชื่อมต่อหลายรายการ:

- **เพิ่มประสิทธิภาพการใช้หน่วยความจำ:** ทำลบออบเจ็กต์ `Workbook` หลังการประมวลผล.  
- **การประมวลผลแบบแบตช์:** รวมหลายไฟล์ในรอบเดียวเพื่อลดค่าโอเวอร์เฮด.  
- **คิวรีที่มีประสิทธิภาพ:** ทำให้คำสั่ง SQL สั้นและกระชับเพื่อลดเวลาโหลด.

## สรุป
ตอนนี้คุณมีวิธีการแบบครบถ้วนและเป็นขั้นตอนเพื่อ **จัดการการเชื่อมต่อ Excel DB** ด้วย Aspose.Cells for Java แล้ว: โหลดเวิร์กบุ๊ก, **แสดงรายการการเชื่อมต่อข้อมูล Excel**, ดึง **รายละเอียดการเชื่อมต่อ DB**, **ดึงข้อมูลการเชื่อมต่อ SQL**, และ **แก้ไขพารามิเตอร์การเชื่อมต่อ Excel DB** เทคนิคเหล่านี้ช่วยให้คุณสร้าง **แดชบอร์ด Excel แบบไดนามิก** ที่แข็งแรงและอัตโนมัติการรายงานข้อมูล Excel

**ขั้นตอนต่อไป**

- ทดลองโค้ดกับไฟล์เวิร์กบุ๊กที่มีการเชื่อมต่อ OLEDB หรือเว็บคิวรีต่าง ๆ.  
- สำรวจเมธอดทั้งหมดของ `DBConnection` ใน [Aspose.Cells documentation](https://reference.aspose.com/cells/java/).  
- ผสานตรรกะนี้เข้ากับ pipeline ETL หรือบริการรายงานขนาดใหญ่ของคุณ.

## คำถามที่พบบ่อย

**Q: ลิขสิทธิ์ชั่วคราวของ Aspose.Cells คืออะไร?**  
A: ลิขสิทธิ์ชั่วคราวให้คุณประเมินฟีเจอร์เต็มของ Aspose.Cells โดยไม่มีข้อจำกัดเป็นระยะเวลาจำกัด.

**Q: สามารถแก้ไข connection string ระหว่างรันได้หรือไม่?**  
A: ได้, คุณสามารถอัปเดตพารามิเตอร์ผ่าน `ConnectionParameter.setValue()` แล้วบันทึกเวิร์กบุ๊ก.

**Q: Aspose.Cells รองรับไฟล์ Excel ที่เข้ารหัสหรือไม่?**  
A: รองรับอย่างเต็มที่ – เพียงระบุรหัสผ่านเมื่อโหลดเวิร์กบุ๊ก: `new Workbook(path, password)`.

**Q: จะจัดการกับการเชื่อมต่อที่ใช้ Windows authentication อย่างไร?**  
A: ตั้งค่า property `IntegratedSecurity` บนออบเจ็กต์ `DBConnection` หรือปรับพารามิเตอร์ที่เกี่ยวข้องตามความเหมาะสม.

**Q: สามารถลบการเชื่อมต่อ DB ออกจากเวิร์กบุ๊กได้หรือไม่?**  
A: ได้, เรียก `connections.remove(index)` หลังจากค้นหาการเชื่อมต่อเป้าหมาย.

**Q: จะทำให้การรายงานข้อมูล Excel อัตโนมัติด้วย API นี้อย่างไร?**  
A: ผสานตรรกะการลิสต์การเชื่อมต่อกับงาน Java ที่กำหนดเวลา (เช่น Quartz) เพื่อรีเฟรชข้อมูลและบันทึกเวิร์กบุ๊กตามช่วงเวลาที่กำหนด.

**Q: หากต้องการเปลี่ยนคำสั่ง SQL สำหรับการเชื่อมต่อเฉพาะ จะทำอย่างไร?**  
A: ใช้ `dbConn.setCommand("NEW SQL QUERY")` แล้วบันทึกเวิร์กบุ๊กเพื่อให้การเปลี่ยนแปลงมีผล.

---

**Last Updated:** 2026-03-17  
**Tested With:** Aspose.Cells for Java 25.3  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}