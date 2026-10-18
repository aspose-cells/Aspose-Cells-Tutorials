---
category: general
date: 2026-08-11
description: Java에서 Aspose를 사용해 새 워크북을 만든 후, Excel에 사용자 정의 속성을 추가하고, 전체 단계별 예제로 워크북을
  XLSB 형식으로 저장합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: ko
lastmod: 2026-08-11
og_description: Java에서 Aspose를 사용해 새 워크북을 만들고, 사용자 정의 속성을 Excel에 추가한 뒤, 완전한 실행 예제와
  함께 워크북을 XLSB 형식으로 저장합니다.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: 새 워크북 만들기 Aspose – Excel에 사용자 정의 속성 추가
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Aspose로 새 워크북 만들기 – Excel에 사용자 정의 속성을 추가하고 XLSB로 저장
url: /ko/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 새 워크북 Aspose 만들기 – Excel 사용자 정의 속성 추가 및 XLSB로 저장

Java 애플리케이션에서 **create new workbook Aspose**가 필요하다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. **add custom property Excel**를 추가하고 값을 가져오며, 메타데이터를 잃지 않고 **save workbook as XLSB**하는 방법을 배울 수 있습니다.

이 튜토리얼은 프로젝트 설정부터 저장된 파일 검증까지 모든 과정을 다룹니다. 외부 문서는 필요 없으며, 단계별로 따라가며 코드를 실행하면 됩니다.

## 사전 요구 사항

- Java Development Kit (JDK) 8 이상이 설치되어 있어야 합니다.
- Maven 또는 Gradle을 사용해 종속성을 관리합니다 (예제는 Maven 사용).
- 활성화된 Aspose.Cells for Java 라이선스가 필요합니다 (테스트용으로 무료 평가 모드 사용 가능).

## 단계 1: 프로젝트에 Aspose.Cells 추가

`pom.xml`에 Aspose.Cells Maven 아티팩트를 추가합니다. 이 종속성은 **create new workbook Aspose** 객체에 필요한 클래스를 제공합니다.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Gradle을 선호한다면 Maven 스니펫을 동등한 `implementation "com.aspose:aspose-cells:23.12"` 라인으로 교체하세요.

## 단계 2: 새 워크북 Aspose 만들기

첫 번째 기능 단계는 `Workbook` 객체를 인스턴스화하는 것입니다. 이 객체는 메모리상의 Excel 파일을 나타내며 이후 모든 작업의 진입점이 됩니다.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

새 워크북 Aspose를 만들면 기본 워크시트가 포함된 빈 워크북이 생성되어 사용자 지정 준비가 됩니다.

## 단계 3: Excel 사용자 정의 속성 추가

사용자 정의 속성을 사용하면 Excel 파일 내부에 임의의 메타데이터를 저장할 수 있습니다. 여기서는 숫자 값으로 `ProjectId`라는 **add custom property Excel**을 추가합니다.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add` 메서드는 속성 이름과 지원되는 모든 유형(문자열, 숫자, 날짜 등)의 값을 받아들입니다. 이 메타데이터는 파일을 복사하는 모든 위치에 함께 이동합니다.

## 단계 4: 사용자 정의 속성 가져오기 및 표시

속성을 다시 읽어오면 올바르게 저장되었는지 확인할 수 있습니다. 가져온 값을 비즈니스 로직에 활용할 수도 있습니다.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

우리는 숫자 값을 저장했기 때문에 `int`로 캐스팅이 가능합니다. 문자열을 저장했다면 `(String)`을 사용하세요.

## 단계 5: 워크북을 XLSB로 저장

이제 **save workbook as XLSB**합니다. XLSB 형식은 워크북을 이진 형태로 저장하므로 열기가 더 빠르고 디스크 공간도 적게 차지합니다. 모든 사용자 정의 속성은 자동으로 보존됩니다.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

특정 디렉터리에 파일이 필요하다면 `"WithCustomProps.xlsb"`를 절대 경로로 교체하세요. `SaveFormat.XLSB` 열거형은 Aspose.Cells에 이진 형식으로 쓰도록 지시합니다.

## 단계 6: 출력 확인

IDE 또는 명령줄에서 프로그램을 실행합니다:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

다음과 같은 출력이 표시됩니다:

```
ProjectId = 12345
```

`WithCustomProps.xlsb`를 Excel에서 엽니다. **File → Info → Properties → Advanced Properties → Custom** 순으로 이동합니다. 값이 `12345`인 `ProjectId` 항목이 표시되어 **add custom property excel** 단계가 성공했으며 **save workbook as xlsb** 작업이 메타데이터를 유지했음을 확인할 수 있습니다.

## 일반적인 질문 및 엣지 케이스

### 문자열 속성을 저장해야 하면 어떻게 하나요?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

다음과 같이 가져옵니다:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### 한 번에 여러 사용자 정의 속성을 추가할 수 있나요?

예. 각 이름/값 쌍마다 `add`를 반복 호출하면 됩니다. Aspose.Cells는 사용자 정의 속성 수에 제한을 두지 않지만, 파일이 비대해지지 않도록 전체 크기를 적절히 유지하세요.

### 이진 형식이 성능에 어떤 영향을 미치나요?

XLSB 파일은 XML 파싱을 피하기 때문에 로드 속도가 빠릅니다. 특히 행이 많거나 수식, 삽입 이미지가 많은 워크북에서 그 차이가 크게 나타납니다.

### 기존 XLSX 파일을 작업해야 하면 어떻게 하나요?

`new Workbook()` 생성자를 `new Workbook("ExistingFile.xlsx")`으로 교체합니다. 나머지 단계(속성 추가, XLSB로 저장)는 동일하게 진행됩니다.

## 전체 소스 코드

아래는 완전한 실행 가능한 예제입니다. `src/main/java` 폴더에 `CustomPropertiesXlsb.java`라는 파일명으로 복사하세요.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

이 클래스를 실행하면 사용자 정의 속성이 포함된 XLSB 파일이 생성되며, 최신 버전의 Microsoft Excel에서 열 수 있습니다.

## 결론

이제 Java를 사용해 **create new workbook Aspose**, **add custom property Excel**, **save workbook as XLSB**하는 방법을 알게 되었습니다. 예제는 초기화, 메타데이터 삽입, 검증, 이진 직렬화의 전체 수명 주기를 보여줍니다.

다음으로 **setting document properties**, **working with Excel formulas**, **converting between XLSX and XLSB**와 같은 관련 주제를 살펴보세요. 이들 모두 방금 사용한 Aspose.Cells API를 기반으로 하므로 새로운 라이브러리를 배우지 않아도 솔루션을 확장할 수 있습니다.

다양한 데이터 유형, 여러 워크시트, 비밀번호 보호 등을 자유롭게 실험해 보세요—Aspose.Cells는 이러한 모든 시나리오를 기본적으로 지원합니다. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방법을 탐색하는 데 도움이 됩니다.

- [Aspose Cells Java로 Excel 워크북 만들기 및 저장](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java를 사용해 Excel 워크북을 SVG로 만들고 저장하는 방법](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells for Java로 Excel 워크북 만들기 및 레이블 추가](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}