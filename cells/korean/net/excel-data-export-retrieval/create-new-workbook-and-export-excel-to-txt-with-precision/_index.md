---
category: general
date: 2026-02-15
description: 새 워크북을 만들고 숫자 정밀도를 설정하면서 Excel을 TXT로 내보냅니다. C#에서 유효 숫자를 설정하고 제한하는 방법을
  배웁니다.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: ko
og_description: 새 워크북을 만들고 Excel을 TXT로 내보내며, 숫자 정밀도를 위해 유효 숫자를 설정합니다. 단계별 C# 가이드.
og_title: 새 워크북 만들기 – 정확하게 Excel을 TXT로 내보내기
tags:
- C#
- Aspose.Cells
- Excel automation
title: 새 워크북 만들기 및 Excel을 정밀하게 TXT로 내보내기
url: /ko/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 새 워크북 만들기 – 정확한 숫자 형식으로 Excel을 TXT로 내보내기

C#에서 **create new workbook** 객체를 만들고 바로 평문 파일로 내보내는 방법이 궁금하신가요? 여러분만 그런 것이 아닙니다. 많은 데이터 파이프라인 시나리오에서 **export Excel to TXT**하면서 숫자를 읽기 쉽게 유지해야 하는데, 이는 소수점 이하에 표시되는 자릿수를 제한한다는 의미입니다.  

이 튜토리얼에서는 전체 과정을 단계별로 살펴보겠습니다. 새 워크북을 생성하고, **sets significant digits**(즉, 유효 숫자 제한)하도록 내보내기 옵션을 구성한 뒤, 파일을 디스크에 저장합니다. 최종적으로 **numeric precision** 요구 사항을 충족하는 실행 가능한 코드 스니펫을 얻을 수 있습니다—추가 라이브러리 없이, 마법 없이.

> **Pro tip:** 이미 Aspose.Cells를 사용 중이라면 아래에 표시된 클래스들은 해당 라이브러리의 일부입니다. 다른 플랫폼을 사용하더라도 개념은 동일하니 API 호출만 교체하면 됩니다.

---

## 필요 사항

- .NET 6+ (코드는 .NET Core와 .NET Framework 모두에서 컴파일됩니다)  
- Aspose.Cells for .NET (무료 체험판 또는 정식 라이선스) – NuGet으로 설치: `dotnet add package Aspose.Cells`  
- 원하는 IDE (Visual Studio, Rider, VS Code)  

그게 전부입니다. 별도의 설정 파일이나 숨겨진 단계는 없습니다.

---

## Step 1: Create a New Workbook

첫 번째로 해야 할 일은 **create new workbook**입니다. `Workbook` 클래스를 빈 Excel 파일이라고 생각하면 됩니다. 시트, 셀, 데이터를 채우기만 하면 됩니다.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** 깨끗한 워크북부터 시작하면 나중에 정밀도 설정에 영향을 줄 수 있는 숨겨진 서식을 피할 수 있습니다.

---

## Step 2: Configure Text Save Options – Set Significant Digits

이제 Aspose.Cells에 `.txt` 파일로 저장할 때 몇 개의 **significant digits**를 사용할지 알려줍니다. `TxtSaveOptions` 클래스의 `SignificantDigits` 속성이 바로 그 역할을 합니다.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5`는 소수점 위치와 관계없이 모든 숫자의 가장 중요한 다섯 자리를 유지한다는 의미입니다. 각 셀을 수동으로 포맷하지 않아도 **set numeric precision**을 손쉽게 적용할 수 있는 방법입니다.

---

## Step 3: Save the Workbook as a Plain‑Text File

워크북과 옵션이 준비되었으니, 이제 **export Excel to txt**를 수행합니다. `Save` 메서드는 파일 경로와 방금 구성한 옵션 객체를 인수로 받습니다.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

프로그램을 실행하면 다음과 같은 파일이 생성됩니다:

```
12346
0.00012346
3.1416
```

각 숫자가 앞서 설정한 **limit significant digits** 규칙을 따르는 것을 확인할 수 있습니다.

---

## Step 4: Verify the Result (Optional but Recommended)

생성된 `numbers.txt` 파일을 아무 편집기에서 열어볼 수 있지만, 특히 CI 파이프라인에서는 검증 단계를 자동화하는 것이 좋습니다.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

콘솔에 위의 세 줄이 표시되면 **set significant digits**가 정상적으로 적용되었으며, 내보내기가 의도대로 동작한 것입니다.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 숫자가 소수점 이하에 너무 많은 자리수로 표시됨 | `SignificantDigits`가 기본값(0)으로 남아 있음 | 원하는 자릿수로 `SignificantDigits`를 명시적으로 설정 |
| 빈 파일이 생성됨 | 저장하기 전에 워크북에 데이터가 전혀 채워지지 않음 | `Save` 호출 **전**에 셀에 데이터를 채움 |
| 파일 경로에서 `UnauthorizedAccessException` 발생 | 보호된 폴더에 쓰려고 함 | 쓰기 권한이 있는 폴더 사용 (예: `C:\Temp` 또는 `%USERPROFILE%\Documents`) |
| 매우 작은 숫자의 정밀도가 이상함 | 유효 숫자 카운트에 소수점 뒤의 앞선 0이 포함됨 | “significant”는 앞선 0을 무시한다는 점을 기억; 예: 0.000123456을 5자리로 하면 `0.00012346` |

---

## Full Working Example (Copy‑Paste Ready)

아래는 완전하고 독립적인 프로그램 전체 코드입니다. 새 콘솔 프로젝트에 붙여넣고 **Run**을 눌러 실행하세요.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Expected console output**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

그리고 `numbers.txt` 파일에는 위에서 본 세 줄이 들어갑니다.

---

## Next Steps: Going Beyond the Basics

- **Export other formats** – Aspose.Cells는 CSV, HTML, PDF도 지원합니다. 필요에 따라 `TxtSaveOptions`를 `CsvSaveOptions` 또는 `PdfSaveOptions`로 교체하세요.  
- **Dynamic precision** – 사용자 입력이나 설정 파일에 따라 런타임에 `SignificantDigits`를 계산할 수 있습니다.  
- **Multiple worksheets** – `workbook.Worksheets`를 순회하면서 각 워크시트를 별도의 `.txt` 파일로 내보내세요.  
- **Localization** – 지역 설정에 맞게 소수 구분자(`.` vs `,`)를 `CultureInfo`를 통해 제어할 수 있습니다.  

이 모든 확장 기능은 이번에 다룬 핵심 아이디어, 즉 **create new workbook**, 내보내기 옵션 설정, 그리고 **set numeric precision**을 기반으로 합니다.

---

## Summary

우리는 새 **create new workbook** 인스턴스를 만들고 데이터를 채운 뒤, **export Excel to TXT**하면서 **setting significant digits**를 적용해 출력 정밀도를 제한하는 방법을 보여주었습니다. 전체 예제는 바로 실행할 수 있으며, 각 라인 뒤에 있는 *why* 설명을 통해 여러분의 프로젝트에 맞게 쉽게 변형할 수 있습니다.

자유롭게 실험해 보세요—`SignificantDigits` 값을 바꾸거나 시트를 추가하고, 출력 형식을 전환해 보세요. 문제가 발생하면 Aspose.Cells 문서를 확인하거나 아래에 댓글을 남겨 주세요. Happy coding!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}