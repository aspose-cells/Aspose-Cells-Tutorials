---
category: general
date: 2026-06-08
description: GridJs에 사용자 정의 컨텍스트 메뉴를 추가하고, 그리드를 CSV 파일 블롭으로 다운로드하여 내보냅니다. 완전히 작동하는
  예제를 위해 단계별 튜토리얼을 따라보세요.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: ko
og_description: GridJs에 사용자 정의 컨텍스트 메뉴를 추가하고 CSV 파일 블롭으로 그리드를 내보내세요. 10분 안에 전체 구현
  방법을 배워보세요.
og_title: GridJs에 맞춤 컨텍스트 메뉴 추가 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: GridJs에 맞춤형 컨텍스트 메뉴 추가 – 완전 가이드
url: /ko/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs에 사용자 정의 컨텍스트 메뉴 추가 – 완전 가이드

GridJs 컴포넌트에 **사용자 정의 컨텍스트 메뉴**를 추가하고 싶으신가요? 이 튜토리얼에서는 바로 그 방법을 단계별로 안내하고, **CSV 파일 Blob 다운로드**를 이용해 **그리드를 CSV로 내보내는** 방법을 보여드립니다. 빠른 관리 패널을 만들든, 본격적인 보고 대시보드를 구축하든, 사용자가 오른쪽 클릭 메뉴로 데이터를 CSV로 추출할 수 있다면 생산성이 크게 향상됩니다.

Python 쪽 Flask 설정, Blob을 생성하는 JavaScript 핸들러, 그리고 GridJs가 출력하는 HTML/JS까지 모두 다룹니다. 끝까지 따라오시면 어떤 프로젝트에도 바로 넣을 수 있는 독립형 예제를 얻으실 수 있습니다.

---

## 준비물

시작하기 전에 아래 항목을 확인하세요:

- **Python 3.9+** 및 **Flask**가 설치되어 있어야 합니다 (`pip install flask`).
- **gridjs** Python 래퍼(또는 직접 JavaScript 라이브러리) – 이 가이드에서는 JavaScript API와 동일한 얇은 Python 래퍼를 가정합니다.
- **async JavaScript**(`fetch`, `Promise`)에 대한 기본 이해 – 걱정 마세요, 각 라인을 자세히 설명합니다.
- 선호하는 편집기(VS Code, PyCharm, 혹은 간단한 텍스트 편집기 등).

이 정도면 충분합니다. 별도의 프론트엔드 빌드 도구나 Node npm 설정은 필요 없습니다. Flask가 GridJs가 생성한 HTML을 그대로 제공하면 됩니다.

---

## GridJs에 사용자 정의 컨텍스트 메뉴 추가

먼저 GridJs에 사용자 정의 오른쪽 클릭 메뉴가 필요하다고 알려줘야 합니다. 기본적으로 GridJs는 최소한의 메뉴(복사, 붙여넣기 등)만 제공하지만, 이를 완전히 교체할 수 있습니다.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**왜 중요한가요:**  
`CustomContextMenu`를 설정하면 기본 메뉴 리스트를 여러분이 제공한 리스트로 교체합니다. 문자열 `"Export CSV"`는 단순히 라벨일 뿐이며, 실제 동작은 사용자가 클릭했을 때 발생합니다. 다음 단계에서 이를 연결합니다.

> *팁:* 메뉴는 짧게 유지하세요. 복잡한 컨텍스트 메뉴는 빠른 액션이라는 목적을 무색하게 합니다.

---

## Blob 다운로드로 Grid를 CSV로 내보내기

이제 메뉴 항목이 생겼으니, 서버와 통신해 CSV를 받아 Blob으로 변환하고 다운로드를 강제하는 JavaScript 핸들러가 필요합니다. 바로 여기서 **download CSV file blob**이라는 문구가 등장합니다.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### 핸들러 상세 분석

| Line | What It Does |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Flask 라우트(`/export/csv`)를 호출하면서 시트 이름을 쿼리 문자열로 전달합니다. |
| `.then(r => r.blob())` | HTTP 응답을 **Blob**으로 변환합니다 – CSV 데이터를 담는 바이너리 컨테이너 역할을 합니다. |
| `URL.createObjectURL(b)` | 브라우저가 파일처럼 취급할 수 있는 임시 URL을 생성합니다. |
| `a.download = cell.sheetName + ".csv"` | 사용자가 다운로드 대화상자에서 보게 될 파일명을 설정합니다. |
| `a.click()` | 숨겨진 앵커를 프로그래밍 방식으로 클릭해 Blob 다운로드를 트리거합니다. |

> **왜 Blob을 사용하나요?**  
> `fetch`가 반환하는 원시 텍스트를 바로 다운로드할 수 없기 때문에, 파일 형태로 변환해야 합니다. Blob‑URL 기법은 페이지를 새로 고치지 않고 **download CSV file blob**을 트리거하는 가장 신뢰할 수 있는 크로스 브라우저 방법입니다.

---

## Flask 백엔드 설정

프론트엔드 핸들러가 기대하는 엔드포인트는 `/export/csv`입니다. 아래는 시트 이름을 받아 워크북에서 데이터를 추출하고 CSV를 스트리밍으로 반환하는 최소 Flask 뷰입니다.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### 핵심 포인트

- **`io.StringIO`**를 사용해 파일 시스템에 접근하지 않고 메모리 상에서 CSV를 생성합니다.
- **`Content‑Disposition`** 헤더는 브라우저에게 파일이 첨부 파일임을 알리고 파일명을 제안합니다. 프론트엔드에서도 `a.download`를 설정하지만, 서버 측에서도 지정해 두면 JS를 사용하지 않는 클라이언트에 대한 폴백이 됩니다.
- 라우트는 의도적으로 간단하게 구현했으며, 이후 인증, 권한 검사, 대용량 데이터 스트리밍 등을 추가할 수 있습니다.

---

## 클라이언트에서 Grid 렌더링하기

컨텍스트 메뉴와 백엔드가 준비되었으니, 마지막으로 GridJs 컴포넌트를 렌더링하고 HTML/JS를 브라우저에 전달합니다.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Flask 뷰에서는 보통 다음과 같이 작성합니다:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

페이지가 로드되면 GridJs가 테이블을 만들고, 사용자 정의 컨텍스트 메뉴를 주입하며, 앞서 정의한 JavaScript 핸들러가 준비됩니다. 셀을 오른쪽 클릭하고 **Export CSV**를 선택하면 시트 이름을 딴 파일이 브라우저에서 자동으로 다운로드됩니다.

---

## 전체 작동 예제 (모든 파일)

아래는 새 폴더에 복사‑붙여넣기만 하면 바로 실행할 수 있는 완전한 코드입니다. Flask를 설치(`pip install flask`)하고 `python app.py`를 실행하세요.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}