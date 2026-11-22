---
category: general
date: 2026-11-22
description: إنشاء ملف xlsb في C# وتعلم كيفية إضافة خصائص إلى ورقة عمل Excel؛ حفظ
  المصنف كملف xlsb باستخدام Aspose.Cells لتخزين ثنائي سريع.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create xlsb file
- how to add properties
- excel worksheet custom properties
- custom worksheet properties
- save workbook as xlsb
language: ar
lastmod: 2026-11-22
og_description: إنشاء ملف xlsb في C# باستخدام Aspose.Cells. يوضح هذا الدليل كيفية
  إضافة خصائص إلى ورقة عمل Excel وحفظ المصنف كملف xlsb لتخزين ثنائي سريع.
og_image_alt: Screenshot of an Excel workbook saved as .xlsb with custom worksheet
  properties displayed in the file explorer
og_title: إنشاء ملف xlsb بخصائص مخصصة – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  headline: How to create xlsb file with custom worksheet properties in C#
  type: TechArticle
- description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  name: How to create xlsb file with custom worksheet properties in C#
  steps:
  - name: Open your preferred IDE (Visual Studio, Rider, or VS Code).
    text: Open your preferred IDE (Visual Studio, Rider, or VS Code).
  - name: 'Create a new console project:'
    text: 'Create a new console project:'
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: Open the file.
    text: Open the file.
  - name: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
    text: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
  - name: You will see the `Department` and `Reviewed` entries.
    text: You will see the `Department` and `Reviewed` entries.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إنشاء ملف xlsb بخصائص ورقة عمل مخصصة في C#
url: /ar/net/saving-and-exporting-excel-files-with-options/how-to-create-xlsb-file-with-custom-worksheet-properties-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء ملف xlsb بخصائص ورقة عمل مخصصة في C#

إذا كنت بحاجة إلى **إنشاء ملف xlsb** برمجيًا، فإن هذا الدليل يوفر حلًا كاملاً. سترى بالضبط **كيفية إضافة الخصائص** إلى ورقة عمل Excel ثم **حفظ المصنف كـ xlsb** باستخدام Aspose.Cells. تعمل الخطوات مع .NET 6 وما بعده، ولا تتطلب تثبيت Excel يدوي.

يغطي الدليل إعداد المشروع، إنشاء المصنف، إضافة خصائص ورقة عمل مخصصة، حفظ الملف بتنسيق Excel الثنائي، والتحقق من النتيجة. في النهاية يمكنك إنشاء مصنف *.xlsb* مضغوط يحمل بيانات وصفية مثل القسم أو حالة المراجعة.

## إنشاء ملف xlsb – نظرة عامة

إنشاء ملف *.xlsb* يختلف عن تنسيق *.xlsx* الكلاسيكي فقط في خطوة الحفظ النهائية. هيكل المصنف، أوراق العمل، وبيانات الخلايا هي نفسها؛ يقلل التنسيق الثنائي من حجم الملف ويسرّع فتحه في Excel. يوضح مثال الشيفرة أدناه دورة الحياة الكاملة، من مصنف فارغ إلى ملف *.xlsb* محفوظ يحتوي على **excel worksheet custom properties**.

## إعداد Aspose.Cells في مشروع C# الخاص بك

1. افتح بيئة التطوير المتكاملة المفضلة لديك (Visual Studio، Rider، أو VS Code).  
2. أنشئ مشروعًا جديدًا من نوع console:

   ```bash
   dotnet new console -n XlsbDemo
   cd XlsbDemo
   ```

3. أضف حزمة Aspose.Cells عبر NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

   توفر الحزمة الفئات `Workbook` و `Worksheet` و `CustomPropertyCollection` اللازمة لهذا الدليل.

## كيفية إضافة الخصائص إلى ورقة عمل Excel

تسمح خصائص ورقة العمل المخصصة لك بتخزين بيانات وصفية عشوائية إلى جانب الورقة. وهي مفيدة للمعالجة اللاحقة، سجلات التدقيق، أو تلميحات واجهة المستخدم. الشيفرة التالية تنشئ مصنفًا، تصل إلى أول ورقة عمل، وتضيف خاصيتين: سلسلة `Department` ومنطقية `Reviewed`.

```csharp
using Aspose.Cells;

class XlsbCustomPropsDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();                 // workbook is the container for all sheets
        Worksheet worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Add custom properties to the worksheet
        // These are *excel worksheet custom properties* that travel with the sheet.
        worksheet.CustomProperties.Add("Department", "Finance");
        worksheet.CustomProperties.Add("Reviewed", true);

        // Step 3: Save the workbook in binary Excel format (.xlsb)
        // The file will contain the custom properties defined above.
        workbook.Save("CustomProps.xlsb");
    }
}
```

**لماذا هذه الأسطر مهمة**

