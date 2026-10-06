---
category: general
date: 2026-06-18
description: تعيين اسم للخلية في إكسل باستخدام جافا – دليل خطوة بخطوة لإضافة نطاق
  مسمى في إكسل، إنشاء خلية مسماة، تحديد اسم للخلية، وحفظ المصنف بصيغة XLSX.
draft: false
keywords:
- assign name to cell
- add named range excel
- save workbook as xlsx
- create named cell
- define name for cell
language: ar
og_description: تعيين اسم للخلية في Excel باستخدام Java. تعلم كيفية إضافة نطاق مسمى
  في Excel، إنشاء خلية مسماة، تعريف اسم للخلية، وحفظ المصنف بصيغة XLSX.
og_title: تعيين اسم للخلية في إكسل باستخدام جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Assign name to cell in Excel with Java – step-by-step guide to add
    named range Excel, create named cell, define name for cell, and save workbook
    as XLSX.
  headline: Assign Name to Cell in Excel Using Java – Complete Guide
  type: TechArticle
- description: Assign name to cell in Excel with Java – step-by-step guide to add
    named range Excel, create named cell, define name for cell, and save workbook
    as XLSX.
  name: Assign Name to Cell in Excel Using Java – Complete Guide
  steps:
  - name: Creates a workbook.
    text: Creates a workbook.
  - name: Assigns three different names (single cell, range, local name).
    text: Assigns three different names (single cell, range, local name).
  - name: Populates a few cells with sample data.
    text: Populates a few cells with sample data.
  - name: Saves the result as `named_cells_demo.xlsx`.
    text: Saves the result as `named_cells_demo.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: تعيين اسم للخلية في إكسل باستخدام جافا – دليل كامل
url: /ar/java/range-management/assign-name-to-cell-in-excel-using-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين اسم للخلية في Excel باستخدام Java – دليل كامل

هل تساءلت يومًا كيف **assign name to cell** في ورقة عمل Excel دون فتح الواجهة الرسومية؟ لست وحدك. يحتاج العديد من المطورين إلى طريقة برمجية لتوسيم خلية واحدة بحيث يمكن للصيغ والكود الآخر الإشارة إليها بمعرف سهل. في هذا الدرس سنستعرض حلًا نظيفًا بلغة Java لا يقتصر فقط على تعيين اسم للخلية بل يوضح لك أيضًا **add named range Excel**، **create named cell**، وأخيرًا **save workbook as XLSX**.

تخيل أنك تبني محرك تقارير يجلب إجماليات المبيعات من *Sheet1!A1* كل ليلة. كتابة العنوان مباشرةً صلبة؛ الخلية المسماة تجعل المنطق مرنًا أمام تغييرات التخطيط المستقبلية. بنهاية هذا الدليل ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Java يستخدم Aspose.Cells.

## المتطلبات المسبقة

- Java 17 (أو أي JDK حديث) مثبت.
- مكتبة Aspose.Cells for Java (الإصدار 23.9 أو أحدث) مضافة إلى classpath الخاص بالمشروع.
- فهم أساسي لصياغة Java—لا حاجة لأي شيء معقد.

إذا كنت تفتقد المكتبة، احصل عليها من Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

الآن، دعنا نبدأ العمل.

![مخطط تعيين اسم للخلية](assign-name-cell.png)

## تعيين اسم للخلية باستخدام Aspose.Cells (Java)

جوهر العملية هو ثلاث أسطر فقط، لكن كل سطر يلعب دورًا حاسمًا. أدناه المثال الكامل القابل للتنفيذ الذي ينشئ مصنفًا جديدًا، يعيّن اسمًا للخلية **A1**، ويحفظ الملف باسم **output.xlsx**.

```java
import com.aspose.cells.*;

