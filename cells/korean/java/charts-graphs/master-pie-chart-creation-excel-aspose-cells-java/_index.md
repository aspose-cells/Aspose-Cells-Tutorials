---
"date": "2025-04-07"
"description": "Aspose.Cells for Java를 사용하여 Excel에서 원형 차트를 만들고 사용자 지정하는 방법을 알아보세요. 이 단계별 가이드를 따라 데이터 시각화 기술을 향상시켜 보세요."
"title": "Aspose.Cells for Java를 사용하여 Excel에서 원형 차트 만들기&#58; 종합 가이드"
"url": "/ko/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Java용 Aspose.Cells를 사용하여 Excel에서 원형 차트 만들기
## 소개
Excel에서 매력적이고 유익한 원형 차트를 만들면 원시 데이터를 강력한 통찰력으로 변환하여 정보에 기반한 비즈니스 의사 결정을 신속하게 내릴 수 있습니다. Microsoft Excel의 기본 기능 사용에 어려움을 겪고 있거나 Java 애플리케이션과 완벽하게 통합되는 확장 가능한 솔루션을 찾고 계신가요? Aspose.Cells for Java가 도와드리겠습니다.

이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 Excel 파일에서 원형 차트를 만들고 사용자 지정하는 방법을 안내합니다. 데이터를 효율적으로 추가하고, 차트 요소를 구성하고, 통합 문서를 완성하는 방법을 쉽고 정확하게 알아보세요.

**배울 내용:**
- Java용 Aspose.Cells 설정 및 사용
- 새 통합 문서를 만들고 샘플 데이터로 채우기
- Excel 워크시트 내에서 원형 차트 추가 및 사용자 지정
- 차트 구성 및 최적화를 위한 모범 사례

