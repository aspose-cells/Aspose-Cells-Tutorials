---
category: general
date: 2026-06-08
description: Aspose를 사용하여 XLSX를 PPTX로 변환하고 도형을 편집 가능하게 유지하는 방법을 배웁니다. 단계별 Java 코드를
  통해 도형을 편집 가능성을 잃지 않고 내보내는 방법을 보여줍니다.
draft: false
keywords:
- convert xlsx to pptx
- how to export shapes
- how to keep shapes
- aspose export pptx
language: ko
og_description: XLSX를 PPTX로 변환하면서 도형 편집 가능성을 유지합니다. 이 가이드는 Java 코드를 단계별로 안내하고 Aspose를
  사용하여 도형을 유지하는 방법을 설명합니다.
og_title: XLSX를 PPTX로 변환 – Aspose로 편집 가능한 도형 내보내기
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  headline: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  type: TechArticle
- description: Learn how to convert XLSX to PPTX and keep shapes editable using Aspose.
    Step‑by‑step Java code shows how to export shapes without losing editability.
  name: Convert XLSX to PPTX – Complete Guide to Export Editable Shapes
  steps:
  - name: Expected Output
    text: '- A PowerPoint file named `editable.pptx` located in the directory you
      specified. - Each worksheet appears as a separate slide. - All shapes (text
      boxes, arrows, charts) remain fully editable, just as they were in Excel.'
  - name: 1. Shapes Turn Into Images
    text: '> **Symptom:** After conversion, clicking a shape shows no resize handles.'
  - name: 2. Missing Slides for Some Worksheets
    text: '> **Symptom:** Only the first sheet appears in the PPTX.'
  - name: 3. File Not Found Exceptions
    text: '> **Symptom:** Java throws `FileNotFoundException` for the source Excel.'
  - name: Wrap‑Up
    text: We’ve walked through the entire process of **convert xlsx to pptx**, showing
      exactly **how to export shapes** and **how to keep shapes** editable using the
      Aspose API. The complete Java program is ready to drop into any Maven project,
      and the optional tweaks let you tailor the conversion to your exa
  type: HowTo
- questions:
  - answer: Yes, you could use OpenXML SDK, but you’d lose the high‑level shape preservation
      that Aspose handles automatically.
    question: Can I convert XLSX to PPTX without Aspose?
  - answer: The conversion strips out VBA; only visual elements are transferred. If
      you need macro logic in PowerPoint, you’ll have to recreate it manually.
    question: Does this work with macros or VBA code inside the workbook?
  - answer: Aspose processes them efficiently, but memory usage can spike. Consider
      converting sheet‑by‑sheet or increasing the JVM heap (`-Xmx2g`).
    question: What about large workbooks with hundreds of shapes?
  type: FAQPage
tags:
- Aspose.Cells
- Aspose.Slides
- Java
- File Conversion
title: XLSX를 PPTX로 변환 – 편집 가능한 도형 내보내기 완전 가이드
url: /ko/java/excel-import-export/convert-xlsx-to-pptx-complete-guide-to-export-editable-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# XLSX를 PPTX로 변환 – 편집 가능한 도형 내보내기 완전 가이드

아름다운 차트와 다이어그램을 평면 이미지로 바꾸지 않고 **XLSX를 PPTX로 변환**하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 수신자가 도형을 조정하고, 텍스트 상자의 크기를 변경하거나, 연결선을 수정할 수 있는 PowerPoint 파일이 필요할 때 난관에 부딪히곤 합니다. 좋은 소식은? Aspose가 이 과정을 손쉽게 만들어 주며, 이번 튜토리얼에서는 **도형을 내보내는 방법**과 **변환 중 도형을 편집 가능하게 유지하는 방법**을 정확히 보여드립니다.

