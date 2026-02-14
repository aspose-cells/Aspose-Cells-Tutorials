---
category: general
date: 2026-02-14
description: 'قم بأتمتة إنشاء الفواتير باستخدام SmartMarker: تعلم كيفية تكرار أوراق
  العمل، وتسميتها ديناميكياً، وإتقان تسمية أوراق العمل الديناميكية في دقائق.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: ar
og_description: قم بأتمتة إنشاء الفواتير باستخدام SmartMarker. يوضح هذا الدليل كيفية
  تكرار أوراق العمل، وتسميتها ديناميكياً، وإتقان تسمية أوراق العمل الديناميكية.
og_title: أتمتة إنشاء الفواتير – تسمية أوراق العمل الديناميكية والتكرار
tags:
- C#
- SmartMarker
- Excel Automation
title: أتمتة إنشاء الفواتير – تسمية ورقة العمل ديناميكيًا وتكرارها في C#
url: /ar/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# أتمتة إنشاء الفواتير – تسمية أوراق العمل ديناميكيًا وتكرارها في C#

هل تساءلت يومًا كيف **أتمتة إنشاء الفواتير** دون الحاجة إلى نسخ الأوراق يدويًا لكل طلب؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى ورقة عمل منفصلة لكل فاتورة ويرغبون أيضًا في أن يعكس اسم الورقة رقم الطلب. في هذا الدرس سنحل هذه المشكلة باستخدام `SmartMarkerProcessor` من SmartMarker ونُظهر لك **كيفية تسمية أوراق العمل** ديناميكيًا مع تغطية **كيفية تكرار ورقة العمل** لكل سجل. في النهاية ستحصل على عينة C# جاهزة للتنفيذ تُنتج مصنفًا حيث كل فاتورة توجد في تبويب خاص بها، مُسمى بشكل جميل.

سنستعرض كل خطوة—من سحب الطلبات من مصدر البيانات إلى تكوين `SmartMarkerOptions` لتسمية أوراق العمل ديناميكيًا. لا حاجة إلى وثائق خارجية؛ كل ما تحتاجه موجود هنا. معرفة أساسية بـ C# وإشارة إلى مكتبة Aspose.Cells (أو أي محرك متوافق مع SmartMarker) كافية.

---

## ما ستبنيه

- استرجاع مجموعة من كائنات الطلب.
- تكوين SmartMarker لت **تكرار ورقة عمل** لكل طلب.
- تطبيق **تسمية أوراق العمل ديناميكيًا** باستخدام العنصر النائب `{OrderId}`.
- إنشاء ملف Excel حيث يُسمى كل تبويب `Invoice_12345`، `Invoice_67890`، إلخ.
- التحقق من النتيجة بفتح المصنف.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يُترجم أيضًا مع .NET 5+).
- Aspose.Cells for .NET (أو أي مكتبة تُنفّذ SmartMarker). التثبيت عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

- فئة `Order` أساسية (يمكنك استبدالها بـ DTO الخاص بك).

---

## الخطوة 1: إعداد المشروع والنموذج

أولاً، أنشئ تطبيق console جديد وعَرّف نموذج البيانات الذي يمثل الطلب.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **نصيحة احترافية:** اجعل النموذج خفيفًا للعرض التجريبي؛ يمكنك دائمًا إثراؤه لاحقًا بعناصر سطر، تفاصيل الضرائب، إلخ.

---

## الخطوة 2: إعداد قالب Excel

يعمل SmartMarker ضد مصنف قالب. أنشئ ملفًا باسم `InvoiceTemplate.xlsx` يحتوي على ورقة عمل واحدة تسمى `InvoiceTemplate`. في الخلية **A1** ضع عنصرًا نائبًا لـ SmartMarker مثل:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

يمكنك تنسيق الخلايا بأي طريقة تريدها—عناوين غامقة، تنسيق عملة، إلخ. احفظ الملف في مجلد الجذر للمشروع.

> **لماذا القالب؟** يفصل القالب بين التصميم والكود، مما يسمح للمصممين بتعديل المظهر دون لمس المنطق.

---

## الخطوة 3: تكوين خيارات SmartMarker – تكرار وتسمية أوراق العمل

الآن سنخبر SmartMarker *بتكرار* ورقة القالب لكل طلب وإعطاء كل نسخة اسمًا يتضمن معرف الطلب. هذا هو جوهر **تسمية أوراق العمل ديناميكيًا**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### كيف يعمل

