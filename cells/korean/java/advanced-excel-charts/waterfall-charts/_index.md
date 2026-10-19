---
date: 2026-09-02
description: Aspose.Cells를 사용하여 Java에서 Excel 워터폴 차트를 만드는 방법을 배우고, 차트 데이터 범위를 설정하고,
  레이블을 사용자 정의하며, XLSX로 내보내는 방법을 알아보세요.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: 워터폴 차트
og_description: Aspose.Cells for Java를 사용하여 Excel 워터폴 차트를 만들고, 차트 데이터 범위를 설정하고, 데이터
  레이블을 추가하며, 몇 단계만에 XLSX로 내보냅니다.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Aspose.Cells for Java를 사용하여 Excel 워터폴 차트 만들기
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Aspose.Cells for Java를 사용하여 Excel 워터폴 차트 만들기
url: /ko/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워터폴 차트

## Aspose.Cells for Java를 사용한 워터폴 차트 소개

이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 **excel 워터폴 차트 만들기**와 **차트 데이터 범위 설정** 방법을 배웁니다. 워터폴 차트는 일련의 양수 및 음수 값을 명확한 시각적 스토리로 변환하여 재무제표, 판매 실적 검토 및 개별 항목이 전체에 어떻게 기여하는지 확인해야 하는 모든 시나리오에 이상적입니다.

## 빠른 답변
- **What is a waterfall chart?** 초기 값이 일련의 중간 값에 의해 증가 및 감소하여 최종 합계에 도달하는 방식을 시각화한 차트입니다.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** 개발용으로는 무료 체험판으로 충분하지만, 운영 환경에서는 상용 라이선스가 필요합니다.  
- **Can I save the file as XLSX?** 예 – `workbook.save("FileName.xlsx")`를 사용합니다.  
- **Is it suitable for Java data visualization?** 물론입니다; Aspose.Cells는 Office 없이도 풍부한 차트 기능을 제공합니다.

## 워터폴 차트란?
워터폴 차트는 시작 값에 순차적인 양수 및 음수 기여도를 표시하여 각 구성 요소가 전체 결과에 어떻게 영향을 미치는지 이해하도록 도와줍니다. 이득과 손실을 나란히 시각화함으로써 복잡한 재무 흐름을 즉시 읽을 수 있게 합니다.

## 워터폴 차트를 추가하기 위해 Aspose.Cells for Java를 사용하는 이유
Aspose.Cells는 Microsoft Excel이 설치되지 않은 서버, CI 파이프라인 또는 데스크톱에서도 Excel 차트를 생성할 수 있게 해줍니다. **15개 이상의 출력 형식**(XLSX, PDF, HTML, CSV 등)을 지원하고, **500개 이상의 행**을 1초 이내에 처리하며, 색상부터 데이터 레이블까지 차트 요소를 프로그래밍 방식으로 제어할 수 있습니다.

## 사전 요구 사항

코드 작성을 시작하기 전에 다음 사전 요구 사항을 확인하십시오:

- Aspose.Cells for Java: Aspose.Cells for Java가 설치되어 있어야 합니다. Aspose.Cells for Java 릴리스 페이지에서 다운로드할 수 있습니다: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java 개발 환경: 시스템에 Java가 설치되어 있고, 빌드 도구(Maven/Gradle)가 준비되어 있어야 합니다.

이제 단계별로 워터폴 차트를 만드는 방법을 시작해 보겠습니다.

## Java에서 워터폴 차트의 차트 데이터 범위를 설정하는 방법
새 워크북을 로드하고 데이터를 채운 뒤 `Chart` 객체를 추가하고, 시리즈 범위를 정의한 후 파일을 저장합니다. 이 과정은 간단합니다: 워크북을 생성하고, 카테고리와 값을 셀에 채운 뒤 차트를 만들고, 데이터 범위를 바인딩하고, 워크북을 내보냅니다. 결과는 보고서나 대시보드에서 사용할 수 있는 완전한 워터폴 차트입니다.

### 단계 1: Aspose.Cells 가져오기
`com.aspose.cells` 패키지는 워크북 생성, 워크시트 처리 및 차트 생성을 포함한 Excel 조작에 필요한 모든 클래스를 포함합니다.

### 단계 2: 워크북 및 워크시트 초기화
**Workbook**은 Excel 파일을 나타내며, **Worksheet**는 해당 파일 내의 단일 시트를 의미합니다. 이러한 객체를 생성하면 원시 데이터와 차트를 위한 캔버스를 제공받게 됩니다.

### 단계 3: 데이터 입력
A열에는 카테고리 레이블을, B열에는 워터폴에 사용할 숫자 값을 입력합니다. 이 레이아웃은 재무 분석에서 일반적으로 사용되는 손익 흐름과 일치합니다.

