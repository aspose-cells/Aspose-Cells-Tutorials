---
category: general
date: 2026-06-30
description: Python Excel 그리드에 사용자 정의 컨텍스트 메뉴를 추가하고, 업데이트된 파일을 저장하면서 Excel 셀에 값을 기록합니다.
  오른쪽 클릭 메뉴를 만들고 Python 스타일로 셀 값을 업데이트하는 방법을 배워보세요.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: ko
og_description: Python에서 사용자 정의 컨텍스트 메뉴를 추가하여 Excel 셀에 값을 쓰고 업데이트된 Excel 파일을 저장합니다.
  이 가이드는 GridJs를 사용해 오른쪽 클릭 메뉴를 만드는 방법을 단계별로 안내합니다.
og_title: Python에서 사용자 정의 컨텍스트 메뉴 추가 – 단계별 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Python에서 사용자 정의 컨텍스트 메뉴 추가 – 완전 가이드
url: /ko/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 사용자 정의 컨텍스트 메뉴 추가 – 완전 가이드

Python에서 제공하는 스프레드시트 그리드에 **사용자 정의 컨텍스트 메뉴** 항목을 추가하는 방법이 궁금하셨나요? 사용자가 셀을 오른쪽 클릭했을 때 나타나는 빠른 “Mark as Reviewed” 버튼이 필요할 수도 있습니다. 이 버튼은 셀에 값을 기록하고 업데이트된 워크북을 저장합니다—웹 UI를 떠나지 않고 모두 수행합니다.  

이 튜토리얼에서는 정확히 그 작업을 구현합니다: GridJs로 구동되는 **사용자 정의 오른쪽 클릭 메뉴**, Excel 셀에 **값을 쓰는** 서버‑사이드 핸들러, 그리고 디스크에 **업데이트된 Excel 파일을 저장하는** 최종 단계. 끝까지 따라오면 Flask, FastAPI, Django 프로젝트 어디에든 적용할 수 있는 재사용 가능한 패턴을 얻게 됩니다.

> **왜 신경 써야 할까요?**  
> 사용자 정의 컨텍스트 메뉴를 추가하면 데이터 검토 워크플로가 간소화되고 수동 복사‑붙여넣이가 줄어들며, 사용자는 그리드 내부에서 네이티브한 경험을 얻습니다. 또한 **Python 스타일로 셀 값 업데이트** 방법을 배우게 되며, 이는 모든 Excel 자동화 작업의 핵심 기술입니다.

## 사전 요구 사항

- Python 3.9+ (코드는 3.10에서도 동작합니다)  
- `openpyxl` – Excel 파일 처리용  
- `gridjs` Python 래퍼 (또는 프론트‑엔드용 JS 라이브러리)  
- 기본 웹 프레임워크 (예시로 Flask 사용)  
- 프로젝트 폴더에 `sample.xlsx` 라는 워크북 파일  

필요한 것이 하나라도 없으면 다음을 실행하세요:

```bash
pip install openpyxl flask gridjs
```

이제 시작합니다.

---

## Step 1 – 사용자 정의 컨텍스트 메뉴 추가: GridJs 초기화 및 워크시트 바인딩

먼저 `GridJs` 인스턴스를 생성하고 작업할 워크시트를 지정해야 합니다. 여기서 **사용자 정의 컨텍스트 메뉴**라는 구문이 코드에 처음 등장하며, 이후 모든 작업의 기반이 됩니다.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**무슨 일이 일어나나요?**  
`grid.set_worksheet(ws)`는 GridJs에게 `ws`의 데이터를 데이터 소스로 사용하도록 알려줍니다. 이제부터 추가하는 모든 컨텍스트‑메뉴 수정은 자동으로 동일한 워크시트를 대상으로 하여 UI와 파일이 동기화됩니다.

> **Pro tip:** 워크북은 읽기/쓰기 모드로 한 번만 열어 두세요. 요청 핸들러 안에서 반복적으로 열면 Windows에서 파일 잠금 문제가 발생할 수 있습니다.

---

## Step 2 – Excel 셀에 값 쓰기: 메뉴 항목에 대한 동작 정의

그리드가 준비되었으니 사용자가 우리 커스텀 명령을 선택했을 때 **Excel 셀에 값 쓰기**가 필요합니다. “Mark as Reviewed”라는 메뉴 항목을 추가하고 식별자 `markReviewed`를 부여합니다. 이 식별자는 클라이언트‑사이드 JavaScript가 서버에 다시 전달할 값입니다.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**왜 커스텀 식별자를 사용하나요?**  
식별자는 UI 텍스트와 서버 로직을 분리해 라벨을 바꾸어도 백엔드 코드를 수정할 필요가 없게 합니다. 또한 **오른쪽 클릭 메뉴 생성** 작업을 명시적이고 재사용 가능하게 만들어 줍니다.

