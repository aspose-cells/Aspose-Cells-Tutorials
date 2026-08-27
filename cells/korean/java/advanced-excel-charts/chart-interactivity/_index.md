---
date: 2026-02-09
description: Aspose.Cells for Java를 사용하여 Excel 차트에 데이터 레이블을 추가하고 차트 유형을 변경하는 방법을 배우고,
  툴팁 및 드릴다운 인터랙티브 기능도 활용하세요.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java를 사용하여 Excel 차트에 데이터 레이블 추가
url: /ko/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 차트에 데이터 레이블 추가 및 차트 유형 변경 – Aspose.Cells Java

대화형 차트는 Excel 보고서에 새로운 인사이트 수준을 제공하며, **Excel 차트에 데이터 레이블을 추가**하면 정보를 즉시 읽을 수 있게 됩니다. 이 튜토리얼에서는 **Excel 차트에 데이터 레이블을 추가**하고, 차트 유형을 변경하며, Aspose.Cells를 사용한 대화형 Java 솔루션을 만드는 방법을 배웁니다. 또한 툴팁과 간단한 드릴‑다운 하이퍼링크를 추가하여 사용자가 데이터를 깊이 탐색할 수 있도록 하는 방법도 보여드립니다.

## 빠른 답변
- **사용된 라이브러리는?** Aspose.Cells for Java  
- **차트 유형을 변경할 수 있나요?** 예 – 차트를 만들 때 `ChartType` 열거형을 수정하면 됩니다.  
- **차트에 툴팁을 어떻게 추가하나요?** 데이터‑라벨 API(`setHasDataLabels(true)`)를 사용하고 값 표시를 활성화합니다.  
- **드릴‑다운이 지원되나요?** 데이터 포인트에 하이퍼링크를 연결하여 기본 드릴‑다운 동작을 구현할 수 있습니다.  
- **전제 조건은?** Java IDE, Aspose.Cells JAR, 그리고 샘플 데이터가 포함된 Excel 파일.

## 전제 조건

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Java 개발 환경 (JDK 8+ 권장)  
- Aspose.Cells for Java 라이브러리 ( [여기](https://releases.aspose.com/cells/java/)에서 다운로드)  
- 시각화하려는 데이터를 포함한 샘플 워크북(`data.xlsx`)  

## 단계 1: Java 프로젝트 설정

1. 선호하는 IDE(IntelliJ IDEA, Eclipse 등)에서 새 Java 프로젝트를 생성합니다.  
2. Aspose.Cells JAR를 프로젝트의 빌드 경로 또는 Maven/Gradle 의존성에 추가합니다.

## 단계 2: 데이터 로드

차트를 사용하려면 먼저 워크북을 메모리로 로드해야 합니다.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 단계 3: 차트 생성 (및 유형 변경)

분석에 맞는 차트 유형을 선택할 수 있습니다. 아래 예에서는 **컬럼 차트**를 만들지만, `ChartType` 열거형을 변경하면 라인, 파이, 바 차트 등으로 쉽게 전환할 수 있습니다.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **전문가 팁:** Excel 차트 유형을 **변경**하려면 `ChartType.COLUMN`을 `ChartType.LINE`, `ChartType.PIE` 등으로 바꾸면 됩니다.

## 단계 4: 인터랙티브 기능 추가

### 4.1. 툴팁 추가 (Add Tooltips to Chart)

툴팁은 사용자가 데이터 포인트 위에 마우스를 올렸을 때 표시됩니다. 다음 코드는 데이터 라벨을 활성화하고 값을 툴팁으로 표시합니다.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 데이터 레이블 추가 – **add data labels to excel chart**

데이터 레이블은 차트 자체에 영구적인 시각적 힌트를 제공합니다. 가독성을 높이기 위해 콜아웃 형태로 표시할 수 있습니다.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **왜 데이터 레이블을 추가하나요?** 차트에 직접 데이터 레이블을 포함하면 사용자가 마우스를 올리거나 값을 추측할 필요가 없어 보고서의 명확성이 향상됩니다.

### 4.3. 드릴‑다운 구현 (데이터 포인트에 하이퍼링크)

드릴‑다운 기능을 추가하는 간단한 방법은 특정 포인트에 하이퍼링크를 연결하는 것입니다. 포인트를 클릭하면 상세 정보를 담은 웹 페이지가 열립니다.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 단계 5: 워크북 저장

차트를 구성한 후에는 워크북을 저장하여 인터랙티브 기능이 출력 파일에 포함되도록 합니다.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 일반적인 문제 및 해결책

| Issue | Solution |
|-------|----------|
| **툴팁이 표시되지 않음** | `setHasDataLabels(true)`를 `setShowValue(true)`를 구성하기 전에 호출했는지 확인하세요. |
| **하이퍼링크가 클릭되지 않음** | 출력 형식이 하이퍼링크를 지원하는지 확인하세요(예: XLSX, CSV는 아님). |
| **차트 유형이 변경되지 않음** | 차트를 추가할 때 올바른 `ChartType` 열거형을 수정했는지 다시 확인하세요. |

## 자주 묻는 질문

**Q: 차트를 만든 후에 차트 유형을 변경하려면 어떻게 해야 하나요?**  
A: 원하는 `ChartType`으로 새 차트를 만들어야 합니다. Aspose.Cells는 기존 차트의 유형을 제자리에서 변환하는 기능을 제공하지 않으므로, 기존 차트를 제거하고 새 차트를 추가하십시오.

**Q: 툴팁의 모양을 커스터마이징할 수 있나요?**  
A: 예. `DataLabel` 속성인 `setFontSize`, `setFontColor`, `setBackgroundColor` 등을 사용하여 툴팁 텍스트의 스타일을 지정할 수 있습니다.

**Q: 웹 애플리케이션에서 사용자 인터랙션을 처리하려면 어떻게 해야 하나요?**  
A: 워크북을 HTML 또는 XLSX 파일로 내보낸 뒤, 클라이언트 측에서 JavaScript를 사용해 차트 요소의 클릭 이벤트를 캡처하면 됩니다.

**Q: 더 많은 예제와 문서는 어디서 찾을 수 있나요?**  
A: 전체 차트 관련 클래스와 메서드 목록은 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)에서 확인하세요.

## 결론

이제 **Excel 차트에 데이터 레이블을 추가**, **Excel 차트 유형을 변경**, **대화형 차트 Java** 솔루션을 만들고, Aspose.Cells for Java를 사용해 툴팁, 데이터 레이블, 드릴‑다운 하이퍼링크로 차트를 풍부하게 만드는 방법을 알게 되었습니다. 이러한 향상 기능은 Excel 보고서를 최종 사용자에게 훨씬 더 매력적이고 인사이트 있게 만들어 줍니다.

---

**마지막 업데이트:** 2026-02-09  
**테스트 환경:** Aspose.Cells for Java 24.12  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}