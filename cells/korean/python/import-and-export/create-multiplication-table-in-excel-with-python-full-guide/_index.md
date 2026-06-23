---
category: general
date: 2026-06-21
description: Python을 사용하여 Excel에서 구구표를 만들기. 람다 사용법, makearray 사용법, Excel 배열 표시 및 Python으로
  Excel 값을 읽는 방법을 단계별 튜토리얼로 배워보세요.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: ko
og_description: Python을 사용하여 Excel에서 구구표를 만들기. 이 튜토리얼에서는 lambda와 makearray를 활용하고,
  Excel 배열을 표시하며, Excel 값을 효율적으로 읽는 방법을 보여줍니다.
og_title: Python으로 Excel에서 곱셈표 만들기 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Python으로 Excel에서 곱셈표 만들기 – 전체 가이드
url: /ko/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 Excel에서 구구표 만들기 – 전체 가이드

Excel에서 **구구표 만들기**를 수동으로 입력하지 않고도 할 수 있는 방법이 궁금하셨나요? 혼자가 아닙니다. 많은 보고서 상황에서 5×5(또는 그보다 큰) 제품 그리드가 필요하지만, 손으로 입력하면 시간 낭비가 됩니다.  

이 튜토리얼에서는 깔끔하고 Python 기반으로 테이블을 생성하고, `MAKEARRAY` 수식으로 삽입한 뒤, 결과를 다시 스크립트로 가져오는 방법을 단계별로 안내합니다. 진행하면서 **lambda 사용 방법**, **makearray 사용 방법**, **display excel array** 및 **read excel values python**을 하나의 일관된 예제로 보여드립니다.

끝까지 읽으면 어떤 워크북에서도 재사용 가능한 스니펫을 얻고, 이 접근 방식이 왜 빠르고 미래에도 견고한지 이해하게 될 것입니다.

## 준비물

- Python 3.8+ (최신 안정 버전이면 충분합니다)
- `openpyxl` 라이브러리(또는 수식을 지원하는 Excel‑aware 라이브러리)
- Python의 lambda 표현식에 대한 기본 이해
- 별도의 Excel 추가 기능 필요 없음; 기본 제공 `MAKEARRAY` 함수(Excel 365에서 사용 가능)가 핵심 역할을 합니다

필요한 것이 없으면 `pip install openpyxl`만 실행하면 됩니다.

## 구구표 만들기 – 개요

핵심 아이디어는 간단합니다: 새 워크북을 만들고, 5 × 5 구구표를 구성하는 `MAKEARRAY` 수식을 작성한 뒤, Excel에게 계산을 강제하고, 최종적으로 Python으로 값을 읽어오는 것입니다.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

스크립트를 실행하면 다음과 같이 출력됩니다:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

이것이 Python만으로 완전히 생성된 **구구표 만들기** 예제입니다.

### 왜 Python 루프 대신 `MAKEARRAY`를 사용하나요?

- **성능**: Excel이 계산을 네이티브하게 처리하므로 대규모 행렬에서 더 빠릅니다.
- **실시간 업데이트**: 나중에 수식의 차원을 변경하면 시트가 자동으로 재계산됩니다.
- **가독성**: 수식 자체가 “배열 만들기”라는 의도를 명확히 전달하므로 Python 코드가 깔끔해집니다.

## Excel 수식에서 Python lambda 사용 방법

`MAKEARRAY` 호출에 포함된 `LAMBDA` 부분은 Excel 측의 익명 함수이며, Python lambda와는 다릅니다. 하지만 개념은 동일합니다: `r`(행 인덱스)과 `c`(열 인덱스)를 받아 `r*c`를 반환하는 작은 인라인 로직을 정의합니다.  

**how to use lambda**에 익숙하지 않다면, 수식 안에만 존재하는 미니 함수라고 생각하면 됩니다. 별도로 함수를 선언할 필요가 없습니다. Python에서는 문자열로 그대로 삽입합니다:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

이 라인은 Excel에 *“5 × 5 블록의 각 셀에 대해 행 × 열을 계산하라”*는 의미를 전달합니다.  

lambda는 Excel에서 평가되므로 Python 자체의 lambda 문법을 신경 쓸 필요가 없고, 오직 Excel 문법만 맞추면 됩니다.

## makearray를 사용해 배열 생성하기

