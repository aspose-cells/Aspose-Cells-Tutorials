---
category: general
date: 2026-08-20
description: Aspose.Cells를 사용하여 Java에서 차트를 docx로 내보내고 Excel 워크북을 docx로 변환하는 방법을 배웁니다.
  전체 코드가 포함된 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: ko
lastmod: 2026-08-20
og_description: Aspose.Cells for Java를 사용하여 차트를 docx로 내보내고 Excel 워크북을 docx로 변환합니다.
  이 완전하고 실행 가능한 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Aspose.Cells로 차트를 docx에 내보내기 – Java 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Aspose.Cells for Java를 사용하여 Excel에서 차트를 docx로 내보내는 방법
url: /ko/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 통합 문서에서 Java를 사용해 차트를 DOCX로 내보내기

Excel 파일에서 **차트를 DOCX로 직접 내보내야** 할 때, 이 튜토리얼은 바로 실행 가능한 솔루션을 제공합니다. 가이드가 끝날 때쯤에는 **Excel 통합 문서를 DOCX로 변환**하면서 편집 가능한 차트를 유지하는 방법도 알게 되며, 결과 Word 문서는 품질 손실 없이 수정할 수 있습니다.

차트 내보내기는 스프레드시트 계산과 풍부한 Word 레이아웃을 결합한 보고서를 생성할 때 흔히 필요합니다. Aspose.Cells for Java는 변환을 간단하게 해 주며, API를 통해 차트를 편집 가능하게 유지할 수 있습니다—정적 이미지가 필요 없습니다.

## 이 튜토리얼에서 다루는 내용

* 차트를 포함한 기존 통합 문서 로드  
* `ImageOrPrintOptions`를 DOCX 형식에 맞게 구성  
* `ExportEditableCharts` 플래그 활성화 (버전 25.10부터 사용 가능)  
* 편집 가능한 차트를 유지한 채 통합 문서를 DOCX 파일로 저장  

Aspose.Cells JAR 외에 별도의 도구가 필요하지 않습니다. 코드는 Java 8+ 및 최신 Aspose.Cells 버전에서 동작합니다.

## 사전 요구 사항

| 요구 사항 | 이유 |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 이상) | `setExportEditableCharts` 기능이 이 릴리스에 도입되었습니다. |
| **Java Development Kit (JDK) 8 이상** | 예제 컴파일 및 실행을 위한 런타임을 제공합니다. |
| **차트가 하나 이상 포함된 Excel 통합 문서 (`.xlsx`)** | 차트가 DOCX로 내보내질 대상 객체입니다. |
| **Java IDE 또는 빌드 도구 (예: Maven, Gradle)** | 의존성 관리 및 실행을 간소화합니다. |

