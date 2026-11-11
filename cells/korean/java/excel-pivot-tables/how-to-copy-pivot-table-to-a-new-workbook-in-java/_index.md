---
category: general
date: 2026-10-26
description: Java를 사용하여 피벗 테이블을 새 워크북으로 복사하는 방법을 배우고, Aspose.Cells를 통해 서식이 포함된 Excel
  범위를 복사하면서 서식과 피벗 정의를 보존하세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: ko
lastmod: 2026-10-26
og_description: Java와 Aspose.Cells를 사용하여 피벗 테이블을 새 워크북으로 복사합니다. 이 가이드는 Excel 범위를 복사하고
  서식을 유지하며 빈 워크북을 효율적으로 만드는 방법을 보여줍니다.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Java에서 피벗 테이블을 새 워크북으로 복사하기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java에서 피벗 테이블을 새 워크북으로 복사하는 방법
url: /ko/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 피벗 테이블을 새 워크북으로 복사하는 방법

한 Excel 파일에서 다른 파일로 **copy pivot table**을 복사해야 한다면, 이 가이드는 완전하고 실행 가능한 솔루션을 보여줍니다. 피벗 정의를 보존하고 모든 서식을 유지하며 Excel 범위를 복사할 때 흔히 발생하는 함정을 피하는 방법을 확인할 수 있습니다.

피벗 테이블을 복사하면 *how to copy pivot*처럼 데이터 소스를 깨뜨리거나 스타일을 잃는 문제가 자주 발생합니다. 이 튜토리얼을 마치면 빈 워크북을 생성하고, 원하는 범위를 복사한 뒤 피벗이 그대로 유지된 상태로 결과를 저장하는 자체 포함 Java 프로그램을 갖게 됩니다.

## 달성 목표

* 피벗 테이블이 포함된 소스 워크북을 로드합니다.  
* 복사된 데이터를 받을 **create empty workbook**을 생성합니다.  
* 피벗을 포함하는 **copy excel range**를 복사 옵션을 사용해 피벗과 서식을 유지합니다.  
* 대상 파일을 저장하고 피벗이 원본과 정확히 동일하게 작동하는지 확인합니다.

### 사전 요구 사항

* Java 17 이상.  
* Aspose.Cells for Java (버전 23.10 이상).  
* Java IDE(IntelliJ IDEA, Eclipse 등)에 대한 기본적인 이해.  

> **Pro tip:** 빠른 테스트를 위해 무료 Aspose.Cells 평가 라이선스를 사용하고, 실제 운영 환경에서는 정식 라이선스로 교체하세요.

## 새 워크북에 피벗 테이블 복사

첫 번째 단계는 소스와 대상 워크북을 설정하는 것입니다. 대상은 **create empty workbook** 호출로 시작되며, 이는 단일 워크시트가 포함된 깨끗한 파일을 제공합니다.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### 왜 이렇게 동작하는가

* `new Workbook()` **creates empty workbook**을 기본 시트와 함께 생성하여 기존 데이터를 삭제할 필요가 없습니다.  
* `CopyOptions`는 Aspose.Cells에 **pivot table** 메타데이터를 복사하도록 지시하며, 단순 값만 복사하지 않습니다. `PASTE_ALL` 모드는 셀 스타일, 숫자 형식 및 조건부 서식까지 전달하여 **copy range with formatting** 요구 사항을 충족합니다.  
* `copyRange`는 소스의 내부 구조를 존중하는 **copy excel range** 작업을 수행하므로 복사 후에도 피벗이 정상적으로 작동합니다.

## 서식을 잃지 않고 피벗 복사하는 방법

기본 `CopyOptions`만 사용할 경우 오래된 Aspose.Cells 버전에서는 일부 스타일 정보가 누락될 수 있습니다. 붙여넣기 유형을 명시적으로 설정하면 **copy range with formatting**이 보장됩니다.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

`setPasteSpecialType`을 추가하면 열 너비, 행 높이 및 데이터 유효성 검사 규칙까지 범위와 함께 전달됩니다. 이는 피벗 테이블이 사용자 지정 너비의 여러 열에 걸쳐 있을 때 특히 유용합니다.

## 복사하기 전에 빈 워크북 만들기

때때로 개발자는 이미 데이터가 들어 있는 기존 워크북에 복사하려고 시도합니다. 이는 범위 겹침이나 예상치 못한 덮어쓰기를 초래할 수 있습니다. **create empty workbook** 호출로 시작하면 작업이 격리됩니다:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

대상에 여러 시트가 필요하면 복사 후에 시트를 추가할 수 있습니다:

```java
destWb.getWorksheets().add("Summary");
```

## CopyOptions를 사용하여 서식과 함께 Excel 범위 복사

피벗 테이블을 넘어, 동일한 패턴은 서식 보존이 필요한 모든 **copy excel range**(차트, 테이블, 조건부 서식 등)에도 적용됩니다.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

`CopyOptions` 인스턴스는 동일하게 유지되므로 다양한 범위에서 일관된 동작을 얻을 수 있습니다.

### 고려해야 할 엣지 케이스

| 상황                                      | 권장 처리 방법 |
|------------------------------------------|----------------|
| 소스 워크북에 피벗이 여러 개 존재        | 각 피벗의 범위를 별도로 복사하거나 전체 시트를 복사합니다. |
| 대상에 이미 데이터가 포함되어 있음       | `copyRange` 호출 시 충돌하지 않는 시작 셀(예: "H1")을 선택합니다. |
| 피벗 데이터 소스가 외부(DB 등)인 경우    | 대상 워크북이 동일한 외부 데이터 소스를 가리키도록 하거나 복사 후 피벗을 새로 고칩니다. |
| 워크북 크기가 10 MB 이상인 경우          | `-Xmx2g`와 같이 Java 힙 크기를 늘려 `OutOfMemoryError`를 방지합니다. |

## 결과 확인

프로그램을 실행한 뒤 `destination.xlsx`를 열면 다음을 확인할 수 있습니다:

* `source.xlsx`와 동일한 피벗 테이블 레이아웃.  
* 모든 셀 색상, 숫자 형식 및 열 너비가 보존됨.  
* 피벗의 데이터 소스가 새 파일 내부의 원본 데이터 범위를 가리키고 있어, 피벗을 새로 고치면 값이 올바르게 업데이트됨.

피벗이 정적 테이블처럼 보이면 `CopyOptions.setPasteType(PasteType.PASTE_ALL)`이 설정되어 있는지 다시 확인하세요. 이 옵션이 없으면 Aspose.Cells가 피벗을 일반 데이터로 처리합니다.

## 결론

이제 Java에서 **copy pivot table**을 새 워크북으로 복사하면서 서식, 데이터 연결 및 시트 레이아웃을 보존하는 방법을 알게 되었습니다. 전체 솔루션은 소스 파일 로드, **create empty workbook** 생성, **copy excel range** 옵션 구성, 결과 저장 과정을 보여줍니다.  

앞으로는 **how to copy pivot**을 다른 워크시트 간에 복사하거나, 피벗과 함께 차트를 삽입하거나, 여러 워크북을 배치 처리하는 자동화 등을 탐색할 수 있습니다. `CopyOptions` 설정을 실험하여 특정 자동화 요구에 맞추면 강력한 Excel 조작 툴킷을 손쉽게 활용할 수 있습니다.

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}