---
category: general
date: 2026-10-07
description: Java와 Aspose.Cells를 사용하여 Excel에서 피벗 테이블을 복제하는 방법을 배워보세요. 피벗 테이블을 워크북
  간에 범위를 복사하여 빠르게 복사합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: ko
lastmod: 2026-10-07
og_description: Java와 Aspose.Cells를 사용하여 Excel에서 피벗 테이블을 복제하는 방법. 이 가이드를 따라 워크북 간에
  범위를 복사하여 피벗 테이블을 복사하세요.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Java를 사용해 Excel에서 피벗 테이블 복제하는 방법 – 전체 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Java를 사용하여 Excel에서 피벗 테이블 복제하는 방법 – 단계별 가이드
url: /ko/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 Java로 피벗 테이블 복제하기 – 단계별 가이드

Excel 워크북에서 **피벗 테이블 복제 방법**이 필요하다면, 이 튜토리얼은 완전하고 바로 실행할 수 있는 솔루션을 보여줍니다. Aspose.Cells for Java를 사용하면 기본 범위를 복사하여 피벗 테이블과 해당 소스 데이터를 함께 복사하고, 결과를 새 워크북으로 저장할 수 있습니다.

피벗 테이블을 복제하는 것은 피벗 캐시가 시트 내부에 숨겨져 있기 때문에 종종 까다롭게 느껴집니다. 피벗이 포함된 전체 범위를 복사하면 Aspose.Cells가 대상 워크북에 캐시를 자동으로 재생성하므로 수동으로 XML을 조작할 필요 없이 완전하게 작동하는 복제본을 얻을 수 있습니다.

이 가이드에서는 다음을 수행합니다:

* 피벗 테이블이 포함된 소스 워크북을 로드합니다.  
* 피벗이 위치한 정확한 범위를 정의합니다.  
* 그 범위를 새 워크북에 복사하여 피벗 정의를 보존합니다.  
* 새 파일을 저장하고 피벗이 정상 작동하는지 확인합니다.  

이 단계는 Aspose.Cells가 지원하는 모든 Excel 버전(2007‑2024)에서 작동하며 Java 코드 몇 줄만 필요합니다.

## 사전 요구 사항

| Requirement | Why it matters |
|-------------|----------------|
| **Java 8 또는 최신 버전** | Aspose.Cells는 Java 8+용으로 제작되었습니다. |
| **Aspose.Cells for Java** (최신 버전) | 예제에서 사용되는 `Workbook`, `Range`, `CopyRange` API를 제공합니다. |
| **Source workbook** 피벗 테이블이 포함된 워크북 (예: `Source.xlsx`) | 복제하려는 피벗 테이블입니다. |
| **Write permission** 대상 디렉터리에 대한 쓰기 권한 | `CopyWithPivot.xlsx`를 저장하는 데 필요합니다. |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## 피벗 테이블 복제 방법 – 전체 구현

아래는 피벗이 포함된 범위를 복사하여 **피벗 테이블 복제 방법**을 보여주는 독립 실행형 Java 프로그램입니다. 코드에는 오류 처리, 주석 및 검증 단계가 포함되어 있습니다.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### 각 단계 설명

| 단계 | 코드가 수행하는 작업 | 왜 **copy pivot table**에 중요한가 |
|------|-------------------|----------------------------------------|
| **1️⃣ 소스 워크북 로드** | `new Workbook(srcPath)`는 `Source.xlsx`를 읽습니다. | 원본 피벗이 존재하는 유일한 파일입니다. |
| **2️⃣ 범위 정의** | `createRange("A1:G20")`는 피벗과 해당 데이터를 포함하는 `Range` 객체를 생성합니다. | 피벗 테이블은 캐시와 함께 저장되므로 전체 범위를 복사하면 캐시도 함께 이동합니다. |
| **3️⃣ 범위 복사** | `copyRange(srcRange, "A1")`는 범위를 대상 시트에 씁니다. | 이는 **copy range between workbooks**의 핵심이며, API가 숨겨진 객체를 자동으로 처리합니다. |
| **4️⃣ 피벗 새로 고침** | `pivotTable.refresh()`는 피벗을 강제로 재계산합니다. | 복제된 피벗이 원본과 동일한 값을 표시하도록 보장하며, 특히 수정 후에 중요합니다. |
| **5️⃣ 워크북 저장** | `destWb.save(destPath)`는 파일을 디스크에 저장합니다. | Excel에서 열 수 있는 최종 **copy excel range** 결과를 생성합니다. |

#### 예상 출력

프로그램을 실행한 후 `CopyWithPivot.xlsx`를 엽니다. 원본 시트와 동일하게 보이는 워크시트가 나타나며, 피벗 테이블은 원본과 정확히 동일하게 작동합니다 – 행을 확장하고, 필드를 필터링하고, 데이터를 새로 고쳐도 오류가 발생하지 않습니다.

## 일반적인 변형 및 엣지 케이스

### 1️⃣ 여러 시트에 걸친 피벗 복사

피벗의 소스 데이터가 피벗 자체와 다른 시트에 있는 경우, 복사 작업에 두 시트 모두 포함해야 합니다. 가장 간단한 방법은 먼저 전체 소스 시트를 복사한 다음 피벗 시트를 복사하는 것입니다:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ 명명된 범위 처리

Aspose.Cells는 범위를 복사할 때 명명된 범위를 보존합니다. 그러나 대상 워크북에 동일한 식별자를 가진 이름이 이미 존재하면 `CellsException`이 발생합니다. 복사하기 전에 충돌하는 이름을 변경하여 해결합니다:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ 대용량 워크북 및 성능

수백만 행에 달하는 매우 큰 범위를 복사하면 메모리를 많이 사용합니다. **memory optimization**을 활성화하십시오:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ 수식 유지

소스 범위에 복사 영역 외부 셀을 참조하는 수식이 포함된 경우, 복사 후 해당 참조가 끊어집니다. 이를 방지하려면 모든 종속 셀을 포함하도록 범위를 확장하거나 `CopyOptions` 플래그 `CopyOptions.COPY_FORMULA`와 함께 `copyRange`를 사용하십시오.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## 신뢰할 수 있는 **copy range between workbooks**를 위한 전문가 팁

* **소스 시트 이름이 변경될 수 있는 경우 절대 주소** (`$A$1:$G$20`)를 항상 사용하십시오.  
* **복사 후 새로 고침** – Aspose.Cells가 캐시를 재구성하더라도 `refresh()`를 호출하면 Excel에서 가끔 발생하는 오래된 캐시 경고를 없앨 수 있습니다.  
* **피벗 검증**: 저장 후 파일을 프로그래밍 방식으로 열고 `pivotTable.validate()`를 호출하여 끊어진 참조가 없는지 확인하십시오.  
* **버전 호환성**: 코드는 Excel 2007‑2024 파일(`.xlsx`, `.xlsm`)에서 작동합니다. 레거시 `.xls` 파일의 경우 `LoadOptions.setLoadFormat(LoadFormat.XLS)`를 설정하십시오.

## 전체 소스 목록 (컴파일 준비 완료)



## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Java에서 피벗 테이블 복사 방법 – 완전한 Aspose.Cells 가이드](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Aspose.Cells for Java를 사용하여 Excel에서 피벗 테이블 만들기: 종합 가이드](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java로 Excel 피벗 테이블 소스 업데이트하기: 종합 가이드](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}