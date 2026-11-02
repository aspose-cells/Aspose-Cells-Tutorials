---
category: general
date: 2026-06-27
description: DataTable을 Excel로 가져오면서 교차 열 색상을 적용하는 방법을 배워보세요. 포맷을 포함한 데이터 가져오기와 Java를
  사용하여 열 글꼴 색상을 설정하는 단계별 가이드.
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: ko
og_description: DataTable을 Excel로 가져올 때 교차 열 색상을 마스터하세요. 이 가이드는 Java에서 서식이 적용된 데이터를
  가져오고 열 글꼴 색상을 설정하는 방법을 보여줍니다.
og_title: Excel에서 교차 열 색상 – 서식이 포함된 DataTable 가져오기
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: Excel에서 교차 열 색상 – 서식이 적용된 DataTable 가져오기
url: /ko/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 교차 열 색상 적용 – 서식과 함께 DataTable 가져오기

코드에서 벗어나지 않고 Excel 내보내기에 시각적인 멋을 더하고 싶으셨나요? **Alternating column colors**는 큰 테이블을 읽기 쉽게 만드는 빠른 방법이며, **import datatable to excel**을 수행하면서도 적용할 수 있습니다. 이 튜토리얼에서는 데이터를 워크시트에 가져올 뿐만 아니라 열별로 파란‑녹색 글꼴 패턴을 적용하는 완전한 Java 솔루션을 단계별로 살펴보겠습니다.

**import data with formatting**을 수행하고, 각 열의 글꼴 색상을 설정하며, 지속되던 “**how to import datatable**” 질문에 최종적으로 답변하는 방법을 보여드립니다. 외부 도구 없이 순수 Java와 인기 있는 스프레드시트 라이브러리만 사용합니다.

## 만들게 될 것

이 가이드를 끝까지 따라오면 실행 가능한 Java 코드 조각을 얻게 됩니다:

1. `DataTable`(또는 `ResultSet`과 유사한 컬렉션)을 가져옵니다.  
2. 짝수 열은 파란색, 홀수 열은 녹색인 `Style` 배열을 생성합니다.  
3. `importDataTable`를 호출하여 데이터를 **A1** 셀에 넣고 스타일을 적용합니다.

이 모든 작업은 몇 줄의 코드로 이루어지지만, 결과는 손수 만든 보고서처럼 보입니다.

### 사전 요구 사항

- Java 8+ (코드는 최신 버전에서도 동작합니다).  
- 클래스패스에 Apache POI 5.x – Excel 파일과 통신하는 라이브러리.  
- `getColumns()`와 `size()`를 제공하는 `DataTable` 구현체(또는 예제를 `ResultSet`에 맞게 조정).

이미 POI를 다른 Excel 작업에 사용하고 있다면, 바로 이 코드를 삽입하면 됩니다.

---

## DataTable을 Excel로 가져오면서 교차 열 색상 적용

솔루션의 핵심은 네 가지 간결한 단계에 있습니다. 각각을 살펴보겠습니다.

### 단계 1 – 내보낼 DataTable 확보

먼저, 행과 열의 소스가 필요합니다. 실제 프로젝트에서는 데이터베이스 쿼리, CSV 파서, 혹은 메모리 내 컬렉션일 수 있습니다. 예제에서는 사용 가능한 `DataTable`을 반환하는 헬퍼 메서드 `getDataTable()`을 가정합니다.

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **왜 중요한가:**  
> 데이터를 먼저 가져오면 열 개수를 확인할 수 있어 이후 스타일 배열 크기를 결정합니다. 또한 가져오기 단계에서 구체적인 객체를 사용할 수 있게 합니다.

### 단계 2 – 각 열에 대한 Style 준비

`Style[]`를 생성하는데, 길이는 열 수와 동일합니다. 각 항목은 파란색과 녹색을 교차하는 글꼴 색상을 보관합니다.

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **팁:** `DataTable`이 런타임에 형태가 바뀔 수 있다면, 내보낼 때마다 `columnCount`를 다시 계산하세요. 이렇게 하면 `ArrayIndexOutOfBoundsException`을 방지할 수 있습니다.

### 단계 3 – 교차 글꼴 색상의 Style 생성

