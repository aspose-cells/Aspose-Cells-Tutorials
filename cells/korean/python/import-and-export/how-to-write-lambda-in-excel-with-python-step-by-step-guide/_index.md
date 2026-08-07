---
category: general
date: 2026-06-21
description: Python을 사용하여 Excel에서 람다를 작성하는 방법을 배웁니다. 이 튜토리얼에서는 Python으로 Excel 워크북을
  생성하는 방법과 Aspose.Cells를 사용해 셀을 읽는 방법도 다룹니다.
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: ko
og_description: Python을 사용해 Excel에서 람다 함수를 작성하는 방법을 설명합니다. Excel 워크북을 Python으로 만들고,
  BYROW를 적용하며, 셀 결과를 읽는 명확한 단계들을 따라보세요.
og_title: Python을 사용하여 Excel에서 람다 작성하는 방법 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: Python으로 Excel에서 람다 작성 방법 – 단계별 가이드
url: /ko/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Write Lambda in Excel with Python – Step‑by‑Step Guide

Excel 수식을 Python으로 자동화할 때 **람다를 어떻게 작성하는지** 궁금하셨나요? 혼자가 아닙니다. 많은 개발자들이 Excel의 최신 동적 배열 함수와 Python 기반 워크플로를 결합하려다 막히곤 합니다. 이 튜토리얼에서는 완전하고 실행 가능한 예제를 통해 정확히 어떻게 하는지 단계별로 보여드리며, **create excel workbook python**, **how to read cells**, 그리고 편리한 **how to use byrow** 패턴도 함께 다룹니다.

이 가이드를 끝까지 읽으면 새 워크북, 람다를 활용한 BYROW 수식, 그리고 결과를 Python 스크립트로 다시 가져오는 간단한 방법을 얻게 됩니다. 별도의 Excel 애드인 없이 Aspose.Cells for Python과 약간의 코드만 있으면 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Python 3.8 이상
- `aspose-cells` 패키지 (`pip install aspose-cells`)
- Python 리스트와 함수에 대한 기본 이해
- (선택) 익숙한 IDE 또는 텍스트 편집기

이것만 있으면 됩니다. 익숙하지 않은 부분이 있다면 먼저 패키지를 설치하고 진행하세요; 나머지 단계는 Python이 실행되는 모든 플랫폼에서 동작합니다.

## Create Excel Workbook Python

먼저 깨끗한 워크북 객체가 필요합니다. Aspose.Cells는 메모리 상의 전체 Excel 파일을 나타내는 `Workbook` 클래스를 제공합니다.

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

왜 새 워크북부터 시작하나요? 숨겨진 수식이나 남은 서식 없이 결정적인 환경을 보장하기 위해서입니다. 이것이 모든 **create excel workbook python** 튜토리얼의 기반이 됩니다.

## Fill the Worksheet with Data

다음으로 **A1** 셀부터 시작하는 5 × 3 숫자 테이블을 채웁니다. 데이터는 수학을 명확히 확인할 수 있도록 의도적으로 단순합니다.

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

`put_value`에 중첩된 Python 리스트를 사용하면 Aspose.Cells가 자동으로 행과 열을 매핑합니다. CSV나 데이터베이스에서 데이터를 가져와야 한다면 `table_data`만 해당 소스로 교체하면 됩니다—다른 부분은 변경되지 않습니다.

## How to Write Lambda in BYROW Formula (Python)

이제 핵심 부분: Excel 엔진이 평가할 **람다를 어떻게 작성하는지**입니다. Excel의 `BYROW` 함수는 지정된 범위의 각 행을 순회하면서 사용자가 제공한 `LAMBDA`에 행을 전달합니다. 여기서는 각 행의 평균을 구하고자 합니다.

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

구성 요소를 살펴보면:

- `BYROW(A1:C5, …)`는 A1:C5 범위의 모든 행을 대상으로 함을 의미합니다.
- `LAMBDA(r, AVERAGE(r))`는 익명 함수(`r`은 행 배열)로, 해당 행의 평균을 반환합니다.
- 결과는 자동으로 D1:D5에 넘쳐서 표시됩니다—BYROW가 배열을 반환하기 때문입니다.