- **`RepeatWorksheet = true`** يُخبر المحرك بإنشاء نسخة من الورقة المصدر لكل عنصر في مجموعة `orders`. هذا يلبي متطلب **كيفية تكرار ورقة العمل**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** هو سلسلة قالب حيث `{OrderId}` عنصر نائب يستبدله SmartMarker بمعرف الطلب الحالي. هذا هو الجواب على **كيفية تسمية أوراق العمل** و**تسمية أوراق العمل ديناميكيًا**.
- يقوم المعالج بدمج حقول كل طلب (`{{OrderId}}`، `{{Customer}}`، إلخ) في الورقة المكررة، مُنتجًا فاتورة مكتملة.

---

## الخطوة 4: تشغيل التطبيق والتحقق من النتيجة

قم بترجمة وتشغيل تطبيق console:

```bash
dotnet run
```

ستظهر رسالة النجاح في وحدة التحكم. افتح `GeneratedInvoices.xlsx` وستجد ثلاث تبويبات:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

كل ورقة تحتوي على بيانات الطلب المستبدلة في العناصر النائبة. التصميم الذي أنشأته في القالب محفوظ، مما يثبت أن **أتمتة إنشاء الفواتير** تعمل من البداية إلى النهاية.

### لقطة شاشة متوقعة (نص بديل لتحسين SEO)

![مثال على أتمتة إنشاء الفواتير يُظهر ثلاث أوراق عمل مسماة ديناميكيًا](/images/invoice-automation.png)

> *نص بديل للصورة يتضمن الكلمة المفتاحية الأساسية لتلبية متطلبات SEO.*

---

## الخطوة 5: الحالات الخاصة والاختلافات الشائعة

### ماذا لو كان OrderId يحتوي على أحرف غير صالحة؟

أسماء أوراق Excel لا يمكن أن تحتوي على `\ / ? * [ ] :`. إذا كان من الممكن أن تشمل معرّفاتك هذه الأحرف، قم بتنظيفها:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

أضف خاصية محسوبة إلى `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### هل تحتاج إلى الاحتفاظ بورقة القالب الأصلية؟

عيّن `smartMarkerOptions.RemoveTemplate = false;` (القيمة الافتراضية هي `true`). هذا يترك `InvoiceTemplate` الأصلي دون تعديل كمرجع.

### هل تريد تجميع الفواتير حسب العميل؟

يمكنك تعشيق **مجموعات التكرار**. أولًا كرّر حسب العميل، ثم حسب الطلبات داخل كل ورقة عميل. يصبح التركيب أكثر تعقيدًا قليلًا، لكن المبدأ يبقى نفسه—استخدم `RepeatWorksheet` ونمط تسمية يعكس التسلسل الهرمي.

---

## مثال كامل يعمل (جميع الشيفرات في مكان واحد)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

انسخ‑الصق هذا في `Program.cs`، وضع `InvoiceTemplate.xlsx` بجانبه، وستكون جاهزًا للانطلاق.

---

## الأسئلة المتكررة

**س: هل يعمل هذا النهج مع مجموعات بيانات كبيرة (آلاف الفواتير)؟**  
ج: نعم. SmartMarker يبث البيانات بكفاءة، لكن راقب استهلاك الذاكرة. إذا وصلت إلى حدود، فكر في المعالجة على دفعات وكتابة كل دفعة إلى مصنف منفصل.

**س: هل يمكنني إضافة شعار إلى كل فاتورة تلقائيًا؟**  
ج: بالتأكيد. ضع صورة الشعار على ورقة القالب. بما أن الورقة تُكرر، سيظهر الشعار في كل فاتورة مُولدة دون الحاجة إلى كود إضافي.

**س: ماذا لو احتجت لحماية أوراق العمل؟**  
ج: بعد المعالجة، قم بالتكرار عبر `wb.Worksheets` واستدعِ `ws.Protect(Password, ProtectionType.All)`.

---

## الخاتمة

لقد قمنا للتو **بأتمتة إنشاء الفواتير** باستخدام ميزة تكرار ورقة العمل في SmartMarker ونمط تسمية ذكي. غطى الدرس **كيفية تسمية أوراق العمل**، وأظهر **كيفية تكرار ورقة العمل** لكل طلب، وعرض **تسمية أوراق العمل ديناميكيًا** التي تحافظ على تنظيم المصنف وسهولة البحث فيه.  

من سحب البيانات، إعداد القالب، تكوين `SmartMarkerOptions`، إلى معالجة الحالات الخاصة، لديك الآن حل كامل وقابل للتنفيذ. الآن جرّب إضافة جداول بنود، تطبيق تنسيق شرطي، أو تصدير نفس البيانات إلى PDF لإنشاء خط أنابيب فواتير آلي بالكامل.

هل أنت مستعد للارتقاء؟ استكشف مواضيع ذات صلة مثل “تصدير Excel بالجملة باستخدام Aspose.Cells”، “تحويل أوراق العمل إلى PDF”، أو “إرسال الفواتير المُولدة بالبريد الإلكتروني مباشرة من C#”. السماء هي الحد—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}