public class AssignNameToCellDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // empty workbook
        Worksheet ws = workbook.getWorksheets().get(0);   // first (default) sheet

        // Step 2: Define a name that points to cell A1 on Sheet1
        // This is the “assign name to cell” operation.
        // If a name called "Sales" already exists, an exception will be thrown.
        ws.getNames().add("Sales", "=Sheet1!$A$1");

        // Optional: put a value in the cell so you can see it later
        ws.getCells().get("A1").putValue(12345);

        // Step 3: Save the workbook as an XLSX file
        workbook.save("output.xlsx", SaveFormat.XLSX);
    }
}
```

### لماذا يعمل هذا

- **Workbook & Worksheet** – `Workbook` هو الحاوية لجميع الأوراق. بشكل افتراضي ينشئ *Sheet1*، وهذا هو السبب في أن الصيغة `=Sheet1!$A$1` تعمل مباشرة.
- **Names collection** – `ws.getNames()` تُرجع مجموعة الأسماء المعرفة المقتصرة على ورقة العمل. استدعاء `add` ينشئ الاسم **Sales** ويربطه بالمرجع المطلق `A1`. هذا هو جوهر **define name for cell**.
- **Save format** – تمرير `SaveFormat.XLSX` يخبر Aspose.Cells بكتابة ملف Office Open XML حديث، مما يلبي متطلب **save workbook as xlsx**.

إذا شغلت البرنامج، ستجد `output.xlsx` في دليل العمل الخاص بك. افتحه في Excel، انتقل إلى *Formulas → Name Manager*، وستجد **Sales** يشير إلى *Sheet1!$A$1*. بسيط، أليس كذلك؟

## إضافة نطاق مسمى Excel – ما وراء الخلية الواحدة

النطاق المسمى لا يقتصر على عنوان واحد. افترض أنك لاحقًا تحتاج إلى الإشارة إلى كتلة بيانات (مثلاً *B2:C10*). نفس استدعاء API يعمل؛ كل ما عليك هو تغيير سلسلة الصيغة:

```java
ws.getNames().add("QuarterlyData", "=Sheet1!$B$2:$C$10");
```

ذلك السطر **adds named range Excel** لكتلة متعددة الخلايا، موضحًا مدى مرونة طريقة `add`. يمكنك حتى تحديد نطاق الاسم على مستوى المصنف بدلاً من ورقة واحدة باستخدام `workbook.getWorksheets().getNames()`.

## حفظ المصنف كملف XLSX – ماذا عن التوافق؟

بينما يستخدم المثال `SaveFormat.XLSX`، يدعم Aspose.Cells العديد من الصيغ: `XLS`، `CSV`، `ODS`، `PDF`، وأكثر. اختيار XLSX يضمن أقصى توافق مع إصدارات Office الحديثة وخدمات السحابة مثل OneDrive. إذا احتجت إلى فرض نسخة Excel محددة، يمكنك أيضًا ضبط `WorkbookSettings`:

```java
workbook.getSettings().setExcelVersion(ExcelVersion.EXCEL_2016);
```

هذا التعديل الصغير يضمن أن الملف يفتح دون تحذير في إصدارات Excel القديمة.

## إنشاء خلية مسماة – الأخطاء الشائعة

عند **create named cell** برمجيًا، احذر من هذه المشكلات:

| المشكلة | سبب الأهمية | الحل |
|---------|----------------|-----|
| اسم مكرر | Aspose.Cells يرمي `ArgumentException` إذا كان المعرف موجودًا بالفعل. | تحقق من `ws.getNames().contains("MyName")` قبل الإضافة، أو احطها بـ try/catch وأعد التسمية. |
| إشارة إلى ورقة خاطئة | استخدام `Sheet2` في الصيغة بينما الخلية موجودة على `Sheet1` يؤدي إلى أخطاء #REF!. | بنِ الصيغة ديناميكيًا: `String formula = "=Sheet1!$" + column + "$" + row;` |
| مشاكل اللغة | بعض اللغات تستخدم الفواصل بدلاً من الفواصل المنقوطة في الصيغ. | استخدم نمط A1 العالمي (`=Sheet1!$A$1`) الذي تقوم Aspose.Cells بتطبيعه. |

بتوقع هذه الأمور، يصبح منطق **assign name to cell** قويًا جدًا.

## تعريف اسم للخلية – نصائح متقدمة

إذا كنت بحاجة إلى أن يكون الاسم *محليًا* لورقة (مرئيًا فقط عندما تكون الورقة نشطة)، استخدم مجموعة `Names` على مستوى المصنف وحدد النطاق صراحةً:

```java
Name localName = workbook.getWorksheets().getNames().add("LocalTotal");
localName.setRefersToFormula("=Sheet1!$A$1");
localName.setScope(ws); // limits visibility to Sheet1
```

هذا النهج مفيد عندما يكون لديك العديد من الأوراق كل منها يحتوي على خلية “Total” الخاصة به—بدون تصادمات في الأسماء، ويمكن لكل ورقة الإشارة إلى **define name for cell** الخاص بها دون غموض.

## مثال كامل من البداية إلى النهاية

بجمع كل شيء معًا، إليك برنامج مستقل يقوم بـ:

1. إنشاء مصنف.
2. تعيين ثلاثة أسماء مختلفة (خلية واحدة، نطاق، اسم محلي).
3. ملء بعض الخلايا ببيانات تجريبية.
4. حفظ النتيجة كـ `named_cells_demo.xlsx`.

```java
import com.aspose.cells.*;

