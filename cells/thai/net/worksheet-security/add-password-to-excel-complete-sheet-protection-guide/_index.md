---
category: general
date: 2026-03-27
description: เพิ่มรหัสผ่านให้กับ Excel และปกป้องข้อมูลของคุณด้วยตัวเลือกการป้องกันแผ่นงาน
  Excel โดยอนุญาตให้เลือกเซลล์ที่ปลดล็อกได้ขณะบันทึกเวิร์กบุ๊กที่ได้รับการป้องกันอย่างง่ายดาย.
draft: false
keywords:
- add password to excel
- excel sheet protection options
- allow select unlocked cells
- save protected workbook
- enable sheet protection
language: th
og_description: เพิ่มรหัสผ่านให้กับ Excel และปกป้องแผ่นงานของคุณด้วยตัวเลือกในตัวที่อนุญาตให้เลือกเซลล์ที่ปลดล็อกและบันทึกเวิร์กบุ๊กที่ได้รับการปกป้องในไม่กี่นาที.
og_title: เพิ่มรหัสผ่านให้กับ Excel – คู่มือการป้องกันแผ่นงานอย่างครบถ้วน
tags:
- Aspose.Cells
- C#
- Excel security
title: เพิ่มรหัสผ่านใน Excel – คู่มือการปกป้องแผ่นงานอย่างครบถ้วน
url: /th/net/worksheet-security/add-password-to-excel-complete-sheet-protection-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มรหัสผ่านให้กับ Excel – คู่มือการป้องกันชีตอย่างครบถ้วน

เคยสงสัยไหมว่าจะ **เพิ่มรหัสผ่านให้กับไฟล์ Excel** อย่างไรโดยไม่ต้องบิดหัว? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องล็อกข้อมูลสำคัญในสเปรดชีต ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และ Aspose.Cells คุณสามารถเปิดใช้งานการป้องกันชีต เลือกตัวเลือกการป้องกัน Excel ที่ต้องการได้อย่างแม่นยำ และแม้กระทั่งอนุญาตให้เลือกเซลล์ที่ปลดล็อกเพื่อประสบการณ์ผู้ใช้ที่ราบรื่นขึ้น

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่การสร้างเวิร์กบุ๊ก การเขียนค่าที่เป็นความลับ การใช้รหัสผ่านแบบ SHA‑256 การปรับตั้งค่าการป้องกัน และสุดท้าย **บันทึกเวิร์กบุ๊กที่ป้องกัน** ลงดิสก์ เมื่อจบคุณจะรู้วิธีเพิ่มรหัสผ่านให้กับ Excel อย่างแม่นยำ เหตุผลที่แต่ละตัวเลือกสำคัญ และวิธีปรับโค้ดให้เข้ากับโปรเจกต์ของคุณ

## ข้อกำหนดเบื้องต้น

- .NET 6 หรือใหม่กว่า (โค้ดทำงานได้กับ .NET Core และ .NET Framework ทั้งหมด)
- Aspose.Cells for .NET ติดตั้งผ่าน NuGet (`dotnet add package Aspose.Cells`)
- ความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C# (ไม่ต้องมีเทคนิคขั้นสูง)

หากส่วนใดส่วนหนึ่งยังไม่คุ้นเคย ให้หยุดที่นี่และติดตั้งแพคเกจก่อน—เมื่อพร้อมแล้วเราจะดำเนินการต่อ

## ขั้นตอนที่ 1 – สร้าง Workbook ใหม่ (เปิดใช้งานการป้องกันชีต)

ก่อนที่เราจะ **เพิ่มรหัสผ่านให้กับ Excel** เราต้องมีอ็อบเจกต์ workbook เพื่อทำงาน ขั้นตอนนี้ยังเป็นการเตรียมพื้นฐานสำหรับการปรับการป้องกันในขั้นต่อไป

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Create a fresh workbook – think of it as a blank Excel file
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

*ทำไมจึงสำคัญ:* การสร้าง `Workbook` ให้คุณเริ่มจากแผ่นเปล่า หากคุณเปิดไฟล์ที่มีอยู่แล้ว ให้ใช้ `new Workbook("path.xlsx")` แทน การอ้างอิง `Worksheet` จะเป็นที่ที่เราจะเขียนข้อมูลและตั้งค่าการป้องกันต่อไป

## ขั้นตอนที่ 2 – เขียนข้อมูลที่เป็นความลับ (สิ่งที่เราจะป้องกัน)

ต่อไปเราจะใส่ข้อมูลที่ผู้ใช้ไม่ควรแก้ไข—อาจเป็นรหัสผ่าน ตัวเลขทางการเงิน หรือหมายเลขประจำตัวส่วนบุคคล

```csharp
        // Write confidential text into cell A1
        worksheet.Cells["A1"].PutValue("Sensitive Information");
```

