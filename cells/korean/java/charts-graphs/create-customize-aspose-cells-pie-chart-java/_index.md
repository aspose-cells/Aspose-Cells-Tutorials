---
"date": "2025-04-08"
"description": "Aspose.Cells for Java를 사용하여 원형 차트를 만들고 사용자 지정하는 방법을 알아보세요. 개발자를 위한 코드 예제가 포함된 단계별 가이드입니다."
"title": "Aspose.Cells 마스터하기&#58; Java로 파이 차트 만들기 및 사용자 정의"
"url": "/ko/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells 마스터하기: Java로 파이 차트 만들기 및 사용자 정의

## 소개
Excel에서 데이터 시각화를 다룰 때 시각적으로 매력적인 차트를 만드는 것은 일반적인 요구 사항입니다. 인구 통계 정보를 제시하거나 시장 동향을 분석할 때 원형 차트는 비례 데이터를 명확하게 표현하는 방법을 제공합니다. 하지만 이러한 차트를 프로그래밍 방식으로 설정하는 것은 복잡할 수 있습니다. 이 튜토리얼에서는 Java를 사용하여 Aspose.Cells 원형 차트를 만들고 사용자 지정하는 방법을 안내하여 개발자의 프로세스를 간소화합니다.

**배울 내용:**
- Aspose.Cells for Java로 환경을 설정하세요.
- 새 통합 문서를 만들고 워크시트 셀에 액세스합니다.
- 차트 생성을 준비하기 위해 특정 셀에 데이터를 채웁니다.
- 이 데이터에서 원형 차트를 생성합니다.
- 색상, 제목, 범례를 포함하여 파이 차트의 모양을 사용자 정의합니다.

시작하기 전에 Java 프로그래밍과 Maven 또는 Gradle 종속성 관리에 대한 기본적인 이해가 있는지 확인하세요. 이제 환경을 설정해 봅시다!

## 필수 조건
이 튜토리얼을 따라하려면 다음이 필요합니다.
- **자바 개발 키트(JDK)**: 버전 8 이상.
- **통합 개발 환경(IDE)**: IntelliJ IDEA나 Eclipse와 같은 것.
- **종속성 관리**: Maven이나 Gradle을 사용하여 종속성을 관리합니다.

### 필수 라이브러리 및 종속성
Maven이나 Gradle을 사용하여 프로젝트에 Java용 Aspose.Cells를 포함해야 합니다.