public class NamedCellDemo {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // Populate sample data
        cells.get("A1").putValue(5000);          // Sales total
        cells.get("B2").putValue(120);
        cells.get("C2").putValue(130);
        cells.get("B3").putValue(140);
        cells.get("C3").putValue(150);

        // 1️⃣ Assign name to a single cell (Sales)
        ws.getNames().add("Sales", "=Sheet1!$A$1");

        // 2️⃣ Add named range for a block of data (QuarterlyData)
        ws.getNames().add("QuarterlyData", "=Sheet1!$B$2:$C$3");

        // 3️⃣ Define a local name visible only on Sheet1 (LocalTotal)
        Name local = wb.getWorksheets().getNames().add("LocalTotal");
        local.setRefersToFormula("=Sheet1!$A$1");
        local.setScope(ws);

        // Save the workbook
        wb.save("named_cells_demo.xlsx", SaveFormat.XLSX);
    }
}
```

**النتيجة المتوقعة:** افتح `named_cells_demo.xlsx` → *Formulas → Name Manager* → ستظهر ثلاث إدخالات: **Sales**، **QuarterlyData**، و**LocalTotal**. اختيار كل منها سيُبرز الخلايا المشار إليها في الورقة.

## نصائح احترافية وحالات حافة

- **Performance tip:** إذا كنت تضيف العشرات من الأسماء داخل حلقة، عطل تحديث الشاشة: `wb.getSettings().setScreenUpdating(false);` وأعد تمكينه بعد الانتهاء.
- **Thread safety:** كائنات Aspose.Cells **ليست** آمنة للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة من `Workbook` لكل خيط.
- **Cross‑workbook references:** للإشارة إلى اسم في مصنف آخر، استخدم صيغة المرجع الخارجي: `=‘[OtherBook.xlsx]Sheet1’!$A$1`. يعمل ذلك عندما يكون الملفان محفوظين في نفس المجلد.
- **Unicode names:** يمكنك استخدام أحرف غير ASCII (مثل “销售额”) طالما أن نسخة Excel الأساسية تدعمها. اختبر ذلك بفتح سريع في Excel للتأكد.

## الخاتمة

في هذا الدليل نحن

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تحويل أسماء خلايا Excel إلى مؤشرات باستخدام Aspose.Cells for Java: دليل خطوة بخطوة](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [إتقان معالجة خلايا المصنف مع Aspose.Cells في Java: دليل كامل لأتمتة Excel](/cells/english/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [تكرار مصنفات Excel والخلايا باستخدام Aspose.Cells Java: دليل المطور](/cells/english/java/workbook-operations/excel-operations-aspose-cells-java-workbook-cell-iteration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}