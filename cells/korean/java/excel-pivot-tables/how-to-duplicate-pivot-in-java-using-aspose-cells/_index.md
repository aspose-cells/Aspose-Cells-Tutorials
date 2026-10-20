---
category: general
date: 2026-09-18
description: Aspose.Cells를 사용한 Java에서 피벗 복제 방법 – 피벗 테이블을 워크북 간에 빠르고 안정적으로 복사합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: ko
lastmod: 2026-09-18
og_description: Aspose.Cells를 사용하여 Java에서 피벗 테이블을 복제하는 방법. 깔끔한 Java 코드로 워크북 간에 피벗
  테이블을 복사하는 전체 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Java에서 피벗 테이블 복제하기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java에서 Aspose.Cells를 사용하여 피벗을 복제하는 방법
url: /ko/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Aspose.Cells를 사용하여 피벗 복제하는 방법

Java 애플리케이션에서 **how to duplicate pivot**이 필요하다면, 이 가이드는 정확한 단계들을 보여줍니다. Excel 워크북을 로드하고, 피벗의 셀 영역을 정의한 다음 해당 범위를 새 워크북으로 복사하면 피벗 테이블을 정의나 데이터를 잃지 않고 이동할 수 있습니다.

피벗 테이블을 복사하는 것은 보고서를 생성하거나, 분석을 보관하거나, 큰 워크북을 모듈식 조각으로 분할할 때 흔히 요구되는 작업입니다. 이 튜토리얼에서는 **copy range between workbooks** 방법, **load Excel workbook Java** 방법, 그리고 **how to copy pivot**을 안전하게 수행하는 미묘한 차이를 배울 수 있습니다.

Aspose.Cells for Java를 사용하여 `Source.xlsx`에서 `PivotCopied.xlsx`로 피벗 테이블을 복제하는 실행 가능한 Java 프로그램을 완성하게 됩니다.

## 사전 요구 사항

* JDK 8 또는 그 이상이 설치되어 있어야 합니다.
* Maven(또는 다른 빌드 도구)으로 의존성을 관리합니다.
* Aspose.Cells for Java 버전 23.10 이상. 다음 Maven 의존성을 `pom.xml`에 추가하십시오:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* 피벗 테이블이 **A1:H30** 범위에 포함된 소스 워크북(`Source.xlsx`)이 필요합니다.

## Java에서 피벗 복제하는 방법

핵심 아이디어는 간단합니다:

1. **Load the source workbook** – 피벗이 포함된 워크시트에 접근할 수 있게 됩니다.
2. **Define the cell area** – 피벗을 둘러싼 셀 영역을 정의합니다.
3. **Create a destination workbook** – 복사된 범위를 받을 빈 파일을 생성합니다.
4. **Copy the range** – Aspose.Cells가 피벗 정의를 자동으로 복제합니다.
5. **Save the destination workbook** – 이제 동일한 피벗을 가진 별도의 파일이 생성됩니다.

다음은 위 단계들을 수행하는 완전하고 실행 가능한 Java 프로그램입니다.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### 이 방법이 작동하는 이유

* **Aspose.Cells**는 피벗 테이블을 워크시트 셀 컬렉션의 일부로 취급합니다. `copyRange`를 호출하면 라이브러리는 셀 값뿐만 아니라 기본 피벗 캐시와 정의까지 복사하므로 새 워크북에 완전한 기능을 가진 복제본이 포함됩니다.
* `CopyOptions` 객체는 기본적으로 수식, 서식 및 포함된 객체를 보존하도록 설정됩니다. 추가 제어가 필요하면 (예: `setCopyColumnWidths(true)`)와 같이 사용자 지정할 수 있습니다.

## 워크북 간 범위 복사 – 심층 분석

