---
category: general
date: 2026-07-03
description: كيفية إضافة خاصية مخصصة في Excel باستخدام Java و Aspose Cells. تعلم خطوة
  بخطوة كيفية تعيين وقراءة خصائص المصنف المخصصة بكفاءة.
draft: false
keywords:
- how to add custom property
- Aspose Cells Java
- Excel custom property
- Java workbook manipulation
- set custom property Java
language: ar
og_description: كيفية إضافة خاصية مخصصة في Excel باستخدام Java. يشرح هذا الدليل كيفية
  إنشاء وقراءة وحفظ الخصائص المخصصة باستخدام Aspose Cells.
og_title: كيفية إضافة خاصية مخصصة في إكسل باستخدام جافا – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to add custom property in Excel with Java using Aspose Cells. Learn
    step‑by‑step to set and read workbook custom properties efficiently.
  headline: How to Add Custom Property in Excel Using Java – Complete Guide
  type: TechArticle
- description: How to add custom property in Excel with Java using Aspose Cells. Learn
    step‑by‑step to set and read workbook custom properties efficiently.
  name: How to Add Custom Property in Excel Using Java – Complete Guide
  steps:
  - name: Load the Existing Workbook (How to Add Custom Property)
    text: The very first thing you need is a `Workbook` object that points to your
      source file. This is where **how to add custom property** begins—once the workbook
      is in memory you can start tinkering with its metadata.
  - name: Access the First Worksheet (Excel Custom Property Context)
    text: Even though custom properties belong to the workbook, many developers instinctively
      look at the worksheet level first. Here we simply fetch the first sheet to keep
      the example concrete.
  - name: Add a Custom Property Named "ProjectId" (Set Custom Property Java)
    text: Now we get to the heart of the matter—adding a custom property. The `CustomPropertyCollection`
      lets you add a key/value pair with a single call.
  - name: Retrieve the Value and Convert It to a String (Java Workbook Manipulation)
    text: Reading back the property verifies that the addition succeeded and shows
      how you can later consume the metadata.
  - name: Save the Modified Workbook (Aspose Cells Java Persistence)
    text: After you’ve added (or possibly updated) a property, you must persist the
      changes back to disk. Aspose Cells supports saving in the same format or converting
      to another one.
  - name: Verify the Property in Excel (Optional Manual Check)
    text: Open `updated.xlsb` in Microsoft Excel, go to **File → Info → Properties
      → Advanced Properties**, and you’ll see “ProjectId” listed under the **Custom**
      tab. This manual verification confirms that **how to add custom property** truly
      worked end‑to‑end.
  - name: Next Steps
    text: '- **Explore other metadata**: Try adding built‑in properties like `Author`
      or `Company`. - **Batch processing**: Loop through a folder of workbooks and
      inject the same property into each. - **Read‑only scenarios**: Use the same
      API to *extract* custom properties from third‑party files.'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- custom-properties
title: كيفية إضافة خاصية مخصصة في إكسل باستخدام جافا – دليل شامل
url: /ar/java/workbook-operations/how-to-add-custom-property-in-excel-using-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة خاصية مخصصة في Excel باستخدام Java – دليل شامل

هل تساءلت يومًا **كيفية إضافة خاصية مخصصة** إلى مصنف Excel من خلال Java؟ ربما تقوم بإنشاء محرك تقارير وتحتاج إلى وضع علامة على كل ملف بمعرف مشروع، رقم نسخة، أو أي بيانات وصفية يمكن لعملية ما لاحقًا قراءتها. الخبر السار؟ الأمر بسيط جدًا بمجرد أن تتوفر لديك المكتبة المناسبة.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يُظهر بالضبط **كيفية إضافة خاصية مخصصة** إلى مصنف، استرجاعها، وحفظ التغييرات. سنستخدم **Aspose Cells for Java**، واجهة برمجة تطبيقات قوية تُجردك من تفاصيل الباينري منخفض المستوى لملفات `.xlsb`. بنهاية هذا الدرس ستتمكن من تضمين بيانات وصفية مخصصة مثل “ProjectId” بسطر واحد من الشيفرة—بدون الحاجة إلى تعديل XML.

## المتطلبات المسبقة

قبل الغوص في التفاصيل، تأكد من وجود ما يلي:

- Java 17 أو أحدث مثبتة (الشيفرة تُجمّع مع أي JDK حديث).
- Maven أو Gradle لجلب تبعية **Aspose Cells Java**.
- فهم أساسي لصياغة Java—ليس شيئًا معقدًا، فقط `import`، `class`، وطريقة `main`.
- مصنف `.xlsb` موجود (أو يمكنك إنشاء ملف فارغ للاختبار).

> **نصيحة احترافية:** إذا لم يكن لديك ترخيص Aspose Cells بعد، يمكنك طلب مفتاح تقييم مجاني من موقع Aspose. المكتبة تعمل بشكل جيد في وضع التجربة لأغراض التعلم.

## تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى ست خطوات واضحة. كل خطوة لها عنوان H2 خاص، والعنوان الأول يحتوي على الكلمة المفتاحية الأساسية لتلبية متطلبات SEO.

### الخطوة 1: تحميل المصنف الموجود (How to Add Custom Property)

أول شيء تحتاجه هو كائن `Workbook` يشير إلى ملف المصدر الخاص بك. هنا يبدأ **how to add custom property**—بمجرد تحميل المصنف في الذاكرة يمكنك البدء بالتلاعب ببياناته الوصفية.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Adjust the path to point to your actual .xlsb file
        String inputPath = "YOUR_DIRECTORY/book.xlsb";

        // Load the workbook
        Workbook workbook = new Workbook(inputPath);
        // -----------------------------------------------------------------
        // At this point the workbook is fully loaded and ready for manipulation.
```

*لماذا هذا مهم:* تحميل المصنف يمنحك الوصول إلى هياكله الداخلية، بما في ذلك المجموعة التي تخزن الخصائص المخصصة. بدون هذه الخطوة، لا مكان لتوصيل البيانات الوصفية الخاصة بك.

### الخطوة 2: الوصول إلى الورقة الأولى (Excel Custom Property Context)

على الرغم من أن الخصائص المخصصة تنتمي إلى المصنف، إلا أن العديد من المطورين يتجهون أولًا إلى مستوى الورقة. هنا نستدعي الورقة الأولى فقط لجعل المثال ملموسًا.

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // -----------------------------------------------------------------
        // You could also target a different sheet by name:
        // Worksheet worksheet = workbook.getWorksheets().get("Sheet1");
```

*ملاحظة:* الخصائص المخصصة **ليست** خاصة بالورقة، لكن وجود مرجع للورقة يسهل توضيح مكان استخدام الخاصية لاحقًا.

### الخطوة 3: إضافة خاصية مخصصة باسم "ProjectId" (Set Custom Property Java)

الآن نصل إلى جوهر الموضوع—إضافة خاصية مخصصة. تسمح لك `CustomPropertyCollection` بإضافة زوج مفتاح/قيمة باستدعاء واحد.

```java
        // Add a custom property called "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
        // -----------------------------------------------------------------
        // The value can be any primitive type: int, double, boolean, or even a String.
```

*لماذا نستخدم `worksheet.getCustomProperties()`*: Aspose Cells تُظهر نفس المجموعة على مستوى المصنف والورقة، لذا يمكنك اختيار النطاق الذي يناسبك. في معظم السيناريوهات ستخزن البيانات الوصفية على مستوى المصنف، لكن الـ API مرن.

### الخطوة 4: استرجاع القيمة وتحويلها إلى سلسلة (Java Workbook Manipulation)

قراءة الخاصية مرة أخرى يتحقق من نجاح الإضافة ويظهر كيف يمكنك استهلاك البيانات الوصفية لاحقًا.

```java
        // Retrieve the custom property value and convert it to a string
        String projectIdValue = worksheet.getCustomProperties()
                                         .get("ProjectId")
                                         .getValue()
                                         .toString();

        System.out.println("ProjectId = " + projectIdValue);
        // Expected output: ProjectId = 12345
        // -----------------------------------------------------------------
```

*تحذير حالة حافة:* إذا لم يكن اسم الخاصية موجودًا، فإن `get()` تُعيد `null` واستدعاء `.getValue()` سيتسبب في `NullPointerException`. احرص دائمًا على الحماية في الشيفرة الإنتاجية.

### الخطوة 5: حفظ المصنف المعدل (Aspose Cells Java Persistence)

بعد إضافة (أو تعديل) خاصية، يجب حفظ التغييرات على القرص. Aspose Cells يدعم الحفظ بنفس الصيغة أو التحويل إلى صيغة أخرى.

