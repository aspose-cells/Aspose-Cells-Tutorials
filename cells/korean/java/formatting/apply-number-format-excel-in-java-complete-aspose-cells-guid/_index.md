---
category: general
date: 2026-07-20
description: Java와 Aspose.Cells를 사용하여 엑셀에 숫자 서식을 적용합니다. 통화 스타일 엑셀 적용 방법, Java로 엑셀
  워크북 생성, 그리고 데이터테이블을 효율적으로 엑셀에 가져오는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: ko
lastmod: 2026-07-20
og_description: Java로 엑셀에 숫자 서식을 적용합니다. 이 가이드는 통화 스타일 엑셀 적용 방법, Java로 엑셀 워크북 생성, 그리고
  데이터 테이블을 엑셀로 단계별로 가져오는 방법을 보여줍니다.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Java에서 Excel 숫자 서식 적용 – 전체 Aspose.Cells 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Java에서 Excel 숫자 서식 적용 – 완전한 Aspose.Cells 가이드
url: /ko/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Excel 숫자 서식 적용 – Aspose.Cells 완전 가이드

Java 코드에서 **apply number format excel**을 직접 적용하는 방법이 궁금하셨나요? 재무 보고서를 만들거나 Excel을 직접 열지 않고도 금액 열을 빠르게 스타일링해야 할 때가 있죠. 좋은 소식은 Aspose.Cells를 사용하면 몇 줄의 코드만으로 가능하고, **apply currency style excel**, **create excel workbook java**, **import datatable to excel**을 한 번에 배울 수 있다는 점입니다.

이 튜토리얼에서는 실제 예제를 통해 Java `List<Map<String,Object>>`에 저장된 금액 목록을 새 워크북에 가져오고, 첫 번째 열에 내장된 통화 서식을 적용한 뒤 파일을 저장하는 과정을 단계별로 살펴봅니다. 얼마나 쉬운지 확인해 보세요. 시작합니다.

## Prerequisites – What You’ll Need

시작하기 전에 다음이 준비되어 있어야 합니다:

- **Java Development Kit (JDK) 8+** – 최신 JDK에서 코드를 실행할 수 있습니다.
- **Aspose.Cells for Java** 라이브러리 (Maven 아티팩트 `com.aspose:aspose-cells`) – Office 없이 Excel 파일을 조작할 수 있게 해 줍니다.
- 선호하는 **IDE** (IntelliJ IDEA, Eclipse, VS Code…) – 어떤 편집기든 가능하지만 IDE를 사용하면 디버깅이 편리합니다.
- **Java 컬렉션**에 대한 기본 지식 – `List`와 `Map`을 사용해 DataTable을 흉내낼 것입니다.

이것만 있으면 됩니다. 외부 서비스나 Excel 설치는 필요 없습니다. 순수 Java만으로 가능합니다.

## Step 1: Create Excel Workbook Java – Instantiating the Workbook

먼저 워크북 객체를 생성해야 합니다. 이는 모든 내용이 들어갈 빈 캔버스와 같습니다.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

왜 먼저 워크북을 만들까요? Aspose.Cells는 메모리 상에서 완전히 동작하므로 디스크에 접근하기 전에 시트, 스타일, 데이터를 추가할 수 있습니다. 이 방식은 빠르고 코드 테스트에도 유리합니다.

## Step 2: Prepare Data – Import Datatable to Excel Using a List of Maps

많은 엔터프라이즈 애플리케이션에서 데이터는 데이터베이스 테이블 형태로 들어옵니다. 여기서는 `List<Map<String,Object>>`로 이를 시뮬레이션합니다. 각 맵은 한 행을 나타내며, 키 `"Amount"`가 숫자 값을 매핑합니다.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

“왜 `ResultSet`이나 POJO를 사용하지 않나요?” 라고 궁금할 수 있습니다. `importDataTable` 메서드는 DataTable처럼 동작하는 컬렉션을 받아들이며, 추가 의존성을 도입하지 않고 개념을 보여주기에 리스트‑맵이 가장 간단합니다.

## Step 3: Define the Number Format – Apply Currency Style Excel

이제 튜토리얼의 핵심, **apply number format excel** 단계입니다. Aspose.Cells에는 내장된 숫자 서식이 있으며, 통화 서식은 인덱스 5에 해당합니다. 첫 번째 워크시트의 기본 스타일을 가져와 숫자 서식을 조정하고, 이후에 사용할 수 있도록 저장합니다.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

