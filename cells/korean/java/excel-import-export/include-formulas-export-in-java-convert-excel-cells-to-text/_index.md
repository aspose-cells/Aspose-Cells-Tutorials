---
category: general
date: 2026-07-03
description: Aspose.Cells를 사용하여 Java에서 수식을 포함한 내보내기로 Excel 셀을 텍스트로 변환합니다. Excel 범위를
  출력하고 셀 값을 문자열로 효율적으로 가져오는 방법을 배워보세요.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: ko
og_description: Java에서 수식 내보내기를 포함해 Excel 셀을 텍스트로 변환합니다. Excel 범위를 출력하고 셀 값을 문자열로
  가져오는 단계별 가이드.
og_title: Java에서 수식 포함 내보내기 – Excel 셀을 텍스트로 변환
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Java에서 수식 포함 내보내기 – Excel 셀을 텍스트로 변환
url: /ko/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 수식 내보내기 포함 – Excel 셀을 텍스트로 변환

Excel 워크북에서 데이터를 추출할 때 **수식 내보내기 포함**이 필요했던 적이 있나요? 원본 수식을 보존하면서 깔끔한 텍스트 블롭을 제공해야 하는 보고 서비스를 구축하고 있을지도 모릅니다. 그런 경우라면, 여기서 맞는 곳입니다. 이 가이드는 Aspose.Cells for Java를 사용하여 Excel 셀을 일반 텍스트로 변환하는 방법을 단계별로 안내합니다—*포함된* 모든 수식도 함께 변환합니다.

또한 **Excel 범위 출력** 방법, **export table options** 조정, 그리고 최종적으로 **셀 값 문자열 가져오기**에 대해서도 다룰 것입니다. 이 문자열은 로그에 기록하거나 API를 통해 전송하거나 데이터베이스에 저장할 수 있습니다. 끝까지 읽으면 완전하게 실행 가능한 코드 스니펫과 각 호출 뒤의 이유를 확실히 이해하게 됩니다.

## 얻을 수 있는 것

- `.xlsx` 파일을 읽고, 범위를 선택한 뒤, 포맷된 문자열로 내보내는 완전한 복사‑붙여넣기 가능한 Java 프로그램.
- `ExportTableOptions` 클래스와 `setExportAsString` 및 `setIncludeFormula` 토글이 왜 중요한지에 대한 이해.
- 대형 워크시트 처리, 다양한 데이터 유형 다루기, 출력 형식 맞춤에 대한 팁.
- 일반적인 함정(병합 셀, 숨겨진 행, 로케일별 숫자 형식 등)에 대한 빠른 체크리스트.

### 사전 요구 사항

- Java 17 이상(코드는 이전 버전에서도 컴파일되지만 최신 LTS를 사용합니다).
- Aspose.Cells for Java 23.10(또는 최신 릴리스) — Maven Central에서 가져올 수 있습니다.
- 직접 관리하는 폴더에 위치한 샘플 `input.xlsx`(예제에서는 경로가 명시적으로 하드코딩되어 있습니다).

이미 준비되었다면, 바로 시작해봅시다.

## 단계 1: 프로젝트 설정 및 종속성 추가

먼저, Maven 프로젝트(또는 선호한다면 Gradle)를 생성합니다. `pom.xml`에 Aspose.Cells 종속성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** 기업 프록시를 사용하는 경우, 저장소에 접근할 수 있는지 확인하세요. 그렇지 않으면 “Could not resolve dependencies” 오류와 함께 빌드가 실패합니다.

Maven 다운로드가 완료되면 Java 코드를 작성할 준비가 된 것입니다.

## 단계 2: 워크북 로드 및 원하는 워크시트 가져오기

코드 예제의 첫 번째 줄은 기존 워크북을 여는 방법을 보여줍니다:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`YOUR_DIRECTORY`를 파일의 절대 경로나 상대 경로로 교체하세요. `Workbook` 생성자는 파일 형식(XLS, XLSX, CSV 등)을 자동으로 감지하므로 별도로 지정할 필요가 없습니다.

다음으로 첫 번째 시트를 가져옵니다:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

왜 첫 번째 시트일까요? 많은 템플릿에서 데이터가 첫 번째 탭에 존재하지만, 원하는 인덱스를 전달하거나 이름 기반 접근을 원한다면 `get("SheetName")`을 사용할 수도 있습니다.

## 단계 3: 내보낼 범위 정의

이제 **convert excel cells text** 작업의 핵심 단계입니다. `Range` 객체를 생성하여 Aspose.Cells에 가져올 셀을 지정합니다:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