```java
        // Save the workbook with the new custom property
        String outputPath = "YOUR_DIRECTORY/updated.xlsb";
        workbook.save(outputPath);
        // -----------------------------------------------------------------
        // You can also save as .xlsx, .csv, etc., by changing the file extension.
    }
}
```

*ماذا يحدث خلف الكواليس؟* Aspose Cells يكتب الخاصية المخصصة في تدفق “Document Summary Information” داخل المصنف، والذي يقرأه Excel تلقائيًا عند فتح الملف.

### الخطوة 6: التحقق من الخاصية في Excel (فحص يدوي اختياري)

افتح `updated.xlsb` في Microsoft Excel، انتقل إلى **File → Info → Properties → Advanced Properties**، وسترى “ProjectId” مدرجة تحت تبويب **Custom**. هذا التحقق اليدوي يؤكد أن **how to add custom property** عمل بنجاح من البداية إلى النهاية.

> **نصيحة سريعة:** إذا أردت تعداد جميع الخصائص المخصصة برمجيًا، استدعِ `worksheet.getCustomProperties().size()` وتكرّر عبر المجموعة.

## مثال عملي كامل

فيما يلي الملف المصدر الكامل الذي يمكنك نسخه‑لصقه في بيئة تطوير وتشغيله فورًا (فقط استبدل مسارات الملفات الوهمية).

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        String inputPath = "YOUR_DIRECTORY/book.xlsb";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Add custom property "ProjectId"
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // 4️⃣ Retrieve and print the property
        String projectIdValue = worksheet.getCustomProperties()
                                         .get("ProjectId")
                                         .getValue()
                                         .toString();
        System.out.println("ProjectId = " + projectIdValue); // → ProjectId = 12345

        // 5️⃣ Save the updated workbook
        String outputPath = "YOUR_DIRECTORY/updated.xlsb";
        workbook.save(outputPath);
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
ProjectId = 12345
```

والملف `updated.xlsb` الآن يحمل البيانات الوصفية المخصصة التي عرّفتها.

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إضافة عدة خصائص مخصصة مرة واحدة؟* | نعم. استدعِ `add()` بشكل متكرر أو كرر عبر `Map<String,Object>` يحتوي على أزواج المفتاح/القيمة. |
| *ما أنواع البيانات المدعومة؟* | الأنواع الأولية (`int`, `double`, `boolean`) و`String`. الكائنات المعقدة تحتاج إلى تسلسل إلى سلسلة أولًا. |
| *هل يعمل هذا مع ملفات `.xlsx`؟* | بالتأكيد. نفس الـ API يعمل مع جميع صيغ Excel التي يدعمها Aspose Cells (`.xls`, `.xlsx`, `.xlsb`, إلخ). |
| *كيف أزيل خاصية مخصصة؟* | استخدم `worksheet.getCustomProperties().remove("ProjectId");`. |
| *هل هناك تأثير على الأداء؟* | إضافة عدد قليل من الخصائص لا يُحدث فرقًا ملحوظًا. قد تستفيد التحديثات الضخمة من إعادة استخدام نفس كائن `Workbook`. |

## خلاصة (How to Add Custom Property Recap)

لقد غطينا الآن **كيفية إضافة خاصية مخصصة** إلى مصنف Excel باستخدام Java وAspose Cells. سارت الرحلة من تحميل الملف، الوصول إلى ورقة، إدراج الخاصية، قراءتها، وأخيرًا حفظ التغييرات. الآن يمكنك وضع أي بيانات وصفية تحتاجها—مثل “ReportId”، “GeneratedBy”، أو حتى حمولة JSON لخدمات ما بعد المعالجة.

### الخطوات التالية

- **استكشاف بيانات وصفية أخرى**: جرّب إضافة خصائص مدمجة مثل `Author` أو `Company`.
- **المعالجة الدفعية**: كرّر عبر مجلد من المصنفات وأدخل نفس الخاصية في كلٍ منها.
- **سيناريوهات القراءة فقط**: استخدم نفس الـ API *لاستخراج* الخصائص المخصصة من ملفات طرف ثالث.

إذا وجدت هذا الدليل مفيدًا، فكر في وضع نجمة على المستودع الذي يحتوي على العينة، أو اترك تعليقًا بحالتك الخاصة. برمجة سعيدة!

![مخطط يوضح كيفية إضافة خاصية مخصصة إلى مصنف Excel باستخدام Java](/images/add-custom-property-diagram.png "مخطط مثال كيفية إضافة خاصية مخصصة")

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}