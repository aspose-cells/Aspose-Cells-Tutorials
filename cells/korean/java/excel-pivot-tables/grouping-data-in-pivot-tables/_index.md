---
"description": "Aspose.Cells for Java를 사용하여 Excel에서 피벗 테이블을 만드는 방법을 알아보세요. 소스 코드 예제를 통해 데이터 그룹화 및 분석을 자동화하세요."
"linktitle": "피벗 테이블에서 데이터 그룹화"
"second_title": "Aspose.Cells Java Excel 처리 API"
"title": "피벗 테이블에서 데이터 그룹화"
"url": "/ko/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 테이블에서 데이터 그룹화


피벗 테이블은 스프레드시트의 데이터를 분석하고 요약하는 강력한 도구입니다. 데이터를 그룹화하고 분류하여 귀중한 통찰력을 얻을 수 있습니다. 이 글에서는 Aspose.Cells for Java를 사용하여 피벗 테이블에서 데이터를 효과적으로 그룹화하는 방법과 소스 코드 예제를 살펴보겠습니다.

## 소개

피벗 테이블은 대용량 데이터세트의 데이터를 구성하고 요약하는 유연한 방법을 제공합니다. 데이터를 범주 또는 계층 구조로 그룹화하여 사용자 지정 뷰를 만들 수 있습니다. 이를 통해 데이터에서 추세, 패턴 및 이상값을 더 쉽게 파악할 수 있습니다.

## 1단계: 피벗 테이블 만들기

Aspose.Cells for Java를 사용하여 피벗 테이블을 만들어 보겠습니다. 아래는 샘플 Excel 파일에서 피벗 테이블을 만드는 방법의 예입니다.

```java
// Excel 파일을 로드합니다
Workbook workbook = new Workbook("sample.xlsx");

// 데이터가 포함된 워크시트에 액세스하세요
Worksheet worksheet = workbook.getWorksheets().get(0);

// 데이터 범위를 지정하세요
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // 20행의 데이터를 가정합니다
sourceData.startColumn = 0;
sourceData.endColumn = 3; // 4개의 데이터 열을 가정합니다

// 데이터 범위를 기반으로 피벗 테이블 만들기
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// 인덱스로 피벗 테이블 가져오기
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// 행과 열에 필드 추가
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// 값을 추가하고 집계를 적용합니다.
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// 수정된 Excel 파일을 저장합니다.
workbook.save("output.xlsx");
```

## 2단계: 데이터 그룹화

Java용 Aspose.Cells에서는 다음을 사용하여 피벗 테이블 내에서 데이터를 그룹화할 수 있습니다. `PivotField` 클래스. 다음은 피벗 테이블에서 필드를 그룹화하는 방법의 예입니다.

```java
// 피벗 테이블의 "제품" 필드에 액세스합니다.
PivotField productField = pivotTable.getPivotFields().get("Product");

// "제품" 필드를 특정 기준(예: 시작 문자)으로 그룹화합니다.
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// 수정된 Excel 파일을 그룹화된 데이터로 저장합니다.
workbook.save("output_grouped.xlsx");
```

## 3단계: 그룹화 사용자 정의

날짜 기반 그룹화 간격이나 사용자 지정 그룹화 규칙 지정 등 그룹화 설정을 더욱 세부적으로 사용자 지정할 수 있습니다. 날짜 기반 그룹화를 사용자 지정하는 예는 다음과 같습니다.

```java
// 피벗 테이블의 "날짜" 필드에 액세스합니다(날짜 필드인 경우)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// 월별로 날짜를 그룹화합니다.
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// 사용자 정의 날짜 그룹화로 수정된 Excel 파일을 저장합니다.
workbook.save("output_custom_grouping.xlsx");
```

## 결론

피벗 테이블에서 데이터를 그룹화하는 것은 Excel에서 데이터를 분석하고 요약하는 데 유용한 기술이며, Aspose.Cells for Java를 사용하면 이 과정을 쉽게 자동화할 수 있습니다. 제공된 소스 코드 예제를 사용하면 피벗 테이블을 만들고, 그룹화를 사용자 지정하고, 데이터에서 효율적으로 통찰력을 얻을 수 있습니다.

## 자주 묻는 질문

### 1. Excel에서 피벗 테이블의 목적은 무엇입니까?

Excel의 피벗 테이블은 대규모 데이터 세트를 요약하고 분석하는 데 사용됩니다. 피벗 테이블을 사용하면 데이터에 대한 사용자 지정 뷰를 만들어 패턴과 추세를 더 쉽게 파악할 수 있습니다.

### 2. 피벗 테이블의 데이터 그룹화를 사용자 지정하려면 어떻게 해야 하나요?

피벗 테이블의 데이터 그룹화를 사용자 정의하려면 다음을 사용하십시오. `PivotField` Java용 Aspose.Cells의 클래스입니다. 이를 통해 날짜 기반 간격이나 사용자 지정 규칙과 같은 그룹화 기준을 지정할 수 있습니다.

### 3. Aspose.Cells for Java를 사용하여 피벗 테이블 생성을 자동화할 수 있나요?

네, 제공된 소스 코드 예제에서 보여주듯이, Aspose.Cells for Java를 사용하여 Excel에서 피벗 테이블을 자동으로 만들 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}