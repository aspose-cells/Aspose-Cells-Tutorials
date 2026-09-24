---
category: general
date: 2026-03-01
description: Aspose.Cells for Java를 사용하여 PDF를 생성하고 워크북을 PDF로 저장하는 방법, Excel을 HTML로
  내보내는 방법, 그리고 확장 기능을 사용하는 방법. 단계별 코드 포함.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: ko
og_description: Aspose.Cells for Java를 사용하여 워크북에서 PDF를 만드는 방법. 워크북을 PDF로 저장하고, Excel을
  HTML로 내보내며, EXPAND 함수를 사용하는 방법을 배웁니다.
og_title: 워크북에서 PDF 생성 방법 – Java 튜토리얼
tags:
- Aspose.Cells
- Java
- PDF generation
title: 워크북에서 PDF 만들기 – 완전한 Java 가이드
url: /ko/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크북에서 PDF 만들기 – 완전한 Java 가이드

Excel 워크북에서 서드‑파티 변환기를 사용하지 않고 **PDF를 만드는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 빠른 PDF 내보내기, HTML 미리보기, 혹은 고급 배열 수식이 한 번에 필요할 때 벽에 부딪히곤 합니다.  

이 튜토리얼에서는 바로 그 작업을 수행하는 단일, 독립형 Java 프로그램을 단계별로 살펴보겠습니다. **워크북을 PDF로 저장**하고, 동결된 행을 유지하면서 **Excel을 HTML로 내보내는 방법**을 보여주며, 워크시트 내에서 **EXPAND 함수 사용**을 시연합니다. 마지막까지 진행하면 Maven이나 Gradle 빌드에 바로 넣어 사용할 수 있는 실행 가능한 프로젝트를 얻게 됩니다.

> **Pro tip:** 아래 모든 코드는 Aspose.Cells 23.10(이상)에서 작동합니다. 이전 버전을 사용 중이라면 일부 메서드 이름이 약간 다를 수 있습니다.

---

## Prerequisites

- **Java 17**(또는 다른 LTS 버전)이 설치되고 설정되어 있어야 합니다.
- **Aspose.Cells for Java** 라이브러리. 다음 Maven 의존성을 `pom.xml`에 추가하십시오:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- 선호하는 IDE 또는 텍스트 편집기(IntelliJ IDEA, VS Code, Eclipse 등).

외부 API나 웹 서비스 없이 순수 Java와 Aspose.Cells SDK만 사용합니다.

---

## Overview of the Solution

구현을 **일곱 개의 논리적 단계**로 나눕니다:

1. 워크북을 생성하고 **EXPAND** 함수를 시연합니다.  
2. 폰트 변형 선택자를 활성화하고 **워크북을 PDF로 저장**합니다.  
3. 동결된 행을 유지하면서 동일한 워크북을 HTML로 내보냅니다.  
4. `IF`‑파라미터가 있는 Smart Marker를 사용해 조건부 텍스트를 삽입합니다.  
5. 계층형 데이터를 위한 마스터‑디테일 Smart Marker를 적용합니다.  
6. Base‑64‑인코딩된 이미지가 포함된 Markdown 파일을 로드합니다.  
7. 정렬 및 테두리를 위한 GridJs 옵션을 구성하고 데이터를 삽입합니다.

각 단계는 별도의 메서드로 감싸 `main` 메서드를 깔끔하게 유지하고, **무엇을** 입력하는지뿐 아니라 **왜** 그렇게 하는지를 보여줍니다.

---

## Step 1 – Create a Workbook and Use the EXPAND Function

**EXPAND** 함수는 Office 365에서 도입된 새로운 동적 배열 수식입니다. 셀을 수동으로 복사하지 않고도 범위를 더 큰 영역으로 자동으로 확장할 수 있습니다.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**이것이 중요한 이유:**  
- `EXPAND`는 결과를 자동으로 빈 셀로 채워주므로, 이후 **워크북을 PDF로 저장**할 때 깨끗하고 직사각형 형태의 테이블이 PDF에 표시됩니다.  
- `calculateFormula()`를 호출하면 내보내기 전에 수식 엔진이 실행됩니다.

---

## Step 2 – Enable Font Variation Selectors and **Save Workbook as PDF**

고급 타이포그래피(예: 이모지 또는 CJK 변형 선택자)를 지원해야 한다면, 저장하기 **전에** 해당 기능을 활성화해야 합니다.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**핵심 포인트:** 여기서 주요 키워드 **how to create pdf**에 대한 답을 얻을 수 있습니다—설정을 마친 후 `workbook.save(..., SaveFormat.PDF)`를 호출하면 됩니다.

---

## Step 3 – **Export Excel to HTML** While Preserving Frozen Rows

종종 이해관계자들이 빠른 웹 미리보기를 요구합니다. Aspose.Cells는 HTML로 내보낼 수 있으며, `setPreserveFrozenRows(true)`를 사용하면 Excel과 동일한 스크롤 경험을 유지합니다.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**왜 중요한가:** 동결된 행은 사용성 향상 요소입니다; 없으면 사용자가 페이지를 스크롤할 때 헤더 행이 사라집니다.

---

## Step 4 – Smart Marker with an IF‑Parameter

Smart Marker는 루프를 작성하지 않고도 데이터를 템플릿에 병합할 수 있게 해줍니다. `if`‑파라미터를 사용하면 마커 안에 직접 조건 로직을 추가할 수 있습니다.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

출력 PDF는 `IsVIP`가 `true`이므로 **“VIP Customer: Acme Corp”** 라고 표시됩니다. 플래그를 `false`로 바꾸면 **“Regular Customer: Acme Corp”** 가 표시되며, 추가 코드는 필요 없습니다.

---

## Step 5 – Master‑Detail Smart Marker Using a Hierarchical Range

부모‑자식 데이터(예: 주문 및 라인 아이템)가 있을 때, 마스터‑디테일 마커를 사용하면 수동으로 행을 삽입할 필요가 없습니다.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**얻는 이점:** 엔진이 각 주문에 대해 마스터 행을 확장하고, 상세 행을 자동으로 그 아래에 중첩시킵니다—청구서나 구매 보고서에 이상적입니다.

---

## Step 6 – Load a Markdown Document with Embedded Base‑64 Images

소스 데이터가 Markdown에 있다면(문서 파이프라인에서 흔함), Aspose.Cells가 이를 바로 워크북에 렌더링할 수 있습니다.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**예외 상황 주의:** Base‑64 문자열이 잘못된 경우, Aspose는 이미지를 건너뛰고 문서의 나머지 부분을 계속 처리합니다—크래시가 발생하지 않습니다.

---

## Step 7 – Configure GridJs Options and Insert Data

GridJs는 Aspose가 HTML로 렌더링할 수 있는 가벼운 JavaScript 그리드입니다. 숫자를 정렬하고 테두리를 적용하면 가독성이 향상됩니다.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**왜 중요한가:** 적절한 정렬과 테두리는 생성된 HTML을 깔끔한 스프레드시트처럼 보이게 하여 대시보드에 유용합니다.

---

## Putting It All Together – The `main` Method

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}