실제 Java 예제를 통해 Excel 워크북을 로드하고, 올바른 옵션을 토글한 뒤, 바로 PowerPoint에서 열어 편집할 수 있는 PPTX 파일을 작성하는 과정을 단계별로 안내합니다. 끝까지 읽으면 *어떤 메서드를 호출해야 하는지*뿐만 아니라 *각 설정이 왜 중요한지*를 이해하고, 일반적인 함정을 피할 수 있는 팁도 얻을 수 있습니다.

## Prerequisites – 시작하기 전에 준비할 것

코드 작성을 시작하기 전에 아래 항목들이 머신에 준비되어 있는지 확인하세요:

- **Java Development Kit (JDK) 8 또는 최신 버전** – 코드는 최신 JDK와 호환됩니다.
- **Aspose.Cells for Java**와 **Aspose.Slides for Java** JAR 파일 – Aspose Maven 저장소에서 가져오거나 Aspose 웹사이트에서 최신 버전을 다운로드할 수 있습니다.
- **Excel 파일 (`shapes.xlsx`)** – 보존하려는 도형이 포함된 파일. 몇 개의 그린 객체만 있는 간단한 워크북이면 테스트에 충분합니다.
- 선호하는 IDE (IntelliJ IDEA, Eclipse, VS Code…) 혹은 일반 텍스트 편집기와 터미널.

이 중 익숙하지 않은 것이 있더라도 걱정하지 마세요. JAR 파일 설치는 `pom.xml`에 두 개의 의존성을 추가하는 것만큼 쉽습니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-slides</artifactId>
    <version>23.12</version>
</dependency>
```

이제 기본 사항을 살펴보았으니, 실제로 손을 더럽혀 보겠습니다.

## Step 1: Load the Excel Workbook Containing the Shapes

도형이 들어 있는 `.xlsx` 파일을 읽는 것이 첫 번째 작업입니다. Aspose.Cells는 저수준 OpenXML 세부 사항을 추상화하므로, `Workbook`을 단순히 인스턴스화하면 됩니다.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the source workbook – replace the path with your actual file location
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // From here on we can manipulate the workbook or pass it straight to Slides
```

> **Why this matters:** 워크북을 올바르게 로드하면 임베드된 차트, SmartArt, 자유형 도형 등 모든 그리기 객체가 네이티브 Aspose 객체로 메모리에 유지됩니다. 이 단계를 건너뛰거나 일반 파일 스트림을 사용하면 변환 엔진이 시트를 정적 이미지로 처리해 편집 가능성을 잃게 됩니다.

## Step 2: Tell Aspose to Keep Shapes Editable

Aspose.Slides는 `setSaveEditableShape` 라는 플래그를 제공합니다. 이를 `true` 로 설정하면 라이브러리가 도형 데이터를 래스터화하지 않고 원본 형태로 보존합니다. 이것이 바로 **도형을 유지하는 방법**에 해당합니다.

```java
        // Create save options for PPTX output
        ImageOrPrintOptions pptxSaveOptions = new ImageOrPrintOptions();

        // Enable editable shape preservation – this is the key switch
        pptxSaveOptions.setSaveEditableShape(true);
```

> **Pro tip:** `SaveEditableShape`의 기본값은 `false` 입니다. 이 옵션을 활성화하지 않으면 개발자들이 평면 이미지로 가득 찬 PPTX를 얻게 되는 가장 흔한 원인입니다. 출력 파일이 “붙어 있는” 것처럼 보이면 이 라인을 다시 확인하세요.

## Step 3: Convert and Save the Workbook as PPTX

이제 `save` 메서드를 호출하고 `SaveFormat.PPTX` 열거형과 커스텀 옵션을 전달합니다. 이것이 **convert xlsx to pptx**의 핵심 부분입니다.

```java
        // Save the workbook as a PPTX file with editable shapes preserved
        workbook.save("YOUR_DIRECTORY/editable.pptx", SaveFormat.PPTX, pptxSaveOptions);
    }
}
```

