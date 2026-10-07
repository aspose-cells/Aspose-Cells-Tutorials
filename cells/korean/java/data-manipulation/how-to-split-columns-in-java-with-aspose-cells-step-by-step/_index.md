---
category: general
date: 2026-10-07
description: Aspose.Cells for Java를 사용하여 열을 분할하는 방법. 문자열을 열로 나누고, Excel 수식을 자동화하며,
  몇 줄의 코드로 셀에 수식을 작성하는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: ko
lastmod: 2026-10-07
og_description: Aspose.Cells를 사용하여 Java에서 열을 분할하는 방법. 이 튜토리얼에서는 문자열을 열로 분할하는 방법, Excel
  수식 평가를 자동화하는 방법, 그리고 셀에 수식을 쓰는 방법을 보여줍니다.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Aspose.Cells를 사용한 Java에서 열 분할 방법 – 빠른 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells를 사용한 Java에서 열 분할 방법 – 단계별 가이드
url: /ko/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java와 Aspose.Cells를 사용하여 열을 분할하는 방법 – 단계별 가이드

Excel 워크시트에서 프로그래밍 방식으로 **열을 분할하는 방법**이 필요하다면, 이 가이드는 Aspose.Cells for Java를 사용한 전체 과정을 보여줍니다. 또한 **문자열을 열로 분할하는 방법**, **Excel 수식 자동화** 평가, 그리고 **셀에 수식 쓰기**를 간결하고 프로덕션 수준의 코드로 배울 수 있습니다.

프로그램을 통한 열 분할은 수동 복사‑붙여넣기를 없애고 오류를 줄이며 대규모 데이터 변환을 가능하게 합니다. 이 튜토리얼을 마치면 실시간으로 수식을 생성, 수정 및 평가할 수 있어 Excel을 Java 백엔드의 진정한 일부로 만들 수 있습니다.

## 사전 요구 사항

* Java 17 이상이 설치되어 있어야 합니다.
* Maven 3.8+ (또는 Gradle)를 사용한 의존성 관리.
* Aspose.Cells for Java 라이선스(학습용으로는 무료 평가판도 작동합니다).
* Java 구문 및 Excel 개념에 대한 기본적인 이해.

위 항목 중 하나라도 없으면 먼저 설치하십시오; 코드 샘플은 표준 Maven 프로젝트를 전제로 합니다.

## 단계 1: 프로젝트에 Aspose.Cells 추가

`pom.xml`에 다음 의존성을 추가합니다. 이는 최신 안정 버전의 Aspose.Cells 라이브러리를 가져옵니다.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**이 단계가 중요한 이유:** 이 라이브러리는 Microsoft Office 없이 Excel 파일을 조작하는 데 필요한 `Workbook`, `Worksheet`, `Cell` 클래스를 제공합니다. 의존성이 없으면 코드를 컴파일할 수 없습니다.

## 단계 2: 워크북을 생성하고 첫 번째 워크시트를 선택

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

`Workbook` 객체는 전체 Excel 파일을 나타냅니다. 첫 번째 워크시트에 접근하면 우리가 작성할 수식의 예측 가능한 시작점을 확보할 수 있습니다.

## 단계 3: 대상 셀에 WRAPCOLS 수식 작성

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**우리가 `WRAPCOLS`를 사용하는 이유:** 내장 Excel 함수 `WRAPCOLS`는 단일 텍스트 값을 정의된 열 수로 자동으로 분할하며, 단어 경계를 지능적으로 처리합니다. 이는 사용자 정의 파싱 로직 없이 **문자열을 열로 분할**하는 가장 신뢰할 수 있는 방법입니다.

## 단계 4: 워크북이 수식을 평가하도록 강제

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

`calculateFormula()`를 호출하면 서버 측에서 **Excel 수식 자동화** 평가가 이루어집니다. 이 호출이 없으면 셀에는 계산된 값이 아니라 수식 텍스트가 그대로 남습니다.

## 단계 5: 래핑된 결과를 가져와 표시

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

프로그램을 실행하면 콘솔에 다음이 출력됩니다:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

생성된 `SplitColumnsResult.xlsx` 파일은 분할된 텍스트가 채워진 세 개의 열을 보여줍니다.

## WRAPCOLS 함수 이해

