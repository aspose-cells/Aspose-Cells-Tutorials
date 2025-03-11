---
title: إنشاء التحقق من صحة البيانات المخصصة
linktitle: إنشاء التحقق من صحة البيانات المخصصة
second_title: واجهة برمجة تطبيقات معالجة Excel في Java من Aspose.Cells
description: تعرف على كيفية إنشاء التحقق المخصص للبيانات باستخدام Aspose.Cells لـ Java. دليل خطوة بخطوة مع الكود المصدر.
weight: 10
url: /ar/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء التحقق من صحة البيانات المخصصة


## مقدمة

تساعد عملية التحقق من صحة البيانات في الحفاظ على سلامة البيانات من خلال منع المستخدمين من إدخال بيانات غير صحيحة أو غير صالحة في جداول بيانات Excel. وفي حين يوفر Excel خيارات التحقق من صحة البيانات المضمنة، فهناك سيناريوهات تحتاج فيها إلى تحديد قواعد التحقق المخصصة. وتمكنك Aspose.Cells for Java من تحقيق ذلك بكفاءة.

## المتطلبات الأساسية

قبل الغوص في الكود، تأكد من أن لديك المتطلبات الأساسية التالية:

-  Aspose.Cells for Java: قم بتنزيل المكتبة وتثبيتها من[هنا](https://releases.aspose.com/cells/java/).

## الخطوة 1: إعداد مشروع Java الخاص بك

للبدء، قم بإنشاء مشروع Java جديد في بيئة التطوير المتكاملة المفضلة لديك. أضف مكتبة Aspose.Cells for Java إلى مسار فئة المشروع الخاص بك.

## الخطوة 2: إنشاء مصنف Excel

لنبدأ بإنشاء مصنف Excel جديد باستخدام Aspose.Cells for Java.

```java
// كود جافا لإنشاء مصنف Excel جديد
Workbook workbook = new Workbook();
```

## الخطوة 3: إضافة ورقة عمل

الآن، دعنا نضيف ورقة عمل إلى المصنف حيث سنطبق التحقق من صحة البيانات المخصصة لدينا.

```java
// كود جافا لإضافة ورقة عمل
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## الخطوة 4: تحديد معايير التحقق المخصصة

في هذه الخطوة، سنحدد معايير التحقق المخصصة التي يجب أن تلتزم بها بياناتنا. لنفترض أننا نريد تقييد العمر المدخل في خلية ما بحيث يتراوح بين 18 و60 عامًا.

```java
// كود جافا لتحديد معايير التحقق المخصصة
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## الخطوة 5: تطبيق التحقق من صحة البيانات على نطاق

الآن بعد أن حددنا معايير التحقق المخصصة، فلنطبقها على نطاق محدد من الخلايا.

```java
// كود جافا لتطبيق التحقق من صحة البيانات على نطاق
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // تطبيق التحقق على الصفوف العشرة الأولى
area.endColumn = 0;

validation.addArea(area);
```

## الخطوة 6: حفظ ملف Excel

وأخيرًا، احفظ ملف Excel مع تطبيق قواعد التحقق من صحة البيانات المخصصة.

```java
// كود جافا لحفظ ملف الاكسل
workbook.save("CustomDataValidation.xlsx");
```

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية إنشاء قواعد مخصصة للتحقق من صحة البيانات باستخدام Aspose.Cells for Java. باتباع هذه الخطوات، يمكنك التأكد من أن بيانات Excel الخاصة بك تلتزم بمعايير محددة، مما يعزز سلامة البيانات ودقتها.

## الأسئلة الشائعة

### كيف يمكنني تنزيل Aspose.Cells لـ Java؟

 يمكنك تنزيل Aspose.Cells لـ Java من موقع الويب على[هنا](https://releases.aspose.com/cells/java/).

### هل يمكنني تطبيق التحقق من صحة البيانات المخصصة على نطاقات متعددة في نفس ورقة العمل؟

نعم، يمكنك تطبيق التحقق من صحة البيانات المخصصة على نطاقات متعددة ضمن نفس ورقة العمل عن طريق تكرار الخطوة 5 لكل نطاق مرغوب.

### هل هناك أنواع أخرى من التحقق من صحة البيانات التي يدعمها Aspose.Cells لـ Java؟

نعم، يدعم Aspose.Cells for Java أنواعًا مختلفة من التحقق من صحة البيانات، بما في ذلك الأعداد الصحيحة والأعداد العشرية والتاريخ والوقت وطول النص والمزيد.

### كيف يمكنني تخصيص رسالة الخطأ التي تظهر عند فشل التحقق من صحة البيانات؟

 يمكنك تخصيص رسالة الخطأ عن طريق تعديل`setErrorMessage` الطريقة في الخطوة 4، حيث يمكنك تحديد معايير التحقق.

### هل يعمل Aspose.Cells for Java مع ملفات Excel بتنسيقات مختلفة؟

نعم، يدعم Aspose.Cells for Java مجموعة واسعة من تنسيقات ملفات Excel، بما في ذلك XLS، وXLSX، وXLSM، والمزيد.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
