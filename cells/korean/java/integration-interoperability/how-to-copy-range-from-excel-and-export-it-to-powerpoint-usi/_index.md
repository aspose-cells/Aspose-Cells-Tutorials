---
category: general
date: 2026-09-05
description: Excel에서 범위를 복사하는 방법, Excel을 PowerPoint로 내보내는 방법 및 Excel을 pptx 파일로 변환하는
  방법을 완전한 Java 예제로 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: ko
lastmod: 2026-09-05
og_description: Java를 사용하여 범위를 복사하고 Excel을 PowerPoint로 내보내는 방법. 이 단계별 가이드를 따라 Excel을
  PPTX로 효율적으로 변환하세요.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Java에서 Excel 범위를 복사하여 PowerPoint로 내보내는 방법
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Java를 사용하여 Excel에서 범위를 복사하고 PowerPoint로 내보내는 방법
url: /ko/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java를 사용하여 Excel에서 범위를 복사하고 PowerPoint로 내보내는 방법

Excel 워크북에서 **범위를 복사하는 방법**을 배우고 **Excel을 PowerPoint로 내보내는 방법**을 찾고 있다면, 이 가이드는 완전하고 바로 실행 가능한 솔루션을 제공합니다. 피벗 테이블이 포함된 범위를 복사하고, 복사본을 위한 새 워크시트를 만든 다음, 단일 메서드 호출로 **Excel을 PPTX로 변환**하는 과정을 정확히 확인할 수 있습니다.

범위를 복사하고 워크북을 내보내는 작업은 보고서, 슬라이드덱, 대시보드를 프로그래밍 방식으로 생성할 때 흔히 요구됩니다. 이 튜토리얼을 마치면 다음을 수행하는 Java 프로그램을 갖게 됩니다:

* 기존 `.xlsx` 파일을 로드합니다.
* 피벗 테이블을 포함한 `A1:H20` 범위를 새 시트에 복사합니다.
* 워크북을 편집 가능한 `.pptx` 프레젠테이션으로 저장합니다.

필요한 것은 Aspose.Cells for Java 라이브러리뿐이며, 추가 종속성은 필요하지 않습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* Java 17(또는 최신 버전) 설치
* Maven 또는 Gradle을 사용한 종속성 관리
* Aspose.Cells for Java 23.9(또는 최신 버전) – 아래 Maven 스니펫에 표시된 대로 프로젝트에 추가
* 복사하려는 데이터와 피벗 테이블이 포함된 Excel 파일(`input.xlsx`)

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Step 1: Load the workbook from a file

**범위 복사 방법**의 첫 번째 작업은 소스 워크북을 여는 것입니다. 이를 통해 워크시트, 셀 및 피벗 테이블에 접근할 수 있습니다.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*왜 이 단계가 필요한가요?*  
파일을 로드하면 Excel 문서의 메모리 내 표현이 생성되어 원본 파일을 건드리지 않고도 내용을 조작할 수 있습니다.

## Step 2: Get the source worksheet that holds the data

보통 첫 번째 시트에 복사하려는 데이터가 들어 있습니다. 인덱스로 해당 시트를 가져올 수 있습니다.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

워크북에 피벗 테이블이 다른 시트에 있다면 `0`을 해당 인덱스로 바꾸거나 `get("SheetName")`을 사용하세요.

## Step 3: Add a new worksheet for the copied range

대상 시트를 만들면 복사된 데이터를 격리할 수 있어 이후 내보내기가 더 깔끔해집니다.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

시트 이름은 자유롭게 지정할 수 있습니다; “Copy”라는 이름은 복제된 범위를 담고 있음을 명확히 나타냅니다.

## Step 4: Copy the range (how to copy range) including the pivot table

이제 핵심 **범위 복사 방법** 작업을 수행합니다. `copyRange` 메서드는 값과 서식을 모두 복사하며 피벗 테이블 정의도 보존합니다.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*왜 `CopyOptions`를 사용하나요?*  
`CopyOptions` 인스턴스를 제공하면 복사할 항목(예: 수식, 열 너비)을 세밀하게 조정할 수 있습니다. 기본 생성자는 모든 것을 복사하므로 **피벗 테이블 시트 복사**와 같이 정확한 복제본이 필요할 때 이상적입니다.

