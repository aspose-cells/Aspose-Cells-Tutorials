---
category: general
date: 2026-08-14
description: Java와 Aspose.Cells를 사용하여 워크북 간 범위를 복사합니다. 피벗 테이블 워크북 복사, 그림을 PowerPoint로
  내보내기, Excel 테이블에서 자동 필터 제거 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: ko
lastmod: 2026-08-14
og_description: Java에서 워크북 간 범위를 복사합니다. 이 가이드는 피벗 테이블 워크북 복사, 그림을 PowerPoint로 내보내기
  및 Excel 테이블에서 자동 필터 제거 방법을 보여줍니다.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Java에서 워크북 간 범위 복사 – 완전한 Aspose.Cells 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Java에서 워크북 간 범위 복사 – 단계별 가이드
url: /ko/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 워크북 간 범위 복사 – 단계별 가이드

Java에서 **워크북 간 범위 복사**가 필요하다면, Aspose.Cells는 피벗 테이블 및 그림과 같은 복잡한 객체를 처리하는 깔끔한 API를 제공합니다. 이 튜토리얼에서는 **피벗 테이블 워크북 복사**, **그림을 PowerPoint로 내보내기**, 그리고 **Excel 테이블에서 AutoFilter 제거**를 코드가 읽기 쉽고 유지 관리하기 쉬운 상태로 수행하는 방법을 보여줍니다.

다음 내용을 배울 수 있습니다:

* 소스 워크북을 로드하고 소스 범위를 정의합니다.  
* 대상 워크북을 생성하고 범위를 복사하여 피벗 테이블이 그대로 유지되도록 합니다.  
* 시트의 첫 번째 그림을 편집 가능한 PowerPoint 객체로 내보냅니다.  
* 첫 번째 Excel 테이블에서 AutoFilter를 제거합니다.  
* `SmartMarkerOptions`를 사용하여 워크북을 로드하고 JSON 배열을 단일 셀 값으로 처리합니다.

예제는 Java용 Aspose.Cells 23.10을 사용하지만, 개념은 이전 버전에도 적용됩니다.

---

## 사전 요구 사항

| 요구 사항 | 중요한 이유 |
|-------------|----------------|
| Java 17 이상 | 최신 Aspose.Cells 런타임에서 필요합니다. |
| Aspose.Cells for Java (Maven 아티팩트 `com.aspose:aspose-cells`) | `Workbook`, `Worksheet`, `Range` 및 코드에서 사용되는 관련 클래스를 제공합니다. |
| 피벗 테이블, 그림 및 AutoFilter가 적용된 테이블을 포함하는 소스 Excel 파일 (`src.xlsx`). | 이 튜토리얼은 이러한 객체들을 조작하여 각 기능을 시연합니다. |

`pom.xml`에 Maven 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 워크북 간 범위 복사 – 소스 및 대상 로드

첫 번째 단계는 소스 워크북을 열고 복사하려는 데이터가 포함된 범위를 선택한 다음 빈 대상 워크북을 만드는 것입니다.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **왜 중요한가:** `Range.copy`를 사용하면 Aspose.Cells는 원시 셀 값뿐만 아니라 기본 피벗 캐시도 복사하여 대상 워크북에서 피벗 테이블이 정상적으로 작동하도록 유지합니다.

---

## 범위를 복사하면서 피벗 테이블 워크북 복사

이제 정의된 범위를 소스 워크북에서 대상 워크북으로 복사합니다. 범위에 피벗 캐시가 포함되어 있기 때문에 피벗 테이블이 자동으로 보존됩니다.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **결과:** `destination.xlsx`를 열면 `src.xlsx`와 동일한 피벗 테이블 레이아웃이 표시됩니다. 피벗 캐시를 재구성하기 위한 추가 코드는 필요하지 않습니다.

---

## 그림을 PowerPoint로 내보내기

