---
category: general
date: 2026-03-27
description: أضف كلمة مرور إلى إكسل واحمِ بياناتك باستخدام خيارات حماية ورقة إكسل،
  مما يسمح بتحديد الخلايا غير المقفلة أثناء حفظ المصنف المحمي بسهولة.
draft: false
keywords:
- add password to excel
- excel sheet protection options
- allow select unlocked cells
- save protected workbook
- enable sheet protection
language: ar
og_description: أضف كلمة مرور إلى Excel واحمِ أوراقك باستخدام الخيارات المدمجة، مما
  يتيح اختيار الخلايا غير المقفلة وحفظ المصنف المحمي في دقائق.
og_title: إضافة كلمة مرور إلى إكسل – دليل شامل لحماية الورقة
tags:
- Aspose.Cells
- C#
- Excel security
title: إضافة كلمة مرور إلى إكسل – دليل شامل لحماية الورقة
url: /ar/net/worksheet-security/add-password-to-excel-complete-sheet-protection-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة كلمة مرور إلى Excel – دليل كامل لحماية الورقة

هل تساءلت يومًا كيف **تضيف كلمة مرور إلى ملفات Excel** دون أن تشعر بالإحباط؟ لست وحدك—الكثير من المطورين يواجهون صعوبة عندما يحتاجون إلى تأمين البيانات الحساسة في جداول البيانات. الخبر السار؟ ببضع أسطر من C# و Aspose.Cells يمكنك تمكين حماية الورقة، اختيار خيارات حماية Excel التي تحتاجها بالضبط، وحتى السماح بخلايا غير مقفلة لتجربة مستخدم أكثر سلاسة.

في هذا الدرس سنستعرض العملية بالكامل: من إنشاء مصنف، كتابة القيم السرية، تطبيق كلمة مرور SHA‑256، تعديل إعدادات الحماية، وأخيرًا **حفظ المصنف المحمي** على القرص. في النهاية ستعرف بالضبط كيف تضيف كلمة مرور إلى Excel، لماذا كل خيار مهم، وكيفية تعديل الكود لمشروعاتك الخاصة.

## المتطلبات المسبقة

- .NET 6 أو أحدث (الكود يعمل مع .NET Core و .NET Framework على حد سواء)
- Aspose.Cells for .NET مثبت عبر NuGet (`dotnet add package Aspose.Cells`)
- فهم أساسي لصياغة C# (لا تحتاج إلى حيل متقدمة)

إذا كان أي من ذلك غير مألوف لك، توقف هنا وقم بتثبيت الحزمة—وبعد أن تكون جاهزًا، يمكننا المتابعة مباشرة.

## الخطوة 1 – إنشاء مصنف جديد (تمكين حماية الورقة)

قبل أن نتمكن من **إضافة كلمة مرور إلى Excel**، نحتاج إلى كائن مصنف للعمل معه. هذه الخطوة أيضًا تهيئ البيئة لتعديلات الحماية اللاحقة.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Create a fresh workbook – think of it as a blank Excel file
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

*لماذا هذا مهم:* إنشاء كائن `Workbook` يمنحك صفحة فارغة. إذا كنت تفتح ملفًا موجودًا، ستستدعي `new Workbook("path.xlsx")` بدلاً من ذلك. مرجع `Worksheet` هو المكان الذي سنكتب فيه البيانات ثم نطبق الحماية لاحقًا.

## الخطوة 2 – كتابة البيانات الحساسة (ما سنحميه)

الآن سنُدخل شيئًا لا يجب على المستخدم تحريره—ربما كلمة مرور، رقم مالي، أو هوية شخصية.

```csharp
        // Write confidential text into cell A1
        worksheet.Cells["A1"].PutValue("Sensitive Information");
```

*نصيحة احترافية:* إذا كنت تحتاج إلى قفل جزء فقط من الورقة، يمكنك وضع علامة على خلايا معينة كغير مقفلة لاحقًا. بشكل افتراضي، تصبح جميع الخلايا مقفلة عندما تُفعَّل الحماية، لذا سنتعامل مع ذلك في الخطوة التالية.

