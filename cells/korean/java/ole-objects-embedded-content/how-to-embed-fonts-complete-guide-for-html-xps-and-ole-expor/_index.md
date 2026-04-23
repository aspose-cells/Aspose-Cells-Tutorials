---
category: general
date: 2026-03-01
description: HTML 및 기타 형식에 글꼴을 삽입하는 방법을 배워보세요. 단계별 튜토리얼에서는 HTML에 글꼴 삽입, Excel을 HTML로
  변환, OLE 내보내는 방법, 그리고 Excel을 XPS로 변환하는 내용을 다룹니다.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: ko
og_description: HTML, XPS 및 OLE 내보내기에서 글꼴을 삽입하는 방법. 전체 워크플로를 배우고 실행 가능한 Java 코드를 확인하며,
  Excel 변환을 위한 HTML 글꼴 삽입을 마스터하세요.
og_title: 글꼴 삽입 방법 – 전체 Java 튜토리얼
tags:
- Aspose.Cells
- Java
- Document Export
title: 글꼴 삽입 방법 – HTML, XPS 및 OLE 내보내기를 위한 완전 가이드
url: /ko/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML, XPS 및 OLE 내보내기를 위한 폰트 삽입 완전 가이드

Excel 워크북을 웹 페이지나 인쇄 가능한 문서로 변환할 때 **폰트를 삽입하는 방법**이 궁금하셨나요? 혼자가 아닙니다. 많은 개발자들이 출력은 자신의 머신에서는 정상인데 다른 환경에서는 필요한 폰트가 없어 깨지는 문제에 부딪히곤 합니다.

이 튜토리얼에서는 Aspose.Cells for Java를 사용한 실제 시나리오를 단계별로 살펴봅니다: HTML에 폰트를 삽입하고, XPS로 변환할 때 이모지 변형 선택자를 보존하며, PPTX로 내보낼 때 OLE 객체를 편집 가능하게 유지합니다. 최종적으로 “폰트를 삽입하는 방법”에 대한 확실한 복사‑붙여넣기 솔루션을 제공하며 **embed fonts in html**, **convert excel to html**, **how to export ole**, **convert excel to xps**와 같은 주제도 다룹니다.

## 사전 요구 사항

- Java 17 (또는 최신 JDK)  
- Aspose.Cells for Java 25.x 이상  
- 개발 IDE (IntelliJ IDEA, Eclipse, 또는 VS Code)  
- Excel 데이터 구조에 대한 기본적인 이해  

외부 서비스가 필요하지 않습니다—모든 작업이 로컬에서 실행됩니다.

## 솔루션 개요

1. **워크북 생성** 및 `WRAPCOLS` 함수를 사용해 세로 범위를 3열 레이아웃으로 변환합니다.  
2. **워크북을 XPS로 저장**하면서 폰트 변형 선택자를 활성화해 이모지가 손상되지 않도록 합니다.  
3. **HTML로 내보내기** 시 폰트를 삽입하여 페이지가 모든 환경에서 동일하게 보이도록 보장합니다.  
4. **OLE 객체가 포함된 워크북을 PPTX로 내보내기**, 편집 가능성을 유지합니다.  
5. **스마트 마커 템플릿 적용**으로 마스터‑디테일 데이터 바인딩을 시연합니다.  

![폰트 삽입 방법 일러스트레이션](image.png "폰트 삽입 방법")

*이미지 대체 텍스트: Excel에서 HTML, XPS 및 PPTX로의 워크플로를 보여주는 폰트 삽입 다이어그램.*

---

## 단계 1 – 워크북 생성 및 WRAPCOLS 사용 (embed fonts in html와 관련된 이유)

폰트를 삽입하기에 앞서 실제 데이터가 들어 있는 워크북이 필요합니다. `WRAPCOLS` 함수는 하나의 열을 여러 열로 나누는 편리한 방법으로, 최종 HTML을 보다 읽기 쉽게 만들 수 있습니다.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**왜 이 단계인가?**  
`WRAPCOLS` 호출은 나중에 HTML에서 테이블로 나타나는 다중 열 범위를 생성합니다. 이후 **embed fonts in html**을 수행하면 테이블 스타일이 삽입한 폰트에 의존하게 되어 브라우저 간 일관된 렌더링을 보장합니다.

---

## 단계 2 – 이모지를 보존하면서 워크북을 XPS로 저장 (convert excel to xps)

인쇄용 포맷이 필요하다면 XPS가 좋은 선택입니다. 하지만 최신 문서에는 변형 선택자를 사용하는 이모지나 기호가 포함되는 경우가 많습니다. `EnableFontVariationSelectors`를 활성화하면 이러한 문자들이 변환 과정에서도 유지됩니다.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**얻는 결과:**  
임베드된 이모지가 원본 워크북과 동일하게 표시되는 XPS 파일을 얻습니다. 이는 **convert excel to xps** 요구 사항을 충족시키며 폰트 처리가 HTML에만 국한되지 않음을 보여줍니다.

