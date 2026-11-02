---
date: 2026-09-02
description: Aspose.Cells for Java를 사용하여 차트를 PNG로 내보내고, 데이터 시리즈를 추가하고, line column
  chart를 결합하고, 워크북을 XLSX로 저장하며, legend chart를 추가하는 방법을 배웁니다.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: 차트를 PNG로 내보내고 결합 차트에 데이터 시리즈 추가
og_description: Aspose.Cells for Java와 함께 차트를 PNG로 내보내고, line and column chart를 결합하고,
  데이터 시리즈를 추가하며, 워크북을 XLSX로 저장하는 단일 튜토리얼.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: 차트를 PNG로 내보내고 결합 차트에 데이터 시리즈 추가
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: 차트를 PNG로 내보내고 결합 차트에 데이터 시리즈 추가
url: /ko/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG로 차트 내보내기 및 결합 차트를 위한 데이터 시리즈 추가

이 튜토리얼에서는 Excel 워크북에 **데이터 시리즈 추가**하고, **라인 및 컬럼 차트 결합** 요소를 사용하며, Aspose.Cells for Java를 사용하여 **차트를 PNG로 내보내기** 방법을 배웁니다. 워크북 설정, 워크시트에 차트 추가, 범례 사용자 지정, **워크북을 XLSX로 저장** 및 차트의 PNG 이미지 생성까지 모든 단계를 안내합니다. 최종적으로 보고서나 대시보드에 삽입할 수 있는 사용 준비가 된 결합 차트를 얻게 됩니다.

## 빠른 답변
- **어떤 라이브러리가 결합 차트를 생성합니까?** Aspose.Cells for Java.  
- **데이터 시리즈를 어떻게 추가합니까?** 적절한 범위와 함께 `chart.getNSeries().add(...)`를 호출합니다.  
- **차트를 PNG로 어떻게 내보낼 수 있나요?** `chart.toImage("chart.png", ImageFormat.getPng())`를 사용합니다.  
- **워크북을 어떤 파일 형식으로 저장할 수 있나요?** 표준 `.xlsx` (워크북을 XLSX로 저장).  
- **프로덕션에 라이선스가 필요합니까?** 예 – 프로덕션 배포에는 유효한 Aspose.Cells 라이선스가 필요합니다.

## Aspose.Cells에서 차트를 PNG로 내보내는 것이란?
차트를 PNG로 내보내면 Excel 차트의 래스터 이미지가 생성되어 Excel 애플리케이션 없이 웹 페이지, 보고서 또는 이메일에 표시할 수 있습니다. 이 방법은 정확한 시각적 레이아웃, 색상 및 데이터 마커를 캡처하여 휴대 가능한 이미지 파일을 생성합니다.

## 왜 결합 라인-컬럼 차트를 만들까요?
결합 라인‑컬럼 차트를 사용하면 서로 다른 데이터 세트를 구별된 시각적 표현(예: 컬럼 시리즈 위에 라인 시리즈)으로 하나의 뷰에 표시할 수 있습니다. 이 접근 방식은 전체와 추세를 비교하거나, 상관관계를 강조하거나, 시각적 공간을 최소화하면서 풍부한 인사이트를 제공하는 데 이상적입니다.

## 사전 요구 사항
- Java Development Kit (JDK) 8 이상
- Aspose.Cells for Java 라이브러리 (아래 링크에서 다운로드)
- Java 구문 및 Excel 개념에 대한 기본적인 이해

## 시작하기

먼저 공식 사이트에서 Aspose.Cells for Java 라이브러리를 다운로드합니다:

[다운로드 Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR 파일을 프로젝트의 클래스패스에 추가하면 차트 구축을 시작할 수 있습니다.

### 단계 1: aspose.cells 클래스 가져오기
`Workbook`은 메모리 내에서 전체 Excel 파일을 나타내는 Aspose.Cells의 핵심 객체입니다.  
```java
import com.aspose.cells.*;
```

### 단계 2: 새 워크북 만들기
`Worksheet`는 `Workbook` 내부의 단일 시트를 나타내며 셀, 행 및 차트에 대한 접근을 제공합니다.  
```java
Workbook workbook = new Workbook();
```

### 단계 3: 첫 번째 워크시트에 접근하기
`Chart`는 차트와 관련된 모든 설정, 시리즈 및 렌더링 옵션을 보유하는 객체입니다.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 단계 4: 워크시트에 결합 차트 객체 추가
우선 라인 차트로 시작하고 나중에 컬럼 시리즈를 추가하여 **결합 라인 컬럼 차트** 효과를 구현합니다.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 차트에 데이터 추가

차트 컨테이너가 생성되었으므로 이제 데이터로 채워야 합니다.

### 단계 5: 데이터 범위 정의 및 데이터 시리즈 추가
`NSeries`는 차트의 각 데이터 시리즈를 저장하는 컬렉션입니다. 시리즈를 추가하면 셀 범위가 차트와 연결됩니다.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **팁:** 첫 번째 매개변수(`"A1:A5"`)는 첫 번째 시리즈의 범위이며, 두 번째 매개변수(`"B1:B5"`)는 첫 번째와 결합될 두 번째 시리즈를 생성합니다.

### 단계 6: 카테고리 (X‑축) 데이터 설정
`CategoryAxis`는 차트의 수평 축을 나타내며 X‑축에 표시되는 레이블을 제어합니다.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 차트 사용자 지정

좋은 차트는 이야기를 전달합니다. 차트에 제목, 축 레이블 및 명확한 범례를 추가해 보겠습니다.

### 단계 7: 차트 축 레이블 및 제목 설정
`Title`은 차트의 메인 제목을 설정하고, `Axis` 객체는 X 및 Y 축을 나타냅니다.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 단계 8: 차트 범례 추가 및 위치 조정
`Legend`는 차트 내 시리즈 범례의 위치와 모양을 제어합니다.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 차트 저장 및 내보내기

사용자 지정 후에는 **워크북을 XLSX로 저장**하고 이미지를 생성하고 싶을 것입니다.

### 단계 9: 워크북을 Excel 파일(XLSX)로 저장
`Workbook.save`는 메모리 내 워크북을 지정된 형식의 파일로 기록합니다.  
```java
workbook.save("CombinedChart.xlsx");
```

### 단계 10: 차트를 PNG로 내보내기
`Chart.toImage`는 선택한 형식으로 차트를 이미지 파일로 렌더링합니다.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 메서드는 **Excel 차트** 이미지를 생성하여 웹 페이지, 보고서 또는 이메일에 사용할 수 있습니다.

## 일반적인 문제 및 해결 방법

| 문제 | 해결책 |
|-------|----------|
| **데이터가 표시되지 않음** | 차트를 만들기 전에 셀 범위(`A1:A5`, `B1:B5`, `C1:C5`)에 실제로 데이터가 있는지 확인하십시오. |
| **범례가 차트와 겹침** | `chart.getLegend().setOverlay(false)`를 설정하거나 범례를 다른 위치(예: `RIGHT`)로 이동하십시오. |
| **이미지 파일이 비어 있음** | 차트에 최소 하나의 시리즈가 있는지 확인하고, 모든 사용자 지정 후에 `chart.toImage`가 호출되었는지 확인하십시오. |
| **저장 시 예외 발생** | 대상 디렉터리에 대한 쓰기 권한이 있는지, 파일이 Excel에서 열려 있지 않은지 확인하십시오. |

## 자주 묻는 질문

**Q: Aspose.Cells for Java를 어떻게 설치합니까?**  
A: 공식 사이트에서 JAR를 다운로드하고 프로젝트의 클래스패스에 추가합니다. 다운로드 링크: [다운로드 Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: 라인 및 컬럼 외에 다른 차트 유형을 만들 수 있나요?**  
A: 예, Aspose.Cells는 막대, 원형, 산점도, 영역 등 다양한 차트 유형을 지원합니다. 전체 목록은 API 문서를 참조하십시오.

**Q: 프로덕션 사용에 라이선스가 필요합니까?**  
A: 프로덕션 배포에는 유효한 Aspose.Cells 라이선스가 필요합니다. 평가용 무료 체험판을 사용할 수 있습니다.

**Q: 각 시리즈의 색상을 어떻게 변경합니까?**  
A: 시리즈를 추가한 후 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`(또는 유사한 메서드)를 사용합니다.

**Q: 더 많은 코드 예제를 어디서 찾을 수 있나요?**  
A: 포괄적인 문서와 추가 샘플은 Aspose 레퍼런스 사이트에서 확인할 수 있습니다: [Aspose Cells Java 레퍼런스 문서](https://reference.aspose.com/cells/java/).

**마지막 업데이트:** 2026-09-02  
**테스트 환경:** Aspose.Cells for Java 최신 버전  
**작성자:** Aspose

## 관련 튜토리얼

- [Aspose.Cells for Java를 사용하여 Excel 차트에 레이블 추가 방법](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Aspose.Cells for Java를 사용하여 추세선이 포함된 Excel 차트 만들기 및 이미지로 내보내기](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells for Java를 사용하여 Excel 차트를 PDF로 내보내기: 사용자 지정 페이지 크기 안내](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}