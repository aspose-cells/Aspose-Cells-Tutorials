---
category: general
date: 2026-03-30
description: C#에서 Aspose.Cells를 사용하여 워크시트를 복사하는 방법 – 셀 범위 복사, 시트 간 열 복사, 워크시트 피벗 테이블
  복사 및 새 워크시트 추가 코드를 포함한 단계별 가이드.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: ko
og_description: Aspose.Cells를 사용하여 C#에서 워크시트를 복사하는 방법을 배웁니다. 이 가이드는 셀 범위 복사, 피벗 테이블
  보존, 시트 간 열 복사 및 새 워크시트 추가 코드를 보여줍니다.
og_title: C#에서 워크시트 복사하는 방법 – 전체 Aspose.Cells 튜토리얼
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C#에서 Aspose.Cells를 사용하여 워크시트를 복사하는 방법 – 완전 가이드
url: /ko/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#와 Aspose.Cells를 사용한 워크시트 복사 방법 – 완전 가이드

C#에서 **how to copy worksheet**을 고민해 본 적 있나요? 피벗 테이블이나 수식을 하나도 잃지 않고 말이죠. 당신만 그런 것이 아닙니다—많은 개발자들이 시트를 복제하면서 모든 요소를 그대로 유지해야 할 때 난관에 봉착합니다. 이 튜토리얼에서는 데이터를 복사할 뿐만 아니라 **copy worksheet pivot table**, **copy cell range**를 처리하고 필요한 **add new worksheet code**를 보여주는 실용적인 엔드‑투‑엔드 솔루션을 단계별로 안내합니다.

소스 워크북을 로드하는 것부터 대상 파일을 저장하는 것까지 모든 과정을 다룹니다. 이를 통해 시트 간에 열을 복사하고, 객체를 보존하며, 코드를 깔끔하게 유지할 수 있습니다. 모호한 설명 없이, 오늘 바로 프로젝트에 넣어 사용할 수 있는 완전하고 실행 가능한 예제를 제공합니다.

## 이 튜토리얼에서 다루는 내용

- Aspose.Cells를 사용하여 기존 Excel 파일 로드  
- **add new worksheet code**를 사용해 대상 시트 생성  
- 피벗 테이블을 포함하는 **copy cell range** 정의  
- 차트, 수식, 피벗 테이블을 유지하도록 **CopyOptions** 설정  
- 행 단위 정밀도로 **copy columns between sheets** 실행  
- 결과 저장 및 워크시트가 올바르게 복사되었는지 확인  

이 가이드를 마치면 보고서를 자동화하든 스프레드시트 기반 UI를 구축하든, “how to copy worksheet” 질문에 자신 있게 답할 수 있게 됩니다.

## 워크시트 복사 방법 – 개요

코드에 들어가기 전에 전체 흐름을 개략적으로 살펴보겠습니다. 레시피처럼 생각하세요:

1. **Load** 소스 워크북 (`Source.xlsx`).  
2. **Add** 복사본을 담을 새 워크시트 (`add new worksheet code`).  
3. **Define** 복제하려는 영역 (`copy cell range`).  
4. **Configure** 피벗 테이블이 유지되도록 복사 옵션 설정 (`copy worksheet pivot table`).  
5. **Copy** 행과 열 (`copy columns between sheets`).  
6. **Save** 새 워크북 (`Destination.xlsx`).  

이것이 전부—여섯 단계, 마법은 없습니다. 각 단계는 아래에서 코드 스니펫과 함께 이유를 설명합니다.

## 단계 1 – 소스 워크북 로드

먼저 해야 할 일: 복제하려는 파일을 가리키는 `Workbook` 인스턴스가 필요합니다. 이 단계는 Aspose.Cells가 Office UI가 아니라 파일 시스템과 직접 작업하기 때문에 필수적입니다.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*왜 중요한가:* 파일을 로드하면 모든 시트, 셀, 객체가 메모리에 표현됩니다. 이것이 없으면 복사할 것이 없으며, 이후 `add new worksheet code`를 시도해도 소스 데이터가 없기 때문에 실패합니다.

## 단계 2 – 새 워크시트 추가 (add new worksheet code)

