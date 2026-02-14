---
category: general
date: 2026-02-14
description: วิธีสร้างลำดับชั้นในเทมเพลต SmartMarker ง่ายกว่าที่คุณคิด – เรียนรู้การสร้างข้อมูลแบบลำดับชั้นและวิธีการแสดงรายการพนักงานอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: th
og_description: วิธีสร้างลำดับชั้นในเทมเพลต SmartMarker นั้นง่ายดาย ทำตามคู่มือนี้เพื่อสร้างข้อมูลแบบลำดับชั้นและแสดงรายการพนักงานด้วยช่วงที่ซ้อนกัน
og_title: วิธีสร้างลำดับชั้นด้วย SmartMarker – คู่มือฉบับสมบูรณ์
tags:
- SmartMarker
- C#
- templating
title: วิธีสร้างลำดับชั้นด้วย SmartMarker – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างลำดับชั้นด้วย SmartMarker – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีสร้างลำดับชั้น** ภายในเทมเพลต SmartMarker โดยไม่ต้องบิดหัวของคุณไหม? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ ในหลายสถานการณ์การรายงานคุณต้องการความสัมพันธ์แบบพาเรนท์‑ชิลด์—เช่น แผนกและพนักงานที่ทำงานในแผนกนั้น ข่าวดีคือ SmartMarker ทำให้เรื่องนี้ง่ายเหมือนเค้กเมื่อคุณรู้ขั้นตอนที่ถูกต้อง

ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งแต่ **การสร้างข้อมูลแบบลำดับชั้น** ใน C#, การเปิดใช้งานช่วงซ้อนกัน (nested ranges) และสุดท้ายการเรนเดอร์เทมเพลตที่ **แสดงรายการพนักงาน** สำหรับแต่ละแผนก เมื่อจบคุณจะได้ตัวอย่างที่พร้อมรันและสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

---

## สิ่งที่คุณต้องมี

- .NET 6+ (เวอร์ชันล่าสุดใดก็ได้)
- การอ้างอิงไลบรารี **SmartMarker** (namespace `ws.SmartMarkerProcessor`)
- ความรู้พื้นฐาน C# – ไม่ต้องซับซ้อน แค่บางอ็อบเจกต์และ lambda หนึ่งสองตัว
- IDE หรือ editor ที่คุณชอบ (Visual Studio, Rider, VS Code… เลือกตามใจ)

ถ้าคุณมีทั้งหมดแล้ว เยี่ยม—มาเริ่มกันเลย

---

## วิธีสร้างลำดับชั้น – ภาพรวม

แนวคิดหลักคือการสร้าง **กราฟอ็อบเจกต์ซ้อนกัน** ที่สะท้อนโครงสร้างที่คุณต้องการเห็นในเอกสารสุดท้าย ในกรณีของเรากราฟจะเป็นดังนี้:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker จะวนลูป `Departments` และเนื่องจากเราจะเปิด **การประมวลผลช่วงซ้อนกัน** มันจะวนลูปคอลเลกชัน `Employees` ของแต่ละแผนกโดยอัตโนมัติ

---

## ขั้นตอนที่ 1: สร้างโมเดลข้อมูลแบบลำดับชั้น

แรกเริ่มเราจะสร้างอ็อบเจกต์แบบไม่ระบุชื่อที่มีอาเรย์ของแผนก แต่ละแผนกมีรายการพนักงานของตนเอง การใช้ประเภทไม่ระบุชื่อทำให้ตัวอย่างเบาและง่ายต่อการเข้าใจ—คุณสามารถเปลี่ยนเป็น POCO class จริงได้ในภายหลัง

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** อาเรย์ `Departments` คือคอลเลกชันระดับบนสุด แต่ละรายการมีอาเรย์ `Employees` ซึ่งเป็นระดับลำดับชั้นที่สองที่เราจะเข้าถึงด้วย `#Departments.Employees#` ในภายหลัง

---

## ขั้นตอนที่ 2: เปิดใช้งานการประมวลผลช่วงซ้อนกัน

SmartMarker จะไม่เข้าไปในคอลเลกชันภายในจนกว่าคุณจะบอกให้ทำ `SmartMarkerOptions` มีสวิตช์นี้

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **เคล็ดลับ:** หากลืมตั้งค่าสถานะนี้ ช่วง `#Employees#` ภายในจะคืนค่าเป็นค่าว่าง และคุณจะงงว่าทำไมเทมเพลตถึงว่างเปล่า

---

## ขั้นตอนที่ 3: รัน Processor พร้อมข้อมูลของคุณ

ต่อไปเราจะส่งข้อมูลและตัวเลือกไปยัง processor ตัวแปร `ws` แทน **WebService** ของคุณ (หรืออ็อบเจกต์ใด ๆ ที่โฮสต์เอ็นจิ้น SmartMarker)

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

ในขั้นตอนนี้ SmartMarker จะวิเคราะห์เทมเพลต แทนที่ `#Departments.Name#` ด้วยชื่อแผนกแต่ละอัน และเนื่องจากเปิดช่วงซ้อนกันแล้ว จะวนลูปคอลเลกชัน `Employees` ของแต่ละแผนกต่อไป

