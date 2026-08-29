---
category: general
date: 2026-08-20
description: Aspose.Cells를 사용하여 Java에서 엑셀 워크북을 생성하고, 통화 형식을 설정하고, 굵은 글꼴을 추가하며, 스타일이
  적용된 셀을 위해 스타일 배열을 가져옵니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: ko
lastmod: 2026-08-20
og_description: Java에서 엑셀 워크북을 생성하고, 통화 형식을 설정하고, 굵은 글꼴을 추가하고, Aspose.Cells를 사용하여
  스타일을 가져오는 방법을 배웁니다.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Java로 스타일이 적용된 통화 셀을 포함한 엑셀 워크북 만들기
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Java로 통화 형식과 굵은 글꼴이 적용된 Excel 워크북 만들기
url: /ko/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 통화 형식 및 굵은 글꼴이 적용된 Excel 워크북 만들기

프로그램matically **Excel 워크북을 생성**해야 한다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. 워크북을 만들고, 통화 형식을 적용하고, 굵은 글꼴을 추가하며, Aspose.Cells의 **how to import style** 기능을 사용해 모든 가져온 셀이 일관되게 보이도록 진행합니다.

완료되면 `DataTableWithStyleArray.xlsx` 파일이 준비되어 숫자가 달러 표시로 나타나고 굵게 강조됩니다. Excel에서 수동으로 서식을 지정할 필요가 없습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Java 17 이상이 설치되어 있어야 합니다.
- Aspose.Cells for Java 라이선스(또는 무료 평가 키).
- Maven 또는 Gradle을 사용해 `aspose-cells` 종속성을 관리합니다.
- Java 컬렉션 및 `DataTable`에 대한 기본적인 이해.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** `LicenseException`이 발생하면 라이선스 파일을 클래스패스에 두고 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`를 워크북을 생성하기 전에 호출하세요.

## How to create excel workbook with styled currency cells

이 섹션에는 핵심 단계가 포함되어 있습니다. 각 단계는 **왜** 중요한지 설명하며, **무엇을** 입력해야 하는지뿐만 아니라 그 이유도 알려줍니다.

### Step 1: Initialise the workbook and worksheet

새 워크북을 만들면 이후 모든 서식을 적용할 깨끗한 컨테이너를 얻을 수 있습니다.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Why:** `Workbook` 객체는 전체 Excel 파일을 나타냅니다. 첫 번째 `Worksheet`에 접근하면 데이터를 즉시 채우기 시작할 수 있습니다.

### Step 2: Build a DataTable with numeric data

`DataTable`은 데이터베이스 테이블을 모방하므로 행을 한 번에 쉽게 가져올 수 있습니다.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Why:** `DOUBLE`을 사용하면 값이 소수점 정밀도를 유지하므로 나중에 **format cells currency**를 적용할 때 필수적입니다.

### Step 3: Define a style – currency format and bold font

여기서 `Style` 객체에 **통화 형식**과 **굵은 글꼴**을 설정합니다.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Why:** `Number` 형식 문자열 `$#,##0.00`은 Excel에 셀을 금액 값으로 처리하도록 지시하고, `setBold(true)`는 숫자를 강조합니다. 스타일을 배열에 넣으면 **how to import style** 단계에 대비할 수 있습니다.

### Step 4: Configure import options to use the style array

Aspose.Cells는 `ImportTableOptions`를 통해 `Style[]`을 전달할 수 있습니다. 이것이 공식 **how to import style** 방법입니다.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Why:** `ImportTableOptions` 없이 가져온 셀은 기본 스타일을 상속받아 우리가 정의한 통화 서식과 굵은 글꼴을 잃게 됩니다.

### Step 5: Import the DataTable into the worksheet

