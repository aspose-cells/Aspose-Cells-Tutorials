---
category: general
date: 2026-09-08
description: Aspose.Cells를 사용한 Java에서 범위 복사 방법 – 피벗 테이블 복사, 피벗 테이블 복제, 서식을 유지하면서 피벗
  테이블 내보내기를 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: ko
lastmod: 2026-09-08
og_description: Aspose.Cells를 사용한 Java에서 범위 복사 방법. 이 튜토리얼에서는 피벗 테이블을 복사하고, 피벗 테이블을
  복제하며, 서식을 유지하면서 피벗 테이블을 내보내는 방법을 보여줍니다.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Java에서 범위 복사 방법 – 완전한 Aspose.Cells 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells를 사용하여 Java에서 범위 복사하는 방법
url: /ko/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Aspose.Cells를 사용하여 범위 복사하는 방법

Java에서 **범위 복사 방법**이 필요하다면, Aspose.Cells가 작업을 간단하게 해줍니다. 일반 셀 블록을 이동하든 전체 기능을 갖춘 피벗 테이블을 이동하든, 라이브러리는 복사 작업을 수행하면서 수식, 스타일 및 피벗 캐시를 그대로 유지합니다. 이 가이드에서는 **피벗 테이블 복사**, **피벗 테이블 복제**, 그리고 전체 서식이 포함된 새 워크북으로 **피벗 테이블 내보내기** 방법을 배웁니다.

이 튜토리얼은 프로젝트 설정부터 최종 검증 단계까지 모든 과정을 다루므로, 읽은 직후 코드를 바로 실행할 수 있습니다. Aspose.Cells for Java JAR 외에 별도의 외부 도구는 필요하지 않습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- IDE에 설치 및 구성된 Java 17(또는 지원되는 JDK).
- 의존성 관리를 위한 Maven 또는 Gradle(예제는 Maven 사용).
- 범위 `A1:H20`에 피벗 테이블이 포함된 소스 Excel 파일(`source.xlsx`).
- Java 프로그래밍에 대한 기본적인 이해.

## Step 1: Add Aspose.Cells to your project

Aspose.Cells는 상용 라이브러리이지만, 무료 평가 버전을 사용할 수 있습니다. `pom.xml`에 다음 의존성을 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Gradle을 선호한다면, 동등한 항목은 다음과 같습니다:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

JAR를 추가하면 이 가이드 전반에 걸쳐 사용되는 `Workbook`, `Worksheet`, `Range`, `CopyOptions` 클래스를 사용할 수 있게 됩니다.

## Step 2: Load the source workbook and select the first worksheet

**범위 복사 방법**의 첫 번째 단계는 이동하려는 데이터를 포함한 워크북을 여는 것입니다.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Why this matters:** 워크북을 열면 원본 파일을 디스크에서 직접 건드리지 않고도 API가 조작할 수 있는 메모리 내 표현이 생성됩니다.

## Step 3: Define the range that contains the pivot table

피벗 테이블은 직사각형 블록 안에 존재합니다. Aspose.Cells가 복사할 대상을 알 수 있도록 해당 블록을 지정해야 합니다.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Note:** `createRange` 메서드는 아직 아무 것도 복사하지 **않으며**, 복제하려는 셀을 가리키는 `Range` 객체만 생성합니다.

## Step 4: Create a new workbook and get its first worksheet

이제 복사된 범위가 위치할 대상 워크북을 생성합니다.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Why a new workbook?** 새 파일을 사용하면 숨겨진 스타일이나 이름 정의 범위가 복사 작업에 방해되지 않으며, 특히 **피벗 테이블 내보내기**를 별도 파일로 할 때 중요합니다.

## Step 5: Copy the range (including the pivot table) to the destination sheet

이것이 **서식 포함 범위 복사 방법**의 핵심입니다. `CopyOptions` 객체는 Aspose.Cells에게 값, 수식, 스타일 및 피벗 캐시를 모두 보존하도록 지시합니다.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** 소스 범위에 피벗 테이블이 포함되어 있기 때문에 API가 피벗 캐시를 자동으로 복제하여 새 워크시트에 원본과 동일하게 동작하는 완전한 피벗 테이블이 생성됩니다.

