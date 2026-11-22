---
category: general
date: 2026-11-22
description: تعلم كيفية استخدام wrapcols في Java لتحويل نطاق إلى أعمدة باستخدام Aspose.Cells.
  يشرح هذا الدليل خطوة بخطوة وظيفة wrap columns في Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: ar
lastmod: 2026-11-22
og_description: كيفية استخدام wrapcols في جافا لتحويل نطاق إلى أعمدة. اتبع هذا الدرس
  لإتقان وظيفة wrap columns في إكسل باستخدام Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: كيفية استخدام wrapcols في جافا – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: كيفية استخدام wrapcols في جافا مع Aspose.Cells
url: /ar/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام wrapcols في Java مع Aspose.Cells

إذا كنت بحاجة إلى **how to use wrapcols** لإعادة تشكيل البيانات في مصنف Excel، فإن هذا الدليل يوضح العملية بالكامل. سترى كيف تقوم صيغة WRAPCOLS بتحويل نطاق عمودي إلى مجموعة من الأعمدة، مما يجعل من السهل عرض القوائم جنبًا إلى جنب.

الدليل يغطي كل ما تحتاجه: تحميل المصنف، تطبيق صيغة WRAPCOLS، وحفظ النتيجة. لا توجد مراجع خارجية مطلوبة، لذا يمكنك نسخ الكود وتشغيله فورًا. خلال الشرح نوضح أيضًا *wrap columns excel function* ونظهر كيفية **convert range to columns** لسيناريوهات التقارير الشائعة.

## ما ستحتاجه

- Java 17 أو أحدث  
- Aspose.Cells for Java (أحدث نسخة)  
- بيئة تطوير Java (IntelliJ IDEA، Eclipse، أو VS Code)  
- ملف Excel إدخال (`input.xlsx`) يحتوي على بيانات في العمود A  

## كيفية استخدام wrapcols في Java مع Aspose.Cells

الخطوات الأربع التالية تنفّذ سير عمل **how to use wrapcols**. كل خطوة تتضمن مقتطف كود، شرح لأهميتها، ونصيحة لتجنب الأخطاء الشائعة.

### الخطوة 1: تحميل المصنف

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*لماذا هذه الخطوة مهمة*: `Workbook` هو نقطة الدخول لجميع عمليات Excel في Aspose.Cells. تحميل الملف يمنحك الوصول إلى أوراق العمل، الخلايا، والصيغ.  

**نصيحة احترافية**: استخدم مسارًا مطلقًا أثناء التطوير لتجنب `FileNotFoundException`. انتقل إلى مسار نسبي بمجرد تعبئة المشروع.

### الخطوة 2: الوصول إلى ورقة العمل الأولى

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

عادةً ما تحتوي ورقة العمل الأولى (`index 0`) على البيانات التي تريد تحويلها. إذا كانت بياناتك موجودة في ورقة مختلفة، غيّر الفهرس أو استخدم `get("SheetName")`.  

**لماذا هذه الخطوة مهمة**: العمل مع ورقة العمل الصحيحة يضمن أن صيغة WRAPCOLS تشير إلى النطاق المقصود.

