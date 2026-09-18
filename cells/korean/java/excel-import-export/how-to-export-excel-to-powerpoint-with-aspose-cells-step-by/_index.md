---
category: general
date: 2026-09-18
description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내는 방법을 배우세요. Excel을 PPTX로 변환하고,
  Excel에서 PowerPoint를 만들며, 몇 분 안에 Excel을 PowerPoint로 저장합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: ko
lastmod: 2026-09-18
og_description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내는 방법. 이 가이드를 따라 Excel을 PPTX로
  변환하고, Excel에서 PowerPoint를 만들며, Excel을 효율적으로 PowerPoint로 저장하세요.
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: Excel을 PowerPoint로 내보내는 방법 – 완전한 Aspose.Cells 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내는 방법 – 단계별 가이드
url: /ko/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 PowerPoint로 내보내는 방법 – Aspose.Cells 단계별 가이드

PowerPoint 프레젠테이션으로 **Excel을 내보내는 방법**이 필요하다면, 이 튜토리얼은 완전하고 바로 실행 가능한 솔루션을 보여줍니다. 처음 두 문장을 읽고 나면 `.xlsx` 파일을 편집 가능한 `.pptx` 로 변환하는 API 호출이 정확히 어떤 것인지 알 수 있습니다. 이 접근 방식은 차트, 그림 또는 기타 도형을 포함하는 모든 워크북에서 작동하며 Java 코드 몇 줄만 필요합니다.

이 가이드에서는 차트와 이미지의 편집 가능성을 유지하면서 **Excel을 PPTX로 변환**, **Excel에서 PowerPoint 만들기**, **Excel을 PowerPoint로 저장**하는 방법을 배웁니다. Aspose.Cells 외에 추가 도구가 필요 없으며 코드는 Java 8+ 및 최신 JDK에서 실행됩니다.  

Prerequisites:

* Java Development Kit (JDK) 8 이상이 설치되어 있음  
* Maven 또는 Gradle을 사용한 종속성 관리 (또는 클래스패스에 Aspose.Cells JAR)  
* `WithShapes.xlsx` 워크북에 최소 하나의 그림 또는 차트가 포함되어 있음  

---

