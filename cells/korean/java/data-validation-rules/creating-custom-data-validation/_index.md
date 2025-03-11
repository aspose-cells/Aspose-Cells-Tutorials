---
title: 사용자 정의 데이터 검증 생성
linktitle: 사용자 정의 데이터 검증 생성
second_title: Aspose.Cells Java Excel 처리 API
description: Aspose.Cells for Java를 사용하여 사용자 정의 데이터 검증을 만드는 방법을 알아보세요. 소스 코드가 포함된 단계별 가이드.
weight: 10
url: /ko/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 사용자 정의 데이터 검증 생성


## 소개

데이터 검증은 사용자가 Excel 스프레드시트에 잘못되거나 유효하지 않은 데이터를 입력하지 못하도록 하여 데이터 무결성을 유지하는 데 도움이 됩니다. Excel은 기본 제공 데이터 검증 옵션을 제공하지만 사용자 지정 검증 규칙을 정의해야 하는 시나리오가 있습니다. Aspose.Cells for Java를 사용하면 이를 효율적으로 달성할 수 있습니다.

## 필수 조건

코드를 살펴보기 전에 다음 전제 조건이 충족되었는지 확인하세요.

-  Java용 Aspose.Cells: 라이브러리를 다운로드하고 설치하세요.[여기](https://releases.aspose.com/cells/java/).

## 1단계: Java 프로젝트 설정

시작하려면 선호하는 통합 개발 환경(IDE)에서 새 Java 프로젝트를 만듭니다. Aspose.Cells for Java 라이브러리를 프로젝트의 클래스 경로에 추가합니다.

## 2단계: Excel 통합 문서 만들기

Aspose.Cells for Java를 사용하여 새 Excel 통합 문서를 만드는 것으로 시작해 보겠습니다.

```java
// 새 Excel 통합 문서를 만드는 Java 코드
Workbook workbook = new Workbook();
```

## 3단계: 워크시트 추가

이제 통합 문서에 사용자 지정 데이터 유효성 검사를 적용할 워크시트를 추가해 보겠습니다.

```java
// 워크시트를 추가하는 Java 코드
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 4단계: 사용자 정의 검증 기준 정의

이 단계에서는 데이터가 준수해야 하는 사용자 지정 검증 기준을 정의합니다. 셀에 입력된 연령을 18~60세로 제한하고 싶다고 가정해 보겠습니다.

```java
// 사용자 정의 검증 기준을 정의하는 Java 코드
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## 5단계: 범위에 데이터 검증 적용

이제 사용자 지정 유효성 검사 기준을 정의했으므로 이를 특정 셀 범위에 적용해 보겠습니다.

```java
// 범위에 데이터 검증을 적용하는 Java 코드
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // 첫 번째 10개 행에 검증을 적용합니다.
area.endColumn = 0;

validation.addArea(area);
```

## 6단계: Excel 파일 저장

마지막으로 사용자 지정 데이터 검증 규칙을 적용하여 Excel 파일을 저장합니다.

```java
// Excel 파일을 저장하는 Java 코드
workbook.save("CustomDataValidation.xlsx");
```

## 결론

이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 사용자 지정 데이터 검증 규칙을 만드는 방법을 살펴보았습니다. 이러한 단계를 따르면 Excel 데이터가 특정 기준을 준수하는지 확인하여 데이터 무결성과 정확성을 향상시킬 수 있습니다.

## 자주 묻는 질문

### Java용 Aspose.Cells를 어떻게 다운로드하나요?

 Aspose.Cells for Java는 웹사이트에서 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/java/).

### 같은 워크시트에서 여러 범위에 사용자 지정 데이터 유효성 검사를 적용할 수 있나요?

네, 원하는 각 범위에 대해 5단계를 반복하여 동일한 워크시트 내의 여러 범위에 사용자 지정 데이터 유효성 검사를 적용할 수 있습니다.

### Aspose.Cells for Java에서 지원하는 다른 유형의 데이터 검증이 있습니까?

네, Aspose.Cells for Java는 정수, 소수, 날짜, 시간, 텍스트 길이 등 다양한 유형의 데이터 유효성 검사를 지원합니다.

### 데이터 검증에 실패할 때 표시되는 오류 메시지를 사용자 지정하려면 어떻게 해야 하나요?

 오류 메시지를 수정하여 사용자 정의할 수 있습니다.`setErrorMessage` 4단계에서 검증 기준을 정의하는 방법입니다.

### Aspose.Cells for Java는 다양한 형식의 Excel 파일을 처리할 수 있나요?

네, Aspose.Cells for Java는 XLS, XLSX, XLSM 등 다양한 Excel 파일 형식을 지원합니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
