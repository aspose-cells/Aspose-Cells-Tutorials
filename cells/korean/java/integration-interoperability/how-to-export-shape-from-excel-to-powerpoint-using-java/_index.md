---
category: general
date: 2026-11-16
description: Java에서 Excel 도형을 PowerPoint로 내보내는 방법, Excel 차트를 PPTX 파일로 변환하고 Aspose.Cells로
  도형 PPTX를 저장하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: ko
lastmod: 2026-11-16
og_description: Java에서 Excel 도형을 PowerPoint로 내보내는 방법. 이 전체 튜토리얼을 따라 Excel 차트를 변환하고,
  도형을 PPTX로 저장하며, 도형을 PowerPoint 파일에 삽입하세요.
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: Java에서 Excel 도형을 PowerPoint로 내보내는 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: Java를 사용하여 Excel에서 PowerPoint로 도형 내보내는 방법
url: /ko/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java를 사용하여 Excel에서 PowerPoint로 도형을 내보내는 방법

Excel 워크북에 있는 **도형을 내보내는 방법**을 PowerPoint 슬라이드에 삽입하고 싶다면, 이 가이드는 정확한 단계들을 보여줍니다. **Excel 차트** 객체를 **PowerPoint 도형**으로 변환하고, 최종적으로 **도형 PPTX 저장** 옵션을 사용해 저장하는 과정을 확인할 수 있습니다.

도형을 내보내는 것은 프로그램matically 보고서를 생성할 때 흔히 요구되는 작업입니다. 이 튜토리얼을 마치면 프레젠테이션용 `shape.pptx` 파일을 생성하는 독립 실행형 Java 프로그램을 갖게 됩니다. 외부 스크립트는 필요 없으며, 코드는 Aspose.Cells 2024‑R2 이상 버전에서 동작합니다.

## Prerequisites

* Java 17 이상 (코드는 JDK 8+에서도 컴파일됩니다)
* Aspose.Cells for Java 라이브러리 (Aspose 웹사이트에서 다운로드하거나 Maven 의존성을 추가)
* 최소 하나의 도형(차트, 텍스트 상자 또는 SmartArt)이 포함된 Excel 파일(`chart.xls`)
* Java 예외 처리에 대한 기본 지식

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## Excel에서 PowerPoint로 도형을 내보내는 전체 흐름

이 과정은 네 개의 논리적 섹션으로 구성됩니다:

1. **도형이 포함된 워크북 로드**  
2. **첫 번째 워크시트에서 도형 찾기**  
3. **내보내기 옵션 구성** – 도형을 편집 가능한 PowerPoint 객체로 만들기  
4. **도형을 PPTX 파일로 저장**

각 섹션은 아래에서 자세히 설명하며, 전체 실행 가능한 프로그램은 설명 뒤에 제공합니다.

## Step 1: 도형이 포함된 워크북 로드

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*왜 이 단계가 필요한가?*  
`Workbook`은 Aspose.Cells 모든 작업의 진입점입니다. 파일을 로드하면 워크시트, 셀 및 도형 컬렉션에 접근할 수 있습니다. 파일을 찾을 수 없으면 Aspose.Cells가 `FileNotFoundException`을 발생시키며, 이는 이후에 잡아 처리합니다.

## Step 2: 첫 번째 워크시트에 접근하고 대상 도형 가져오기

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*왜 이 단계가 필요한가?*  
워크시트는 0부터 시작하는 컬렉션에 저장되므로 `get(0)`은 첫 번째 시트를 반환합니다. 도형도 인덱스로 관리되며, `get(0)`은 일반적으로 내보내려는 차트인 첫 번째 도형을 가져옵니다. 워크북에 여러 도형이 있는 경우 컬렉션을 반복하거나 `shape.getName()`을 사용해 특정 도형을 선택할 수 있습니다.

## Step 3: 내보내기 옵션 준비 – 편집 가능한 PPTX 객체로 도형 만들기

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*왜 이 단계가 필요한가?*  
`ImageOrPrintOptions`는 도형이 렌더링되는 방식을 제어합니다. `SaveFormat.PPTX`를 선택하면 라이브러리가 Excel 그래픽을 벡터 기반 PowerPoint 도형으로 변환하여 가져온 뒤에도 편집이 가능합니다. 이는 **Excel 차트를 PowerPoint 도형으로 변환**하는 핵심 단계이며, PNG나 JPEG와 같은 이미지 포맷을 사용하면 그래픽이 고정됩니다.