최신 Aspose.Cells JAR는 [Aspose 웹사이트](https://products.aspose.com/cells/java/)에서 다운로드할 수 있습니다.

## 1단계: 프로젝트 설정 및 Aspose.Cells 의존성 추가

Maven을 사용하는 경우 `pom.xml`에 다음 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Gradle을 사용하는 경우 다음을 추가합니다:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** `ExportEditableCharts`를 도입한 정확한 버전(25.10) 또는 그 이후 버전을 사용하세요. 이전 버전은 플래그를 무시하고 정적 이미지가 생성됩니다.

## 2단계: 차트를 포함한 통합 문서 로드

`Workbook` 클래스는 전체 Excel 파일을 나타냅니다. 로드 작업은 한 줄로 수행됩니다:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **왜 중요한가:** 내보내기 옵션을 적용하려면 통합 문서가 완전히 로드되어 있어야 합니다. 파일 경로가 잘못되면 Aspose.Cells가 `FileNotFoundException`을 발생시킵니다.

## 3단계: DOCX 출력용 이미지/인쇄 옵션 구성

`ImageOrPrintOptions`는 통합 문서가 어떻게 렌더링될지를 제어합니다. 저장 형식을 `DOCX`로 설정하면 Aspose.Cells가 이미지가 아닌 Word 문서를 생성합니다.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

여기서 페이지 크기, DPI, 이미지 품질 등을 조정할 수 있지만 차트 내보내기에는 선택 사항입니다.

## 4단계: 편집 가능한 차트 내보내기 활성화

버전 25.10부터 Aspose.Cells는 차트를 네이티브 Word 차트 객체로 삽입할 수 있습니다. 이렇게 하면 Microsoft Word에서 완전히 편집할 수 있습니다.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** 이 플래그를 `false`로 설정하거나 생략하면 차트가 정적 이미지로 렌더링됩니다. 변환 후 차트를 편집해야 하는 경우에만 `true`로 설정하세요.

## 5단계: 통합 문서를 DOCX 파일로 저장

마지막으로 구성한 옵션을 사용해 `Workbook.save`를 호출합니다:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

프로그램이 종료되면 Microsoft Word에서 `ChartEditable.docx`를 엽니다. 원본 차트가 표시되고, 차트를 오른쪽 클릭하면 **Edit Data** 옵션이 나타나 차트가 실제로 편집 가능함을 확인할 수 있습니다.

## 전체 실행 가능한 예제

아래는 완전한 소스 파일입니다. IDE에 복사하고 `YOUR_DIRECTORY`를 절대 경로나 상대 경로로 바꾼 뒤 실행하세요.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**예상 결과**

* 지정된 디렉터리에 `ChartEditable.docx` 파일이 생성됩니다.  
* Word에서 파일을 열면 차트가 Excel에서 보였던 그대로 표시되고, 차트를 더블 클릭하면 데이터 시리즈를 편집할 수 있습니다.

## 흔히 발생하는 문제와 해결 방법

| 증상 | 원인 | 해결 방법 |
|---------|-------|-----|
| Word에서 **정적 이미지**가 표시됨 | `setExportEditableCharts`를 호출하지 않았거나 25.10 미만 버전 사용 | 플래그를 `true`로 설정하고 Aspose.Cells 25.10 이상을 사용하세요. |
| 생성된 DOCX가 **빈 파일**임 | 원본 통합 문서 경로 오류 또는 권한 부족 | 통합 문서 경로를 확인하고 읽기/쓰기 권한을 확인하세요. |
| 차트 레이아웃이 **왜곡**됨 | Excel의 페이지 설정(숨긴 행/열 등)이 Word 기본값과 다름 | `ImageOrPrintOptions`(예: `setOnePagePerSheet(true)`)를 조정해 스케일링을 제어하세요. |
| 큰 통합 문서에서 **성능 저하** | 많은 차트 또는 대용량 데이터 세트 내보내기 | 필요한 시트만 내보내거나 `setSheetIndex`로 처리 범위를 제한하세요. |

## 솔루션 확장하기

* **다중 차트:** 모든 워크시트를 순회하고 `worksheet.getCharts()`를 호출해 각 차트를 개별적으로 내보냅니다.  
* **맞춤 DOCX 스타일링:** 저장 후 Aspose.Words를 사용해 헤더, 푸터 또는 스타일을 적용합니다.  
* **배치 변환:** 코드를 루프로 감싸 `.xlsx` 파일이 있는 디렉터리를 처리해 각각 DOCX를 생성합니다.

## 결론

이제 **차트를 DOCX로 내보내기**와 **Excel 통합 문서를 DOCX로 변환**하면서 차트의 완전한 편집 가능성을 유지하는 신뢰할 수 있는 방법을 알게 되었습니다. 핵심 단계는 통합 문서 로드, `ImageOrPrintOptions`를 DOCX용으로 구성, `ExportEditableCharts` 활성화, 그리고 결과 저장입니다.

페이지 여백 설정이나 통합 문서 수식 삽입 등 추가 옵션을 실험해 보고, Excel 데이터를 프로그래밍 방식으로 Word 보고서에 활용할 때 이 접근법을 활용해 보세요.

--- 

*시도해 볼 준비가 되셨나요? 예제를 복제하고 파일 경로를 업데이트한 뒤 프로그램을 실행해 보세요. 문제가 발생하면 Aspose.Cells for Java 문서를 참고하거나 아래 관련 주제를 살펴보세요.*  

### 다음에 탐색할 관련 주제

* **excel 통합 문서를 pdf로 변환** – 동일한 통합 문서에서 PDF 보고서를 생성합니다.  
* **Aspose.Cells 차트 서식 지정** – 내보내기 전에 색상, 마커, 축 등을 맞춤 설정합니다.  
* **Aspose.Words를 사용해 DOCX에 이미지 삽입** – 차트를 다른 Word 콘텐츠와 결합합니다.  

Happy coding!


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스에는 단계별 설명과 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용해 추세선이 포함된 Excel 차트를 만들고 이미지로 내보내는 방법](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells Java로 Excel 차트에 자동으로 접근하는 단계별 가이드](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Aspose.Cells for Java로 Excel 차트 데이터 레이블 맞춤 설정하기 단계별 가이드](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}