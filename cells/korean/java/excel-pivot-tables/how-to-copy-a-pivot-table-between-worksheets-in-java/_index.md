---
category: general
date: 2026-10-16
description: Aspose.Cells를 사용한 Java에서 피벗 테이블 복사 방법 – 범위를 다른 시트로 복사하고 워크시트 간에 효율적으로
  복사하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: ko
lastmod: 2026-10-16
og_description: Aspose.Cells를 사용하여 Java에서 피벗 테이블을 복사하는 방법. 이 튜토리얼에서는 범위를 다른 시트로 복사하고
  워크시트 간에 범위를 복사하는 방법을 전체 코드와 함께 보여줍니다.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Java에서 워크시트 간 피벗 테이블 복사 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Java에서 워크시트 간 피벗 테이블 복사 방법
url: /ko/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 워크시트 간 피벗 테이블 복사 방법

같은 워크북 내에서 한 시트에서 다른 시트로 **피벗 테이블 복사 방법**이 필요하다면, 이 가이드는 완전하고 바로 실행할 수 있는 솔루션을 제공합니다. 피벗 테이블이 포함된 원본 범위를 복사하고, 기능을 유지하며, 결과를 검증하는 방법을 Aspose.Cells for Java를 사용해 보여드립니다.

피벗 테이블을 복사하는 것은 프로그램matically 보고서를 생성할 때 흔히 수행되는 작업이며, 이를 올바르게 수행하면 피벗 캐시 손실이나 수식 깨짐을 방지할 수 있습니다. 이 튜토리얼을 마치면 **범위를 다른 시트로 복사** 및 **워크시트 간 범위 복사**를 수동 단계 없이 수행할 수 있게 됩니다.

## 배울 내용

* 피벗 테이블이 포함된 기존 Excel 파일을 로드합니다.
* 피벗 테이블이 포함된 원본 범위를 정의합니다.
* 다른 워크시트에 대상 범위를 정의합니다.
* `CopyOptions`를 사용하여 피벗 테이블을 그대로 유지합니다.
* 복사된 피벗 테이블이 예상대로 작동하는지 확인합니다.

**전제 조건**

* Java 17 이상.
* Aspose.Cells for Java (버전 23.12 이상).  
* 첫 번째 시트에 피벗 테이블이 포함된 Excel 파일(`input.xlsx`).

---

## Aspose.Cells를 사용한 피벗 테이블 복사 방법

이 작업의 핵심은 네 단계 프로세스입니다: 워크북 로드, 원본 범위 찾기, 대상 범위 설정, 복사 수행. 아래에서 각 단계가 자세히 설명됩니다.

### 단계 1: 워크북 로드

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*왜 이 단계인가?*  
워크북을 로드하면 전체 파일이 메모리로 로드되어 워크시트, 셀 및 피벗 캐시에 접근할 수 있습니다. Aspose.Cells는 파일 형식을 자동으로 읽으므로 `.xls`와 `.xlsx`를 신경 쓸 필요가 없습니다.

### 단계 2: 피벗 테이블이 포함된 원본 범위 찾기

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*왜 이 단계인가?*  
피벗 테이블은 숨겨진 캐시를 참조하는 셀 블록에 저장됩니다. 정확한 범위(`A1:G20` 예시)를 선택하면 복사 시 캐시가 연결된 상태를 유지합니다.

### 단계 3: 다른 시트에 대상 범위 정의

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*왜 이 단계인가?*  
다른 워크시트에 대상을 선택하면 **범위를 다른 시트로 복사**할 수 있습니다. 왼쪽 위 셀(`A1`)은 일반적인 시작점이지만 주소를 변경하여 원하는 위치에 배치할 수 있습니다.

### 단계 4: 피벗 테이블을 유지하면서 원본 범위 복사

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*왜 이 단계인가?*  
`CopyOptions`는 전송되는 내용을 제어합니다. `PasteType.PASTE_ALL`을 사용하면 피벗 테이블, 서식 및 기본 수식이 모두 복제됩니다. 이러한 옵션이 없으면 원시 값만 복사되어 피벗 기능이 깨질 수 있습니다.