`"A1:C3"` 문자열은 전통적인 A1 스타일 주소입니다. 프로그래밍 방식으로도 만들 수 있습니다:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

이 유연성은 범위 크기가 동적일 때 도움이 됩니다—예를 들어 `ws.getCells().getMaxDataRow()`로 마지막 사용 행을 읽는 경우 등.

## 단계 4: 수식 포함을 위한 Export Table Options 설정

여기서 **include formulas export** 마법이 작동합니다. 기본적으로 Aspose.Cells는 *표시된* 값을 반환합니다. 셀에 `=SUM(A1:A3)`와 같은 수식이 있으면 계산된 숫자를 얻으며, 수식 텍스트는 얻지 못합니다. 이를 변경하려면 `ExportTableOptions`를 설정합니다:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

두 플래그가 왜 필요한가요? `setExportAsString(true)`는 API에 기본 구분자(열은 탭, 행은 줄바꿈)를 사용해 셀을 연결하도록 지시합니다. `setIncludeFormula(true)`는 값 소스를 “표시된 값”에서 “원시 수식”으로 전환합니다. 값만 원한다면 `false`로 두세요.

### 선택적 조정

- `eto.setExportHiddenRows(true);` – Excel에서 숨겨진 행을 포함합니다.
- `eto.setExportHiddenColumns(true);` – 열에 대해서도 동일합니다.
- `eto.setExportAsHTML(true);` – 일반 텍스트 대신 HTML을 얻습니다.

자유롭게 실험해 보세요; 옵션 클래스는 **export table options** 놀이터와 같습니다.

## 단계 5: 범위를 포맷된 문자열로 가져오기

이제 데이터를 가져옵니다:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

반환된 `txt`는 다음과 같은 형태입니다(가정: A1:C3에 값과 수식이 혼합되어 있음):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

열은 탭(`\t`)으로, 행은 줄바꿈(`\n`)으로 구분됩니다. 2‑D 배열이 필요하면 문자열을 나중에 분할할 수 있습니다:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## 단계 6: 결과 출력 – “Print Excel Range” 간단히

마지막으로 문자열을 콘솔에 출력합니다:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

프로그램을 실행하면 위에 표시된 정확한 출력이 콘솔에 표시됩니다. 여기서 문자열을 로그 파일에 기록하거나 HTTP로 전송하거나 NoSQL 문서에 저장할 수 있습니다.

## 전체 실행 가능한 예제

모두 합치면 완전한 프로그램이 됩니다. 복사·붙여넣기 후 **Run**을 눌러 보세요—누락된 import는 없습니다.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### 예상 출력 (예시)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

워크북에 날짜 형식으로 포맷된 숫자가 포함되어 있으면 로케일에 맞는 형식(예: `2026‑07‑03`)으로 표시됩니다. ISO 날짜 형식으로 강제하려면 사용자 정의 `NumberFormat`을 사용해 `ExportTableOptions`를 조정하면 됩니다.

## 엣지 케이스 및 일반 질문 처리

### 범위에 병합 셀이 포함된 경우는?

병합 셀은 좌상단 셀의 값으로 처리됩니다. 병합 영역의 나머지는 빈 문자열로 표시됩니다. 병합 영역 주소가 필요하면 내보내기 전에 `Cell.getMergedRange()`를 조회하세요.

### 수십만 행의 대용량 시트를 내보낼 수 있나요?

가능하지만 메모리 사용량에 유의하세요. `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`를 사용하면 Aspose.Cells가 데이터를 디스크에 스트리밍하도록 할 수 있습니다. 또한 문자열 크기를 관리하기 위해 (예: 한 번에 10 000행) 청크 단위로 내보내는 것을 고려하세요.

### 열 구분자를 어떻게 변경하나요?

`ExportTableOptions`는 `setSeparator(char separator)`를 제공합니다. CSV 스타일 출력의 경우 `','` 로 설정합니다:

```java
eto.setSeparator(',');
```

### 수식이 외부 참조를 인식하나요?

수식이 다른 워크북을 참조하면 Aspose.Cells는 참조 텍스트(`='[Other.xlsx]Sheet1'!A1`)를 그대로 유지합니다. 해당 워크북을 로드하지 않으면 외부 값을 평가하지 않습니다.

## 프로덕션 준비 코드를 위한 팁

- **Cache the workbook** if you’re reading the

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells Java를 사용하여 Excel을 HTML로 생성 및 내보내는 방법 | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Aspose.Cells를 사용하여 Java에서 Excel을 PDF로 변환하는 방법: 단계별 가이드](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북을 이미지로 내보내는 방법: 단계별 가이드](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}