왜 기본 스타일을 기반으로 사용할까요? 워크북의 기본 폰트, 정렬 등 설정이 이미 포함되어 있어 숫자 서식만 바꾸면 됩니다. 만약 사용자 정의 서식(예: “€#,##0.00”)이 필요하면 `currencyStyle.setCustom("#,##0.00 €")`를 호출하면 됩니다.

## Step 4: Set Up Import Options – Linking the Style Array

Aspose.Cells에서는 열마다 대응되는 `Style` 객체 배열을 전달할 수 있습니다. 우리 데이터는 한 열만 있으므로 통화 스타일을 담은 단일 요소 배열을 제공합니다.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

여러 열을 각각 다른 스타일로 지정해야 한다면 배열을 확장하면 됩니다: `new Style[] { styleForCol1, styleForCol2, … }`. 스타일 순서는 소스 데이터의 열 순서와 일치합니다.

## Step 5: Import Data – Bringing the Datatable Into the Worksheet

워크북이 준비되고, 데이터와 스타일이 정의되었으니 이제 **import datatable to excel**을 수행합니다. 셀 `A1`부터 시작하고, 컬럼 헤더(`true`)를 포함한 뒤 `ImportTableOptions`를 전달합니다.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

`true` 플래그에 주목하세요—Aspose.Cells는 맵 키(`"Amount"`)를 기반으로 자동으로 헤더 행을 생성합니다. `false`로 설정하면 헤더가 생략되어 최종 레이아웃을 직접 제어할 수 있습니다.

## Step 6: Save the File – Create Excel Workbook Java on Disk

마지막 단계는 메모리 상의 워크북을 실제 파일로 저장하는 것입니다. Aspose가 지원하는 모든 포맷(`.xlsx`, `.xls`, `.csv`, …) 중 원하는 것을 선택할 수 있습니다. 여기서는 XLSX 파일로 저장합니다.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

프로그램을 실행한 뒤 생성된 파일을 열어보세요. `"Amount"` 열이 달러 기호와 소수점 두 자리, 천 단위 구분 기호가 적용된 것을 확인할 수 있습니다—바로 **apply number format excel**을 통화 값에 적용한 결과입니다.

## Expected Result

| 금액 |
|------|
| $1,234.56 |
| $7,890.12 |

헤더 “금액”은 기본 스타일(볼드)로 표시되고, 아래 셀들은 우리가 설정한 통화 서식으로 나타납니다. Excel에서 수동으로 서식을 지정할 필요가 없습니다.

## Pro Tips and Common Pitfalls

- **스타일 재사용을 현명하게** – 스타일 객체는 가볍지만, 셀마다 새 `Style`을 만들면 성능이 저하됩니다. 동일한 서식을 여러 셀에 적용할 때는 `currencyStyle`처럼 하나의 스타일 객체를 재사용하세요.
- **사용자 정의 서식** – 로케일에 따라 다른 통화 기호가 필요하면 `currencyStyle.setNumber(5)` 대신 `currencyStyle.setCustom("€#,##0.00")`를 사용하세요. Excel에서 실제 동작을 확인해 보는 것이 좋습니다.
- **대용량 데이터** – 수천 행을 처리할 때는 `ImportTableOptions.setImportDataOnly(true)` 플래그를 사용해 헤더 생성을 건너뛰고 가져오기 속도를 높일 수 있습니다.
- **스레드 안전성** – Aspose.Cells 객체는 **스레드 안전하지** 않습니다. 병렬로 보고서를 생성한다면 스레드당 별도의 `Workbook`을 생성하세요.

## Frequently Asked Questions

**Q: 기존 워크북에 숫자 서식을 적용할 수 있나요?**  
A: 가능합니다. `new Workbook("Existing.xlsx")`로 워크북을 연 뒤 대상 워크시트를 가져와 3‑5단계를 따라 스타일 배열을 새 데이터에 적용하면 됩니다.

**Q: 통화가 아니라 날짜를 서식 지정하려면 어떻게 하나요?**  
A: 다른 내장 숫자 인덱스를 사용합니다 (`14`는 짧은 날짜, `22`는 긴 날짜) 혹은 `yyyy‑mm‑dd`와 같은 사용자 정의 서식을 지정하면 됩니다. 워크플로우는 동일합니다.

**Q: 오래된 Excel 버전(.xls)에서도 동작하나요?**  
A: 네. `workbook.save("MyFile.xls")`처럼 파일 확장자를 바꾸기만 하면 Aspose가 자동으로 바이너리 포맷으로 저장합니다.

## Wrap‑Up – What We Achieved

우리는 **apply number format excel**을 사용해 통화 값 열에 서식을 적용하고, **apply currency style excel**을 구현했으며, 가장 간단한 방법으로 **create excel workbook java**를 수행하고, UI를 전혀 건드리지 않고 **import datatable to excel**을 완료했습니다. 이 모든 과정은 복사·붙여넣기만으로 바로 실행 가능한 간결한 프로그램으로 구현되었습니다.

다음 단계는 어떨까요?

- 더 많은 컬럼(예: “Date”, “Description”)을 추가하고 각 컬럼에 다른 스타일을 지정해 보세요.
- 동일 데이터를 CSV로 내보내고 숫자 서식이 어떻게 사라지는지 비교해 보세요.
- 코드를 Spring Boot 서비스에 통합해 워크북을 다운로드 가능한 HTTP 응답으로 반환하도록 해 보세요.

실험해 보시고 궁금한 점이 있으면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!


## What Should You Learn Next?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 프로젝트에 적용할 수 있는 다양한 구현 방법을 제공하는 관련 주제들입니다.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}