## الخطوة 3 – تمكين حماية الورقة وإضافة كلمة مرور SHA‑256

هذا هو جوهر الدرس: نضيف أخيرًا **كلمة مرور إلى Excel** عبر تشغيل الحماية وتعيين تجزئة قوية.

```csharp
        // Access the protection object for the worksheet
        WorksheetProtection protection = worksheet.Protection;

        // Turn on protection – this is the “enable sheet protection” flag
        protection.IsProtected = true;

        // Set a SHA‑256 hashed password (much stronger than plain text)
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);
```

*لماذا نستخدم SHA‑256؟* كلمات المرور النصية يمكن اختراقها بأدوات القوة الغاشمة، بينما تجزئة SHA‑256 تضيف طبقة تشفيرية تتولى Aspose.Cells معالجتها لك. إذا كنت تفضل التجزئة المتوافقة مع إصدارات Excel القديمة، استبدل `PasswordType.SHA256` بـ `PasswordType.Standard`.

## الخطوة 4 – ضبط خيارات حماية ورقة Excel بدقة

الآن بعد أن أصبحت الورقة مقفلة، نحدد **خيارات حماية ورقة Excel** مثل ما إذا كان بإمكان المستخدمين تحديد الخلايا المقفلة، تحرير الكائنات، أو، وهو أمر حاسم للعديد من سير العمل، **السماح بتحديد الخلايا غير المقفلة**.

```csharp
        // Allow users to click on unlocked cells (useful for data entry)
        protection.AllowSelectUnlockedCells = true;

        // Disallow editing of embedded objects like charts or shapes
        protection.AllowEditObject = false;

        // You can also restrict formatting, inserting rows, etc.
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;
```

*شرح:*  
- `AllowSelectUnlockedCells` يسمح للمستخدمين بالتنقل في الورقة دون ظهور تحذير “الورقة محمية”. هذا مفيد عندما تعرض منطقة تشبه النموذج.  
- `AllowEditObject = false` يمنع تعديل المخططات، الصور، أو أي كائنات مدمجة أخرى، مما يعزز الأمان.  
- هناك أعلام إضافية للتحكم الدقيق—يمكنك تمكين ما يتناسب مع سيناريوك.

## الخطوة 5 – حفظ المصنف المحمي (Save Protected Workbook)

الخطوة الأخيرة هي حفظ الملف. هنا نُجري **حفظ المصنف المحمي** على القرص، وسترى حماية كلمة المرور تعمل عند فتحه في Excel.