## Step 5: Prepare options to export the workbook as an editable PowerPoint presentation

PowerPoint로 내보내는 작업은 `ImageOrPrintOptions`를 통해 수행됩니다. 저장 형식을 `SaveFormat.PPTX`로 설정하면 Aspose.Cells가 이미지가 아닌 PowerPoint 파일을 생성합니다.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

맞춤 레이아웃이 필요하다면 `pptOptions`를 통해 슬라이드 크기, DPI 및 기타 프레젠테이션 설정을 조정할 수 있습니다.

## Step 6: Save the workbook as a PPTX file (convert excel to pptx)

마지막으로 PPTX 옵션을 사용해 `workbook.save`를 호출합니다. 이 단계는 **Excel을 슬라이드덱으로 내보내는 방법**을 구현합니다.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

프로그램이 종료되면 `output.pptx`에 복사된 범위가 Excel과 동일하게 표시된 단일 슬라이드가 포함됩니다. 피벗 테이블 컨트롤도 그대로 유지됩니다.

### Expected output

Microsoft PowerPoint 또는 호환 뷰어에서 `output.pptx`를 열어 보세요. `A1:H20` 범위가 표시된 슬라이드가 하나 나타나며 셀 색상, 테두리, 피벗 테이블 레이아웃이 그대로 보존됩니다. 슬라이드는 완전히 편집 가능하므로 표를 이동, 크기 조정 또는 서식 변경을 자유롭게 할 수 있습니다.

## Full runnable example

모든 단계를 합치면 다음과 같은 독립 실행형 Java 클래스가 됩니다:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

IDE에서 또는 커맨드 라인에서 클래스를 실행하세요:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

파일이 작성되면 확인 메시지가 표시됩니다.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Can I copy a non‑contiguous range?** | Use `copyRange` with a named range that includes multiple areas, or call `copyRange` multiple times for each block. |
| **What if the source sheet contains multiple pivot tables?** | Each pivot table inside the copied rectangle is transferred. For tables outside the rectangle, copy them separately. |
| **How do I export multiple sheets as separate slides?** | Loop through the worksheets, copy each one to a temporary sheet, and call `workbook.save` with `pptOptions` for each iteration, appending to the same PPTX via `Presentation` API. |
| **Is the generated PPTX editable?** | Yes. The export creates native PowerPoint objects, so you can modify text, reshape tables, or add animations after the fact. |
| **What about large workbooks?** | Increase `pptOptions.setDpi(300)` for higher fidelity, but be aware of memory usage; process sheets in batches if needed. |

## Pro tips

* **Preserve column widths** – set `CopyOptions.setColumnWidth(true)` before copying if you need exact width matching.
* **Use a custom slide size** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` to match a 16:9 presentation.
* **Add a title slide** – after exporting, open the PPTX with Aspose.Slides and prepend a slide with a title and date.

## Conclusion

이제 Java를 사용해 **Excel 워크북에서 범위를 복사하는 방법**, **Excel을 PowerPoint로 내보내는 방법**, 그리고 **Excel을 PPTX로 변환하는 방법**을 알게 되었습니다. 위의 여섯 단계를 따라 하면 보고서 자동 생성, 실시간 데이터 기반 슬라이드덱 제작, 피벗 테이블 기능 유지 등을 손쉽게 구현할 수 있습니다.

### What’s next?

* **copy pivot table sheet** 변형 탐색 – 피벗 캐시만 복사하기 등
* **Aspose.Slides**와 결합해 맞춤 애니메이션이나 브랜딩 추가
* 수십 개 워크북을 정기 작업으로 배치 처리 자동화

옵션을 자유롭게 실험하고 코드를 자체 보고 파이프라인에 맞게 조정해 보세요. 문제가 발생하면 Aspose.Cells for Java 문서에서 `CopyOptions`와 `ImageOrPrintOptions`에 대한 자세한 정보를 확인할 수 있습니다. Happy coding!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하는 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하도록 돕습니다.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}