---
category: general
date: 2026-10-26
description: C#에서 WRAPCOLS를 사용해 범위를 열로 나누고, WRAPROWS를 적용해 행을 처리하며, 워크북을 프로그래밍 방식으로
  XLSX 파일로 저장하는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: ko
lastmod: 2026-10-26
og_description: C#에서 WRAPCOLS를 사용해 데이터를 열로 나누고, WRAPROWS를 사용해 행으로 나눈 뒤 워크북을 XLSX 형식으로
  저장하는 방법. 전체 단계별 가이드를 따라보세요.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: C#에서 WRAPCOLS 사용 방법 – 범위 나누기 및 XLSX로 저장
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#에서 WRAPCOLS를 사용하는 방법 및 워크북을 XLSX로 저장하기
url: /ko/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 WRAPCOLS 사용 방법 및 워크북을 XLSX로 저장하기

Excel 파일에서 데이터를 재구성하기 위해 **WRAPCOLS 사용 방법**이 필요하다면, 이 가이드는 완전하고 실행 가능한 솔루션을 보여줍니다. **excel wrapcols 예제**를 확인하고, **WRAPROWS**로 **범위를 행으로 나누는 방법**을 배우며, 마지막으로 **워크북을 XLSX로 저장**하는 과정을 **프로그램matically**하게 진행합니다.

C#에서 Excel을 다루는 것은 일반적으로 워크북을 생성하고, 수식을 적용한 뒤 파일을 저장하는 과정을 의미합니다. 아래 코드는 Microsoft Office가 설치되지 않아도 Excel 파일을 조작할 수 있는 Aspose.Cells 라이브러리를 사용합니다. 이 튜토리얼을 마치면 **excel 워크북을 프로그래밍으로 생성**하고, 데이터를 가로와 세로 모두에서 분할하며, 다운스트림 처리에 사용할 수 있는 깔끔한 `.xlsx` 파일을 만들 수 있게 됩니다.

## 사전 요구 사항

시작하기 전에 다음을 준비하세요:

* .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 동작합니다)
* **Aspose.Cells** NuGet 패키지에 대한 참조  
  ```bash
  dotnet add package Aspose.Cells
  ```
* C#와 Excel 수식에 대한 기본 지식

## 단계 1: WRAPCOLS를 사용해 범위를 열로 나누기

**WRAPCOLS** 함수는 1차원 범위를 받아 지정된 열 수만큼 값을 퍼뜨립니다. 이 예제에서는 `A1:A10`에 있는 값을 세 개의 열로 만들도록 WRAPCOLS에 요청합니다.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **결과:** 셀 `C1:E4`에 원래의 10개 항목이 세 열로 배열됩니다 (마지막 열에 남은 항목이 들어갑니다).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## 단계 2: WRAPROWS로 범위를 행으로 나누기

**WRAPCOLS**가 가로 방향으로 작동한다면, **WRAPROWS**는 반대로 동작합니다: 지정된 행 수만큼 범위를 퍼뜨립니다. 여기서는 `B1:B10`의 값을 `F1`부터 시작하는 두 행에 배치합니다.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **결과:** 수식이 셀 `F1:K2`에 10개의 값을 두 행에 걸쳐 채웁니다.

## 단계 3: 워크북을 XLSX로 저장하기

수식을 적용한 뒤 마지막 단계는 파일을 영구 저장하는 것입니다. **save workbook as xlsx** 작업은 메모리 상의 워크북을 최신 OpenXML 형식으로 디스크에 기록합니다.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### 저장된 파일 모습

`wrapcols_wraprows_output.xlsx` 파일을 Excel에서 열면 다음과 같이 표시됩니다:

| C | D | E |
|---|---|---|
| 항목 1 | 항목 4 | 항목 7 |
| 항목 2 | 항목 5 | 항목 8 |
| 항목 3 | 항목 6 | 항목 9 |
|        |        | 항목 10 |

그리고

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| 값 1 | 값 3 | 값 5 | 값 7 | 값 9 | |
| 값 2 | 값 4 | 값 6 | 값 8 | 값 10 | |

수식은 셀에 그대로 남아 있어, 원본 범위가 변경되면 자동으로 반영됩니다.

## 단계 4: 일반적인 변형 및 엣지 케이스

### 열 또는 행 수 변경하기

* **열을 더 늘리기:** `WRAPCOLS`의 두 번째 인수를 증가시킵니다.  
  예시: `=WRAPCOLS(A1:A10,5)`는 다섯 열을 만들고, 데이터가 부족한 셀은 빈 상태로 남깁니다.
* **동적 열 수:** 하드코딩된 숫자 대신 셀 참조를 사용합니다.  
  `=WRAPCOLS(A1:A10, G1)` 여기서 `G1`은 원하는 열 수를 포함합니다.

### 빈 셀 또는 비숫자 셀 처리

WRAPCOLS와 WRAPROWS는 기본적으로 빈 셀을 무시하지만, 비어 있지 않은 값의 순서는 유지합니다. 빈 셀까지 보존하려면 WRAPCOLS 적용 전에 `IFERROR` 또는 `TEXT` 함수로 원본 범위를 감싸세요.

### 다른 형식으로 저장하기

이 튜토리얼은 **save workbook as xlsx**에 초점을 맞추지만, Aspose.Cells는 다양한 형식(`.xls`, `.csv`, `.pdf` 등)을 지원합니다:

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## 전문가 팁 및 주의사항

* **전문가 팁:** 수식을 저장 직후 바로 평가하려면 `Workbook.Settings.CalcEngineEnabled = true`를 설정하세요.
* **주의할 점:** 큰 원본 범위는 매우 큰 스필 영역을 만들 수 있어 성능에 영향을 줄 수 있습니다. 범위 크기를 제한하거나 작업을 여러 워크시트로 나누세요.
* **스레드 안전성:** Aspose.Cells 객체는 **스레드‑안전하지** 않습니다. 병렬 처리 시 스레드당 별도의 `Workbook` 인스턴스를 생성하세요.

## 결론

이제 **WRAPCOLS 사용 방법**을 통해 세로 범위를 여러 열로 나누고, **WRAPROWS**로 행으로 나누며, 변환 후 **워크북을 XLSX로 저장**하는 전체 흐름을 알게 되었습니다. 위 단계를 따라 하면 **excel 워크북을 프로그래밍으로 생성**, 강력한 스필 수식을 적용하고, 수동 작업 없이 바로 공유 가능한 Excel 파일을 만들 수 있습니다.

### 다음 단계는?

* **조건부 서식**을 활용해 스필된 데이터를 강조하기
* **WRAPCOLS**와 **SORT**, **FILTER**를 결합해 동적 대시보드 만들기
* Aspose.Cells의 **차트 API**를 사용해 코드에서 바로 재배열된 데이터를 시각화하기

코딩을 즐기시고, Excel 워크플로우 자동화를 만끽하세요!


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 한 연관 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}