이제 데이터를 `A1` 셀부터 가져오면서 스타일 배열이 자동으로 적용됩니다.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true`는 `DataTable`의 첫 번째 행이 열 헤더임을 나타냅니다.
- `"A1"`은 가져오기가 시작되는 좌측 상단 셀입니다.

> **Why:** 스타일 배열과 함께 가져오면 각 셀에 앞서 준비한 **format cells currency** 스타일이 자동으로 적용됩니다.

### Step 6: Save the workbook to disk

마지막으로 메모리 상의 워크북을 실제 파일로 저장합니다.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Why:** 저장을 통해 서식이 영구적으로 적용되며, 이후 Excel에서 파일을 열었을 때 원하는 모습으로 표시됩니다.

## Full source code

아래는 완전하고 바로 실행 가능한 Java 클래스입니다. IDE에 복사하고 `YOUR_DIRECTORY`를 실제 폴더 경로로 바꾼 뒤 실행하세요.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Expected output

`DataTableWithStyleArray.xlsx` 파일을 Microsoft Excel에서 열면 다음과 같이 표시됩니다:

| 금액 |
|------|
| **$1,234.56** |
| **$7,890.12** |

- 숫자는 **통화 형식**(`$` 기호와 두 자리 소수)으로 표시됩니다.
- 두 셀 모두 **굵은 글꼴**로 강조되어 눈에 잘 띕니다.

## Common variations and edge cases

| 시나리오 | 변경 내용 | 이유 |
|----------|-----------|------|
| **다른 통화** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | 유로 기호 또는 지역별 형식을 사용합니다. |
| **다른 스타일을 가진 여러 열** | 여러 `Style` 객체를 만들고, 열 순서와 동일하게 `styleArray`에 채웁니다. | 각 열마다 고유한 숫자 형식, 글꼴, 배경 등을 지정할 수 있습니다. |
| **대용량 데이터 세트** | `cells.importDataTable(dataTable, false, "A1", importOptions);` 및 `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` 사용 | 헤더 행이나 불필요한 메타데이터를 건너뛰어 성능을 향상시킵니다. |
| **가져온 후 스타일 적용** | 개별 셀에 대해 `cells.get("A2").setStyle(currencyStyle);` 호출 | 일부 행만 특별한 서식이 필요할 때 유용합니다. |

## Tips for production use

- **License early**: 워크북을 만들기 전에 Aspose.Cells 라이선스를 등록해 평가 워터마크가 나타나지 않도록 합니다.
- **Thread safety**: `Workbook` 인스턴스는 **스레드 안전하지** 않습니다. 동시에 많은 파일을 생성해야 한다면 스레드당 별도 인스턴스를 생성하세요.
- **Memory management**: 매우 큰 시트의 경우 `Workbook` 스트리밍 API(`Workbook` → `WorkbookDesigner`)를 사용해 메모리 사용량을 낮추세요.
- **Testing**: 저장된 파일을 Apache POI로 열어 셀 스타일의 숫자 형식이 `"$#,##0.00"`과 일치하는지 검증하는 단위 테스트를 포함시키세요.

## Conclusion

이제 Java에서 **Excel 워크북을 생성**, **통화 형식 설정**, **굵은 글꼴 추가**, 그리고 Aspose.Cells의 `ImportTableOptions`를 활용한 **how to import style** 방법을 정확히 알게 되었습니다. 이 엔드‑투‑엔드 솔루션은 수동 Excel 작업을 없애고 모든 가져온 셀이 동일한 **format cells currency** 스타일을 따르도록 보장합니다.

다음 도전 과제가 준비되셨나요? 조건부 서식 추가, 차트 삽입, 혹은 워크북을 PDF로 내보내는 작업을 시도해 보세요—모두 동일한 스타일‑배열 기법을 재사용할 수 있습니다. 즐거운 코딩 되세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하며, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방법을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용해 Excel 워크북 만들기: 단계별 가이드](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java를 사용해 Excel 셀 만들기 및 서식 지정: 단계별 가이드](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Aspose.Cells for Java를 사용해 Excel 셀에 스타일 적용 및 하이퍼링크 추가](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}