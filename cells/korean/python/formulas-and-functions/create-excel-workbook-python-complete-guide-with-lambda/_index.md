---
category: general
date: 2026-06-08
description: Excel 워크북을 Python으로 생성하는 예시로, Excel에서 람다를 사용하는 방법, BYROW를 이용한 행 합계, 그리고
  몇 단계만으로 계산을 자동화하는 방법을 보여줍니다.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: ko
og_description: Python으로 Excel 워크북을 만들고, BYROW 수식을 사용해 람다를 활용하여 행을 효율적으로 합산하는 방법을
  배워보세요.
og_title: Python으로 Excel 워크북 만들기 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Python으로 Excel 워크북 만들기 – 람다와 함께하는 완전 가이드
url: /ko/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 Python 만들기 – Lambda를 활용한 완전 가이드

Ever wondered how to **create Excel workbook Python** scripts that automate boring number‑crunching? You're not alone—many developers hit a wall when they need to generate a sheet, drop a formula in, and pull the results back into their code.

이번 튜토리얼에서는 Excel에서 **how to use lambda** 를 보여주고, 최신 `BYROW` 함수를 사용한 **how to sum rows** 를 설명하며, 오늘 바로 복사‑붙여넣기 해서 실행할 수 있는 깔끔한 엔드‑투‑엔드 예제를 제공합니다.

## 배울 내용

- Python만으로 Excel을 수동으로 열지 않고 새 워크북을 설정합니다.  
- 3 × 3 숫자 행렬로 범위를 채웁니다.  
- 각 행을 합산하기 위해 **use lambda excel** 구문을 활용한 `BYROW` 수식을 삽입합니다.  
- 시트를 재계산하여 수식이 평가되도록 하고, 결과를 다시 Python으로 읽어옵니다.  

이 가이드를 마치면 인보이스, 점수표 또는 실시간으로 **sum rows** 가 필요할 때마다 적용할 수 있는 독립 실행형 스크립트를 얻게 됩니다.

### 사전 요구 사항

- Python 3.8+이 설치되어 있어야 합니다.  
- `openpyxl` 라이브러리(`xlwings`를 선호한다면 COM 기반 접근 방식도 가능). 여기서는 순수 Python이며 모든 플랫폼에서 동작하는 `openpyxl`을 사용합니다.  
- `BYROW` 함수와 Lambda 수식을 지원하는 최신 Microsoft Excel(365 또는 2021) 버전이 필요합니다.  

Install the library with:

```bash
pip install openpyxl
```

> **Pro tip:** Windows에서 권한 문제가 발생하면 `python -m pip install --user openpyxl`을 사용하세요.

## Excel 워크북 Python 만들기 – 워크북 초기화

우리가 처음 해야 할 일은 메모리 내에만 존재하는 완전 새로운 워크북 객체를 만드는 것입니다. `openpyxl`을 사용하면 한 줄 코드로 가능합니다:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

`wb.active`를 사용하고 `Worksheets[0]`을 인덱싱하지 않는 이유는 무엇일까요? `openpyxl`은 활성 시트를 직접 노출하므로 더 명확하고 추가 리스트 조회를 피할 수 있습니다. 여러 시트를 다뤄야 할 경우 언제든 `wb.create_sheet(title="MySheet")`으로 추가할 수 있습니다.

## 워크시트에 데이터 채우기 – 간단한 3×3 행렬

다음으로, 작은 행렬을 시트에 채웁니다. 이는 고전적인 “각 행 합산” 예제를 반영하며 코드를 간결하게 유지합니다.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

`ws.append()`나 `ws.values`를 사용하지 않고 직접 루프를 도는 이유가 궁금할 수 있습니다. 명시적인 루프를 사용하면 시작 셀을 완전히 제어할 수 있고, 나중에 오프셋을 조정하기도 쉬워 헤더 행이나 열을 비워두고 싶을 때 유용합니다.

## Excel 수식에서 Lambda 사용 방법

Excel의 **use lambda excel** 기능을 사용하면 셀 안에 익명 함수를 직접 작성할 수 있습니다. 스프레드시트 엔진 안에 존재하는 Python의 `lambda`와 같은 개념이라고 생각하면 됩니다. 구문은 다음과 같습니다:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

