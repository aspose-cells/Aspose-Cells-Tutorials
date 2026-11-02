---
category: general
date: 2026-10-07
description: Python으로 Excel 워크북을 생성하고, 셀 배경색을 설정하며, 열 너비를 자동 맞춤하고, Excel에 날짜를 채우는
  간결한 코드 예제.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: ko
lastmod: 2026-10-07
og_description: Python으로 Excel 워크북을 만든 뒤 셀 배경색을 설정하고, 열을 자동 맞춤하며, Excel에 날짜를 채워 넣으세요.
  이 단계별 가이드를 따라 TimePeriodDemo.xlsx 파일을 생성하세요.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Python으로 Excel 워크북 만들기 – 배경 설정 및 자동 맞춤
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Python에서 Excel 워크북을 생성하고 셀 배경을 설정하기
url: /ko/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 Excel 워크북 만들고 셀 배경 설정하기

Python에서 Excel 워크북을 만들고 몇 줄의 코드만으로 조건부 서식을 적용합니다. 이 튜토리얼에서는 **excel** 파일을 프로그래밍 방식으로 생성하고, 셀 배경 색을 지정하고, Excel 열을 자동 맞춤하며, Aspose.Cells 라이브러리를 사용해 Excel에 날짜를 채우는 방법을 보여줍니다.

다음 내용을 배울 수 있습니다:
* 워크북을 초기화하고 첫 번째 워크시트를 가져오기.  
* “어제” 날짜를 강조하는 조건부 서식 정의하기.  
* 특정 셀에 샘플 날짜 삽입하기.  
* 데이터를 명확히 볼 수 있도록 열 자동 맞춤하기.  
* 워크북을 원하는 폴더에 저장하기.

전제 조건은 `aspose-cells`와 `aspose-pydrawing` 패키지가 설치된 Python 3 환경입니다:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Python에서 Excel 워크북 만들기 – 단계별 가이드

다음 섹션에서는 과정을 관리하기 쉬운 단계로 나눕니다. 각 단계마다 필요한 코드, **왜** 중요한지에 대한 설명, 흔히 발생하는 실수를 피하기 위한 팁을 제공합니다.

### Step 1: 필요한 네임스페이스 가져오기 및 헬퍼 함수 정의

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: 올바른 클래스를 가져오면 워크북 생성, 조건부 서식, 색상 처리를 사용할 수 있습니다.  
**Pro tip**: import 문은 파일 상단에 두세요. 스크립트를 읽기 쉽고 순환 import 오류를 방지할 수 있습니다.

### Step 2: 워크북 생성 및 첫 번째 워크시트 가져오기

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()` 생성자는 메모리 상에 빈 Excel 워크북을 만듭니다.  
**Why**: 새 워크북으로 시작하면 이전 실행에서 남은 서식이 없으므로 깨끗한 상태를 유지할 수 있습니다.

### Step 3: 조건부 서식으로 셀 배경 색 지정하기

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Why*: **time period** 조건을 사용하면 어제 날짜가 들어 있는 셀을 자동으로 강조하므로 수동 날짜 검사를 없앨 수 있습니다.  
**Tip**: `Color.pink`는 예시일 뿐이며, `Color.yellow`, `Color.light_green` 등 원하는 `Color` 객체를 사용할 수 있습니다.

### Step 4: Excel에 날짜 채우기

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

여기서는 Excel 셀 `I19`와 `K20`에 **날짜를 채웁니다**. 첫 번째 날짜는 조건부 서식을 트리거하고, 두 번째는 트리거하지 않습니다.  
**Why this matters**: 일치하는 값과 일치하지 않는 값을 모두 보여줌으로써 규칙이 기대대로 동작하는지 확인할 수 있습니다.

### Step 5: 가독성을 위해 Excel 열 자동 맞춤하기

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column`은 가장 긴 셀 값을 기준으로 열 너비를 조정합니다.  
**Tip**: 모든 데이터를 쓴 뒤에 호출하세요. 그렇지 않으면 불완전한 내용으로 너비가 계산될 수 있습니다.

### Step 6: 워크북 저장하기

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

파일을 저장하면 메모리 상의 워크북이 최신 XLSX 형식으로 디스크에 기록됩니다.

### 전체 스크립트 – 모두 합치기

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

생성된 파일을 Excel에서 열면 `I19:K20` 셀에 “어제”에 해당하는 날짜가 핑크 배경으로 표시되고, L 열은 라벨이 잘리지 않도록 충분히 넓게 자동 맞춤됩니다.

---

## 왜 이 접근 방식이 최적일까

* **단일 패스 워크플로** – 모든 작업이 동일한 `Workbook` 인스턴스에서 이루어져 불필요한 I/O를 방지합니다.  
* **조건부 서식** – `FormatConditionType.TIME_PERIOD`를 사용하면 Excel이 날짜 로직을 처리하므로 직접 Python으로 날짜를 검사하는 것보다 더 신뢰할 수 있습니다.  
* **명시적 스타일링** – `background_color`와 `pattern`을 설정하면 Excel 버전 간에 시각적 결과가 일관됩니다.  
* **데이터 입력 후 자동 맞춤** – 모든 셀에 값이 채워진 뒤 열을 자동 맞춤하면 정확한 너비가 계산됩니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 코드 예제와 자세한 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Python으로 Excel 워크북 만들기 – 전체 가이드](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Python으로 Excel 워크북 만들기 – 완전 단계별 가이드](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Python으로 Excel 워크북 만들기 – 람다와 함께하는 완전 가이드](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}