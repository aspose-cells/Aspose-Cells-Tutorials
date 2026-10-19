---
date: '2026-04-08'
description: Aspose.Cells for Java를 사용하여 마커가 있는 선 차트를 만드는 방법을 배우고, 차트를 워크시트에 추가하며,
  자동 보고를 위한 Excel 차트를 사용자 정의하십시오.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Aspose.Cells for Java를 사용하여 마커가 있는 선 차트 만들기
url: /ko/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java를 사용한 Excel 차트 만들기 및 스타일링

## 소개

오늘날 데이터 중심의 세계에서 **마커가 있는 선 차트**는 추세와 이상치를 시각화하는 가장 효과적인 방법 중 하나입니다. 자동 보고서나 매일 업데이트되는 대시보드를 구축하든, 워크시트에 프로그래밍 방식으로 마커가 있는 선 차트를 추가할 수 있으면 수많은 수작업을 절감할 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 이러한 차트를 만들고, 스타일을 지정하고, 내보내는 방법을 단계별로 안내하므로 번거로운 Excel 작업 대신 인사이트에 집중할 수 있습니다.

**배우게 될 내용**
- Aspose.Cells를 사용하여 워크북을 초기화하고 데이터를 채우기.  
- **워크시트에 마커가 있는 선 차트를 추가하고** 모양을 구성하는 방법.  
- 시리즈 색상, 마커 및 기타 스타일 옵션 사용자 정의.  
- 스타일이 적용된 차트를 포함한 Excel 파일로 워크북 저장.

## 빠른 답변
- **시작할 기본 클래스는 무엇인가요?** `Workbook`은 새로운 Excel 파일을 초기화합니다.  
- **마커가 있는 선 차트를 만들 차트 유형은?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **시리즈 포인트에 사용자 정의 색상을 설정하려면?** `chart.getNSeries().setColorVaried(true)`를 사용하고 마커 영역 색상을 설정합니다.  
- **전체 기능을 위해 라이선스가 필요합니까?** 예, 유료 또는 임시 Aspose.Cells 라이선스를 사용하면 평가 제한이 해제됩니다.  
- **결과를 XLSX로 내보낼 수 있나요?** 물론—`workbook.save("StyledChart.xlsx")`는 XLSX 파일을 생성합니다.

## 전제 조건

Aspose.Cells for Java를 사용하여 차트를 만들고 스타일링하기 전에 다음 설정이 준비되어 있는지 확인하십시오.

### 필수 라이브러리
프로젝트에 Aspose.Cells를 종속성으로 포함하십시오. Maven과 Gradle 사용자를 위한 지침은 다음과 같습니다:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 환경 설정 요구 사항
- 시스템에 Java Development Kit (JDK)가 설치되어 있어야 합니다.  
- 코딩 및 테스트를 위한 IntelliJ IDEA 또는 Eclipse와 같은 통합 개발 환경(IDE).

### 지식 전제 조건
Java 프로그래밍에 대한 기본 이해와 Excel 워크북 및 차트 개념에 대한 친숙함이 필요합니다.

### 라이선스 획득
Aspose.Cells는 전체 기능을 위해 라이선스가 필요한 상용 제품입니다. 무료 체험판을 받아 기능을 평가하거나, 장기 테스트를 위한 임시 라이선스를 요청하거나, 장기 사용을 위해 제품을 구매할 수 있습니다.