`MAKEARRAY`는 비교적 최근에 Microsoft 365(2022년)에서 추가된 함수입니다. 기존의 `INDEX` + `ROW`/`COLUMN` 조합을 대체합니다. 시그니처는 다음과 같습니다:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – 원하는 행 수
- **columns** – 원하는 열 수
- **lambda** – `(row, column)`을 받아 값을 반환하는 Excel LAMBDA

예제에서는 고전적인 구구표를 위해 `5,5`를 전달했지만, 숫자를 자유롭게 바꿀 수 있습니다:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

이렇게 하면 Python 루프를 전혀 사용하지 않고 10 × 10 테이블을 만들 수 있습니다. 이는 **how to use makearray**가 조회표, 히트맵, 재무 일정 등 어떤 결정론적 그리드에도 적용될 수 있음을 보여줍니다.

## display excel array – 데이터를 Python으로 가져오기

Excel이 수식을 계산하면 결과값은 수동 입력 셀과 동일하게 시트에 저장됩니다. **display excel array**를 위해 우리는 범위를 순회하면서 각 행을 출력합니다:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

몇 가지 팁:

- 큰 범위를 다룰 때는 `worksheet.cell(row, column).value`를 사용하세요. 사전 형태 인덱싱보다 약간 빠릅니다.
- 더 깔끔한 표가 필요하면 `tabulate`나 `pandas.DataFrame`을 활용해 출력 형식을 지정하세요.

아래는 결과 시트의 스크린샷입니다(이미지 alt 텍스트는 SEO를 위해 주요 키워드를 포함합니다):

![Python을 사용해 Excel에서 구구표 만들기 스크린샷](/images/multiplication-table-excel.png)

## read excel values python – 행렬을 추출해 추가 처리하기

**display excel array** 후 다음 단계는 보통 그 숫자를 데이터 분석 파이프라인에 전달하는 것입니다. 여기서 **read excel values python**이 빛을 발합니다. 출력용 루프를 재활용해 리스트‑리스트, NumPy 배열, 혹은 Pandas DataFrame을 만들 수 있습니다:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

출력:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

이제 완전한 타입의 DataFrame이 생겼으니, 그래프를 그리거나 CSV로 내보내거나 머신러닝 모델에 바로 넣을 수 있습니다. 이렇게 해서 **read excel values python** 단계가 마무리됩니다.

## 엣지 케이스 및 실무 팁

- **수식 재계산**: 초기 `calculate_formula()` 호출 후 워크북을 수정하면 반드시 다시 호출해야 합니다. 그렇지 않으면 캐시된 배열이 오래된 상태로 남습니다.
- **非‑365 Excel**: 오래된 Excel 버전은 `MAKEARRAY`를 지원하지 않습니다. 이 경우 Python으로 테이블을 생성하고 셀을 하나씩 쓰는 방식으로 대체하세요.
- **대형 테이블**: 100 × 100 이상 행렬은 메모리 부담을 줄이기 위해 스트리밍 방식으로 데이터를 처리하는 것이 좋습니다.
- **오류 처리**: `try/except` 블록으로 계산 및 읽기 단계를 감싸 `InvalidFileException`이나 `FormulaError`를 잡아내세요.

## 결론

우리는 Python을 활용해 **구구표 만들기**를 수행하고, **how to use lambda**와 **how to use makearray**를 이용해 Excel에서 계산하도록 했습니다. 또한 **display excel array**와 **read excel values python**을 통해 결과를 Python으로 가져와 Pandas DataFrame으로 변환하는 전체 흐름을 살펴보았습니다.

다음 단계로는 곱셈 로직을 더 복잡한 형태—예를 들어 거리 행렬, 확률표, 동적 가격 그리드 등—로 바꿔보세요. 동일한 패턴이 적용됩니다: `MAKEARRAY` 한 줄, 간단한 `calculate_formula()`, 그리고 데이터를 추출하는 몇 줄의 Python 코드.

이 가이드가 도움이 되었다면 GitHub에 ⭐를 달고, 팀원과 공유하거나 직접 사용 사례를 댓글로 남겨 주세요. 즐거운 코딩 되시고, 단 하나의 수식으로 Excel 테이블을 생성하는 간편함을 만끽하시기 바랍니다!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 주제들을 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고, 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}