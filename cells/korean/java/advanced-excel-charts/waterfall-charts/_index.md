---
date: 2026-02-16
description: Aspose.Cells를 사용하여 Java에서 차트 데이터 범위를 설정하고 워터폴 차트를 만드는 방법을 배웁니다. 데이터 시리즈
  차트를 추가하고, 사용자 정의하며, XLSX로 내보내는 단계별 가이드.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: 차트 데이터 범위 설정 – Aspose.Cells for Java 워터폴 차트
url: /ko/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 폭포 차트

## Aspose.Cells for Java를 사용한 폭포 차트 소개

이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 **set chart data range**를 설정하고 **waterfall chart**를 만드는 방법을 배웁니다. 폭포 차트는 데이터 시각화에서 필수 도구로, 양수와 음수 값들의 연속적인 누적 효과를 확인할 수 있게 해줍니다. 재무 보고서, 판매 실적 보고서 또는 기타 데이터 기반 분석을 준비하든, 폭포 차트는 원시 데이터를 명확하고 실행 가능한 인사이트로 변환할 수 있습니다.

## 빠른 답변
- **폭포 차트란 무엇인가요?** 초기 값이 일련의 중간 값에 의해 증가 및 감소되어 최종 합계에 도달하는 과정을 시각적으로 보여줍니다.  
- **어떤 라이브러리를 사용하나요?** Aspose.Cells for Java.  
- **라이선스가 필요합니까?** 개발용으로는 무료 체험판이 충분하며, 운영 환경에서는 상용 라이선스가 필요합니다.  
- **파일을 XLSX 형식으로 저장할 수 있나요?** 예 – `workbook.save("FileName.xlsx")`를 사용합니다.  
- **Java 데이터 시각화에 적합한가요?** 물론입니다; Aspose.Cells는 Office 없이도 풍부한 차트 기능을 제공합니다.

## 폭포 차트란?

폭포 차트는 시작값에 순차적인 양수와 음수 기여도를 표시하여 각 구성 요소가 전체 결과에 어떻게 영향을 미치는지 이해하도록 도와줍니다.

## 왜 Aspose.Cells for Java를 사용하여 폭포 차트를 추가해야 할까요?
- **Microsoft Excel이 필요 없음** – 모든 서버나 CI 파이프라인에서 차트를 생성합니다.  
- **서식에 대한 완전한 제어** – 색상, 데이터 레이블 및 축을 프로그래밍 방식으로 사용자 지정할 수 있습니다.  
- **다양한 출력 형식 지원** – XLSX, PDF, HTML 등 여러 형식을 지원합니다.  
- **고성능** – 대용량 워크북 및 자동 보고에 이상적입니다.

## 전제 조건

코드 작성을 시작하기 전에 다음 전제 조건이 준비되어 있는지 확인하세요:

- Aspose.Cells for Java: Aspose.Cells for Java를 설치해야 합니다. [여기](https://releases.aspose.com/cells/java/)에서 다운로드할 수 있습니다.

- Java Development Environment: 시스템에 Java가 설치되어 있는지 확인하세요.

이제 단계별로 폭포 차트를 만드는 방법을 시작해 보겠습니다.

## How to Set Chart Data Range for a Waterfall Chart in Java

### Step 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

먼저 Aspose.Cells 라이브러리를 Java 프로젝트에 가져와야 합니다. 이 라이브러리는 차트 생성 등을 포함한 Excel 파일 작업을 위한 광범위한 기능을 제공합니다.

### Step 2: Initialize Workbook and Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

새 워크북을 만들고 워크시트를 추가합니다. 이 워크시트를 사용해 데이터를 입력하고 **add chart to worksheet**를 수행합니다.

### Step 3: Enter Data

이제 폭포 차트에 표시할 데이터를 워크시트에 채워 넣겠습니다.

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

이 예제에서는 A 열에 카테고리, B 열에 해당 값을 배치했습니다. 필요에 따라 데이터를 자유롭게 교체하세요.

### Step 4: Create the Waterfall Chart

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

워크시트에 폭포 차트를 추가하고 데이터 시리즈와 카테고리 데이터를 지정했습니다. 이것이 시트에 **adds waterfall chart**를 삽입하는 핵심 단계입니다. `add` 메서드가 `"B2:B6"` 범위를 사용하고 있음을 확인하세요 – 여기서 시리즈에 대한 **set chart data range**를 지정합니다. `Chart` 객체의 속성을 활용해 색상, 데이터 레이블 등 차트 외형을 추가로 맞춤 설정할 수 있습니다.

### Step 5: Save the Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

워크북을 파일로 저장합니다. 예제는 XLSX 형식을 사용하지만, Aspose.Cells는 PDF, CSV 등 **export excel pdf java**‑호환 파일도 생성할 수 있습니다. 이는 **save workbook xlsx** 요구 사항을 충족합니다.

## Common Issues and Solutions

- **Chart appears blank** – 데이터 범위 참조(`B2:B6` 및 `A2:A6`)가 실제 값과 카테고리가 들어 있는 셀과 일치하는지 확인하세요.  
- **Negative values not displayed correctly** – 시리즈 유형이 `ChartType.WATERFALL`으로 설정되어 있는지 확인합니다; 다른 차트 유형은 음수를 다르게 처리합니다.  
- **File not opening in Excel** – 최신 버전의 Aspose.Cells(최신 릴리스)를 사용하고 파일 확장자가 형식(`.xlsx` for Excel)과 일치하는지 확인하세요.

## Frequently Asked Questions

### How can I customize the appearance of my waterfall chart?

색상, 데이터 레이블, 축 레이블 등 속성을 수정하여 폭포 차트의 외형을 맞춤 설정할 수 있습니다. 자세한 내용은 Aspose.Cells 문서를 참고하세요.

### Can I create multiple waterfall charts in the same worksheet?

예, 서로 다른 데이터 범위를 사용해 동일한 워크시트에 여러 개의 폭포 차트를 만들 수 있습니다.

### Is Aspose.Cells compatible with different Java development environments?

예, Aspose.Cells for Java는 Eclipse, IntelliJ IDEA, NetBeans 등 다양한 Java 개발 환경과 호환됩니다.

### Can I add additional data series to my waterfall chart?

물론입니다. 추가 데이터 시리즈를 삽입해 복잡한 데이터 시나리오를 효과적으로 표현할 수 있습니다. 이는 **add data series chart**를 프로그래밍 방식으로 수행하는 예시입니다.

### Where can I find more resources and examples for Aspose.Cells for Java?

자세한 정보와 코드 예제는 [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/)에서 확인할 수 있습니다.

## FAQ

**Q: How do I set the chart data range for a financial waterfall chart?**  
A: 차트 시리즈의 `add` 메서드를 사용해 값이 들어 있는 셀 범위(예: `"B2:B6"`)를 전달하면 됩니다.

**Q: Can I export the workbook to PDF instead of XLSX?**  
A: 예, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);`를 호출하면 **export excel pdf java**‑호환 출력이 생성됩니다.

**Q: What if I need to create a financial waterfall chart with more categories?**  
A: 값 열과 카테고리 열 모두에서 데이터 범위를 확장한 뒤 `add`와 `setCategoryData` 호출을 해당 범위에 맞게 업데이트하면 됩니다.

**Q: Is there a way to automatically format positive and negative bars?**  
A: `Series` 컬렉션을 순회하면서 각 값의 부호에 따라 `FillFormat` 색상을 설정하면 자동으로 서식이 적용됩니다.

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
A: 예, 차트 생성 후 셀 값을 수정하면 워크북을 저장할 때 차트가 변경된 데이터를 반영합니다.

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}