### الخطوة 3: تعيين صيغة WRAPCOLS

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` هي **wrap columns excel function** التي توزع القيم من `range` عبر عدد الأعمدة المحدد. في هذا المثال نأخذ القيم من `A1:A10` ونلفها إلى ثلاثة أعمدة، بدءًا من `A1`.  

**لماذا هذه الخطوة مهمة**: الصيغة تقوم بالعمل الشاق—لا حاجة للتكرار اليدوي أو معالجة المصفوفات.  

**نصيحة لـ convert range to columns**: عدّل الوسيط الثاني (`3`) ليتطابق مع عدد الأعمدة التي تحتاجها. إذا لم يكن طول النطاق مضاعفًا لعدد الأعمدة، سيحتوي العمود الأخير على العناصر المتبقية.

### الخطوة 4: حفظ المصنف

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

الحفظ يكتب صيغة WRAPCOLS في `output.xlsx`. عند فتح الملف في Excel، ستقوم الصيغة بالتقييم وعرض البيانات ملفوفة في أعمدة.  

**لماذا هذه الخطوة مهمة**: حفظ المصنف يتيح لك التحقق من النتيجة ومشاركة الملف مع المستخدمين غير المتعاملين مع Java.

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="لقطة شاشة لكيفية استخدام wrapcols في Excel"}

### النتيجة المتوقعة

عند فتح `output.xlsx`، الخلايا `A1:C4` (أو عدد الصفوف المطلوبة) ستحتوي على القائمة الأصلية من `A1:A10` موزعة عبر ثلاثة أعمدة. الشكل سيكون كالتالي:

| A | B | C |
|---|---|---|
| العنصر 1 | العنصر 4 | العنصر 7 |
| العنصر 2 | العنصر 5 | العنصر 8 |
| العنصر 3 | العنصر 6 | العنصر 9 |
| العنصر 10 |   |   |

تقوم **wrap columns excel function** تلقائيًا بملء الخلايا الفارغة بالفراغات، لذا لا تحتاج إلى كود تنظيف إضافي.

## فهم wrap columns excel function

صيغة WRAPCOLS هي جزء من وظائف المصفوفات الديناميكية في Excel التي تم تقديمها في Excel 365. تعمل بشكل مشابه لـ `TEXTSPLIT` لكنها تركز على التوزيع حسب الأعمدة.

- **الصيغة**: `=WRAPCOLS(source_range, columns)`  
- **المعلمات**:  
  - `source_range` – النطاق العمودي الذي تريد إعادة تشكيله.  
  - `columns` – عدد الأعمدة التي تريد لف البيانات فيها.  

عند استدعاء `=WRAPCOLS(A1:A10, 3)`، يتعامل Excel مع المصدر كمصفوفة أحادية البعد ويملأ العمود الأول، ثم الثاني، وهكذا حتى يتم وضع جميع القيم. هذا يجعل **how to use wrapcols** أداة مثالية لتحويل قائمة عمود واحد إلى تقرير متعدد الأعمدة دون VBA.

## تحويل النطاق إلى أعمدة بدون صيغ (اختياري)

إذا كنت تفضل تنفيذ عملية **convert range to columns** بالكامل في Java—دون الاعتماد على محرك حسابات Excel—يمكنك قراءة القيم المصدر، بناء مصفوفة ثنائية الأبعاد، وكتابتها يدويًا مرة أخرى:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

هذا المقتطف يوضح طريقة بديلة لـ **convert range to columns** عندما تحتاج إلى تحكم كامل في النتيجة (مثل تطبيق تنسيق مخصص لكل عمود). ومع ذلك، فإن استخدام **wrap columns excel function** عبر WRAPCOLS يكون عادةً أكثر اختصارًا ويسمح لـ Excel بالتعامل مع إعادة الحساب تلقائيًا.

## الحالات الخاصة وأفضل الممارسات

- **الخلايا الفارغة**: WRAPCOLS يتعامل مع الخلايا الفارغة كفراغات. إذا كان نطاق المصدر يحتوي على فراغات، سيحافظ الناتج على تلك الفراغات.  
- **النطاقات الديناميكية**: استخدم نطاقًا مسمى أو إشارة جدول (`Table1[Column]`) لجعل الصيغة تتكيف عند إضافة صفوف.  
- **الأداء**: تطبيق الصيغة هو O(1) لأن Excel يقيمها بشكل كسول. التحويل البرمجي الموضح أعلاه هو O(n) وقد يكون أبطأ للنطاقات الكبيرة جدًا.  
- **توافق الإصدارات**: وظيفة WRAPCOLS تتطلب Excel 365 أو أحدث. إذا كنت بحاجة لدعم إصدارات أقدم، اعتمد على طريقة التحويل من جانب Java.  

## كيفية استخدام wrapcols في سيناريوهات أخرى

- **لوحات التقارير**: تحويل قائمة عمودية لأسماء KPI إلى جدول مضغوط بثلاثة أعمدة لكل صف.  
- **نماذج إدخال البيانات**: تحويل عمود من مدخلات المستخدم إلى تخطيط جنبًا إلى جنب لتسهيل المقارنة البصرية.  
- **التصدير إلى CSV**: بعد تطبيق WRAPCOLS، احفظ المصنف كملف CSV للحصول على عرض مفصول يتطابق مع تخطيط الأعمدة.  

كل من هذه الحالات يتبع نمط **how to use wrapcols** نفسه: تحميل، إشارة، تعيين الصيغة، حفظ.

## الخلاصة

أنت الآن تعرف **how to use wrapcols** في Java مع Aspose.Cells لتقوم بـ **convert range to columns** بفعالية. من خلال تطبيق صيغة `WRAPCOLS` تستفيد من *wrap columns excel function* الأصلي، مما يبقي كودك مختصرًا بينما يمنح Excel التحكم الكامل في الحساب والعرض.

جرّب عددًا مختلفًا من الأعمدة، نطاقات ديناميكية، أو التحويل الاختياري من جانب Java لتناسب احتياجات مشروعك. عندما تتقن هذه التقنية، يصبح إعادة تشكيل البيانات في Excel عملية بسطر واحد بدلاً من مهمة يدوية.

---

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام wrapcols لتحويل قائمة إلى عدة أعمدة في Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [كيفية استخدام WRAPCOLS في Java – دليل كامل لصيغ مصفوفات Excel](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [كيفية استخدام WRAPCOLS في Java – مثال كامل على WRAPCOLS في Excel](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}