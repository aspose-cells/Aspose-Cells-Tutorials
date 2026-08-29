---
date: 2026-08-21
description: Aspose.Cells for Java를 사용하여 Excel 차트에 tooltips와 data labels를 추가하고 chart
  type을 변경하는 방법을 배우세요 – 단계별 가이드와 인터랙티브 예제 포함.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Excel Chart Type 변경
og_description: Aspose.Cells for Java를 사용하여 Excel 차트에 tooltips와 data labels를 추가하고
  chart type을 변경하는 방법을 배우세요 – 단계별 가이드와 인터랙티브 예제 포함.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Java에서 Excel 차트에 tooltips와 data labels 추가하는 방법
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Java에서 Excel 차트에 tooltips와 data labels 추가하는 방법
url: /ko/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 차트에 데이터 레이블 추가 및 차트 유형 변경 – Aspose.Cells Java

대화형 차트는 Excel 보고서에 새로운 수준의 인사이트를 제공하며, **툴팁 추가 방법**은 정보를 즉시 읽을 수 있게 합니다. 이 튜토리얼에서는 **Excel 차트에 데이터 레이블 추가**, **차트 유형 변경**, 그리고 Aspose.Cells를 사용한 대화형 Java 솔루션을 만드는 방법을 배웁니다. 또한 툴팁을 추가하고 간단한 드릴‑다운 하이퍼링크를 제공하여 청중이 데이터를 깊이 탐색할 수 있도록 보여드립니다.

## 빠른 답변
- **사용된 라이브러리는 무엇입니까?** Aspose.Cells for Java  
- **차트 유형을 변경할 수 있나요?** 예 – 차트를 생성할 때 `ChartType` 열거형을 수정하면 됩니다.  
- **차트에 툴팁을 어떻게 추가하나요?** 데이터 레이블 API(`setHasDataLabels(true)`)를 사용하고 값 표시를 활성화합니다.  
- **드릴‑다운이 지원되나요?** 데이터 포인트에 하이퍼링크를 연결하여 기본 드릴‑다운 동작을 구현할 수 있습니다.  
- **전제 조건은?** Java IDE, Aspose.Cells JAR, 그리고 샘플 데이터가 포함된 Excel 파일.  

## 툴팁 추가 방법이란 무엇인가요?
**툴팁 추가 방법**은 Excel 차트에서 데이터 포인트의 값이나 사용자 정의 정보를 표시하는 호버 텍스트를 활성화하는 과정을 말합니다. Aspose.Cells에서는 차트의 데이터 레이블 설정을 통해 이를 구현합니다. 툴팁은 차트를 복잡하게 만들지 않으면서 사용자가 데이터를 빠르게 이해하도록 도와주며, 글꼴, 색상 및 형식으로 맞춤 설정할 수 있습니다.

## 왜 Aspose.Cells와 함께 대화형 차트를 사용하나요?
Aspose.Cells는 **50개 이상의 입력 및 출력 형식**(XLSX, CSV, PDF, HTML 등)을 지원하며, 전체 파일을 메모리에 로드하지 않고도 **1 000개 이상의 시트**가 포함된 워크북을 처리할 수 있어 엔터프라이즈 보고를 위한 빠른 서버‑사이드 차트 생성을 제공합니다. 대화형 차트는 하이퍼링크 삽입, 동적 데이터 업데이트, 웹 친화적 형식으로의 내보내기를 가능하게 하여 대시보드 및 보고 포털에 이상적입니다.

## 전제 조건

시작하기 전에 다음이 준비되어 있는지 확인하십시오:

- Java 개발 환경 (JDK 8+ 권장)  
- Aspose.Cells for Java 라이브러리 ([Aspose.Cells for Java 다운로드 페이지](https://releases.aspose.com/cells/java/)에서 다운로드)  
- 시각화하려는 데이터가 포함된 샘플 워크북(`data.xlsx`)  

## 단계 1: Java 프로젝트 설정

1. 선호하는 IDE(IntelliJ IDEA, Eclipse 등)에서 새 Java 프로젝트를 생성합니다.  
2. Aspose.Cells JAR를 프로젝트의 빌드 경로나 Maven/Gradle 의존성에 추가합니다.

## 단계 2: 데이터 로드

차트를 사용하려면 먼저 워크북을 메모리에 로드해야 합니다.

`Workbook` 클래스는 Excel 파일을 나타내며, `Worksheet`는 해당 파일 내의 단일 시트를 나타냅니다.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Aspose.Cells에서 차트 유형을 변경하는 방법

원하는 `ChartType` 열거형으로 새 차트를 생성합니다; Aspose.Cells는 기존 차트의 유형을 제자리에서 수정하지 않으므로 올바른 유형의 새 차트를 추가하고 필요에 따라 기존 차트를 제거해야 합니다. 이 방법은 모든 시리즈와 축이 새로운 시각적 표현에 맞게 올바르게 재구성되도록 보장합니다.

## 단계 3: 차트 생성 (및 유형 변경)

분석에 맞는 차트 유형을 선택할 수 있습니다. 아래에서는 **컬럼 차트**를 만들지만, `ChartType` 열거형을 변경하면 라인, 파이, 또는 바 차트로 쉽게 전환할 수 있습니다.

`Chart` 객체는 워크시트에서 데이터의 시각적 표현을 구성하는 메서드를 제공합니다.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **프로 팁:** Excel 차트 유형을 **변경하려면**, `ChartType.COLUMN`을 `ChartType.LINE`, `ChartType.PIE` 등으로 교체합니다.

## Excel 차트에 툴팁을 추가하는 방법

차트를 로드하고 데이터 레이블을 활성화한 뒤 `showValue` 플래그를 설정합니다. 그러면 사용자가 렌더링된 Excel 파일이나 HTML 뷰에서 데이터 포인트 위에 마우스를 올릴 때 툴팁이 해당 셀 값을 표시합니다. 또한 보고서 스타일에 맞게 툴팁의 글꼴, 색상 및 배경을 맞춤 설정할 수 있습니다.

`DataLabel` 클래스는 데이터 레이블의 모양과 내용을 제어하며, 이는 툴팁 역할도 합니다.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## 단계 4: 대화형 기능 추가

### 4.1. 툴팁 추가 (차트에 툴팁 추가)

사용자가 데이터 포인트 위에 마우스를 올리면 툴팁이 표시됩니다. 아래 코드는 데이터 레이블을 활성화하고 값을 툴팁으로 표시합니다.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. 데이터 레이블 추가 – **Excel 차트에 데이터 레이블 추가**

데이터 레이블은 차트 자체에 영구적인 시각적 표시를 제공합니다. 가독성을 높이기 위해 콜아웃 형태로 표시할 수 있습니다.

`DataLabel` 클래스는 각 시리즈의 레이블 모양을 제어합니다. `setHasDataLabels(true)`를 호출하고 `setShowValue(true)`와 같은 속성을 구성하면 숫자 값을 차트에 직접 삽입하여 별도의 상호작용 없이 즉시 표시됩니다. 추가 옵션을 사용하면 시리즈 이름, 백분율 또는 사용자 정의 텍스트를 표시하여 더 풍부한 컨텍스트를 제공할 수 있습니다.

> **데이터 레이블을 추가하는 이유는?** 차트에 직접 데이터 레이블을 포함하면 사용자가 마우스를 올리거나 값을 추측할 필요가 없어 보고서의 명확성이 향상됩니다.

### 4.3. 드릴‑다운 구현 (데이터 포인트에 하이퍼링크)

드릴‑다운 기능을 추가하는 간단한 방법은 특정 포인트에 하이퍼링크를 연결하는 것입니다. 포인트를 클릭하면 상세 정보가 포함된 웹 페이지가 열립니다.

`Hyperlink` 클래스는 차트 요소에 클릭 가능한 링크를 연결하여 드릴‑다운 탐색을 가능하게 합니다.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Excel 차트에 데이터 레이블을 추가하는 방법

`DataLabel` 클래스는 각 시리즈의 레이블 모양을 제어합니다. `setHasDataLabels(true)`를 호출하고 `setShowValue(true)`와 같은 속성을 구성하면 숫자 값을 차트에 직접 삽입하여 별도의 상호작용 없이 즉시 표시됩니다. 추가 옵션을 사용하면 시리즈 이름, 백분율 또는 사용자 정의 텍스트를 표시하여 더 풍부한 컨텍스트를 제공할 수 있습니다.

## 단계 5: 워크북 저장

차트를 구성한 후 워크북을 저장하여 대화형 기능이 출력 파일에 저장되도록 합니다.

`workbook.save`를 호출하면 수정된 워크북이 선택한 형식의 파일로 기록됩니다.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 일반적인 문제 및 해결책

| 문제 | 해결책 |
|-------|----------|
| **툴팁이 표시되지 않음** | `setHasDataLabels(true)`를 `setShowValue(true)`를 구성하기 전에 호출했는지 확인하십시오. |
| **하이퍼링크가 클릭되지 않음** | 출력 형식이 하이퍼링크를 지원하는지 확인하십시오(예: XLSX, CSV는 아님). |
| **차트 유형이 변경되지 않음** | 차트를 추가할 때 올바른 `ChartType` 열거형을 수정했는지 다시 확인하십시오. |

## 자주 묻는 질문

**Q: 차트가 생성된 후 차트 유형을 어떻게 변경할 수 있나요?**  
A: 원하는 `ChartType`으로 새 차트를 생성해야 합니다. Aspose.Cells는 제자리 변환을 제공하지 않으므로 기존 차트를 제거하고 새 차트를 추가합니다.

**Q: 툴팁의 모양을 맞춤 설정할 수 있나요?**  
A: 예. `setFontSize`, `setFontColor`, `setBackgroundColor`와 같은 `DataLabel` 속성을 사용하여 툴팁 텍스트를 스타일링합니다.

**Q: 웹 애플리케이션에서 사용자 상호작용을 어떻게 처리하나요?**  
A: 워크북을 HTML 또는 XLSX 파일로 내보낸 후 클라이언트 측에서 JavaScript를 사용해 차트 요소의 클릭 이벤트를 캡처합니다.

**Q: 더 많은 예제와 문서는 어디서 찾을 수 있나요?**  
A: 차트 관련 클래스와 메서드 전체 목록은 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)를 방문하십시오.

## 결론

이제 **Excel 차트에 데이터 레이블 추가**, **Excel 차트 유형 변경**, **대화형 차트 Java 솔루션 생성** 방법을 알고 있으며, Aspose.Cells for Java를 사용해 툴팁, 데이터 레이블 및 드릴‑다운 하이퍼링크로 차트를 풍부하게 만들 수 있습니다. 이러한 향상은 Excel 보고서를 최종 사용자에게 더욱 매력적이고 통찰력 있게 만듭니다.

---

**마지막 업데이트:** 2026-08-21  
**테스트 환경:** Aspose.Cells for Java 24.12  
**작성자:** Aspose

## 관련 튜토리얼

- [Aspose.Cells for Java를 사용하여 Excel 차트 및 데이터 레이블 수정하는 방법](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Aspose.Cells Java를 사용하여 Excel 차트 축 레이블 추출하기: 종합 가이드](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Aspose.Cells for Java를 사용하여 Excel에서 버블 차트 만들기: 단계별 가이드](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}