---

## Step 3 – 오른쪽 클릭 메뉴 생성: 서버‑사이드 핸들러 등록

메뉴 항목을 추가했으니 사용자가 클릭했을 때 GridJs가 무엇을 해야 하는지 알려줘야 합니다. 여기서 **오른쪽 클릭 메뉴 생성** 기능이 실제로 Python에 요청을 보내는 역할을 합니다.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

주의할 점 몇 가지:

1. **`ws[cell_address] = "Reviewed"`** 은 **Python 스타일로 셀 값 업데이트**하는 가장 직관적인 방법입니다. `openpyxl`이 A1 스타일 주소를 행/열 인덱스로 변환합니다.  
2. 핸들러는 작은 JSON 페이로드를 반환합니다. GridJs는 상태 표시자를 기대하므로 필요에 따라 오류 메시지를 포함하도록 확장할 수 있습니다.

이제 식별자를 핸들러에 바인딩합니다:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**셀에 값이 없거나 보호된 경우는 어떻게 하나요?**  
- 빈 셀은 문제 없습니다—`openpyxl`이 자동으로 생성합니다.  
- 보호된 시트인 경우 먼저 보호를 해제해야 합니다 (`ws.protection.sheet = False`) 혹은 `PermissionError`를 잡아야 합니다.

---

## Step 4 – Python으로 셀 값 업데이트: 워크북 저장으로 변경 사항 영구화

값을 쓰는 것만으로는 이야기가 절반에 불과합니다; **업데이트된 Excel 파일 저장**을 해야 현재 세션을 넘어 변경 사항이 유지됩니다. 여기서 UI에서 디스크까지의 라운드‑트립을 마무리합니다.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**왜 별도 폴더에 저장하나요?**  
`output/` 디렉터리에 저장하면 원본 템플릿을 건드리지 않아 감사 추적에 유용합니다. 배포 환경에 맞게 경로를 조정하세요.

> **Watch out:** 동시 사용자가 많을 경우 `wb.save()` 주변에 `threading.Lock` 같은 스레드‑안전 잠금을 사용해 레이스 컨디션을 방지하세요.

---

## Step 5 – 클라이언트 설정 JSON 생성 및 전체 연결

마지막으로 프론트‑엔드 GridJs 인스턴스가 사용할 JSON을 생성해야 합니다. 이 JSON에는 워크시트 데이터 **와** 커스텀 메뉴 정의가 포함됩니다.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

HTML 페이지에 `config_json`을 삽입하면 GridJs가 “Mark as Reviewed” 항목이 모든 셀에서 오른쪽 클릭 가능하도록 그리드를 렌더링합니다.

### 전체 Flask 예제

아래는 모든 요소를 하나로 묶은 최소 Flask 앱 예제입니다. 실행 후 `http://localhost:5000`에 접속하고 셀을 오른쪽 클릭하면 커스텀 메뉴가 작동하는 것을 확인할 수 있습니다.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**예상 결과:**  
- 셀을 오른쪽 클릭 → “Mark as Reviewed”가 나타납니다.  
- 클릭하면 셀 내용이 “Reviewed”로 바뀝니다.  
- 워크북 `output/sample-updated.xlsx`에 새로운 값이 저장됩니다.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *여러 개의 커스텀 액션이 필요하면 어떻게 하나요?* | `grid.settings.context_menu.custom_items`에 객체를 더 추가하고 각각 고유 식별자를 등록하면 됩니다. |
| *핸들러에 추가 데이터(예: 행 ID)를 전달할 수 있나요?* | 가능합니다. 클라이언트 측에서 JSON 페이로드에 추가 키를 넣고 `on_custom_command` 내부에서 `request`로 읽어오세요. |
| *비동기 프레임워크와 호환되나요?* | 물론입니다—`on_custom_command`를 async 함수로 만들고 `aiofiles` 등으로 `await wb.save(...)`를 사용하면 됩니다. |
| *메뉴 아이콘은 어떻게 스타일링하나요?* | 任意의 Material‑Icons 이름(`"icon": "edit"` 등)을 제공하면 프론트‑엔드가 자동으로 아이콘 폰트를 로드합니다. |
| *대용량 워크북은 어떻게 처리하나요?* | 필요한 시트만 로드하고 `openpyxl.iter_rows()` 로 스트리밍하면 메모리 사용량을 최소화할 수 있습니다. |

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}