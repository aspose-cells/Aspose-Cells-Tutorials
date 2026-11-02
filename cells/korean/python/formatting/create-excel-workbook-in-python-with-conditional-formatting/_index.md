---
category: general
date: 2026-09-05
description: Python으로 Excel 워크북을 만들고 어제 셀을 강조하는 조건부 서식을 추가하세요. 전체 코드를 배우고 각 단계가 왜
  중요한지 알아보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: ko
lastmod: 2026-09-05
og_description: Python으로 Excel 워크북을 만들고 어제 셀을 강조하는 조건부 서식을 추가하세요. 완전한 솔루션을 위한 단계별
  가이드를 따라보세요.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Python으로 Excel 워크북 만들기 – 조건부 서식 추가
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Python에서 조건부 서식을 사용하여 Excel 워크북 만들기
url: /ko/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 조건부 서식으로 Excel 워크북 만들기

보고 작업을 위해 **create Excel workbook python**이 필요하다면, 이 가이드는 워크북을 생성하고 어제 날짜를 강조하는 조건부 서식 규칙을 적용하는 방법을 보여줍니다. 정확한 코드와 각 줄이 존재하는 이유, 그리고 다른 날짜 범위에 솔루션을 적용하는 방법을 확인할 수 있습니다.

조건부 서식은 특정 조건을 만족하는 데이터에 주의를 끌어올리는 강력한 방법입니다. 이 튜토리얼에서는 Microsoft Office 없이도 전체 Excel 기능을 지원하는 Python via .NET용 Aspose.Cells 라이브러리를 사용합니다. 가이드를 끝낼 때쯤 *I19:K20* 범위의 셀들이 어제 날짜를 포함하면 분홍색으로 표시되는 파일을 얻게 됩니다.

## 사전 요구 사항

* Python 3.9+ 설치
* `aspose-cells` 패키지 (`pip install aspose-cells` 로 설치)
* Python 구문에 대한 기본적인 이해
* 워크북이 저장될 디렉터리에 대한 쓰기 권한

.NET 런타임이 사용 가능한 한, 코드는 Windows, macOS, Linux 모두에서 작동합니다.

## Python에서 Excel 워크북 만들기

첫 번째 단계는 `Workbook` 객체를 인스턴스화하고 기본 워크시트를 가져오는 것입니다. 이 객체는 메모리상의 전체 Excel 파일을 나타냅니다.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters*: `Workbook()`은 단일 워크시트가 포함된 빈 워크북을 생성합니다. `worksheets[0]`에 접근하면 이후 데이터, 스타일 및 서식을 추가할 수 있는 핸들을 얻습니다.

## 조건부 서식 범위 추가

다음으로 조건부 규칙이 평가할 영역을 정의합니다. `I19:K20` 범위는 두 행에 걸쳐 총 여섯 개 셀을 포함합니다.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Why this matters*: 특정 범위에 조건부 서식 컬렉션을 추가하면 규칙이 격리되어 관련 없는 셀에 영향을 주지 않게 됩니다. 이는 **add conditional formatting range** 요구 사항을 충족합니다.

## 규칙 정의: 날짜를 기준으로 셀 강조

이제 `TIME_PERIOD` 유형의 조건을 생성합니다. 이는 Excel에 각 셀의 값을 미리 정의된 시간 창과 비교하도록 지시합니다.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Why this matters*: `TIME_PERIOD`는 “Yesterday”, “Today”, “Last Week” 등을 직접 지원하는 유일한 내장 유형입니다. `condition.time_period`를 `YESTERDAY`로 설정하면 규칙이 자동으로 각 셀의 날짜 값을 현재 날짜의 전날과 비교합니다.

## 조건을 만족하는 셀 스타일 지정

조건부 서식에는 시각적 스타일도 필요합니다. 여기서는 일치하는 셀을 돋보이게 하기 위해 분홍색 단색 채우기를 선택합니다.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Why this matters*: 스타일 객체는 Excel이 조건을 만족하는 셀을 어떻게 렌더링할지 정의합니다. 단색 분홍색 채우기를 사용하면 **highlight cells based on date** 요구 사항을 충족하고 결과를 쉽게 확인할 수 있습니다.

## 평가를 위한 샘플 날짜 채우기

규칙이 작동하는 모습을 확인하기 위해 두 개의 날짜를 삽입합니다—하나는 어제 날짜이고 다른 하나는 그렇지 않습니다. `number` 형식 `30`은 내장 날짜 형식 `mm-dd-yy`에 해당합니다.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Why this matters*: 일치하는 날짜와 일치하지 않는 날짜를 모두 제공하면 조건부 서식이 올바르게 작동하는지 확인할 수 있습니다. 스크립트를 실행할 때 날짜를 현재 월에 맞게 조정하거나 동적 값으로 교체하세요.

## 워크북 저장

마지막으로 파일을 디스크에 씁니다. `SaveFormat.XLSX` 상수는 출력이 최신 Excel 파일임을 보장합니다.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Why this matters*: 워크북을 저장하면 Excel, LibreOffice 또는 XLSX를 지원하는 모든 뷰어에서 열 수 있습니다. 출력된 경로는 파일이 저장된 위치를 확인시켜 줍니다.

## 전체 스크립트

모든 요소를 합치면, 완전하고 실행 가능한 스크립트는 다음과 같습니다:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 예상 출력

`TimePeriodExample.xlsx`를 열면:

* 셀 **I19**는 값이 어제와 일치하므로 분홍색 배경으로 표시됩니다.
* 셀 **K20**은 날짜가 기간 외이므로 기본 배경을 유지합니다.
* 레이블 **“Yesterday”**는 명확성을 위해 셀 I20에 배치됩니다.

## 일반적인 변형 및 엣지 케이스

| Situation | Adjustment |
|-----------|------------|
| **어제 대신 오늘을 강조** | `condition.time_period = TimePeriodType.TODAY`를 변경합니다. |
| **규칙을 더 큰 영역에 적용** | `add("I19:K20")`의 범위 문자열을 `"A1:Z100"`와 같이 업데이트합니다. |
| **다른 채우기 색상 사용** | `DrawingColor.pink`를 다른 `DrawingColor`(예: `DrawingColor.light_green`)로 교체합니다. |
| **동적 날짜 사용** | 어제 날짜를 구하기 위해 `datetime.now() - timedelta(days=1)`를 계산하고, 규칙을 적용하기 전에 해당 값을 셀에 기록합니다. |

**Pro tip:** 여러 사용자에게 프로그램matically 워크북을 생성할 때, 조건부 서식 정의를 데이터 삽입과 분리해 두세요. 이렇게 하면 코드를 중복하지 않고 여러 시트에서 동일한 스타일을 재사용할 수 있습니다.

## 프로그래밍 방식으로 결과 확인 (옵션)

Excel을 열지 않고 서식을 확인하려면, 저장 후 셀의 스타일을 검사할 수 있습니다.



## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}