- **무료 체험:** [무료 체험 다운로드](https://releases.aspose.com/cells/java/)  
- **임시 라이선스:** [임시 라이선스 요청](https://purchase.aspose.com/temporary-license/)  
- **구매:** [Aspose.Cells 구매](https://purchase.aspose.com/buy)

## Aspose.Cells for Java 설정

필요한 종속성을 설치한 후, Aspose.Cells를 사용하도록 개발 환경을 설정하십시오. 라이브러리를 가져오고 Java 애플리케이션에서 `Workbook` 객체를 초기화하는 것으로 시작합니다:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 구현 가이드

이 섹션에서는 구현을 다음과 같은 개별 기능으로 나누어 설명합니다: 워크북 초기화 및 데이터 입력, 차트 생성 및 구성, 시리즈 사용자 정의, 그리고 워크북 저장.

### 기능 1: 워크북 초기화 및 데이터 입력

**Overview:** 이 기능은 새 워크북을 만들고, 첫 번째 워크시트에 접근한 뒤, 차트 생성을 위한 데이터를 채우는 데 중점을 둡니다.

#### 단계 1: 워크북 초기화
`Workbook` 객체를 인스턴스화하여 시작합니다:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 단계 2: 열 제목 설정 및 데이터 입력
열 헤더를 정의하고 샘플 데이터로 행을 채웁니다:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 기능 2: 차트 생성 및 구성

**Overview:** 이 기능은 워크북의 워크시트에 차트를 추가하고, 스타일을 설정하며 기본 속성을 구성하는 방법을 보여줍니다.

#### 단계 3: 워크시트에 차트 추가
마커가 있는 선 차트를 추가합니다:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 기능 3: 시리즈 구성 및 사용자 정의

**Overview:** 색상 다양화 및 마커 스타일과 같은 시리즈 설정을 사용자 정의하여 차트의 시각적 매력을 향상시킵니다.

#### 단계 4: 시리즈 설정 사용자 정의
시리즈 데이터를 구성하고, 사용자 정의 형식을 적용하며, 마커를 조정합니다:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 기능 4: 워크북 저장

**Overview:** 마지막으로 워크북을 저장하여 변경 사항을 영구히 보존하고 차트가 Excel 파일에 포함되도록 합니다.

#### 단계 5: 워크북 저장
새로 만든 차트를 포함하여 워크북을 저장합니다:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### 일반적인 문제 및 해결 방법

- **차트가 비어 있음:** `setXValues`와 `setValues`에 사용된 셀 범위가 실제 데이터가 들어 있는 셀을 정확히 참조하는지 확인하십시오.  
- **색상이 적용되지 않음:** 개별 시리즈를 사용자 정의하기 전에 `chart.getNSeries().setColorVaried(true)`가 호출되었는지 확인하십시오.  
- **라이선스 오류:** 평가판 라이선스는 차트 수에 제한이 있을 수 있습니다; 전체 라이선스를 설치하면 제한이 해제됩니다.

## 자주 묻는 질문

**Q: Aspose.Cells로 다른 차트 유형(예: 막대, 파이)을 만들 수 있나요?**  
A: 예, Aspose.Cells는 다양한 차트 유형을 지원합니다; 원하는 enum 값으로 `ChartType.LINE_WITH_DATA_MARKERS`를 교체하면 됩니다.

**Q: 워크북을 닫거나 리소스를 해제해야 하나요?**  
A: `Workbook` 클래스가 리소스를 자동으로 관리하지만, 장시간 실행되는 애플리케이션에서는 `workbook.dispose()`를 호출하여 메모리를 해제할 수 있습니다.

**Q: 동일한 워크시트에 여러 차트를 추가할 수 있나요?**  
A: 물론입니다—삽입하려는 각 차트에 대해 `worksheet.getCharts().add(...)`를 호출하면 됩니다.

**Q: 파일을 오래된 Excel 형식(XLS)으로 내보내려면 어떻게 해야 하나요?**  
A: `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`를 사용하십시오.

**Q: 차트가 Microsoft Excel에서 열릴 때 스타일이 유지되나요?**  
A: 예, Aspose.Cells는 네이티브 Excel 차트 객체를 작성하므로 모든 스타일, 색상 및 마커가 정의된 그대로 표시됩니다.

---

**마지막 업데이트:** 2026-04-08  
**테스트 환경:** Aspose.Cells 25.3 for Java  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}