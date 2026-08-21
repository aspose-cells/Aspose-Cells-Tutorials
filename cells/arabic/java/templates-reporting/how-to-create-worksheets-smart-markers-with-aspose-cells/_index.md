---
category: general
date: 2026-08-20
description: إنشاء علامات ذكية في أوراق العمل باستخدام Java و Aspose.Cells والتحكم
  في تسمية ورقة التفاصيل باستخدام SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: ar
lastmod: 2026-08-20
og_description: إنشاء علامات ذكية للورقات في Java باستخدام Aspose.Cells. تعلم كيفية
  تسمية أوراق التفاصيل ديناميكياً باستخدام SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: إنشاء علامات ذكية لأوراق العمل – دليل Java مع Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: كيفية إنشاء علامات ذكية في أوراق العمل باستخدام Aspose.Cells
url: /ar/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء علامات ذكية لأوراق العمل باستخدام Aspose.Cells

إذا كنت بحاجة إلى **إنشاء علامات ذكية لأوراق العمل** في مصنف Java، يوضح لك هذا الدليل الخطوات الدقيقة للقيام بذلك باستخدام Aspose.Cells. سترى كيفية تكوين `SmartMarkerOptions` بحيث يحصل كل ورقة تفصيلية على اسم فريد ومتوقع.

إنشاء تقارير Excel التي توسّع قالب رئيس‑تفصيل هو مطلب شائع في أنظمة المالية، المخزون، والتقارير. استخدام العلامات الذكية يلغي الحاجة إلى تكرار الأوراق يدويًا ويسمح لك بالتركيز على البيانات بدلاً من التفاصيل التقنية.

## ما ستتعلمه

* كيفية تحميل مصنف رئيسي يحتوي على علامات ذكية.  
* كيفية ضبط `SmartMarkerOptions` للتحكم في تسمية أوراق التفصيل التي يتم إنشاؤها.  
* كيفية توفير `DataTable` ببيانات عينة وتطبيقها على العلامات الذكية.  
* كيفية حفظ النتيجة بحيث يكون لكل ورقة تفصيلية اسم مميز، مما يتجنب تكرار أسماء الأوراق.

**المتطلبات المسبقة**  
* Java 17 أو أحدث (الكود يتوافق أيضًا مع JDK 8+).  
* Aspose.Cells for Java 23.9 أو أحدث – المكتبة توفر الفئات `Workbook`، `SmartMarkerOptions`، والفئات المرتبطة.  
* بيئة تطوير متكاملة مثل IntelliJ IDEA، Eclipse، أو VS Code.

المفاهيم الثانوية التي ستصادفها تشمل **Aspose.Cells Java**، **smart marker options**، ومعالجة **duplicate sheet names** عندما يتم توسيع القالب.

## إنشاء علامات ذكية لأوراق العمل – دليل خطوة بخطوة

الأقسام التالية تقسم العملية إلى خطوات منفصلة وقابلة لإعادة الاستخدام. كل خطوة تتضمن مقتطف كود، شرح لأهميتها، ونصائح عملية لتجنب الأخطاء الشائعة.

### الخطوة 1: إعداد مشروع Maven وإضافة Aspose.Cells

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**لماذا هذه الخطوة مهمة** – المكتبة توفر الفئة `Workbook` التي تقرأ وتكتب ملفات Excel، بالإضافة إلى محرك العلامات الذكية الذي يوسّع القالب تلقائيًا. بدون الاعتماد الصحيح، لا يستطيع المترجم حل استدعاءات API المستخدمة لاحقًا.

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، قم بتكوين `settings.xml` الخاص بـ Maven لسحب مستودع Aspose بأمان.

### الخطوة 2: تحميل المصنف الرئيسي الذي يحتوي على العلامات الذكية

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**لماذا هذه الخطوة مهمة** – المصنف الرئيسي يحدد التخطيط، الصيغ، وعلامات العنصر النائب (`«SmartMarker»`) التي سيستبدلها المحرك. تحميل الملف مرة واحدة يحافظ على استهلاك الذاكرة منخفضًا ويسمح لك بإعادة استخدام نفس المصنف لمجموعات بيانات متعددة.

