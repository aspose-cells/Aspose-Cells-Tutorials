---
category: general
date: 2026-06-18
description: كيفية إضافة خاصية مخصصة في Excel باستخدام Java. تعلم استرجاع قيمة الخاصية
  المخصصة وحفظ المصنف بصيغة XLSB مع مثال كامل قابل للتنفيذ.
draft: false
keywords:
- how to add custom property
- retrieve custom property value
- save workbook as xlsb
- create custom property in excel
language: ar
og_description: كيفية إضافة خاصية مخصصة في Excel باستخدام Java. يوضح هذا الدليل كيفية
  استرجاع قيمة الخاصية المخصصة وحفظ المصنف بصيغة XLSB.
og_title: كيفية إضافة خاصية مخصصة في إكسل (جافا) – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add custom property in Excel using Java. Learn to retrieve custom
    property value and save workbook as XLSB with a complete, runnable example.
  headline: How to Add Custom Property in Excel (Java) – Retrieve Value & Save as
    XLSB
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: كيفية إضافة خاصية مخصصة في Excel (Java) – استرجاع القيمة وحفظها كملف XLSB
url: /ar/java/workbook-operations/how-to-add-custom-property-in-excel-java-retrieve-value-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة خاصية مخصصة في Excel (Java) – استرجاع القيمة وحفظها كـ XLSB

إضافة خاصية مخصصة في Excel باستخدام Java هي حاجة شائعة عندما تريد وضع بيانات وصفية على أوراق العمل. في هذا الدرس سنسترجع أيضًا قيمة الخاصية المخصصة **ونحفظ المصنف كملف XLSB**، لتحصل على حل كامل من البداية إلى النهاية يمكنك دمجه في أي مشروع.

تخيل أنك تبني محرك تقارير يولد عشرات جداول البيانات كل ليلة. ترغب في تضمين “ProjectId” أو “ReportVersion” مباشرة داخل الملف حتى تتمكن الأنظمة اللاحقة من تصفيتها أو تدقيقها لاحقًا. هذا بالضبط ما توفره الخصائص المخصصة—قطع صغيرة من البيانات تُخزن داخل المصنف دون إغراق الخلايا الظاهرة.

سنغطي:

* إنشاء خاصية مخصصة في Excel (مثال “ProjectId”).  
* استرجاع قيمة تلك الخاصية المخصصة للتحقق من عملها.  
* حفظ المصنف المعدل كملف **XLSB**، وهو التنسيق الثنائي الذي يقلل حجم الملف ويسرّع أوقات التحميل.  

**المتطلبات المسبقة**

* Java 17 أو أحدث.  
* Aspose.Cells for Java (المكتبة التي تسمح لك بالتعامل مع ملفات Excel دون الحاجة إلى Microsoft Office).  
* رخصة صالحة لـ Aspose.Cells – النسخة التجريبية المجانية تكفي لهذا العرض، لكن الرخصة تزيل علامة التقييم.  

إذا لم تستخدم Aspose.Cells من قبل، لا تقلق. الـ API بسيط، والكود أدناه جاهز للتنفيذ بمجرد إضافة ملف الـ JAR إلى مسار الفئات الخاص بك.

![كيفية إضافة خاصية مخصصة في Excel باستخدام Java](image-url-placeholder "كيفية إضافة خاصية مخصصة في Excel باستخدام Java")

---

## كيفية إضافة خاصية مخصصة – الخطوة 1

أولاً، نحتاج إلى تحميل مصنف موجود (أو إنشاء واحد جديد) ثم إرفاق خاصية مخصصة بالورقة الأولى. الخاصية هي مجرد زوج مفتاح/قيمة يُخزن في مجموعة `CustomProperties` الخاصة بالورقة.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook from a file (you can also create a new workbook)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        // This is the core of how to add custom property in Excel.
        sheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the value of the custom property we just added
        // (We'll also show you how to retrieve custom property value later.)
        Object projectIdValue = sheet.getCustomProperties().get("ProjectId").getValue();

        // Step 5: Display the retrieved value on the console
        System.out.println("ProjectId = " + projectIdValue);

        // Step 6: Save the modified workbook to a new file in XLSB format
        // This demonstrates how to save workbook as XLSB.
        workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
    }
}
```

**لماذا يعمل هذا**

* `Workbook` هو نقطة الدخول لأي ملف Excel—فكر فيه كحاوية لجميع الأوراق، الأنماط، والبيانات الوصفية.  
* `Worksheet.getCustomProperties()` تُعيد مجموعة تتصرف كقاموس؛ استدعاء `.add(name, value)` ينشئ الخاصية إذا لم تكن موجودة.  
* قيمة الخاصية يمكن أن تكون أي نوع بدائي (int, double, String, boolean) – Aspose.Cells يتولى التحويل لك.  

تشغيل البرنامج يطبع:

```
ProjectId = 12345
```

الآن قد أضفت **خاصية مخصصة** بنجاح وتأكدت من وجودها.

---

## استرجاع قيمة الخاصية المخصصة

قد تتساءل، “ماذا لو احتجت لقراءة الخاصية لاحقًا، ربما في وحدة مختلفة؟” مجموعة `CustomProperties` نفسها تتيح لك الجلب بالاسم. المقتطف التالي يوضح **استرجاع قيمة الخاصية المخصصة** دون إعادة إضافتها.

```java
// Assume workbook is already loaded and sheet points to the correct worksheet
CustomPropertyCollection props = sheet.getCustomProperties();

