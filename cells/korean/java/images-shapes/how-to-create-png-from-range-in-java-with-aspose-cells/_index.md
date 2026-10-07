---
category: general
date: 2026-10-07
description: Java에서 범위로부터 PNG를 생성하고 데이터를 PNG로 내보내는 방법을 배워보세요. 이 가이드는 Aspose.Cells를
  사용하여 Excel 범위 이미지를 저장하는 방법을 보여줍니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: ko
lastmod: 2026-10-07
og_description: Java에서 범위에서 PNG를 생성하고 Aspose.Cells를 사용해 데이터를 PNG로 내보냅니다. 이 완전한 튜토리얼을
  따라 Excel 범위 이미지를 즉시 저장하세요.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Java에서 범위로 PNG 만들기 – 단계별 Aspose.Cells 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java와 Aspose.Cells를 사용하여 범위에서 PNG를 만드는 방법
url: /ko/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java와 Aspose.Cells를 사용하여 범위에서 PNG 만들기

Excel 통합 문서에서 **범위에서 PNG 만들기**가 필요하다면, 이 튜토리얼이 정확한 방법을 알려드립니다. 가이드를 끝까지 따라 하면 **데이터를 PNG로 내보내기**, Excel 범위 이미지를 저장하기, 그리고 보고서나 웹 페이지에서 파일을 재사용하기가 가능해집니다.

전체 실행 가능한 Java 프로그램을 통해 통합 문서를 로드하고, 원하는 셀을 선택한 뒤 PNG로 렌더링하고, 결과를 디스크에 저장하는 과정을 확인할 수 있습니다. 외부 도구는 전혀 필요하지 않으며, Aspose.Cells가 모든 작업을 내부에서 처리합니다.

## 이 튜토리얼에서 다루는 내용

* Aspose.Cells를 위한 사전 요구 사항 및 Maven 설정
* 피벗 테이블 또는 임의 데이터 범위를 포함한 통합 문서 로드
* 변환하려는 정확한 셀 범위 정의
* PNG 출력용 이미지 옵션 구성
* 범위를 렌더링하고 PNG 파일로 저장
* 흔히 발생하는 문제와 고품질 이미지를 위한 팁

이 단계들을 마치면 **워크시트에서 PNG로 변환**하는 방법을 익히게 되며, 단순 테이블이든 복잡한 피벗 차트든 어떤 범위든 PNG로 만들 수 있습니다.

## 사전 요구 사항

* Java 17 이상 (코드는 JDK 11+에서도 컴파일됩니다)
* Maven 3.6+ (원한다면 Gradle 사용 가능)
* Aspose.Cells for Java 23.12 이상 – 아래 의존성을 추가하세요
* 캡처하려는 범위를 포함한 기존 Excel 파일(`PivotWithStyle.xlsx`)

> **Pro tip:** 라이선스가 없으면 Aspose에서 임시 평가 키를 요청할 수 있습니다. 라이브러리는 추가 설정 없이 평가 모드에서도 작동합니다.

### Maven 의존성

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## 1단계: 대상 범위가 있는 통합 문서 로드

첫 번째 작업은 Excel 파일을 여는 것입니다. Aspose.Cells는 Microsoft Office 없이 파일을 메모리로 읽어들입니다.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*왜 중요한가*: 통합 문서를 로드하면 워크시트, 셀, 페이지 설정 등 렌더링에 필요한 속성에 접근할 수 있습니다.

## 2단계: 범위를 포함하고 있는 워크시트에 접근

대부분의 통합 문서는 인덱스 0에 기본 시트가 있지만, 시트 이름을 사용할 수도 있습니다.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

데이터가 다른 시트에 있다면 `0`을 해당 인덱스로 바꾸거나 `workbook.getWorksheets().get("SheetName")`을 사용하세요.

## 3단계: 변환하려는 셀 범위 정의

A1 표기법을 사용해 사각형 영역을 지정할 수 있습니다. 여기서는 `A1:D15`를 캡처하는 예시이며, 피벗 테이블이거나 일반 데이터 블록일 수 있습니다.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*예외 상황*: 범위에 병합 셀이 포함된 경우, Aspose.Cells는 자동으로 병합 영역을 포함하도록 이미지를 확장합니다.

## 4단계: PNG 이미지 옵션 준비

`ImageOrPrintOptions`를 사용하면 포맷, 해상도 및 기타 렌더링 세부 정보를 제어할 수 있습니다. 저장 포맷을 PNG로 지정하면 무손실 품질을 보장합니다.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

소형 폰트나 세밀한 차트가 포함된 경우 DPI를 높이는 것이 유용합니다.