### 단계 5: 워크북 저장 및 결과 검증

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Excel에서 `output.xlsx`를 열고 다음을 확인합니다:

* 두 번째 시트에 원본과 동일한 완전한 기능의 피벗 테이블이 포함되어 있습니다.
* 피벗 테이블을 새로 고치면 데이터가 업데이트되어 캐시가 그대로임을 증명합니다.

## Java를 사용한 범위 다른 시트로 복사

목표가 피벗 테이블 없이 단순히 **범위를 다른 시트로 복사**하는 것이라면, 동일한 코드를 일반 셀 범위에 적용할 수 있습니다. 변경되는 유일한 부분은 원본 주소이며, `CopyOptions` 설정은 동일하게 유지되어 수식과 서식이 보존됩니다.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

이 스니펫은 피벗 및 비피벗 시나리오 모두에 대한 API의 유연성을 보여줍니다.

## 워크시트 간 범위 복사 시 수식 손실 방지

워크시트 간 **범위 복사**를 할 때, 다른 시트를 참조하는 수식은 상대 참조가 변경되면 깨질 수 있습니다. 이를 방지하려면:

1. `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`를 사용하여 수식만 필요할 경우 적용합니다.
2. 대상 시트를 동일 워크북에 두어 내부 참조가 유효하게 유지되도록 합니다.
3. 복사 후 `workbook.calculateFormula();`를 호출하여 강제로 재계산합니다.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

이러한 추가 단계는 복사된 범위가 원본과 정확히 동일하게 동작하도록 보장하며, 여러 워크시트에 걸쳐 있더라도 적용됩니다.

## 전문가 팁 및 일반적인 함정

| Situation | Tip |
|-----------|-----|
| **피벗 캐시 업데이트 안 됨** | 복사 후 `destSheet.getPivotTables().get(0).refresh();`를 호출하여 캐시를 새로 고칩니다. |
| **다른 워크북으로 복사** | `Workbook destWorkbook = new Workbook();`를 사용하고 `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`를 실행합니다. 필요하면 피벗 캐시를 별도로 복사해야 함을 기억하세요. |
| **대용량 피벗 테이블** | 복사 중 `OutOfMemoryError`를 방지하려면 Java 힙 크기(`-Xmx2g`)를 늘립니다. |
| **스타일 보존** | `copyOptions.setPasteType(PasteType.PASTE_ALL)`를 설정합니다; 그렇지 않으면 값만 복사됩니다. |

## 예상 출력

전체 프로그램을 실행하면 `output.xlsx`가 생성됩니다. Excel에서 열면:

* **Sheet2!A1:G20**에 **Sheet1!A1:G20**와 동일한 피벗 테이블이 표시됩니다.
* 피벗 필드 목록, 행/열 레이블 및 데이터 값이 원본과 일치합니다.
* 피벗을 새로 고치면 숫자가 업데이트되어 캐시가 정상 작동함을 확인합니다.

콘솔에 다음이 출력됩니다:

```
Pivot table copied successfully.
```

## 결론

이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 한 워크시트에서 다른 워크시트로 **피벗 테이블 복사 방법**을 배웠습니다. 워크북을 로드하고, 올바른 원본 범위를 선택하고, 대상을 정의하며, `CopyOptions`를 구성함으로써 모든 피벗 기능을 유지하면서 **범위를 다른 시트로 복사** 및 **워크시트 간 범위 복사**를 신뢰성 있게 수행할 수 있습니다.

다음으로 탐색해 볼 수 있는 내용:

* 복사된 피벗 테이블을 PDF 또는 HTML로 내보내기.
* 여러 워크북에 걸쳐 피벗 테이블 새로 고침 자동화.
* `CopyOptions`를 사용하여 특정 요소만 복사(예: 값, 서식).

다양한 범위 주소, 워크북 구조, 혹은 워크북 간 복사를 자유롭게 실험해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Java에서 범위 복사 방법 – Aspose.Cells로 피벗 테이블 복사](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Java에서 피벗 테이블 복사 – 완전한 Aspose.Cells 가이드](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Excel 피벗 테이블 복사 – Java 사용 단계별 가이드](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}