---
category: general
date: 2026-11-25
description: Aspose.Cells 스마트 마커를 사용하여 JSON 배열을 단일 값으로 바인딩하는 Excel 워크북 Java 코드 예제
  만들기.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: ko
lastmod: 2026-11-25
og_description: Aspose.Cells를 사용하여 Java에서 Excel 워크북을 생성하고 JSON 배열을 단일 셀로 쉽게 내보내세요.
  단계별 가이드를 따라보세요.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Java에서 Excel 워크북 만들기 – Aspose.Cells 스마트 마커 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells 마커를 사용하여 Java에서 Excel 워크북 만드는 방법
url: /ko/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java와 Aspose.Cells 마커를 사용하여 Excel 워크북 만들기

JSON 배열을 단일 셀에 기록하는 **Java용 Excel 워크북** 코드를 만들어야 한다면, 이 튜토리얼이 정확히 어떻게 하는지 보여줍니다. Aspose.Cells 스마트 마커를 사용하면 전체 배열을 하나의 값으로 취급할 수 있어 수동 루프와 셀별 쓰기를 피할 수 있습니다.

워크북 설정, 스마트 마커 정의, JSON‑스타일 배열을 포함하는 `Map` 데이터 소스 바인딩, 최종 파일 저장 방법을 배웁니다. 이 예제는 Java 17+, Maven, 그리고 무료 Aspose.Cells for Java 체험 라이브러리와 함께 작동합니다.

---

![Java와 Aspose.Cells 스마트 마커를 사용하여 만든 Excel 워크북 스크린샷](excel-workbook-java.png){: .center-image alt="Java와 Aspose.Cells 스마트 마커를 사용하여 만든 Excel 워크북 스크린샷"}

## 사전 요구 사항

| 요구 사항 | 중요한 이유 |
|-------------|----------------|
| Java 17 이상 | 최신 언어 기능 및 보안 업데이트 |
| Maven 3.6+ | 의존성 관리를 간소화 |
| Aspose.Cells for Java (v23.12 이상) | `Workbook`, `Worksheet`, 및 샘플에 사용된 스마트 마커 API를 제공합니다 |
| Java 컬렉션에 대한 기본 지식 | `Map<String, Object>`를 데이터 소스로 생성하게 됩니다 |

Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Java Excel 워크북 생성 – 전체 예제

다음 프로그램은 **완전하고 실행 가능한** 솔루션입니다. `ExcelSmartMarkerDemo.java`라는 파일에 복사하고, 컴파일한 뒤 실행하세요.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### 코드 설명

1. **새 워크북을 생성** – `new Workbook()`은 기본 시트가 포함된 메모리 내 Excel 파일을 제공합니다.  
2. **셀 A1에 스마트 마커 배치** – `{{jsonArray:ArrayAsSingle}}`는 Aspose.Cells에 마커를 *전체* 배열로 교체하도록 지시하며, 콤마로 연결합니다.  
3. **`Map` 데이터 소스 구축** – 키 `"jsonArray"`는 마커 이름과 일치하고, 값은 `String[]`입니다.  
4. **`setSmartMarkerData` 호출** – 이 메서드는 맵을 마커에 바인딩하고 교체를 수행합니다.  
5. **파일 저장** – `workbook.save(...)`는 `JsonSingleValue.xlsx`를 디스크에 기록합니다.

생성된 Excel 파일을 열면 셀 **A1**에 다음과 같이 들어 있습니다:

```
One, Two, Three
```

`ArrayAsSingle` 옵션 때문에 배열이 단일 콤마 구분 문자열로 렌더링됩니다.

---

## JSON 데이터를 바인딩하기 위한 Aspose.Cells 스마트 마커 사용

Aspose.Cells 스마트 마커는 복잡한 객체(예: JSON과 유사한 구조)를 워크시트에 직접 매핑하는 강력한 방법입니다. 구문 `{{fieldName:Option}}`은 템플릿 엔진과 매우 유사하게 동작합니다:

* **fieldName** – 데이터 소스(`Map`, POJO, 또는 `DataTable`)의 키입니다.  
* **Option** – 컬렉션 처리 방식을 제어합니다. `ArrayAsSingle`은 전체 컬렉션을 하나의 값으로 취급하고, `Array`와 같은 다른 옵션은 배열을 행별로 확장합니다.

**루프 대신 스마트 마커를 사용하는 이유는?**  
루프는 셀 주소를 수동으로 계산하고, 오류가 발생하기 쉬운 인덱싱을 수행하며, 스타일링을 위한 추가 코드를 필요로 합니다. 스마트 마커를 사용하면 선언형 플레이스홀더를 작성하고, Java 코드를 간결하게 유지하며, 레이아웃 세부 사항을 라이브러리가 처리합니다.

---

## Java Map 데이터 소스 설정

`Map<String, Object>`는 Aspose.Cells에서 가장 간단한 데이터 컨테이너입니다:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*키(`jsonArray`)는 마커 이름과 정확히 일치해야 합니다.*  
`List<String>`, 사용자 정의 POJO, 혹은 더 복잡한 JSON 구조를 위한 중첩 `Map`도 사용할 수 있습니다. Aspose.Cells는 객체 그래프를 자동으로 탐색합니다.

**팁:** 연결된 문자열을 다른 형식(예: 세미콜론 사용)으로 표시해야 한다면, 배열을 `Map`에 할당하기 전에 Java에서 미리 처리하세요:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## 워크북 저장 및 출력 확인

```java
workbook.save("JsonSingleValue.xlsx");
```

`save` 메서드는 다양한 형식(`.xlsx`, `.xls`, `.csv`, `.pdf`)을 지원합니다. 이 튜토리얼에서는 기본 Excel Open XML 형식을 사용합니다.

**검증 단계**

1. Microsoft Excel, LibreOffice Calc, 또는 Google Sheets에서 `JsonSingleValue.xlsx`를 엽니다.  
2. 셀 **A1**에 `One, Two, Three`가 표시되는지 확인합니다.  
3. 추가 행이나 열이 생성되지 않았는지 확인합니다 – 스마트 마커가 제자리 교체를 수행했습니다.

셀에 원시 마커 텍스트(`{{jsonArray:ArrayAsSingle}}`)가 표시된다면, 다음을 다시 확인하세요:

* 마커 이름이 맵 키와 정확히 일치하는지(대소문자 구분).  
* `setSmartMarkerData`가 마커를 배치한 **후에** 호출되는지.  
* 사용 중인 Aspose.Cells 버전이 `ArrayAsSingle` 옵션을 지원하는지(v20.3 이후 지원).

---

## 일반적인 변형 및 엣지 케이스

| 시나리오 | 조정 |
|----------|------------|
| **다른 구분자** | Java에서 사용자 정의 조인을 사용하여 `ArrayAsSingle`과 함께 사용합니다(위 팁 참고). |
| **한 시트에 여러 배열** | 다른 셀에 `{{anotherArray:ArrayAsSingle}}`와 같은 추가 마커를 배치하고, 맵에 해당 항목을 추가합니다. |
| **중첩 JSON 객체** | 중첩 `Map<String, Object>`를 제공하고, 점 표기법(`{{parent.child}}`)으로 필드를 참조합니다. |
| **대용량 데이터 세트** | 수천 개 행의 경우 `Array` 옵션을 사용하여 Aspose.Cells가 행을 자동으로 확장하도록 합니다, which |

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells Java를 사용하여 Excel을 HTML로 생성 및 내보내는 방법 | 워크북 작업 가이드](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북을 이미지로 내보내기: 단계별 가이드](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북을 SVG로 생성 및 저장하는 방법](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}