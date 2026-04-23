---
category: general
date: 2026-03-18
description: C#를 사용하여 워크시트에 교차 행 색상을 적용하는 방법을 배웁니다. 행 배경색 설정, 연한 노란색 배경 추가, 행을 교대로
  색칠하는 내용을 포함합니다.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: ko
og_description: C#에서 교대 행 색상을 적용하여 가독성을 향상시킵니다. 이 가이드는 행 배경 색상을 설정하고, 연한 노란색 배경을 추가하며,
  행을 교대로 색칠하는 방법을 보여줍니다.
og_title: C#에서 교대 행 색상 적용 – 완전 튜토리얼
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: C#에서 교차 행 색상 적용 – 단계별 가이드
url: /ko/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 교차 행 색상 적용 – 전체 튜토리얼

데이터 기반 워크시트에 **교차 행 색상**을 적용해야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다 — 대부분의 개발자는 테이블을 좀 더 친숙하게 보이게 만들고 싶을 때 이 문제에 부딪힙니다. 좋은 소식은? 몇 줄의 C# 코드만으로 **행 배경 색상**을 설정하고 **연한 노란색 배경**을 추가해, 가독성을 즉시 높여주는 깔끔한 그리드를 만들 수 있다는 것입니다.

이 튜토리얼에서는 `DataTable`을 메모리로 가져오는 단계부터 각 행에 은은한 노랑‑흰색 스트라이프를 입히는 과정까지 전체 흐름을 살펴봅니다. 끝까지 따라오시면 **행을 교차로 색칠**하는 방법을 자신 있게 사용할 수 있게 되고, 다른 색조나 동적 테마가 필요할 때 활용할 수 있는 몇 가지 변형도 확인할 수 있습니다.

## 준비물

본격적으로 시작하기 전에 다음 항목이 준비되어 있는지 확인하세요:

- .NET 6 이상을 타깃으로 하는 .NET 프로젝트 (코드는 .NET Framework 4.7+에서도 동작합니다).  
- 스타일 객체를 지원하는 스프레드시트 라이브러리 – 예시에서는 **Aspose.Cells**, **GemBox.Spreadsheet**, **ClosedXML** 등과 유사한 일반적인 `Workbook`/`Worksheet` API를 사용합니다.  
- `DataTable` 소스 – 데이터베이스 쿼리, CSV 가져오기, 혹은 메모리 컬렉션 등 어디서든 얻을 수 있습니다.  

스프레드시트 라이브러리 자체 외에 추가 NuGet 패키지는 필요하지 않습니다. Aspose.Cells를 사용한다면 네임스페이스는 `Aspose.Cells`; ClosedXML이라면 `ClosedXML.Excel`입니다. 상황에 맞게 `CreateStyle` 및 `ImportDataTable` 호출을 교체하면 됩니다.

## 1단계: DataTable 형태로 원본 데이터 가져오기

먼저 표시할 데이터를 확보합니다. 실제 애플리케이션에서는 보통 데이터베이스를 조회하지만, 여기서는 `GetData()`라는 헬퍼 메서드가 채워진 `DataTable`을 반환한다고 가정합니다.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **왜 중요한가:** `DataTable`은 나중에 교차 색상을 입힐 행과 열을 정의합니다. 테이블이 비어 있으면 스타일을 적용할 대상이 없으므로, 진행하기 전에 `Rows.Count` > 0 인지 항상 확인하세요.

### 팁
Entity Framework에서 데이터를 가져오는 경우 `SqlCommand` 실행 후 `DataTable.Load(reader)`를 사용하면 코드를 깔끔하게 유지하고 컬럼 정의를 수동으로 할 필요가 없습니다.

## 2단계: 각 행에 적용할 스타일을 보관할 배열 할당

다음으로 행 개수와 동일한 크기의 컨테이너가 필요합니다. 대부분의 스프레드시트 API는 스타일 배열을 import 메서드에 전달할 수 있으므로, 행 수에 정확히 맞는 `Style[]`를 생성합니다.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **설명:** 배열을 미리 할당하면 반복마다 새로운 스타일 객체를 재생성하지 않아도 되므로, 수천 행을 처리할 때 성능 향상에 도움이 됩니다.

## 3단계: 교차 행 색상 적용 (연한 노랑 / 흰색)

