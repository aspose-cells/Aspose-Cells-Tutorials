---
category: general
date: 2026-11-25
description: 편집 가능한 도형이 포함된 Excel을 PPTX로 내보내는 방법을 배워보세요. 이 가이드는 인쇄 영역을 설정하고 프레젠테이션용
  Excel 차트를 변환하는 방법도 보여줍니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: ko
lastmod: 2026-11-25
og_description: Aspose.Cells를 사용하여 편집 가능한 도형이 포함된 Excel을 PPTX로 내보내는 방법, 인쇄 영역 설정 및
  프레젠테이션용 Excel 차트 변환 팁.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: 편집 가능한 도형이 포함된 Excel을 PPTX로 내보내는 방법
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: 편집 가능한 도형이 포함된 Excel을 PPTX로 내보내는 방법
url: /ko/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 편집 가능한 도형이 포함된 PPTX로 내보내는 방법

PowerPoint로 **how to export Excel** 파일을 내보내면서 편집 가능한 텍스트 상자와 도형을 보존해야 한다면, 이 가이드는 전체 과정을 안내합니다. 또한 집중된 슬라이드를 위해 **set print area**를 설정하는 방법과 **convert Excel chart** 객체를 변환하여 내보낸 후에도 완전히 편집 가능하도록 하는 방법을 배울 수 있습니다.

데이터 기반 보고서에서 프레젠테이션 데크를 만들 때 Excel을 PPTX로 내보내는 경우가 흔합니다. Aspose.Cells for Java를 사용하면 수동 복사‑붙여넣기를 피하고, 서식을 그대로 유지하며, 출력에 대한 프로그래밍 제어를 얻을 수 있습니다.

## 배울 내용

* 텍스트 상자 또는 차트가 포함된 기존 XLSX 워크북을 로드합니다.  
* 내보내기 옵션을 구성하여 결과 PPTX 파일에 **editable shapes**가 포함되도록 합니다.  
* **Set the print area**를 설정하여 내보낼 범위를 필요한 셀로 제한합니다.  
* 워크시트를 PPTX 파일로 저장하고 텍스트 상자와 차트를 PowerPoint에서 편집할 수 있는지 확인합니다.  

**전제 조건**

* Java 17 이상이 설치되어 있어야 합니다.  
* 의존성 관리를 위한 Maven 또는 Gradle.  
* Excel 워크북 및 Java 프로그래밍에 대한 기본 이해.

---

## Excel을 편집 가능한 도형이 포함된 PPTX로 내보내는 방법

이 섹션에서는 내보내기를 수행하는 핵심 코드를 제공합니다. 예제는 Aspose.Cells 23.9(작성 시 최신 버전)를 사용하며 필요한 모든 단계를 보여줍니다.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### 각 라인이 중요한 이유

1. **Dependency** – Aspose.Cells는 워크시트를 PPTX 슬라이드로 렌더링할 수 있는 `ImageOrPrintOptions` 클래스를 제공합니다. Maven을 통해 추가하면 라이브러리가 클래스패스에 포함됩니다.  
2. **Imports** – 올바른 클래스를 import하면 코드가 깔끔해지고 완전한 클래스 이름을 피할 수 있습니다.  
3. **Loading the workbook** – 내보내려는 객체가 포함된 정확한 파일을 지정해야 합니다. 경로는 절대 경로나 프로젝트 루트에 대한 상대 경로일 수 있습니다.  
4. **Export options** – `setEditable(true)`를 설정하는 것이 **how to export Excel**의 핵심이며, 이렇게 하면 결과 PowerPoint 도형이 편집 가능하게 유지됩니다. 이 플래그가 없으면 텍스트 상자가 정적 이미지가 됩니다.  
5. **Print area** – `setPrintArea` 호출은 내보내기를 원하는 영역으로 제한하여 파일 크기를 줄이고 불필요한 행/열을 제거합니다. 이는 **set print area excel** 요구 사항을 직접 해결합니다.  
6. **Saving** – `SaveFormat.PPTX` 상수는 Aspose.Cells에 이미지나 PDF가 아닌 PowerPoint 파일을 생성하도록 지시합니다.