프로그램을 실행하면 Aspose가 Excel 시트를 읽어 각 워크시트를 슬라이드로 변환하고 `editable.pptx` 파일을 작성합니다. PowerPoint에서 해당 파일을 열면 원본 도형이 그대로 유지된 것을 확인할 수 있으며, 바로 이동·색상 변경·크기 조정이 가능합니다.

### Expected Output

- 지정한 디렉터리에 `editable.pptx` 라는 이름의 PowerPoint 파일이 생성됩니다.
- 각 워크시트가 별개의 슬라이드로 나타납니다.
- 모든 도형(텍스트 상자, 화살표, 차트)이 Excel에 있던 그대로 완전히 편집 가능하게 유지됩니다.

PPTX를 열어 도형을 편집하려고 하면 PowerPoint에서 새로 도형을 만들 때와 동일한 핸들이 표시됩니다.

## Common Pitfalls and How to Avoid Them

### 1. Shapes Turn Into Images

> **Symptom:** 변환 후 도형을 클릭해도 크기 조절 핸들이 나타나지 않습니다.

**Cause:** `setSaveEditableShape(false)`(기본값) 이 설정되어 있거나, 해당 플래그를 지원하지 않는 오래된 Aspose 버전을 사용하고 있습니다.

**Fix:** `save` 호출 **이전**에 `pptxSaveOptions.setSaveEditableShape(true);` 를 반드시 호출하고, Aspose.Cells/Slides 23.x 이상인지 확인하세요.

### 2. Missing Slides for Some Worksheets

> **Symptom:** PPTX에 첫 번째 시트만 나타납니다.

**Cause:** 워크북이 숨겨진 워크시트와 함께 저장되었거나, `SaveOptions`가 잘못 구성되었습니다.

**Fix:** `workbook.getWorksheets().setVisible(true);` 로 모든 시트를 보이게 하거나, 암호가 설정된 파일을 로드할 경우 `LoadOptions`를 조정하세요.

### 3. File Not Found Exceptions

> **Symptom:** Java가 소스 Excel에 대해 `FileNotFoundException`을 발생시킵니다.

**Cause:** 경로가 잘못되었거나 파일 권한이 부족합니다.

**Fix:** 절대 경로를 사용하거나 파일을 프로젝트의 `resources` 폴더에 두고 `getClass().getResourceAsStream("/shapes.xlsx")` 로 로드하세요.

## Advanced: Converting Specific Sheets Only

전체 워크북이 필요하지 않을 때도 있습니다—예를 들어 “Dashboard” 시트만 슬라이드로 만들고 싶을 때가죠. 간단히 다음과 같이 수정하면 됩니다:

```java
        // Create a new workbook that contains only the desired sheet
        Workbook source = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        int sheetIndex = source.getWorksheets().get("Dashboard").getIndex();

        // Clone the target sheet into a fresh workbook
        Workbook singleSheet = new Workbook();
        singleSheet.getWorksheets().addCopy(source.getWorksheets().get(sheetIndex));

        // Save the single‑sheet workbook as PPTX
        singleSheet.save("YOUR_DIRECTORY/dashboard.pptx", SaveFormat.PPTX, pptxSaveOptions);
```

이 스니펫은 단일 워크시트에서 **도형을 내보내는 방법**을 보여 주면서도 편집 가능성을 유지합니다.

## Step‑by‑Step Recap (Quick Reference)

| 단계 | 작업 | 핵심 API |
|------|------|----------|
| 1 | `.xlsx` 로드 | `new Workbook(path)` |
| 2 | 편집 가능한 도형 활성화 | `pptxSaveOptions.setSaveEditableShape(true)` |
| 3 | PPTX로 저장 | `workbook.save(pptPath, SaveFormat.PPTX, pptxSaveOptions)` |

이 표를 손에 두면 나중에 코드를 다시 볼 때 몇 번의 클릭만으로도 작업을 재현할 수 있습니다.

## Testing the Result