Aspose.Cells는 그림을 편집 가능한 PowerPoint 객체로 내보내도록 표시할 수 있습니다. 다음 코드는 대상 시트의 첫 번째 그림을 선택하고 내보내기 플래그를 설정합니다.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **보이는 내용:** PowerPoint에서 `destination.pptx`를 열면 그림이 편집, 크기 조정 또는 애니메이션을 할 수 있는 기본 도형으로 표시됩니다.

---

## Excel 테이블에서 AutoFilter 제거

소스 시트에 AutoFilter가 적용된 테이블이 포함되어 있다면, 복사 후 이를 제거하고 싶을 수 있습니다. 아래 코드는 첫 번째 테이블에 접근하여 필터를 제거합니다.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **효과:** 테이블은 워크북에 그대로 남지만, 드롭다운 필터 화살표가 사라져 깔끔한 데이터 뷰를 제공합니다.

---

## SmartMarker 옵션으로 워크북 로드 – JSON 배열을 단일 셀로 처리

JSON으로 보고서를 생성할 때, Aspose.Cells는 전체 배열을 단일 셀 값으로 처리할 수 있습니다. 이는 JSON 문자열을 템플릿에 삽입하면서 여러 셀로 확장되지 않도록 할 때 유용합니다.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **이 기능을 사용할 이유:** JSON 페이로드에 단일 셀에 JSON 문자열로 표시되어야 하는 배열이 포함된 경우, `setArrayAsSingle(true)`를 사용하면 Aspose.Cells가 배열을 별도의 행이나 열로 확장하는 것을 방지합니다.

![Java에서 워크북 간 범위 복사 – Aspose.Cells 코드 예제](copy-range-workbooks.png)

*이미지 대체 텍스트:* **Java에서 워크북 간 범위 복사 – Aspose.Cells 코드 예제** (주요 키워드와 일치).

---

## 예상 출력

| 파일 이름                | 포함 내용 |
|--------------------------|----------|
| `destination.xlsx`       | 피벗 테이블이 정상 작동하는 복사된 범위. |
| `destination.pptx`       | 편집 가능한 PowerPoint 도형으로 내보낸 그림. |
| `final_output.xlsx`      | AutoFilter 화살표가 없는 테이블. |
| `template_filled.xlsx`   | JSON 배열이 단일 셀 값으로 저장됨. |

각 파일을 해당 애플리케이션(Excel 또는 PowerPoint)에서 열어 작업이 성공했는지 확인합니다.

---

## 결론

이제 Aspose.Cells를 사용하여 Java에서 **워크북 간 범위 복사** 방법을 알게 되었으며, 피벗 테이블을 보존하고, 그림을 PowerPoint로 내보내며, Excel 테이블에서 AutoFilter를 제거하는 방법을 배웠습니다. 동일한 패턴을 사용하면 모든 Excel 범위를 새 워크북으로 복사하거나, SmartMarker JSON 배열을 처리하거나, 추가 변환을 연쇄할 수 있습니다.

다음 단계로 살펴볼 수 있습니다:

* **여러 워크시트가 있는 새 워크북으로 Excel 범위 복사**.  
* 배치 이미지 추출을 위해 **그림을 PowerPoint로 내보내기**를 사용합니다.  
* 대규모 보고 파이프라인에서 **Excel 테이블에서 AutoFilter 제거**를 적용합니다.  
* 전체 Excel‑to‑PowerPoint 자동화를 위해 Aspose.Slides와 이 기술들을 결합합니다.

다양한 범위 주소, 여러 피벗 테이블 또는 사용자 정의 그림 형식으로 자유롭게 실험해 보세요. Aspose.Cells API는 프로그래밍 유연성을 위해 설계되었으므로, 여기서 보여준 패턴을 어떤 기업 Excel 자동화 시나리오에도 맞게 적용할 수 있습니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스에는 단계별 설명이 포함된 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용한 Excel 시트 간 이미지 복사: 종합 가이드](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Aspose.Cells Java를 사용한 Excel 워크시트 간 페이지 설정 복사](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [워크북 간 Excel 워크시트 복사](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}