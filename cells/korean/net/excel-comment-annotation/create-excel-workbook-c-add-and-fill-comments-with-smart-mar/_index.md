---
category: general
date: 2026-03-21
description: C#로 Excel 워크북을 만들고, Excel에 주석을 추가하는 방법과 Smart Markers를 사용해 주석을 자동으로 채우는
  방법을 배웁니다. 개발자를 위한 단계별 가이드.
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: ko
og_description: C#로 Excel 워크북을 만들고, Excel에 주석을 빠르게 추가한 뒤 Smart Markers를 사용해 주석을 채웁니다.
  코드와 함께하는 완전한 튜토리얼.
og_title: Excel 워크북 만들기 C# – 주석 추가 및 채우기
tags:
- C#
- Excel automation
- Aspose.Cells
title: C#로 Excel 워크북 만들기 – 스마트 마커로 주석 추가 및 채우기
url: /ko/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 C# 만들기 – 스마트 마커로 주석 추가 및 채우기

Ever needed to **create Excel workbook C#** and wondered how to embed a comment that updates itself automatically? You're not the only one. In many reporting scenarios you want a cell comment that says *“Created by Alice on 2024‑07‑15”* without hard‑coding the name or date each time.  

많은 보고 시나리오에서 셀 주석에 *“Created by Alice on 2024‑07‑15”*와 같이 이름이나 날짜를 매번 하드코딩하지 않고 표시하고 싶습니다.  

In this tutorial we’ll show you exactly **how to add comment to Excel**, then **how to fill comment** using Aspose.Cells’ Smart Markers. By the end you’ll have a ready‑to‑run program that creates a workbook, injects a dynamic comment, and saves the file—all in a few tidy steps.

> **What you’ll get:** a complete, compilable C# console app, an explanation of every line, tips for common pitfalls, and ideas for extending the solution.

> **얻을 수 있는 것:** 완전하고 컴파일 가능한 C# 콘솔 앱, 각 라인에 대한 설명, 일반적인 함정에 대한 팁, 그리고 솔루션을 확장하기 위한 아이디어.

## Prerequisites

## 사전 요구 사항

