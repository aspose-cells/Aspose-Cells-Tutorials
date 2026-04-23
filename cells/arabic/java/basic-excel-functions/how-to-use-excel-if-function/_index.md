---
date: 2026-01-24
description: تعلم كيفية حساب الدرجات في Excel باستخدام دالة IF مع Aspose.Cells للغة
  Java. دليل خطوة بخطوة لإنشاء صيغة شرطية وتطبيق منطق شرطي في Excel.
linktitle: Calculate Grades Excel with IF Function
second_title: Aspose.Cells Java Excel Processing API
title: حساب الدرجات في إكسل باستخدام دالة IF باستخدام Aspose.Cells
url: /ar/java/basic-excel-functions/how-to-use-excel-if-function/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# حساب الدرجات في Excel باستخدام دالة IF مع Aspose.Cells

## مقدمة

إذا كنت بحاجة إلى **حساب الدرجات في Excel** بسرعة وموثوقية، فإن دالة IF هي أداتك المفضلة. عندما تجمعها مع **Aspose.Cells for Java**، يمكنك إنشاء وتعديل وحفظ جداول البيانات برمجيًا دون الحاجة إلى فتح Excel. في هذا الدليل سنستعرض مثالًا واقعيًا يوضح **كيفية استخدام IF** لإنشاء صيغة شرطية، وتضمين عبارات IF متداخلة، وتطبيق منطق شرطي على طريقة Excel—كل ذلك من خلال كود Java.

## إجابات سريعة
- **ما الذي تفعله دالة IF؟** تُرجع قيمة إذا كان الشرط صحيحًا وأخرى إذا كان خاطئًا.  
- **لماذا نستخدم Aspose.Cells؟** يتيح لك العمل مع ملفات Excel على الخادم دون الحاجة إلى Microsoft Office.  
- **كم عدد الدرجات التي يمكنني حسابها؟** غير محدود – فقط قم بنسخ الصيغة إلى أسفل العمود.  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم الحصول على ترخيص تجاري للإنتاج.  
- **هل يمكنني تضمين عبارات IF متداخلة؟** نعم – يمكنك دمج عدة عبارات IF للتعامل مع مقاييس تقييم معقدة.

## ما هو “حساب الدرجات في Excel”؟
حساب الدرجات في Excel يعني تطبيق مجموعة من القواعد الشرطية (مثال: الدرجة ≥ 90 → “A”) مباشرة داخل ورقة العمل. باستخدام دالة IF يمكنك أتمتة هذا المنطق بحيث يحصل كل نتيجة جديدة فورًا على الدرجة المناسبة.

## لماذا نستخدم Aspose.Cells for Java؟
- **معالجة على الخادم** – لا حاجة لتثبيت Excel.  
- **دعم كامل للصيغ** – جميع دوال Excel، بما في ذلك IF المتداخلة، تعمل مباشرة.  
- **أداء عالي** – معالجة دفاتر العمل الكبيرة بسرعة.  
- **متعدد المنصات** – يعمل على أي بيئة متوافقة مع JVM.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر المتطلبات التالية:

