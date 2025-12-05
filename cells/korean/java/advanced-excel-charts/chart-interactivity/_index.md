---
date: 2025-12-05
description: Aspose.Cells를 사용하여 Java에서 데이터 레이블 차트를 추가하고 인터랙티브 차트를 만드는 방법을 배웁니다. 툴팁,
  데이터 레이블 및 드릴다운 기능을 추가하세요.
language: ko
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java에서 인터랙티브한 데이터 레이블 차트 추가
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java에서 인터랙티브 데이터 레이블 차트 추가하기

인터랙티브 차트는 사용자가 실시간으로 데이터를 탐색할 수 있게 해줍니다. 이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 **데이터 레이블 차트** 기능—툴팁, 데이터 레이블, 드릴‑다운 액션—을 추가합니다. 완료하면 복잡한 데이터를 즉시 이해할 수 있는 세련된 인터랙티브 차트를 얻을 수 있습니다.

## 빠른 답변
- **필요한 라이브러리는?** Aspose.Cells for Java  
- **Excel 차트에 툴팁을 추가할 수 있나요?** 네 – API의 데이터‑레이블 설정을 사용합니다.  
- **어떤 차트 유형이 인터랙티브를 지원하나요?** 대부분의 기본 차트 유형(컬럼, 라인, 파이 등).  
- **프로덕션에 라이선스가 필요합니까?** 유효한 Aspose.Cells 라이선스가 필요합니다.  
- **구현 시간은 얼마나 걸리나요?** 기본 차트의 경우 대략 10–15분 정도 소요됩니다.

## “데이터 레이블 차트 추가”란?
*데이터 레이블 차트 추가*는 각 데이터 포인트에 레이블(값, 이름 또는 사용자 정의 텍스트)이 시각적으로 직접 표시되는 차트를 의미합니다. 이를 통해 사용자는 별도의 레전드에 마우스를 올리거나 교차 참조하지 않아도 정확한 값을 바로 읽을 수 있습니다.

## 왜 Java용 인터랙티브 차트 솔루션을 만들까요?
툴팁, 클릭 가능한 포인트, 드릴‑다운 링크와 같은 인터랙티브 기능을 삽입하면 정적인 스프레드시트를 탐색형 대시보드로 전환할 수 있습니다. 사용자는:
- 이상치를 빠르게 식별
- 한 번의 클릭으로 더 깊은 데이터 레이어에 접근
- 별도 보고서 없이 의사결정 속도 향상

## 사전 준비 사항

시작하기 전에 다음을 준비하세요:

- Java 개발 환경(JDK 8 이상 권장)  
- Aspose.Cells for Java 라이브러리([여기](https://releases.aspose.com/cells/java/)에서 다운로드)

## 1단계: Java 프로젝트 설정

1. 선호하는 IDE(IntelliJ, Eclipse, VS Code 등)에서 새 Java 프로젝트를 생성합니다.  
2. Aspose.Cells for Java JAR 파일을 프로젝트 클래스패스에 추가합니다.

## 2단계: 데이터 로드

인터랙티브 차트를 만들려면 먼저 워크시트에 데이터가 있어야 합니다. 아래 스니펫은 **data.xlsx**라는 기존 워크북을 로드합니다.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 3단계: 차트 생성

이제 컬럼 차트를 만들고 워크시트에 배치합니다. 원하는 경우 `ChartType.COLUMN`을 다른 유형으로 교체해도 됩니다.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 4단계: 인터랙티브 기능 추가 – “데이터 레이블 차트 추가”의 핵심

### 4.1. 툴팁 추가 (add tooltips excel chart)

툴팁은 사용자가 데이터 포인트 위에 마우스를 올릴 때 표시됩니다. 다음 코드는 데이터 레이블을 활성화하고 값을 표시하도록 설정하여 툴팁을 켭니다.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 데이터 레이블 추가 (add data labels chart)

데이터 레이블은 각 포인트 옆에 표시되는 텍스트입니다. 이 스니펫은 일반 값 대신 콜아웃 레이블을 표시하도록 차트를 구성합니다.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. 드릴‑다운 구현 (create interactive chart java)

드릴‑다운은 사용자가 포인트를 클릭하면 상세 보기로 이동하도록 합니다. 여기서는 첫 번째 데이터 포인트에 하이퍼링크를 연결합니다; 필요한 다른 포인트에도 동일하게 적용할 수 있습니다.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 5단계: 워크북 저장

차트 구성을 마친 후 워크북을 새 파일에 저장하여 Excel에서 열어 인터랙티브 기능을 테스트합니다.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 흔히 발생하는 문제 및 팁

| Issue | Solution |
|-------|----------|
| **툴팁이 표시되지 않음** | `setHasDataLabels(true)`를 `ShowValue` 설정 전에 호출했는지 확인합니다. |
| **하이퍼링크가 클릭되지 않음** | URL이 올바른 형식인지, Excel 보안 설정이 외부 링크를 허용하는지 확인합니다. |
| **차트 유형 불일치** | 일부 차트 유형(예: 레이더)은 레이블 지원이 제한적입니다—컬럼이나 라인 같은 호환 유형을 선택하세요. |
| **대용량 데이터에서 성능 저하** | 데이터 레이블이 있는 포인트 수를 제한하고, 중요도가 낮은 시리즈는 `setShowValue(false)`를 고려하세요. |

## 자주 묻는 질문

**Q: 차트 유형을 어떻게 변경하나요?**  
A: 차트 생성 라인에서 `ChartType` 열거형을 원하는 유형으로 바꾸면 됩니다(예: `ChartType.LINE`).

**Q: 툴팁의 모양을 커스터마이즈할 수 있나요?**  
A: 네—`DataLabel` 객체의 폰트, 배경색, 테두리 속성을 사용해 툴팁을 스타일링할 수 있습니다.

**Q: 웹 애플리케이션에서 사용자 인터랙션을 처리하려면?**  
A: 워크북을 HTML 페이지로 내보내거나 Aspose.Cells Cloud를 사용해 차트를 렌더링한 뒤 JavaScript로 클릭 이벤트를 캡처합니다.

**Q: 더 많은 예제와 문서는 어디서 찾을 수 있나요?**  
A: 전체 차트 관련 클래스와 메서드 목록은 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)를 참고하세요.

## 결론

이 가이드에서는 **데이터 레이블 차트** 기능을 추가하고 Aspose.Cells를 활용해 **인터랙티브 차트 Java** 솔루션을 만드는 방법을 보여주었습니다. 툴팁, 데이터 콜아웃, 드릴‑다운 하이퍼링크를 적용하면 정적인 Excel 차트를 동적인 데이터 탐색 도구로 변환하여 인사이트와 사용성을 크게 향상시킬 수 있습니다.

---

**마지막 업데이트:** 2025-12-05  
**테스트 환경:** Aspose.Cells for Java 24.12  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}