**메이븐**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**그래들**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 라이센스 취득 단계
Aspose.Cells for Java는 상용 라이브러리이지만, 무료 평가판으로 시작하거나 임시 라이선스를 신청할 수 있습니다. [구매 페이지](https://purchase.aspose.com/buy) 라이선싱 옵션을 살펴보세요.

## Java용 Aspose.Cells 설정
먼저, 위에서 설명한 것처럼 Maven이나 Gradle을 통해 필요한 라이브러리를 추가하여 프로젝트 환경에 필요한 라이브러리가 포함되어 있는지 확인하세요. 라이브러리가 포함되면 Aspose.Cells를 초기화할 수 있습니다.

```java
import com.aspose.cells.Workbook;

// 새 통합 문서 인스턴스 초기화
Workbook workbook = new Workbook();
```

## 구현 가이드

### 통합 문서 만들기 및 구성
통합 문서를 만드는 것은 데이터를 설정하는 첫 단계입니다.

#### 라이브러리 가져오기
다음 가져오기가 파일 맨 위에 포함되어 있는지 확인하세요.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### 1단계: 통합 문서 인스턴스 만들기
```java
// 작업할 빈 통합 문서 인스턴스를 만듭니다.
Workbook workbook = new Workbook();
```
이 단계에서는 Excel 파일을 프로그래밍 방식으로 초기화하여 Aspose.Cells 기능을 사용하여 조작할 수 있습니다.

### 워크시트 셀 액세스 또는 수정
다음으로, 파이 차트에 사용될 워크시트 셀에 데이터를 채웁니다.

#### 2단계: 워크시트 및 셀에 액세스
```java
// 통합 문서의 첫 번째 워크시트에 액세스합니다.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// 원형 차트에 사용되는 샘플 값을 특정 셀에 입력합니다.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// 원형 차트의 백분율 값을 특정 셀에 입력합니다.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
여기에서는 파이 차트의 다양한 세그먼트를 나타내는 데이터로 워크시트를 채웁니다.

### 파이 차트 만들기

#### 3단계: 워크시트에 원형 차트 추가
```java
// 워크시트에 원형 차트를 만듭니다.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
이 단계에서는 지정된 위치와 크기에 워크시트에 새로운 원형 차트를 추가합니다.

### 파이 차트 시리즈 및 데이터 구성

#### 4단계: 차트 시리즈 설정
```java
// 차트의 시리즈 데이터 범위를 구성합니다.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// 원형 차트 제목을 제목 텍스트가 포함된 셀에 연결합니다.
pie.getTitle().setLinkedSource("D2");
```
이 코드는 데이터 범위를 연결하고 원형 차트의 시리즈를 설정합니다.

### 차트 범례 및 제목 모양 구성

#### 5단계: 차트 범례 및 제목 사용자 지정
```java
// 차트 하단에 범례 위치를 설정합니다.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// 차트 제목의 글꼴 속성을 설정합니다.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
모양을 사용자 지정하면 가독성과 시각적 매력이 향상됩니다.

### 차트 시리즈 색상 사용자 정의

#### 6단계: 파이 세그먼트 색상 변경
```java
import com.aspose.cells.Color;

// 개별 파이 차트 세그먼트의 색상에 접근하여 사용자 정의합니다.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
이러한 설정을 사용하면 특정 색상 구성표에 맞게 차트를 개인화할 수 있습니다.

### 열 자동 맞춤 및 통합 문서 저장

#### 7단계: 열 너비 조정 및 파일 저장
```java
// 모든 열에 자동 맞춤을 적용합니다.
worksheet.autoFitColumns();

// 통합 문서를 저장하기 위한 출력 디렉토리 플레이스홀더 경로를 정의합니다.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// 수정된 통합 문서를 지정된 디렉토리의 Excel 파일로 저장합니다.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
마지막으로, 열을 자동으로 맞추고 통합 문서를 저장합니다.

## 실제 응용 프로그램
1. **인구 통계 분석**: 원형 차트를 사용하면 여러 국가나 지역의 인구 분포를 표시할 수 있습니다.
2. **시장 점유율 보고서**: 특정 산업 분야에서 다양한 회사의 시장점유율을 보여줍니다.
3. **예산 할당**: 조직 내 다양한 부서에 예산이 어떻게 할당되는지 시각화합니다.

이러한 애플리케이션은 실제 시나리오에서 Aspose.Cells의 다재다능함과 유용성을 보여줍니다.

## 성능 고려 사항
Aspose.Cells를 사용할 때 성능을 최적화하려면:
- 더 이상 필요하지 않은 객체를 삭제하여 메모리 사용량을 최소화합니다.
- 대용량 데이터 세트를 처리하려면 효율적인 데이터 구조를 사용하세요.
- 병목 현상을 파악하기 위해 애플리케이션 프로파일을 작성하세요.

모범 사례를 준수하면 원활하고 반응성이 뛰어난 애플리케이션을 보장할 수 있습니다.

## 결론
이 튜토리얼에서는 Java에서 Aspose.Cells를 사용하여 원형 차트를 만들고 사용자 지정하는 방법을 단계별로 안내했습니다. 이 지식을 바탕으로 이제 프로젝트의 다양한 데이터 시각화 작업에 이러한 기법을 적용할 수 있습니다. 더 자세히 알아보려면 Aspose.Cells에서 제공하는 추가 차트 유형과 고급 사용자 지정 옵션을 살펴보세요.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}