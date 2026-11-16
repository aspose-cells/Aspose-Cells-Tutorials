---
category: general
date: 2026-11-16
description: Python을 사용하여 Excel에서 조건부 서식을 만들기. 조건부 서식 범위를 추가하고, 날짜를 강조 표시하며, 프로그래밍
  방식으로 워크북을 구축하는 방법을 배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: ko
lastmod: 2026-11-16
og_description: Python을 사용하여 Excel에서 조건부 서식을 만들기. 이 튜토리얼에서는 조건부 서식 범위를 추가하고, 날짜를 강조
  표시하며, 워크북을 생성하는 방법을 보여줍니다.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Python으로 Excel에서 조건부 서식 만들기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Python을 사용하여 Excel에서 조건부 서식 만들기
url: /ko/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 Excel에서 조건부 서식 만들기

Python으로 작업하면서 Excel 파일에 **조건부 서식**을 **만들어야** 할 경우, 이 가이드는 정확한 방법을 보여줍니다. **create excel workbook python** 스타일로 워크북을 만들고, 서식 범위를 정의하며, IDE를 떠나지 않고 날짜를 강조 표시하는 방법을 배웁니다.

조건부 서식은 특정 기준을 만족하는 셀을 시각적으로 표시해 주어 대시보드, 보고서, 데이터 검증 시트에 이상적입니다. 이 튜토리얼을 마치면 “Yesterday”(어제) 날짜가 있는 셀은 핑크색으로, 나머지 범위는 녹색으로 표시되는 완전한 워크북을 얻게 됩니다.

## 이번 튜토리얼에서 달성할 내용

* 처음부터 새 워크북을 구축합니다.  
* 특정 셀 블록에 대한 조건부 서식 컬렉션을 추가합니다.  
* 날짜를 강조하는 **TIME_PERIOD** 규칙을 적용합니다(“날짜 강조” 시나리오).  
* 다운스트림 처리를 위해 XLSX 워크북으로 파일을 저장합니다.

**Prerequisites**  
* Python 3.8+  
* `aspose-cells` Python 패키지 (`pip install aspose-cells`)  
* Python `datetime` 모듈에 대한 기본 지식  

---

## Python에서 조건부 서식 만들기

첫 번째 단계는 서식 규칙을 호스팅할 워크북과 워크시트를 설정하는 것입니다.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Why this matters** – `Workbook`은 모든 Excel 작업의 진입점입니다. 워크북을 프로그래밍 방식으로 생성하면 수동 “File → New” 단계를 대체하여 자동화된 보고 파이프라인을 구현할 수 있습니다.

---

## 조건부 서식 컬렉션 준비 – 조건부 서식 범위 추가

다음으로 규칙이 적용될 셀 블록을 정의합니다. 이 예시에서는 범위가 **I19:K20**입니다.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explanation** – `conditional_formattings.add`는 주소 문자열에 연결된 새로운 컬렉션을 등록합니다. 첫 번째 조건(`conds[0]`)은 “기본” 스타일 역할을 하며, 이후 규칙이 조건을 만족하면 이를 덮어씁니다.

---

## TIME_PERIOD 조건 추가 – 날짜 강조하기

이제 실제 로직을 추가해 “Yesterday”(어제) 날짜를 식별하고 핑크색으로 색칠합니다.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Why use TIME_PERIOD?** – Aspose.Cells는 `YESTERDAY`, `TODAY`, `LAST_WEEK`와 같은 내장 열거형을 제공합니다. 이 열거형은 셀의 날짜 값을 현재 시스템 날짜와 비교해 평가하므로 사용자 정의 수식이 필요 없습니다.

---

## 샘플 데이터 채우기 – 규칙 시연

서식이 적용되는 모습을 확인하려면 규칙에 맞는 날짜와 맞지 않는 날짜를 삽입합니다.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Edge case note** – `TIME_PERIOD` 규칙은 *실제* 날짜에만 적용됩니다. 셀에 텍스트(예: “N/A”)가 들어 있으면 규칙이 무시되어 예기치 않은 색상 변경을 방지합니다.

---

## 워크북 저장 – add conditional formatting python

마지막으로 워크북을 디스크에 기록합니다. 파일은 모든 스프레드시트 프로그램에서 열어 색상을 확인할 수 있습니다.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Expected result**  

| I19 (녹색 → 핑크) | J19 (녹색) | K19 (녹색) |
|--------------------|------------|------------|
| 7/30/2008 (어제) | – | – |
| **I20**: “어제” 라벨 | – | – |
| I21‑K21 (녹색) | – | – |

셀 **I19**는 날짜가 “Yesterday”(어제) 기간과 일치하므로 핑크색 배경으로 표시되고, **K20**은 녹색 상태를 유지합니다.

---

## 흔히 묻는 질문 및 실용 팁

* **내장 기간 대신 사용자 정의 날짜 범위를 사용할 수 있나요?**  
  예. `condition.time_period` 대신 `condition.formula1 = "TODAY()-1"`을 사용하고 `condition.type = FormatConditionType.FORMULA`로 설정합니다.

* **워크북에 이미 데이터가 존재한다면?**  
  조건부 서식 컬렉션을 추가하기 전에 `worksheet.cells.import_data`를 사용해 데이터를 대량 로드합니다.

* **대용량 시트에서 성능은 어떨까요?**  
  많은 조건을 추가하면 렌더링이 느려질 수 있습니다. 동일한 규칙을 적용할 셀을 하나의 범위(예: “A1:C1000”)로 묶어 조건 수를 최소화하세요.

* **다중 플랫폼 호환성은 보장되나요?**  
  생성된 XLSX 파일은 Office Open XML 표준을 따르므로 Windows, macOS, Linux의 스프레드시트 애플리케이션에서 모두 작동합니다.

---

## 결론

이제 Python을 사용해 Excel 워크북에 **조건부 서식**을 **만드는** 방법을 알게 되었습니다. 워크북 생성, **add conditional formatting range** 정의, **날짜 강조** 규칙 적용, 파일 저장까지 모두 Aspose.Cells가 제공하는 **add conditional formatting python** 접근 방식으로 수행했습니다.

다음 단계로 할 수 있는 일:

* `TimePeriodType` 값(`TODAY`, `LAST_MONTH` 등)을 추가해 규칙 세트를 확장합니다.  
* 동일 범위에 여러 조건을 결합해 시각적 효과를 풍부하게 합니다.  
* 이 워크플로를 자동 보고 파이프라인이나 웹 서비스에 통합합니다.

코딩을 즐기시고, 보고 요구에 맞게 다양한 색상, 범위, 날짜 로직을 실험해 보세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색하는 데 도움이 됩니다.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}