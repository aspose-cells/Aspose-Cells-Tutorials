---
category: general
date: 2026-01-14
description: كيفية تضمين الخطوط في HTML وإجبار حساب الصيغ أثناء تحويل Excel إلى HTML.
  تعلم تعيين منطقة الطباعة وتصدير المخططات.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: ar
og_description: كيفية تضمين الخطوط في HTML، فرض حساب الصيغ، وتحويل Excel إلى HTML
  مع إعدادات منطقة الطباعة — كل ذلك باستخدام C#.
og_title: كيفية تضمين الخطوط في HTML – دليل C# الكامل
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية تضمين الخطوط في HTML – دليل C# الكامل
url: /ar/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في HTML – دليل C# كامل

هل تساءلت يومًا **كيف يتم تضمين الخطوط في HTML** عند تصدير مصنف Excel؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يبدو HTML المُولد جيدًا على جهازهم لكنه يفقد الطباعة على جهاز آخر. الخبر السار؟ مع Aspose.Cells for .NET يمكنك تضمين ملفات الخطوط الدقيقة مباشرةً داخل مخرجات HTML — لا مزيد من الأحرف المفقودة.

في هذا الدرس سنستعرض مثالًا شاملًا لا يوضح فقط **كيفية تضمين الخطوط في HTML**، بل يُظهر أيضًا **فرض حساب الصيغ**، **تحويل Excel إلى HTML**، وحتى **كيفية تعيين منطقة الطباعة** قبل تصدير مخطط إلى PPTX قابل للتحرير. في النهاية ستحصل على برنامج C# واحد قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

---

## ما ستقوم ببنائه

- إنشاء مصنف جديد، كتابة بعض صيغ المصفوفة، و**فرض حساب الصيغ** بحيث تُدمج النتائج في الملف.
- حفظ المصنف كـ HTML مع **تضمين الخطوط** ومحددات التباين الخاصة بها.
- تحميل مصنف ثانٍ يحتوي على مخطط، تعريف **منطقة الطباعة**، وتصدير تلك الورقة إلى عرض تقديمي PowerPoint قابل للتحرير.
- كل ذلك باستخدام عدد قليل من الأسطر النظيفة والمُعَلَّقة جيدًا من كود C#.

لا أدوات خارجية، لا نسخ يدوي لملفات الخطوط — Aspose.Cells يتولى كل العمل الشاق نيابةً عنك.

---

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث | ميزات لغة حديثة وأداء أفضل |
| Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`) | يوفر `Workbook`، `HtmlSaveOptions`، `ImageOrPrintOptions`، إلخ |
| بضع ملفات خط TrueType/OpenType (مثل `Arial.ttf`) موجودة في مجلد المشروع | ضرورية للتضمين؛ سيقوم Aspose بسحبها تلقائيًا إذا كانت مُثبتة على نظام التشغيل |
| معرفة أساسية بـ C# | لتتبع الكود وتكييفه مع سيناريوهاتك الخاصة |

---

## الخطوة 1 – إنشاء مصنف وكتابة صيغ المصفوفة  

أولًا نقوم بإنشاء كائن `Workbook` جديد ونضع صيغتي مصفوفة في الخلايا **A1** و **A3**. تُنتج هذه الصيغ (`WRAPCOLS` و `WRAPROWS`) مصفوفة صغيرة مكوّنة من عمودين/صفين سنرى لاحقًا كيف تُعرض في مخرجات HTML.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **لماذا هذا مهم:** بإدراج الصيغ تحصل على محتوى ديناميكي سيتم تقييمه عندما نفرض الحساب لاحقًا. كما يُظهر أن تصدير HTML يمكنه التعامل مع نتائج المصفوفة بشكل صحيح.

---

## الخطوة 2 – فرض حساب الصيغ  

تقوم Aspose.Cells بحساب الصيغ بشكل كسول. لضمان أن يحتوي HTML على القيم المحسوبة (بدلاً من الصيغ الخام)، نستدعي `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **نصيحة محترف:** إذا تخطيت هذه الخطوة، سيعرض HTML نص الصيغة (`=WRAPCOLS...`) بدلًا من الأرقام، مما يُفقد التصدير مظهره المصقول.

---

## الخطوة 3 – تكوين خيارات حفظ HTML لتضمين الخطوط  

الآن يأتي نجم العرض: تضمين الخطوط. ضبط `EmbedFonts` على `true` يخبر Aspose بأن يضمّن بيانات الخط كتيارات Base64 داخل ملف HTML المُولد. تمكين `EmbedFontVariationSelectors` يضمن أيضًا أن أي محددات تباين OpenType (المستخدمة للطباعة المتقدمة) تُحفظ.

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **كيف يعمل:** عند كتابة HTML، يضيف Aspose كتلة `<style>` تحتوي على قواعد `@font-face` التي تشير إلى بيانات URI المضمَّنة. ستعرض المتصفحات الخط نفسه بغض النظر عن الخطوط المثبتة على جهاز العميل.

---

## الخطوة 4 – حفظ المصنف كـ HTML  

نحفظ المصنف أولًا كملف `.xlsx` (للاحتياط إذا احتجت المصدر) ثم نصدره إلى HTML باستخدام الخيارات التي عرّفناها للتو.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **النتيجة:** افتح `fontDemo.html` في أي متصفح حديث وسترى قيم المصفوفة مُعرضة بالخط المضمّن، حتى وإن لم يكن الخط مثبتًا على جهازك.

---

## الخطوة 5 – تحميل مصنف يحتوي على مخطط وتعيين منطقة الطباعة  

