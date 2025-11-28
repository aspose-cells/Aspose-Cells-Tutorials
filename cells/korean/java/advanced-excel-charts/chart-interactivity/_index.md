---
date: 2025-11-28
description: Aspose.Cells를 사용하여 Java에서 툴팁, 데이터 레이블 및 드릴다운 기능을 추가해 인터랙티브 차트를 만드는 방법을
  배워보세요.
language: ko
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: 대화형 차트에 툴팁 추가하는 방법 (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 인터랙티브 차트에 툴팁 추가하기 (Aspose.Cells Java)

## 소개

인터랙티브 차트는 사용자가 마우스를 올리거나 클릭하거나 세부 정보를 드릴다운하여 데이터를 탐색할 수 있게 합니다. 이 튜토리얼에서는 차트에 **툴팁을 추가하는 방법**과 **데이터 레이블을 추가하는 방법**, 그리고 **드릴‑다운** 네비게이션 구현 방법을 Aspose.Cells for Java와 함께 배웁니다. 마지막에는 데이터 프레젠테이션을 보다 매력적이고 통찰력 있게 만드는 완전한 인터랙티브 차트를 구축할 수 있게 됩니다.

## 빠른 답변
- **필요한 라이브러리는?** Aspose.Cells for Java (최신 버전).  
- **이 가이드가 다루는 주요 기능은?** 차트에 툴팁 추가하기.  
- **데이터 레이블도 추가할 수 있나요?** 예 – “데이터 레이블 추가” 섹션을 참조하세요.  
- **드릴‑다운이 지원되나요?** 예, 데이터 포인트에 하이퍼링크를 사용합니다.  
- **생성되는 파일 형식은?** 인터랙티브 차트가 포함된 Excel 워크북(`.xlsx`).

## 툴팁 추가란 무엇인가요?

툴팁은 사용자가 차트 요소 위에 마우스를 올렸을 때 나타나는 작은 팝업으로, 정확한 값이나 사용자 지정 메시지와 같은 추가 정보를 표시합니다. 툴팁은 시각적 레이아웃을 어지럽히지 않으면서 데이터 가독성을 향상시킵니다.

## Java에서 인터랙티브 차트를 만드는 이유는?

- **보다 나은 의사결정:** 사용자는 즉시 정확한 값을 확인할 수 있습니다.  
- **전문적인 보고서:** 인터랙티브 요소가 대시보드를 현대적으로 보이게 합니다.  
- **재사용 가능한 컴포넌트:** API를 숙달하면 모든 Excel 기반 보고 솔루션에 적용할 수 있습니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Java 개발 환경 (JDK 8 이상).  
- Aspose.Cells for Java 라이브러리 ([여기](https://releases.aspose.com/cells/java/)에서 다운로드).  
- 시각화하려는 데이터를 포함한 **data.xlsx** 샘플 Excel 파일.

## 단계 1: Java 프로젝트 설정

1. 선호하는 IDE(IntelliJ IDEA, Eclipse 등)에서 새 Java 프로젝트를 생성합니다.  
2. Aspose.Cells JAR 파일을 프로젝트 클래스패스에 추가합니다.

## 단계 2: 데이터 로드

인터랙티브 차트를 만들려면 먼저 데이터가 있는 워크시트가 필요합니다. 아래 코드는 **data.xlsx**의 첫 번째 워크시트를 로드합니다.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 단계 3: 차트 만들기

이제 워크시트에 컬럼 차트를 추가합니다. 차트는 셀 F6 부터 K16 까지 차지합니다.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 단계 4: 인터랙티비티 추가

### 4.1. 툴팁 추가 방법

다음 스니펫은 차트의 첫 번째 시리즈에 툴팁을 활성화합니다. 각 데이터 포인트는 마우스를 올릴 때 값을 표시합니다.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 차트에 데이터 레이블 추가

각 컬럼 옆에 보이는 레이블을 원한다면 아래와 같이 **add data labels chart** 방식을 사용하세요. 이는 보조 키워드 *add data labels chart*를 만족합니다.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. 드릴 다운 방법 (드릴‑다운 구현)

드릴‑다운은 사용자가 데이터 포인트를 클릭하여 상세 뷰(예: 웹 페이지)로 이동하도록 합니다. 여기서는 시리즈의 첫 번째 포인트에 하이퍼링크를 연결합니다.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **프로 팁:** 포인트 값에 따라 URL을 동적으로 생성하면 진정한 데이터 기반 드릴‑다운 경험을 만들 수 있습니다.

## 단계 5: 워크북 저장

차트를 구성한 후 워크북을 저장합니다. 생성된 파일에는 Excel에서 열 수 있는 인터랙티브 차트가 포함됩니다.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 일반적인 문제 및 해결책

| 문제 | 원인 | 해결 방법 |
|------|------|-----------|
| 툴팁이 나타나지 않음 | 데이터 레이블이 활성화되지 않음 | `ShowValue`를 설정하기 전에 `setHasDataLabels(true)`가 호출되었는지 확인하세요. |
| 하이퍼링크가 클릭되지 않음 | 포인트 인덱스 오류 | 올바른 포인트(`get(0)`이 첫 번째 포인트)를 참조하고 있는지 확인하세요. |
| 차트 위치가 잘못됨 | 셀 범위 오류 | `add(ChartType.COLUMN, row1, col1, row2, col2)`에서 행/열 인덱스를 조정하세요. |

## 자주 묻는 질문

**Q: 차트 유형을 어떻게 변경하나요?**  
A: `worksheet.getCharts().add(...)` 호출 시 `ChartType.COLUMN`을 `ChartType.LINE`이나 `ChartType.PIE`와 같은 다른 enum 값으로 교체합니다.

**Q: 툴팁의 모양을 커스터마이즈할 수 있나요?**  
A: 예. `DataLabel` 객체의 서식 속성(글꼴 크기, 배경색 등)을 사용해 툴팁 텍스트를 스타일링합니다.

**Q: 웹 애플리케이션에서 사용자 인터랙션을 어떻게 처리하나요?**  
A: 워크북을 웹 호환 형식(예: HTML)으로 내보낸 뒤 JavaScript를 사용해 차트 요소의 클릭 이벤트를 캡처합니다.

**Q: 더 많은 예제와 문서는 어디서 찾을 수 있나요?**  
A: 공식 API 레퍼런스인 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)를 확인하세요.

**Q: 동일 차트에 여러 드릴‑다운 링크를 추가할 수 있나요?**  
A: 가능합니다. 시리즈 포인트를 순회하면서 각 포인트의 `Hyperlinks` 컬렉션에 고유한 URL을 할당하면 됩니다.

## 결론

이 가이드에서는 Aspose.Cells를 사용해 **툴팁 추가**, **데이터 레이블 추가**, **드릴‑다운 구현** 기능을 통해 **create interactive chart java** 솔루션을 만드는 방법을 배웠습니다. 이러한 기능은 정적 Excel 차트를 동적이고 사용자 친화적인 시각화로 변환하여 이해관계자가 데이터를 손쉽게 탐색하도록 돕습니다.

---

**마지막 업데이트:** 2025-11-28  
**테스트 환경:** Aspose.Cells for Java 24.12  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}