`BYROW`와 결합하면 해당 lambda를 범위의 각 행에 적용하여 결과 열을 생성할 수 있습니다. 이것이 우리의 **how to sum rows** 트릭의 핵심입니다.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

What’s happening under the hood?

- `A1:C3`은 소스 범위(우리 행렬)입니다.  
- `LAMBDA(r, SUM(r))`는 단일 행(`r`)을 받아 그 합을 반환하는 임시 함수를 정의합니다.  
- `BYROW`는 **각 행**에 대해 해당 lambda를 실행하고 결과를 D열에, `D1`부터 채워 넣습니다.  

`BYROW`는 *동적 배열* 함수이므로 Excel이 자동으로 `D1:D3`에 세 개의 합을 채웁니다.

> **Note:** `BYROW`와 Lambda 수식은 Excel 365/2021 이후 버전에서만 사용할 수 있습니다. 이전 버전을 사용 중이라면 기존 `SUM` 수식이나 VBA로 대체해야 합니다.

## BYROW와 Lambda를 활용한 행 합산 방법

이제 수식이 시트에 존재하므로 Excel에 계산을 수행하도록 알려야 합니다. `openpyxl` 자체는 수식을 계산하지 않으며, 읽고 쓰기만 합니다. 계산을 트리거하려면 다음 중 하나를 선택할 수 있습니다:

1. 워크북을 저장하고 Excel에서 열어 수동으로 계산합니다.  
2. `xlwings` COM 엔진을 사용해 강제 재계산합니다(Excel이 설치되어 있어야 함).

순수 Python 솔루션을 위해 계산 단계에만 `xlwings`를 사용하고, 그 외에는 아무것도 사용하지 않을 것입니다.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

`wb.calculate()`를 호출하지 않는 이유는 무엇일까요? `openpyxl`에는 자체 엔진이 없으므로 `xlwings`를 통해 Excel에 의존합니다. 작은 시트에서는 오버헤드가 최소이며 Excel이 표시하는 정확한 결과를 얻을 수 있습니다.

## 재계산 및 결과 가져오기 – 합계를 Python으로 다시 가져오기

마지막으로, D열에 흩어진 결과를 읽어옵니다. `openpyxl`을 사용하면 매우 간단합니다:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

`openpyxl`만 사용하고 싶다면 Excel 재계산 후 셀을 읽을 수 있습니다:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

두 방법 모두 동일한 리스트 `[6, 15, 24]`를 반환하며, `BYROW` + Lambda를 사용한 **how to sum rows**가 기대대로 동작함을 확인시켜 줍니다.

## 엣지 케이스 및 흔히 발생하는 실수

| 상황 | 주의할 점 | 해결 방법 |
|-----------|-------------------|-----|
| Excel 버전이 365보다 오래된 경우 | `BYROW`와 `LAMBDA`가 `#NAME?` 오류로 표시됨 | 전통적인 `=SUM(A1:C1)`을 수동으로 복사하거나 Excel을 업그레이드하세요. |
| 대형 행렬(10 k+ 행) | 재계산이 느려질 수 있음 | `book.api.CalculateFullRebuild()`를 한 번만 호출하거나 워크북을 분할하세요. |
| Excel 없이 헤드리스 서버에서 실행 | `xlwings`가 Excel을 실행할 수 없음 | 계산을 위해 `pandas` + `numpy`와 같은 순수 Python 라이브러리로 전환한 뒤 결과를 기록하세요. |
| 지역 설정 문제(쉼표 vs 세미콜론) | 수식이 거부될 수 있음 | `;`를 사용하는 로케일에서는 `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"`를 사용하세요. |

## 전체 작업 예제 (복사‑붙여넣기 준비 완료)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells Java로 Excel 워크북 만들기 - 완전 가이드](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Aspose.Cells로 Excel 워크북 만들기 및 보고서 자동화](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [.NET용 Aspose.Cells를 사용해 Excel 워크북을 ODS로 만들고 저장하는 방법](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}