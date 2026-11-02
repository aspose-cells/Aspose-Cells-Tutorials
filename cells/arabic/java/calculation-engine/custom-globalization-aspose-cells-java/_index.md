---
date: '2026-08-16'
description: تعلم كيفية إضافة العولمة في Java باستخدام Aspose.Cells، وتخصيص رسائل
  خطأ Excel، وإعداد تبعية Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: تعلم كيفية إضافة العولمة في Java باستخدام Aspose.Cells، وتخصيص رسائل
  خطأ Excel، وإعداد تبعية Maven. اتبع الدليل خطوة بخطوة.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: كيفية إضافة العولمة في Java باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: كيفية إضافة العولمة في Java باستخدام Aspose.Cells
url: /ar/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة العولمة في Java باستخدام Aspose.Cells

## مقدمة

إضافة العولمة إلى دفتر عمل Java الخاص بك تتيح لك عرض رسائل الأخطاء، القيم المنطقية، وغيرها من السلاسل الخاصة بالمحلية باللغة التي يتوقعها المستخدمون. في هذا البرنامج التعليمي ستتعلم **كيفية إضافة العولمة** للغة الروسية، لكن النمط نفسه يعمل مع أي لغة. في نهاية الدليل ستكون قادرًا على:

- تجاوز نص الخطأ الافتراضي وتمثيلات القيم المنطقية.
- تطبيق الإعدادات المخصصة الخاصة بك على أي كائن `Workbook`.
- دمج الحل في مشروع Java نموذجي يعتمد على Maven.

هل أنت مستعد لجعل ملفات Excel الخاصة بك متعددة اللغات حقًا؟ دعنا أولاً نتأكد من أن بيئة التطوير الخاصة بك تلبي المتطلبات المسبقة.

## إجابات سريعة

- **ما هي العولمة في Aspose.Cells؟** إنها مجموعة من السلاسل المتوافقة مع اللغة (الأخطاء، القيم المنطقية، إلخ) التي يمكنك استبدالها بنص مخصص.  
- **ما هو العنصر (artifact) المطلوب في Maven؟** `com.aspose:aspose-cells:25.3`.  
- **هل يمكنني استهداف لغات غير الروسية؟** نعم – قم بتمديد `GlobalizationSettings` وتجاوز الطرق المطلوبة لكل لغة.  
- **هل أحتاج إلى ترخيص للتطوير؟** النسخة التجريبية المجانية تعمل للاختبار؛ الترخيص الدائم يزيل علامات التقييم.  
- **هل الحل آمن للخطوط المتعددة؟** تطبيق الإعدادات لكل دفتر عمل؛ كائن `GlobalizationSettings` نفسه غير قابل للتغيير بعد الإنشاء.

## ما هي العولمة في Aspose.Cells؟

`GlobalizationSettings` هو كائن التكوين في Aspose.Cells الذي يتحكم في السلاسل الخاصة بالمحلية مثل رسائل الأخطاء، القيم المنطقية، رموز العملات، وأنماط التاريخ. من خلال توفير الفئة الفرعية الخاصة بك، تخبر المكتبة بالنص الذي يجب عرضه لكل ثقافة، مما يتيح لك استبدال السلاسل الإنجليزية الافتراضية بترجمات تتطابق مع لغة المستخدم النهائي والعادات الإقليمية.

## لماذا نضيف عولمة مخصصة؟

يدعم Aspose.Cells **أكثر من 50 تنسيقًا للإدخال والإخراج** – بما في ذلك XLSX و CSV و PDF و ODS – ويمكنه معالجة دفاتر العمل التي تحتوي على **حتى 200 000 صف** دون تحميل الملف بالكامل في الذاكرة. يضمن تخصيص العولمة أن يرى المستخدمون النهائيون الرسائل بلغتهم الأم، مما يقلل من تذاكر الدعم بنسبة تُقدَّر بـ **30 %** في عمليات النشر متعددة الجنسيات.

## المتطلبات المسبقة

- **Java Development Kit** 8 أو أحدث.
- **IDE** مثل IntelliJ IDEA أو Eclipse.
- **Aspose.Cells for Java** الإصدار 25.3 (أو أحدث) مضاف عبر Maven أو Gradle.

### إعداد Aspose.Cells لـ Java

أضف تبعية Maven إلى ملف `pom.xml` الخاص بك:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

