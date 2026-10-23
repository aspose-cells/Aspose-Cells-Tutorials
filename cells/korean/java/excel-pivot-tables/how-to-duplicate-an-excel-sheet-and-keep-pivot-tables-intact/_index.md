---
category: general
date: 2026-10-23
description: Java에서 피벗 테이블을 유지하면서 Excel 시트를 복제하는 방법을 배워보세요. 이 가이드는 피벗 테이블 복사, Excel
  범위 복사, 그리고 피벗 데이터가 포함된 시트 복사 방법도 보여줍니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: ko
lastmod: 2026-10-23
og_description: 피벗 테이블을 보존하면서 Java에서 Excel 시트를 복제합니다. 피벗 테이블 복사, Excel 범위 복사, 피벗 데이터가
  포함된 시트 복사에 대한 전체 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Java에서 피벗 테이블이 포함된 Excel 시트를 복제하는 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Java에서 Excel 시트를 복제하고 피벗 테이블을 그대로 유지하는 방법
url: /ko/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Excel 시트를 복제하고 피벗 테이블을 유지하는 방법

모든 피벗 테이블을 유지하면서 **Excel 시트를 복제**해야 한다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. 시트를 복사하고, 특정 범위를 복사하며, 피벗 테이블을 다른 워크북으로 복사하는 간결한 솔루션을 순수 Java와 Aspose.Cells를 사용해 확인할 수 있습니다.

Excel 시트를 복제하는 작업은 템플릿에서 월간 보고서를 생성하거나 테스트용 샌드박스 복사본이 필요할 때 흔히 수행됩니다. 아래 코드는 `setCopyPivotTable(true)` 옵션을 도입한 Aspose.Cells 25.11 이상에서 동작합니다.

## 준비 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Java 17(또는 최신 JDK) 설치
- 프로젝트에 Aspose.Cells for Java 25.11 이상 추가 (`com.aspose:aspose-cells:25.11` Maven 좌표)
- 피벗 테이블이 포함된 소스 워크북(`SourceWithPivot.xlsx`)
- 원하는 IDE 또는 빌드 도구(IntelliJ IDEA, Eclipse, Maven, Gradle 등)

## Step 1: 피벗 테이블이 포함된 소스 워크북 로드

먼저 복제하려는 피벗이 들어 있는 워크북을 엽니다.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **이 단계가 중요한 이유:** 소스 워크북을 로드하면 워크시트 객체, 셀 및 내장된 피벗 테이블에 접근할 수 있습니다. 이를 통해 복사하려는 피벗 데이터를 참조할 수 있습니다.

## Step 2: 빈 대상 워크북 생성(또는 기존 워크북 로드)

새 워크북을 시작하거나 복제된 시트를 받을 기존 파일을 열 수 있습니다.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **팁:** 이미 보고서 워크북이 있다면 위 코드를 `new Workbook("ExistingReport.xlsx")` 로 교체하여 해당 워크북에 복제된 시트를 추가하세요.

## Step 3: 전체 워크시트 복사 – 피벗 테이블 자동 보존

전체 워크시트를 복사하는 것이 **피벗이 포함된 시트 복사**의 가장 간단한 방법입니다. Aspose.Cells는 피벗 정의와 캐시를 자동으로 복사합니다.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **작동 원리:** `addCopy`는 시트 구조, 셀 값, 스타일 및 내장된 피벗 테이블을 모두 복제합니다. `dstWb`의 새 워크시트는 원본과 동일하게 보이며 피벗 캐시도 포함됩니다.

## Step 4: (선택) 피벗 테이블이 포함된 특정 범위만 복사

전체 시트를 복사하고 싶지 않을 때가 있습니다—예를 들어 피벗이 포함된 일부 영역만 필요할 경우입니다. 이때 **Excel 범위 복사**와 함께 피벗 복사를 명시적으로 요청합니다.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **도움이 되는 이유:** `setCopyPivotTable(true)` 플래그는 제한된 범위를 복사할 때도 피벗 정의를 복제하도록 엔진에 지시합니다. 이 플래그가 없으면 원시 데이터만 복사되고 피벗은 사라집니다.

## Step 5: 대상 워크북 저장

복제된 내용을 새 파일에 기록합니다.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### 예상 결과

프로그램을 실행하면 대상 디렉터리에 `DuplicatedWithPivot.xlsx` 파일이 생성됩니다. Excel에서 파일을 열면 다음을 확인할 수 있습니다:

- `Sheet1 (Copy)`(또는 “Copy”가 붙은 원본 이름)이라는 새 워크시트
- 피벗 테이블이 원본 시트와 동일하게 표시되며 정상 작동
- 선택적으로 범위 복사를 사용한 경우 A1:G30 셀만 존재하지만 피벗 캐시가 복사돼 피벗은 여전히 작동

## 자주 묻는 질문 및 예외 상황

### 전체 시트를 복사하지 않고 피벗만 다른 워크북에 복사하려면?

피벗과 해당 데이터가 포함된 범위를 복사하고 `setCopyPivotTable(true)`를 사용합니다. **Step 4**의 코드를 그대로 사용하되, 범위가 데이터 소스와 피벗을 모두 포함하도록 지정하면 됩니다.

### 소스 워크북에 피벗이 있는 여러 워크시트가 있으면 어떻게 하나요?

복제하고자 하는 각 워크시트에 대해 **Step 3**을 반복합니다:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### 보호된 워크시트에서도 작동하나요?

Aspose.Cells는 보호된 시트를 복사할 수 있지만, 복사 후 피벗을 수정하려면 먼저 보호를 해제해야 합니다:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### 동일한 이름의 시트가 이미 존재하는 워크북에 피벗 테이블을 복사할 수 있나요?

가능합니다. 고유한 이름을 지정하여 `addCopy`를 사용하세요:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## 전문가 팁: 피벗 캐시 확인

복사 후 피벗 캐시가 존재하는지 프로그래밍 방식으로 확인할 수 있습니다:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

캐시 ID가 음수가 아닌 숫자로 출력되면 피벗이 성공적으로 복제된 것입니다.

## 결론

이제 Java에서 **Excel 시트를 복제**하면서 모든 피벗 테이블을 보존하는 방법, 피벗 테이블을 직접 **복사**하는 방법, 피벗이 포함된 **Excel 범위 복사** 방법, 그리고 Aspose.Cells 25.11+을 사용해 **피벗이 포함된 시트 복사** 또는 **피벗을 워크북에 복사**하는 방법을 알게 되었습니다. 이 패턴을 활용해 보고서 자동 생성, 템플릿 복제, 동일한 피벗 기반 분석이 필요한 테스트 환경 등을 손쉽게 구축하세요.

더 탐구하고 싶나요? 복제된 워크북을 PDF로 내보내거나, 복사 후 피벗 캐시를 프로그래밍 방식으로 새로 고쳐 최신 데이터를 반영하도록 해보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 완전한 코드 예제가 포함되어 있어 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}