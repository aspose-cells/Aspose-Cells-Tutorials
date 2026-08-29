---
category: general
date: 2026-08-08
description: Aspose.Cells에서 피벗 테이블을 복사하고 Java를 사용하여 범위를 워크북에 복사하는 방법. CopyOptions를
  사용하여 피벗 테이블을 복제하는 정확한 단계들을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: ko
lastmod: 2026-08-08
og_description: Aspose.Cells에서 피벗 테이블을 복사하고 Java로 범위를 워크북에 복사하는 방법. CopyOptions를 사용하여
  피벗 테이블을 복제하는 전체 가이드를 확인하세요.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Aspose.Cells에서 피벗 복사 방법 – 범위를 워크북에 복사
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Aspose.Cells에서 피벗 복사 방법 – 범위를 워크북에 복사
url: /ko/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells에서 피벗 복사 – 워크북에 범위 복사

Aspose.Cells를 사용하여 Excel 파일에서 **피벗 복사 방법**이 필요하다면, 이 가이드는 정확한 절차를 보여줍니다. 튜토리얼이 끝날 때쯤에는 피벗 테이블 정의를 보존하면서 **범위를 워크북에 복사**할 수 있게 됩니다.

예제는 Java를 사용하지만, 동일한 개념은 Aspose.Cells와 함께 작동하는 모든 .NET 언어에도 적용됩니다. 외부 도구는 필요 없으며—Aspose.Cells for Java 라이브러리와 기본 개발 환경만 있으면 됩니다.

## 사전 요구 사항

* Java Development Kit (JDK) 8 이상.
* Maven 또는 Gradle을 사용하여 종속성을 관리 (예제는 Maven 사용).
* 프로젝트에 추가된 Aspose.Cells for Java 23.9 (또는 최신 버전).
* 첫 번째 워크시트에 피벗 테이블이 최소 하나 포함된 입력 워크북(`input.xlsx`).

이 항목들을 준비하면 코드가 워크북에 접근할 때 런타임 오류를 방지할 수 있습니다.

## Aspose.Cells로 피벗 복사 방법

이 섹션에서는 시트의 한 부분에서 다른 부분으로 **피벗 복사 방법**을 수행하는 데 필요한 각 단계를 `CopyOptions` 클래스를 사용하여 설명합니다.

### 단계 1: 프로젝트에 Aspose.Cells 추가

Maven을 사용하는 경우, 다음 의존성을 `pom.xml`에 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*이 단계가 중요한 이유*: 이 라이브러리는 **aspose.cells copy range** 작업에 필요한 `Workbook`, `CopyOptions` 및 기타 클래스를 제공합니다. 의존성이 없으면 컴파일러가 해당 타입을 찾을 수 없습니다.

### 단계 2: 소스 워크북 로드

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

파일을 로드하면 스프레드시트의 메모리 내 표현이 생성됩니다. `Workbook` 객체를 통해 워크시트, 셀 및 피벗 테이블에 접근할 수 있습니다.

### 단계 3: 피벗 테이블을 포함하도록 복사 옵션 구성

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)`는 Aspose.Cells에 해당 작업이 피벗 테이블 메타데이터를 보존해야 함을 알려줍니다. 이 플래그를 생략하면 피벗 테이블이 정적 데이터로 변환되어 인터랙티브 기능을 잃게 됩니다.

### 단계 4: 피벗 테이블이 포함된 원하는 범위 복사

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange` 메서드는 셀, 서식 및—이전 단계에서 설정한 옵션 때문에—범위와 교차하는 모든 피벗 테이블을 복사합니다. 이것이 **copy range to workbook** 기능의 핵심입니다.

### 단계 5: 수정된 워크북 저장

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

저장을 하면 변경 사항이 새 파일(`output.xlsx`)에 기록됩니다. 이제 Excel에서 이 파일을 열어 보면 피벗 테이블이 복사된 범위와 정확히 동일한 위치에 복제된 것을 확인할 수 있습니다.

## 전체 실행 가능한 예제

모든 요소를 합치면, 컴파일하고 실행할 수 있는 전체 프로그램은 다음과 같습니다:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 예상 결과

* `output.xlsx`는 `input.xlsx`와 동일한 데이터를 포함합니다.
* 원본 범위를 차지하던 피벗 테이블이 대상 셀에 나타나며, 완전하게 기능합니다(필터, 새로 고침 기능 등).
* `copyRange`가 전체 셀 블록을 복사하기 때문에 모든 셀 서식, 수식 및 열 너비가 보존됩니다.

## 일반적인 질문 및 엣지 케이스

**목적지 범위가 기존 피벗 테이블과 겹치는 경우는?**  
Aspose.Cells는 대상 셀을 덮어씁니다. 데이터 손실을 방지하려면 목적지 영역이 비어 있거나 기존 피벗 테이블을 먼저 이동하십시오.

**워크시트 간에 피벗 테이블을 복사할 수 있나요?**  
예. `targetSheetIndex`가 대상 시트를 가리키도록 `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` 를 사용하십시오.

**`setCopyPivotTable(true)`가 기본 데이터 소스를 복사합니까?**  
이 메서드는 피벗 캐시 참조만 복사합니다. 소스 데이터가 동일한 워크북에 있으면 대상 피벗은 동일한 캐시를 가리킵니다. 캐시를 복제하려면 새 피벗 캐시를 수동으로 생성해야 합니다.

**큰 범위를 효율적으로 복사하려면?**  
매우 큰 범위를 복사할 때는 필요할 경우에만 `CopyOptions.setCopyFormula(true)`와 `setCopyDataValidation(true)`를 사용하십시오. 옵션 수를 줄이면 성능이 향상될 수 있습니다.

## 안정적인 **aspose.cells copy range** 사용을 위한 팁

* **프로 팁:** 범위에 피벗 캐시를 참조하는 수식이 포함된 경우 복사 후 항상 `workbook.calculateFormula()`를 호출하십시오.
* **주의할 점:** 숨겨진 워크시트. `copyRange`는 숨겨진 시트를 명시적으로 인덱스로 지정하지 않는 한 보이는 워크시트에서만 작동합니다.
* **버전 확인:** `setCopyPivotTable` 플래그는 Aspose.Cells 20.9부터 제공됩니다. 사용 중인 라이브러리 버전이 이를 지원하는지 확인하십시오.

## 결론

이제 Aspose.Cells에서 **피벗 복사 방법**과 **범위를 워크북에 복사**하여 전체 피벗 기능을 보존하는 방법을 알게 되었습니다. 라이브러리 추가, 워크북 로드, `CopyOptions` 구성, 복사 수행, 저장이라는 단계는 다른 복사‑붙여넣기 시나리오에도 적용할 수 있는 반복 가능한 패턴을 형성합니다.

다음으로 차트, 조건부 서식 및 데이터 검증을 위한 **aspose.cells copy range**와 같은 관련 주제를 살펴보세요. 다양한 파일 형식 간 복사(XLSX → XLS)를 실험하여 자동화 역량을 확장하십시오. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방법을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용하여 Excel에서 피벗 테이블 만들기: 종합 가이드](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 피벗 테이블 소스 업데이트: 종합 가이드](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 피벗 테이블에 슬라이서 구현: 종합 가이드](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}