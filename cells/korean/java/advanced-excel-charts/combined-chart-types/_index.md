---
date: 2025-12-06
description: Aspose.Cells for Java를 사용하여 데이터 시리즈를 추가하고, 결합 차트 유형을 만들며, 워크북을 Excel로
  저장하고 차트를 PNG로 내보내는 방법을 배웁니다.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells를 사용하여 결합 차트를 만들기 위해 데이터 시리즈 추가
url: /ko/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 결합 차트 만들기 위해 데이터 시리즈 추가

이 튜토리얼에서는 Excel 워크북에 **데이터 시리즈를 추가**하고 Aspose.Cells for Java를 사용하여 **결합 차트** 유형을 만드는 방법을 배웁니다. 워크북 설정, 시리즈 추가, 범례 사용자 지정, **워크북 Excel** 파일 저장 및 **차트를 PNG**로 내보내는 모든 단계를 차근차근 안내합니다. 끝까지 진행하면 보고서나 대시보드에 삽입할 수 있는 사용 준비가 된 결합 차트를 얻을 수 있습니다.

## 빠른 답변
- **어떤 라이브러리로 결합 차트를 만들 수 있나요?** Aspose.Cells for Java  
- **데이터 시리즈는 어떻게 추가하나요?** `chart.getNSeries().add(...)` 사용  
- **차트를 이미지로 내보낼 수 있나요?** 예, `chart.toImage(...)` (PNG) 로 가능  
- **워크북을 어떤 파일 형식으로 저장할 수 있나요?** 표준 `.xlsx` (Excel)  
- **프로덕션에서 라이선스가 필요하나요?** 유효한 Aspose.Cells 라이선스가 필요합니다  

## Aspose.Cells에서 **데이터 시리즈 추가**란?
데이터 시리즈를 추가하면 차트가 플롯할 값이 들어 있는 셀 범위를 지정하게 됩니다. 각 시리즈는 선, 열, 혹은 다른 차트 유형을 나타낼 수 있으며, 이를 혼합하여 **결합 차트**를 만들 수 있습니다.

## **결합 차트**를 만드는 이유는?
결합 차트를 사용하면 서로 다른 데이터 세트를 서로 다른 시각적 표현(예: 열 차트 위에 선 차트)으로 하나의 화면에 표시할 수 있습니다. 이는 추세와 총합을 비교하거나 상관관계를 강조하거나, 제한된 공간에서 풍부한 인사이트를 제공할 때 이상적입니다.

## 사전 준비
- Java Development Kit (JDK) 8 이상  
- Aspose.Cells for Java 라이브러리 (아래 링크에서 다운로드)  
- Java 문법 및 Excel 기본 개념에 대한 기본 지식  

## 시작하기

먼저 공식 사이트에서 Aspose.Cells for Java 라이브러리를 다운로드합니다:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR 파일을 프로젝트의 클래스패스에 추가하면 차트 작성을 시작할 수 있습니다.

### 1단계: Aspose.Cells 클래스 가져오기
```java
import com.aspose.cells.*;
```

### 2단계: 새 워크북 만들기
```java
Workbook workbook = new Workbook();
```

### 3단계: 첫 번째 워크시트에 접근
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 4단계: 결합 차트 객체 추가  
먼저 선 차트를 만들고 이후 다른 시리즈를 추가하여 **결합 차트** 효과를 구현합니다.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 차트에 데이터 추가

차트 컨테이너가 준비되었으니 이제 데이터를 채워야 합니다.

### 5단계: 데이터 범위를 정의하고 **데이터 시리즈 추가**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **팁:** 첫 번째 매개변수(`"A1:A5"`)는 첫 번째 시리즈의 범위이며, 두 번째 매개변수(`"B1:B5"`)는 첫 번째와 결합될 두 번째 시리즈를 생성합니다.

### 6단계: 카테고리(X‑축) 데이터 설정
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 차트 사용자 지정

좋은 차트는 이야기를 전달합니다. 제목, 축 레이블, 명확한 범례를 추가해 보겠습니다.

### 7단계: 차트 제목 및 축 레이블 설정
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 8단계: **범례 차트 추가** 및 위치 조정
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 차트 저장 및 내보내기

사용자 지정이 끝나면 **워크북 Excel**을 저장하고 이미지도 생성하고 싶을 겁니다.

### 9단계: 워크북을 Excel 파일로 저장
```java
workbook.save("CombinedChart.xlsx");
```

### 10단계: **차트를 PNG**로 내보내기
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 메서드는 **excel 차트** 이미지를 생성하여 웹 페이지, 보고서 또는 이메일에 사용할 수 있게 합니다.

## 일반적인 문제 및 해결 방법

| 문제 | 해결책 |
|------|--------|
| **데이터가 표시되지 않음** | 차트를 만들기 전에 셀 범위(`A1:A5`, `B1:B5`, `C1:C5`)에 실제 데이터가 들어 있는지 확인하세요. |
| **범례가 차트와 겹침** | `chart.getLegend().setOverlay(false)` 로 설정하거나 범례 위치를 다른 곳(예: `RIGHT`)으로 이동하세요. |
| **이미지 파일이 빈 화면** | 최소 하나의 시리즈가 차트에 포함되어 있는지, 그리고 모든 사용자 지정 후에 `chart.toImage` 가 호출되는지 확인하세요. |
| **저장 시 예외 발생** | 대상 디렉터리에 쓰기 권한이 있는지, 파일이 Excel에서 열려 있지 않은지 확인하세요. |

## 자주 묻는 질문

**Q: Aspose.Cells for Java를 어떻게 설치하나요?**  
A: 공식 사이트에서 JAR 파일을 다운로드하고 프로젝트의 클래스패스에 추가합니다. 다운로드 링크: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)  

**Q: 선 차트와 열 차트 외에 다른 차트 유형도 만들 수 있나요?**  
A: 예, Aspose.Cells는 막대, 파이, 산점도, 영역 등 다양한 차트 유형을 지원합니다. 전체 목록은 API 문서를 참고하세요.  

**Q: 프로덕션 사용에 라이선스가 필요합니까?**  
A: 프로덕션 배포 시 유효한 Aspose.Cells 라이선스가 필요합니다. 평가용 무료 체험판을 제공하고 있습니다.  

**Q: 각 시리즈의 색상을 어떻게 변경하나요?**  
A: 시리즈를 추가한 후 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`(또는 유사 메서드) 를 사용합니다.  

**Q: 더 많은 코드 예제를 어디서 찾을 수 있나요?**  
A: 자세한 문서와 추가 샘플은 Aspose 레퍼런스 사이트에서 확인할 수 있습니다: [here](https://reference.aspose.com/cells/java/)  

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
