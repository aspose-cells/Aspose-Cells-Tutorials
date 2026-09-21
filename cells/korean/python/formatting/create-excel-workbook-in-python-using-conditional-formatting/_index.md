---
category: general
date: 2026-09-21
description: Python에서 Excel 워크북을 만드는 방법, 셀 배경색을 설정하는 방법, 그리고 Aspose.Cells를 사용한 날짜
  기반 조건부 서식 적용 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: ko
lastmod: 2026-09-21
og_description: Python에서 Excel 워크북을 만들고, 셀 배경색을 설정하며, Aspose.Cells를 사용하여 날짜 기반 조건부
  서식을 적용합니다. 단계별 가이드를 따라하세요.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Python으로 조건부 서식을 적용한 Excel 워크북 만들기
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: 조건부 서식을 사용하여 Python으로 Excel 워크북 만들기
url: /ko/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 조건부 서식을 사용하여 Excel 워크북 만들기

날짜를 자동으로 강조 표시하는 **create Excel workbook python** 스크립트가 필요하다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. **set cell background color** 방법, “Yesterday” 규칙 추가, 파일 저장까지 모두 Aspose.Cells for Python으로 수행합니다.

프로그래밍 방식으로 Excel 파일을 다루면 많은 시트에 동일한 서식 로직을 반복해야 하는 경우가 많습니다. 이 튜토리얼을 마치면 **excel conditional formatting python**에 대한 재사용 가능한 패턴을 얻어 어떤 프로젝트에도 적용할 수 있습니다.

## 사전 요구 사항

- Python 3.8+ 설치  
- `aspose-cells` 패키지 (`pip install aspose-cells`)  
- Python 함수와 datetime 모듈에 대한 기본적인 이해  

추가 라이브러리는 필요하지 않으며, Aspose.Cells가 모든 Excel 작업을 처리합니다.

## 단계 1: 워크북 생성 및 첫 번째 워크시트 접근

첫 번째 단계는 **create excel workbook python** 객체를 생성하고 기본 워크시트를 가져오는 것입니다. 이를 통해 이후 스타일링을 위한 깨끗한 캔버스를 얻을 수 있습니다.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*왜 중요한가:* `Workbook()`은 메모리 내 Excel 파일을 생성합니다. `worksheets[0]`에 접근하면 시트 이름을 하드코딩하지 않아도 되며 기본 이름이 변경되어도 작동합니다.

## 단계 2: TIME_PERIOD 조건부 서식 추가 도우미

코드를 깔끔하게 유지하기 위해 조건부 서식 생성을 도우미 함수로 감쌉니다. 이 함수는 셀 범위, 배경 색상, 원하는 시간 기간 규칙을 매개변수로 받습니다.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*왜 중요한가:* 도우미는 조건부 서식 생성의 반복적인 단계를 추상화하여 “Today” 또는 “Last Week”와 같은 다른 날짜 기반 규칙에 쉽게 재사용할 수 있게 합니다.

## 단계 3: 범위에 “Yesterday” 규칙 적용

이제 도우미를 사용하여 어제 날짜가 들어 있는 셀을 강조합니다. 조건이 충족되면 범위 `I19:K20`이 **medium sea green** 색으로 변합니다.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*왜 중요한가:* `TimePeriodType.YESTERDAY`는 Aspose.Cells의 내장 열거형에 포함되어 있어 날짜를 수동으로 계산할 필요가 없습니다. 라이브러리는 워크북이 열릴 때마다 규칙을 평가합니다.

## 단계 4: 샘플 날짜로 범위 채우기

규칙이 작동하는 모습을 확인하기 위해 두 개의 날짜를 기록합니다—하나는 “Yesterday”와 일치하고, 다른 하나는 일치하지 않습니다. `number` 스타일 `30`은 내장 날짜 형식에 해당합니다.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*왜 중요한가:* 구체적인 날짜를 삽입함으로써 특정 날짜에 파일을 열 필요 없이 조건부 서식이 정상 작동하는지 확인할 수 있습니다.

## 단계 5: 설명 레이블 추가 및 열 자동 맞춤

작은 레이블은 서식이 적용된 범위의 목적을 명확히 하고, `auto_fit_column`은 시트를 읽기 쉽게 만듭니다.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## 단계 6: 워크북 저장

마지막으로 워크북을 디스크에 저장합니다. `os.makedirs` 호출은 대상 폴더가 존재하도록 보장합니다.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

*TimePeriodDemo.xlsx* 파일을 열면 다음과 같이 표시됩니다:

- 셀 **I19**가 **medium sea green** 색으로 채워집니다. 값이 “Yesterday” 규칙과 일치하기 때문입니다.  
- 셀 **K20**은 기본 배경을 유지합니다. 날짜가 조건을 만족하지 않기 때문입니다.  

이는 Python 코드 한 줄로 **format cells by date**를 구현한 예시입니다.

## 전체 실행 가능한 예제

모든 부분을 합치면, 복사‑붙여넣기하여 실행할 수 있는 전체 스크립트는 다음과 같습니다:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

스크립트를 실행하고 결과 파일을 열면 조건부 서식이 적용된 것을 확인할 수 있습니다.

## 일반적인 변형 및 엣지 케이스

| 변형 | 구현 방법 | 사용 시점 |
|-----------|------------------|-------------|
| **Highlight “Today”** | `TimePeriodType.YESTERDAY`를 `TimePeriodType.TODAY`로 교체 | 실시간 대시보드 |
| **Multiple ranges** | `add_time_period`를 각 범위에 대해 호출하고 서로 다른 색상을 전달 | 복잡한 보고서 |
| **Dynamic date range** | `TimePeriodType.LAST_7_DAYS` 또는 `TimePeriodType.NEXT_MONTH` 사용 | 롤링 보고서 |
| **Custom color** | `Color.from_argb(255, r, g, b)`를 사용하여 원하는 색조 생성 | 브랜드 일관성 스타일링 |

**Pro tip:** 단색 채우기를 원한다면 항상 `condition.style.pattern = BackgroundType.SOLID`를 설정하세요; 그렇지 않으면 Excel이 버전마다 일관되지 않은 그라데이션을 표시할 수 있습니다.

## 결론

이제 Aspose.Cells를 사용하여 **create Excel workbook python** 스크립트로 **set cell background color**를 설정하고, **excel conditional formatting python**을 적용하며, **format cells by date**를 수행하는 방법을 알게 되었습니다. 예제는 **date based conditional formatting** 시나리오를 다루지만, 동일한 패턴을 모든 시간 기간 규칙에 적용할 수 있습니다.

다음으로, 다음을 탐색해 볼 수 있습니다:

- 데이터 바 또는 아이콘 세트 추가 (`FormatConditionType.DATA_BAR`)  
- 같은 범위에 여러 조건부 규칙 결합  
- 보고서를 위해 워크북을 PDF(`SaveFormat.PDF`)로 내보내기  

다양한 색상, 범위 및 시간 기간 유형을 실험하여 특정 보고 요구에 맞게 조정해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Aspose.Cells for .NET로 Excel 셀 서식 및 워크북 관리 마스터](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Aspose.Cells .NET로 Excel 자동화: 워크북 생성 및 외부 링크 설정](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Aspose.Cells .NET를 사용하여 Excel에서 워크북 범위 지정된 명명된 범위 만들기](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}