بعد ذلك نوضح **كيفية تعيين منطقة الطباعة** قبل تصدير ورقة تحتوي على مخطط. تحدد منطقة الطباعة ما سيتم تصديره، وهو مفيد عندما تريد نطاقًا محددًا فقط في PPTX النهائي.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **لماذا نحدد منطقة طباعة؟** بدون ذلك، سيقوم Aspose بتصدير الورقة بأكملها، مما قد يجلب صفوفًا/أعمدة فارغة ويزيد حجم ملف PPTX.

---

## الخطوة 6 – تصدير الورقة إلى PPTX قابل للتحرير  

أخيرًا نصدر الورقة إلى ملف PowerPoint قابل للتحرير. بضبط `ExportChartAsEditable = true`، يُحفظ المخطط كأشكال PowerPoint أصلية، مما يسمح للمستخدمين بتعديلها مباشرةً في PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **ما ستحصل عليه:** `editableChart.pptx` يحتوي على المخطط من `chartEditable.xlsx` ككائنات PowerPoint قابلة للتحرير، مقيدة بالنطاق `A1:G20`.

---

## نظرة عامة على المخرجات المتوقعة  

| الملف | الوصف |
|------|-------------|
| `fontDemo.xlsx` | المصنف الأصلي مع صيغ المصفوفة المحسوبة. |
| `fontDemo.html` | ملف HTML **يضمّن الخطوط**، يعرض نتائج المصفوفة، ويعمل دون اتصال. |
| `editableChart.pptx` | عرض تقديمي PowerPoint يحتوي على مخطط قابل للتحرير، مع احترام **منطقة الطباعة** التي حددتها. |

افتح `fontDemo.html` في Chrome أو Edge؛ ستلاحظ أن النص يستخدم الخط المحدد (مثل Arial) حتى وإن لم يكن موجودًا على نظامك. يمكن النقر المزدوج على المخطط في `editableChart.pptx` وتعديله كما لو كان مخطط PowerPoint أصلي.

---

## أسئلة شائعة وحالات خاصة  

### ماذا لو لم يكن الخط مثبتًا على الخادم؟  
ستقوم Aspose.Cells بتضمين الخطوط *المتاحة* فقط للوقت التشغيلي. إذا كان ملف خط معين مفقودًا، سيتراجع HTML إلى الخط الافتراضي للمتصفح. لضمان التضمين، انسخ ملفات `.ttf`/`.otf` المطلوبة إلى مجلد تطبيقك واستخدم `FontInfo` (سيناريو متقدم).

### هل يمكن تضمين جزء فقط من الأحرف لتقليل حجم الملف؟  
نعم. استخدم `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. هذا يُخبر Aspose بأن يضمّن فقط الرموز المستخدمة فعليًا في المصنف، مما يقلل حجم HTML بشكل كبير.

### هل **فرض حساب الصيغ** يعمل أيضًا مع الدوال المتقلبة مثل `NOW()`؟  
بالطبع. `CalculateFormula()` يُقيم جميع الصيغ، بما فيها المتقلبة، في اللحظة التي تستدعيها فيها. إذا أردت أن يعكس الحساب تاريخًا/وقتًا محددًا، اضبط `CalculationOptions` للمصنف مسبقًا.

### ماذا عن المصنفات الكبيرة — هل سيؤدي تضمين الخطوط إلى زيادة حجم HTML؟  
تضيف الخطوط المضمَّنة تقريبًا 100‑200 KB لكل خط (حسب الحجم). بالنسبة للتقارير الضخمة، فكر في ربط الخطوط المستضافة على الويب بدلًا من تضمينها، أو استخدم وضع الـ subset المذكور أعلاه.

---

## نصائح احترافية وأفضل الممارسات  

- **حفظ دفعي:** إذا كنت تُولِّد عشرات ملفات HTML، أعد استخدام كائن `HtmlSaveOptions` واحد لتجنب تخصيصات غير ضرورية.  
- **تخزين مناطق الطباعة مؤقتًا:** عند تصدير عدة أوراق، احفظ نطاقات الطباعة المطلوبة في ملف إعدادات لتقليل تكرار الكود.  
- **التحقق من المخرجات:** بعد حفظ HTML، نفّذ فحصًا سريعًا باستخدام متصفح رأسٍ (مثل Puppeteer) للتأكد من أن الخطوط تُعرض بشكل صحيح قبل توزيعها على المستخدمين.  
- **قفل الإصدار:** الكود أعلاه يستهدف Aspose.Cells 23.12+. قد تُضيف الإصدارات الأحدث خيارات إضافية مثل `FontEmbeddingMode`. راجع دائمًا ملاحظات الإصدار.

---

## الخاتمة  

غطّينا **كيفية تضمين الخطوط في HTML** باستخدام Aspose.Cells، وأظهرنا أهمية **فرض حساب الصيغ**، وعرضنا سير عمل نظيف لتحويل Excel إلى HTML، وشرحنا **كيفية تعيين منطقة الطباعة** قبل تصدير مخطط إلى PPTX قابل للتحرير. المثال الكامل القابل للتنفيذ موجود في ملف `Program.cs` واحد، لذا يمكنك نسخه، تعديل المسارات، وتشغيله اليوم.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال الخط المضمّن بخط علامة تجارية مخصّص، أو جرّب وضع الـ `Subset` لتبقي HTML خفيفًا. نفس النمط يعمل مع PDFs، الصور، وحتى تصدير CSV — فقط غيّر فئة `SaveOptions`.

هل لديك المزيد من الأسئلة حول تضمين الخطوط، معالجة الصيغ، أو حيل منطقة الطباعة؟ اترك تعليقًا أدناه أو تواصل معي عبر منتديات مجتمع Aspose. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}