## Step 4: 도형을 PowerPoint 파일로 내보내기

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*왜 이 단계가 필요한가?*  
`save` 메서드는 앞서 정의한 옵션을 사용해 도형을 파일에 기록합니다. 결과물인 `shape.pptx`는 Excel에서 보였던 도형이 그대로 나타나는 단일 슬라이드를 포함하지만, 이제 PowerPoint에서 색상 변경, 크기 조정, 애니메이션 추가 등 편집이 가능합니다. 이는 **도형 PPTX 저장** 요구사항을 충족합니다.

## 전체 실행 가능한 예제

전체 클래스를 `ExportShapeDemo.java` 파일에 복사하고, `YOUR_DIRECTORY`를 절대 경로나 상대 경로로 교체한 뒤 `javac ExportShapeDemo.java && java ExportShapeDemo` 명령을 실행하세요. 실행 후 대상 폴더에 `shape.pptx`가 생성됩니다.

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### 예상 출력

```
Export completed. File saved as shape.pptx
```

Microsoft PowerPoint에서 `shape.pptx`를 열면 원본 Excel 차트(또는 텍스트 상자)가 완전히 편집 가능한 PowerPoint 도형으로 포함된 단일 슬라이드를 확인할 수 있습니다.

## 일반적인 변형 및 예외 상황

| 상황 | 권장 조정 |
|-----------|------------------------|
| **여러 도형** | `worksheet.getShapes()`를 순회하면서 각 도형에 대해 `save`를 호출하거나 `shape.getName()`으로 특정 도형을 선택 |
| **데이터 시리즈가 있는 차트 도형** | `exportOptions.setExportChartAsEditable(true)`를 사용해 시리즈를 편집 가능하게 유지 |
| **특정 슬라이드 레이아웃 필요** | 저장 후 Aspose.Slides로 PPTX를 열어 도형을 사용자 정의 레이아웃에 삽입 |
| **대용량 워크북** | `Workbook(String, LoadOptions)`를 사용해 필요한 워크시트만 로드해 메모리 사용량 감소 |
| **다른 출력 포맷(PDF, PNG)** | `exportOptions.setSaveFormat(SaveFormat.PDF)` 또는 `SaveFormat.PNG`로 변경. 이는 **Excel 차트를 정적 이미지**로 변환할 때 유용 |

**팁:** 도형 인덱스(`get(0)`)가 실제 내보내려는 시각적 요소와 일치하는지 항상 확인하세요. 도형 컬렉션 순서는 Excel에 삽입된 순서를 반영하므로 시각적 쌓임 순서와 다를 수 있습니다.

## Excel에서 PowerPoint로 도형을 내보내는 문제 해결 체크리스트

* **파일을 찾을 수 없음** – `new Workbook()`에 지정한 경로가 존재하는 `.xls` 또는 `.xlsx` 파일을 가리키는지 확인  
* **도형이 반환되지 않음** – 워크시트에 실제 도형이 있는지 확인하고, `worksheet.getShapes().getCount()`로 디버깅  
* **내보낸 파일이 비어 있음** – `exportOptions.setSaveFormat(SaveFormat.PPTX)`가 설정되었는지 확인. 이미지 포맷을 사용하면 도형 대신 그림이 저장됩니다.  
* **호환성 문제** – Aspose.Cells 24.9 이상은 모든 주요 플랫폼에서 PPTX 내보내기를 지원합니다. `UnsupportedOperationException`이 발생하면 업그레이드하세요.

## 결론

이제 Java를 사용해 Excel 워크북에서 **도형을 내보내는 방법**을 알고, PowerPoint 프레젠테이션에 삽입할 수 있습니다. 튜토리얼에서는 워크북 로드, 도형 찾기, **Excel에서 도형 내보내기** 옵션 구성, 그리고 **도형 PPTX 저장**까지 전 과정을 다루었습니다. 이를 기반으로 보고서 자동 생성, 대시보드 구축, Excel 시각화를 슬라이드에 수동 복사‑붙여넣기 없이 통합할 수 있습니다.

### 다음 단계

* **Excel 차트를 PDF 또는 DOCX**와 같은 다른 Office 포맷으로 변환하는 방법 탐색  
* 이 기술을 Aspose.Slides와 결합해 하나의 슬라이드에 여러 도형 배치  
* `ImageOrPrintOptions` 속성(예: `setResolution`, `setTransparent`)을 실험해 내보낸 도형의 시각적 품질 미세 조정

코드를 배치 처리에 맞게 수정하거나 더 큰 보고 서비스에 통합해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하는 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to export shape with ShapeExportOptions in Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Export Charts from Excel to PowerPoint – Full Java Guide](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}