### الخطوة 3: تكوين SmartMarkerOptions لأسماء أوراق تفصيل مخصصة

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**لماذا هذه الخطوة مهمة** – بشكل افتراضي، تقوم Aspose.Cells بإنشاء أوراق تفصيل بأسماء عامة مثل “DetailSheet”. عندما يتم توسيع القالب لعدد كبير من الصفوف، تتصادم هذه الأسماء، مما يؤدي إلى **duplicate sheet names** واستثناء وقت التشغيل. النمط `"DetailSheet_{0}"` يضمن اسمًا فريدًا لكل صف، مما يحل مشكلة التكرار.

### الخطوة 4: بناء DataTable يتطابق مع حقول العلامة الذكية

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**لماذا هذه الخطوة مهمة** – الـ `DataTable` يزود القيم الفعلية التي تستبدل علامات العنصر النائب. يجب أن تتطابق أسماء الأعمدة مع أسماء العلامات في القالب؛ وإلا سيتخطى المحرك الاستبدال بصمت.

> **خطأ شائع:** استخدام اسم عمود يختلف في حالة الأحرف (مثال: “id” مقابل “Id”) يؤدي إلى فقدان البيانات في الأوراق التي تم إنشاؤها.

### الخطوة 5: تطبيق البيانات على العلامات الذكية مع خيارات التسمية

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**لماذا هذه الخطوة مهمة** – طريقة `apply` تُطلق محرك العلامات الذكية. هي تقرأ كل صف، تنشئ ورقة تفصيل جديدة باستخدام نمط التسمية من `SmartMarkerOptions`، وتملأ الورقة ببيانات ذلك الصف. هذه الدعوة الواحدة تستبدل عشرات الأسطر من استنساخ الأوراق وتعبئة الخلايا يدويًا.

### الخطوة 6: حفظ المصنف والتحقق من النتيجة

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

بعد التنفيذ، افتح `MasterDetailDuplicatedNames.xlsx`. يجب أن ترى:

* ورقة الماستر الأصلية دون تغيير.  
* ورقتين جديدتين باسم `DetailSheet_1` و `DetailSheet_2`.  
* كل ورقة تفصيل تحتوي على القيم من الصف المقابل في الـ `DataTable`.

**لماذا هذه الخطوة مهمة** – حفظ المصنف ينهى عملية توسيع العلامات الذكية. يمكن الآن إرسال الملف إلى الأنظمة المت downstream، إرفاقه بالبريد الإلكتروني، أو فتحه في Excel لمزيد من التحليل.

## التعامل مع الحالات الطرفية والاختلافات

### عدة أوراق ماستر

إذا كان القالب يحتوي على أكثر من ورقة ماستر، قم بالتكرار عبر علامات الذكية في كل ورقة:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### تسمية مخصصة تتجاوز فهرس الصف

يمكنك دمج أي عمود بيانات في اسم الورقة باستخدام عناصر نائبة مثل `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

تأكد من وجود العمود `OrderId` في الـ `DataTable` المقدم.

### منع أسماء الأوراق الطويلة جدًا

Excel يحدّ أسماء الأوراق إلى 31 حرفًا. إذا كان نمط التسمية قد يتجاوز هذا الحد، قص أو احصر القيمة:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

ثم عالج الاسم المُولد باستخدام `StringUtils.abbreviate` قبل تمريره إلى Aspose.

## مثال كامل قابل للتنفيذ

فيما يلي ملف المصدر الكامل الذي يمكنك نسخه، تعديل مسارات الملفات، وتشغيله مباشرة:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**الناتج المتوقع**

* يحتوي `MasterDetailDuplicatedNames.xlsx` على:

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [إتقان Aspose.Cells Java: استخدام العلامات الذكية للبيانات الديناميكية في أوراق العمل](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [إنشاء مخططات ديناميكية باستخدام العلامات الذكية في Aspose.Cells for Java | دليل خطوة بخطوة](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Smart Markers Worksheets](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}