---
title: فتح ملفات CSV باستخدام المحلل المفضل
linktitle: فتح ملفات CSV باستخدام المحلل المفضل
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية فتح ملفات CSV وتحليلها باستخدام المحللات المخصصة في Aspose.Cells for .NET. تعامل مع النصوص والتاريخ بسهولة. مثالي للمطورين.
weight: 11
url: /ar/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# فتح ملفات CSV باستخدام المحلل المفضل

## مقدمة
عند التعامل مع ملفات CSV، قد ترغب أحيانًا في التعامل مع أنواع بيانات مختلفة باستخدام محللات مخصصة. سيرشدك هذا البرنامج التعليمي إلى كيفية فتح ملفات CSV باستخدام محلل مفضل باستخدام Aspose.Cells for .NET. سواء كنت ترغب في التعامل مع النصوص أو التواريخ أو التنسيقات المخصصة الأخرى، فسيرشدك هذا الدليل خلال كل خطوة بشرح واضح.
## المتطلبات الأساسية
قبل الغوص في الكود، دعنا نغطي العناصر الأساسية التي تحتاجها للبدء.
1.  مكتبة Aspose.Cells لـ .NET: تأكد من تثبيت مكتبة Aspose.Cells. يمكنك تنزيلها[هنا](https://releases.aspose.com/cells/net/) يمكنك أيضًا استخدام الإصدار التجريبي المجاني[هنا](https://releases.aspose.com/).
2. بيئة تطوير .NET: يوصى باستخدام Visual Studio، ولكن أي بيئة تطوير متكاملة متوافقة مع .NET سوف تعمل.
3. المعرفة الأساسية بلغة C#: يفترض هذا البرنامج التعليمي أنك على دراية بلغة C# والبرمجة الموجهة للكائنات.
## استيراد الحزم
لاستخدام Aspose.Cells، ستحتاج إلى استيراد المساحات الأساسية اللازمة في الجزء العلوي من ملف C# الخاص بك:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
الآن بعد أن هيأنا المسرح، دعنا نتعرف على كيفية فتح ملف CSV باستخدام المحلل المفضل، والتعامل مع تنسيقات البيانات المختلفة مثل النص والتاريخ.
## الخطوة 1: تحديد المحللات المخصصة
 للتعامل مع أنواع بيانات مختلفة، مثل النص أو تنسيقات التاريخ المحددة، تحتاج إلى تعريف محللات مخصصة. في Aspose.Cells، تنفذ المحللات المخصصة`ICustomParser` واجهة.
### 1.1 إنشاء محلل نص
يتعامل هذا المحلل مع قيم النص العادية. ولا يعدل التنسيق، لذا يتم إرجاع القيمة كما هي.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 ال`ParseObject` الطريقة ببساطة تعيد قيمة الإدخال. الأمر أشبه بقولك "لا تغير أي شيء، فقط أعطني النص!"
### 1.2 إنشاء محلل تاريخ
 بالنسبة للتواريخ، ستحتاج إلى التأكد من تحليل بيانات CSV بشكل صحيح`DateTime` الأشياء. إليك كيفية إنشاء محلل تاريخ:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 في هذا المحلل، نستخدم`ParseExact` لضمان تفسير التاريخ بشكل صحيح بناءً على تنسيق محدد مسبقًا (`"dd/MM/yyyy"`بهذه الطريقة، سيتم معالجة أي تاريخ في ملف CSV الخاص بك يتبع هذا التنسيق دون مشاكل.
## الخطوة 2: تكوين خيارات التحميل
 بعد ذلك، تحتاج إلى تكوين كيفية تحميل ملف CSV. يتم ذلك باستخدام`TxtLoadOptions` الفئة، التي تسمح لك بتحديد خيارات التحليل، بما في ذلك الترميز والمحللات المخصصة.
### 2.1 إعداد خيارات التحميل
 سنبدأ بتهيئة`TxtLoadOptions` وتحديد المعلمات الرئيسية مثل الفاصل والترميز:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- الفاصل: يحدد هذا الحرف المستخدم لفصل القيم في ملف CSV (الفاصلات، في هذه الحالة).
- الترميز: نستخدم ترميز UTF-8 للتعامل مع مجموعة واسعة من الأحرف.
-  ConvertDateTimeData: يؤدي تعيين هذا على true إلى ضمان تحويل قيم التاريخ تلقائيًا إلى`DateTime` الأشياء عندما يكون ذلك ممكنا.
### 2.2 تطبيق المحللات المخصصة
بعد ذلك، سنقوم بتعيين المحللات التي أنشأناها سابقًا للتعامل مع القيم الموجودة في ملف CSV:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 يخبر هذا Aspose.Cells باستخدام`TextParser` لقيم النص العامة و`DateParser`لأي حقول تاريخ يواجهها في ملف CSV.
## الخطوة 3: تحميل ملف CSV وقراءته
 الآن بعد تكوين خيارات التحميل، يمكنك تحميل ملف CSV إلى`Aspose.Cells.Workbook` هدف.
### 3.1 تحميل ملف CSV
 نقوم بتحميل ملف CSV عن طريق تمرير مسار الملف والملفات التي تم تكوينها`TxtLoadOptions` الى`Workbook` المنشئ:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
تؤدي هذه الخطوة إلى تحويل بيانات CSV إلى مصنف Excel يعمل بكامل طاقته، مع تحليل كل قيمة وفقًا للقواعد المفضلة لديك.
## الخطوة 4: الوصول إلى بيانات الخلية وعرضها
بمجرد تحميل ملف CSV إلى المصنف، يمكنك البدء في العمل بالبيانات. على سبيل المثال، قد ترغب في طباعة نوع وقيمة خلايا معينة.
### 4.1 استرداد وعرض الخلية A1
لنستعيد الخلية الأولى (A1) ونعرض قيمتها ونوعها:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 هنا،`Type` تُظهر الخاصية نوع البيانات (مثل`String` أو`DateTime` )، و`DisplayStringValue` يعطيك القيمة المنسقة.
### 4.2 استرداد وعرض الخلية B1
وبنفس الطريقة، يمكننا استرداد وعرض خلية أخرى، مثل B1:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
يمكن تكرار هذه العملية لعدد الخلايا التي تحتاج إلى فحصها.
## الخطوة 5: احفظ المصنف
 بعد العمل بالبيانات، قد ترغب في حفظ المصنف في ملف جديد. يجعل Aspose.Cells هذا الأمر سهلاً باستخدام طريقة بسيطة`Save` طريقة:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
يؤدي هذا إلى حفظ المصنف كملف Excel، مع الحفاظ على كافة التنسيقات وتحليل البيانات التي قمت بتطبيقها.
## خاتمة
إن فتح ملفات CSV باستخدام محلل مفضل في Aspose.Cells for .NET هو طريقة مرنة وقوية للتعامل مع أنواع مختلفة من البيانات. من خلال إنشاء محللات مخصصة وتكوين خيارات التحميل، يمكنك التأكد من تحليل ملفات CSV الخاصة بك بالضبط بالطريقة التي تريدها، سواء كنت تتعامل مع نص أو تواريخ أو تنسيقات مخصصة أخرى. باستخدام هذا البرنامج التعليمي، أصبحت الآن مجهزًا للتعامل مع سيناريوهات تحليل البيانات الأكثر تعقيدًا في مشاريعك.
## الأسئلة الشائعة
### ما هو الغرض من المحللات المخصصة في Aspose.Cells لـ .NET؟
تتيح لك المحللات المخصصة تحديد كيفية تحليل أنواع بيانات معينة، مثل النص أو التواريخ، عند تحميل ملف CSV.
### هل يمكنني استخدام حرف فاصل مختلف في ملف CSV؟
 نعم، يمكنك تحديد أي حرف كفاصل في`TxtLoadOptions.Separator` ملكية.
### كيف أتعامل مع الترميز في Aspose.Cells عند تحميل ملف CSV؟
 يمكنك ضبط`Encoding` ممتلكات`TxtLoadOptions` إلى أي مخطط ترميز مثل UTF-8، ASCII، وما إلى ذلك.
### ماذا يحدث إذا كان تنسيق التاريخ في ملف CSV مختلفًا؟
بإمكانك تحديد تنسيق التاريخ المحدد باستخدام محلل مخصص، مما يضمن التحليل الصحيح لقيم التاريخ.
### هل يمكنني حفظ المصنف بتنسيقات أخرى؟
نعم، يسمح لك Aspose.Cells بحفظ المصنف بتنسيقات مختلفة مثل XLSX، وCSV، وPDF، والمزيد.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
