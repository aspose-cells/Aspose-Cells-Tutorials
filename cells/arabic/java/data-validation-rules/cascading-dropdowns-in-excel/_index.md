---
title: القوائم المنسدلة المتتالية في Excel
linktitle: القوائم المنسدلة المتتالية في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel في Java من Aspose.Cells
description: تعرف على كيفية إنشاء قوائم منسدلة متتالية في Excel باستخدام Aspose.Cells for Java. يوفر هذا الدليل خطوة بخطوة التعليمات البرمجية المصدرية ونصائح الخبراء للتعامل بكفاءة مع جداول بيانات Excel.
weight: 13
url: /ar/java/data-validation-rules/cascading-dropdowns-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# القوائم المنسدلة المتتالية في Excel


## مقدمة حول القوائم المنسدلة المتتالية في Excel

في عالم معالجة جداول البيانات، يعتبر Aspose.Cells for Java بمثابة مجموعة أدوات قوية تمكن المطورين من العمل مع ملفات Excel بكفاءة. ومن بين الميزات المثيرة للاهتمام التي يوفرها القدرة على إنشاء قوائم منسدلة متتالية في Excel، مما يسمح للمستخدمين بتحديد الخيارات بشكل ديناميكي بناءً على تحديد سابق. في هذا الدليل التفصيلي، سنتعمق في عملية تنفيذ القوائم المنسدلة المتتالية باستخدام Aspose.Cells for Java. لذا، فلنبدأ!

## المتطلبات الأساسية

قبل أن نبدأ هذه الرحلة، تأكد من توفر المتطلبات الأساسية التالية:

-  Aspose.Cells for Java: قم بتنزيله وتثبيته من[هنا](https://releases.aspose.com/cells/java/).
- بيئة تطوير Java: يجب أن يكون لديك بيئة تطوير Java مُعدّة على جهازك.
- الفهم الأساسي لبرنامج Excel: إن الإلمام ببرنامج Excel ومفاهيمه الأساسية سيكون مفيدًا.

## إعداد المسرح

هدفنا هو إنشاء جدول بيانات Excel يحتوي على قوائم منسدلة متتالية. تخيل سيناريو حيث لديك قائمة بالدول، وعندما تختار دولة، يجب أن تكون قائمة المدن في تلك الدولة متاحة للاختيار. دعنا نوضح الخطوات لتحقيق ذلك.

## الخطوة 1: إنشاء مصنف Excel

أولاً، لنقم بإنشاء مصنف Excel باستخدام Aspose.Cells for Java. سنضيف ورقتين: واحدة لقائمة الدول والأخرى لقائمة المدن.

```java
// كود جافا لإنشاء مصنف Excel
Workbook workbook = new Workbook();
Worksheet countrySheet = workbook.getWorksheets().get(0);
countrySheet.setName("Countries");
Worksheet citySheet = workbook.getWorksheets().add("Cities");
```

## الخطوة 2: ملء البيانات

الآن، نحتاج إلى ملء أوراق العمل الخاصة بنا بالبيانات. في ورقة "الدول"، سنقوم بإدراج البلدان، وفي ورقة "المدن"، سنتركها فارغة في البداية، حيث سنقوم بملئها ديناميكيًا لاحقًا.

```java
//كود جافا لملء ورقة "الدول"
countrySheet.getCells().get("A1").putValue("Country");
countrySheet.getCells().get("A2").putValue("USA");
countrySheet.getCells().get("A3").putValue("Canada");
countrySheet.getCells().get("A4").putValue("UK");
// أضف المزيد من البلدان حسب الحاجة
```

## الخطوة 3: إنشاء القوائم المنسدلة

بعد ذلك، سننشئ قوائم منسدلة لعمودي الدولة والمدينة. سيتم ربط هذه القوائم المنسدلة بطريقة تجعل القائمة المنسدلة للمدينة يتم تحديثها وفقًا لذلك عند تحديد دولة.

```java
// كود جافا لإنشاء قوائم منسدلة
DataValidationCollection validations = countrySheet.getDataValidations();
DataValidation validation = validations.get(validations.add(1, 1, countrySheet.getCells().getMaxDataRow(), 1));
validation.setType(DataValidationType.LIST);
validation.setFormula1("Countries!$A$2:$A$4"); // الإشارة إلى قائمة البلدان
```

## الخطوة 4: تنفيذ القوائم المنسدلة المتتالية

الآن يأتي الجزء المثير: تنفيذ القوائم المنسدلة المتتالية. سنستخدم Aspose.Cells for Java لتحديث القائمة المنسدلة للمدينة ديناميكيًا بناءً على البلد المحدد.

```java
// كود جافا لتنفيذ القوائم المنسدلة المتتالية
countrySheet.getCells().setCellObserver(new ICellObserver() {
    @Override
    public void cellChanged(Cell cell) {
        if (cell.getName().equals("B2")) {
            // مسح القائمة المنسدلة للمدينة السابقة
            citySheet.getCells().get("B2").setValue("");
            
            // تحديد البلد المحدد
            String selectedCountry = cell.getStringValue();
            
            // بناءً على البلد المحدد، قم بملء القائمة المنسدلة للمدينة
            switch (selectedCountry) {
                case "USA":
                    validation.setFormula1("Cities!$A$2:$A$4"); // التواجد في مدن الولايات المتحدة الأمريكية
                    break;
                case "Canada":
                    validation.setFormula1("Cities!$B$2:$B$4"); // التواجد في مدن كندا
                    break;
                case "UK":
                    validation.setFormula1("Cities!$C$2:$C$4"); // التواجد في مدن المملكة المتحدة
                    break;
                // إضافة المزيد من الحالات للدول الأخرى
            }
        }
    }
});
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية إنشاء قوائم منسدلة متتالية في Excel باستخدام Aspose.Cells for Java. بدأنا بإعداد المتطلبات الأساسية وإنشاء مصنف Excel وملء البيانات، ثم تعمقنا في تعقيدات إنشاء القوائم المنسدلة وتنفيذ سلوك التتالي الديناميكي. بصفتك مطورًا، لديك الآن المعرفة والأدوات اللازمة لتحسين ملفات Excel الخاصة بك باستخدام القوائم المنسدلة التفاعلية، مما يوفر تجربة مستخدم سلسة.

## الأسئلة الشائعة

### كيف يمكنني إضافة المزيد من البلدان والمدن إلى القوائم المنسدلة؟

لإضافة المزيد من البلدان والمدن، تحتاج إلى تحديث الأوراق ذات الصلة في مصنف Excel الخاص بك. ما عليك سوى توسيع القوائم في أوراق "البلدان" و"المدن"، وستتضمن القوائم المنسدلة الإدخالات الجديدة تلقائيًا.

### هل يمكنني استخدام هذه التقنية مع ميزات Excel الأخرى؟

بالتأكيد! يمكنك الجمع بين القوائم المنسدلة المتتالية وميزات Excel المتنوعة مثل التنسيق الشرطي والصيغ والرسوم البيانية لإنشاء جداول بيانات قوية وتفاعلية مصممة خصيصًا لتلبية احتياجاتك المحددة.

### هل Aspose.Cells for Java مناسب للمشاريع الصغيرة والكبيرة؟

نعم، يعد Aspose.Cells for Java متعدد الاستخدامات ويمكن استخدامه في مشاريع بجميع الأحجام. سواء كنت تعمل على أداة مساعدة صغيرة أو تطبيق مؤسسي معقد، يمكن لـ Aspose.Cells for Java تبسيط المهام المرتبطة بـ Excel.

### هل أحتاج إلى مهارات برمجة متقدمة لتنفيذ القوائم المنسدلة المتتالية مع Aspose.Cells لـ Java؟

على الرغم من أن الفهم الأساسي للغة Java مفيد، فإن Aspose.Cells for Java يوفر توثيقًا وأمثلة شاملة لإرشادك خلال العملية. ومع بعض التفاني والممارسة، يمكنك إتقان هذه الميزة.

### أين يمكنني العثور على المزيد من الموارد والوثائق الخاصة بـ Aspose.Cells for Java؟

 يمكنك الوصول إلى الوثائق والموارد الشاملة لـ Aspose.Cells for Java على[هنا](https://reference.aspose.com/cells/java/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