// Check if the property exists to avoid NullPointerException
if (props.contains("ProjectId")) {
    Object value = props.get("ProjectId").getValue();
    System.out.println("Retrieved ProjectId = " + value);
} else {
    System.out.println("ProjectId property not found.");
}
```

**نقاط رئيسية**

* `contains` هو حماية—الكود الواقعي يجب دائمًا التحقق من وجود الخاصية قبل القراءة.  
* الكائن `Object` المرتجع يمكن تحويله إلى النوع المتوقع إذا احتجت عمليات حسابية (مثلاً `(int) value`).  

هذا النمط الصغير يحل معظم سيناريوهات التدقيق حيث تحتاج لسحب البيانات الوصفية من مصنف تم إنشاؤه منذ أسابيع.

---

## حفظ المصنف كـ XLSB

لماذا نختار XLSB على XLSX الأكثر شيوعًا؟ ملفات XLSB الثنائية عادةً **أصغر بنسبة 30‑40 %** وتفتح أسرع، خاصةً مع مجموعات بيانات كبيرة. Aspose.Cells يجعل حفظ هذا التنسيق سطرًا واحدًا، كما هو موضح في **الخطوة 6** من الكود الأول.

إذا أردت الاحتفاظ بالمصنف في الذاكرة (مثلاً لإرساله عبر خدمة ويب)، يمكنك الكتابة إلى `ByteArrayOutputStream` بدلاً من ذلك:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
workbook.save(baos, SaveFormat.XLSB);
byte[] xlsbBytes = baos.toByteArray();
// Now you can attach xlsbBytes to an email, upload to S3, etc.
```

العدد `SaveFormat.XLSB` يضمن التنسيق الثنائي، ونفس الاستدعاء يعمل مع أي مصنف، سواء أضفت خاصية مخصصة أو نفذت حسابات مكثفة.

---

## إنشاء خاصية مخصصة في Excel – مثال كامل من البداية إلى النهاية

فيما يلي برنامج متكامل، مستقل، يجمع بين **كيفية إضافة خاصية مخصصة**، **استرجاع قيمة الخاصية المخصصة**، و**حفظ المصنف كـ XLSB**. يمكنك نسخه ولصقه في بيئة التطوير الخاصة بك، تعديل مسارات الملفات، وتشغيله فورًا.

```java
import com.aspose.cells.*;

public class ExcelCustomPropertyExample {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load an existing XLSB workbook (or create a new one)
            Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

            // 2️⃣ Grab the first worksheet – you could loop through all sheets if needed
            Worksheet sheet = workbook.getWorksheets().get(0);

            // 3️⃣ Create a custom property called "ProjectId"
            // This is the essential step for how to add custom property.
            sheet.getCustomProperties().add("ProjectId", 12345);
            System.out.println("Custom property 'ProjectId' added.");

            // 4️⃣ Retrieve the property to prove it works – demonstrates retrieve custom property value
            CustomPropertyCollection props = sheet.getCustomProperties();
            if (props.contains("ProjectId")) {
                Object val = props.get("ProjectId").getValue();
                System.out.println("Retrieved ProjectId = " + val);
            }

            // 5️⃣ Optionally, add another property (string type) to show flexibility
            sheet.getCustomProperties().add("ReportVersion", "v2.1");
            System.out.println("Added ReportVersion property.");

            // 6️⃣ Save the workbook as an XLSB file – this is the save workbook as XLSB step.
            workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
            System.out.println("Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb");

        } catch (Exception e) {
            // Real‑world code should log the exception; here we just print stack trace.
            e.printStackTrace();
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Custom property 'ProjectId' added.
Retrieved ProjectId = 12345
Added ReportVersion property.
Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb
```

افتح `customOut.xlsb` في Excel، انتقل إلى **File → Info → Properties → Advanced Properties → Custom**، وسترى كلًا من `ProjectId` و `ReportVersion` مدرجة—دليل على أن **إنشاء خاصية مخصصة في Excel** تم بنجاح.

---

## الأخطاء الشائعة & نصائح احترافية

| الخطأ | السبب | الحل |
|-------|--------|------|
| نسيان استدعاء `workbook.save(...)` |  |  |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Excel Workbook Custom Property Management Using Aspose.Cells .NET](/cells/english/net/workbook-operations/excel-workbook-property-management-aspose-cells-net/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}