---
category: general
date: 2026-03-29
description: كيفية تحليل التواريخ اليابانية في C# باستخدام DateTimeParser وCultureInfo.
  تعلم تحليل تواريخ العصور اليابانية، نصائح تحليل التواريخ في C#، وتعامل مع الحالات
  الخاصة.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: ar
og_description: كيفية تحليل التواريخ اليابانية في C# باستخدام DateTimeParser وCultureInfo.
  احصل على حل خطوة بخطوة لتحليل تواريخ العصور اليابانية.
og_title: كيفية تحليل التواريخ اليابانية في C# – دليل شامل
tags:
- C#
- .NET
- DateTime
- Localization
title: كيفية تحليل التواريخ اليابانية في C# – دليل كامل
url: /ar/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحليل تواريخ يابانية في C# – دليل كامل

هل تساءلت يومًا **how to parse japanese** عن سلاسل تواريخ يابانية داخل تطبيق .NET؟ ربما تعمل على نظام مالي يتلقى تواريخ مثل “令和3年5月12日” من عميل ياباني، وتحتاج إلى تحويلها إلى `DateTime` عادي. لست وحدك—مشكلات التوطين تظهر باستمرار.  

الخبر السار هو أنه باستخدام إعدادات الثقافة الصحيحة وفئة مساعدة صغيرة، تصبح **how to parse japanese** عملية سهلة. في هذا الدرس سنستعرض كل خطوة، من إعداد `CultureInfo` للغة *ja‑JP* إلى معالجة الحالات الخاصة مثل العصور التاريخية. في النهاية ستحصل على `DateTimeParser` قابل لإعادة الاستخدام يعمل مع أي تاريخ ياباني عصري.

> **What you’ll get** – مثال كامل قابل للتنفيذ، شروحات عن *why* كل سطر مهم، نصائح للعصور القديمة، وقائمة تحقق سريعة حتى لا تنسى أي خطوة.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7 + – الـ API الذي نستخدمه لم يتغير)
- معرفة أساسية بـ C# (يجب أن تكون مرتاحًا مع عبارات `using` و `Console.WriteLine`)
- لا حزم NuGet خارجية—كل شيء موجود في `System` و `System.Globalization`

إذا كان لديك مشروع مفتوح بالفعل، رائع—فقط الصق الكود. إذا لم يكن كذلك، أنشئ تطبيق وحدة تحكم جديد باستخدام `dotnet new console -n JapaneseDateDemo` وستكون جاهزًا.

## الخطوة 1: فهم نظام التقويم الياباني

قبل أن نغوص في الكود، دعنا نجيب على سؤال “why”. تُعبّر التواريخ اليابانية بصيغة **era** (元号)، حيث يُعاد تعيين رقم السنة عندما يتولى إمبراطور جديد العرش. على سبيل المثال:

- **令和** (Reiwa) بدأ في 2019‑05‑01.
- **平成** (Heisei) امتد من 1989‑2019.
- **昭和** (Showa) استمر من 1926‑1989.

فئة `JapaneseCalendar` في .NET تعرف بالفعل هذه العصور، لكن عليك إخبار المحلل أي ثقافة يجب استخدامها. هنا يأتي دور **cultureinfo ja‑jp**—فهو يربط التقويم بالمنطقة اليابانية.

## الخطوة 2: إنشاء غلاف صغير – `DateTimeParser`

بدلاً من توزيع `CultureInfo` في كل مكان، سنغلف المنطق في مساعدة صغيرة. هذا يجعل الكود قابلًا لإعادة الاستخدام ويحافظ على نظافة باقي تطبيقك.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Why this helper?**  
- **Single responsibility** – كل التحليل المتعلق بالمنطقة يتركز في مكان واحد.  
- **Error handling** – نعرض رسائل واضحة عندما يكون التنسيق خاطئًا.  
- **Future‑proof** – إذا احتجت لاحقًا لدعم العصور القديمة *Taisho* أو *Meiji*، فقط عدل النمط أو أضف حلًا احتياطيًا.

## الخطوة 3: ربط كل شيء في `Program.cs`

الآن سنستخدم الغلاف لتحليل سلسلة مثال فعليًا. لاحظ كيف نحصل على الثقافة اليابانية باستخدام `CultureInfo.GetCultureInfo("ja-JP")`. هذا يفي بمتطلب **cultureinfo ja‑jp** ويضمن تفعيل `JapaneseCalendar`.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

عند تشغيل `dotnet run` سترى:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

هذا هو جوهر **how to parse japanese** التواريخ. بسيط، أليس كذلك؟

## الخطوة 4: معالجة الحالات الخاصة والعصور القديمة

### 4.1 تواريخ تاريخية قبل 1912

فئة `JapaneseCalendar` المدمجة تدعم فقط العصور الحديثة (من ميجي فصاعدًا). إذا احتجت إلى تحليل تواريخ من فترات *Taisho* (1912‑1926) أو *Meiji* (1868‑1912)، فإن النمط نفسه يعمل—فقط تأكد أن السلسلة تتضمن اسم العصر الصحيح (“大正”, “明治”). سيظل المحلل يُعيد `DateTime` غريغوري صحيح.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 فقدان العصر (إدخال غامض)

إذا أرسل عميل السلسلة “2021年5月12日” بدون عصر، سيفشل المحلل لأن النمط يتوقع وجود عصر (`ggg`). لديك خياران:

1. **Assume Gregorian** – الرجوع إلى `CultureInfo.InvariantCulture` واستخدام نمط مختلف.  
2. **Reject the input** – إبلاغ المستدعي بأن العصر مطلوب.

إليك تعديل سريع:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 ملاحظة حول أمان الخيوط

كائنات `CultureInfo` تصبح للقراءة فقط بعد الإنشاء، لذا يمكنك إعادة استخدام نفس المثيل بأمان عبر الخيوط. `DateTimeParser` نفسه لا يحتفظ بحالة قابلة للتغيير، مما يجعله **thread‑safe** – حقيقة مفيدة لواجهات برمجة تطبيقات الويب ذات الإنتاجية العالية.

## الخطوة 5: جمع كل شيء معًا – مثال جاهز للنسخ

فيما يلي الشيفرة الكاملة التي يمكنك لصقها في مشروع وحدة تحكم جديد. لا حزم خارجية، ولا تبعيات مخفية.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}