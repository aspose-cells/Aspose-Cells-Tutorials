---
category: general
date: 2026-06-27
description: Học cách phân tích ngày theo niên hiệu Nhật trong C# và sau đó định dạng
  datetime yyyy‑mm‑dd cho đầu ra ISO. Mã từng bước, các trường hợp đặc biệt và mẹo.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: vi
og_description: Phân tích ngày theo thời đại Nhật Bản trong C# và định dạng datetime
  yyyy-mm-dd một cách dễ dàng. Ví dụ đầy đủ kèm giải thích và các lưu ý.
og_title: Phân tích ngày theo niên hiệu Nhật trong C# – Hướng dẫn lập trình chi tiết
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Phân tích ngày theo niên hiệu Nhật trong C# – Hướng dẫn đầy đủ
url: /vi/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Phân tích ngày theo niên hiệu Nhật trong C# – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **phân tích ngày theo niên hiệu Nhật** trong một ứng dụng .NET và thắc mắc tại sao kết quả lại sai lệch? Bạn không phải là người duy nhất. Trong nhiều hệ thống kế thừa, ngày được ghi dưới dạng “R3‑04‑01”, và bạn cần chuyển chúng thành một chuỗi **format datetime yyyy-mm-dd** sạch sẽ để gửi tới API hoặc cơ sở dữ liệu.  

Trong tutorial này chúng ta sẽ đi qua các bước chính xác để thực hiện, giải thích lý do mỗi phần quan trọng, và chỉ cho bạn cách xử lý các trường hợp biên khó khăn mà thường làm khó các nhà phát triển.

> **Lưu ý:** Tất cả mã nguồn đã sẵn sàng để sao chép‑dán vào một console app nhắm tới .NET 6 hoặc phiên bản mới hơn.

## Những gì bạn cần

- .NET 6 SDK (hoặc bất kỳ phiên bản gần đây nào)
- Kiến thức cơ bản về C# và namespace `System.Globalization`
- Một IDE hoặc trình soạn thảo – Visual Studio, VS Code, Rider, bất kỳ công cụ nào bạn thích

Không cần bất kỳ gói NuGet bên ngoài nào; mọi thứ đều có trong BCL.

## Bước 1: Thiết lập văn hoá Nhật Bản với lịch hoàng đế

Đầu tiên, chúng ta cần một `CultureInfo` biết về lịch hoàng đế Nhật Bản. Mặc định, `ja-JP` sử dụng lịch Gregorian, vì vậy chúng ta thay thế `DateTimeFormat.Calendar` của nó bằng một thể hiện `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Tại sao điều này quan trọng:** `JapaneseCalendar` chuyển đổi các ký hiệu niên hiệu (như “R” cho Reiwa) thành năm Gregorian đúng. Nếu không có nó, `DateTime.Parse` sẽ ném ra một `FormatException`.

## Bước 2: Phân tích chuỗi ngày dựa trên niên hiệu

Bây giờ chúng ta có thể truyền một chuỗi như `"R3-04-01"` vào `DateTime.Parse`. Văn hoá mà chúng ta vừa cấu hình sẽ cho parser biết cách diễn giải phần “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Nếu bạn muốn một cách tiếp cận an toàn hơn, tránh ngoại lệ khi đầu vào không hợp lệ, hãy thay `Parse` bằng `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Mẹo chuyên nghiệp:** Chuỗi định dạng tùy chỉnh `"ggy-MM-dd"` cho parser biết chính xác những gì cần mong đợi. “gg” là ký hiệu niên hiệu, “y” là năm trong niên hiệu đó.

## Bước 3: Chuyển kết quả sang ISO 8601 (`format datetime yyyy-mm-dd`)

Cuối cùng, chúng ta xuất `DateTime` dưới dạng chuẩn ISO. Bộ định dạng `"yyyy-MM-dd"` thực hiện đúng việc này.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Chạy chương trình sẽ in ra:

```
2021-04-01
```

Đó là **format datetime yyyy-mm-dd** mà bạn cần, sẵn sàng cho payload JSON, câu lệnh INSERT SQL, hoặc bất kỳ hệ thống downstream nào.

![parse japanese era date example](placeholder.png){alt="ví dụ phân tích ngày theo niên hiệu Nhật"}

## Xử lý các niên hiệu và trường hợp biên khác

### Nhiều niên hiệu

Nhật Bản đã trải qua nhiều niên hiệu (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` tự động ánh xạ chúng, vì vậy `"H30-12-31"` (Heisei 30) sẽ trở thành `2018-12-31`. Chỉ cần giữ nguyên logic phân tích; lịch sẽ thực hiện phần việc nặng.

### Đầu vào không hợp lệ

Nếu một chuỗi không khớp với mẫu mong đợi, `Parse` sẽ ném ngoại lệ. Hãy dùng `TryParseExact` như đã chỉ ra ở trên, hoặc kiểm tra trước bằng biểu thức chính quy:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Múi giờ

Đối tượng `DateTime` mặc định là “kind‑agnostic”. Nếu bạn cần một dấu thời gian UTC, gọi:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Hoặc dùng `DateTimeOffset` để có nhận thức đầy đủ về múi giờ.

## Ví dụ hoàn chỉnh

Dưới đây là toàn bộ đoạn mã bạn có thể đưa vào một dự án console mới:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Kết quả console mong đợi**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Tóm tắt

Chúng ta đã tìm hiểu cách **phân tích ngày theo niên hiệu Nhật** bằng cách:

1. Tạo một `CultureInfo` cho `ja-JP` và thay thế `JapaneseCalendar`.
2. Sử dụng `DateTime.Parse` hoặc `TryParseExact` mạnh mẽ hơn với định dạng tùy chỉnh.
3. Định dạng `DateTime` kết quả bằng `"yyyy-MM-dd"` để đạt được **format datetime yyyy-mm-dd** mong muốn.

Đó là tất cả những gì bạn cần để kết nối dữ liệu niên hiệu Nhật cũ vào các hệ thống hiện đại tuân thủ ISO.

## Tiếp theo là gì?

- **Xử lý hàng loạt:** Lặp qua một file CSV chứa các ngày theo niên hiệu và ghi chuỗi ISO vào cơ sở dữ liệu.
- **Bản địa hoá:** Chuyển lại ngày ISO thành định dạng niên hiệu để hiển thị UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Lịch tùy chỉnh:** Khám phá `TaiwanCalendar` hoặc `HijriCalendar` cho các nhu cầu khu vực khác.

Hãy tự do thử nghiệm—thay đổi chuỗi niên hiệu, kiểm tra các trường hợp biên, hoặc tích hợp logic này vào các endpoint ASP.NET Core. Nếu gặp khó khăn, hãy để lại bình luận bên dưới; chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã mẫu đầy đủ và các giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [How to Implement and Format Excel Comments Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}