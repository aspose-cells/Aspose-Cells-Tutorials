---
category: general
date: 2026-09-27
description: Java에서 Aspose.Cells를 사용하여 Excel 시트를 PowerPoint로 내보내는 방법 – Excel 워크북을
  PowerPoint 프레젠테이션으로 변환하는 방법도 보여주는 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: ko
lastmod: 2026-09-27
og_description: Java에서 Aspose.Cells를 사용하여 Excel 시트를 PowerPoint로 내보내는 방법. 전체 코드를 통해
  Excel 워크북을 PowerPoint 프레젠테이션으로 변환하는 방법을 배워보세요.
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: Excel 시트를 PowerPoint로 내보내는 방법 – Aspose.Cells를 사용한 Java 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: Java에서 Aspose.Cells를 사용하여 Excel 시트를 PowerPoint로 내보내는 방법
url: /ko/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용한 Java에서 Excel 시트를 PowerPoint로 내보내는 방법

Excel 시트를 PowerPoint로 내보내는 방법이 필요하다면, 이 튜토리얼은 완전하고 바로 실행할 수 있는 솔루션을 제공합니다. **Excel 워크북을 PowerPoint 프레젠테이션으로 변환**하는 방법을 정확히 확인할 수 있으며, 편집 가능한 텍스트 상자와 기본 서식을 보존합니다.

이 가이드는 작업 중인 Java 개발 환경과 유효한 Aspose.Cells for Java 라이선스가 있다고 가정합니다. 기사 끝까지 읽으면 Excel 워크북을 로드하고, 첫 번째 워크시트를 내보내며, Microsoft PowerPoint에서 열고 편집할 수 있는 `.pptx` 파일을 작성하는 Java 프로그램을 얻게 됩니다.

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 이상 | Aspose.Cells는 최신 Java 런타임을 지원하며 성능이 향상됩니다. |
| Aspose.Cells for Java (버전 23.10 이상) | 라이브러리에는 변환에 사용되는 `Workbook.save(..., SaveFormat.PPTX)` 오버로드가 포함되어 있습니다. |
| Aspose.Cells 라이선스 사본 | 라이선스가 없으면 라이브러리가 평가 모드로 실행되어 워터마크가 추가됩니다. |
| 최소 하나의 편집 가능한 텍스트 상자를 포함한 Excel 파일 | 변환 시 텍스트 상자가 PowerPoint에서 편집 가능한 도형으로 보존됩니다. |
| IDE 또는 빌드 도구 (예: Maven, Gradle) | 예제 코드를 컴파일하고 실행하기 위해 필요합니다. |

## Step 1: Add Aspose.Cells to your project

Maven을 사용하는 경우 `pom.xml`에 다음 종속성을 추가하십시오:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Gradle을 사용하는 경우 `build.gradle`에 다음 스니펫을 배치하십시오:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** 서버에서 런타임에만 라이브러리가 필요하다면 `provided` 스코프에 종속성을 선언하십시오.

## Step 2: Prepare the Excel workbook

첫 번째 워크시트에 편집 가능한 텍스트 상자를 포함하는 Excel 파일(`WorkbookWithTextbox.xlsx`)을 만듭니다. 텍스트 상자는 Excel에서 **Insert → Text Box**를 통해 삽입할 수 있습니다. 예를 들어 `src/main/resources`와 같이 Java에서 참조할 수 있는 디렉터리에 파일을 저장하십시오.

## Step 3: Write the conversion code

`ExportEditableTextbox`라는 이름의 Java 클래스를 생성합니다. 아래 코드는 전체 import, 오류 처리 및 각 작업을 설명하는 주석을 포함합니다.

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### Why this works

* `Workbook`은 전체 Excel 파일을 나타냅니다. 로드하면 모든 워크시트, 차트 및 도형을 파싱합니다.
* `workbook.save(..., SaveFormat.PPTX)`는 Aspose.Cells의 내장 변환 엔진을 호출합니다. 이 엔진은 Excel 셀, 행 및 도형을 PowerPoint 슬라이드에 매핑하고, 편집 가능한 텍스트 상자를 PowerPoint 도형으로 보존합니다.
* 이 메서드는 워크시트당 하나의 슬라이드를 작성합니다. 이 예제에서는 첫 번째 워크시트가 유일한 슬라이드가 됩니다.

