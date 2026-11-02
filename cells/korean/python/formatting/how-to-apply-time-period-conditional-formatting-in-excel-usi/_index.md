---
category: general
date: 2026-09-15
description: Python에서 Aspose.Cells를 사용하여 시간 구간 조건부 서식을 적용하고 워크북을 XLSX로 저장하는 방법을 배웁니다.
  단계별 코드가 포함되어 있습니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: ko
lastmod: 2026-09-15
og_description: Python을 사용하여 Excel에서 기간별 조건부 서식을 적용하고 워크북을 XLSX 형식으로 저장하세요. Aspose.Cells에
  대한 전체 가이드를 확인하십시오.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Python을 사용하여 Excel에서 기간별 조건부 서식 적용
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Python을 사용해 Excel에서 기간 조건부 서식을 적용하는 방법
url: /ko/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python을 사용하여 Excel에서 시간 기간 조건부 서식을 적용하는 방법

If you need **time period conditional formatting** in an Excel file, this tutorial shows you exactly how to do it with Python. You’ll see a complete, runnable example that creates a workbook, highlights yesterday’s dates, and **save workbook as XLSX** in just a few lines of code.

Conditional formatting is a powerful way to draw attention to data that meets a specific rule. In this guide we focus on the “Yesterday” time period, but the same pattern works for other built‑in periods such as Today, LastWeek, and NextMonth. By the end of the tutorial you will be able to **how to create excel workbook python**‑style scripts that are ready for production.

## 사전 요구 사항

- Python 3.8+ 설치  
- `aspose-cells` 및 `aspose-pydrawing` 패키지 (`pip install aspose-cells aspose-pydrawing`)  
- Python 구문에 대한 기본적인 이해  

Aspose.Cells가 파일 생성을 내부적으로 처리하므로 추가적인 Office 설치가 필요하지 않습니다.

## Python에서 Aspose.Cells를 사용한 시간 기간 조건부 서식

This section walks through every line of code needed for the primary task. The code block below is the full script; comments explain the purpose of each step.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### 각 단계가 중요한 이유

1. **Creating the workbook**은 Excel을 열지 않고도 조작할 수 있는 메모리 내 Excel 파일을 제공합니다.  
2. **Defining the range** (`I19:K20`)는 규칙이 적용되는 위치를 Aspose.Cells에 알려주어 로직을 분리합니다.  
3. **Adding a TIME_PERIOD condition**은 Aspose의 내장 열거형 `TimePeriodType.YESTERDAY`를 사용합니다. 이를 통해 수동 날짜 계산을 피하고 파일을 다른 날에 열었을 때 자동으로 업데이트됩니다.  
4. **Setting the style** (`background_color` 및 `pattern`)은 강조된 셀의 표시 방식을 결정합니다. `Color.pink`를 사용하면 규칙을 쉽게 식별할 수 있습니다.  
5. **Writing sample dates**에 번호 형식 30을 적용하면 Excel이 날짜를 일련 번호가 아닌 짧은 날짜 형식으로 표시합니다.  
6. **Auto‑fitting the column**은 나중에 파일을 여는 사람들의 가독성을 향상시킵니다.  
7. **Saving as XLSX**는 Excel, Google Sheets 또는 최신 스프레드시트 프로그램에서 열 수 있는 호환성이 높은 파일을 생성합니다.

## Aspose.Cells를 사용한 Python‑style Excel 워크북 생성 방법

The script above already demonstrates the minimal steps to **how to create excel workbook python**. In practice you may want to:

- 여러 워크시트 추가 (`workbook.worksheets.add("Report")`).  
- 루프 또는 pandas DataFrame(`worksheet.cells.import_data_table`)을 사용해 대규모 데이터 테이블 채우기.  
- `cell.get_style()`을 사용해 추가 서식(글꼴, 테두리) 적용.  

All of these actions follow the same pattern: obtain the object, modify its properties, and call `set_style` or `save`.

