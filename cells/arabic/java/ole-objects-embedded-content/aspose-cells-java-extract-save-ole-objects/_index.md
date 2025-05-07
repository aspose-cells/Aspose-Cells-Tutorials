---
"date": "2025-04-08"
"description": "تعرّف على كيفية إدارة واستخراج كائنات OLE المُضمّنة في ملفات Excel بكفاءة باستخدام Aspose.Cells لـ Java. اتبع هذا الدليل خطوة بخطوة لدمج سلس."
"title": "استخراج وحفظ كائنات OLE من Excel باستخدام Aspose.Cells Java - دليل كامل"
"url": "/ar/java/ole-objects-embedded-content/aspose-cells-java-extract-save-ole-objects/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# استخراج كائنات OLE وحفظها من Excel باستخدام Aspose.Cells Java: دليل كامل

## مقدمة

تُعدّ إدارة كائنات OLE (ربط الكائنات وتضمينها) المُضمّنة في ملفات Excel مهمةً بالغة الأهمية لمطوري البرامج ومحللي البيانات. يُقدّم هذا البرنامج التعليمي دليلاً شاملاً حول استخدام Aspose.Cells لجافا لاستخراج هذه الكائنات وحفظها بكفاءة، مما يُبسّط سير عملك مع تنسيقات ملفات مُتنوّعة.

**ما سوف تتعلمه:**
- تهيئة مصنف Excel باستخدام Aspose.Cells
- استخراج كائنات OLE من الأوراق
- حفظ الملفات المستخرجة بتنسيقات مختلفة (DOCX، XLSX، PPTX، PDF)
- التعامل مع حالات محددة مثل الحفظ كملفات Excel جديدة

بحلول نهاية هذا الدليل، ستكون مجهزًا لتعزيز تطبيقات Java الخاصة بك بإمكانيات قوية للتعامل مع البيانات.

## المتطلبات الأساسية

قبل المتابعة، تأكد من أن لديك:

**المكتبات المطلوبة:**
- Aspose.Cells لـ Java (الإصدار 25.3 أو أحدث)
- التوافق مع إصدارات JDK المناسبة لتشغيل Aspose.Cells

**متطلبات إعداد البيئة:**
- فهم أساسي لأدوات بناء Java وMaven/Gradle
- بيئة تطوير متكاملة (IDE) مثل IntelliJ IDEA أو Eclipse

**المتطلبات المعرفية:**
- المعرفة بكيفية التعامل مع الملفات في جافا
- فهم كائنات OLE داخل Excel

## إعداد Aspose.Cells لـ Java

للبدء، قم بتضمين Aspose.Cells في مشروعك باستخدام التكوينات التالية:

**مافن:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**جرادل:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### الحصول على الترخيص

يوفر Aspose.Cells خيارات ترخيص مختلفة:
- **نسخة تجريبية مجانية**:قم بتنزيل نسخة تجريبية لاختبار الوظيفة.
- **رخصة مؤقتة**:الحصول على ترخيص تقييم ممتد.
- **شراء**:الحصول على ترخيص دائم للاستخدام الإنتاجي.

قم بزيارة [صفحة الشراء](https://purchase.aspose.com/buy) أو اطلب [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) بناءً على احتياجاتك.

### التهيئة الأساسية

فيما يلي كيفية تهيئة Aspose.Cells في تطبيق Java الخاص بك:
```java
import com.aspose.cells.Workbook;

public class InitializeWorkbook {
    public static void main(String[] args) {
        Workbook workbook = new Workbook("path/to/excel/file.xlsx");
        // استمر في استخدام كائن المصنف حسب الحاجة
    }
}
```

## دليل التنفيذ

### الميزة 1: استخراج كائنات OLE من Excel

**ملخص:** قم بتهيئة مصنف واستخراج الكائنات المضمنة من ورقة العمل الأولى.

#### الخطوة 1: تهيئة المصنف
قم بإعداد مسارات دليل البيانات الخاص بك وإنشاء `Workbook` مثال:
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/oleFile.xlsx");
```

#### الخطوة 2: استخراج كائنات OLE
الوصول إلى مجموعة كائنات OLE في ورقة العمل الأولى:
```java
import com.aspose.cells.OleObjectCollection;

OleObjectCollection oleObjects = workbook.getWorksheets().get(0).getOleObjects();
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    // معالجة كل كائن هنا
}
```

#### الخطوة 3: حفظ الكائنات المستخرجة
احفظ كل كائن OLE مستخرج استنادًا إلى نوع الملف الخاص به:
```java
import com.aspose.cells.FileFormatType;
import java.io.FileOutputStream;

