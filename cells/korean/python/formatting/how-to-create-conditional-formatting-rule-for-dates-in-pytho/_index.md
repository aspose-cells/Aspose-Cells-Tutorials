---
category: general
date: 2026-08-24
description: Aspose.Cells를 사용하여 Python에서 날짜를 강조 표시하는 조건부 서식 규칙을 만들고, 열 자동 맞춤 및 배경
  색상 서식을 적용합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: ko
lastmod: 2026-08-24
og_description: Aspose.Cells를 사용하여 Python에서 조건부 서식 규칙을 만들고, 몇 줄의 코드만으로 날짜를 강조하고 배경
  색을 설정하며 열을 자동 맞춤하는 방법을 배워보세요.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Python에서 날짜에 대한 조건부 서식 규칙 만들기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Python에서 날짜에 대한 조건부 서식 규칙 만들기
url: /ko/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 날짜에 대한 조건부 서식 규칙 만들기

날짜에 반응하는 **조건부 서식 규칙**을 만들어야 할 때, 이 가이드는 Aspose.Cells for Python을 사용해 정확히 어떻게 하는지 보여줍니다. 보고서 대시보드든 자동화된 스프레드시트든, 어제 날짜를 강조하고, 사용자 정의 배경색을 적용하며, **열 자동 맞춤**을 통해 결과를 깔끔하게 만드는 방법을 확인할 수 있습니다.

이 튜토리얼에서는 **날짜 기반 조건부 서식**, **배경색 조건부 서식**을 시연하고, 마지막으로 워크북을 XLSX 파일로 저장하는 과정을 다룹니다. 끝까지 진행하면 필요한 **날짜 기반 조건부 서식**을 언제든 재사용할 수 있는 헬퍼를 얻게 됩니다.

## 배울 내용

* Aspose.Cells를 사용해 워크북과 워크시트를 설정합니다.
* 任意의 셀 범위에 **날짜 기반 조건부 서식**을 추가하는 헬퍼 함수를 작성합니다.
* 규칙이 평가될 수 있도록 샘플 날짜를 셀에 채웁니다.
* **열 자동 맞춤**을 적용해 내용이 읽기 쉽도록 합니다.
* 워크북을 저장하고 강조된 셀을 확인합니다.

필수 조건은 `aspose-cells` 패키지가 설치된 Python 환경만 있으면 됩니다.

## 사전 요구 사항

| 요구 사항 | 세부 정보 |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Excel 기본 개념에 대한 이해 | 워크시트, 셀, 서식 |
| 선택 사항: IDE (VS Code, PyCharm 등) | Python 스크립트를 실행할 수 있는 편집기 |

## 1단계: 워크북을 만들고 첫 번째 워크시트를 가져오기

첫 번째 단계는 **조건부 서식 규칙**을 적용할 준비가 된 객체, 즉 `Workbook`과 기본 `Worksheet`를 **생성**하는 것입니다. 이 객체들이 이후 모든 작업의 진입점이 됩니다.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*왜 중요한가:* `Workbook`은 전체 Excel 파일을 보관하고, `Worksheet`는 셀, 스타일, **날짜 기반 조건부 서식**을 적용하는 장소입니다. 이 객체가 없으면 나머지 코드는 작동할 수 없습니다.

## 2단계: TIME_PERIOD 조건부 서식을 추가하는 헬퍼 만들기

각 범위마다 동일한 보일러플레이트 코드를 반복하는 대신, 로직을 헬퍼 함수에 캡슐화합니다. 이 함수는 `TimePeriodType`(예: Yesterday, Today, LastWeek)에 따라 셀 색상을 지정하는 **배경색 조건부 서식**을 연결합니다.

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*헬퍼를 사용하는 이유:* **날짜 기반 조건부 서식** 로직을 분리함으로써 코드 가독성, 테스트 용이성, 여러 시트나 프로젝트에서의 재사용성을 높입니다.

## 3단계: 특정 범위에 조건부 서식 규칙 적용하기

이제 헬퍼를 사용해 “Yesterday”(어제) 날짜가 들어 있는 셀을 강조합니다. 이것이 **조건부 서식 규칙 만들기** 작업의 핵심입니다.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