- `Workbook()` ينشئ تمثيلًا في الذاكرة لملف Excel.  
- `worksheet.CustomProperties.Add` يخزن أزواج المفتاح‑القيمة التي يمكن لـ Excel قراءتها عبر حوار *Custom Properties*.  
- `workbook.Save` مع امتداد `.xlsb` يطلق مسار **save workbook as xlsb**، ويستخدم تلقائيًا التنسيق الثنائي.

يمكنك إضافة أي عدد من الخصائص؛ المجموعة تقبل سلاسل، أرقام، تواريخ، ومنطقيات. إذا احتجت لقراءتها لاحقًا، استخدم `worksheet.CustomProperties["Department"]`.

## حفظ المصنف كـ xlsb

طريقة `Save` تحدد تنسيق الملف بناءً على الامتداد. تمرير `"CustomProps.xlsb"` يوجه Aspose.Cells لكتابة المصنف الثنائي. هذه الخطوة هي المكان الوحيد الذي يظهر فيه **save workbook as xlsb** في الشيفرة، لكن الأثر واضح في حجم الملف وسرعة الفتح.

إذا كنت تفضل التحكم في التنسيق صراحةً، استخدم كائن `SaveOptions`:

```csharp
// Alternative: specify the save format with SaveOptions
var options = new XlsbSaveOptions(SaveFormat.Xlsb);
workbook.Save("CustomPropsExplicit.xlsb", options);
```

كلا النهجين ينتجان ملف *.xlsb* صالح يحتوي على **custom worksheet properties** التي حددتها.

## التحقق من خصائص ورقة العمل المخصصة

بعد تشغيل البرنامج، افتح الملف `CustomProps.xlsb` الذي تم إنشاؤه في Excel:

1. افتح الملف.  
2. انقر بزر الماوس الأيمن على تبويب الورقة واختر **View Code** → **Properties** (أو استخدم حوار *File → Info → Properties*).  
3. سترى مدخلات `Department` و `Reviewed`.

وجود هذه المدخلات يؤكد أن **excel worksheet custom properties** تم تضمينها بشكل صحيح.

### النتيجة المتوقعة

تشغيل البرنامج ينشئ ملفين في مجلد المشروع:

- `CustomProps.xlsb` – المصنف الثنائي مع الخصائص المخصصة.  
- `CustomPropsExplicit.xlsb` – محتوى مماثل، محفوظ عبر `XlsbSaveOptions`.

كلا الملفين يفتحان في Excel دون تحذيرات ويظهران البيانات الوصفية المخصصة عند الفحص.

## الأخطاء الشائعة ونصائح الممارسات الأفضل

- **لا تخلط بين امتدادات الملفات.** استخدام `.xlsx` مع تمرير `XlsbSaveOptions` ينتج ملفًا فاسدًا. احرص دائمًا على مطابقة الامتداد مع التنسيق المختار.  
- **أسماء الخصائص حساسة لحالة الأحرف** في المجموعة. احصل عليها باستخدام المفتاح الدقيق الذي استخدمته عند الإضافة.  
- **المصنفات الكبيرة تستفيد من التنسيق الثنائي** لأن حجم الملف يمكن أن ينخفض حتى 50 % مقارنةً بـ `.xlsx`. هذا صحيح بشكل خاص عندما يحتوي المصنف على العديد من الصيغ أو الأنماط.  
- **سلامة الخيوط:** كائنات `Workbook` غير آمنة للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة لكل خيط إذا كنت تولد ملفات متعددة بشكل متزامن.  

## الخطوات التالية

الآن بعد أن يمكنك **إنشاء ملف xlsb** مع **custom worksheet properties**، قد ترغب في استكشاف:

- إضافة **excel worksheet custom properties** إلى عدة أوراق في نفس المصنف.  
- استخدام **how to add properties** للصفوف أو الخلايا عبر مجموعة `Cell.CustomProperties`.  
- تصدير المصنف إلى PDF أو HTML مع الحفاظ على البيانات الوصفية.  
- أتمتة العملية في واجهة ويب API تُعيد تدفق *.xlsb* مباشرةً إلى العميل.

تتيح لك هذه الإضافات بناء خطوط أنابيب أتمتة Excel قوية تستفيد من سرعة التنسيق الثنائي ومرونة البيانات الوصفية المخصصة.

*لقد تعلمت كيفية إنشاء مصنف *.xlsb* في C#، إضافة خصائص ورقة عمل مخصصة، وحفظ الملف باستخدام Aspose.Cells. طبّق الأنماط أعلاه على تقاريرك المدفوعة بالبيانات، لوحات التحكم، أو خدمات تبادل البيانات.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [How to Save XLSB and Add Custom Document Properties in C#](/cells/english/net/document-properties/how-to-save-xlsb-and-add-custom-document-properties-in-c/)
- [How to Save XLSB with Custom Properties in C# – Step‑by‑Step Guide](/cells/english/net/document-properties/how-to-save-xlsb-with-custom-properties-in-c-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}