![Excel을 PowerPoint로 내보내는 방법을 보여주는 다이어그램](https://example.com/diagram.png "Excel을 PowerPoint로 내보내는 방법 일러스트")

## Aspose.Cells를 사용하여 Excel을 PowerPoint로 내보내는 방법

변환의 핵심은 네 가지 간결한 단계에 있습니다. 각 단계는 메서드로 감싸져 있어 더 큰 애플리케이션에서 로직을 재사용할 수 있습니다.

### 단계 1: 도형이 포함된 워크북 로드

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**왜 중요한가:**  
워크북을 로드하면 워크시트, 그림 및 차트에 접근할 수 있습니다. Aspose.Cells는 Microsoft Office를 호출하지 않고 파일을 읽기 때문에 이 작업은 헤드리스 서버에서도 작동합니다.

### 단계 2: PowerPoint 변환을 위한 내보내기 옵션 구성

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**왜 중요한가:**  
`setExportChartAsEditable(true)`는 Aspose.Cells에 래스터 이미지 대신 벡터 도형을 생성하도록 지시합니다. 이를 통해 PowerPoint 출력이 **Excel에서 PowerPoint 만들기**를 완전 편집 가능한 차트와 함께 제공되어 대부분의 프레젠테이션 작성 워크플로를 만족합니다.

### 단계 3: 그림(또는 차트)을 편집 가능하도록 표시

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**왜 중요한가:**  
그림이 편집 가능하도록 표시되면 Aspose.Cells는 이를 PPTX 파일에 EMF/WMF 도형으로 내보냅니다. 이는 수신자가 나중에 이미지를 조정해야 하는 **Excel을 PowerPoint로 내보내기** 사용 사례에 필수적입니다.

### 단계 4: 워크북을 편집 가능한 PowerPoint 프레젠테이션으로 저장

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**왜 중요한가:**  
`save` 호출은 이전의 모든 수정(편집 가능한 그림, 차트 설정)을 하나의 `.pptx` 아카이브로 묶습니다. 결과 파일은 Microsoft PowerPoint, Google Slides 또는 PPTX 호환 뷰어에서 열 수 있습니다.

### 전체 실행 가능한 예제

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**예상 결과:**  
`Result.pptx`를 PowerPoint에서 열면 `WithShapes.xlsx`의 첫 번째 워크시트를 그대로 복제한 슬라이드가 표시됩니다. 차트는 데이터를 편집하기 위해 두 번 클릭할 수 있는 벡터 도형으로 나타나며, 첫 번째 그림은 편집 가능한 객체로 PowerPoint에서 직접 크기 조정, 색상 변경 또는 교체가 가능합니다.

---

## Excel을 PPTX로 변환 – 고급 사용자 정의

기본 흐름은 대부분의 시나리오에 충분하지만, 다음과 같은 경우가 필요할 수 있습니다:

* **여러 워크시트 내보내기** – `workbook.getWorksheets()`를 순회하고 각 워크시트마다 `workbook.save`를 호출하며, `ImageOrPrintOptions.setSlideNumber(int)`를 통해 다른 슬라이드 인덱스를 전달합니다.
* **슬라이드 크기 제어** – `exportOptions.setImageHeight(int)`와 `setImageWidth(int)`를 사용하여 특정 PowerPoint 슬라이드 크기(예: 1024 × 768)에 맞춥니다.
* **수식 보존** – 원본 Excel 수식을 숨겨진 데이터로 포함하려면 `exportOptions.setExportFormulasAsValues(false)`를 설정합니다.

이러한 조정으로 기업 브랜드나 프레젠테이션 표준에 맞는 **Excel에서 PowerPoint 만들기**를 할 수 있습니다.

---

## Excel을 PowerPoint로 저장 – 흔히 발생하는 문제와 해결 방법

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| 차트가 래스터 이미지로 표시됨 | `setExportChartAsEditable(false)` (기본값) | `setExportChartAsEditable(true)` 로 편집 가능한 차트를 활성화 |
| 슬라이드에 그림이 표시되지 않음 | 그림이 편집 가능하도록 표시되지 않았거나 그림 인덱스가 범위를 벗어남 | `setEditable(true)` 호출 전에 `sheet.getPictures().size() > 0` 를 확인 |
| 숨겨진 워크시트가 PPTX에 나타남 | `setExportHiddenWorksheet(true)` | 기본값 `false` 를 유지하거나 명시적으로 `false` 로 설정 |
| 출력 파일이 손상됨 | 구버전 Aspose.Cells 사용 (pre‑20.10) | 최신 Aspose.Cells for Java (예: 23.12) 로 업그레이드 |

---

## Excel을 PowerPoint로 내보내기: 성능 팁

* **같은 `ImageOrPrintOptions` 객체를 여러 번 저장에 재사용** – 반복 할당을 방지합니다.
* **소스 워크북을 스트리밍** (`new Workbook(InputStream)`) 하면 메모리 제한 서버에서 대용량 파일을 처리할 때 유용합니다.
* **워크시트별 변환을 병렬화** 하면 수백 개 슬라이드의 데크를 생성할 때 도움이 됩니다; 각 워크시트는 자체 스레드에서 처리할 수 있으며 Aspose.Cells 객체는 생성 후 스레드 안전합니다.

---

## 다음 단계

이제 **Excel을 PowerPoint로 내보내는 방법**, **Excel을 PPTX로 변환**, **Excel을 PowerPoint로 저장**을 편집 가능한 콘텐츠와 함께 알게 되었습니다. 이 지식을 확장하려면 다음을 시도할 수 있습니다:

* **Aspose.Slides**를 탐색하여 변환 후 애니메이션이나 마스터 슬라이드 레이아웃을 추가합니다.
* CI/CD 파이프라인에서 워크플로를 자동화하여 새로운 Excel 보고서가 자동으로 PPTX 슬라이드 데크가 되도록 합니다.
* Aspose.Cells에 전달하기 전에 Excel 파일을 사전 처리하기 위해 **Apache POI**와 이 접근 방식을 결합합니다.

## 결론

이 튜토리얼에서는 Aspose.Cells를 사용하여 **Excel을 PowerPoint로 내보내는 방법**을 워크북 로드부터 편집 가능한 `.pptx` 저장까지 모든 단계를 다루었습니다. 이제 Java 애플리케이션에서 **Excel을 PPTX로 변환**, **Excel에서 PowerPoint 만들기**, **Excel을 PowerPoint로 저장**을 자신 있게 수행할 수 있습니다. 선택적 설정을 실험하여 출력물을 정확한 프레젠테이션 요구에 맞게 조정해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 전체 작동 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET를 사용하여 Excel을 PowerPoint로 변환하는 방법: 완전 가이드](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel을 PowerPoint로 내보내는 방법 – 단계별 가이드](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [C#를 사용하여 Excel을 PowerPoint로 내보내는 방법 – 완전 가이드](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}