#### 예상 출력

프로그램을 실행한 후 PowerPoint에서 `EditableShapes.pptx`를 엽니다. 선택한 Excel 범위를 그대로 반영한 슬라이드가 표시되며, 텍스트 상자나 차트 범례를 더블 클릭하면 기본 PowerPoint 객체처럼 편집할 수 있습니다.

---

## Excel에서 인쇄 영역 설정하기

워크시트의 일부만 필요할 때 **print area**를 정의하면 성능과 시각적 명확성을 모두 향상시킵니다.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* 나중에 데이터 범위를 변경하면 내보내기 전에 `setPrintArea`를 다시 호출하십시오. 내보내기는 최신 설정을 반영합니다.

---

## XLSX 차트를 편집 가능한 PowerPoint 차트로 변환하기

Aspose.Cells는 차트를 그리기 객체로 취급합니다. `setEditable(true)`를 활성화하면 차트가 기본 PowerPoint 차트로 변환되어 편집이 가능해집니다(예: 시리즈, 축 제목 변경).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

여러 차트가 포함된 **how to convert xlsx** 파일이 필요하면 각 워크시트에 대해 내보내기를 반복하거나 활성 시트를 조정한 후 `Workbook.save`와 `SaveFormat.PPTX`를 사용하십시오.

---

## 프로그래밍 방식으로 XLSX 변환하기 (보너스)

PPTX 외에도 워크북을 PDF나 PNG와 같은 다른 형식으로 변환하고 싶을 수 있습니다. 동일한 `ImageOrPrintOptions` 클래스를 사용하면 이러한 대상에도 적용됩니다:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

이는 Aspose.Cells의 보다 넓은 **how to convert xlsx** 기능을 보여줍니다.

---

## 일반적인 함정 및 모범 사례 팁

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| 도형이 이미지가 됨 | `setEditable(false)`(기본값) | `exportOptions.setEditable(true)` 호출 |
| 내보낸 슬라이드가 비어 있음 | 인쇄 영역에 데이터가 포함되지 않음 | `setPrintArea`에 전달된 범위 문자열을 확인하십시오 |
| 차트 서식 손실 | 구버전 Aspose.Cells 사용 | 최신 라이브러리(≥ 23.9)로 업그레이드 |
| 파일 크기 큼 | 전체 워크시트를 내보냄 | 인쇄 영역을 제한하거나 사용하지 않는 행/열을 숨기기 |

---

## 결론

이제 **how to export Excel** 워크북을 PPTX로 내보내어 완전한 편집 가능한 도형과 차트를 포함시키는 방법, **set print area**를 설정해 출력 범위를 집중시키는 방법, 그리고 **convert Excel chart** 객체를 변환해 원활한 프레젠테이션 편집을 수행하는 방법을 알게 되었습니다. 위의 완전하고 실행 가능한 Java 예제는 Aspose.Cells를 이미 사용 중인 모든 프로젝트에 바로 적용할 수 있습니다.

**다음 단계**

* PowerPoint에서 **convert excel chart** 옵션을 탐색해 보세요(예: 차트 유형 변경).  
* 이 내보내기를 **set print area excel** 자동화와 결합하여 단일 워크북에서 여러 슬라이드를 생성하십시오.  
* 동일한 `ImageOrPrintOptions` 패턴을 사용해 다른 형식(PDF, PNG)으로 내보내기를 시도해 보세요.

다양한 범위, 여러 워크시트, 맞춤 슬라이드 레이아웃을 자유롭게 실험해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Excel에서 인쇄 영역을 설정하고 PowerPoint로 내보내는 방법](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Excel을 PowerPoint로 변환하고 인쇄 영역 설정하기](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Excel에서 인쇄 영역을 설정하고 PowerPoint로 내보내기 – 단계별 가이드](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}