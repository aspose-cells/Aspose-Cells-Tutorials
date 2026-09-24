---
category: general
date: 2026-03-29
description: كيفية استبدال المتغيرات في JSON باستخدام SmartMarker – تعلم استخدام تعبير
  if، تطبيق المنطق الشرطي، ضرب القيم، وإنشاء JSON بسهولة.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: ar
og_description: كيفية استبدال المتغيرات في JSON باستخدام SmartMarker. اكتشف كيفية
  استخدام تعبير if، وتطبيق المنطق الشرطي، وضرب القيم، وتوليد JSON في دقائق.
og_title: كيفية استبدال المتغيرات في JSON باستخدام SmartMarker – خطوة بخطوة
tags:
- C#
- SmartMarker
- JSON templating
title: كيفية استبدال المتغيرات في JSON باستخدام SmartMarker – دليل كامل
url: /ar/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استبدال المتغيرات في JSON باستخدام SmartMarker – دليل كامل

هل تساءلت يومًا **how to substitute variables** داخل حمولة JSON دون كتابة محلل مخصص؟ لست وحدك. في العديد من سيناريوهات التكامل—فكر في الفواتير، محركات التسعير، أو ملفات التكوين الديناميكية—تحتاج إلى حقن قيم وقت التشغيل، تطبيق شروط بسيطة، وربما حتى إجراء عملية ضرب سريعة. يوضح لك هذا الدرس بالضبط **how to substitute variables** باستخدام مكتبة SmartMarker، مع الحفاظ على JSON نظيفًا وقابلًا للقراءة.

سنستعرض مثالًا واقعيًا يغطي **use if expression**، **how to apply conditional**، **how to multiply values**، و **how to generate json** في الوقت الفعلي. في النهاية، ستحصل على مقطع C# جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- إعداد `SmartMarkerOptions` لتخزين المتغيرات القابلة لإعادة الاستخدام.  
- كتابة قالب JSON يحتوي على تعبير `if` للمنطق الشرطي.  
- ضرب قيمة في متغير داخل القالب.  
- معالجة القالب باستخدام `SmartMarkerProcessor` والحصول على سلسلة JSON النهائية.  
- استكشاف الأخطاء الشائعة مثل المتغيرات المفقودة أو التعابير غير الصحيحة.

بدون خدمات خارجية، بدون تبعيات ثقيلة—فقط C# عادي وحزمة SmartMarker NuGet.

---

## كيفية استبدال المتغيرات – نظرة عامة خطوة بخطوة

فيما يلي صورة عالية المستوى لسير العمل. فكر فيها كخط أنابيب حيث يدخل قالب JSON الخام الخاص بك من اليسار، يقوم محرك SmartMarker بسحره، وتخرج JSON المُنشأة بالكامل من اليمين.

