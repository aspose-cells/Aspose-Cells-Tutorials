---
category: general
date: 2026-02-15
description: C#에서 글꼴을 복사하고 셀 스타일을 적용하는 방법을 간단한 예제로 알아보세요. 셀 스타일을 가져오고 셀 서식을 사용하여 텍스트박스
  글꼴 크기를 설정하는 방법을 배웁니다.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: ko
og_description: 워크시트 셀에서 글꼴을 복사하여 텍스트 상자에 셀 스타일을 적용하는 방법. 이 가이드는 셀 스타일을 가져오고, 셀 서식을
  사용하며, 텍스트 상자 글꼴 크기를 설정하는 방법을 보여줍니다.
og_title: Excel 셀에서 글꼴 복사 방법 – 완전한 C# 튜토리얼
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Excel 셀의 글꼴을 TextBox에 복사하는 방법 – 단계별 가이드
url: /ko/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 셀에서 폰트를 복사하여 TextBox에 적용하는 방법 – 완전한 C# 튜토리얼

스프레드시트 셀에서 **폰트를 복사**해서 UI 텍스트 박스를 정확히 동일하게 만들고 싶었던 적이 있나요? 여러분만 그런 것이 아닙니다. 많은 보고서 도구나 맞춤형 대시보드에서 Excel에서 데이터를 가져오면서 시각적 일관성—폰트 패밀리, 크기, 색상—을 유지하려고 합니다.  

좋은 소식은 몇 줄의 C# 코드만으로 **셀 스타일을 가져오고**, 폰트 속성을 읽은 뒤 **셀 스타일을 적용**하여 텍스트‑박스 컨트롤에 적용할 수 있다는 것입니다. 이 튜토리얼에서는 **셀 서식 사용**과 **프로그래밍 방식으로 텍스트박스 폰트 크기 설정**을 보여주는 완전하고 실행 가능한 예제를 단계별로 살펴보겠습니다.

---

## 배울 내용

- 그리드 컴포넌트(`gridJs` 샘플)에서 `TextBox` 객체를 가져오는 방법
- 특정 Excel 셀(`B2`)에서 폰트 패밀리, 크기, 색상을 읽는 방법
- 해당 폰트 속성을 텍스트 박스로 복사하여 UI가 스프레드시트와 동일하게 보이게 하는 방법
- 흔히 발생하는 함정(예: 색상 변환)과 코드를 견고하게 유지하기 위한 몇 가지 **프로 팁**
- 콘솔 앱이나 WinForms 프로젝트에 바로 넣어 실행할 수 있는 코드 스니펫

**전제 조건**  
다음이 준비되어 있어야 합니다:

1. .NET 6+ (또는 .NET Framework 4.8) 설치  
2. EPPlus NuGet 패키지 (Excel 처리용)  
3. `TextBoxes` 딕셔너리를 노출하는 그리드 컨트롤 (예제는 가상의 `gridJs`를 사용하지만, 어떤 UI 라이브러리에서도 동일하게 적용 가능)

그럼 바로 시작해 보겠습니다.

---

## Step 1: 프로젝트 설정 및 워크시트 로드

먼저 새 콘솔 또는 WinForms 프로젝트를 만들고 EPPlus를 추가합니다:

```bash
dotnet add package EPPlus --version 6.*
```

그 다음 워크북을 로드하고 복사하려는 셀의 스타일을 가져옵니다.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**왜 중요한가:** EPPlus는 `Style` 객체에 직접 접근할 수 있게 해 주며, 여기에는 `Font` 서브‑오브젝트가 포함됩니다. 여기서 `Name`, `Size`, `Color`를 읽을 수 있습니다. 이것이 **셀 스타일 가져오기** 작업의 핵심입니다.

---

## Step 2: 그리드에서 대상 TextBox 가져오기

UI 그리드(`gridJs`)가 컬럼 이름을 키로 하는 딕셔너리 형태로 텍스트 박스를 저장하고 있다고 가정하면, 다음과 같이 원하는 텍스트 박스를 가져올 수 있습니다:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

WinForms에서는 `notesTextBox`가 `TextBox` 컨트롤일 수 있고, WPF에서는 `TextBox` 요소일 수 있으며, 웹‑기반 그리드에서는 JavaScript 인터옵 객체일 수 있습니다. 중요한 점은 조작할 수 있는 레퍼런스를 확보했다는 것입니다.

---

## Step 3: 폰트 패밀리 복사

이제 원본 스타일과 대상 컨트롤을 모두 확보했으니, 폰트 패밀리를 복사합니다.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**프로 팁:** 모든 UI 프레임워크가 문자열을 직접 받아들이는 `FontFamily` 속성을 제공하는 것은 아닙니다. WinForms에서는 `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`와 같이 설정합니다. 상황에 맞게 조정하세요.

---

## Step 4: 폰트 크기 복사

