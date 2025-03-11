---
title: 동적 피벗 테이블
linktitle: 동적 피벗 테이블
second_title: Aspose.Cells Java Excel 처리 API
description: Aspose.Cells for Java를 사용하여 동적 피벗 테이블을 손쉽게 만드세요. 데이터를 쉽게 분석하고 요약하세요. 데이터 분석 역량을 강화하세요.
weight: 13
url: /ko/java/excel-pivot-tables/dynamic-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 동적 피벗 테이블


피벗 테이블은 데이터 분석에서 강력한 도구로, 스프레드시트에서 데이터를 요약하고 조작할 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for Java API를 사용하여 동적 피벗 테이블을 만드는 방법을 살펴보겠습니다.

## 피벗 테이블 소개

피벗 테이블은 스프레드시트에서 데이터를 요약하고 분석할 수 있는 대화형 테이블입니다. 데이터를 구성하고 분석하는 동적인 방법을 제공하여 통찰력을 얻고 정보에 입각한 결정을 내리는 것을 더 쉽게 만듭니다.

## 1단계: Aspose.Cells 라이브러리 가져오기

 동적 피벗 테이블을 만들기 전에 Aspose.Cells 라이브러리를 Java 프로젝트로 가져와야 합니다. Aspose 릴리스에서 라이브러리를 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/java/).

라이브러리를 다운로드한 후 프로젝트의 빌드 경로에 추가하세요.

## 2단계: 통합 문서 로드

피벗 테이블로 작업하려면 먼저 분석하려는 데이터가 포함된 통합 문서를 로드해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```java
// Excel 파일을 로드합니다
Workbook workbook = new Workbook("your_excel_file.xlsx");
```

 바꾸다`"your_excel_file.xlsx"` Excel 파일의 경로를 포함합니다.

## 3단계: 피벗 테이블 만들기

이제 워크북을 로드했으니 피벗 테이블을 만들어 보겠습니다. 피벗 테이블의 원본 데이터 범위와 워크시트에 배치할 위치를 지정해야 합니다. 다음은 예입니다.

```java
// 첫 번째 워크시트를 받으세요
Worksheet worksheet = workbook.getWorksheets().get(0);

// 피벗 테이블의 데이터 범위를 지정하세요
String sourceData = "A1:D10"; // 데이터 범위로 바꾸세요

// 피벗 테이블의 위치를 지정하세요
int firstRow = 1;
int firstColumn = 5;

// 피벗 테이블 만들기
PivotTable pivotTable = worksheet.getPivotTables().add(sourceData, worksheet.getCells().get(firstRow, firstColumn), "PivotTable1");
```

## 4단계: 피벗 테이블 구성

이제 피벗 테이블을 만들었으므로 필요에 따라 데이터를 요약하고 분석하도록 구성할 수 있습니다. 행 필드, 열 필드, 데이터 필드를 설정하고 다양한 계산을 적용할 수 있습니다. 다음은 예입니다.

```java
// 피벗 테이블에 필드 추가
pivotTable.addFieldToArea(PivotFieldType.ROW, 0); // 행 필드
pivotTable.addFieldToArea(PivotFieldType.COLUMN, 1); // 열 필드
pivotTable.addFieldToArea(PivotFieldType.DATA, 2); // 데이터 필드

// 데이터 필드에 대한 계산을 설정하세요
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);
```

## 5단계: 피벗 테이블 새로 고침

피벗 테이블은 동적일 수 있습니다. 즉, 소스 데이터가 변경되면 자동으로 업데이트됩니다. 피벗 테이블을 새로 고치려면 다음 코드를 사용할 수 있습니다.

```java
// 피벗 테이블 새로 고침
pivotTable.refreshData();
pivotTable.calculateData();
```

## 결론

이 튜토리얼에서는 Aspose.Cells for Java API를 사용하여 동적 피벗 테이블을 만드는 방법을 알아보았습니다. 피벗 테이블은 데이터 분석을 위한 귀중한 도구이며 Aspose.Cells를 사용하면 Java 애플리케이션에서 피벗 테이블의 생성 및 조작을 자동화할 수 있습니다.

질문이 있거나 추가 지원이 필요하면 언제든지 문의하세요. 즐거운 코딩 되세요!

## 자주 묻는 질문

### 질문 1: 피벗 테이블 데이터 필드에 사용자 지정 계산을 적용할 수 있나요?

네, 사용자 정의 논리를 구현하여 데이터 필드에 사용자 정의 계산을 적용할 수 있습니다.

### 질문 2: 피벗 테이블의 서식을 어떻게 변경할 수 있나요?

피벗 테이블의 서식을 변경하려면 스타일 속성에 액세스하고 원하는 서식을 적용하면 됩니다.

### 질문 3: 같은 워크시트에 여러 개의 피벗 테이블을 만들 수 있나요?

네, 서로 다른 대상 위치를 지정하여 동일한 워크시트에 여러 피벗 테이블을 만들 수 있습니다.

### Q4: 피벗 테이블에서 데이터를 필터링할 수 있나요?

네, 피벗 테이블에 필터를 적용하여 특정 데이터 하위 집합을 표시할 수 있습니다.

### 질문 5: Aspose.Cells는 Excel의 고급 피벗 테이블 기능을 지원하나요?

네, Aspose.Cells는 Excel의 고급 피벗 테이블 기능에 대한 광범위한 지원을 제공하여 복잡한 피벗 테이블을 만들 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
