---
"description": "تعرّف على كيفية إنشاء قوائم منسدلة متتالية في Excel باستخدام Aspose.Cells لجافا. يوفر هذا الدليل خطوة بخطوة شفرة المصدر ونصائح الخبراء للتعامل بكفاءة مع جداول بيانات Excel."
"linktitle": "القوائم المنسدلة المتتالية في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel لـ Aspose.Cells Java"
"title": "القوائم المنسدلة المتتالية في Excel"
"url": "/ar/java/data-validation-rules/cascading-dropdowns-in-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# القوائم المنسدلة المتتالية في Excel


## مقدمة إلى القوائم المنسدلة المتتالية في Excel

في عالم معالجة جداول البيانات، يُعدّ Aspose.Cells for Java مجموعة أدوات فعّالة تُمكّن المطورين من العمل بكفاءة مع ملفات Excel. من ميزاته الرائعة إمكانية إنشاء قوائم منسدلة متتالية في Excel، مما يسمح للمستخدمين باختيار الخيارات ديناميكيًا بناءً على اختيار سابق. في هذا الدليل المُفصّل، سنتعمق في عملية إنشاء قوائم منسدلة متتالية باستخدام Aspose.Cells for Java. هيا بنا نبدأ!

## المتطلبات الأساسية

قبل أن نبدأ هذه الرحلة، تأكد من توفر المتطلبات الأساسية التالية لديك:

- Aspose.Cells لـ Java: قم بتنزيله وتثبيته من [هنا](https://releases.aspose.com/cells/java/).
- بيئة تطوير Java: يجب أن يكون لديك بيئة تطوير Java مُجهزة على جهازك.
- الفهم الأساسي لبرنامج Excel: إن الإلمام ببرنامج Excel ومفاهيمه الأساسية سيكون مفيدًا.

## إعداد المسرح

هدفنا هو إنشاء جدول بيانات إكسل بقوائم منسدلة متتالية. تخيل أن لديك قائمة دول، وعند اختيار دولة، ستظهر قائمة بمدنها. لنشرح خطوات تحقيق ذلك.

## الخطوة 1: إنشاء مصنف Excel

أولاً، لنُنشئ مُصنّف Excel باستخدام Aspose.Cells لجافا. سنضيف ورقتين: واحدة لقائمة الدول وأخرى لقائمة المدن.

```java
// كود جافا لإنشاء مصنف Excel
Workbook workbook = new Workbook();
Worksheet countrySheet = workbook.getWorksheets().get(0);
countrySheet.setName("Countries");
Worksheet citySheet = workbook.getWorksheets().add("Cities");
```

## الخطوة 2: ملء البيانات

الآن، علينا ملء أوراق العمل بالبيانات. في ورقة "الدول"، سنسرد الدول، وفي ورقة "المدن"، سنتركها فارغةً في البداية، حيث سنملأها ديناميكيًا لاحقًا.

```java
// كود جافا لملء ورقة "الدول"
countrySheet.getCells().get("A1").putValue("Country");
countrySheet.getCells().get("A2").putValue("USA");
countrySheet.getCells().get("A3").putValue("Canada");
countrySheet.getCells().get("A4").putValue("UK");
// أضف المزيد من البلدان حسب الحاجة
```

## الخطوة 3: إنشاء القوائم المنسدلة

بعد ذلك، سننشئ قوائم منسدلة لعمودي البلد والمدينة. سيتم ربط هذه القوائم المنسدلة بحيث يتم تحديث قائمة المدينة المنسدلة عند اختيار بلد.

```java
// كود جافا لإنشاء قوائم منسدلة
DataValidationCollection validations = countrySheet.getDataValidations();
DataValidation validation = validations.get(validations.add(1, 1, countrySheet.getCells().getMaxDataRow(), 1));
validation.setType(DataValidationType.LIST);
validation.setFormula1("Countries!$A$2:$A$4"); // الإشارة إلى قائمة البلدان
```

## الخطوة 4: تنفيذ القوائم المنسدلة المتتالية

الآن يأتي الجزء المثير: تنفيذ قوائم منسدلة متتالية. سنستخدم Aspose.Cells لجافا لتحديث قائمة المدينة المنسدلة ديناميكيًا بناءً على البلد المحدد.

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
                // إضافة المزيد من الحالات لدول أخرى
            }
        }
    }
});
```

## خاتمة

في هذا الدليل الشامل، استكشفنا كيفية إنشاء قوائم منسدلة متتالية في Excel باستخدام Aspose.Cells لجافا. بدأنا بإعداد المتطلبات الأساسية، وإنشاء مصنف Excel، وملء البيانات، ثم تعمقنا في تعقيدات إنشاء القوائم المنسدلة وتطبيق سلوك التتالي الديناميكي. بصفتك مطورًا، لديك الآن المعرفة والأدوات اللازمة لتحسين ملفات Excel الخاصة بك بقوائم منسدلة تفاعلية، مما يوفر تجربة مستخدم سلسة.

## الأسئلة الشائعة

### كيف يمكنني إضافة المزيد من البلدان والمدن إلى القوائم المنسدلة؟

لإضافة المزيد من الدول والمدن، عليك تحديث أوراق العمل الخاصة بها في مصنف Excel. ما عليك سوى توسيع القوائم في ورقتي "الدول" و"المدن"، وستتضمن القوائم المنسدلة الإدخالات الجديدة تلقائيًا.

### هل يمكنني استخدام هذه التقنية مع ميزات Excel الأخرى؟

بالتأكيد! يمكنك دمج القوائم المنسدلة المتتالية مع ميزات Excel المتنوعة، مثل التنسيق الشرطي والصيغ والرسوم البيانية، لإنشاء جداول بيانات فعّالة وتفاعلية مصممة خصيصًا لتلبية احتياجاتك.

### هل Aspose.Cells for Java مناسب للمشاريع الصغيرة والكبيرة؟

نعم، Aspose.Cells for Java متعدد الاستخدامات ويمكن استخدامه في مشاريع متنوعة الأحجام. سواء كنت تعمل على برنامج صغير أو تطبيق مؤسسي معقد، يُمكن لـ Aspose.Cells for Java تبسيط مهامك المتعلقة بـ Excel.

### هل أحتاج إلى مهارات برمجة متقدمة لتنفيذ القوائم المنسدلة المتتالية مع Aspose.Cells لـ Java؟

مع أن فهم أساسيات جافا مفيد، يوفر Aspose.Cells for Java وثائق وأمثلة شاملة لإرشادك خلال العملية. مع بعض التفاني والممارسة، يمكنك إتقان هذه الميزة.

### أين يمكنني العثور على المزيد من الموارد والوثائق الخاصة بـ Aspose.Cells for Java؟

يمكنك الوصول إلى الوثائق والموارد الشاملة لـ Aspose.Cells for Java على [هنا](https://reference.aspose.com/cells/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}