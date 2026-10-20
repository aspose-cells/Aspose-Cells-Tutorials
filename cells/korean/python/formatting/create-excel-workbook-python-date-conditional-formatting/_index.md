---
category: general
date: 2026-08-08
description: Python으로 Excel 워크북을 생성하고 날짜를 기준으로 조건부 서식을 추가합니다. 어제 셀을 강조 표시하는 Aspose.Cells
  사용 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: ko
lastmod: 2026-08-08
og_description: Aspose.Cells를 사용하여 Python으로 Excel 워크북을 만들고 날짜를 기준으로 조건부 서식을 적용해 동적
  스프레드시트를 구현합니다.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Python으로 Excel 워크북 만들기 – 날짜 조건부 서식
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Excel 워크북 만들기 Python 날짜 조건부 서식
url: /ko/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 Excel 워크북 만들기 및 날짜 조건부 서식

특정 날짜와 일치하는 셀을 자동으로 강조 표시해야 할 경우, **create Excel workbook Python**을(를) 수행하고 이 튜토리얼에서 정확히 방법을 보여줍니다. **conditional formatting based on date**를 적용하여 어제 날짜가 핑크색으로 표시되도록 Aspose.Cells 라이브러리를 사용합니다.

이 가이드는 SDK 설치부터 최종 .xlsx 파일 저장까지 모든 단계를 자세히 안내하므로, 작업 예제를 복사‑붙여넣기하여 자체 프로젝트에 바로 사용할 수 있습니다. 외부 문서는 필요 없으며, 모든 코드와 설명이 자체적으로 포함되어 있습니다.

## 전제 조건

* Python 3.8 이상이 설치되어 있어야 합니다.
* `aspose-cells` 패키지(Aspose.Cells용 Python 래퍼). 다음으로 설치합니다:
  ```bash
  pip install aspose-cells
  ```
* 워크시트 및 셀 스타일과 같은 Python 및 Excel 개념에 대한 기본적인 이해.

> **Pro tip:** Aspose.Cells는 Microsoft Excel이 설치되지 않아도 작동하므로 서버‑사이드 자동화에 이상적입니다.

## 단계 1: Python에서 Excel 워크북 만들기

첫 번째 작업은 새 워크북을 인스턴스화하고 기본 워크시트를 가져오는 것입니다. 이 객체는 전체 Excel 파일을 나타내며 행, 열 및 서식 API에 접근할 수 있게 합니다.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

워크북을 만드는 것은 데이터, 수식 또는 서식 규칙을 추가하든, 이후 모든 조작의 기반이 됩니다.

## 단계 2: 날짜 기반 조건부 서식 정의

이제 **conditional formatting based on date**를 추가합니다. `FormatConditionType.TIME_PERIOD` 열거형을 사용하면 Yesterday, Today, LastWeek와 같은 내장 시간 기간을 지정할 수 있습니다.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

이 단계가 중요한 이유: Excel은 범위 내 각 셀에 대해 조건을 평가합니다. 셀 값이 정의된 기간(어제)에 해당하면, 우리가 지정한 스타일이 자동으로 적용됩니다.

## 단계 3: 샘플 날짜로 범위 채우기

규칙이 적용되는 모습을 확인하려면, 대상 셀에 몇 개의 `datetime` 객체를 기록합니다. 그 중 하나는 워크북 내부 날짜 시스템을 기준으로 어제 날짜로 의도적으로 설정됩니다.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

`number = 30` 라인은 Excel에 표준 짧은 날짜 형식으로 값을 표시하도록 지시합니다. 다른 표시 형식을 원한다면 이 인덱스를 다른 내장 숫자 형식으로 변경할 수 있습니다.

## 단계 4: 가독성을 위한 열 너비 조정

날짜가 들어 있는 열을 자동 맞춤하면, 특히 Excel이나 뷰어에서 워크북을 열 때 출력이 더 읽기 쉬워집니다.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## 단계 5: 워크북을 디스크에 저장

마지막으로 워크북을 .xlsx 파일로 저장합니다. `"YOUR_DIRECTORY"`를 실제 경로로 교체하세요.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

`TimePeriodDemo.out.xlsx`를 Excel에서 열면, 셀 **I19**는 값이 “Yesterday” 규칙과 일치하므로 핑크 배경으로 표시되고, **K20**은 변경되지 않은 상태로 남습니다.

### 예상 출력

| I19 (날짜) | I20 (라벨) | J19 | J20 | K19 | K20 (날짜) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (핑크 배경) | Yesterday | – | – | – | *2008‑08‑03* (서식 없음) |

핑크 색상은 **conditional formatting based on date**가 의도대로 작동함을 확인시켜 줍니다.

## 일반적인 변형 및 엣지 케이스

| 상황 | 코드 적용 방법 |
|-----------|-----------------------|
| **“Yesterday” 대신 “Today” 강조** | Change `condition.time_period = TimePeriodType.TODAY` |
| **전체 열에 규칙 적용** | Use `worksheet.get_range("A:A").format_conditions` |
| **사용자 정의 날짜 범위 사용 (예: 최근 7일)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **다른 배경 색상** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **디스플레이 없이 Linux에서 실행** | Aspose.Cells는 완전 무인(headless) 모드이며, 추가 설정이 필요하지 않습니다. |

## 전체 실행 가능한 예제

아래는 출력 디렉터리를 업데이트한 후 그대로 실행할 수 있는 전체 스크립트입니다. 모든 import, 주석 및 오류 처리 기본 사항이 포함되어 있습니다.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

스크립트를 실행하면 “Yesterday” 셀이 자동으로 강조된 Excel 파일이 생성되어, **create Excel workbook Python**과 **conditional formatting based on date**가 결합된 모습을 보여줍니다.

## 결론

이제 **create Excel workbook Python** 객체를 만들고, **date‑based conditional formatting**을 정의하는 방법을 알게 되었습니다.

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Java에서 Aspose.Cells를 사용하여 Excel 워크북 만들기: 단계별 가이드](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells .NET을 사용하여 차트가 포함된 Excel 워크북 만들기 | 단계별 가이드](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel 자동화: Aspose.Cells for .NET을 사용하여 워크북 만들고 ListBox 추가](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}