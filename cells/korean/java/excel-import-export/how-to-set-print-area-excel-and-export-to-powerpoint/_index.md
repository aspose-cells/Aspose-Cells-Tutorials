---
category: general
date: 2026-08-20
description: Aspose.Cells를 사용하여 Excel의 인쇄 영역을 설정하고 Excel을 PPTX로 내보내는 방법을 배워보세요. 이
  가이드는 워크시트를 PowerPoint로 변환하고 PPTX 파일로 저장하는 과정을 안내합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: ko
lastmod: 2026-08-20
og_description: Aspose.Cells를 사용하여 Excel의 인쇄 영역을 설정한 후 Excel을 PPTX로 내보냅니다. 이 단계별 튜토리얼을
  따라 워크시트를 PowerPoint로 변환하고 PPTX 파일로 저장하세요.
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: Excel에서 인쇄 영역 설정 및 PowerPoint로 내보내기 – 전체 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: Excel에서 인쇄 영역 설정하고 PowerPoint로 내보내는 방법
url: /ko/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 인쇄 영역 설정 및 PowerPoint로 내보내기

슬라이드 데크에 데이터를 공유하기 전에 **Excel 인쇄 영역 설정**이 필요하다면, 이 튜토리얼에서 정확히 어떻게 하는지 보여드립니다. 인쇄 영역을 구성하고, **Excel을 PPTX로 내보내기**하면서 텍스트 상자를 편집 가능하게 유지하는 방법을 확인할 수 있습니다. 결과물인 PowerPoint는 추가 편집이 바로 가능합니다.

우리는 Aspose.Cells for Java를 사용해 **워크시트를 PowerPoint로 변환**하고 최종적으로 **워크시트를 PPTX 형식으로 저장**합니다. Aspose.Cells JAR 외에 추가 라이브러리는 필요하지 않습니다. 이 가이드를 끝까지 따라 하면 Java 호환 환경 어디서든 코드를 실행해 선택한 Excel 범위와 동일한 프레젠테이션을 만들 수 있습니다.

## Prerequisites

- Java Development Kit 17 이상  
- Aspose.Cells for Java (공식 Aspose 사이트에서 다운로드)  
- 편집 가능한 도형이 포함된 Excel 워크북 (예: `BookWithShapes.xlsx`)  

Aspose.Cells JAR가 클래스패스에 포함되어 있는지 확인하세요:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Step 1: Aspose.Cells를 사용해 Excel 인쇄 영역 설정

첫 번째 단계는 내보낼 범위를 정의하는 것입니다. 인쇄 영역을 설정하면 변환 대상이 필요한 셀로 제한되어 성능이 향상됩니다.

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**왜 중요한가** – `setPrintArea` 메서드는 Aspose.Cells에 어떤 셀을 인쇄 가능한 페이지에 포함시킬지 알려줍니다. 이후 **Excel을 PPTX로 내보내기**를 수행하면 이 영역만 렌더링되어 불필요한 데이터가 슬라이드에 나타나지 않습니다.

### Pro tip
동적 범위가 필요하면 주소를 프로그래밍 방식으로 계산할 수 있습니다:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Step 2: 편집 가능한 텍스트 상자를 포함해 Excel을 PPTX로 내보내기

인쇄 영역을 정의한 뒤 내보내기 옵션을 설정합니다. `setExportEditableTextBoxes`를 활성화하면 도형 텍스트가 PowerPoint에서 편집 가능한 필드로 유지됩니다.

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**왜 중요한가** – 기본적으로 Aspose.Cells는 텍스트 상자를 래스터화하여 이미지의 일부로 만들습니다. `ExportEditableTextBoxes`를 `true`로 설정하면 원본 도형 객체가 보존되어 사용자가 PowerPoint에서 직접 텍스트를 수정할 수 있습니다.

## Step 3: 워크시트를 PowerPoint로 변환하고 파일 저장

이제 실제 변환을 수행합니다. `Workbook.save` 메서드는 대상 파일 이름과 앞서 준비한 옵션을 인수로 받습니다.

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

코드 실행이 끝나면 `SheetWithEditableShapes.pptx`에 정의한 인쇄 영역(`A1:G30`)과 동일한 단일 슬라이드가 포함됩니다. 텍스트 상자를 포함한 모든 도형이 편집 가능한 상태로 유지됩니다.

### Expected output
생성된 PPTX를 Microsoft PowerPoint에서 열어보세요:

- 슬라이드에 **A1부터 G30까지**의 셀 내용이 Excel과 동일하게 표시됩니다.  
- 원본 워크시트에 있던 모든 도형이 PowerPoint 도형으로 나타납니다.  
- 해당 도형 안의 텍스트는 PowerPoint에서 직접 편집할 수 있습니다 (래스터화되지 않음).

## Step 4: 전체 실행 가능한 예제

아래는 완전한 프로그램 코드입니다. `YOUR_DIRECTORY`를 실제 폴더 경로로 교체하세요.

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

*Prerequisites* 섹션에 설명된 대로 프로그램을 실행하면 지정한 디렉터리에 PowerPoint 파일이 생성됩니다.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Can I export multiple worksheets?** | Yes. Loop through `workbook.getWorksheets()` and call `save` for each sheet, optionally changing the output filename. |
| **What if my workbook contains charts?** | Charts are rendered as images by default. To keep them editable you would need to convert them to PowerPoint shapes manually, which is beyond the scope of this guide. |
| **Is the print area required?** | No. If you omit `setPrintArea`, Aspose.Cells exports the entire used range of the worksheet. Setting it gives you precise control. |
| **Does this work with .xlsx files created by other tools?** | Absolutely. Aspose.Cells supports any valid Office Open XML workbook, regardless of its origin. |

## Next steps

- **Save worksheet as PowerPoint** with custom slide layouts: explore `Presentation` class from Aspose.Slides to merge the exported slide into a larger deck.  
- **Export excel to pptx** with different image resolutions: adjust `exportOptions.setResolution(300)` for high‑DPI output.  
- **Automate batch conversions**: combine this code with a file‑watcher to process multiple Excel files in a folder.

**set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, **save worksheet as powerpoint**를 마스터하면 Excel 데이터를 프로그래밍 방식으로 슬라이드 데크에 통합할 수 있어 보고 파이프라인을 효율화하고 수동 복사‑붙여넣기 작업을 크게 줄일 수 있습니다.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}