![مخطط يوضح كيفية استبدال المتغيرات في JSON](https://example.com/images/smartmarker-flow.png "كيفية استبدال المتغيرات في JSON")

*نص بديل للصورة: مخطط يوضح كيفية استبدال المتغيرات في JSON.*

---

## الخطوة 1: تثبيت واستيراد SmartMarker

قبل أن تبدأ، تأكد من أن حزمة SmartMarker مُشار إليها في مشروعك. إذا كنت تستخدم .NET CLI، نفّذ:

```bash
dotnet add package SmartMarker
```

بعد ذلك، أضف توجيهات `using` اللازمة في أعلى ملف C# الخاص بك:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **نصيحة احترافية:** أحدث نسخة (اعتبارًا من مارس 2026) هي 2.4.1. تدعم .NET 6 وما بعده، لكنها تعمل بشكل جيد مع .NET Framework 4.7 أيضًا.

---

## الخطوة 2: إنشاء خيارات SmartMarker وتعريف المتغيرات

الآن سننشئ مثالًا من `SmartMarkerOptions` سيحتوي على أي متغيرات نرغب في إعادة استخدامها عبر القالب. هنا نجيب على سؤال **how to substitute variables**—المتغيرات تعمل كعناصر نائبة سيستبدلها SmartMarker لاحقًا.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

لماذا نخزن المعدل في `Variables` بدلاً من تعيينه صراحةً؟ لأنك قد تجلب هذا الرقم من قاعدة بيانات، ملف إعدادات، أو إدخال المستخدم. حفظه في الخيارات يجعل القالب قابلًا لإعادة الاستخدام والاختبار.

---

## الخطوة 3: كتابة قالب JSON مع تعبير `if`

هنا يبرز دور كلمة **use if expression**. يتيح لك SmartMarker تضمين المنطق الشرطي مباشرة داخل سلسلة JSON. يبدو التركيب كاسم خاصية، لكن SmartMarker يتعامل معه كتعليمات.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

لاحظ المفتاح `if(Amount>500)`. يقوم SmartMarker بتقييم التعبير `Amount>500`؛ إذا كان صحيحًا، تُدرج القيمة المقابلة (`${Amount * Rate}`) في الناتج. تركيبة `${...}` هي محرك *استبدال المتغيرات*—هنا نطبق **how to multiply values** (`Amount * Rate`) قبل حقن النتيجة.

---

## الخطوة 4: معالجة القالب واسترجاع JSON النهائي

مع إعداد الخيارات والقالب، نسلم كل شيء إلى المعالج. تقوم الطريقة `ProcessJson` بتحليل القالب، تطبيق الشرط، إجراء الضرب، وإرجاع سلسلة JSON نظيفة.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

تشغيل المقتطف يطبع:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**ماذا حدث؟**  
- `Amount` يساوي 1000، وهو يحقق الشرط `Amount>500`.  
- SmartMarker يقيم `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- المفتاح الشرطي الأصلي (`if(Amount>500)`) يُستبدل باسم خاصية نظيف (`Result`). بشكل افتراضي يستخدم SmartMarker `"Result"` لكن يمكنك تخصيصه (المزيد لاحقًا).

إذا غيرت `Amount` إلى `400`، يصبح الناتج:

```json
{
  "Amount": 400
}
```

يختفي الجزء الشرطي لأن التعبير قيمته `false`. هذا هو جوهر **how to apply conditional** في JSON.

---

## الخطوة 5: تخصيص اسم خاصية الإخراج (اختياري)

أحيانًا لا تريد المفتاح العام `"Result"`. يتيح لك SmartMarker تحديد اسم مخصص باستخدام خيار `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

النتيجة:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

الآن يتم تخزين القيمة الشرطية تحت اسم خاصية أكثر معنى—مثالي للخدمات اللاحقة التي تتوقع حقلًا محددًا.

---

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثه | الحل |
|-------|----------------|-----|
| المتغير غير موجود | قمت بالإشارة إلى متغير غير موجود في `smartMarkerOptions.Variables`. | تحقق من التهجئة وتأكد من إضافة المتغير قبل المعالجة. |
| صيغة `if` غير صالحة | فقدان الأقواس أو استخدام عامل غير صحيح (`>`, `<`, `==`). | اتبع النمط الدقيق `if(<expression>)`؛ يدعم SmartMarker فقط المقارنات العددية البسيطة. |
| JSON يصبح غير صالح | ترك فاصلة زائدة عن طريق الخطأ بعد الكتلة الشرطية. | دع SmartMarker يتعامل مع الإزالة؛ حافظ على صحة القالب الأصلي من الناحية النحوية. |
| تنسيق رقم غير متوقع | تظهر النتيجة كسلسلة `"80"` بدلاً من رقم. | قم بالتحويل أو التحليل لاحقًا، أو استخدم `${(Amount * Rate):N0}` لتنسيق رقمي. |

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله. يوضح **how to generate json** باستخدام متغيرات ديناميكية، شروط، وحسابات رياضية—كل ذلك في أقل من 30 سطرًا.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

لا تتردد في تغيير `Amount` لاختبار الفرع الشرطي، أو تعديل `Rate` لرؤية حسابات خصم مختلفة.

---

## توسيع النمط – المزيد من سيناريوهات “How to”

- **How to substitute variables** من ملف إعدادات: حمّل `Dictionary<string, object>` من `appsettings.json` ومرره إلى `smartMarkerOptions.Variables`.  
- **How to use if expression** لعدة شروط: ربطها مثل `"if(Amount>500 && CustomerType=='VIP')"`—يدعم SmartMarker عمليات AND/OR المنطقية.  
- **How to apply conditional** تنسيق: استخدم `${Amount:0.00}` داخل التعبير للتحكم في عدد الأرقام العشرية.  
- **How to multiply values** باستخدام حسابات أكثر تعقيدًا: `${(Amount - Discount) * TaxRate}` يعمل بنفس الطريقة.  
- **How to generate json** للكائنات المتداخلة: ضع الكتلة الشرطية داخل كائن JSON آخر، وسيحافظ SmartMarker على الهيكل.

---

## الخلاصة

لقد غطينا **how to substitute variables** في JSON باستخدام SmartMarker، وأظهرنا **use if expression** للإدراج الشرطي، وشرحنا **how to apply conditional** في المنطق، وعرضنا **how to multiply values** داخل القالب، وأخيرًا أوضحنا **how to generate json** الجاهز للاستخدام في الخدمات اللاحقة. النهج خفيف الوزن، لا يتطلب محرك قوالب خارجي، ويتناسب بسهولة مع أي قاعدة شفرة C#.

جرّبه—عدّل المتغيرات، أضف شروطًا أكثر، أو غلف كل ذلك في فئة مساعدة لإعادة الاستخدام عبر الحل الخاص بك. عندما تحتاج إلى إنتاج JSON ديناميكي بسرعة، فإن SmartMarker خيار قوي وجاهز للإنتاج.

**الخطوات التالية**

- استكشف ميزات SmartMarker المتقدمة مثل الحلقات (`foreach`) والوظائف المخصصة.  
- ادمج هذه التقنية مع نقاط النهاية في ASP.NET Core لتقديم واجهات برمجة تطبيقات JSON ديناميكية.  
- استكشف مكتبات القوالب الأخرى (مثل Handlebars.NET) للمقارنة، خاصة إذا كنت تحتاج إلى صياغة أغنى.

هل لديك أسئلة أو حالة استخدام معينة تواجهها؟ اترك تعليقًا أدناه، ولنحل المشكلة معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}