---
category: general
date: 2026-03-01
description: 피벗을 유지하면서 Java에서 피벗 테이블을 복사하고, Excel을 PPTX로 내보내며, Excel 자동 필터를 비활성화하고,
  JSON 배열에 스마트 마커를 사용하는 전체 단계별 가이드.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: ko
og_description: Java에서 피벗 테이블 복사, 피벗 정의 보존, PPTX로 내보내기, 자동 필터 비활성화, Smart Marker 사용
  – 개발자를 위한 완전 가이드.
og_title: Java에서 피벗 테이블 복사 – 보존하고 PPTX로 내보내기
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Java에서 피벗 테이블 복사 – 유지하고 PPTX로 내보내기
url: /ko/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 피벗 테이블 복사 – 유지하고 PPTX로 내보내기

하나의 워크북에서 다른 워크북으로 **copy pivot table**을 복사하면서 기본 피벗 정의를 잃어버린 적이 있나요? 당신만 그런 고민을 하는 것이 아닙니다. 실제 프로젝트에서는 데이터를 옮기는 경우가 많으며, 실행 시 오류를 일으키는 손상된 피벗을 원하지 않을 것입니다.  

이 튜토리얼에서는 **copy pivot table**을 수행할 뿐만 아니라 복사 시 **preserve pivot table**을 유지하는 방법, **export Excel to PPTX**, **disable Excel AutoFilter**, 그리고 **use smart marker**를 사용해 JSON 배열을 단일 셀에 삽입하는 방법까지 모두 다룹니다. 마지막에는 네 가지 시나리오를 모두 포함한 단일 실행 가능한 Java 프로그램을 얻게 됩니다.

## Prerequisites

- Java 8 이상 (코드는 Java 11에서도 동작합니다)  
- Aspose.Cells for Java 라이브러리 (버전 23.9 이상) – Maven Central에서 가져올 수 있습니다  
- 피벗 테이블, 테이블, 텍스트 상자와 같은 Excel 개념에 대한 기본적인 이해  

Aspose.Cells JAR가 없으시다면 `pom.xml`에 다음을 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

그럼 시작해 보겠습니다.

## 단계 1: 피벗 테이블 복사 – 피벗 정의 유지

피벗 테이블이 포함된 셀 범위를 단순히 복사하면 피벗 메타데이터가 남지 않는 경우가 많습니다. Aspose.Cells는 `copyRange`와 `CopyOptions` 인스턴스를 사용해 정의를 그대로 유지하는 깔끔한 방법을 제공합니다.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**왜 작동하나요:** `CopyOptions`는 Aspose.Cells에게 피벗 캐시와 필드 설정을 포함한 모든 정보를 함께 복사하도록 지시합니다. 이를 사용하지 않으면 값만 복사되고 피벗을 새로 고칠 수 없게 됩니다.

**예외 상황:** 소스 피벗이 하드코딩된 `A1:G20`보다 넓다면 범위를 조정하거나 `sourceSheet.getPivotTables().get(0).getDataRange()`를 사용해 동적으로 가져오세요.

![피벗 테이블 복사 예시](image.png "Java에서 피벗 테이블 복사")

*이미지 대체 텍스트: Java에서 피벗 테이블 복사 다이어그램*

## 단계 2: 편집 가능한 텍스트 상자가 포함된 워크시트를 PPTX로 내보내기

Excel 시트를 PowerPoint 슬라이드로 변환해야 할 때가 많습니다—예를 들어 주간 대시보드를 발표해야 할 경우 등. Aspose.Cells는 텍스트 상자와 같은 도형을 보존하면서 워크시트를 바로 PPTX 파일로 저장할 수 있습니다.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**무슨 일이 일어나나요:** `SaveFormat.PPTX`와 함께 `save` 메서드를 호출하면 전체 시트가 PowerPoint 슬라이드로 변환되며, 텍스트 상자 안의 내용도 편집 가능한 상태로 유지됩니다. PPTX를 PowerPoint에서 열면 상자 안 텍스트를 그대로 편집할 수 있습니다.

**팁:** 여러 시트가 있을 때 특정 시트만 저장하고 싶다면, 저장하기 전에 `wb.getWorksheets().removeAt(index)`를 사용해 나머지 시트를 제거하세요.

## 단계 3: 테이블에서 Excel AutoFilter 비활성화

AutoFilter는 최종 사용자가 편리하게 사용할 수 있지만, 데이터를 내보내기 전이나 깔끔한 보고서를 생성하기 위해 프로그램matically 끄고 싶을 때가 있습니다. 여기서는 Excel 테이블에서 **disable excel autofilter**를 수행하는 방법을 보여드립니다.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**왜 필요할까요:** CSV나 PDF와 같이 AutoFilter를 지원하지 않는 형식으로 내보낼 경우 필터 아이콘이 남아 있어 보기 좋지 않을 수 있습니다. 이를 비활성화하면 깨끗한 출력물을 얻을 수 있습니다.

**흔히 놓치는 점:** 시트에 테이블이 없으면 `getTables().get(0)`가 `IndexOutOfBoundsException`을 발생시킵니다. 실제 코드에서는 항상 `sheet.getTables().size()`를 먼저 확인하세요.

## 단계 4: Smart Marker 사용 – JSON 배열을 단일 셀 값으로 삽입

Smart Marker는 Aspose의 템플릿 엔진입니다. 전체 JSON 배열을 하나의 셀 값으로 처리하면 로깅이나 구조화된 데이터를 하위 시스템에 전달할 때 유용합니다. 이제 **use smart marker**를 활용해 이를 구현해 보겠습니다.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**작동 원리:** 워크북에 있는 `${json}` 마커는 `ArrayAsSingle` 옵션을 설정했기 때문에 전체 JSON 문자열로 교체됩니다. 이 옵션이 없으면 Aspose가 배열 요소를 각각 별도의 행으로 확장하려 시도합니다.

**변형:** 배열을 행별로 나누어 삽입하고 싶다면 `ArrayAsSingle`을 생략하고 Smart Marker가 자동으로 확장하도록 두면 됩니다.

## 전체 작업 예제 – 모든 단계 결합

아래는 지금까지 다룬 모든 작업을 하나의 Java 클래스로 연결한 예제입니다. 일반 `main` 메서드로 실행하면 되며, 파일 경로만 환경에 맞게 조정하면 됩니다.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}