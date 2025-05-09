---
"description": "เรียนรู้วิธีการคัดลอก VBA Macro User Form Designer ใน Aspose.Cells สำหรับ .NET อย่างมีประสิทธิภาพด้วยบทช่วยสอนทีละขั้นตอนที่ครอบคลุมของเรา! ปลดล็อกศักยภาพของ Excel"
"linktitle": "คัดลอก VBAMacro User Form Designer Storage ไปยังเวิร์กบุ๊กโดยใช้ Aspose.Cells"
"second_title": "API การประมวลผล Excel ของ Aspose.Cells .NET"
"title": "คัดลอก VBAMacro User Form Designer Storage ไปยังเวิร์กบุ๊กโดยใช้ Aspose.Cells"
"url": "/th/net/workbook-vba-project/copy-vbamacro-user-form-designer/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# คัดลอก VBAMacro User Form Designer Storage ไปยังเวิร์กบุ๊กโดยใช้ Aspose.Cells

## การแนะนำ
ยินดีต้อนรับ! หากคุณกำลังมองหาวิธีปรับปรุงประสบการณ์การใช้ Excel ของคุณด้วยแมโคร VBA และแบบฟอร์มผู้ใช้ คุณมาถูกที่แล้ว! ในคู่มือนี้ เราจะอธิบายวิธีคัดลอกแมโคร VBA UserForm Designer จากเวิร์กบุ๊กหนึ่งไปยังอีกเวิร์กบุ๊กหนึ่งได้อย่างราบรื่นโดยใช้ Aspose.Cells สำหรับ .NET ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น เราจะแนะนำคุณตลอดทุกขั้นตอนที่สำคัญ ถือว่านี่คือคู่มือของคุณสำหรับการเชี่ยวชาญศิลปะการจัดการไฟล์ Excel ด้วยโปรแกรม พร้อมหรือยังที่จะลงมือทำเลย เริ่มเลย!
## ข้อกำหนดเบื้องต้น
ก่อนที่เราจะเข้าสู่รายละเอียดเล็กๆ น้อยๆ ของการเขียนโค้ด เรามาตรวจสอบก่อนว่าคุณมีทุกสิ่งที่คุณต้องการ:
1. สภาพแวดล้อมการพัฒนา C#: คุณควรมีสภาพแวดล้อมการทำงานที่พร้อมสำหรับการพัฒนา C# ขอแนะนำ Visual Studio อย่างยิ่ง
2. Aspose.Cells สำหรับไลบรารี .NET: ตรวจสอบให้แน่ใจว่าคุณได้รวมไลบรารี Aspose.Cells ไว้ในโปรเจ็กต์ของคุณแล้ว คุณสามารถทำได้ง่ายๆ [ดาวน์โหลดได้ที่นี่](https://releases-aspose.com/cells/net/).
3. ความรู้พื้นฐานเกี่ยวกับ VBA และแมโครของ Excel: ความเข้าใจที่ดีเกี่ยวกับ VBA และการทำงานของแมโครของ Excel จะช่วยให้คุณนำทางผ่านบทช่วยสอนนี้ได้อย่างง่ายดาย
4. ไฟล์ Excel ที่มีแบบฟอร์มผู้ใช้: เพื่อทดลองใช้ สร้าง หรือรับเวิร์กบุ๊ก Excel ที่มีแบบฟอร์มผู้ใช้ โดยควรมีการเปิดใช้งานแมโคร (เช่น `.xlsm` ไฟล์)
## แพ็คเกจนำเข้า
ในโปรเจ็กต์ C# ของคุณ คุณจะต้องนำเข้าเนมสเปซบางส่วนที่ด้านบนสุดของไฟล์เพื่อใช้ฟังก์ชัน Aspose.Cells วิธีดำเนินการมีดังนี้:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
การรวมเนมสเปซเหล่านี้ทำให้คุณสามารถเข้าถึงเครื่องมืออันทรงพลังทั้งหมดที่ฝังอยู่ในไลบรารี Aspose.Cells ได้ 
ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นและแพ็คเกจต่างๆ แล้ว ถึงเวลาที่จะไปต่อกันที่ส่วนที่สนุกสนาน: การเขียนโค้ด! มาแบ่งขั้นตอนออกเป็นขั้นตอนต่างๆ กัน
## ขั้นตอนที่ 1: กำหนดไดเรกทอรีแหล่งที่มาและเอาต์พุตของคุณ
ก่อนอื่น คุณต้องกำหนดว่าไฟล์ของคุณอยู่ที่ไหน:
```csharp
// ไดเรกทอรีแหล่งที่มา
string sourceDir = "Your Document Directory";
// ไดเรกทอรีผลลัพธ์
string outputDir = "Your Document Directory";
```
ที่นี่แทนที่ `"Your Document Directory"` โดยใช้เส้นทางจริงที่จัดเก็บไฟล์ของคุณ นี่คือที่ที่เราจะดึงเวิร์กบุ๊กต้นทาง (พร้อม UserForm) และที่ที่เวิร์กบุ๊กใหม่จะถูกบันทึก
## ขั้นตอนที่ 2: สร้างสมุดงานเป้าหมายที่ว่างเปล่า
ต่อไปเรามาสร้างเวิร์กบุ๊กเป้าหมายกัน โดยที่เราจะคัดลอกแบบฟอร์มผู้ใช้และแมโครของเรา:
```csharp
// สร้างสมุดงานเป้าหมายที่ว่างเปล่า
Workbook target = new Workbook();
```
โค้ดบรรทัดนี้จะสร้างเวิร์กบุ๊กว่างเปล่าขึ้นมาใหม่เพื่อให้เรากรอกข้อมูลลงไป ลองนึกภาพว่าเวิร์กบุ๊กนี้เป็นผืนผ้าใบเปล่าสำหรับงานศิลปะชิ้นเอกของคุณสิ!
## ขั้นตอนที่ 3: โหลดเทมเพลตเวิร์กบุ๊กของคุณ
เราจำเป็นต้องโหลดเวิร์กบุ๊กที่มีแบบฟอร์มผู้ใช้และแมโครของคุณ:
```csharp
// โหลดไฟล์ Excel ที่มีแบบฟอร์มผู้ใช้ VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
อย่าลืมเปลี่ยนแปลง `"sampleDesignerForm.xlsm"` เป็นชื่อไฟล์ของคุณ สมุดงานเล่มนี้เปรียบเสมือนหนังสือสูตรอาหารของคุณ—เป็นส่วนผสมที่เราจะใช้!
## ขั้นตอนที่ 4: คัดลอกแผ่นงานไปยังสมุดงานเป้าหมาย
ตอนนี้เรามาเริ่มคัดลอกเวิร์กชีตจากเทมเพลตของเราไปยังเวิร์กบุ๊กเป้าหมาย:
```csharp
// คัดลอกแผ่นงานเทมเพลตทั้งหมดไปยังสมุดงานเป้าหมาย
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // ใส่ข้อความในเซลล์ A2 ของเวิร์กชีตเป้าหมาย
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
ในขั้นตอนนี้ เราจะวนซ้ำผ่านแต่ละเวิร์กชีตในเทมเพลตและคัดลอกไปยังเวิร์กบุ๊กเป้าหมาย ลองคิดดูสิ มันก็เหมือนกับการถ่ายโอนสูตรอาหารที่ดีที่สุดของคุณจากหนังสือทำอาหารเล่มหนึ่งไปยังอีกเล่มหนึ่ง!
## ขั้นตอนที่ 5: คัดลอก VBA Macro จากเทมเพลต
ต่อไปเราจะคัดลอกแมโคร VBA รวมถึงโมดูล UserForm Designer ไปยังเวิร์กบุ๊กใหม่ของเรา:
```csharp
// คัดลอกแบบฟอร์มผู้ใช้ VBA-Macro Designer จากเทมเพลตไปยังเป้าหมาย
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // คัดลอกรหัสโมดูล ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // คัดลอกโค้ดและข้อมูลของโมดูลอื่น ๆ
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // รับข้อมูลของแบบฟอร์มผู้ใช้ เช่น ที่เก็บของนักออกแบบ
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // เพิ่มที่เก็บข้อมูลนักออกแบบเพื่อกำหนดเป้าหมายโครงการ VBA
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
โค้ดชิ้นใหญ่ชิ้นนี้ทำหน้าที่ตรวจสอบโมดูล VBA แต่ละตัวในไฟล์เทมเพลต เรากำลังคัดลอกการออกแบบ UserForm และโค้ดที่เกี่ยวข้อง ซึ่งก็เหมือนกับการให้แน่ใจว่าคุณได้รับสูตรพายชื่อดังของยายเท่านั้น แต่ยังรวมถึงเทคนิคการอบขนมที่แม่นยำของยายด้วย!
## ขั้นตอนที่ 6: บันทึกสมุดงานเป้าหมาย
หลังจากที่เราได้รับสำเนาทั้งหมดแล้ว ก็ถึงเวลาที่จะบันทึกงานหนักของเรา:
```csharp
// บันทึกสมุดงานเป้าหมาย
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
อย่าลืมแก้ไขชื่อไฟล์เอาต์พุตตามต้องการ เมื่อคุณบันทึกแล้ว คุณก็จะสร้างเวิร์กบุ๊กเวอร์ชันเฉพาะของคุณเองที่เต็มไปด้วยแมโครและแบบฟอร์มผู้ใช้ น่าตื่นเต้นแค่ไหนล่ะ?
## ขั้นตอนที่ 7: ยืนยันความสำเร็จ
ในที่สุด ให้พิมพ์ข้อความแสดงความสำเร็จไปยังคอนโซล:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
บรรทัดเล็กๆ นี้ช่วยให้คุณมั่นใจได้ว่ากระบวนการของคุณดำเนินไปอย่างราบรื่น นี่คือส่วนสำคัญของการเขียนโค้ดของคุณ!
## บทสรุป
ขอแสดงความยินดี! คุณได้ทำตามคู่มือทีละขั้นตอนในการคัดลอก VBA Macro User Form Designer จากเวิร์กบุ๊กหนึ่งไปยังอีกเวิร์กบุ๊กหนึ่งโดยใช้ Aspose.Cells สำหรับ .NET เสร็จเรียบร้อยแล้ว อาจดูยุ่งยากเล็กน้อยในตอนแรก แต่ด้วยการฝึกฝน คุณจะสามารถจัดการกับเวิร์กบุ๊กได้อย่างมืออาชีพ โปรดจำไว้ว่าการเขียนโค้ดต้องอาศัยการฝึกฝน ดังนั้นอย่าอายที่จะลองทำสิ่งอื่นๆ ในไฟล์ Excel ของคุณ หากคุณมีคำถามหรือประสบปัญหาใดๆ โปรดไปที่ฟอรัมหรือเอกสารประกอบของ Aspose เพื่อขอรับการสนับสนุน!
## คำถามที่พบบ่อย
### Aspose.Cells รองรับ Excel เวอร์ชันใดบ้าง
Aspose.Cells รองรับรูปแบบ Excel หลากหลาย รวมถึง XLSX, XLSM, CSV และอื่นๆ
### ฉันสามารถใช้ Aspose.Cells ได้ฟรีหรือไม่?
ใช่! คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรี ซึ่งจะช่วยให้คุณประเมินไลบรารีได้: [ทดลองใช้งานฟรี](https://releases-aspose.com/).
### ฉันต้องมี Visual Studio เพื่อรันโค้ดนี้หรือไม่?
แม้ว่าจะได้รับการแนะนำอย่างยิ่งเนื่องจากคุณสมบัติที่เป็นมิตรต่อผู้ใช้ แต่ IDE C# ใดๆ ก็สามารถใช้ได้ตราบใดที่รองรับการพัฒนา .NET
### ฉันสามารถหาตัวอย่างและเอกสารเพิ่มเติมได้ที่ไหน
คุณสามารถสำรวจได้ [เอกสารประกอบ Aspose.Cells](https://reference.aspose.com/cells/net/) เพื่อดูตัวอย่างเพิ่มเติมและคำอธิบายโดยละเอียด
### ฉันจะแก้ไขปัญหาการใช้งาน Aspose.Cells ได้อย่างไร
คุณควรไปเยี่ยมชม [ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/c/cells/9) เพื่อขอความช่วยเหลือจากชุมชนและเจ้าหน้าที่สนับสนุน Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}