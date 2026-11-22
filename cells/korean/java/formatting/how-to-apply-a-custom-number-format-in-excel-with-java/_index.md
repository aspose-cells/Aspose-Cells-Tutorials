---
category: general
date: 2026-11-22
description: Java를 사용하여 Excel에서 열을 통화 형식으로 지정하기 위해 사용자 지정 숫자 형식을 사용하는 방법을 배웁니다. 간단한
  스타일로 Excel 숫자 형식을 빠르게 설정하세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: ko
lastmod: 2026-11-22
og_description: Java를 사용하여 Excel에 사용자 지정 숫자 형식을 적용합니다. 이 튜토리얼에서는 Excel 숫자 형식을 설정하고
  첫 번째 열을 통화 형식으로 스타일링하는 방법을 보여줍니다.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Java로 Excel에서 사용자 지정 숫자 형식 적용 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Java로 Excel에서 사용자 지정 숫자 형식을 적용하는 방법
url: /ko/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java로 Excel에서 사용자 정의 숫자 서식 적용하기

Excel 워크시트에서 열에 **사용자 정의 숫자 서식**을 적용해야 한다면, 이 가이드는 Java를 사용하여 정확히 수행하는 방법을 보여줍니다. 재무 보고서를 생성하거나 회계 데이터를 내보내는 경우, 첫 번째 열을 통화 형식으로 서식 지정하면 출력이 즉시 읽기 쉬워집니다.

아래 예제에서는 **열을 통화 형식으로 서식 지정**하고, 스타일을 첫 번째 열에 적용한 다음 `DataTable`을 워크시트에 가져옵니다. 동일한 접근 방식은 표시하려는 모든 숫자 형식에 적용할 수 있습니다.

## 배울 내용

* Apache POI의 `Style` 객체를 사용하여 **사용자 정의 숫자 서식**을 만드는 방법.  
* 특정 열에 대해 **Excel 숫자 서식 설정**하는 방법, 여기에는 **통화 서식 설정** 사례가 포함됩니다.  
* `DataTable`을 가져오는 동안 **첫 번째 열에 스타일 적용**하는 방법.  
* 워크북을 저장하고 서식이 올바르게 적용되었는지 확인하는 방법.

### 사전 요구 사항

* Java 17 이상.  
* Apache POI 5.x (`Workbook`, `Worksheet`, `Style`을 제공하는 라이브러리).  
* 코드 샘플과 같이 반복할 수 있는 `DataTable` 구현.  
* Java와 Excel 개념에 대한 기본적인 이해.

---

## 단계 1: 프로젝트 설정 및 데이터 가져오기

먼저, 프로젝트에 Apache POI를 추가합니다. Maven을 사용하는 경우, 다음 의존성을 포함하십시오:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

다음으로, 소스 데이터를 `DataTable`로 가져옵니다. 실제 상황에서는 데이터베이스 쿼리, CSV 파일 또는 API 응답에서 가져올 수 있습니다.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **팁:** `DataTable` 열이 올바른 Java 타입(`Integer`, `Double` 등)인지 확인하십시오. 숫자 서식은 숫자 셀에만 영향을 미칩니다.

---

## 단계 2: 첫 번째 열에 대한 **사용자 정의 숫자 서식** 만들기

**사용자 정의 숫자 서식**은 Excel에 숫자 값을 어떻게 표시할지 알려줍니다. 값을 통화로 표시하려면 내장 `CURRENCY` 형식을 사용하지만, `"$#,##0.00"`와 같은 패턴을 정의할 수도 있습니다.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**이 동작 원리:**
* `createCellStyle()`는 재사용 가능한 스타일 객체를 반환합니다.  
* `setDataFormat()`은 스타일에 **통화 서식 설정**을 연결하고, Excel은 이 스타일을 사용하는 모든 셀에 적용합니다.  
* 스타일을 `columnStyles[0]`에 저장함으로써 첫 번째 열에만 통화 서식이 적용되도록 보장합니다.

---

## 단계 3: 열 스타일을 적용하면서 `DataTable` 가져오기

이제 데이터를 워크시트에 가져옵니다. `importDataTable` 메서드는 스타일 배열을 받아 **첫 번째 열에 스타일 적용**을 가능하게 하고, 나머지 열은 기본 서식을 유지합니다.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

위 호출은 첫 번째 열에만 **Excel 숫자 서식 설정**을 수행합니다. 다른 모든 열은 워크북의 기본 스타일을 상속받아 코드가 간단하고 효율적입니다.

---

## 단계 4: 워크북 저장 및 결과 확인

마지막으로 워크북을 파일에 기록하고 Excel에서 열어 첫 번째 열에 통화 기호가 표시되는지 확인합니다.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**예상 출력:**  
*FormattedReport.xlsx* 파일을 열면, A 열의 값이 적절한 통화 기호(예: `$1,234.00`)와 함께 표시됩니다. 다른 모든 열은 원래의 숫자 표현을 유지합니다.

---

## 일반적인 변형 및 엣지 케이스

| 상황 | 조정 |
|-----------|------------|
| **다른 통화** (예: Euro) | `Style.CustomNumberFormat.CURRENCY`를 사용자 정의 패턴으로 교체합니다: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **여러 개의 스타일된 열** | `columnStyles[]`에 추가 항목을 채워 각각의 `CellStyle` 객체를 할당합니다. |
| **대용량 데이터 세트** | `importDataTable`을 배치로 사용하거나 행을 스트리밍하여 `OutOfMemoryError`를 방지합니다. |
| **지역별 구분 기호** | `java.text.NumberFormat`을 사용하여 지역에 맞는 패턴을 생성하고 이를 `setDataFormat`에 전달합니다. |

> **주의:** 여러 열에 단일 `CellStyle` 객체를 재사용하면 Excel이 워크북당 허용하는 고유 스타일 수에 제한이 있기 때문에 예상치 못한 서식이 발생할 수 있습니다. 필요한 각 고유 형식마다 별도의 스타일을 생성하십시오.

---

## 전체 실행 가능한 예제

아래는 데이터 생성부터 서식이 적용된 워크북 저장까지 전체 흐름을 보여주는 독립 실행형 프로그램입니다.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

프로그램을 실행하면 **FormattedReport.xlsx** 파일이 생성되며, A 열(“Amount” 열)은 달러 기호와 소수점 두 자리 표시가 포함된 **사용자 정의 숫자 서식**으로 표시됩니다.

---

## 결론

이제 Java에서 Excel 워크시트에 **사용자 정의 숫자 서식**을 적용하고, **열을 통화 형식으로 서식 지정**하며, 데이터를 가져오는 동안 **첫 번째 열에 스타일 적용**하는 방법을 알게 되었습니다. 재사용 가능한 `CellStyle`을 생성하고 이를 `importDataTable`에 전달하면 각 셀을 수동으로 반복하지 않고도 원하는 열에 **Excel 숫자 서식 설정**을 할 수 있습니다.

다음에 시도해 보세요:

* 지역별 패턴을 사용한 `setDataFormat`으로 **통화 서식 설정**

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Java에서 Excel 숫자 서식 설정 – 완전 가이드](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Java에서 Excel 숫자 서식 적용 – 완전 Aspose.Cells 가이드](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Java에서 통화 서식 및 굵은 글꼴이 적용된 Excel 워크북 만들기](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}