---

## 단계 3 – 폰트를 삽입한 HTML로 내보내기 (how to embed fonts & embed fonts in html)

이제 튜토리얼의 핵심인 Excel을 HTML로 변환할 때 **폰트를 삽입하는 방법**을 살펴봅니다. Aspose.Cells를 사용하면 생성된 HTML 파일에 폰트를 직접 삽입할 수 있어 외부 폰트 파일이 필요하지 않습니다.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**작동 방식:**  
`setEmbedFonts(true)`는 렌더러에게 워크북에서 사용된 폰트 파일을 읽어 `<style>` 태그 내부에 Base64‑인코딩된 `@font-face` 규칙으로 삽입하도록 지시합니다. 결과 HTML은 자체 포함형이므로 어떤 서버에 배포해도 폰트가 올바르게 렌더링됩니다—이는 개발자들이 **how to embed fonts**를 검색할 때 기대하는 바로 그 해결책입니다.

**예상 출력 스니펫 (`embeddedFonts.html` 내부):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

`@font-face` 규칙을 확인하세요—이것이 **embed fonts in html**에 대한 구체적인 답변입니다.

---

## 단계 4 – OLE 객체가 포함된 워크북을 PPTX로 내보내기 (how to export ole)

많은 비즈니스 보고서에서는 Word 문서, PDF 또는 다른 Excel 시트를 OLE 객체로 삽입합니다. 이러한 워크북을 PowerPoint로 내보낼 경우 객체 편집 기능이 사라지는 경우가 많습니다. Aspose.Cells는 기본적으로 편집 가능성을 유지합니다.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**왜 중요한가:**  
**how to export ole**를 찾고 있다면, 이 스니펫이 정확한 API 호출을 보여줍니다. 결과 PowerPoint 슬라이드에는 OLE 객체가 실시간으로 두 번 클릭해 편집할 수 있는 컴포넌트로 포함되어 있어 추가 후처리가 필요 없습니다.

---

## 단계 5 – 스마트 마커 템플릿 적용 (master‑detail) 및 데모 마무리

스마트 마커를 사용하면 데이터 소스(Map, JSON, DataTable)를 Excel 템플릿에 직접 바인딩할 수 있습니다. 아래는 마스터‑디테일 행을 출력하는 최소 예제입니다.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**결과:**  
템플릿 자리표시자가 데이터로 교체된 새로운 워크북(`smartMarkerResult.xlsx`)이 생성됩니다. 이 단계는 폰트와 직접적인 관련은 없지만, 일반적인 보고 워크플로를 보여줌으로써 **embed fonts in html** 내보내기 전에 자주 수행되는 과정을 완성합니다.

---

## 흔히 발생하는 문제 및 전문가 팁 (폰트 삽입 성공 보장)

| 문제 | 발생 원인 | 해결 방법 |
|-------|----------------|-----|
| HTML 파일에 폰트가 누락됨 | 워크북이 서버에 설치되지 않은 시스템 폰트를 사용하고 있습니다. | 데이터 로드 전에 `Workbook.getSettings().setDefaultFont("Arial")`을 사용하거나, 필요한 폰트 파일을 수동으로 삽입하세요. |
| 출력 HTML 파일이 너무 큼 | 많은 대용량 폰트를 삽입하면 파일 크기가 크게 증가합니다. | 실제로 사용하는 폰트만 삽입하도록 제한하세요: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| XPS 변환 후 이모지 사라짐 | 기본적으로 변형 선택자가 제거됩니다. | Step 2에서와 같이 `settings.setEnableFontVariationSelectors(true)`를 활성화하세요. |
| PPTX에서 OLE 객체가 정적 이미지로 변환됨 | 원본 워크북이 `setSuppressOLEObjects(true)`와 함께 저장되었습니다. | PPTX로 저장할 때 OLE 객체를 **억제하지 않도록** 하세요. |

---

## 결과 확인

1. Chrome/Firefox에서 `embeddedFonts.html`을 엽니다. 해당 폰트가 머신에 설치되지 않았더라도 테이블이 삽입된 폰트(예: Arial)로 표시되어야 합니다.  
2. Windows XPS Viewer에서 `withVariations.xps`를 엽니다. 👍와 같은 이모지가 올바르게 렌더링되어야 합니다.  
3. PowerPoint에서 `oleEditable.pptx`를 엽니다. OLE 도형을 두 번 클릭합니다;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}