워크북을 열면 `I19:K20` 범위 내에서 날짜가 어제와 일치하는 셀은 핑크색 채우기로 표시됩니다(헬퍼에서 설정한 스타일). `bg_color` 인자는 필요에 따라 기본 배경색을 조건부 색상 뒤에 겹쳐 놓을 수 있음을 보여줍니다.

## 4단계: 샘플 날짜로 범위 채우기

조건부 규칙은 워크시트에 조건을 만족하는 데이터가 있어야만 보입니다. 여기서는 “Yesterday”(어제)와 일치하는 날짜 하나와, 기간 외의 날짜 하나를 삽입합니다.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*왜 중요한가:* `datetime` 객체를 사용하면 Excel이 값을 실제 날짜로 인식하게 되며, 이는 **날짜 기반 조건부 서식**이 올바르게 동작하는 데 필수입니다. 숫자 형식(`30`)은 셀을 인식 가능한 날짜 형태로 표시하도록 보장합니다.

## 5단계: 열 자동 맞춤 및 워크북 저장

데이터와 서식이 적용된 후 마지막 마무리는 **열 자동 맞춤**을 통해 날짜가 완전히 보이도록 열 너비를 조정하는 것입니다. 그 다음 파일을 디스크에 기록합니다.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

`auto_fit_column` 호출은 12번째 열(Excel에서는 **L** 열에 해당)에서 가장 긴 내용을 검사하고, 그에 맞게 너비를 확장합니다. 이 작은 단계 덕분에 날짜가 잘려 보이지 않으며 **배경색 조건부 서식**이 명확히 드러납니다.

### 예상 결과

`TimePeriodDemo.out.xlsx` 파일을 열면 다음과 같이 표시됩니다:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (핑크색 강조) | Yesterday | 03‑Aug‑2008 (강조 없음) |

* 어제 날짜가 들어 있는 셀은 **조건부 서식 규칙 만들기**가 `YESTERDAY` 기간과 일치했기 때문에 핑크색 배경으로 표시됩니다.
* 다른 셀은 기본 배경(또는 제공한 `medium_sea_green`)을 유지합니다.
* L 열이 자동으로 넓어져 날짜가 완전히 읽히게 됩니다.

## 일반적인 변형 및 엣지 케이스

| 상황 | 코드 적용 방법 |
|-----------|-----------------------|
| **“Yesterday” 대신 “Today” 강조** | `TimePeriodType.YESTERDAY`를 `TimePeriodType.TODAY`로 교체 |
| **다른 배경색 사용** | `condition.style.background_color = Color.pink`를 원하는 다른 `Color`(예: `Color.light_sky_blue`)로 변경 |
| **비연속 범위에 규칙 적용** | 서로 다른 `cell_range` 문자열(예: `"A1:A10", "C1:C10"`)을 사용해 `add_time_period_condition`을 여러 번 호출 |
| **기존 워크북과 작업** | 새 워크북을 만들 대신 `Workbook("myfile.xlsx")`로 파일을 로드 |
| **같은 범위에 여러 날짜 기반 조건 추가** | 첫 번째 `add_time_period_condition` 호출 뒤에 `conditions.add_condition(FormatConditionType.TIME_PERIOD)`를 사용해 다른 `time_period`를 설정 |

## 결론

이제 **날짜에 반응하는 조건부 서식 규칙**을 만들고, **배경색 조건부 서식**을 적용하며, Aspose.Cells for Python을 이용해 **열 자동 맞춤**까지 수행하는 방법을 알게 되었습니다. 헬퍼 함수를 통해 로직을 추상화했으므로 “Yesterday”, “LastWeek”, 혹은 사용자 정의 기간 등 어떤 **날짜 기반 조건부 서식** 시나리오에도 동일한 패턴을 재사용할 수 있습니다.

다음 단계로 살펴볼 내용:

* 날짜 규칙과 함께 **아이콘 집합**이나 **데이터 막대** 추가
* 데이터베이스에서 날짜를 가져와 동적 보고서 생성
* 단일 시트에 여러 **날짜 기반 조건부 서식** 규칙 결합

다양한 색상, 기간, 범위를 실험해 보면서 프로젝트에 맞게 적용해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 관련 주제를 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}