## Step 4: Run the program

빌드 도구를 사용해 클래스를 컴파일하고 실행하십시오:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

Gradle을 사용하는 경우:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

프로그램이 완료되면 Microsoft PowerPoint에서 `Worksheet.pptx`를 엽니다. Excel 시트를 그대로 복제한 슬라이드가 표시되고, Excel에서 만든 텍스트 상자는 더블 클릭하여 수정할 수 있는 편집 가능한 도형으로 나타납니다.

## Step 5: Handling multiple worksheets (optional)

워크북의 **전체** 워크시트를 내보내야 하는 경우, 단일 워크시트 호출을 루프로 교체하십시오:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

각 반복은 별도의 PowerPoint 파일(`Worksheet_0.pptx`, `Worksheet_1.pptx`, …)을 생성합니다. 여러 슬라이드를 포함하는 단일 프레젠테이션이 필요하면 `save`를 한 번 호출할 때 Aspose.Cells가 워크시트당 슬라이드를 자동으로 추가하므로 추가 코드는 필요하지 않습니다.

## Edge cases and best practices

| Situation | Recommended approach |
|-----------|----------------------|
| 대용량 워크북(수백 MB) | JVM 힙(`-Xmx4g`)을 늘리고 메모리 부족 오류를 방지하기 위해 워크시트를 개별적으로 내보내는 것을 고려하십시오. |
| 암호로 보호된 워크북 | 로드하기 전에 `LoadOptions`를 사용해 비밀번호를 제공하십시오: `new LoadOptions(LoadFormat.XLSX, "pwd")`. |
| Excel 수식 유지 필요 | PowerPoint는 수식을 지원하지 않으며, 변환 중에 정적 값으로 렌더링됩니다. |
| 사용자 정의 슬라이드 레이아웃 필요 | 변환 후 Aspose.Slides for Java를 사용해 생성된 `.pptx`를 조작하여 슬라이드 마스터를 수정하거나 애니메이션을 추가하십시오. |
| 웹 서비스에서 실행 | 파일을 쓰는 대신 HTTP 응답 스트림에 직접 출력하십시오: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## Expected output

예제를 실행하면 `Worksheet.pptx`라는 파일이 생성됩니다. PowerPoint에서 열면 다음과 같이 표시됩니다:

* 첫 번째 Excel 워크시트와 시각적으로 일치하는 하나의 슬라이드.
* Excel에서 위치한 그대로 정확히 배치된 편집 가능한 텍스트 상자.
* 기본 셀 서식(글꼴 크기, 색상, 테두리)이 보존됨.

콘솔에는 다음이 출력됩니다:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## Conclusion

이제 Aspose.Cells for Java를 사용해 **Excel 시트를 PowerPoint로 내보내는 방법**을 알게 되었으며, 실제 시나리오에서 **Excel 워크북을 PowerPoint 프레젠테이션으로 변환**하는 방법도 이해하게 되었습니다. 이 솔루션은 단일 워크시트 내보내기, 다중 워크시트 워크북 모두에 적용 가능하며, Aspose.Slides를 활용해 슬라이드 맞춤 설정을 추가로 확장할 수 있습니다.

---

### Next steps

* 변환 후 애니메이션, 차트 또는 사용자 정의 슬라이드 마스터를 추가하려면 **Aspose.Slides for Java**를 탐색하십시오.  
* 차트를 포함한 워크북을 변환해 보십시오; Aspose.Cells는 차트를 네이티브 PowerPoint 차트 객체로 렌더링합니다.  
* 디렉터리의 Excel 파일을 읽어 파일당 PowerPoint를 생성하는 배치 처리를 조사하십시오.

코드를 자유롭게 실험하고, 파일 경로를 조정하며, 보고 서비스나 자동화된 문서 파이프라인과 같은 더 큰 Java 애플리케이션에 변환 기능을 통합해 보세요. 즐거운 코딩 되세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하며, 밀접하게 관련된 주제를 다룹니다. 각 리소스는 완전한 작업 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}