- .NET 6.0 SDK or later (the code works with .NET Core and .NET Framework as well)  
- .NET 6.0 SDK 또는 그 이후 버전 (코드는 .NET Core 및 .NET Framework에서도 작동합니다)  
- Visual Studio 2022 or any IDE you prefer  
- Visual Studio 2022 또는 선호하는 IDE  
- **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`) – this library powers the `Workbook`, `Worksheet`, and `SmartMarkerProcessor` classes used below.  
- **Aspose.Cells for .NET** NuGet 패키지 (`Install-Package Aspose.Cells`) – 이 라이브러리는 아래에서 사용되는 `Workbook`, `Worksheet`, `SmartMarkerProcessor` 클래스를 지원합니다.  
- Basic familiarity with C# syntax – if you’ve written a `Console.WriteLine`, you’re good to go.  
- C# 구문에 대한 기본적인 이해 – `Console.WriteLine`을 작성해 본 적이 있다면 바로 시작할 수 있습니다.

Now that the groundwork is out of the way, let’s dive in.

이제 기본 준비가 끝났으니, 본격적으로 시작해 봅시다.

![Excel 워크북 C# 예제 스크린샷](excel-workbook.png "Excel 워크북 C# 예제")

## Step 1: Initialise a New Workbook – Create Excel Workbook C# Basics

## 단계 1: 새 워크북 초기화 – Excel 워크북 C# 기본

First we need a clean workbook object. Think of `Workbook` as the blank canvas; without it you can’t place any cells, rows, or comments.

먼저 깨끗한 워크북 객체가 필요합니다. `Workbook`을 빈 캔버스로 생각하면 됩니다; 이것이 없으면 셀, 행 또는 주석을 배치할 수 없습니다.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**Why this matters:** `Workbook` automatically creates a default worksheet, so you don’t have to call `Add` unless you need extra tabs. Accessing `Worksheets[0]` is the fastest way to start populating data.

**왜 중요한가:** `Workbook`은 자동으로 기본 워크시트를 생성하므로 추가 탭이 필요하지 않은 한 `Add`를 호출할 필요가 없습니다. `Worksheets[0]`에 접근하는 것이 데이터를 채우기 시작하는 가장 빠른 방법입니다.

## Step 2: Insert a Smart Marker Comment – How to Add Comment with Tokens

## 단계 2: 스마트 마커 주석 삽입 – 토큰으로 주석 추가하는 방법

Next we place a comment in cell **B2** that contains Smart Marker tokens (`«UserName»` and `«CreatedDate»`). These tokens will be replaced later with actual values.

다음으로 **B2** 셀에 스마트 마커 토큰(`«UserName»` 및 `«CreatedDate»`)이 포함된 주석을 삽입합니다. 이 토큰들은 나중에 실제 값으로 교체됩니다.

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**Explanation:**  
- `CreateComment()` creates the comment object if none exists; otherwise it returns the existing one.  
- `CreateComment()`는 주석 객체가 없을 경우 생성하고, 이미 존재하면 기존 객체를 반환합니다.  
- The `Note` property holds the visible text. By wrapping the placeholders in `« »` we tell Aspose.Cells that they are **Smart Markers** – placeholders that can be swapped out in one shot.  
- `Note` 속성은 표시되는 텍스트를 보관합니다. 플레이스홀더를 `« »`로 감싸면 Aspose.Cells에 이것이 **스마트 마커**임을 알리는 것으로, 한 번에 교체 가능한 플레이스홀더가 됩니다.

> **Pro tip:** If you need a multi‑line comment, use `\n` inside the string, e.g., `"Line1\nLine2"`.

> **프로 팁:** 여러 줄 주석이 필요하면 문자열 안에 `\n`을 사용하세요. 예: `"Line1\nLine2"`.

## Step 3: Prepare the Data Object – How to Fill Comment Dynamically

## 단계 3: 데이터 객체 준비 – 주석을 동적으로 채우는 방법

Smart Markers need a data source. In C# the easiest way is an anonymous type that matches the placeholder names.

스마트 마커에는 데이터 소스가 필요합니다. C#에서 가장 쉬운 방법은 플레이스홀더 이름과 일치하는 익명 형식을 사용하는 것입니다.

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**Why an anonymous type?**  
It’s lightweight, requires no extra class file, and matches the property names (`UserName`, `CreatedDate`) exactly to the token names. If you prefer a strongly‑typed model, just create a class with the same properties.

**왜 익명 형식인가?**  
가볍고 별도의 클래스 파일이 필요 없으며, 속성 이름(`UserName`, `CreatedDate`)이 토큰 이름과 정확히 일치합니다. 강력히 타입된 모델을 선호한다면 동일한 속성을 가진 클래스를 만들면 됩니다.

## Step 4: Process Smart Markers – How to Fill Comment Using the Data Object

## 단계 4: 스마트 마커 처리 – 데이터 객체를 사용해 주석 채우기

Now the magic happens. The `SmartMarkerProcessor` scans the workbook for any `«…»` tokens and swaps them with values from `markerData`.

이제 마법이 일어납니다. `SmartMarkerProcessor`는 워크북에서 모든 `«…»` 토큰을 스캔하고 `markerData`의 값으로 교체합니다.

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**What’s under the hood?**  
`SmartMarkerProcessor` walks through each cell, comment, header, etc., looking for the `«Token»` pattern. When it finds one, it uses reflection to read the matching property from `markerData` and writes the value back. No manual loops required.

**내부 동작:**  
`SmartMarkerProcessor`는 각 셀, 주석, 헤더 등을 순회하며 `«Token»` 패턴을 찾습니다. 찾으면 리플렉션을 사용해 `markerData`에서 일치하는 속성을 읽어 값을 기록합니다. 수동 루프가 필요 없습니다.

## Step 5: Save the Workbook – Fill Excel Comment and Persist the File

## 단계 5: 워크북 저장 – Excel 주석 채우고 파일에 저장

Finally we write the workbook to disk. The comment now reads something like *“Created by Alice on 03/21/2026 10:15 AM”*.

마지막으로 워크북을 디스크에 저장합니다. 이제 주석은 *“Created by Alice on 03/21/2026 10:15 AM”*와 같이 표시됩니다.

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Result verification:** Open `CommentFilled.xlsx` in Excel, hover over cell **B2**, and you’ll see the comment with the actual user name and timestamp. No further code changes needed for future runs—just change `markerData` values.

**결과 확인:** Excel에서 `CommentFilled.xlsx`를 열고 **B2** 셀 위에 마우스를 올리면 실제 사용자 이름과 타임스탬프가 포함된 주석을 볼 수 있습니다. 향후 실행을 위해 추가 코드를 변경할 필요 없이 `markerData` 값만 바꾸면 됩니다.

## Common Variations & Edge Cases

## 일반적인 변형 및 엣지 케이스

### Using a Custom Date Format

### 사용자 정의 날짜 형식 사용

If you want the date in `yyyy‑MM‑dd` format, adjust the data object:

날짜를 `yyyy‑MM‑dd` 형식으로 표시하고 싶다면 데이터 객체를 다음과 같이 조정합니다:

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### Adding Multiple Comments

### 여러 주석 추가

You can repeat **Step 2** for other cells. Each comment can have its own set of tokens, or share the same ones if the information is universal.

**Step 2**를 다른 셀에 반복해서 적용할 수 있습니다. 각 주석은 자체 토큰 세트를 가질 수 있으며, 정보가 공통적이라면 동일한 토큰을 공유할 수도 있습니다.

### Working with Existing Workbooks

### 기존 워크북 작업

Instead of `new Workbook()`, load an existing file:

`new Workbook()` 대신 기존 파일을 로드합니다:

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

The rest of the steps stay identical—Smart Markers work on both new and pre‑existing files.

나머지 단계는 동일하게 유지됩니다—스마트 마커는 새 파일과 기존 파일 모두에서 작동합니다.

### Handling Null Values

### Null 값 처리

If a token might be missing, wrap the property in a nullable type or provide a fallback:

토큰이 없을 수도 있는 경우, 속성을 nullable 타입으로 감싸거나 대체 값을 제공하세요:

```csharp
UserName = user?.Name ?? "Unknown"
```

The processor will insert *“Unknown”* when the source is `null`.

소스가 `null`이면 프로세서는 *“Unknown”*를 삽입합니다.

## Full Working Example (Copy‑Paste Ready)

## 전체 작업 예제 (복사‑붙여넣기 준비)

Below is the **entire program** you can drop into a console app project and run immediately (just replace `YOUR_DIRECTORY` with a real folder path).

아래는 **전체 프로그램**으로, 콘솔 앱 프로젝트에 바로 넣고 실행할 수 있습니다 (`YOUR_DIRECTORY`를 실제 폴더 경로로 교체하면 됩니다).

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Run the program, open the generated file, and you’ll see the dynamic comment in cell **B2**. Easy, right?

프로그램을 실행하고 생성된 파일을 열면 **B2** 셀에 동적 주석이 표시됩니다. 쉽죠?

## Frequently Asked Questions (FAQ)

## 자주 묻는 질문 (FAQ)

**Q: Does this work with .NET Framework 4.7?**  
**Q: .NET Framework 4.7에서도 작동하나요?**  
A: Absolutely. Aspose.Cells supports .NET Framework 4.0+ and .NET Core/5/6/7. Just reference the appropriate DLL or NuGet package.  
A: 물론입니다. Aspose.Cells는 .NET Framework 4.0 이상 및 .NET Core/5/6/7을 지원합니다. 해당 DLL이나 NuGet 패키지를 참조하면 됩니다.

**Q: Can I use this approach for data validation or conditional formatting?**  
**Q: 이 방법을 데이터 검증이나 조건부 서식에 사용할 수 있나요?**  
A: Smart Markers are primarily for inserting values into cells, comments, headers, and footers. For conditional formatting you’d still use the normal `Style` APIs.  
A: 스마트 마커는 주로 셀, 주석, 헤더, 푸터에 값을 삽입하는 데 사용됩니다. 조건부 서식은 여전히 일반 `Style` API를 사용해야 합니다.

**Q: What if I need to add a comment to a **different** worksheet?**  
**Q: **다른** 워크시트에 주석을 추가하려면 어떻게 해야 하나요?**  
A: Retrieve the target worksheet (`workbook.Worksheets["MySheet"]`) and repeat **Step 2** on that sheet’s cells.  
A: 대상 워크시트(`workbook.Worksheets["MySheet"]`)를 가져온 뒤 해당 시트의 셀에 **Step 2**를 반복하면 됩니다.

## Next Steps & Related Topics

## 다음 단계 및 관련 주제

- **How to add comment to Excel** programmatically for multiple cells (loop through a range).  
- **How to add comment to Excel**를 프로그래밍 방식으로 여러 셀에 적용하기 (범위 반복).  
- **Fill Excel comment** with data from a database (use a `DataTable` as the data source for Smart Markers).  
- **Fill Excel comment**를 데이터베이스 데이터로 채우기 (`DataTable`을 스마트 마커의 데이터 소스로 사용).  
- Explore **Smart Marker arrays** to generate tables automatically.  
- **Smart Marker arrays**를 탐색하여 테이블을 자동으로 생성하기.  
- Learn about **Aspose.Cells styling** to format the comment’s font, color, and size.  
- **Aspose.Cells styling**을 배워 주석의 글꼴, 색상 및 크기를 지정하기.

Experiment with the snippets, swap out the data source, and you’ll quickly master **how to fill comment** in any Excel automation scenario.

스니펫을 실험하고 데이터 소스를 교체하면 어떤 Excel 자동화 시나리오에서도 **how to fill comment**를 빠르게 마스터할 수 있습니다.

### Wrap‑Up

### 마무리

We’ve just walked through the entire process of **create excel workbook c#**, **add comment to excel**, and **fill excel comment** using Smart Markers. The solution is compact, reusable, and ready for production.  

Give it a try, tweak the placeholders, and let the library handle the heavy lifting. If you run into any snags, drop a comment below—happy coding!

우리는 이제 **create excel workbook c#**, **add comment to excel**, 그리고 스마트 마커를 사용한 **fill excel comment** 전체 과정을 살펴보았습니다. 이 솔루션은 간결하고 재사용 가능하며 프로덕션에 바로 사용할 수 있습니다.  

시도해 보고, 플레이스홀더를 조정하고, 라이브러리가 무거운 작업을 처리하도록 하세요. 문제가 발생하면 아래에 댓글을 남겨 주세요—행복한 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}