프로그램을 실행한 뒤 PowerPoint에서 `editable.pptx` 파일을 열고:

1. 아무 도형이나 클릭 – 일반적인 경계 상자가 표시되어야 합니다.  
2. 채우기 색상을 변경 – 즉시 업데이트됩니다.  
3. 도형을 새로운 위치로 이동 – PowerPoint가 새로운 좌표를 유지합니다.

세 가지 동작이 모두 정상 작동한다면 **convert xlsx to pptx**를 성공적으로 수행하면서 도형을 편집 가능하게 만든 것입니다. 뭔가 이상하다면 `setSaveEditableShape` 플래그를 다시 확인하고 Aspose 버전을 재검토하세요.

## Frequently Asked Questions

- **Can I convert XLSX to PPTX without Aspose?**  
  네, OpenXML SDK를 사용할 수 있지만 Aspose가 자동으로 제공하는 고수준 도형 보존 기능은 손실됩니다.

- **Does this work with macros or VBA code inside the workbook?**  
  변환 과정에서 VBA는 제거됩니다; 시각적 요소만 전송됩니다. PowerPoint에 매크로 로직이 필요하면 직접 재구성해야 합니다.

- **What about large workbooks with hundreds of shapes?**  
  Aspose는 효율적으로 처리하지만 메모리 사용량이 급증할 수 있습니다. 시트별로 변환하거나 JVM 힙(`-Xmx2g`)을 늘리는 것을 고려하세요.

## Next Steps – Take Your Conversion Skills Further

이제 **convert xlsx to pptx**를 편집 가능한 객체와 함께 마스터했으니, 다음과 같은 주제를 탐색해 보세요:

- **Embedding videos or audio** using Aspose.Slides’ media APIs.  
- **Applying slide themes** programmatically to give the deck a uniform look.  
- **Batch converting multiple workbooks** with a simple loop—perfect for automated reporting pipelines.  
- **Exporting to other formats** like PDF or HTML while still preserving shape data (`SaveFormat.PDF` with similar options).

위 주제들은 모두 이번에 다룬 핵심 개념을 기반으로 하므로 학습 곡선이 완만합니다.

---

![xlsx를 pptx로 변환 다이어그램](image.png "Excel 시트 → Aspose 변환 → 편집 가능한 PPTX를 보여주는 다이어그램")

*이미지 대체 텍스트: “xlsx를 pptx로 변환 워크플로우 다이어그램”*

### Wrap‑Up

우리는 **convert xlsx to pptx** 전체 과정을 차근차근 살펴보면서 **도형을 내보내는 방법**과 **도형을 편집 가능하게 유지하는 방법**을 Aspose API를 통해 정확히 보여드렸습니다. 완전한 Java 프로그램은 어떤 Maven 프로젝트에도 바로 삽입할 수 있으며, 선택적인 트윅을 통해 변환을 정확히 원하는 대로 맞출 수 있습니다. 직접 실행해 보고 다양한 시트를 실험해 보세요. 무거운 작업은 Aspose가 대신 처리해 줍니다.

문제가 발생하면 최신 `ImageOrPrintOptions` 속성을 확인하거나 아래에 댓글을 남겨 주세요. 즐거운 코딩 되시고, Excel에서 바로 생성된 편집 가능한 PowerPoint 덱의 자유를 만끽하시기 바랍니다!

## What Should You Learn Next?

다음 튜토리얼들은 이번 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 다양한 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells를 사용한 Java에서 Excel을 PDF로 변환하는 방법: 단계별 가이드](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Aspose.Cells를 사용한 Java에서 SmartArt를 그룹 도형으로 변환하기: 종합 가이드](/cells/english/java/images-shapes/convert-smartart-group-shapes-java/)
- [Aspose.Cells Java를 사용하여 Excel에 도형 추가 및 스타일링하는 방법](/cells/english/java/images-shapes/aspose-cells-java-add-styling-shapes-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}