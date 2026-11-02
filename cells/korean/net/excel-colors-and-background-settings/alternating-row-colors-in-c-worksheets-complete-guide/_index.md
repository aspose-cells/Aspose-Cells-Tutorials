---
category: general
date: 2026-05-30
description: C# 워크시트에서 교차 행 색상을 추가하는 방법, 셀 배경을 단색 채우기 패턴으로 설정하는 방법, 그리고 워크시트 셀 스타일을
  손쉽게 사용자 지정하는 방법을 배워보세요.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: ko
og_description: C# 워크시트에서 행 색상을 번갈아 적용하는 것이 쉬워졌습니다. 셀 배경 설정 방법, 단색 채우기 패턴 사용법, 그리고
  워크시트 셀 스타일 마스터하기를 배워보세요.
og_title: C# 워크시트에서 교차 행 색상 적용 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: C# 워크시트에서 교차 행 색상 적용 – 완전 가이드
url: /ko/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 워크시트에서 교차 행 색상 적용 – 완전 가이드

Excel 내보내기를 **교차 행 색상**으로 깔끔하게 만들고 싶었던 적이 있나요? 당신만 그런 것이 아닙니다—개발자들은 행에 *배경 색상*을 추가하는 방법을 수많은 코드를 작성하지 않고도 자주 묻습니다.  

이 튜토리얼에서는 각 행에 **셀 배경을 설정**하고, **단색 채우기 패턴**을 적용하며, **워크시트 셀 스타일**을 제어하는 간단한 방법을 단계별로 안내합니다. 이를 통해 결과물이 가독성이 높고 시각적으로도 매력적이게 됩니다.

## 배울 내용

- `DataTable`(또는 기타 표 형식 소스)로 데이터를 가져오기.  
- 두 가지 색상이 교차하도록 `Style` 객체 배열을 만들기.  
- 해당 스타일을 적용하면서 `DataTable`을 워크시트에 가져오기.  
- 출력을 확인하고 필요에 따라 색상이나 패턴을 조정하기.  

.NET 환경과 스프레드시트 라이브러리(예제에서는 **Aspose.Cells**를 사용)만 있으면 됩니다. 끝까지 진행하면 어느 보고 파이프라인에든 삽입할 수 있는 재사용 가능한 메서드를 얻게 됩니다.

---

## 단계 1: 소스 데이터를 `DataTable`로 가져오기

우선, 데이터가 없으면 스타일을 적용할 것이 없습니다. 아래는 샘플 행으로 `DataTable`을 만드는 작은 도우미 코드입니다. 실제 프로젝트에서는 이를 데이터베이스 호출이나 CSV 파서로 교체하면 됩니다.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **왜 중요한가:** 데이터를 `DataTable`에 보관하면 워크시트 엔진이 한 번에 *import*하여 열 이름과 데이터 형식을 자동으로 보존합니다.

## 단계 2: **교차 행 색상** 스타일 만들기

이제 각 행마다 하나씩 `Style` 객체 배열을 생성합니다—짝수 행은 연한 노란색, 홀수 행은 부드러운 시안 색으로 지정합니다. 이것이 **교차 행 색상** 기법의 핵심입니다.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### **단색 채우기 패턴**을 사용하는 이유

`Pattern` 속성은 엔진에게 색상을 어떻게 렌더링할지 알려줍니다. `Solid` 채우기는 셀 전체 배경을 칠하도록 보장하여, 격자선이 비치는 것을 방지합니다. 깔끔한 모습을 원할 때 **셀 배경을 설정**하는 가장 일반적인 방법입니다.

## 단계 3: 준비된 스타일로 `DataTable` 가져오기

스타일 배열이 준비되면 가져오기 호출은 한 줄로 끝납니다. Aspose.Cells가 각 행에 해당 스타일을 자동으로 적용합니다.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **내부에서 무슨 일이 일어나나요?**  
> 라이브러리는 각 행을 순회하면서 값을 셀에 복사하고, `rowStyles`에서 일치하는 `Style`을 적용합니다. 이미 **단색 채우기 패턴**을 정의했기 때문에 행의 모든 셀은 동일한 배경 색을 상속받아 완벽한 **교차 행 색상**을 제공합니다.

## 단계 4: 워크북 저장 및 결과 확인

간단히 저장하면 Excel(또는 호환 뷰어)에서 파일을 열어 효과를 확인할 수 있습니다.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

파일을 열면 1, 3, 5… 행은 연한 노란색, 2, 4, 6… 행은 연한 시안 색이 됩니다. 열 헤더는 흰색으로 유지되어 데이터가 돋보입니다.

![교차 행 색상이 적용된 워크시트](/images/alternating-row-colors.png "교차 행 색상이 적용된 워크시트의 스크린샷")

*이미지 대체 텍스트:* **교차 행 색상** 스크린샷으로, 각 행의 배경이 연한 노란색과 연한 시안 색으로 교차합니다.

## 단계 5: 추가 커스터마이징 (선택 사항)

### 색상 변경

브랜드 색상이 다르면 `Color.LightYellow`와 `Color.LightCyan`을 원하는 `System.Drawing.Color`로 교체하면 됩니다. 예시:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### 다른 **배경 유형** 사용하기

`BackgroundType.Solid`가 가장 일반적이지만, `BackgroundType.Gray125`, `BackgroundType.Horizontal` 등 라이브러리가 지원하는 다른 패턴을 실험해 볼 수 있습니다. 이렇게 하면 시각적 질감이 바뀌면서도 **배경 색상 추가**가 가능합니다.

### 특정 열에 **워크시트 셀 스타일** 적용하기

때때로 데이터 열에만 교차 효과를 적용하고 첫 번째 열(예: ID)은 그대로 두고 싶을 때가 있습니다. 해당 열에 별도의 스타일을 만들고 가져온 후에 할당하면 됩니다:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## 결론

이제 C# 워크시트에서 **교차 행 색상**을 적용하기 위한 완전하고 재사용 가능한 솔루션을 갖게되었습니다. `Style` 객체 배열을 만들고, **단색 채우기 패턴**으로 **셀 배경을 설정**하며, `DataTable`을 한 번에 가져오면 최소한의 코드로 전문가 수준의 보고서를 만들 수 있습니다.  

다음과 같이 활용해 볼 수 있습니다:

- 헤더 행에 **배경 색상 추가**하여 강조하기.  
- 동적 시각적 힌트를 위해 조건부 서식과 결합하기.  
- 글꼴, 테두리, 숫자 형식 등 다른 **워크시트 셀 스타일** 속성 탐색하기.

다음 내보내기 작업에 적용해 보세요—사용자들은 더 깔끔하고 가독성 높은 스프레드시트에 감사할 것입니다. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

- [Aspose.Cells for .NET을 사용하여 워크시트 행 높이 설정](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Aspose.Cells for .NET을 사용하여 Excel 셀 이름을 행 및 열 인덱스로 변환](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Aspose.Cells .NET을 사용하여 Excel 워크시트 탭 색상 설정 - 종합 가이드](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}