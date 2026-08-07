---
category: general
date: 2026-07-16
description: إنشاء مصنف جديد ونسخ جدول محوري باستخدام Aspose.Cells للغة Java. تعلم
  كيفية تكرار الجدول المحوري ونسخ نطاق Excel في دقائق.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: ar
lastmod: 2026-07-16
og_description: إنشاء مصنف جديد ونسخ جدول محوري باستخدام Aspose.Cells للغة Java. يوضح
  هذا الدليل كيفية تكرار الجدول المحوري ونسخ نطاق Excel بكفاءة.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: إنشاء دفتر عمل جديد ونسخ جدول محوري في جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: إنشاء دفتر عمل جديد ونسخ جدول محوري في جافا – دليل كامل خطوة بخطوة
url: /ar/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد ونسخ جدول محوري في Java – دليل كامل خطوة‑بخطوة

هل تساءلت يومًا كيف **create new workbook** مع الحفاظ على جدول محوري معقد من ملف موجود؟ إذا وجدت نفسك تنظر إلى ورقة Excel وتفكر “أحتاج هذا الجدول المحوري في مصنف آخر”، ثم تشعر بالحيرة، فأنت لست وحدك. الخبر السار هو أنه باستخدام Aspose.Cells for Java يمكنك تكرار جدول محوري ببضع أسطر فقط.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ **copy pivot table** البيانات، **duplicate pivot table** الهياكل، و**copy Excel range** المحتويات—كل ذلك أثناء إنشاء مصنف جديد من الصفر. في النهاية ستحصل على برنامج Java جاهز للتنفيذ يقوم بما طلبته بالضبط.

## ما ستتعلمه

- كيفية **create new workbook** برمجيًا باستخدام Aspose.Cells.
- الطريقة الدقيقة لتحديد النطاق الذي يحتوي على جدول محوري.
- تقنيات **copy pivot table** و **duplicate pivot table** دون فقدان التنسيق أو اتصالات البيانات.
- كيفية **copy Excel range** بفعالية وحفظ النتيجة.
- المشكلات الشائعة ونصائح التعامل مع جداول محورية كبيرة.

لا حاجة لمراجع خارجية—كل شيء مكتمل، قابل للتنفيذ، ومُشرح.

---

## المتطلبات المسبقة

قبل أن نغوص، تأكد من أنك تمتلك:

1. **Java Development Kit (JDK) 11+** – أي نسخة حديثة تعمل.  
2. **Aspose.Cells for Java** library (أحدث نسخة حتى 2026‑07‑16). يمكنك الحصول عليها من Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. ملف Excel مصدر (`SourceWithPivot.xlsx`) يحتوي بالفعل على جدول محوري تريد نسخه.  
4. بيئة تطوير متكاملة أو محرر نصوص بسيط—IntelliJ IDEA، Eclipse، أو VS Code يكفي.

هل لديك كل ذلك؟ رائع—هيا نبدأ.

## الخطوة 1: **Create New Workbook** وتحميل ملف المصدر

أول شيء نحتاجه هو كائن مصنف جديد سيحمل لاحقًا الجدول المحوري المكرر. في الوقت نفسه يجب تحميل المصنف الأصلي حتى نتمكن من الإشارة إلى نطاق جدول المحوري الخاص به.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **لماذا هذا مهم:**  
> تحميل المصنف المصدر يمنحنا الوصول إلى كائن `Range` الأساسي الذي يحتوي على الجدول المحوري. إذا تخطيت هذه الخطوة لن يكون لديك شيء لتنسخه، وستفشل عملية **duplicate pivot table** بصمت.

## الخطوة 2: تحديد **Copy Excel Range** الذي يحتوي على الجدول المحوري

الجدول المحوري ليس خلية واحدة—إنه يمتد على كتلة مستطيلة. نحتاج إلى إخبار Aspose.Cells بالضبط أي خلايا يجب نسخها.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **نصيحة:**  
> إذا لم تكن متأكدًا من النطاق الدقيق، افتح المصنف المصدر في Excel، حدد الجدول المحوري، وانظر إلى مربع الاسم. سيظهر شيء مثل `A1:G20`. استخدام النطاق الدقيق يضمن احتفاظ جميع إعدادات الحقول، الفلاتر، والحسابات عندما نقوم بـ **copy pivot table** لاحقًا.

## الخطوة 3: **Create New Workbook** الذي سيتلقى الجدول المحوري المنسوخ

الآن ننشئ مصنفًا جديدًا تمامًا—هذا هو المكان الذي سيعيش فيه **duplicate pivot table** الخاص بنا.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **ما الذي يحدث في الخلفية؟**  
> المُنشئ الافتراضي يُنشئ مصنفًا بورقة واحدة فارغة. هذه هي اللوحة النظيفة التي نحتاجها لسيناريو **create new workbook**. لا توجد أنماط متبقية أو أوراق مخفية للقلق بشأنها.

## الخطوة 4: **Copy Pivot Table** – فعليًا نسخ نطاق Excel المحدد

مع جاهزية كل من المصدر والوجهة، نقوم بتنفيذ عملية النسخ. هذه الخطوة تُكمل جزء **how to copy pivot** من اللغز.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **لماذا يعمل `copy` مع الجداول المحورية:**  
> Aspose.Cells يتعامل مع الجدول المحوري كجزء من مجموعة الخلايا. عندما تنسخ النطاق، يتم نقل ذاكرة التخزين المؤقت للجدول المحوري، قائمة الحقول، والتخطيط. النتيجة هي **duplicate pivot table** كامل الوظيفة في المصنف الجديد.

