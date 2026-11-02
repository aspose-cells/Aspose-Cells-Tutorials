---
category: general
date: 2026-06-21
description: إنشاء عدة أوراق في Excel باستخدام Java. تعلم كيفية تصدير البيانات إلى
  الأوراق، واستخدام نهج Excel القائم على القالب، وحفظ ملف العمل بصيغة xlsx بكفاءة.
draft: false
keywords:
- create multiple sheets
- export data to sheets
- template based excel
- save workbook xlsx
- insert index worksheet
language: ar
og_description: إنشاء عدة أوراق في Excel باستخدام Java. يوضح هذا الدليل كيفية تصدير
  البيانات إلى الأوراق، وتطبيق سير عمل Excel القائم على القالب، وحفظ المصنف بصيغة
  xlsx.
og_title: إنشاء أوراق متعددة في إكسل باستخدام جافا – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiple sheets in Excel using Java. Learn how to export data
    to sheets, use a template based Excel approach, and save workbook xlsx efficiently.
  headline: Create Multiple Sheets in Excel with Java – Complete Template‑Based Guide
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Automation
title: إنشاء أوراق متعددة في إكسل باستخدام جافا – دليل شامل يعتمد على القوالب
url: /ar/java/worksheet-management/create-multiple-sheets-in-excel-with-java-complete-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء أوراق متعددة في Excel باستخدام Java – دليل كامل قائم على القوالب

هل احتجت يومًا إلى **إنشاء أوراق متعددة** في مصنف Excel من تطبيق Java لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. سواء كنت تبني محرك تقارير، أداة تصدير بيانات، أو مجرد محاولة لأتمتة مهمة جدول بيانات مرهقة، فإن إتقان كيفية *تصدير البيانات إلى الأوراق* يمكن أن يوفر لك ساعات من العمل اليدوي.

في هذا الدرس سنستعرض حل **Excel قائم على القوالب** يتيح لك إدراج ورقة فهرس، إنشاء ورقة لكل عنصر بيانات، وأخيرًا **حفظ المصنف بصيغة xlsx** باستدعاء طريقة واحدة. لا إطالة، مجرد مثال عملي من البداية إلى النهاية يمكنك إدراجه في مشروعك اليوم.

## ما ستتعلمه

- كيفية تهيئة مصنف سيحمل **أوراق متعددة**.
- استخدام صيغة Aspose.Cells Smart Marker لتكرار أوراق العمل تلقائيًا.
- إعداد مصدر البيانات (قائمة من الخرائط، POJOs، أو أي مجموعة) للقالب.
- تطبيق القالب باستخدام `SmartMarkerProcessor`.
- حفظ النتيجة كملف **xlsx**.
- نصائح اختيارية لإدراج ورقة فهرس ومعالجة الحالات الخاصة.

*المتطلبات المسبقة*: Java 8+، Maven أو Gradle، ومكتبة Aspose.Cells for Java (الإصدار التجريبي المجاني يعمل جيدًا للاختبار). إذا كنت جديدًا على Aspose، لا تقلق—سنبقي خطوات الإعداد مختصرة.

---

## الخطوة 1: تهيئة المصنف – القالب لـ **إنشاء أوراق متعددة**

قبل ظهور أي أوراق، تحتاج إلى كائن `Workbook`. فكر فيه كقالب فارغ سيحمل لاحقًا كل ورقة عمل مُنشأة.

```java
import com.aspose.cells.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty workbook that will hold the generated worksheets
        Workbook workbook = new Workbook();
        // ... we'll add more code here later
    }
}
```

> **لماذا هذا مهم:** كائن `Workbook` يُجسد ملف Excel بالكامل. ببدء مصنف فارغ، تحتفظ بالتحكم الكامل في إنشاء الأوراق، التنسيق، والحفظ النهائي.

---

## الخطوة 2: تعريف علامة **Excel قائم على القالب** – المخطط لكل ورقة

محرك Smart Marker في Aspose.Cells يتيح لك تضمين نواقل مكانية مباشرةً في قالب نصي. العلامة الخاصة `${#WorksheetRepeat}` تخبر المعالج ببدء **ورقة عمل جديدة** لكل عنصر في مجموعة البيانات.

```java
// Step 2: Define a Smart Marker template.
// ${#WorksheetRepeat} starts a new worksheet for each item in the data collection.
// ${Index} inserts the current item index, and ${Data} inserts the item value.
String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";
```

> **نصيحة احترافية:** حرف `\n` يُنشئ سطرًا جديدًا بعد اسم الورقة، لذا الصف الأول من كل ورقة سيحمل قيمة البيانات الفعلية. عدل القالب لتضمين رؤوس، صيغ، أو تنسيقات حسب الحاجة.

