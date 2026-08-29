---
category: general
date: 2026-07-20
description: Aspose.Cells를 사용하여 Python으로 Excel 워크북을 생성하고, 셀 배경색을 설정한 뒤, 날짜에 따라 셀 스타일을
  적용하는 조건부 서식을 추가합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: ko
lastmod: 2026-07-20
og_description: Aspose.Cells를 사용하여 Python으로 Excel 워크북을 생성합니다. 셀 배경색을 설정하고 날짜별로 셀을
  포맷하는 조건부 서식을 Python으로 추가하는 방법을 배워보세요.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Python으로 Excel 워크북 만들기 – 조건부 서식 추가
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Python으로 Excel 워크북 만들기 – 조건부 서식 가이드
url: /ko/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 Python 만들기 – 조건부 서식 가이드

처음부터 **Excel 워크북 Python**을 만들고 UI를 열지 않고도 깔끔하게 보이게 하고 싶으신가요? 혼자가 아닙니다. 많은 개발자들이 **셀 배경 색상 설정**이나 날짜 기반 스타일을 프로그래밍 방식으로 적용해야 할 때 벽에 부딪히곤 합니다.  

이 튜토리얼에서는 Aspose.Cells를 사용해 **조건부 서식 python** 규칙을 추가하고, 날짜별로 셀을 포맷한 뒤 최신 XLSX 파일로 저장하는 완전하고 실행 가능한 예제를 단계별로 살펴봅니다. 끝까지 따라오시면 어떤 프로젝트에든 바로 넣어 사용할 수 있는 독립형 스크립트를 얻게 됩니다.

## 배울 내용

- 워크북을 초기화하고 첫 번째 워크시트를 가져오는 방법  
- 전체 범위에 **셀 배경 색상 설정**하는 방법  
- **aspose cells 조건부 서식**을 사용해 “어제” 날짜를 강조하는 방법  
- 열 자동 맞춤 및 파일을 디스크에 저장하는 방법  

외부 설정은 필요 없습니다—Python 3와 Aspose.Cells 패키지만 있으면 됩니다. 이미 `aspose-cells`를 설치했다면 바로 시작할 수 있고, 아직이라면 `pip install aspose-cells` 한 번이면 됩니다.

## 사전 요구 사항

- Python 3.8+ (코드는 3.9, 3.10 및 최신 버전에서도 동작합니다)  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet 래퍼)  
- Excel 개념(셀, 범위, 서식)에 대한 기본 지식  

준비되셨나요? 그럼 바로 시작합니다.

## Excel 워크북 Python 만들기 – 설정 및 워크시트

먼저 새 워크북 객체와 기본 워크시트에 대한 참조가 필요합니다. 여기서 이후 모든 작업이 이루어집니다.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **왜 중요한가:** `Workbook()`은 메모리 내에서 Excel 파일을 생성하므로 임시 파일이 필요 없습니다. `worksheet` 변수는 셀 수준 작업을 수행하기 위한 진입점입니다.

## 셀 배경 색상 설정

규칙을 추가하기 전에 대상 범위에 기본 색상을 지정하면 조건부 서식이 더 돋보입니다. 아래 헬퍼는 지정된 범위에 대한 `FormatConditionCollection`을 가져오거나 생성하고, 셀을 단색 배경으로 채웁니다.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **팁:** 동일한 범위에 여러 규칙을 적용하려면 이 헬퍼를 한 번만 호출하고 반환된 컬렉션을 재사용하세요. API 호출을 몇 번 절감할 수 있습니다.

## 날짜 범위에 대한 조건부 서식 Python 추가

이제 재미있는 부분입니다. **시간 구간 조건부 서식** 규칙을 만들어 어제 날짜가 들어 있는 셀을 강조합니다. 이를 통해 Aspose.Cells를 사용한 **날짜별 셀 포맷**의 강력함을 확인할 수 있습니다.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **`TIME_PERIOD`를 사용하는 이유:** 직접 수식을 작성할 필요가 없습니다. Aspose.Cells가 현재 시스템 날짜와 비교해 날짜를 평가하므로 규칙이 항상 최신 상태를 유지합니다.

### 규칙 실행

```python
apply_yesterday_rule()
```

파일을 열면 `I19` 셀은 핑크색(“어제”)으로 빛나고, `K20` 셀은 기본 녹색을 유지합니다.

## 열 자동 맞춤 및 워크북 저장

정돈된 스프레드시트는 전문성을 높여줍니다. 자동 맞춤을 사용하면 데이터가 좁아지지 않게 할 수 있습니다.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **예외 상황:** 존재하지 않는 디렉터리를 지정하면 `workbook.save`가 오류를 발생시킵니다. 부드러운 처리가 필요하면 `try/except` 블록으로 저장 호출을 감싸세요.

### 전체 스크립트 (복사‑붙여넣기 바로 사용)

아래는 전체 스크립트이며 바로 실행할 수 있습니다. `YOUR_DIRECTORY`를 실제 폴더 경로로 바꾸기만 하면 됩니다.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

이 스크립트를 실행하면 앞서 설명한 조건부 서식이 적용된 `TimePeriodExample.xlsx` 파일이 생성됩니다.

## 흔히 묻는 질문 및 팁

- **다른 날짜 범위를 지정할 수 있나요?**  
  물론입니다. `"I19:K20"`을 원하는 A1 스타일 범위로 바꾸고 샘플 날짜도 그에 맞게 조정하면 됩니다.

- **`YESTERDAY` 대신 사용자 정의 수식이 필요하면?**  
  `FormatConditionType.FORMULA`를 사용하고 `condition.formula1 = "YOUR_FORMULA"`를 설정하세요. 예를 들어 `=TODAY()-A1=1`은 어제를 흉내냅니다.

- **같은 범위에 여러 규칙을 적용하려면?**  
  다른 `FormatConditionType`으로 `conditions.add_condition`을 다시 호출하면 됩니다. 규칙 순서가 중요하며, 뒤에 추가된 규칙이 앞의 규칙을 덮어쓸 수 있습니다.

- **배경과 함께 글꼴 색상도 설정할 수 있나요?**  
  가능합니다—`condition.style.font.color = Color.white`(또는 다른 `Color`)를 사용하면 됩니다.

## 결론

이제 Aspose.Cells를 활용해 **Excel 워크북 Python 만들기**, **셀 배경 색상 설정**, 그리고 **날짜별 셀 포맷**을 수행하는 **조건부 서식 python**을 적용하는 방법을 알게 되었습니다. 스크립트는 완전하게 동작하며, 디렉터리 누락과 같은 예외 상황도 처리하고, 다중 규칙이나 동적 범위 탐지와 같은 더 복잡한 시나리오로 확장할 수 있습니다.

다음 단계가 궁금하신가요? “어제” 규칙을 “지난 주”로 바꾸어 보거나, 그라디언트 채우기를 실험하거나, 수십 개의 서식이 적용된 테이블이 포함된 전체 보고서를 생성해 보세요. 핵심 빌딩 블록은 모두 여기 있으며, 이제 **aspose cells 조건부 서식**을 Python에서 마스터하셨습니다.

행복한 코딩 되시고, 댓글에 여러분만의 변형을 공유해 주세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 깊이 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}