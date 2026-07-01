---
category: general
date: 2026-06-30
description: Java를 사용하여 Excel에서 고유 값을 정렬합니다. 수식을 설정하고, 수식을 다시 계산하며, Aspose.Cells를
  사용하여 고유 목록 Excel을 생성하는 방법을 배웁니다.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: ko
og_description: Java로 Excel 고유값 정렬하기. 이 가이드는 수식을 설정하고, 수식을 다시 계산하며, 몇 분 안에 Excel에서
  고유 목록을 생성하는 방법을 보여줍니다.
og_title: Excel에서 고유 값 정렬 – 배열 수식을 위한 Java 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Excel에서 고유값 정렬 – 배열 수식 설정을 위한 완전한 Java 가이드
url: /ko/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sort Unique Values Excel – Complete Java Guide to Set Array Formulas

Excel에서 **고유 값을 정렬**하려고 공식들을 끌어다 놓지 않고도 할 수 있는 방법이 궁금하셨나요? 여러분만 그런 것이 아닙니다. 많은 보고서 시나리오에서 중복되지 않은 항목들의 알파벳 순 정렬 리스트가 필요하지만, 수작업으로 만들기는 번거롭습니다.  

좋은 소식은? 몇 줄의 Java 코드만으로 워크시트에 **배열 수식**을 설정하고, **수식 재계산**을 수행하면 스필된 범위가 자동으로 채워집니다. 이 튜토리얼에서는 워크북 생성부터 Excel 스타일의 고유 리스트 생성까지 모든 과정을 단계별로 살펴보며, 솔루션을 애플리케이션에 바로 삽입할 수 있도록 안내합니다.

## What This Tutorial Covers

- Aspose.Cells(코드 스니펫을 구동하는 라이브러리)를 사용한 Java 프로젝트 설정.  
- `SORT`와 `UNIQUE` 함수를 함께 사용해 **Excel에서 고유 리스트 생성** 결과를 얻는 방법.  
- 프로그래밍 방식으로 **배열 수식**을 셀에 적용하기.  
- **수식 재계산**을 트리거하여 즉시 결과가 나타나게 하기.  
- 출력 확인 및 빈 셀이나 비연속 범위와 같은 엣지 케이스에 대한 해결 방법.

이 가이드를 끝까지 읽으면, 깨끗한 Excel 시트를 내보내야 하는 모든 Java 서비스에 바로 사용할 수 있는 메서드를 손쉽게 추가할 수 있습니다.

> **Pro tip:** 이미 Maven을 사용 중이라면 Aspose.Cells를 의존성에 추가하면 JAR 파일을 직접 관리할 필요가 없습니다.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells는 Java 8 이상을 목표로 합니다. |
| Maven (or Gradle) | 의존성 관리를 간소화합니다. |
| Aspose.Cells for Java | `Workbook`, `Worksheet`, 그리고 수식 API를 제공합니다. |
| Basic familiarity with Excel functions | `SORT`와 `UNIQUE`를 이해하면 코드를 쉽게 적용할 수 있습니다. |

