---
category: general
date: 2026-09-21
description: Aspose.Cells for Java를 사용하여 Excel을 PowerPoint로 변환 – 차트를 PPTX로 내보내고 워크북을
  PPTX로 저장하는 방법을 몇 줄의 코드만으로 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: ko
lastmod: 2026-09-21
og_description: Java에서 Aspose.Cells를 사용하여 Excel을 PowerPoint로 변환합니다. 이 튜토리얼에서는 차트를
  PPTX로 내보내고 편집 가능한 텍스트 상자가 포함된 워크북을 PPTX로 저장하는 방법을 보여줍니다.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Aspose.Cells를 사용하여 Excel을 PowerPoint로 변환 – Java 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Java에서 Aspose.Cells를 사용하여 Excel을 PowerPoint로 변환
url: /ko/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용한 Java에서 Excel을 PowerPoint로 변환하기

Excel을 PowerPoint로 **변환**해야 하는 경우, 이 가이드는 간결하고 프로덕션에 적합한 방법을 보여줍니다. 차트를 PPTX로 내보내고, 텍스트 상자를 편집 가능하게 유지하며, **save workbook as PPTX**를 Java 코드 세 줄만으로 수행하는 방법을 확인할 수 있습니다.

많은 개발자가 데이터를 PDF로 내보내지만, 실시간 차트와 편집 가능한 요소가 필요한 프레젠테이션에는 PowerPoint가 더 적합한 경우가 많습니다. 이 튜토리얼은 프로젝트 설정부터 일반적인 함정 처리까지 필요한 모든 내용을 다루므로, Java IDE를 떠나지 않고도 Excel 차트에서 PowerPoint를 만들 수 있습니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* Java 17 이상이 설치되어 있어야 합니다.
* Maven(또는 Gradle)으로 종속성을 관리합니다.
* Aspose.Cells for Java 라이선스(무료 체험판으로 평가 가능)  
* 최소 하나의 차트와 텍스트 상자를 포함한 Excel 파일(`ChartAndTextbox.xlsx`)

## 1단계: 프로젝트에 Aspose.Cells 추가하기

첫 번째 단계는 Aspose.Cells 라이브러리를 포함하는 것입니다. Maven을 사용한다면 `pom.xml`에 다음 종속성을 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Gradle을 사용하는 경우, 동등한 코드는 다음과 같습니다:  
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

라이브러리를 포함하면 변환에 필요한 `Workbook`, `PdfSaveOptions`, `SaveFormat` 열거형에 접근할 수 있습니다.

## 2단계: 차트와 텍스트 상자를 포함한 워크북 로드하기

이제 Excel 파일을 로드합니다. `Workbook` 클래스는 차트, 수식, 텍스트 상자를 보존하면서 전체 워크북을 메모리로 읽어들입니다.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**왜 중요한가:** 워크북을 먼저 로드하면 모든 임베디드 객체(차트, 이미지, 텍스트 상자)가 내보내기 과정에서 사용 가능해집니다. 파일을 찾을 수 없을 경우 Aspose.Cells는 명확한 `FileNotFoundException`을 발생시키며, 이를 잡아 사용자에게 친절한 메시지를 표시할 수 있습니다.

## 3단계: 텍스트 상자를 편집 가능하도록 내보내기 옵션 구성하기

Aspose.Cells는 대상 형식이 PowerPoint일 때 객체가 어떻게 기록되는지를 제어하기 위해 `PdfSaveOptions`를 사용합니다. `setExportEditableTextBoxes(true)`를 활성화하면 Excel 시트의 모든 텍스트 상자가 변환 후에도 편집 가능하게 유지됩니다.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **왜 `PdfSaveOptions`를 PPTX에 사용하는가?**  
> 내부적으로 Aspose.Cells는 PDF 렌더링 파이프라인을 재사용해 PowerPoint 출력을 생성하므로, 편집 가능한 요소에 대한 세밀한 제어가 가능합니다. 이 플래그를 설정하는 것이 텍스트 상자 편집 가능성을 보존하는 권장 방법입니다.

## 4단계: 워크북을 PowerPoint 프레젠테이션으로 저장하기