* **구문:** `WRAPCOLS(text, columns, [delimiter])`
* **매개변수:**
  * `text` – 분할하려는 문자열.
  * `columns` – 텍스트를 배분할 열 수.
  * `delimiter` (옵션) – 문자열을 구분하는 문자; 기본값은 공백.
* **반환값:** 인접 셀에 흘러들어가는 배열이며, 각 요소는 원본 텍스트의 일부를 포함합니다.

함수가 가로로 흘러들어가기 때문에, 예시에서는 가장 왼쪽 셀(A1)에만 수식을 작성하면 됩니다. Excel은 필요에 따라 자동으로 B1, C1, …을 채웁니다.

## 일반적인 변형 및 엣지 케이스

| 상황 | 권장 조정 |
|-----------|------------------------|
| **가변 열 수** | 하드코딩된 `3`을 변수로 교체합니다: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **사용자 정의 구분자** | 세 번째 인수를 사용합니다. 예: `=WRAPCOLS(A2,4,",")`를 사용해 쉼표로 분할합니다. |
| **빈 원본 문자열** | 함수는 빈 셀을 반환합니다; 수식을 설정하기 전에 `null` 또는 빈 문자열을 방지하세요. |
| **대용량 데이터셋** | 각 행에 대해 루프 내에서 수식을 적용하고, 루프가 끝난 후 한 번만 `calculateFormula()`를 호출해 성능을 향상시킵니다. |
| **비ASCII 문자** | WRAPCOLS는 유니코드를 지원합니다; Java 소스 파일이 UTF‑8로 저장되었는지 확인하세요. |

**프로 팁:** 많은 행을 처리할 때는 수식을 문자열 변수에 저장하고 재사용하여 반복적인 문자열 연결 오버헤드를 피하세요.

## 전체 실행 가능한 예제

아래는 복사‑붙여넣기 가능한 전체 프로그램입니다. import 문, 예외 처리 및 선택적 저장 작업이 포함되어 있습니다.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

이 프로그램을 실행하면 앞서 보여진 동일한 콘솔 출력이 생성되고, **열을 분할하는 방법**을 명확히 보여주는 Excel 파일이 작성됩니다.

## 문제 해결 체크리스트

* **수식이 평가되지 않음** – 수식을 설정한 후 `workbook.calculateFormula()`가 호출되었는지 확인하세요.
* **분할 후 빈 셀** – 원본 문자열이 `null`이 아니고 비어 있지 않은지, 열 수가 0보다 큰지 확인하세요.
* **라이선스 예외** – 워크북을 생성하기 전에 유효한 Aspose.Cells 라이선스 파일(`License license = new License(); license.setLicense("Aspose.Total.lic");`)을 제공하여 평가 워터마크를 제거하세요.
* **대형 시트에서 성능 지연** – 각 셀마다가 아니라 모든 수식을 작성한 후 한 번만 `calculateFormula()`를 호출하세요.

## 결론

이제 Aspose.Cells를 사용해 Java에서 **열을 분할하는 방법**, `WRAPCOLS` 함수로 **문자열을 열로 분할하는 방법**, **Excel 수식 자동화** 평가 방법, 그리고 프로그래밍 방식으로 **셀에 수식 쓰는 방법**을 알게 되었습니다. 이 기법은 수동 데이터 준비 단계를 없애고 Excel의 강력한 텍스트 처리 기능을 Java 애플리케이션에 직접 통합합니다.

### 다음 단계

* `TEXTSPLIT` 및 `FILTERXML`과 같은 다른 텍스트 함수를 탐색하여 더 복잡한 파싱 시나리오에 활용하세요.
* 예기치 않은 입력을 부드럽게 처리하기 위해 `WRAPCOLS`를 `IFERROR`와 결합하세요.
* 이 솔루션을 REST를 통해 CSV 데이터를 받고 채워진 Excel 파일을 반환하는 Spring Boot 서비스에 통합하세요.

이 패턴을 마스터하면 비즈니스 요구에 맞게 확장 가능한 견고하고 자동화된 Excel 워크플로를 구축할 수 있습니다. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 작동 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [aspose cells java – 이름을 열로 분할](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Java에서 Aspose.Cells를 사용해 Excel 열 자동 맞춤](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Aspose.Cells Java를 사용해 Excel에서 빈 열 삭제하기: 종합 가이드](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}