EPPlus에서는 폰트 크기가 `float` 형태로 저장됩니다. 그대로 적용하면 됩니다:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

대부분의 컨트롤이 포인트 단위를 사용하므로 변환 없이 값을 할당할 수 있습니다. CSS 기반 그리드에서는 `"pt"`를 붙여야 할 수도 있습니다.

---

## Step 5: 폰트 색상 복사

색상 변환은 가장 까다로운 부분입니다. EPPlus는 색상을 ARGB 정수로 저장하지만, 많은 UI 프레임워크는 `System.Drawing.Color` 혹은 CSS 헥스 문자열을 기대합니다.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **왜 동작하는가:** `GetColor()`는 테마 기반 색상을 해결하고 구체적인 `System.Drawing.Color`를 반환합니다. 셀에 기본 색상(명시적 설정 없음)만 사용된 경우, 널 레퍼런스 예외를 방지하기 위해 기본값을 검정색으로 지정합니다.

---

## 전체 작동 예제

모든 코드를 합치면, Excel 파일을 읽고 **B2** 셀의 폰트를 추출한 뒤 모의 텍스트 박스에 적용하는 최소 콘솔 앱이 됩니다.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**예상 출력 (B2 셀에 Arial, 12 pt, 파란색 사용 가정):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

프로그램을 실행하고 UI를 열면 “Notes” 텍스트 박스가 셀 **B2**와 정확히 동일한 폰트 스타일을 갖게 됩니다. 수동 조정이 전혀 필요 없습니다.

---

## Frequently Asked Questions & Edge Cases

### 셀에 명시적 RGB 값 대신 테마 색상이 사용된 경우는?

EPPlus의 `GetColor()`는 테마 색상을 자동으로 구체적인 `System.Drawing.Color`로 변환합니다. 하지만 오래된 라이브러리에서 테마 인덱스만 반환한다면, 해당 인덱스를 색상 팔레트와 매핑해야 합니다.

### 굵게, 기울임 등 다른 스타일 속성도 복사할 수 있나요?

가능합니다. `ExcelStyle.Font` 객체는 `Bold`, `Italic`, `Underline`, `Strike`도 제공하므로 UI 컨트롤에 해당 속성을 설정하면 됩니다:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### 그리드 컨트롤에 `FontColor` 속성이 없으면?

대부분 최신 UI 프레임워크는 제공하지만, CSS 문자열만 받는 경우 `Color`를 헥스 문자열로 변환하면 됩니다:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### 여러 셀을 한 번에 처리하려면?

원하는 범위를 순회하면서 각 셀의 스타일을 가져와 해당 텍스트 박스에 적용합니다. 많은 행을 처리할 경우 스타일 객체를 캐시해 성능 저하를 방지하세요.

---

## Pro Tips & Common Pitfalls

- **ExcelPackage 캐시** – 셀마다 파일을 열고 닫는 것은 비용이 큽니다. 워크북을 한 번 로드하고 `ExcelWorksheet` 객체를 재사용하세요.  
- **널 색상 주의** – 기본 색상을 상속받는 셀은 `null`을 반환합니다. 항상 검정색이나 컨트롤 기본값 등 대체 색상을 제공하세요.  
- **DPI 스케일링** – 고 DPI 모니터를 대상으로 할 경우 폰트 크기가 약간 크게 보일 수 있습니다. 필요하면 `Graphics.DpiX`를 활용해 조정하세요.  
- **스레드 안전성** – EPPlus는 스레드‑세이프하지 않습니다. 여러 시트를 병렬 처리한다면 스레드당 별도의 `ExcelPackage` 인스턴스를 생성하세요.

---

## 결론

이제 **Excel 셀에서 폰트를 복사**하고 **셀 스타일을 텍스트‑박스 컨트롤에 적용**하는 방법을 C#으로 알게 되었습니다. 셀의 `Style`을 가져와 `Font` 속성을 추출하고 UI 요소에 할당함으로써 수동 복사 없이도 시각적 일관성을 유지할 수 있습니다.  

워크북 로드, 셀 스타일 획득, 텍스트박스의 폰트 패밀리·크기·색상 설정까지의 전체 솔루션은 **셀 서식 사용**과 **텍스트박스 폰트 크기 설정**의 핵심을 다루며, 실제 프로젝트에 바로 적용할 수 있습니다.  

다음 단계로 배경 색, 테두리, 혹은 전체 셀 내용을 복사하도록 예제를 확장해 보세요. 풍부한 셀 렌더링을 지원하는 데이터‑그리드 라이브러리를 사용한다면, Excel에서 추출한 정확한 스타일 정보를 그대로 전달해 UI와 보고서를 완벽히 동기화할 수 있습니다.

추가 질문이 있나요? 댓글을 남기거나 “동적 Excel‑to‑UI 바인딩”, “테마 인식 색상 변환” 같은 관련 주제를 탐색해 보세요. 즐거운 코딩 되세요!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}