위 예제는 단일 연속 블록을 복사하지만, `copyRange`는 모든 직사각형 영역을 처리할 수 있습니다. 피벗이 비인접 범위에 걸쳐 있는 경우 `copyRange`를 여러 번 호출하거나 `Worksheet.copy`를 사용해 전체 시트를 복제할 수 있습니다.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** 대용량 워크북을 복사할 때 `CopyOptions.setPreserveCellStyle(true)`를 활성화하면 불필요한 스타일 복제를 방지하여 성능을 향상시킬 수 있습니다.

## 피벗을 워크북에 복사하는 방법 – 다중 피벗 처리

소스 시트에 피벗이 하나 이상 포함되어 있다면, 워크시트의 피벗 테이블을 순회하면서 각각을 개별적으로 복사할 수 있습니다:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

이 방법을 사용하면 모든 피벗이 원래 이름과 데이터 소스를 유지합니다.

## Excel 워크북 로드 Java – 일반적인 함정

* **File path separators:** 코드가 플랫폼에 독립적이도록 슬래시(`/`) 또는 `File.separator`를 사용하십시오.
* **Missing license:** Aspose.Cells는 평가 모드로 동작하지만 출력에 워터마크가 표시됩니다. 워크북을 로드하기 전에 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`와 같이 라이선스를 등록하여 워터마크를 제거하십시오.
* **Large files:** 100 MB보다 큰 워크북의 경우 메모리 사용량을 줄이기 위해 스트리밍 옵션과 함께 `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` 사용을 고려하십시오.

## 전체 엔드‑투‑엔드 예제 요약

모든 내용을 종합하면, IDE에 복사‑붙여넣기 할 수 있는 최종 프로그램은 다음과 같습니다:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Expected output:** 실행 후 지정된 디렉터리에 `PivotCopied.xlsx`가 생성됩니다. Excel에서 열면 `Source.xlsx`와 동일한 피벗 테이블 레이아웃, 필터 및 데이터가 표시됩니다. 모든 계산된 필드와 서식이 보존됩니다.

## 자주 묻는 질문

* **이것이 오래된 Excel 형식(.xls)에서도 작동합니까?**  
  예. Aspose.Cells가 자동으로 형식을 감지합니다. `new Workbook("file.xls")`를 사용하면 동일한 복사 로직이 적용됩니다.

* **피벗이 외부 데이터 소스를 참조하는 경우는 어떻게 해야 하나요?**  
  복사본은 원본 데이터 소스 참조를 유지합니다. 대상 환경에서 해당 소스에 접근할 수 없으면 피벗이 `#REF!` 오류를 표시합니다. 이를 방지하려면 복사 후 피벗을 새로 고치거나 `PivotTable.setDataSource(...)`를 통해 데이터 소스를 변경하십시오.

* **피벗을 특정 시트 이름으로 복사할 수 있나요?**  
  물론 가능합니다. 대상 워크시트를 만든 후 이름을 변경하면 됩니다:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## 결론

이제 Aspose.Cells를 사용하여 Java에서 **how to duplicate pivot** 테이블을 복제하는 방법, **copy range between workbooks** 방법, 그리고 **load Excel workbook Java**에 대한 모범 사례를 알게 되었습니다. 로드, 정의, 대상 생성, 복사, 저장의 5단계 프로세스를 따르면 피벗 기능을 잃지 않고 보고서 생성 자동화, 분석 보관, 복잡한 워크북 분할 등을 수행할 수 있습니다.

다음으로 **copy pivot to workbook**와 같이 여러 시트를 포함한 관련 주제를 탐색하거나, Aspose가 아닌 경우 Apache POI를 사용해 복제된 피벗을 더 큰 데이터 처리 파이프라인에 통합해 보세요. 대용량 워크북에 대한 성능을 미세 조정하려면 다양한 `CopyOptions` 설정을 실험해 보십시오.

코딩을 즐기세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용하여 Excel에서 피벗 테이블 만들기: 종합 가이드](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 피벗 테이블 소스 업데이트: 종합 가이드](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북에서 피벗 필드 그룹화 - 종합 가이드](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}