أو، إذا كنت تفضل Gradle، أدخل ما يلي في `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

تقدم Aspose عدة خيارات للترخيص:

- **نسخة تجريبية مجانية** – تقييم كامل المميزات لمدة 30 يومًا.  
- **ترخيص مؤقت** – تقييم غير محدود بدون علامات مائية.  
- **ترخيص تجاري** – جاهز للإنتاج، مع دعم أولوية.

بعد الحصول على ملف الترخيص، قم بتعيينه مرة واحدة عند بدء تشغيل التطبيق:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## كيفية إضافة العولمة للغة الروسية؟

كائن `Workbook` يمثل ملف Excel محملاً في الذاكرة، ويوفر الوصول إلى أوراقه وخلاياه وإعداداته. قم بتحميل دفتر العمل الخاص بك، أنشئ فئة فرعية من `GlobalizationSettings`، واربطها بدفتر العمل. الإجابة المباشرة هي: **إنشاء كائن `GlobalizationSettings` مخصص، وتجاوز `getErrorValueString` و `getBooleanValueString`، ثم استدعاء `workbook.setGlobalizationSettings(customSettings)`**. هذه الطريقة ذات الخطوتين تستبدل السلاسل الروسية الافتراضية بما تفضله.

### تعريف الإعدادات المخصصة

المرة الأولى التي تشير فيها إلى `GlobalizationSettings` في هذا الدليل، لاحظ التعريف:

`GlobalizationSettings` هي الفئة الأساسية التي يستخدمها Aspose.Cells لاسترجاع السلاسل الخاصة بالمحلية.  

الآن أنشئ فئة فرعية تُعيد نصًا خاصًا بالروسية:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### تطبيق الإعدادات على دفتر عمل

بعد تعريف الفئة الفرعية، اربطها بأي كائن `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## تطبيقات عملية

- **التقارير المالية** – عرض رموز الأخطاء بلغة المحاسب الأصلية، مما يقلل من سوء الفهم.  
- **أدوات على مستوى المؤسسة** – تضمين نفس منطق العولمة عبر العشرات من الأدوات الداخلية القائمة على Excel.  
- **خطوط أنابيب البيانات المؤتمتة** – ضمان أن الأنظمة المت downstream تتلقى قيمًا متوافقة مع اللغة دون خطوات ترجمة إضافية.

## اعتبارات الأداء

عند تمكين العولمة المخصصة، لا يزال Aspose.Cells يعالج الصيغ والإدخال/الإخراج بنفس الأداء العالي. للحفاظ على انخفاض استهلاك الذاكرة:

- تحرير مراجع دفتر العمل (`wb.dispose()`) بعد الحفظ.  
- استخدام `CalculationOptions.setEnableIterativeCalculation(true)` فقط عند الضرورة.  
- ضبط ذاكرة JVM (`-Xmx2g`) لدفاتر العمل التي تزيد عن 100 MB.

## الأسئلة المتكررة

**س: هل يمكنني تطبيق نفس إعدادات العولمة على عدة دفاتر عمل في آن واحد؟**  
ج: نعم. أنشئ نسخة واحدة من `RussianGlobalization` ومررها إلى كل دفتر عمل عبر `setGlobalizationSettings`.

**س: ماذا لو احتجت لدعم لغة تستخدم كتابة من اليمين إلى اليسار؟**  
ج: تجاوز طرق إضافية مثل `getCurrencySymbol` و `getDatePattern` في الفئة الفرعية لإرجاع الرموز المناسبة للكتابة من اليمين إلى اليسار.

**س: هل يلزم وجود ترخيص للإصدار التجريبي لاستخدام العولمة المخصصة؟**  
ج: لا. يدعم الإصدار التجريبي `GlobalizationSettings` بالكامل؛ تظهر علامات مائية للتقييم فقط على بعض تنسيقات الإخراج.

**س: كيف يمكنني تصحيح سلاسل الأخطاء غير الصحيحة؟**  
ج: أدخل عبارات `System.out.println` داخل الطرق التي قمت بتجاوزها للتحقق من أن قيمة `err` المدخلة تتطابق مع حالات `switch` الخاصة بك.

**س: هل يؤثر هذا على سرعة حساب الصيغ؟**  
ج: بشكل ضئيل. المكتبة تبحث عن السلسلة فقط عند عرض قيم الخلايا، وليس أثناء خطوات الحساب الوسيطة.

## موارد إضافية

- **التوثيق**: استكشف أدلة مفصلة في [توثيق Aspose.Cells](https://reference.aspose.com/cells/java/)  
- **التنزيل**: احصل على أحدث الإصدارات في [تنزيلات Aspose](https://releases.aspose.com/cells/java/)  
- **الشراء**: اشترِ ترخيصًا للاستخدام التجاري عبر [شراء Aspose](https://purchase.aspose.com/buy)  
- **نسخة تجريبية مجانية**: ابدأ بنسخة تجريبية مجانية من [نسخة تجريبية Aspose](https://releases.aspose.com/cells/java/)  
- **ترخيص مؤقت**: احصل على ترخيص مؤقت عبر [ترخيص مؤقت Aspose](https://purchase.aspose.com/temporary-license/)  
- **الدعم**: احصل على المساعدة من المجتمع في [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)

---

**آخر تحديث:** 2026-08-16  
**تم الاختبار مع:** Aspose.Cells 25.3 for Java  
**المؤلف:** Aspose

## دروس ذات صلة

- [Aspose.Cells Java: دليل محرك الحساب المخصص](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [كيفية استخدام Aspose Cells – دروس محرك Excel للـ Java](/cells/java/calculation-engine/)
- [اعتماد Maven لـ Aspose Cells – إدارة اتصالات بيانات Excel باستخدام Aspose.Cells في Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}