### 단계 4: 워터폴 차트 만들기
**Chart** 객체는 시각적 표현을 생성합니다; 차트 유형을 `ChartType.WATERFALL`으로 설정하면 워터폴 차트가 됩니다. `add` 메서드를 사용해 시리즈의 차트 데이터 범위(`"B2:B6"` )를 지정하고, 카테고리 축을 `"A2:A6"`에 연결합니다.

### 단계 5: 워크북 저장
워크북을 저장하면 차트와 데이터가 지정된 파일 형식으로 기록됩니다. `workbook.save("WaterfallChart.xlsx")`를 호출해 XLSX 파일을 생성하거나, 형식 매개변수를 변경해 PDF, CSV, HTML 등으로 내보낼 수 있습니다.

## 일반적인 문제 및 해결책

- **Chart appears blank** – 데이터 범위 참조(`B2:B6` 및 `A2:A6`)가 실제 값과 카테고리가 들어 있는 셀과 일치하는지 확인하십시오.  
- **Negative values not displayed correctly** – 시리즈 유형이 `ChartType.WATERFALL`으로 설정되어 있는지 확인하십시오; 다른 차트 유형은 음수를 다르게 처리합니다.  
- **File not opening in Excel** – 최신 Aspose.Cells 릴리스를 사용하고 파일 확장자가 형식(`.xlsx` for Excel)과 일치하는지 확인하십시오.

## 자주 묻는 질문

### 워터폴 차트의 모양을 어떻게 사용자 정의할 수 있나요?
`Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())`와 같이 속성을 수정해 막대 색상을 변경하고, `setShowDataLabels(true)`로 데이터 레이블을 활성화하며, `getCategoryAxis().setTitle("Stage")`로 축 제목을 조정할 수 있습니다. Aspose.Cells API 레퍼런스에서 전체 사용자 정의 옵션 목록을 확인할 수 있습니다.

### 동일 워크시트에 여러 개의 워터폴 차트를 만들 수 있나요?
예. 첫 번째 차트를 추가한 후 다른 데이터 범위와 새로운 `Chart` 객체로 차트 생성 단계를 반복하면 됩니다. 각 차트는 독립적이며 시트 내 원하는 위치에 배치할 수 있습니다.

### Aspose.Cells가 다양한 Java 개발 환경과 호환되나요?
물론입니다. 이 라이브러리는 Eclipse, IntelliJ IDEA, NetBeans 및 Maven이나 Gradle을 지원하는 모든 빌드 시스템에서 작동합니다. 추가 플러그인은 필요하지 않습니다.

### 워터폴 차트에 추가 데이터 시리즈를 추가할 수 있나요?
`chart.getNSeries().add("C2:C6", true)`와 같이 호출하고 각 시리즈를 별도로 구성하면 됩니다. 이를 통해 여러 시나리오를 나란히 비교할 수 있습니다.

### Aspose.Cells for Java에 대한 추가 리소스와 예제는 어디서 찾을 수 있나요?
전체 문서는 Aspose.Cells Java API 레퍼런스에서 확인하십시오: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: 재무 워터폴 차트의 차트 데이터 범위를 어떻게 설정합니까?**  
A: 차트 시리즈의 `add` 메서드를 사용하고 값이 들어 있는 셀 범위, 예를 들어 `"B2:B6"`을 전달합니다.

**Q: 워크북을 XLSX 대신 PDF로 내보낼 수 있나요?**  
A: 예, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);`를 호출하면 PDF 버전을 생성합니다.

**Q: 카테고리가 더 많은 워터폴 차트를 만들어야 하면 어떻게 해야 하나요?**  
A: 값 열과 카테고리 열 모두에서 데이터 범위를 확장한 뒤 `add` 및 `setCategoryData` 호출을 해당 범위에 맞게 업데이트하면 됩니다.

**Q: 양수와 음수 막대를 자동으로 서식 지정하는 방법이 있나요?**  
A: `Series` 컬렉션을 순회하면서 각 값의 부호에 따라 `FillFormat` 색상을 설정하면 됩니다; Aspose.Cells는 프로그래밍 방식으로 조건부 서식을 적용할 수 있습니다.

**Q: Aspose.Cells가 차트의 동적 데이터 업데이트를 지원하나요?**  
A: 예. 셀 값을 수정한 후 워크북을 다시 저장하면 차트가 자동으로 새로운 데이터를 반영합니다.

---

**마지막 업데이트:** 2026-09-02  
**테스트 환경:** Aspose.Cells for Java (최신)  
**작성자:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## 관련 튜토리얼

- [Aspose.Cells for Java를 사용한 Excel 차트 데이터 레이블 사용자 정의: 단계별 가이드](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java로 Excel 차트에 데이터 레이블 추가](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells를 사용한 Java 차트 생성 및 내보내기: 완전 가이드](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}