이제 복사된 데이터를 붙여넣을 위치가 필요합니다. 바로 여기서 **add new worksheet code**가 빛을 발합니다. 시트 이름은 원하는 대로 지정할 수 있습니다; 여기서는 `"Copy"`라고 부릅니다.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*팁:* 여러 시트를 복사할 계획이라면 루프 안에서 `Worksheets.Add`를 호출하고 각 시트에 고유한 이름을 부여하세요. 이렇게 하면 이름 충돌을 방지하고 워크북을 깔끔하게 유지할 수 있습니다.

## 단계 3 – 복사 셀 범위 정의

**copy cell range**는 Aspose.Cells에 정확히 어떤 행과 열을 복제할지 알려줍니다. 실제 상황에서는 이 범위에 피벗 테이블이 포함되는 경우가 많아 정확해야 합니다.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*왜 필요한가:* 범위를 명시함으로써 전체 시트를 복사하는 비효율을 피하고 피벗 테이블이 복사된 영역에 포함되도록 보장합니다. 이는 시트의 일부만 필요할 때 **how to copy worksheet**의 핵심입니다.

## 단계 4 – 복사 옵션 설정 (copy worksheet 피벗 테이블 보존)

Aspose.Cells는 붙여넣을 내용을 제어하는 `CopyOptions` 객체를 제공합니다. 피벗 테이블, 차트, 수식을 유지하려면 `PasteType.All`을 설정하고 `PasteSpecial`을 활성화합니다.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*설명:* `PasteType.All`은 가장 포괄적인 옵션이며, `PasteSpecial`은 엔진에게 피벗 테이블과 같은 복합 객체를 올바르게 처리하도록 지시합니다. 이 단계를 건너뛰면 복사된 시트가 인터랙티브 기능을 잃는 흔한 실수가 됩니다.

## 단계 5 – 행 및 열 복사 (copy columns between sheets)

이제 실제 데이터 이동이라는 무거운 작업이 시작됩니다. `CopyRows`와 `CopyColumns`를 사용해 **copy columns between sheets**를 처리합니다. 두 작업을 모두 수행하면 병합 셀과 열 너비가 보존됩니다.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*무슨 일인가:* `CopyRows`는 데이터를 행 단위로 이동하고, `CopyColumns`는 열 단위로 이동합니다. 두 작업을 모두 실행하면 전체 직사각형 블록이 복제되어, 열 너비가 다르거나 숨겨진 열이 있는 시트 간에 **copy columns between sheets**가 필요할 때 필수적입니다.

## 단계 6 – 워크북 저장

마지막으로 변경 사항을 디스크에 기록합니다. 이 단계가 **how to copy worksheet** 과정을 완성합니다.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*검증 팁:* `Destination.xlsx`를 열어 `"Copy"` 시트가 원본과 동일하게 보이고, 피벗 테이블이 정상 작동하며, 열 너비가 일치하는지 확인하세요. 문제가 있으면 `CopyOptions` 설정을 다시 검토하세요.

## 엣지 케이스 및 일반적인 변형

### 여러 워크시트 복사

여러 시트를 복제해야 한다면 위 로직을 `foreach` 루프로 감싸세요:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### 다른 워크북 간 수식 보존

소스와 대상 워크북에 서로 다른 이름 정의가 있을 경우, `All` 외에 `PasteType.Formulas`로 `copyOptions`를 설정하세요:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### 대규모 범위 및 성능

수백만 행과 같은 대규모 데이터셋의 경우, 열 너비가 중요하지 않다면 `CopyColumns`를 생략하고 `CopyRows`만 사용하는 것을 고려하세요. 이렇게 하면 몇 초 정도 시간을 절약할 수 있습니다.

## 전체 작업 예제

아래는 지금까지 논의한 모든 내용을 담은 완전하고 바로 실행 가능한 프로그램입니다. 콘솔 앱에 붙여넣고 파일 경로를 조정한 뒤 **F5**를 눌러 실행하세요.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**예상 결과:** `Destination.xlsx`를 열면 **Copy**라는 시트가 `Source.xlsx`의 첫 번째 시트를 그대로 복제한 모습을 보여줍니다—피벗 테이블, 서식, 열 너비 모두 포함됩니다. 원본 파일은 그대로 유지됩니다.

## 자주 묻는 질문

**Q: 이 코드가 Excel 2019에서 만든 .xlsx 파일에도 작동하나요?**  
A: 물론입니다. Aspose.Cells는 모든 최신 Excel 형식을 지원하므로 동일한 코드를 `.xlsx`, `.xlsm`, 그리고 오래된 `.xls` 파일에도 사용할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}