*เคล็ดลับ:* หากต้องการล็อกเฉพาะส่วนของชีต คุณสามารถทำเครื่องหมายเซลล์ที่ต้องการปลดล็อกในภายหลัง โดยค่าเริ่มต้นทั้งหมดจะถูกล็อกเมื่อเปิดการป้องกัน ดังนั้นเราจะจัดการในขั้นตอนต่อไป

## ขั้นตอนที่ 3 – เปิดการป้องกันชีต & เพิ่มรหัสผ่าน SHA‑256

นี่คือหัวใจของบทแนะนำ: เรา **เพิ่มรหัสผ่านให้กับ Excel** โดยเปิดการป้องกันและกำหนดแฮชที่แข็งแรง

```csharp
        // Access the protection object for the worksheet
        WorksheetProtection protection = worksheet.Protection;

        // Turn on protection – this is the “enable sheet protection” flag
        protection.IsProtected = true;

        // Set a SHA‑256 hashed password (much stronger than plain text)
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);
```

*ทำไมต้องใช้ SHA‑256?* รหัสผ่านแบบข้อความธรรมดาสามารถถูกทำลายด้วยเครื่องมือ brute‑force ได้ ในขณะที่แฮช SHA‑256 ให้ชั้นการเข้ารหัสที่ Aspose.Cells จัดการให้คุณ หากต้องการใช้แฮชแบบเก่าที่เข้ากันกับ Excel ให้เปลี่ยน `PasswordType.SHA256` เป็น `PasswordType.Standard`

## ขั้นตอนที่ 4 – ปรับแต่งตัวเลือกการป้องกันชีต Excel อย่างละเอียด

เมื่อชีตถูกล็อกแล้ว เราตัดสินใจ **ตัวเลือกการป้องกันชีต Excel** เช่น ผู้ใช้สามารถเลือกเซลล์ที่ล็อกได้หรือไม่, แก้ไขวัตถุได้หรือไม่, หรือที่สำคัญสำหรับหลายกระบวนการ **อนุญาตให้เลือกเซลล์ที่ปลดล็อก** ได้หรือไม่

```csharp
        // Allow users to click on unlocked cells (useful for data entry)
        protection.AllowSelectUnlockedCells = true;

        // Disallow editing of embedded objects like charts or shapes
        protection.AllowEditObject = false;

        // You can also restrict formatting, inserting rows, etc.
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;
```

*คำอธิบาย:*  
- `AllowSelectUnlockedCells` ให้ผู้ใช้สามารถเลื่อนดูชีตโดยไม่เกิดคำเตือน “ชีตถูกป้องกัน” เหมาะเมื่อคุณต้องการพื้นที่แบบฟอร์ม  
- `AllowEditObject = false` ปิดการแก้ไขแผนภูมิ รูปภาพ หรือวัตถุฝังอื่น ๆ เพื่อเพิ่มความปลอดภัย  
- มีแฟล็กเพิ่มเติมสำหรับการควบคุมแบบละเอียด—เปิดใช้งานตามความต้องการของสถานการณ์ของคุณได้เลย

## ขั้นตอนที่ 5 – บันทึกเวิร์กบุ๊กที่ป้องกัน (Save Protected Workbook)

ขั้นตอนสุดท้ายคือการบันทึกไฟล์ นี่คือจุดที่เราจะ **บันทึกเวิร์กบุ๊กที่ป้องกัน** ลงดิสก์ และคุณจะเห็นการป้องกันรหัสผ่านทำงานเมื่อเปิดไฟล์ใน Excel