마지막으로 `SaveFormat.PPTX`와 함께 `workbook.save`를 호출합니다. 이 단계가 **create PowerPoint from Excel chart** 워크플로를 완성합니다.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

전체 코드는 다음과 같습니다:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 예상 출력

프로그램을 실행하면 다음과 같이 출력됩니다:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

`Result.pptx`를 Microsoft PowerPoint에서 열면 다음을 확인할 수 있습니다:

* 원본 Excel 차트가 네이티브 PowerPoint 차트로 렌더링되어 PowerPoint 차트 편집기에서 편집 가능함.
* Excel의 텍스트 상자가 편집 가능한 도형으로 나타나 슬라이드에서 직접 텍스트를 변경할 수 있음.

## 일반적인 경계 상황 처리

| Situation | Recommended approach |
|-----------|----------------------|
| **File not found** | `Workbook` 생성자를 `try‑catch` 블록으로 감싸고 명확한 메시지를 표시합니다. |
| **Workbook has no chart** | 변환 전에 `worksheet.getCharts().getCount() > 0`을 확인하여 차트가 없으면 해당 단계를 건너뛰거나 자리표시자를 추가합니다. |
| **Large Excel files** | 렌더링 중 `OutOfMemoryError`를 방지하기 위해 JVM 힙 크기(`-Xmx2g`)를 늘립니다. |
| **License not set** | 워크북을 로드하기 전에 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`를 호출해 평가 워터마크를 제거합니다. |

## 자주 묻는 질문

**Q: 여러 워크시트를 별도의 PowerPoint 슬라이드로 변환할 수 있나요?**  
A: 가능합니다. 각 워크시트를 순회하면서 `PdfSaveOptions`를 사용해 차트를 새 슬라이드로 내보낸 뒤, 모든 시트를 처리한 후 한 번만 워크북을 저장합니다.

**Q: 이 방법이 셀 서식을 보존하나요?**  
A: 차트와 텍스트 상자 객체만 PowerPoint로 전송됩니다. 셀 서식은 Excel 파일에 남아 있으며 PPTX에는 나타나지 않습니다.

**Q: PPTX 대신 PDF로 내보내야 하면 어떻게 하나요?**  
A: `SaveFormat.PDF`와 동일한 `PdfSaveOptions`를 사용하면 됩니다. `setExportEditableTextBoxes` 플래그는 PDF에서도 동작합니다.

## 다음 단계

이제 **save workbook as PPTX**와 **export chart to PPTX** 방법을 알았으니 다음을 탐색해 보세요:

* 여러 차트를 서로 다른 슬라이드에 추가하기(`create powerpoint from excel chart`를 루프와 함께 사용).
* Aspose.Slides for Java를 활용해 슬라이드 레이아웃을 맞춤 설정하고 프레젠테이션 스타일을 풍부하게 만들기.
* `Picture` 클래스를 사용해 Excel 셀의 이미지를 PowerPoint에 삽입하기.

이러한 확장을 통해 Excel 데이터에서 직접 다듬어진 프레젠테이션을 자동으로 생성하는 완전 자동화 보고 파이프라인을 구축할 수 있습니다.

---

**Summary:** 이 튜토리얼은 Aspose.Cells for Java를 사용해 **Excel을 PowerPoint로 변환**하는 신뢰할 수 있는 방법을 보여줍니다. 워크북을 로드하고, 텍스트 상자를 편집 가능하게 유지하도록 `PdfSaveOptions`를 구성한 뒤, `SaveFormat.PPTX`로 저장하면 실시간 차트와 편집 가능한 도형이 포함된 PowerPoint 파일을 얻을 수 있습니다—동적인 비즈니스 프레젠테이션에 최적입니다. 배치 처리에 코드를 적용하거나 더 큰 보고 솔루션에 통합해 보세요.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for Java를 사용해 트렌드라인이 포함된 Excel 차트를 만들고 이미지를 내보내는 방법](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells in Java를 사용해 Excel 차트를 SVG로 변환하는 방법](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells&#58; 단계별 가이드를 통해 Java에서 Excel을 PDF로 변환하는 방법](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}