```csharp
        // Persist the workbook with all protection settings applied
        workbook.Save("ProtectedSheet.xlsx");

        // Optional: let the console know we’re done
        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

عند النقر المزدوج على `ProtectedSheet.xlsx`، سيطلب Excel كلمة المرور التي حددتها (`MyStrongPwd!`). إذا حاولت تحرير خلية مقفلة، سيتم منعك؛ ومع ذلك، لا يزال بإمكانك تحديد الخلايا غير المقفلة بفضل الإعداد السابق.

### النتيجة المتوقعة

- **الملف:** `ProtectedSheet.xlsx` يظهر في مجلد الإخراج الخاص بالمشروع.  
- **السلوك:** فتح الملف يطلب كلمة المرور. بعد إدخالها، تظل الخلية A1 للقراءة فقط، بينما يمكن تحرير أي خلايا غير مقفلة (إذا أنشأت بعضها).  
- **التحقق:** جرّب تعديل A1—سيرفض Excel ذلك. جرّب النقر على خلية غير مقفلة (إن وجدت)؛ يجب أن تكون قابلة للتحديد دون خطأ.

## الاختلافات الشائعة وحالات الحافة

| السيناريو | ما الذي يجب تغييره | السبب |
|----------|-------------------|-------|
| **خوارزمية كلمة مرور مختلفة** | استخدم `PasswordType.Standard` | للتوافق مع إصدارات Excel القديمة التي لا تدعم SHA‑256. |
| **حماية مصنف موجود** | حمّل عبر `new Workbook("Existing.xlsx")` | يتيح لك إضافة الحماية إلى ملف لديك مسبقًا. |
| **قفل نطاق محدد فقط** | عيّن `worksheet.Cells["B2:C5"].Style.Locked = false;` قبل الحماية | يفتح نطاقًا معينًا بينما يبقى الباقي مقفلاً. |
| **السماح للمستخدمين بتنسيق الخلايا** | `protection.AllowFormatCells = true;` | مفيد للوحة معلومات حيث يمكن للمستخدمين تغيير الألوان دون تعديل البيانات. |
| **الحفظ إلى تدفق (مثلاً استجابة ويب)** | `workbook.Save(stream, SaveFormat.Xlsx);` | مثالي لواجهات ASP.NET APIs التي تُعيد الملف مباشرة إلى المتصفح. |

*احذر من:* نسيان تعيين `IsProtected = true`—كلمة المرور وحدها لا تقفل الورقة. أيضًا، اختبر دائمًا مع عميل Excel حقيقي لأن بعض أعلام الحماية قد تتصرف بشكل مختلف قليلًا بين إصدارات Office.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console. لا توجد أجزاء مفقودة.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write some sensitive information into a cell
        worksheet.Cells["A1"].PutValue("Sensitive Information");

        // Optional: Unlock a range for user input (e.g., B1:C5)
        worksheet.Cells["B1:C5"].Style.Locked = false;

        // Step 3: Enable sheet protection and set a SHA‑256 hashed password
        WorksheetProtection protection = worksheet.Protection;
        protection.IsProtected = true;                     // enable sheet protection
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);

        // Step 4: Restrict actions – allow selecting unlocked cells only
        protection.AllowSelectUnlockedCells = true;
        protection.AllowEditObject = false;               // disallow editing objects
        // Additional options you might need:
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;

        // Step 5: Save the protected workbook to a file
        workbook.Save("ProtectedSheet.xlsx");

        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

شغّل البرنامج، افتح الملف المُنشأ، وسترى الحماية تعمل.

## مرجع بصري

![إضافة كلمة مرور إلى لقطة شاشة حماية ورقة Excel](https://example.com/images/add-password-to-excel.png "إضافة كلمة مرور إلى إكسل")

*النص البديل يتضمن الكلمة المفتاحية الأساسية لتحسين محركات البحث.*

## ملخص وخطوات تالية

لقد أظهرنا لك **كيفية إضافة كلمة مرور إلى Excel** باستخدام Aspose.Cells، وتناولنا **خيارات حماية ورقة Excel** الأساسية، وعرضنا علم **السماح بتحديد الخلايا غير المقفلة**، وحفظنا **مصنفًا محميًا** يحترم تلك الإعدادات. باختصار، التسلسل هو:

1. إنشاء أو تحميل مصنف.  
2. كتابة البيانات التي تريد حمايتها.  
3. تشغيل الحماية، تعيين كلمة مرور قوية، وتعديل الخيارات.  
4. حفظ المصنف.

الآن بعد أن لديك الأساسيات، فكر في الأفكار التالية:

- **مطالبات كلمة مرور برمجية:** إظهار كلمة المرور عبر واجهة آمنة بدلاً من الترميز الصلب.  
- **حماية دفعات:** حلقة عبر أوراق عمل متعددة وتطبيق نفس الإعدادات.  
- **دمج مع ASP.NET Core:** إرجاع الملف المحمي كاستجابة تنزيل.  

لا تتردد في التجربة—ربما ستقفل مجموعة تقارير كاملة أو مجرد ورقة سرية واحدة. في كلتا الحالتين، لديك الآن الأدوات اللازمة لحماية بيانات Excel بالطريقة الصحيحة.

---

*برمجة سعيدة! إذا ساعدك هذا الدليل في إضافة كلمة مرور إلى Excel، أخبرنا في التعليقات أو شارك تعديلاتك. كلما تعلمنا معًا، كلما أصبحت جداولنا أكثر أمانًا.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}