## Step 6: Save the destination workbook

마지막으로 결과를 디스크에 기록합니다.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

`dest.xlsx`를 열면 원본 피벗 테이블과 동일한 복제본이 서식, 슬라이서 및 계산된 필드까지 모두 포함된 것을 확인할 수 있습니다.

## Expected output

- `dest.xlsx`에 **Sheet1**이라는 워크시트가 포함됩니다.
- `A1:H20` 셀에 원본과 동일한 데이터와 피벗 테이블이 들어 있습니다.
- 모든 셀 스타일(글꼴, 색상, 테두리)이 보존됩니다.
- 피벗 테이블은 완전히 인터랙티브하며, 새로 고침 시 복사된 범위의 기본 데이터를 반영합니다.

## How to copy range with formatting – deeper dive

이전 예제는 가장 단순한 시나리오를 보여주지만, 약간 다른 접근이 필요한 변형 상황도 있을 수 있습니다.

### Copy pivot table to an existing workbook

이미 데이터가 있는 워크북 안에서 **피벗 테이블 복제**가 필요하다면, 동일한 `copyRange` 호출을 사용하되 다른 대상 주소를 지정하면 됩니다:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Export pivot table only (without surrounding data)

때때로 소스 데이터를 제외하고 피벗 테이블만 원할 때가 있습니다. `getPivotTable` 메서드를 통해 피벗 테이블의 표시 범위를 식별하세요:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Preserve conditional formatting

조건부 서식 규칙은 스타일 컬렉션의 일부입니다. `PasteType.ALL` 플래그가 이미 이를 복사하지만, 명시적으로 지정할 수도 있습니다:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Edge cases and troubleshooting

| 상황 | 주의할 점 | 권장 해결책 |
|-----------|-------------------|-----------------|
| 소스와 대상 워크북이 서로 다른 Excel 버전을 사용하는 경우 | 일부 최신 피벗 기능(예: 데이터 모델)이 올바르게 표시되지 않을 수 있음 | 최신 Aspose.Cells 버전을 사용하고 두 워크북 모두 `Workbook.setFileFormatType(FileFormatType.XLSX)`를 설정하십시오 |
| 매우 큰 피벗 테이블(> 10 000 행)으로 메모리 압박이 발생 | 복사 중 메모리 부족 오류 | 로드하기 전에 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`를 활성화하십시오 |
| 대상 시트에 소스와 동일한 이름의 이름 정의 범위가 이미 존재 | 이름 충돌로 `CopyOptions` 실패 | `copyOptions.setIgnoreNameConflicts(true)` 호출 |

## Full, runnable example

아래는 Java 클래스에 복사‑붙여넣기 할 수 있는 전체 프로그램입니다. 모든 import, 오류 처리 및 주석이 포함되어 있습니다.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

프로그램을 실행한 뒤 `dest.xlsx`를 열어 피벗 테이블이 원본과 정확히 동일하게 작동하는지 확인하세요.

## Conclusion

이제 Aspose.Cells를 사용하여 Java에서 **범위 복사 방법**을 알고 있으며, **피벗 테이블 복사**, **피벗 테이블 복제**, 그리고 **피벗 테이블 내보내기**를 전체 서식을 유지하면서 수행할 수 있습니다. 이 라이브러리는 Excel XML 구조의 저수준 세부 사항을 추상화하여 비즈니스 로직에 집중할 수 있게 해줍니다.

### Next steps

- **copy range with formatting**을 차트와 이미지에 적용해 보세요(`PasteType.PICTURES` 사용).
- 배치 처리를 자동화: 여러 소스 파일을 순회하며 피벗 테이블을 요약 워크북에 통합합니다.
- 이 기술을 Aspose.Slides와 결합하여 복사된 피벗을 포함한 PowerPoint 보고서를 생성합니다.

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하며, 밀접하게 연관된 주제를 다룹니다. 각 리소스에는 단계별 설명과 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용하여 Excel 피벗 테이블 소스 업데이트 방법: 종합 가이드](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells를 이용한 Java 피벗 테이블 로딩 최적화 – 종합 가이드](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [C#에서 피벗 테이블 복사 방법 – Excel을 PPTX로 변환, 범위 복사 및 텍스트 상자 만들기](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}