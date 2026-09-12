---
category: general
date: 2026-09-11
description: Aspose.Cells를 사용하여 새 워크시트를 만들고 Excel 범위를 복사합니다. 피벗 테이블을 유지하면서 시트 간에 범위를
  복사하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: ko
lastmod: 2026-09-11
og_description: Aspose.Cells를 사용하여 새 워크시트를 만들고 Excel 범위를 복사합니다. 이 튜토리얼에서는 시트 간 범위를
  복사하고 피벗 테이블을 그대로 유지하는 정확한 단계를 보여줍니다.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: 새 워크시트를 만들고 Excel 범위를 복사 – Aspose.Cells 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Aspose.Cells를 사용하여 새 워크시트를 만들고 Excel 범위를 복사하기
url: /ko/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 새 워크시트를 만들고 Aspose.Cells로 Excel 범위 복사하기

Excel 파일에서 **새 워크시트를 만들고** 데이터를 이동해야 할 경우, Aspose.Cells를 사용하면 간단합니다. 이 가이드는 피벗 테이블을 포함한 범위를 유지하면서 한 시트에서 다른 시트로 Excel 범위를 복사하는 방법을 정확히 보여줍니다.

여기서는 **copy excel range**, **copy range between sheets** 방법, 그리고 Aspose.Cells `copy` 메서드가 피벗 테이블 정의를 그대로 유지하는 이유를 배웁니다. 외부 도구는 필요 없으며, Aspose.Cells 라이브러리가 포함된 Java 프로젝트만 있으면 됩니다.

## 사전 요구 사항

- Java 17 이상이 설치되어 있음
- 프로젝트 클래스패스에 Aspose.Cells for Java (버전 23.12 이상) 추가
- `input.xlsx`라는 피벗 테이블이 포함된 복사하려는 범위를 가진 원본 워크북
- Java 문법 및 Maven/Gradle 의존성 관리에 대한 기본 지식

## 단계 1: 프로젝트 설정 및 Aspose.Cells 가져오기

간단한 Maven 프로젝트(또는 선호한다면 Gradle)를 생성하고 Aspose.Cells 의존성을 추가합니다:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

그런 다음 Java 소스 파일에 필요한 클래스를 가져옵니다:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Why this step matters*: 올바른 클래스를 가져오면 `Workbook`, `Worksheet`, `Range`, 그리고 범위 전송을 처리할 `copy` 메서드에 접근할 수 있습니다.

## 단계 2: 원본 워크북 로드

복사하려는 데이터가 들어 있는 워크북을 엽니다. 다음 코드는 지정한 디렉터리에서 `input.xlsx`를 로드합니다:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explanation*: `Workbook`은 전체 Excel 파일을 나타냅니다. 한 번 로드하면 모든 시트와 셀 컬렉션에 대한 읽기/쓰기 접근 권한을 얻습니다.

## 단계 3: 피벗 테이블을 포함하는 원본 범위 식별

피벗 테이블이 있는 워크시트를 선택하고 복사하려는 정확한 셀 블록을 정의합니다. 이 예제에서는 A1부터 D20까지의 셀을 복사합니다:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Why this matters*: `Range` 객체를 생성함으로써 Aspose.Cells에 어떤 셀(피벗 테이블과 같은 포함된 객체 포함)을 복제할지 정확히 지정합니다.

## 단계 4: **새 워크시트**를 만들어 복사된 데이터를 받기

이제 같은 워크북에 새로운 시트를 추가합니다. 여기서 주요 키워드가 등장합니다:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explanation*: 새 시트를 추가하면 복사된 데이터가 격리되어, 원본 시트에 영향을 주지 않고 **copy excel range** 작업이 성공했는지 쉽게 확인할 수 있습니다.

## 단계 5: 범위 복사 – 피벗 테이블이 자동으로 보존됨

`copy` 메서드를 사용하여 원본 시트에서 대상 시트로 범위를 이동합니다. Aspose.Cells는 수식, 서식 및 피벗 테이블 정의를 복사합니다:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Why this works*: `copy` 메서드는 소스 셀을 깊게 복사합니다. 값만 복사하는 것이 아니라 피벗 캐시를 포함한 전체 셀 구조를 복제합니다. 그래서 **copy range aspose.cells**를 수행해도 새로운 시트에서 기능적인 피벗 테이블을 볼 수 있습니다.

## 단계 6: 새 워크시트와 함께 워크북 저장

마지막으로 수정된 워크북을 디스크에 기록합니다:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Result*: `output.xlsx`에는 원본 시트와 **Copy**라는 새 시트가 포함되며, 동일한 범위와 피벗 테이블이 그대로 들어 있습니다.

## 전체 작업 예제

모든 코드를 합치면 다음과 같은 완전한 실행 가능한 프로그램이 됩니다:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected output**: Excel에서 `output.xlsx`를 열면 **Copy**라는 시트가 나타나며, 셀 A1:D20에 원본과 동일한 데이터, 서식 및 활성 피벗 테이블이 포함됩니다.

## 일반적인 질문 및 엣지 케이스

- **원본 범위에 병합된 셀이 포함된 경우는 어떻게 되나요?**  
  `copy` 메서드는 병합 정보도 복사하므로, 대상 시트에서 병합된 셀이 그대로 유지됩니다.

- **다른 워크북으로 복사할 수 있나요?**  
  예. 두 번째 `Workbook` 인스턴스를 로드하고, 해당 워크북에 대상 범위를 만든 뒤 `sourceRange.copy(destinationRange)`를 호출합니다. 메서드는 교차 워크북 복사를 자동으로 처리합니다.

- **대상 시트에 이미 데이터가 있는 경우는 어떻게 되나요?**  
  복사 작업은 대상 범위와 겹치는 기존 셀을 덮어씁니다. 데이터 손실을 방지하려면 대상 영역을 비워 두거나 다른 시작 셀(예: `"B2"`)을 사용하세요.

- **피벗 캐시가 복제되나요?**  
  Aspose.Cells는 원본 피벗 캐시를 재사용하므로 새 피벗 테이블은 동일한 소스 데이터에 연결됩니다. 독립적인 캐시가 필요하면 복사 후 피벗 테이블을 다시 만들어야 합니다.

## 팁 및 모범 사례

- **프로 팁**: 복사 블록 외부 데이터를 참조하는 수식이 포함된 경우 저장하기 전에 `Workbook.setForceFormulaRecalculation(true)`를 사용하세요.
- **주의** 큰 범위: 대용량 시트를 복사하면 메모리를 많이 차지할 수 있습니다. `OutOfMemoryError`가 발생하면 작은 청크로 나누어 복사하는 것을 고려하세요.
- **성능 팁**: 매우 큰 파일을 다룰 때 화면 업데이트를 비활성화(`workbook.getSettings().setCalculateFormulaOnOpen(false)`)하면 복사 속도를 높일 수 있습니다.

## 결론

이제 Aspose.Cells를 사용하여 시트 간에 **새 워크시트 만들기**와 **excel 범위 복사**를 수행하고 피벗 테이블 및 모든 셀 속성을 보존하는 방법을 알게 되었습니다. 이 기술을 통해 데이터를 프로그래밍 방식으로 복제하고, 보고서 템플릿을 만들거나, 수동 복사‑붙여넣기 없이 워크북을 재구성할 수 있습니다.

다음으로 **copy range aspose.cells**와 같은 교차 워크북 작업, 피벗 테이블 자동 새로 고침, 복사된 시트를 PDF로 내보내기 등 관련 주제를 살펴보세요. 다양한 원본 범위와 시트 이름을 실험하여 특정 자동화 시나리오에 맞게 적용해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 전체 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}