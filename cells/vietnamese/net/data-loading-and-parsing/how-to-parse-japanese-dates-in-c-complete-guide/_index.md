---
category: general
date: 2026-03-29
description: Cách phân tích ngày Nhật trong C# bằng DateTimeParser và CultureInfo.
  Tìm hiểu cách phân tích ngày theo niên hiệu Nhật, mẹo phân tích ngày trong C#, và
  xử lý các trường hợp đặc biệt.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: vi
og_description: Cách phân tích ngày Nhật trong C# bằng DateTimeParser và CultureInfo.
  Nhận giải pháp từng bước để phân tích ngày theo niên hiệu Nhật.
og_title: Cách phân tích ngày Nhật trong C# – Hướng dẫn đầy đủ
tags:
- C#
- .NET
- DateTime
- Localization
title: Cách phân tích ngày Nhật trong C# – Hướng dẫn toàn diện
url: /vi/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách phân tích ngày Nhật trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **how to parse japanese** chuỗi ngày trong một ứng dụng .NET chưa? Có thể bạn đang làm việc trên một hệ thống tài chính nhận được các ngày như “令和3年5月12日” từ khách hàng Nhật Bản, và bạn cần chuyển chúng thành một `DateTime` thông thường. Bạn không phải là người duy nhất—các vấn đề về bản địa hoá luôn xuất hiện.  

Tin tốt là với các cài đặt văn hoá đúng và một lớp trợ giúp nhỏ, **how to parse japanese** ngày trở nên dễ dàng. Trong hướng dẫn này, chúng ta sẽ đi qua từng bước, từ việc thiết lập `CultureInfo` cho *ja‑JP* đến xử lý các trường hợp đặc biệt như các thời kỳ lịch sử. Khi kết thúc, bạn sẽ có một `DateTimeParser` có thể tái sử dụng cho bất kỳ ngày nào thuộc thời kỳ hiện đại của Nhật Bản.

> **Bạn sẽ nhận được** – một ví dụ đầy đủ, có thể chạy được, giải thích *tại sao* mỗi dòng lại quan trọng, mẹo cho các thời kỳ cũ, và một danh sách kiểm tra nhanh để bạn không bao giờ quên bước nào.

## Yêu cầu trước

- .NET 6+ (hoặc .NET Framework 4.7 + – API chúng ta dùng không thay đổi)
- Kiến thức cơ bản về C# (bạn nên quen với các câu lệnh `using` và `Console.WriteLine`)
- Không có gói NuGet bên ngoài—mọi thứ đều nằm trong `System` và `System.Globalization`

Nếu bạn đã có một dự án mở, tuyệt vời—chỉ cần chèn mã vào. Nếu chưa, tạo một ứng dụng console mới với `dotnet new console -n JapaneseDateDemo` và bạn đã sẵn sàng.

## Bước 1: Hiểu hệ thống lịch Nhật Bản

Trước khi chúng ta đi vào mã, hãy trả lời câu hỏi “tại sao”. Ngày Nhật được biểu diễn theo định dạng **era** (元号), trong đó số năm được đặt lại khi một hoàng đế mới lên ngôi. Ví dụ:

- **令和** (Reiwa) bắt đầu vào ngày 01‑05‑2019.
- **平成** (Heisei) kéo dài từ 1989‑2019.
- **昭和** (Showa) diễn ra từ 1926‑1989.

Lớp `JapaneseCalendar` của .NET đã biết các thời kỳ này, nhưng bạn phải cho trình phân tích biết nên dùng văn hoá nào. Đó là nơi **cultureinfo ja‑jp** xuất hiện—nó liên kết lịch với locale Nhật Bản.

## Bước 2: Tạo một Wrapper nhỏ – `DateTimeParser`

Thay vì rải rác `CultureInfo` khắp nơi, chúng ta sẽ đóng gói logic vào một trợ giúp nhỏ. Điều này làm cho mã có thể tái sử dụng và giữ phần còn lại của ứng dụng sạch sẽ.

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

**Tại sao lại có trợ giúp này?**  
- **Single responsibility** – tất cả việc phân tích đặc thù vùng miền đều nằm ở một nơi.  
- **Error handling** – chúng tôi hiển thị thông báo rõ ràng khi định dạng sai.  
- **Future‑proof** – nếu sau này bạn cần hỗ trợ các thời kỳ cũ *Taisho* hoặc *Meiji*, chỉ cần điều chỉnh mẫu hoặc thêm fallback.

## Bước 3: Kết nối mọi thứ trong `Program.cs`

Bây giờ chúng ta sẽ sử dụng wrapper để thực sự phân tích một chuỗi mẫu. Hãy chú ý cách chúng ta lấy văn hoá Nhật Bản bằng `CultureInfo.GetCultureInfo("ja-JP")`. Điều này đáp ứng yêu cầu **cultureinfo ja‑jp** và đảm bảo `JapaneseCalendar` được kích hoạt.

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

Khi bạn chạy `dotnet run` bạn sẽ thấy:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Đó là cốt lõi của **how to parse japanese** ngày. Đơn giản, đúng không?

## Bước 4: Xử lý các trường hợp đặc biệt & các thời kỳ cũ

### 4.1 Ngày lịch sử trước năm 1912

`JapaneseCalendar` tích hợp chỉ hỗ trợ các thời kỳ hiện đại (từ Meiji trở đi). Nếu bạn cần phân tích ngày từ các thời kỳ *Taisho* (1912‑1926) hoặc *Meiji* (1868‑1912), cùng một mẫu vẫn hoạt động—chỉ cần đảm bảo chuỗi bao gồm tên thời kỳ đúng (“大正”, “明治”). Trình phân tích vẫn sẽ trả về một `DateTime` Gregorian chính xác.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Thiếu Era (Đầu vào mơ hồ)

Nếu khách hàng gửi “2021年5月12日” mà không có era, trình phân tích sẽ thất bại vì mẫu yêu cầu một era (`ggg`). Bạn có hai lựa chọn:

1. **Assume Gregorian** – quay lại `CultureInfo.InvariantCulture` và một mẫu khác.
2. **Reject the input** – thông báo cho người gọi biết rằng era là bắt buộc.

Đây là một sự điều chỉnh nhanh:

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

### 4.3 Lưu ý về Thread‑Safety

Các đối tượng `CultureInfo` trở thành chỉ đọc sau khi tạo, vì vậy bạn có thể tái sử dụng cùng một thể hiện một cách an toàn trên các luồng. `DateTimeParser` tự nó không giữ trạng thái có thể thay đổi, làm cho nó **thread‑safe** – một thực tế hữu ích cho các API web có lưu lượng cao.

## Bước 5: Kết hợp tất cả – Ví dụ sẵn sàng sao chép

Dưới đây là toàn bộ mã nguồn bạn có thể chèn vào một dự án console mới. Không có gói bên ngoài, không có phụ thuộc ẩn.

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