String outDir = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    String fileName = outDir + "/object" + i + ".";

    switch (object.getFileFormatType()) {
        case FileFormatType.DOCX:
            fileName += "docx";
            break;
        case FileFormatType.XLSX:
            fileName += "xlsx";
            break;
        // أضف تنسيقات أخرى حسب الحاجة
    }

    if (object.getFileFormatType() == FileFormatType.XLSX) {
        byte[] bytes = object.getObjectData();
        Workbook oleBook = new Workbook(new java.io.ByteArrayInputStream(bytes));
        oleBook.getSettings().setHidden(false);
        oleBook.save(fileName);
    } else {
        try (FileOutputStream fos = new FileOutputStream(fileName)) {
            fos.write(object.getObjectData());
        }
    }
}
```

### الميزة 2: حفظ كائن OLE كملف Excel
**ملخص:** إظهار كيفية حفظ كائن OLE المستخرج على وجه التحديد كملف Excel.

#### الخطوة 1: استرداد بيانات OLE
افترض أن لديك `byte[] bytes` من `OleObject`:
```java
import com.aspose.cells.Workbook;
import java.io.ByteArrayInputStream;

Workbook oleBook = new Workbook(new ByteArrayInputStream(bytes));
oleBook.getSettings().setHidden(false);
oleBook.save("YOUR_OUTPUT_DIRECTORY/object.xlsx");
```

## التطبيقات العملية

- **توحيد البيانات:** استخراج أنواع مختلفة من المستندات من Excel للتخزين المركزي.
- **إنشاء التقارير التلقائية:** دمج التقارير وحفظها بتنسيقات مختلفة مباشرة من تطبيقك.
- **أدوات نقل البيانات:** استخدم البيانات المستخرجة لعمليات الهجرة بين الأنظمة.

## اعتبارات الأداء

- قم بتحسين استخدام الذاكرة من خلال إدارة الكائنات الكبيرة بكفاءة، ربما من خلال طرق البث.
- استخدم إعدادات Aspose.Cells لإدارة رؤية المصنف وحجمه بشكل ديناميكي.
- تنفيذ ممارسات فعالة للتعامل مع الملفات لمنع تسرب الموارد.

## خاتمة

باتباع هذا الدليل، يمكنك استخراج كائنات OLE وحفظها بفعالية باستخدام Aspose.Cells لـ Java. تُحسّن هذه الإمكانيات عمليات إدارة البيانات لديك بشكل ملحوظ.

**الخطوات التالية:**
فكر في استكشاف الميزات الإضافية لـ Aspose.Cells مثل معالجة المخططات أو تحويلات ملفات Excel المتقدمة لتوسيع تطبيقات Java الخاصة بك بشكل أكبر.

## قسم الأسئلة الشائعة

1. **كيف يمكنني التعامل مع تنسيقات كائنات OLE غير المدعومة؟**
   - استخدم تنسيقًا افتراضيًا (مثل JPG) للأشياء غير المعروفة.
2. **هل يمكنني استخراج كائنات OLE من أوراق متعددة؟**
   - نعم، قم بالتكرار على كل ورقة عمل في المصنف وكرر عملية الاستخراج.
3. **ماذا لو فشل كائن OLE في الحفظ بشكل صحيح؟**
   - تحقق من أذونات الملف وتأكد من صحة مسارات دليل الإخراج.
4. **هل يدعم Aspose.Cells جميع إصدارات Excel؟**
   - يدعم Aspose.Cells مجموعة واسعة من تنسيقات Excel، بما في ذلك التنسيقات القديمة مثل XLS.
5. **كيف أقوم بتحسين الأداء عند التعامل مع الملفات الكبيرة؟**
   - فكر في معالجة البيانات على شكل أجزاء أو استخدام تقنيات تدفق الملفات لإدارة استخدام الذاكرة بشكل فعال.

## موارد
- [التوثيق](https://reference.aspose.com/cells/java/)
- [تنزيل Aspose.Cells](https://releases.aspose.com/cells/java/)
- [شراء التراخيص](https://purchase.aspose.com/buy)
- [تنزيلات تجريبية مجانية](https://releases.aspose.com/cells/java/)
- [طلب ترخيص مؤقت](https://purchase.aspose.com/temporary-license/)
- [منتدى دعم المجتمع](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}