---

## الخطوة 3: إعداد مصدر البيانات – **تصدير البيانات إلى الأوراق** بسهولة

القالب يعمل مع أي مجموعة يمكن لـ Aspose التكرار عليها. في هذا المثال سنستخدم `List<Map<String,Object>>`، لكن يمكنك بسهولة تمرير قائمة من POJOs.

```java
// Step 3: Prepare the data source (a list of maps, objects, etc.).
// Replace this with your actual data collection.
List<Map<String, Object>> dataList = getData(); // placeholder for your data
```

إليك تنفيذ تجريبي سريع يمكنك نسخه ولصقه أثناء الاختبار:

```java
private static List<Map<String, Object>> getData() {
    List<Map<String, Object>> list = new ArrayList<>();
    for (int i = 1; i <= 5; i++) {
        Map<String, Object> row = new HashMap<>();
        row.put("Data", "Row value " + i);
        list.add(row);
    }
    return list;
}
```

> **لماذا الخريطة؟** استخدام خريطة يزودك بأزواج مفتاح‑قيمة تتطابق مع الناقل `${Data}`. إذا كنت تفضل POJOs، فقط تأكد من توافق أسماء الحقول مع العلامات الخاصة بك.

---

## الخطوة 4: تهيئة **SmartMarkerProcessor** – المحرك وراء السحر

الآن بعد أن لدينا مصنفًا وقالبًا، نحتاج إلى المعالج الذي سيجمعهما معًا.

```java
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

المعالج يقرأ القالب، يتكرر على `dataList`، وينشئ ورقة عمل جديدة لكل إدخال. لا حاجة للتكرار اليدوي.

---

## الخطوة 5: تطبيق القالب – **إدراج ورقة فهرس** وإنشاء الأوراق

في هذه المرحلة يمكنك ببساطة استدعاء `processor.apply(template, dataList);`. ومع ذلك، يرغب العديد من المستخدمين أيضًا في **ورقة فهرس** تُدرج جميع أسماء الأوراق المُنشأة بروابط قابلة للنقر. أدناه نهج من خطوتين:

1. **إنشاء أوراق البيانات** باستخدام القالب.
2. **إنشاء ورقة فهرس** وتعبئتها بروابط تشعبية.

```java
// Step 5a: Apply the template to the data.
// A new worksheet is created for each element in dataList.
processor.apply(template, dataList);

// Step 5b (optional): Insert an index worksheet at the beginning.
Worksheet indexSheet = workbook.getWorksheets().add("Index");
int row = 0;
indexSheet.getCells().setColumnWidth(0, 25);
indexSheet.getCells().setColumnWidth(1, 30);
indexSheet.getCells().setRowHeight(row, 20);
indexSheet.getCells().get(row, 0).setValue("Sheet Name");
indexSheet.getCells().get(row, 1).setValue("Link");