```csharp
        // Persist the workbook with all protection settings applied
        workbook.Save("ProtectedSheet.xlsx");

        // Optional: let the console know we’re done
        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

เมื่อคุณดับเบิลคลิก `ProtectedSheet.xlsx` Excel จะขอรหัสผ่านที่คุณตั้งไว้ (`MyStrongPwd!`) หากพยายามแก้ไขเซลล์ที่ล็อก จะถูกบล็อก; แต่คุณยังสามารถเลือกเซลล์ที่ปลดล็อกได้ตามตัวเลือกที่ตั้งไว้ก่อนหน้า

### ผลลัพธ์ที่คาดหวัง

- **ไฟล์:** `ProtectedSheet.xlsx` ปรากฏในโฟลเดอร์ output ของโปรเจกต์คุณ  
- **พฤติกรรม:** เปิดไฟล์จะขอรหัสผ่าน หลังจากใส่แล้ว เซลล์ A1 จะเป็นแบบอ่าน‑อย่างอย่างเดียว ส่วนเซลล์ที่ปลดล็อก (ถ้ามี) สามารถแก้ไขได้  
- **การตรวจสอบ:** ลองแก้ไข A1—Excel ควรปฏิเสธ ลองคลิกเซลล์ที่ปลดล็อก (ถ้าคุณสร้างไว้) จะสามารถเลือกได้โดยไม่มีข้อผิดพลาด

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|----------|----------------|-----|
| **อัลกอริทึมรหัสผ่านต่างกัน** | ใช้ `PasswordType.Standard` | เพื่อความเข้ากันได้กับ Excel รุ่นเก่าที่ไม่รองรับ SHA‑256 |
| **ป้องกันเวิร์กบุ๊กที่มีอยู่** | โหลดด้วย `new Workbook("Existing.xlsx")` | เพิ่มการป้องกันให้ไฟล์ที่คุณมีอยู่แล้ว |
| **ล็อกเฉพาะช่วง** | ตั้ง `worksheet.Cells["B2:C5"].Style.Locked = false;` ก่อนเปิดการป้องกัน | ปลดล็อกช่วงเฉพาะขณะที่ส่วนอื่นยังล็อก |
| **อนุญาตให้ผู้ใช้จัดรูปแบบเซลล์** | `protection.AllowFormatCells = true;` | เหมาะสำหรับแดชบอร์ดที่ผู้ใช้เปลี่ยนสีได้แต่ไม่แก้ไขข้อมูล |
| **บันทึกลงสตรีม (เช่น การตอบสนองเว็บ)** | `workbook.Save(stream, SaveFormat.Xlsx);` | เหมาะสำหรับ API ASP.NET ที่ส่งไฟล์ตรงไปยังเบราว์เซอร์ |

*ระวัง:* อย่าลืมตั้ง `IsProtected = true`—รหัสผ่านอย่างเดียวจะไม่ล็อกชีตได้ ควรทดสอบกับ Excel จริงเสมอ เพราะบางแฟล็กการป้องกันอาจทำงานแตกต่างกันเล็กน้อยระหว่างเวอร์ชัน Office

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมครบชุดที่คุณสามารถวางลงในแอปคอนโซลได้เลย ไม่มีส่วนที่ขาดหาย

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write some sensitive information into a cell
        worksheet.Cells["A1"].PutValue("Sensitive Information");

        // Optional: Unlock a range for user input (e.g., B1:C5)
        worksheet.Cells["B1:C5"].Style.Locked = false;

        // Step 3: Enable sheet protection and set a SHA‑256 hashed password
        WorksheetProtection protection = worksheet.Protection;
        protection.IsProtected = true;                     // enable sheet protection
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);

        // Step 4: Restrict actions – allow selecting unlocked cells only
        protection.AllowSelectUnlockedCells = true;
        protection.AllowEditObject = false;               // disallow editing objects
        // Additional options you might need:
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;

        // Step 5: Save the protected workbook to a file
        workbook.Save("ProtectedSheet.xlsx");

        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

รันโปรแกรม เปิดไฟล์ที่สร้างขึ้น แล้วคุณจะเห็นการป้องกันทำงาน

## ภาพอ้างอิง

![Add password to Excel sheet protection screenshot](https://example.com/images/add-password-to-excel.png "add password to excel")

*ข้อความแทนภาพรวมถึงคีย์เวิร์ดหลักสำหรับ SEO*

## สรุป & ขั้นตอนต่อไป

เราได้แสดง **วิธีเพิ่มรหัสผ่านให้กับ Excel** ด้วย Aspose.Cells ครอบคลุม **ตัวเลือกการป้องกันชีต Excel** ที่สำคัญ แสดงการใช้แฟล็ก **allow select unlocked cells** และบันทึก **เวิร์กบุ๊กที่ป้องกัน** ที่เคารพการตั้งค่าเหล่านั้น สรุปขั้นตอนคือ:

1. สร้างหรือโหลดเวิร์กบุ๊ก  
2. เขียนข้อมูลที่ต้องการป้องกัน  
3. เปิดการป้องกัน ตั้งรหัสผ่านที่แข็งแรง และปรับตัวเลือก  
4. บันทึกเวิร์กบุ๊ก

เมื่อคุณเข้าใจพื้นฐานแล้ว ลองพิจารณาไอเดียต่อไปนี้:

- **การแสดงหน้าต่างรหัสผ่านแบบโปรแกรม:** ให้ผู้ใช้กรอกรหัสผ่านผ่าน UI ที่ปลอดภัยแทนการฝังไว้ในโค้ด  
- **การป้องกันเป็นชุด:** วนลูปหลายชีตและใช้การตั้งค่าเดียวกัน  
- **ผสานกับ ASP.NET Core:** ส่งไฟล์ที่ป้องกันเป็นการดาวน์โหลดโดยตรง  

ลองทดลองดู—คุณอาจล็อกชุดรายงานทั้งหมดหรือแค่ชีตลับหนึ่งที่เป็นความลับ ไม่ว่าผลลัพธ์จะเป็นอย่างไร คุณก็มีเครื่องมือครบครันในการปกป้องข้อมูล Excel อย่างถูกต้อง

---

*Happy coding! หากคู่มือนี้ช่วยคุณเพิ่มรหัสผ่านให้กับ Excel ได้ โปรดบอกเราผ่านคอมเมนต์หรือแชร์การปรับแต่งของคุณเอง การเรียนรู้ร่วมกันจะทำให้สเปรดชีตของเราปลอดภัยยิ่งขึ้น*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}