## 5단계: 선택한 범위만 렌더링하도록 영역 제한

범위를 인쇄 영역으로 지정하면 Aspose.Cells는 해당 셀만 렌더링하고 시트의 나머지는 무시합니다.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

이 단계를 건너뛰면 전체 워크시트가 래스터화되어 메모리를 많이 차지하고 이미지 파일이 커집니다.

## 6단계: 범위를 렌더링하고 워크시트에 그림 추가 (선택 사항)

생성된 PNG를 워크북에 다시 삽입해 미리보기 용도로 사용하고 싶다면 그림으로 추가할 수 있습니다. 순수 내보내기 시나리오에서는 이 단계가 선택 사항입니다.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*왜 할까?*: 일부 워크플로에서는 배포 전에 이미지가 워크북의 일부가 되길 요구합니다. 예를 들어, 원본 셀과 이미지를 혼합한 인쇄 가능한 보고서를 만들 때 유용합니다.

## 7단계: PNG 파일을 디스크에 저장

마지막으로 이미지를 파일로 기록합니다. `save` 메서드는 `imageOptions`에 지정된 포맷을 그대로 사용합니다.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

프로그램이 종료되면 `PivotImage.png`에 셀 `A1:D15`의 픽셀 정확도 스냅샷이 저장됩니다.

### 예상 결과

* `YOUR_DIRECTORY`에 위치한 `PivotImage.png` 파일
* 선택한 범위의 레이아웃, 폰트, 색상, 테두리가 정확히 반영된 이미지
* 원본 범위에 피벗 테이블이 포함된 경우, 렌더링된 이미지에도 Excel에 표시된 동일한 스타일과 계산값이 포함됩니다.

## 일반적인 시나리오 처리

### 비연속 범위 내보내기

Aspose.Cells는 단일 이미지에 서로 떨어진 범위를 렌더링하지 못합니다. 여러 영역을 내보내려면 각 범위마다 별도 이미지를 만든 뒤 이미지 처리 라이브러리(예: ImageIO)로 합치세요.

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### 큰 워크시트를 PNG로 저장하기

수천 행에 걸친 전체 시트를 렌더링하면 메모리 사용량이 크게 증가합니다. 다음 방법으로 완화할 수 있습니다.

* DPI를 낮추기 (`imageOptions.setResolution(72)`) → 파일 크기 감소
* `setPageCount`로 렌더링 페이지 수 제한
* `worksheet.getPageSetup().setPrintArea(...)`를 사용해 한 번에 한 페이지씩 내보내기

### 셀 수식 보존

PNG는 래스터 형식이므로 수식은 유지되지 않습니다. 다운스트림에서 원시 데이터가 필요하면 `Range.exportDataTable()`을 이용해 CSV 또는 JSON으로도 내보내세요.

## 전체 실행 가능한 예제

아래는 IDE에 복사‑붙여넣기 할 수 있는 완전한 Java 클래스입니다. `YOUR_DIRECTORY`를 실제 절대 경로나 상대 경로로 바꾸세요.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

`mvn compile exec:java`(또는 선호하는 빌드 도구)로 프로그램을 실행합니다. 실행 후 `PivotImage.png`를 열어 결과를 확인하세요.

## 결론

이제 Java와 Aspose.Cells를 사용해 **범위에서 PNG 만들기** 방법을 알게 되었으며, **데이터를 PNG로 내보내기**와 **Excel 범위 이미지를 저장하기**를 자유롭게 수행할 수 있습니다. 워크북 로드 → 범위 정의 → 이미지 옵션 설정 → 인쇄 영역 지정 → 파일 저장이라는 전체 흐름을 통해 **워크시트를 PNG로 변환**하고 **셀을 PNG로 저장**하는 작업을 마쳤습니다.

### 다음 단계

* 품질과 파일 크기 균형을 맞추기 위해 다양한 `Resolution` 값을 실험해 보세요.
* 투명 배경 PNG가 필요하면 `ImageOrPrintOptions.setTransparent(true)`를 사용하세요.
* 여러 범위 이미지를 하나의 PDF로 합치려면 `PdfSaveOptions`를 활용해 다중 페이지 보고서를 만들 수 있습니다.
* `setSaveFormat`을 변경하면 JPEG, BMP 등 다른 래스터 형식으로도 내보낼 수 있습니다.

이 패턴을 차트, 테이블, 전체 워크시트 등에도 적용해 보세요. 즐거운 코딩 되세요!


## 다음에 배워야 할 내용은?


아래 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하며, 밀접하게 관련된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}