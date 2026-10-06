---
category: general
date: 2026-05-30
description: C#를 사용하여 Excel에서 텍스트 상자 글꼴 크기 변경. 단계별 코드를 통해 Excel 텍스트 상자 글꼴을 빠르게 수정하는
  방법을 배워보세요.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: ko
og_description: C#를 사용하여 Excel에서 텍스트 상자 글꼴 크기 변경. 이 가이드는 Excel 텍스트 상자 글꼴을 안전하고 효율적으로
  수정하는 방법을 보여줍니다.
og_title: C#로 Excel에서 텍스트 상자 글꼴 크기 변경 – 전체 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: C#로 Excel 텍스트 상자 글꼴 크기 변경 – 완전 가이드
url: /ko/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 Excel에서 텍스트 상자 글꼴 크기 변경 – 완전 가이드

C#에서 Excel 워크시트의 **텍스트 상자 글꼴 크기**를 변경해야 하나요? 바로 여기입니다. 보고서를 생성하거나, 대시보드를 구축하거나, 템플릿을 약간 수정하든, 텍스트 상자의 외관을 조정하면 스프레드시트가 훨씬 더 전문적으로 보입니다.

이 튜토리얼에서는 **Excel 텍스트 상자 글꼴**을 크기뿐만 아니라 글꼴 종류, 굵기, 그리고 여러 도형 처리까지 수정하는 방법도 다룹니다. 끝까지 진행하면 워크북을 여는 것부터 COM 객체를 정리하는 것까지 전체 과정을 포괄하는 실행 가능한 코드 스니펫을 얻게 됩니다. 불필요한 내용 없이 바로 프로젝트에 적용할 수 있는 실용적인 코드만 제공합니다.

## 사전 요구 사항 — 필요한 것들

본격적으로 시작하기 전에, 아래 항목들이 시스템에 설치되어 있는지 확인하세요:

| 요구 사항 | 필요한 이유 |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | C# 컴파일러와 런타임을 제공합니다. |
| **Microsoft.Office.Interop.Excel** NuGet package | Excel과 통신하는 데 필요한 COM 인터옵 타입을 제공합니다. |
| **Excel installed** (any recent version) | Interop 레이어는 Office 애플리케이션이 설치되어 있을 때만 작동합니다. |
| **Basic C# knowledge** | 쉽게 따라올 수 있지만, 모든 코드를 자세히 설명합니다. |

위 항목 중 하나라도 누락되었다면, 지금 설치하십시오. 나머지 가이드는 모두 설치되어 있다고 가정합니다.

## 단계 1: 프로젝트 설정 및 네임스페이스 가져오기

먼저, 새 콘솔 앱을 만들거나 기존 프로젝트에 통합하고, Interop 네임스페이스를 가져옵니다.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **팁:** .NET 6+를 대상으로 하는 경우 `dotnet add package Microsoft.Office.Interop.Excel` 명령으로 `Microsoft.Office.Interop.Excel` 패키지를 추가하세요. 이렇게 하면 `Excel` 별칭이 올바르게 해석됩니다.

## 단계 2: 워크북 열기 및 대상 워크시트 가져오기

이제 Excel을 실행하고 파일을 열어 텍스트 상자가 있는 시트를 지정해야 합니다. 이를 `try/finally` 블록으로 감싸면 오류가 발생하더라도 COM 객체가 해제되는 것을 보장합니다.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### 왜 중요한가

COM을 통해 워크북을 열면 실시간 객체 모델을 얻을 수 있어, 변경 사항이 파일에 즉시 반영됩니다. `Visible = false`로 설정하면 자동화 중에 창이 나타나는 것을 방지하고 속도가 빨라집니다.

## 단계 3: 텍스트 상자 도형 가져오기

Excel은 텍스트 상자를 전용 `TextBox` 컬렉션이 아니라 `Shapes` 컬렉션에 포함된 `Shape` 객체로 취급합니다. 그래서 아래 코드는 온라인에서 본 예시와 약간 다르게 보일 수 있습니다.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **주의:** `Shapes` 컬렉션은 1부터 시작하므로 전달한 0 기반 `textboxIndex`에 `+1`을 더합니다. 이를 놓치면 “인덱스 범위 초과” 오류가 발생해 디버깅이 번거로울 수 있습니다.

## 단계 4: 텍스트 상자 글꼴 크기(및 이름) 변경

이제 **텍스트 상자 글꼴 크기**를 실제로 변경합니다. `TextFrame2` 속성을 통해 `Font.Name`과 `Font.Size`를 포함한 풍부한 텍스트 서식 옵션에 접근할 수 있습니다.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### 왜 `TextFrame2`를 사용하는가

`TextFrame2`는 Office 2007에 도입된 최신 객체 모델입니다. 고급 타이포그래피 기능을 지원하며 기존 `TextFrame`보다 일반적으로 더 안정적입니다. 이를 사용하면 **텍스트 상자 글꼴 크기 변경** 작업이 최신 Excel 버전에서도 정상적으로 동작합니다.

## 단계 5: 저장, 정리 및 검증

글꼴을 조정한 후에는 변경 사항을 저장하고 모든 COM 참조를 해제해야 합니다. 정리를 생략하면 백그라운드에 고아 Excel 프로세스가 남을 수 있습니다.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **팁:** 여러 워크시트에서 **Excel 텍스트 상자 글꼴**을 수정해야 한다면, 내부 로직을 `Workbook.Worksheets`를 순회하는 루프로 감싸세요. 각 시트마다 `textboxIndex`를 초기화하는 것을 잊지 마세요.

## 엣지 케이스 처리 — 여러 텍스트 상자 및 누락된 도형

실제 스프레드시트는 보통 하나의 텍스트 상자만 포함하지 않습니다. 아래는 전체 메서드를 다시 작성하지 않고도 적용할 수 있는 두 가지 간단한 전략입니다.

### 1. 시트의 *전체* 텍스트 상자 변경

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. 인덱스 대신 **Name**으로 텍스트 상자 식별

텍스트 상자에 의미 있는 이름(예: “TitleBox”)을 지정했다면, 직접 해당 이름으로 가져올 수 있습니다:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

두 방법 모두 워크북 구조와 관계없이 **Excel 텍스트 상자 글꼴**을 정밀하게 수정할 수 있게 해줍니다.

## 시각적 개요 (선택 사항)

빠른 시각적 힌트를 원한다면, 다음 다이어그램을 상상해 보세요:

![Excel 워크시트에 강조된 텍스트 상자를 보여주는 스크린샷 – 텍스트 상자 글꼴 크기 변경 방법을 시연](change-textbox-font-size.png)

*Alt text:* *Excel에서 텍스트 상자 글꼴 크기 변경 – 글꼴 수정 준비가 된 강조된 텍스트 상자.*

## 전체 작동 예제

모든 내용을 종합하면, 콘솔 프로젝트에 복사‑붙여넣기만 하면 바로 실행할 수 있는 단일 파일 예제가 아래에 있습니다(파일 경로와 시트 이름만 업데이트하면 됩니다).



## 다음에 배울 내용은?

- [Excel에서 글꼴 크기 변경](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Aspose.Cells .NET을 사용하여 Excel 셀의 글꼴 크기 사용자 지정 방법 | 완전 가이드](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Aspose.Cells for .NET을 사용하여 Excel에서 글꼴 스타일 설정 방법 (단계별 가이드)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}