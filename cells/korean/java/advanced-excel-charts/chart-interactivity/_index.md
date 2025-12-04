---
date: 2025-12-04
description: Aspose.Cells를 사용하여 Java에서 인터랙티브 차트를 만드는 방법을 배우고, 차트에 툴팁을 추가하며, 보다 풍부한
  데이터 시각화를 위해 드릴다운 차트를 추가하세요.
language: ko
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells와 Java로 인터랙티브 차트 만들기
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 인터랙티브 차트 Java 만들기

## 소개

인터랙티브 차트는 사용자가 데이터 포인트를 탐색하고, 마우스를 올렸을 때 세부 정보를 확인하며, 심층 데이터 세트로 드릴다운할 수 있게 해줍니다—스프레드시트를 떠나지 않고도 가능합니다. 이 튜토리얼에서는 Aspose.Cells를 사용하여 **Java 인터랙티브 차트 만들기** 애플리케이션을 배우게 됩니다. 툴팁, 데이터 레이블을 추가하고 드릴‑다운 기능을 구현하는 과정을 단계별로 안내하여 차트를 보다 매력적이고 유용하게 만들 수 있습니다.

## 빠른 답변
- **어떤 라이브러리를 사용하나요?** Aspose.Cells for Java  
- **차트에 툴팁을 추가할 수 있나요?** 네, NSeries 데이터 레이블 API를 사용합니다  
- **드릴‑다운이 지원되나요?** 네, 데이터 포인트에 하이퍼링크를 연결하면 됩니다  
- **어떤 파일 형식이 생성되나요?** 차트가 포함된 표준 XLSX 워크북  
- **라이선스가 필요한가요?** 평가용으로는 무료 체험판으로 충분하지만, 제품 환경에서는 상용 라이선스가 필요합니다  

## 사전 요구 사항

- Java 개발 환경 (JDK 8+ 권장)  
- Aspose.Cells for Java 라이브러리 (공식 [Aspose release page](https://releases.aspose.com/cells/java/)에서 다운로드)  
- **data.xlsx** 라는 샘플 Excel 파일(시각화하려는 데이터를 포함)

## Step 1: Java 프로젝트 설정

1. 선호하는 IDE(IntelliJ IDEA, Eclipse, VS Code 등)에서 새 Java 프로젝트를 생성합니다.  
2. Aspose.Cells JAR를 프로젝트 클래스패스에 추가합니다—JAR를 `libs` 폴더에 넣거나 Maven/Gradle 의존성을 추가합니다.

## Step 2: 데이터 로드

인터랙티브 차트를 만들려면 먼저 데이터가 있는 워크시트가 필요합니다. 아래 코드 스니펫은 기존 워크북을 열고 첫 번째 워크시트를 가져옵니다.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**전문가 팁:** 차트에 사용할 데이터 범위가 연속적인지 확인하세요; Aspose.Cells는 시리즈를 바인딩할 때 범위를 자동으로 감지합니다.

## Step 3: 차트 만들기

이제 컬럼 차트를 만들고 워크시트에 배치합니다. 다른 시각 스타일을 원한다면 `ChartType.COLUMN`을 다른 타입(예: `ChartType.LINE`)으로 변경할 수 있습니다.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

**왜 중요한가:** 프로그래밍 방식으로 차트를 추가하면 크기, 위치, 데이터 소스를 완전히 제어할 수 있어 인터랙티브한 경험을 구축하는 데 필수적입니다.

## Step 4: 인터랙티비티 추가

### 차트에 툴팁 추가 방법

툴팁(값을 표시하는 데이터 레이블)은 사용자가 각 막대 뒤에 있는 정확한 수치를 즉시 확인할 수 있게 도와줍니다. 아래 코드는 데이터 레이블을 활성화하고 값을 표시하도록 설정합니다.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 데이터 레이블(콜아웃) 추가 방법

레이블을 일반 텍스트가 아니라 콜아웃 형태로 표시하려면 `ShowLabelAsDataCallout` 속성을 변경하세요.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 드릴다운 차트 추가 방법

드릴‑다운은 사용자가 데이터 포인트를 클릭해 관련 상세 뷰로 이동하도록 합니다—보통 하이퍼링크를 사용해 구현합니다. 아래에서는 시리즈의 첫 번째 포인트에 URL을 연결합니다.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

**흔한 실수:** 하이퍼링크 대상이 상세 데이터를 렌더링할 수 있는 페이지(예: 웹 보고서 또는 다른 Excel 시트)인지 확인하세요. 그렇지 않으면 클릭 시 죽은 링크가 됩니다.

## Step 5: 워크북 저장

차트를 구성한 후 워크북을 저장합니다. 생성된 파일에는 Excel이나 호환 뷰어에서 열 수 있는 인터랙티브 차트가 포함됩니다.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 결론

이 가이드에서는 Aspose.Cells를 사용하여 **Java 인터랙티브 차트 만들기** 솔루션을 배우셨으며, 다음 내용을 다루었습니다:

- 기존 워크북에서 데이터 로드
- 프로그래밍 방식으로 컬럼 차트 생성
- 툴팁 및 콜아웃 데이터 레이블 추가
- 하이퍼링크를 통한 드릴‑다운 기능 구현
- 최종 워크북 저장

이러한 기술은 정적인 스프레드시트를 동적인 사용자 친화형 대시보드로 변환하여 데이터 이해와 의사결정을 향상시킵니다.

## 자주 묻는 질문

**Q: 차트 유형을 어떻게 변경하나요?**  
A: `add` 메서드에서 `ChartType` 열거형을 수정하면 됩니다(예: 라인 차트는 `ChartType.LINE`).

**Q: 툴팁의 모양을 커스터마이즈할 수 있나요?**  
A: 네, `DataLabels` 객체를 통해 글꼴 크기, 색상, 배경 및 기타 스타일 속성을 조정할 수 있습니다.

**Q: 웹 애플리케이션에서 차트 인터랙티비티를 어떻게 처리하나요?**  
A: 워크북을 XLSX로 내보낸 뒤 JavaScript 차트 라이브러리(예: Highcharts)를 사용해 클라이언트 측에서 데이터를 렌더링하거나, 하이퍼링크를 지원하는 Office Web Viewer에 Excel 파일을 삽입합니다.

**Q: 더 많은 예제를 어디서 찾을 수 있나요?**  
A: 공식 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)에서 차트 관련 클래스와 메서드 전체 목록을 확인하세요.

**Q: 제품 환경에서 라이선스가 필요합니까?**  
A: 네, 배포를 위해서는 상용 라이선스가 필요합니다; 테스트용으로는 무료 평가 라이선스를 제공하고 있습니다.

---

**마지막 업데이트:** 2025-12-04  
**테스트 환경:** Aspose.Cells for Java 24.12 (작성 시 최신 버전)  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}