먼저 전제 조건부터 살펴보겠습니다.
## 필수 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
### 필수 라이브러리, 버전 및 종속성
Maven이나 Gradle을 사용하여 프로젝트에 Aspose.Cells for Java 버전 25.3 이상이 포함되어 있는지 확인하세요.
**메이븐:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**그래들:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### 환경 설정 요구 사항
- 시스템에 Java 개발 키트(JDK)가 설치되어 있어야 합니다.
- IntelliJ IDEA, Eclipse 또는 NetBeans와 같은 통합 개발 환경(IDE).
### 지식 전제 조건
Java 프로그래밍에 대한 기본적인 이해와 Excel 파일 구조에 대한 친숙함이 도움이 됩니다.
## Java용 Aspose.Cells 설정
Aspose.Cells는 개발자가 Java 애플리케이션에서 Excel 스프레드시트를 생성, 수정 및 렌더링할 수 있도록 지원하는 강력한 라이브러리입니다. 설정 방법은 다음과 같습니다.
1. **설치**: 위에 표시된 대로 Maven 또는 Gradle 종속성을 추가합니다.
2. **라이센스 취득**:
   - 초기 테스트를 위해 무료 평가판 라이센스를 받으세요. [Aspose 무료 체험판](https://releases.aspose.com/cells/java/).
   - 제한 없이 전체 기능을 테스트하기 위한 임시 라이센스를 신청하세요. [임시 면허](https://purchase.aspose.com/temporary-license/).
3. **기본 초기화**: 인스턴스를 생성하여 시작합니다. `Workbook` Excel 파일을 나타내는 클래스입니다.
```java
import com.aspose.cells.Workbook;
// 새 통합 문서 만들기 및 초기화
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## 구현 가이드
이제 각 기능을 단계별로 구현하여 원형 차트가 있는 Excel 통합 문서를 만들어 보겠습니다.
### 1. 통합 문서 만들기 및 초기화
**개요**: 우리는 초기화로 시작합니다 `Workbook` 객체를 만들고 첫 번째 워크시트에 액세스하여 데이터와 차트를 추가합니다.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// 새 통합 문서 인스턴스 만들기
Workbook workbook = new Workbook();
// 통합 문서의 첫 번째 워크시트에 액세스합니다.
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. 셀에 샘플 데이터 추가
**개요**: 파이 차트에 표시될 샘플 데이터로 워크시트를 채웁니다.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// A열에 국가 이름 추가
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// 다른 국가에 대해서도 계속...
// B열에 해당 판매 데이터를 추가합니다.
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// 나머지 데이터도 계속 진행합니다...
```
### 3. 워크시트에 원형 차트 추가
**개요**미리 정의된 데이터 범위를 사용하여 워크시트에 원형 차트를 삽입합니다.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// 지정된 위치와 크기에 원형 차트 추가
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. 차트 시리즈 구성
**개요**: 판매 및 카테고리 데이터(국가 이름)에 대한 데이터 범위를 정의하여 파이 차트가 데이터 세트를 정확하게 나타내는지 확인합니다.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// 판매 데이터를 차트의 데이터 소스로 설정합니다.
serieses.add("B1:B8", true);
// 카테고리 데이터(국가 이름) 지정
serieses.setCategoryData("A1:A8");
// 각 파이 조각에 다양한 색상 사용
serieses.setColorVaried(true);

// 명확성을 위해 차트에 데이터 테이블 표시
chart.setShowDataTable(true);
```
### 5. 차트 제목 및 스타일 설정
**개요**: 차트의 제목을 사용자 지정하여 가독성과 표현력을 향상시킵니다.
```java
import com.aspose.cells.Color;

// 스타일 옵션을 사용하여 차트 제목 설정
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. 차트 시리즈에 대한 데이터 레이블 구성
**개요**: 각 파이 조각에 데이터 레이블을 추가하여 값의 명확한 분석을 제공합니다.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // 각 파이 조각의 바닥 내부에 레이블 위치 지정
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // 라벨 표시 옵션 구성
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. 통합 문서 저장
**개요**모든 데이터와 차트를 디스크에 저장하여 Excel 파일을 완성합니다.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// 통합 문서를 Excel 파일로 저장
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## 실제 응용 프로그램
- **비즈니스 분석**: 판매 보고서에서 원형 차트를 사용하여 지역별 시장 점유율이나 수익 분포를 시각화합니다.
- **교육 도구**: 통계적 데이터 분포를 표시하는 대화형 학습 모듈을 만듭니다.
- **프로젝트 관리**: 이해관계자들에게 자원 배분과 예산 활용을 시각적으로 표현합니다.
## 성능 고려 사항
성능을 최적화하려면:
- 통합 문서 크기를 효율적으로 관리하여 메모리 사용량을 최소화합니다.
- 방대한 데이터 세트를 다루는 경우 Aspose.Cells의 대용량 파일 스트리밍과 같은 기능을 활용하세요.
- Java의 메모리 관리 모범 사례를 따르고, 리소스가 사용 후 적절하게 해제되도록 보장합니다.
## 결론
이 가이드를 따라 하면 Aspose.Cells for Java를 사용하여 Excel에서 원형 차트를 만들고, 구성하고, 사용자 지정하는 방법을 배울 수 있습니다. 이 강력한 라이브러리를 통해 개발자는 고급 스프레드시트 기능을 Java 애플리케이션에 원활하게 통합할 수 있습니다.
더 자세히 알아보려면 다른 차트 유형을 살펴보거나 Aspose.Cells가 제공하는 추가 기능으로 데이터 조작 기능을 확장해 보세요.
## FAQ 섹션
1. **Aspose.Cells를 무료로 사용할 수 있나요?**
   - 네, 무료 체험판을 이용하실 수 있습니다. 제한 없이 모든 기능을 이용하려면 임시 라이선스를 신청하세요.
2. **Aspose.Cells를 사용하여 다른 차트 유형을 만들 수 있나요?**
   - 물론입니다! 막대형 차트, 선 그래프 등을 조정하여 만들 수 있습니다. `ChartType`.
3. **Java를 사용하여 Excel에서 대용량 데이터 세트를 처리하려면 어떻게 해야 합니까?**
   - 효율적인 데이터 로딩 기술을 사용하고 매우 큰 파일의 경우 스트리밍을 고려하세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}