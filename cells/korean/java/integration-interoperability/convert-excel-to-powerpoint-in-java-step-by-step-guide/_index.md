---
category: general
date: 2026-11-22
description: Aspose.Cells를 사용하여 Java에서 Excel을 PowerPoint로 변환합니다. Excel 파일에서 PowerPoint를
  만드는 방법, 워크시트를 PPTX 슬라이드로 내보내는 방법, 프레젠테이션을 자동화하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: ko
lastmod: 2026-11-22
og_description: Aspose.Cells를 사용하여 Java에서 Excel을 PowerPoint로 변환합니다. 이 튜토리얼에서는 Excel
  파일에서 PowerPoint를 만들고 .xlsx를 .pptx 슬라이드로 내보내는 방법을 보여줍니다.
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: Java에서 Excel을 PowerPoint로 변환하기 – 완전 프로그래밍 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: Java에서 Excel을 PowerPoint로 변환하기 – 단계별 가이드
url: /ko/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 PowerPoint로 변환하기 (Java) – 단계별 가이드

Java에서 **Excel을 PowerPoint로 변환**해야 한다면, 이 가이드는 Aspose.Cells를 사용하여 수행하는 방법을 보여줍니다. 보고서 엔진을 구축하거나 슬라이드 데크를 자동화하든, 프로그래밍 방식으로 **Excel 파일에서 PowerPoint 만들기**를 배우고 각 워크시트를 편집 가능한 PPTX 슬라이드로 내보낼 수 있습니다.

이 튜토리얼은 프로젝트 설정부터 최종 프레젠테이션 저장까지 모든 과정을 다룹니다. 끝까지 진행하면 `.xlsx` 워크북을 Microsoft PowerPoint에서 편집 가능한 `.pptx` 파일로 변환하는 실행 가능한 Java 프로그램을 얻을 수 있습니다. 수동 복사‑붙여넣기는 필요 없습니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* Java 17 이상이 설치되어 있어야 합니다(코드가 최신 모듈 시스템을 사용합니다).  
* Aspose.Cells for Java 라이선스 또는 임시 평가 키.  
* Maven 또는 Gradle(예제는 Maven 사용)으로 의존성 관리.  
* 알려진 디렉터리에 위치한 샘플 Excel 워크북(`input.xlsx`).

> **Pro tip:** Aspose.Cells는 `.xls`와 `.xlsx` 모두를 지원합니다. 동일한 코드를 두 형식에 모두 사용할 수 있으니 파일 확장자만 바꾸면 됩니다.

## Step 1: **Excel을 PowerPoint로 변환**하기 위한 Java 프로젝트 설정

새 Maven 프로젝트를 만들거나 기존 프로젝트에 추가하고 Aspose.Cells 의존성을 포함합니다:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

`mvn clean install`을 실행하여 라이브러리를 다운로드합니다. 라이선스 파일(`Aspose.Total.lic`)이 있다면 `src/main/resources` 폴더에 배치하면 코드가 자동으로 로드합니다.

## Step 2: Excel 워크북 로드

**Excel 워크북을 PPTX 슬라이드로 변환** 프로세스의 첫 번째 기능 단계는 소스 파일을 로드하는 것입니다. Aspose.Cells는 파일 시스템, 스트림, 혹은 바이트 배열에서 파일을 열 수 있습니다.

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**왜 중요한가:** 워크북을 로드하면 파일 형식이 검증되고, 이후 Aspose.Cells가 PowerPoint 객체로 변환할 내부 구조가 준비됩니다.

## Step 3: **Excel 파일에서 PowerPoint 만들기**를 위한 저장 옵션 구성

Aspose.Cells는 프레젠테이션 파일로 변환할 때 출력 형식을 정의하기 위해 `ImageOrPrintOptions`를 사용합니다. `SaveFormat`을 `SaveFormat.PPTX`로 설정하면 편집 가능한 슬라이드가 생성됩니다.

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**왜 중요한가:** `setOnePagePerSheet(false)` 플래그는 Aspose.Cells에게 각 워크시트를 개별 슬라이드로 처리하도록 지시합니다. 이는 **Excel을 PowerPoint로 변환**할 때 가장 일반적인 시나리오입니다.

## Step 4: 워크북을 PPTX 슬라이드로 저장

이제 프레젠테이션을 디스크에 기록할 수 있습니다. `Workbook.save` 메서드는 출력 경로와 앞서 구성한 옵션을 인수로 받습니다.

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

Microsoft PowerPoint에서 `editable.pptx`를 열면 워크시트당 하나의 슬라이드가 표시되며, 모든 셀은 편집 가능한 텍스트 상자와 도형으로 렌더링됩니다. 폰트, 색상 등을 추가로 편집하거나 애니메이션을 직접 삽입할 수 있습니다.

### 예상 출력

프로그램 실행 시 다음과 같이 출력됩니다:

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

그리고 지정한 디렉터리에 `editable.pptx` 파일이 생성되어 수동 조정이나 추가 자동화에 사용할 수 있습니다.

## Step 5: 일반적인 변형 및 엣지 케이스

### 선택된 시트만 변환하기

특정 워크시트를 제외하고 **Excel 워크북을 PPTX 슬라이드로 변환**하고 싶다면, 저장하기 전에 필터링합니다:

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### 대용량 워크북 처리

시트가 많은 워크북은 메모리 사용량이 크게 증가할 수 있습니다. `WorkbookSettings`를 사용해 스트리밍을 활성화하세요:

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 수식 보존

Aspose.Cells는 렌더링 전에 수식을 평가합니다. 슬라이드에 원시 수식 텍스트가 필요하면 `opts.setExportFormulas(true)`를 설정합니다.

## Step 6: 결과를 프로그래밍 방식으로 검증하기 (선택)

생성된 PPTX를 Aspose.Slides로 로드하여 슬라이드 수가 워크시트 수와 일치하는지 확인할 수 있습니다:

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

이 추가 검증은 변환이 성공했는지 확인해야 하는 CI 파이프라인에서 유용합니다.

## 결론

이제 **Java에서 Excel을 PowerPoint로 변환**하는 완전하고 프로덕션 수준의 솔루션을 갖추었습니다. 프로그램은 `.xlsx` 워크북을 로드하고, `ImageOrPrintOptions`를 사용해 **Excel 파일에서 PowerPoint 만들기**를 구성한 뒤, 결과를 편집 가능한 PPTX 슬라이드로 저장합니다. 옵션을 조정하면 해상도를 미세 조정하고, 특정 시트를 선택하거나 대용량 파일을 스트리밍하는 등 다양한 자동화 시나리오에 유연하게 적용할 수 있습니다.

**다음 단계**

* Aspose.Slides를 사용해 **java convert .xlsx to .pptx**를 확장하고 사용자 정의 슬라이드 레이아웃을 추가해 보세요.  
* 간단한 디렉터리 감시자를 이용해 여러 워크북을 배치 처리하도록 자동화하세요.  
* 이 변환을 데이터 기반 차트 생성과 결합해 동적 프레젠테이션을 만들어 보세요.

설정들을 자유롭게 실험하고 결과를 공유하세요. 즐거운 코딩 되세요!


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이 가이드에서 소개한 기술을 기반으로 하며, 밀접하게 관련된 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Convert Excel to PowerPoint with Aspose.Cells in Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}