- **Aspose.Cells for Java** – تحتاج إلى المكتبة في مسار الفئات الخاص بك. **قم بتثبيت Aspose.Cells** بتحميله من [here](https://releases.aspose.com/cells/java/).
- مجموعة تطوير Java (JDK) 8 أو أعلى.
- بيئة تطوير Java أو أداة بناء (Maven/Gradle) لإدارة الاعتمادات.

## الخطوة 1: إعداد مشروع Java الخاص بك

أنشئ مشروع Java جديد (أو افتح مشروعًا موجودًا) وأضف ملفات JAR الخاصة بـ Aspose.Cells إلى مسار الفئات للمشروع.

## الخطوة 2: استيراد الفئات الضرورية

في كود Java الخاص بك، استورد الفئات الأساسية من مكتبة Aspose.Cells.

```java
import com.aspose.cells.*;
```

## الخطوة 3: إنشاء دفتر عمل Excel

الآن سننشئ دفتر عمل جديد، نضيف ورقة عمل، ونملأها بنتائج عينة.

```java
// Create a new Workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);

// Add data to the worksheet
worksheet.getCells().get("A1").putValue("Score");
worksheet.getCells().get("A2").putValue(85);
worksheet.getCells().get("A3").putValue(60);
worksheet.getCells().get("A4").putValue(45);
```

## الخطوة 4: استخدام دالة IF في Excel

هنا يحدث السحر. سن **ننشئ صيغة شرطية** **تضم عبارات IF متداخلة** على طريقة Excel لتعيين درجة بناءً على النتيجة.

```java
// Apply the IF function to calculate grades
Cell cell = worksheet.getCells().get("B2");
cell.setFormula("=IF(A2>=90, \"A\", IF(A2>=80, \"B\", IF(A2>=70, \"C\", IF(A2>=60, \"D\", \"F\"))))");
```

الصيغة هي:

- إذا كانت النتيجة ≥ 90 → “A”  
- وإلا إذا كانت ≥ 80 → “B”  
- وإلا إذا كانت ≥ 70 → “C”  
- وإلا إذا كانت ≥ 60 → “D”  
- وإلا → “F”

## الخطوة 5: حساب الدرجات لجميع النتائج

بدلاً من كتابة الصيغة لكل صف، قم بنسخها إلى أسفل العمود. هذا يوضح **منطقًا شرطيًا على طريقة Excel** يتم تطبيقه برمجيًا.

```java
// Copy the formula down to calculate grades for other scores
worksheet.getCells().copyRow(worksheet.getCells().getRows().get("2"), worksheet.getCells().getRows().get("3"), new CopyOptions());
worksheet.getCells().copyRow(worksheet.getCells().getRows().get("2"), worksheet.getCells().getRows().get("4"), new CopyOptions());
```

## الخطوة 6: حفظ ملف Excel

أخيرًا، اكتب دفتر العمل إلى القرص (أو إلى تدفق) حتى تتمكن من فتحه في Excel ورؤية النتائج.

```java
// Save the workbook to a file
workbook.save("Grades.xlsx");
```

## حالات الاستخدام الشائعة والنصائح

- **تقييم دفعة** – استيراد قائمة درجات الطلاب، تطبيق صيغة IF المتداخلة، وتصدير التقرير المُقَيَّم.  
- **حدود ديناميكية** – استبدال الأرقام الثابتة (90، 80، …) بمراجع خلايا لتسمح للمستخدمين بتعديل مقاييس التقييم دون تغيير الكود.  
- **نصيحة احترافية:** استخدم `worksheet.calculateFormula()` بعد ضبط الصيغ إذا كنت بحاجة إلى القيم المحسوبة فورًا في Java.

## الأسئلة المتكررة

### كيف يمكنني تثبيت Aspose.Cells for Java؟

لتثبيت Aspose.Cells for Java، قم بتحميل المكتبة من [here](https://releases.aspose.com/cells/java/) وأضف ملفات JAR إلى مسار الفئات في مشروعك.

### هل يمكنني استخدام دالة IF في Excel مع شروط معقدة؟

نعم. يمكنك **تضمين عبارات IF متداخلة** للتعامل مع عدة شروط، تمامًا كما في المثال أعلاه. Aspose.Cells يدعم بالكامل مثل هذه الصيغ المتداخلة.

### هل هناك متطلبات ترخيص لـ Aspose.Cells for Java؟

Aspose.Cells for Java هو منتج تجاري. يتوفر ترخيص تجريبي مجاني، لكن يلزم الحصول على ترخيص مدفوع للنشر في بيئات الإنتاج.

### هل يمكنني تطبيق دالة IF على نطاق من الخلايا في Excel؟

بالطبع. باستخدام المراجع النسبية (مثل `A2`) ونسخ الصيغة إلى أسفل العمود، يمكنك تطبيق دالة IF على عمود كامل تلقائيًا.

### هل Aspose.Cells for Java مناسب لتطبيقات مستوى المؤسسة؟

نعم. يوفر أداءً عاليًا، تغطية واسعة للميزات، ودعمًا موثوقًا، مما يجعله مثاليًا لكل من الأدوات الصغيرة والحلول المؤسسية الكبيرة.

---

**آخر تحديث:** 2026-01-24  
**تم الاختبار مع:** Aspose.Cells for Java 24.12  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}