이제 재미있는 부분입니다: 배열을 순회하면서 짝수 인덱스 열에는 파란색 글꼴을, 홀수 인덱스 열에는 녹색 글꼴을 할당합니다. 여기서 **alternating column colors**가 구현됩니다.

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **왜 교차 색상을 사용할까?**  
> 인접한 열이 돋보이면 사람의 눈이 행을 더 쉽게 스캔합니다. 파란‑녹색 리듬은 특히 넓은 테이블에서 시각적 피로를 줄여줍니다.

### 단계 4 – Style 배열을 사용해 DataTable 가져오기

마지막으로 `DataTable`과 `columnStyles` 배열을 POI의 `importDataTable` 메서드에 전달합니다. `true` 플래그는 POI에게 첫 행을 열 헤더로 취급하도록 알려줍니다.

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **내부에서 무슨 일이 일어나나요?**  
> POI는 각 열을 순회하면서 배열에서 해당 `Style`을 가져와 그 스타일로 셀을 씁니다. 글꼴 색상만 설정했기 때문에 다른 요소(테두리, 배경)는 기본값을 유지합니다—더 많은 꾸밈이 필요하면 스타일을 확장해도 됩니다.

### 단계 5 – 워크북 저장 (선택 사항이지만 권장됨)

가져온 후에는 워크북을 디스크에 저장하거나 클라이언트로 스트리밍하고 싶을 것입니다.

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **예외 상황:** 대상 파일이 이미 존재하면 `FileOutputStream`이 덮어씁니다. 호출을 체크로 감싸거나 UI 환경에서 사용자에게 확인을 요청하세요.

---

## 자주 묻는 질문 및 주의사항

- **글꼴 색상이 아니라 배경 색상이 필요하면?**  
  `setFontColor`를 `setPatternForegroundColor`로 교체하고 스타일에 `setPattern(BackgroundType.SOLID)`를 호출합니다.

- **열이 아니라 행에 동일한 색상 스키마를 적용할 수 있나요?**  
  물론 가능합니다—루프 로직을 바꿔 행을 순회하고 행 인덱스별로 스타일을 할당하면 됩니다.

- **DataTable에 워크시트가 처리할 수 있는 것보다 더 많은 열이 있으면?**  
  Excel은 최대 16,384열(XFD)까지 지원합니다. 이 한도를 초과하면 코드가 예외를 발생시킵니다. `columnCount`를 `SpreadsheetVersion.EXCEL2007.getMaxColumns()`와 비교하여 미리 방지하세요.

- **.xls(Excel 97‑2003) 파일에서도 작동하나요?**  
  네, POI가 포맷을 추상화합니다. 다만 오래된 바이너리 포맷은 색상이 적어 가장 가까운 팔레트 항목으로 대체될 수 있습니다.

---

## 전체 작동 예제

아래는 `org.apache.poi:poi-ooxml:5.2.3`을 이미 포함한 Maven 프로젝트에 붙여넣을 수 있는 독립형 클래스입니다. `getDataTable()`을 실제 데이터 소스를 반환하도록 조정하세요.

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**예상 출력:** `AlternatingColorsReport.xlsx`를 엽니다. A열과 C열(짝수 인덱스)은 텍스트가 파란색으로 표시되고, B열(홀수 인덱스)은 녹색 글꼴을 보여줍니다. 첫 번째 행은 `importDataTable`이 헤더로 인식하기 때문에 굵게 표시됩니다.

---

## 결론

우리는 **import datatable to excel**을 수행하면서 **alternating column colors**와 **set column font color**를 프로그래밍 방식으로 적용하는 데 필요한 모든 내용을 다루었습니다. 이 접근 방식은 가볍고 Apache POI만을 사용하며, 테두리나 셀 배경과 같은 다른 스타일 요구에도 확장할 수 있습니다.

다음과 같은 실험을 고려해 보세요:

- 행에 대한 **Import data with formatting**(교차 행 색상).  
- 높은 점수를 강조하는 **conditional formatting** 추가.  
- 웹 앱을 위해 HTTP 응답으로 직접 내보내기.

패턴을 여러분의 보고 파이프라인에 자유롭게 적용하세요—기본을 마스터하면 한계가 없습니다. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Aspose.Cells Java를 사용한 열 색상으로 Excel 데이터 정렬 방법: 완전 가이드](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [Aspose.Cells for Java를 사용한 Excel 열 보호 마스터: 종합 가이드](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [Aspose.Cells for Java를 사용해 Excel에 열 삽입하기 - 종합 가이드](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}