## Python에서 조건부 서식 추가 – 기타 유용한 패턴

Beyond the “Yesterday” example, Aspose.Cells supports several conditional‑formatting types:

| FormatConditionType | 일반적인 사용 사례 |
|---------------------|------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | 사용자 정의 수식 (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | 간단한 비교 (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | 그라디언트 색상 스케일 |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | 셀 내부 바 시각화 |

To **add conditional formatting python** for a numeric threshold, you would replace `FormatConditionType.TIME_PERIOD` with `FormatConditionType.CELL_VALUE` and set `condition.operator_type` and `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## XLSX로 워크북 저장 – 모범 사례

When you **save workbook as xlsx**, consider:

- 올바른 `SaveFormat`(`SaveFormat.XLSX`)을 지정하여 레거시 형식을 피합니다.  
- 스크립트가 루프에서 실행될 경우 결정적인 파일 이름 사용 (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- 장기 실행 서비스에서는 리소스를 해제(`workbook.dispose()`)하여 네이티브 메모리를 확보합니다.  

예제는 이미 `SaveFormat.XLSX`를 사용하고 있으며, 이는 모든 조건부 서식 규칙을 유지하는 최신 zip 기반 워크북을 생성합니다.

## Excel에서 어제 강조 – 검증 단계

After running the script, open `TimePeriodExample.xlsx`:

1. `I19`와 `K20` 셀에 각각 `30‑07‑2008` 및 `03‑08‑2008` 날짜가 들어 있습니다.  
2. `I20` 셀에 “Yesterday” 텍스트가 표시됩니다.  
3. 시스템 날짜를 **2008년 7월 30일**로 변경하고 파일을 다시 열면 일치하는 날짜가 있는 셀에 자동으로 핑크 색상이 채워집니다.  
4. 시스템 날짜를 다른 날로 변경하면 핑크 색상이 사라져 규칙이 **time period conditional formatting** 논리에 따라 작동함을 확인할 수 있습니다.

## 흔히 발생하는 실수와 회피 방법

- `aspose-pydrawing` 누락 – `Color` 클래스는 이 패키지에 포함되어 있습니다; 설치를 잊으면 `ImportError`가 발생합니다.  
- `Incorrect number format` – 기본 General 형식을 사용하면 일련 번호(예: 39822)가 표시됩니다. 짧은 날짜 형식으로 표시하려면 항상 `style.number = 30`을 설정하세요.  
- `Range mismatch` – 조건부 서식 범위에 강조하려는 셀이 포함되어야 하며, 그렇지 않으면 규칙이 적용되지 않습니다.

## 전문가 팁: 서식 루틴 재사용

If you need the same “Yesterday” rule in multiple workbooks, wrap the logic in a helper function:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Call `apply_yesterday_highlight(worksheet, "A1:A10")` wherever needed.

## 결론

This guide showed you how to implement **time period conditional formatting** in Excel using Python, how to **save workbook as XLSX**, and how to **highlight yesterday in Excel** with a single, reusable script. You now have a solid foundation to **add conditional formatting python** code to any automation project, whether you’re generating daily reports, building dashboards, or preparing data exports.

**Next steps**

- `TODAY` 또는 `LAST_WEEK`와 같은 다른 `TimePeriodType` 값을 탐색하세요.  
- 동일 범위에 여러 조건부 규칙을 결합하여 더 풍부한 시각적 힌트를 제공하세요.  
- 워크북 생성을 웹 서비스나 예약 작업에 통합하세요.

코딩을 즐기시고, 조건부 서식이 Excel 자동화에 제공하는 시각적 명확성을 만끽하세요!

## 다음에 배울 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells .NET을 사용한 Excel 조건부 서식 마스터: 종합 가이드](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Aspose.Cells .NET 마스터: Excel에서 교대 행에 조건부 서식 적용](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Aspose.Cells for .NET 및 C#를 사용한 Excel에서 사용자 정의 글꼴로 조건부 서식 마스터](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}