## الخطوة 5: حفظ النتيجة والتحقق من عملية **Copy Pivot Table**

أخيرًا، احفظ المصنف الوجهة على القرص. افتح الملف في Excel لتتأكد من أن الجدول المحوري يظهر تمامًا كما كان في المصدر.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**النتيجة المتوقعة:**  
- يفتح `CopyPivotResult.xlsx` بورقة عمل تحتوي على نفس جدول المحوري الذي رأيته في `SourceWithPivot.xlsx`.  
- جميع تسميات الصفوف/الأعمدة، الفلاتر، والحقول المحسوبة محفوظة.  
- يمكنك الآن تعديل بيانات المصدر بشكل مستقل، وسيحتفظ المصنف الجديد بذاكرة التخزين المؤقت للجدول المحوري الخاصة به.

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان الجدول المحوري المصدر يمتد على أكثر من ورقة؟

Aspose.Cells يمكنه نسخ النطاقات داخل ورقة عمل واحدة في كل مرة. إذا كان جدولك المحوري يمتد عبر أوراق متعددة، سيتعين عليك نسخ كل نطاق ذي صلة على حدة ثم ربطها يدويًا.

### هل يحافظ هذه الطريقة على تنسيقات الأرقام المخصصة؟

نعم. طريقة `copy` تنسخ أنماط الخلايا، بما فيها تنسيقات الأرقام، الخطوط، والألوان. ومع ذلك، إذا كان لديك تنسيق شرطي يشير إلى نطاقات خارجية، تحقق من تلك الإشارات بعد النسخ.

### كيف تنسخ جدولًا محوريًا يستخدم مصدر بيانات خارجي؟

عندما يسحب الجدول المحوري البيانات من اتصال خارجي (مثل استعلام SQL)، لا يتم نقل معلومات الاتصال بواسطة `copy`. ستحتاج إلى إعادة إنشاء مصدر البيانات في المصنف الوجهة أو تضمين بيانات المصدر مسبقًا.

### هل يمكنني نسخ تخطيط الجدول المحوري فقط دون البيانات الأساسية؟

يمكنك تحقيق ذلك أولاً بمسح خلايا البيانات في النطاق المصدر، ثم نسخ تخطيط الجدول المحوري فقط. هذا سيناريو أكثر تقدمًا وعادةً لا يكون مطلوبًا لمهمة **duplicate pivot table** بسيطة.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي الفئة الكاملة الجاهزة للتنفيذ في Java. فقط استبدل `YOUR_DIRECTORY` بمسار المجلد الفعلي على جهازك.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

شغّل البرنامج (`java CopyPivotTableDemo`) وسترى رسالة في وحدة التحكم تؤكد النجاح.

## نصائح احترافية وأفضل الممارسات

- **تحقق من النطاق** قبل النسخ. استخدم `srcWs.getCells().maxDisplayRange` لاكتشاف المنطقة المستخدمة برمجيًا إذا لم ترغب في كتابة `"A1:G20"` يدويًا.  
- **أوقف الحساب** مؤقتًا للمصنفات الضخمة لتسريع عملية النسخ:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **حرّر الموارد** (`srcWb.dispose(); dstWb.dispose();`) في الخدمات طويلة التشغيل لتجنب تسرب الذاكرة.  
- **توافق الإصدارات:** يعمل الكود مع Aspose.Cells 23.12 وما بعده. قد تتطلب الإصدارات الأقدم `srcRange.copyTo` بدلاً من `copy`.

## الخطوات التالية

الآن بعد أن أتقنت **create new workbook** و **copy pivot table**، يمكنك استكشاف:

- **كيفية نسخ الجدول المحوري** عبر أوراق عمل متعددة في مهمة دفعة.  
- إضافة **copy excel range** للجداول العادية إلى جانب الجدول المحوري.  
- أتمتة إنشاء **duplicate pivot table** لكل تقرير شهري باستخدام حلقة.  
- تصدير الجدول المحوري المكرر إلى PDF أو HTML باستخدام أدوات العرض المدمجة في Aspose.Cells.

كل من هذه المواضيع يبني على الأساس الذي وضعناه هنا، وتستفيد جميعها من النهج البرمجي النظيف نفسه.

## الخلاصة

لقد استعرضنا العملية الكاملة لـ **create new workbook**، تحديد **copy excel range** المصدر، و**copy pivot table** لإنتاج **duplicate pivot table** في Java باستخدام Aspose.Cells. الحل مختصر، كامل الوظيفة، وجاهز للاستخدام في بيئات الإنتاج. لا تتردد في تعديل النطاق، تجربة ملفات مصدر مختلفة، أو دمج هذه المنطق في خط أنابيب تقارير أكبر.

إذا واجهت أي صعوبات أو كان لديك أفكار لتوسيع هذا الدرس، اترك تعليقًا أدناه. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء جداول محورية في Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [كيفية تحديث مصدر جدول محوري Excel باستخدام Aspose.Cells for Java: دليل شامل](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [معالجة جداول محورية Excel باستخدام Aspose.Cells Java: دليل شامل](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}