이 한 줄이 **how to write lambda**에 대한 행별 계산 답변입니다. `AVERAGE`를 `SUM`, `MAX` 등 다른 집계 함수로 바꾸면 됩니다—람다 본문만 교체하면 됩니다.

## Force Calculation of the Formula

Aspose.Cells는 수식을 설정할 때 자동으로 계산하지 않으므로, 재계산을 명시적으로 요청해야 합니다.

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

이 단계를 건너뛰면 D 열 셀에 수식 텍스트만 남고 실제 계산된 값은 표시되지 않습니다. 이는 **how to use byrow**를 사용할 때 흔히 발생하는 실수입니다.

## How to Read Cells After Calculation

마지막으로 결과를 Python으로 다시 가져옵니다. 이는 **how to read cells**을 모든 수식 출력에 대해 작동하도록 보여주는 예시입니다.

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

간단한 리스트 컴프리헨션이 다섯 행을 순회하면서 각 셀의 `.value`를 가져와 `row_averages`에 저장합니다. 출력된 리스트를 보면 람다가 정확히 의도대로 동작했음을 확인할 수 있습니다.

### Pro tip
많은 결과 블록을 읽어야 할 경우 `worksheet.cells.get_range("D1:D5").value`를 사용해 한 번에 전체 배열을 가져오면 대규모 시트에서 훨씬 빠릅니다.

## Use Lambda Function Excel for Row Averages (Full Script)

전체 흐름을 하나로 합친 완전 실행 스크립트는 다음과 같습니다:

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

스크립트를 실행하면 다음이 출력됩니다:

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

이것이 전체 라이프사이클입니다: **create excel workbook python**, 데이터 채우기, **how to use byrow**, **how to write lambda**, 그리고 마지막으로 **how to read cells**.

## Edge Cases & Common Questions

- **데이터가 연속되지 않을 경우는?**  
  BYROW는 직사각형 범위에서 동작합니다. 빈칸이 있더라도 더 큰 범위를 지정하고 람다에서 빈 셀을 무시하도록 하면 됩니다 (`AVERAGEIF(r, "<>")`).

- **람다에 인자를 하나 이상 전달할 수 있나요?**  
  가능합니다. 첫 번째 인자는 항상 행(`BYROW`) 또는 열(`BYCOL`)이며, 추가 인자는 범위 뒤에 나열합니다. 예: `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`.

- **구버전 Excel에서도 사용 가능한가요?**  
  BYROW와 LAMBDA는 Excel 365(동적 배열)부터 지원됩니다. 레거시 지원이 필요하면 VBA나 보조 열을 이용해 로직을 직접 구현해야 합니다.

- **워크북을 디스크에 저장해야 하나요?**  
  이번 데모에서는 필요 없지만 물리 파일이 필요하면 `workbook.save("output.xlsx")`를 호출하면 됩니다.

## Conclusion

Python에서 Excel BYROW 수식에 **람다를 어떻게 작성하는지**를 다루고, 전체 **create excel workbook python** 워크플로를 시연했으며, 계산 후 **how to read cells**하는 가장 간단한 방법을 보여드렸습니다. Aspose.Cells를 활용하면 COM 인터옵 문제 없이 작업할 수 있고, 동일 패턴을 수천 행에 걸쳐 최소한의 코드 변경으로 확장할 수 있습니다.

다음 도전 과제가 준비되셨나요? `AVERAGE`를 `MEDIAN`으로 바꾸거나, 람다 안에 조건 로직을 추가하거나, 전체 보고서 덱을 자동으로 생성해 보세요. Python과 Excel 최신 함수의 조합은 데이터 기반 자동화의 새로운 가능성을 열어줍니다.

질문이 있거나 자신만의 람다 팁을 공유하고 싶다면 아래 댓글을 남겨 주세요. 즐거운 코딩 되세요!  

![how to write lambda in Excel using Python](image.png){alt="Excel에서 Python을 사용하여 람다 작성 방법"}

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 데 도움이 되는 연관 주제들을 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Load an Excel Workbook Without Defined Names Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}