// Loop through generated sheets and add a hyperlink entry.
for (int i = 0; i < dataList.size(); i++) {
    String sheetName = "Sheet" + (i + 1);
    row++;
    indexSheet.getCells().get(row, 0).setValue(sheetName);
    // Create a hyperlink that points to the generated worksheet.
    Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
            "'" + sheetName + "'!A1", "Go to " + sheetName);
    indexSheet.getCells().get(row, 1).setValue("Open");
}
```

> **شرح:**  
> - الحلقة تبني جدولًا منظمًا حيث يربط كل صف بالورقة المقابلة.  
> - استخدام `Hyperlink.add` يضمن مرجعًا قابلًا للنقر داخل Excel.  
> - هذه الخطوة تُظهر **إدراج ورقة فهرس** عمليًا، مما يجعل التنقل سهلًا للمستخدمين النهائيين.

---

## الخطوة 6: **حفظ المصنف بصيغة Xlsx** – استدعاء واحد، جاهز للتوزيع

أخيرًا، اكتب المصنف إلى القرص. طريقة `save` تكتشف تلقائيًا تنسيق الملف من الامتداد.

```java
// Step 6: Save the workbook to a file
workbook.save("YOUR_DIRECTORY/output.xlsx");
System.out.println("Workbook saved successfully!");
```

> **نصيحة:** إذا كنت بحاجة إلى بث الملف مباشرةً إلى استجابة HTTP (مثلاً في متحكم Spring)، استخدم `workbook.save(outputStream, SaveFormat.XLSX);` بدلاً من ذلك.

---

## مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج الكامل الذي يجمع كل الأجزاء معًا. فقط استبدل `"YOUR_DIRECTORY"` بمسار حقيقي على جهازك.

```java
import com.aspose.cells.*;
import java.util.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Initialise an empty workbook (Step 1)
        Workbook workbook = new Workbook();

        // Define the Smart Marker template (Step 2)
        String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";

        // Prepare data (Step 3)
        List<Map<String, Object>> dataList = getData();

        // Initialise the processor (Step 4)
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Apply template (Step 5a)
        processor.apply(template, dataList);

        // Optional: Insert an index worksheet (Step 5b)
        Worksheet indexSheet = workbook.getWorksheets().add("Index");
        int row = 0;
        indexSheet.getCells().setColumnWidth(0, 25);
        indexSheet.getCells().setColumnWidth(1, 30);
        indexSheet.getCells().setRowHeight(row, 20);
        indexSheet.getCells().get(row, 0).setValue("Sheet Name");
        indexSheet.getCells().get(row, 1).setValue("Link");

        for (int i = 0; i < dataList.size(); i++) {
            String sheetName = "Sheet" + (i + 1);
            row++;
            indexSheet.getCells().get(row, 0).setValue(sheetName);
            Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
                    "'" + sheetName + "'!A1", "Go to " + sheetName);
            indexSheet.getCells().get(row, 1).setValue("Open");
        }

        // Save the workbook (Step 6)
        workbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Workbook saved successfully!");
    }

    // Mock data generator
    private static List<Map<String, Object>> getData() {
        List<Map<String, Object>> list = new ArrayList<>();
        for (int i = 1; i <= 5; i++) {
            Map<String, Object> row = new HashMap<>();
            row.put("Data", "Row value " + i);
            list.add(row);
        }
        return list;
    }
}
```

**الناتج المتوقع:**  
- ملف `output.xlsx` يحتوي على ست أوراق عمل (`Index`, `Sheet1` … `Sheet5`).  
- ورقة `Index` تُدرج كل اسم ورقة تم إنشاؤه مع رابط “Open” قابل للنقر.  
- كل `SheetX` يحتوي على خلية واحدة (`A1`) بها “Row value X”.

---

## الأسئلة الشائعة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخدام مصدر CSV أو JSON بدلاً من `List<Map>`؟** | بالتأكيد. يعمل Smart Marker في Aspose مع أي مجموعة `Iterable`. فقط قم بربط حقول JSON بأسماء العلامات. |
| **ماذا لو كانت قائمة البيانات فارغة؟** | سيُنشئ المعالج لا أوراق عمل إضافية، لكن ستظل ورقة الفهرس مضافة (قد ترغب في الحماية من ذلك). |
| **كيف يمكنني إضافة رؤوس أو تنسيق لكل ورقة مُنشأة؟** | قم بتمديد القالب: `"${#WorksheetRepeat}Sheet${Index}\nHeader1,Header2\n${Data}"`. يمكنك أيضًا تطبيق نمط برمجيًا بعد `apply`. |
| **هل هناك حد لعدد الأوراق؟** | عمليًا، يحد Excel من 1,048,576 صفًا لكل ورقة؛ عدد الأوراق محدود فقط بالذاكرة. |
| **هل أحتاج إلى ترخيص لـ Aspose.Cells؟** | التقييم المجاني يعمل للتطوير. للإنتاج، الترخيص يزيل علامة التقييم ويفتح جميع المميزات. |

---

## الخلاصة

أصبح لديك الآن تدفق عمل قوي لإنشاء **أوراق متعددة** في Java يعتمد على نهج **Excel قائم على القوالب**، **يصدّر البيانات إلى الأوراق**، ويمكنه اختياريًا **إدراج ورقة فهرس**، وأخيرًا **يحفظ المصنف بصيغة xlsx** بسطر واحد من الشيفرة. هذا النمط يتوسع بسلاسة—from عدد قليل من الصفوف إلى تصديرات بيانات ضخمة—مع الحفاظ على نظافة وصيانة الكود.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة تنسيق شرطي، دمج مخططات، أو دمج الفهرس مع لوحة ملخص. يمكن لمحرك Smart Marker نفسه التعامل مع هذه السيناريوهات ببضع علامات إضافية فقط.

إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو استكشف وثائق Aspose.Cells الواسعة. برمجة سعيدة، واستمتع بأتمتة تلك الجداول!

## ماذا يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء والوصول إلى أوراق Excel، إضافة إشارات PDF باستخدام Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [تصدير أوراق Excel إلى صور باستخدام Aspose.Cells for Java - دليل شامل](/cells/english/java/workbook-operations/export-excel-sheets-images-aspose-cells-java/)
- [كيفية إنشاء وتصدير Excel إلى HTML باستخدام Aspose.Cells Java | دليل عمليات المصنف](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}