> *If you don’t have Aspose.Cells yet, add this to your `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Step 1: Create a New Workbook (How to Set Formula Begins Here)

먼저 빈 워크북을 만들어야 합니다. 이는 나중에 셀 `A1`에 **배열 수식**을 **설정**할 빈 캔버스와 같습니다.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Why create a new workbook?*  
> 깨끗한 환경을 보장하여 테스트 데이터에 영향을 줄 수 있는 숨겨진 수식이 없도록 합니다.

---

## Step 2: Populate Sample Data (Optional but Helpful)

결과를 명확히 확인하려면 **B** 열에 중복된 항목들을 채워 보겠습니다.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Why use column B?*  
> 우리가 작성할 수식이 `B1:B10`을 참조하므로, 데이터를 해당 열에 두면 전형적인 Excel 예제와 동일하게 동작합니다.

---

## Step 3: Set an Array Formula That **Sort Unique Values Excel**

이제 마법이 시작됩니다. `UNIQUE`(중복 제거)와 `SORT`(알파벳 순 정렬)를 결합합니다. 결과 식은 **배열 수식**이며, 인접 셀에 자동으로 스필됩니다.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### How It Works

- `UNIQUE(B1:B10)`은 범위를 스캔해 중복되지 않은 문자열을 세로 배열로 반환합니다.  
- `SORT(...)`는 그 배열을 오름차순으로 정렬합니다.  
- 전체 식을 `=` 로 감싸고 `setFormulaArray`를 호출하면 Aspose.Cells가 결과를 **스필된 배열**로 처리합니다. Excel과 동일한 동작이죠.

> **Note:** `SORT`나 `UNIQUE`가 지원되지 않는 구버전 Excel을 사용한다면, **LET** 함수와 함께 `SORT(UNIQUE(...))`를 사용하거나 레거시 배열 수식(`=INDEX(...)`)을 활용할 수 있습니다. 이 튜토리얼은 가장 깔끔한 현대적 동적 배열 접근법에 초점을 맞추고 있습니다.

---

## Step 4: Recalculate Formulas So the Spilled Range Is Populated

수식을 입력했지만 워크북이 자동으로 평가되지 않습니다. 여기서 **수식 재계산** 단계가 필요합니다.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

`calculateFormula()`를 호출하면 Aspose.Cells가 Excel 엔진을 실행해 셀 `A1`, `A2`, …에 정렬된 고유 값들을 채워 넣습니다.

> *Why not rely on lazy evaluation?*  
> 서버‑사이드 환경에서는 계산 직후 CSV, PDF 등으로 내보내야 할 경우가 많기 때문에 명시적인 호출이 일관성을 보장합니다.

---

## Step 5: Verify the Result (Optional Debugging)

새로 스필된 값을 콘솔에 출력해 보는 것이 좋습니다—특히 새로운 API를 학습 중이라면 더욱 그렇습니다.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

프로그램을 실행하면 다음과 같이 출력됩니다:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

`SortedUniqueValues.xlsx` 파일을 열면 `A1`부터 아래로 동일한 데이터가 스필된 것을 확인할 수 있습니다.

---

## Handling Edge Cases

### Empty Cells in the Source Range

`B1:B10`에 빈 셀이 포함되어 있으면 `UNIQUE`는 이를 별개의 항목으로 취급합니다. 빈 셀을 무시하려면 `FILTER`로 범위를 감싸세요:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Non‑Contiguous Data

데이터가 여러 열에 걸쳐 있을 경우 `CHOOSE` 또는 `TEXTJOIN`으로 결합한 뒤 `UNIQUE`를 적용할 수 있습니다. 예시:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

이와 같은 조정은 **배열 수식 설정**을 보다 복잡한 시나리오에 적용할 수 있음을 보여줍니다.

---

## Full Working Example (All Steps Combined)

아래는 전체 실행 가능한 Java 프로그램입니다. IDE에 복사‑붙여넣기하고 Aspose.Cells 의존성을 추가한 뒤 *Run*을 눌러 보세요.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Expected output** (shown in console) matches the sorted, deduplicated list we discussed earlier. Opening the generated Excel file reveals the same values spilling from `A1` downwards.

---

## Frequently Asked Questions

**Q: Does this work with older Excel versions (pre‑Office 365)?**  
A: `SORT`와 `UNIQUE` 함수는 Excel 365에서 도입된 동적 배열 엔진의 일부입니다. 레거시 파일에서는 `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`와 같은 고전 배열 수식을 사용해야 합니다. Aspose.Cells는 여전히 이를 평가할 수 있지만 구문이 더 복잡합니다.

**Q: Can I set the array formula on a range other than `A1`?**  
A: 물론 가능합니다. `cells.get("A1")` 부분을 원하는 주소로 바꾸면 됩니다. 스필된 배열은 지정한 셀을 시작점으로 오른쪽·아래쪽으로 자동 확장됩니다.

**Q: What if my source data is larger than `B1:B10`?**  
A: 정적 범위를 `B:B`와 같은 동적 범위나 이름 정의된 범위로 교체하면 됩니다. 예: `=SORT(UNIQUE(B:B))`. 다만 전체 열을 참조하면 매우 큰 시트에서는 성능에 영향을 줄 수 있으니 주의하세요.

---

## Conclusion

우리는 Java에서 **배열 수식 설정**을 통해 **Excel에서 고유 값 정렬**을 수행하고, **수식 재계산**을 호출해 결과를 즉시 얻는 방법을 살펴보았습니다. 핵심 흐름은 워크북 생성 → 데이터 입력 → 배열 수식 적용 → 계산 트리거 → 결과 검증입니다.  

이제 여기서 확장해 보세요—조건부 서식 추가, PDF 내보내기, 혹은 웹 서비스에 통합해 즉시 보고서를 제공하는 등. 핵심 아이디어는 변함없습니다: Excel 자체 함수를 활용해 무거운 작업을 맡기고, Java가 전체 흐름을 제어하도록 하는 것이죠.

Excel 자동화를 한 단계 끌어올릴 준비가 되셨나요? `SORT` 대신 `SORTBY`를 사용해 보조 열로 정렬하거나, `FILTER`를 활용해 비즈니스 규칙에 맞지 않는 행을 제외해 보세요. 가능성은 사실상 무한합니다.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}