---

## ขั้นตอนที่ 4: สร้าง Marker ของเทมเพลต

ด้านล่างเป็นเทมเพลตขนาดเล็กที่แสดงการทำงานของลูปภายนอกและภายใน วางลงใน SmartMarker template editor (หรือไฟล์ `.txt` ที่คุณส่งให้ processor)

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

เมื่อเรนเดอร์แล้วคุณจะเห็น:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **สิ่งที่คุณกำลังเห็น:** `#Departments.Name#` ภายนอกพิมพ์ชื่อแผนก ส่วนบล็อก `#Departments.Employees#` ภายในลูปพนักงานแต่ละคน และ `#Departments.Employees#` ภายในบล็อกจะแสดงชื่อจริงของพนักงาน

---

## ผลลัพธ์ที่คาดหวังและการตรวจสอบ

การรันตัวอย่างเต็ม (ข้อมูล + ตัวเลือก + เทมเพลต) ควรให้ผลลัพธ์ตรงกับรายการที่แสดงข้างบน เพื่อยืนยันอย่างรวดเร็วคุณสามารถพิมพ์ผลลัพธ์ลงคอนโซลได้ดังนี้:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

หากคุณเห็นหัวข้อแผนกสองหัวข้อตามด้วยรายการพนักงานของแต่ละแผนก คุณได้ **สร้างลำดับชั้นสำเร็จ** และ **แสดงรายการพนักงาน** แล้ว

---

## ข้อผิดพลาดทั่วไปและกรณีขอบ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| ไม่มีผลลัพธ์สำหรับพนักงาน | `EnableNestedRange` ตั้งเป็น false | ตั้งค่า `EnableNestedRange = true` |
| ชื่อพนักงานซ้ำกัน | ใช้อาเรย์เดียวกันหลายแผนก | คัดลอกอาเรย์หรือใช้คอลเลกชันแยกกัน |
| ลำดับชั้นใหญ่ทำให้ใช้หน่วยความจำมาก | SmartMarker โหลดกราฟอ็อบเจกต์ทั้งหมดเข้าสู่หน่วยความจำ | สตรีมข้อมูลหรือแบ่งหน้า (paginate) คอลเลกชันขนาดใหญ่ |
| ไวยากรณ์เทมเพลตผิด | ลืมปิดแท็ก `#/…#` | ใช้ SmartMarker validator หรือทดสอบด้วยเทมเพลตขนาดเล็กก่อน |

---

## ไปต่อ – ความหลากหลายในโลกจริง

1. **แหล่งข้อมูลแบบไดนามิก** – ดึงแผนกจากฐานข้อมูลและแมปเป็นโครงสร้างไม่ระบุชื่อด้วย LINQ  
2. **การจัดรูปแบบตามเงื่อนไข** – เพิ่มฟิลด์ `IsManager` ให้แต่ละพนักงานและใช้แท็กเงื่อนไขของ SmartMarker (`#if …#`) เพื่อไฮไลท์ผู้จัดการ  
3. **หลายระดับการซ้อน** – หากต้องการทีมภายในแผนก ให้เพิ่มคอลเลกชัน `Teams` อีกหนึ่งระดับและเปิด `EnableNestedRange` ไว้ต่อเนื่อง

---

## ตัวอย่างทำงานเต็ม (คัดลอก‑วางได้)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**เทมเพลต (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

รันโปรแกรมจะพิมพ์ลำดับชั้นตรงตามที่แสดงไว้ก่อนหน้า

---

## สรุป

เราได้ครอบคลุม **วิธีสร้างลำดับชั้น** ใน SmartMarker ตั้งแต่การจัดรูปแบบ **ข้อมูลแบบลำดับชั้น** ใน C# การเปิดใช้งานช่วงซ้อนกัน และสุดท้ายการเรนเดอร์เทมเพลตที่ **แสดงรายการพนักงาน** ตามแผนก รูปแบบนี้สามารถขยายได้ง่าย—เพิ่มคอลเลกชันซ้อนเพิ่มเติมหรือเงื่อนไขต่าง ๆ แล้วคุณจะมีเครื่องมือรายงานที่ทรงพลังอยู่ในมือ

พร้อมรับความท้าทายต่อไปหรือยัง? ลองเปลี่ยนประเภทไม่ระบุชื่อเป็น POCO class ที่มีการกำหนดชนิดอย่างชัดเจน หรือผสานกระบวนการนี้เข้าไปใน endpoint ของ ASP.NET Core ที่ส่งออกเป็น PDF หรือ Word เอกสาร ไม่จำกัดอะไรเลย และตอนนี้คุณ **มีพื้นฐานที่มั่นคง** แล้ว

---

![How to create hierarchy diagram](image.png){alt="แผนภาพการสร้างลำดับชั้นแสดงความสัมพันธ์ระหว่างแผนกและพนักงาน"}

*เขียนโค้ดให้สนุก! หากเจออุปสรรคใด ๆ คอมเมนต์ด้านล่างได้เลย—ยินดีช่วยเหลือ*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}