이제 핵심 단계인 **교차 행 색상 적용**을 수행합니다. 각 행을 순회하면서 워크북에서 새로운 스타일 인스턴스를 만들고, 행 인덱스에 따라 배경색을 설정합니다. 짝수 행은 연한 노랑으로 채우고, 홀수 행은 흰색으로 유지합니다.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### 왜 작동하는가
- **`rowIndex % 2 == 0`** 은 행이 짝수인지 확인합니다.  
- **`Color.LightYellow`** 은 데이터 테이블에 적합한 부드럽고 눈에 거슬리지 않는 색조를 제공합니다.  
- **`BackgroundType.Solid`** 은 셀 전체를 채워 **set row background color** 효과를 보장합니다.  

다른 색상을 원한다면 `Color.LightYellow`를 `Color.LightCyan` 등으로 교체하면 됩니다. 동일한 로직을 활용해 **행을 교차로 색칠**하는 기준을 상태 플래그 등 다른 조건으로 바꿀 수도 있습니다.

## 4단계: 준비된 스타일 배열과 함께 DataTable을 워크시트에 가져오기

마지막으로 모든 내용을 워크시트에 삽입합니다. 대부분의 라이브러리는 스타일 배열을 받는 `ImportDataTable` 오버로드를 제공하며, `true` 플래그는 열 헤더를 작성하도록 지시하고, `0, 0` 좌표는 좌상단 셀부터 시작함을 의미합니다.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **결과:** 워크시트에 깔끔한 **교차 행 색상** 패턴이 적용됩니다—짝수 행은 연한 노랑, 홀수 행은 흰색. 사용자는 눈을 크게 움직이지 않고도 그리드를 스캔할 수 있습니다.

### 예상 출력
결과 스프레드시트를 열면 다음과 같은 모습이 보일 것입니다:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

행 1, 3, 5… 은 **연한 노랑 배경**을, 행 2, 4, 6… 은 **흰색**을 유지합니다. 헤더 행(0번 행)은 별도로 커스터마이징하지 않는 한 기본 스타일을 사용합니다.

## 선택적 변형 및 예외 상황

### 1. 다른 색상 팔레트 사용
연한 노랑이 브랜드와 맞지 않을 경우 `Color.LightYellow`를 다른 `System.Drawing.Color` 로 교체하면 됩니다. 예를 들어 블루‑그레이 테마를 원한다면 다음과 같이 사용할 수 있습니다:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. 데이터 기반 동적 색상 적용
조건에 맞는 행을 강조하고 싶을 때(예: 재고 부족) 모듈로 연산과 사용자 정의 테스트를 결합합니다:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. 특정 열에만 스타일 적용
특정 열에만 **set row background color** 를 적용하려면 각 열마다 별도 스타일을 만들고, import 후 워크시트의 셀 범위 API를 사용해 할당합니다.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. 대용량 테이블 성능 팁
10,000행 이상을 처리할 때는 색상당 하나의 스타일 객체만 재사용하고, 배열에는 두 개의 공유 스타일에 대한 참조만 저장하도록 하면 메모리 사용량을 크게 줄일 수 있습니다.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## 전체 작동 예제

아래는 콘솔 앱에 바로 붙여넣을 수 있는 독립 실행형 프로그램 예시입니다. 가상의 `Workbook`/`Worksheet` API를 사용했으니, 실제 사용 중인 라이브러리 타입으로 교체하세요.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**출력:** `AlternatingRows.xlsx` 라는 파일이 생성되며, 각 행이 연한 노랑 채우기와 흰색을 교차로 적용해 눈에 편안한 테이블이 됩니다.

## 자주 묻는 질문

**Q: 이 방법이 Excel‑style 조건부 서식에도 적용되나요?**  
A: 네. 라이브러리가 조건부 규칙을 지원한다면 `MOD(ROW(),2)=0` 과 같은 규칙으로 동일 로직을 변환할 수 있습니다. 여기서 보여준 코드 기반 방식은 조건부 서식을 제공하지 않는 라이브러리에서도 보다 포터블하게 사용할 수 있습니다.

**Q: Excel 시트가 아니라 PDF 테이블에서 **행을 교차로 색칠** 해야 한다면 어떻게 하나요?**  
A: 대부분의 PDF 테이블 생성기(예: iTextSharp, PdfSharp)에서는 행마다 `BackgroundColor` 를 설정할 수 있습니다. 동일한 모듈로 연산을 적용하면 됩니다—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}