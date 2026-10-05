---
date: 2026-02-14
description: Aspose.Cells for Java를 사용하여 차트를 PNG로 내보내고, 데이터 시리즈를 추가하고, 라인‑컬럼 차트를 결합하며,
  워크북을 XLSX 형식으로 저장하고, 차트에 범례를 추가하는 방법을 배웁니다.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: 차트를 PNG로 내보내고 결합 차트에 데이터 시리즈 추가
url: /ko/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 차트를 PNG로 내보내고 결합 차트에 데이터 시리즈 추가

이 튜토리얼에서는 Excel 워크북에 **데이터 시리즈를 추가**하고, **라인 차트와 컬럼 차트를 결합**하며, Aspose.Cells for Java를 사용하여 **차트를 PNG로 내보내는 방법**을 배웁니다. 워크북 설정, 워크시트에 차트 추가, 범례 맞춤 설정, **워크북을 xlsx로 저장**하고 차트의 PNG 이미지를 생성하는 모든 단계를 안내합니다. 최종적으로 보고서나 대시보드에 삽입할 수 있는 사용 준비가 된 결합 차트를 얻게 됩니다.

## Quick Answers
- **어떤 라이브러리가 결합 차트를 생성합니까?** Aspose.Cells for Java  
- **데이터 시리즈를 어떻게 추가합니까?** Use `chart.getNSeries().add(...)`  
- **차트를 PNG로 어떻게 내보냅니까?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **워크북을 어떤 파일 형식으로 저장할 수 있나요?** Standard `.xlsx` (save workbook as xlsx)  
- **프로덕션에 라이선스가 필요합니까?** A valid Aspose.Cells license is required  

## Aspose.Cells에서 **차트를 PNG로 내보내기**란?
차트를 PNG로 내보내면 Excel 차트의 래스터 이미지가 생성되어 Excel 애플리케이션 없이도 웹 페이지, 보고서 또는 이메일에 표시할 수 있습니다.

## 왜 **결합 라인 컬럼 차트**를 만들까요?
결합 차트를 사용하면 서로 다른 데이터 세트를 별개의 시각적 표현(예: 컬럼 시리즈 위에 라인 시리즈)으로 하나의 화면에 표시할 수 있습니다. 이는 전체와 추세를 비교하거나, 상관관계를 강조하거나, 컴팩트한 형식으로 풍부한 인사이트를 제공하는 데 이상적입니다.

## Prerequisites
- Java Development Kit (JDK) 8 이상  
- Aspose.Cells for Java 라이브러리(아래 링크에서 다운로드)  
- Java 구문 및 Excel 개념에 대한 기본 지식  

## Getting Started

First, download the Aspose.Cells for Java library from the official site:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Once the JAR is added to your project’s classpath, you can start building the chart.

### Step 1: Import Aspose.Cells classes
```java
import com.aspose.cells.*;
```

### Step 2: Create a new workbook
```java
Workbook workbook = new Workbook();
```

### Step 3: Access the first worksheet
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Step 4: Add a combined chart object to the worksheet  
We’ll start with a line chart and later add a column series to achieve a **combined line column chart** effect.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adding Data to the Chart

Now that the chart container exists, we need to feed it with data.

### Step 5: Define the data ranges and **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **팁:** 첫 번째 매개변수(`"A1:A5"`)는 첫 번째 시리즈의 범위이며, 두 번째 매개변수(`"B1:B5"`)는 첫 번째와 결합될 두 번째 시리즈를 생성합니다.

### Step 6: Set the category (X‑axis) data
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Customizing the Chart

A good chart tells a story. Let’s give it titles, axis labels, and a clear legend.

### Step 7: **Set chart axis labels** and title
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Step 8: **Add legend chart** and adjust its position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Saving and Exporting the Chart

After customizing, you’ll want to **save workbook as xlsx** and also generate an image.

### Step 9: Save the workbook as an Excel file (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Step 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 메서드는 **Excel 차트** 이미지를 생성하여 웹 페이지, 보고서 또는 이메일에 사용할 수 있습니다.

## Common Issues & Troubleshooting

| 문제 | 해결책 |
|-------|----------|
| **데이터가 표시되지 않음** | 차트를 만들기 전에 셀 범위(`A1:A5`, `B1:B5`, `C1:C5`)에 실제 데이터가 있는지 확인하십시오. |
| **범례가 차트와 겹침** | `chart.getLegend().setOverlay(false)`를 설정하거나 범례를 다른 위치(예: `RIGHT`)로 이동하십시오. |
| **이미지 파일이 비어 있음** | 차트에 최소 하나의 시리즈가 포함되어 있는지, 그리고 모든 맞춤 설정 후에 `chart.toImage`가 호출되는지 확인하십시오. |
| **저장 시 예외 발생** | 대상 디렉터리에 대한 쓰기 권한이 있는지, 파일이 Excel에서 열려 있지 않은지 확인하십시오. |

## Frequently Asked Questions

**Q: Aspose.Cells for Java를 어떻게 설치합니까?**  
A: 공식 사이트에서 JAR를 다운로드하고 프로젝트의 클래스패스에 추가합니다. 다운로드 링크는: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: 라인 및 컬럼 외에 다른 차트 유형을 만들 수 있나요?**  
A: 예, Aspose.Cells는 막대, 원형, 산점도, 영역 등 다양한 차트 유형을 지원합니다. 전체 목록은 API 문서를 참조하십시오.

**Q: 프로덕션 사용에 라이선스가 필요합니까?**  
A: 프로덕션 배포에는 유효한 Aspose.Cells 라이선스가 필요합니다. 평가용 무료 체험판을 제공하고 있습니다.

**Q: 각 시리즈의 색상을 어떻게 변경합니까?**  
A: 시리즈를 추가한 후 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`(또는 유사한 메서드)를 사용하십시오.

**Q: 더 많은 코드 예제를 어디서 찾을 수 있나요?**  
A: 포괄적인 문서와 추가 샘플은 Aspose 레퍼런스 사이트에서 확인할 수 있습니다: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-14  
**Tested With:** Aspose.Cells for Java 최신 버전  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}