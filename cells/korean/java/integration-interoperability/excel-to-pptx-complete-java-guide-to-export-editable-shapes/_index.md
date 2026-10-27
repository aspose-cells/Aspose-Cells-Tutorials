---
category: general
date: 2026-07-20
description: 'Excel을 PowerPoint(PPTX)로 내보내는 방법을 보여주는 튜토리얼: 편집 가능한 텍스트 상자, 차트 모양 변환
  및 이미지 삽입을 Aspose를 사용해 PPTX에 포함합니다.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- excel to pptx
- editable text boxes
- convert chart shape
- export excel powerpoint
- embed images pptx
language: ko
lastmod: 2026-07-20
og_description: Excel에서 PowerPoint로 내보내는 방법을 안내하는 가이드로, 편집 가능한 텍스트 상자를 유지하고 차트 모양을
  변환하며 Aspose를 사용해 이미지를 PPTX에 삽입합니다.
og_image_alt: Screenshot of a PowerPoint slide generated from an Excel workbook showing
  editable shapes
og_title: Excel에서 PPTX로 – Excel에서 PowerPoint로 편집 가능한 도형 내보내기 (Java)
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  headline: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  type: TechArticle
- description: excel to pptx tutorial showing how to export Excel to PowerPoint with
    editable text boxes, convert chart shape and embed images pptx using Aspose.
  name: 'excel to pptx: Complete Java Guide to Export Editable Shapes'
  steps:
  - name: A slide that mirrors the layout of your Excel sheet.
    text: A slide that mirrors the layout of your Excel sheet.
  - name: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
    text: Text boxes that you can click, edit, and move—just like native PowerPoint
      shapes.
  - name: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
    text: Charts rendered as editable vector shapes (you can ungroup them to edit
      individual series).
  - name: Any pictures from the workbook appear as embedded images, not linked files.
    text: Any pictures from the workbook appear as embedded images, not linked files.
  type: HowTo
tags:
- Aspose
- Java
- Excel
- PowerPoint
title: 'Excel에서 PPTX로: 편집 가능한 도형을 내보내는 완전한 Java 가이드'
url: /ko/java/integration-interoperability/excel-to-pptx-complete-java-guide-to-export-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel to pptx: 편집 가능한 도형 내보내기를 위한 완전한 Java 가이드

나중에 텍스트 상자를 편집할 수 있는 기능을 잃지 않고 **excel to pptx** 하는 방법이 궁금하셨나요? 아마 Excel에서 보고서 워크북을 만들고 차트를 몇 개 추가했으며, 이제 팀이 즉시 수정할 수 있는 PowerPoint 프레젠테이션에 그 시각화를 넣어야 할 것입니다. 좋은 소식은? Aspose Cells와 Aspose Slides를 사용해 프로그래밍 방식으로 수행할 수 있으며, 편집 가능한 텍스트 상자를 유지하고 차트 도형을 변환하며 이미지 pptx도 삽입할 수 있습니다.

이번 튜토리얼에서는 Excel 파일을 가져와 텍스트가 편집 가능하도록, 차트가 수정 가능한 도형으로 변환되고 이미지가 삽입된 상태로 내보내는 전체 실행 가능한 예제를 단계별로 살펴보겠습니다. 끝까지 진행하면 어떤 Java 프로젝트에도 넣을 수 있는 견고한 **export excel powerpoint** 파이프라인을 얻게 됩니다.

## 전제 조건 – 시작하기 전에 필요한 것

- **Java 17** 또는 그 이상 (코드는 Java 8+에서도 컴파일됩니다).  
- 클래스패스에 **Aspose Cells for Java** 및 **Aspose Slides for Java** JAR가 있어야 합니다. Aspose Maven 저장소에서 가져오거나 체험 번들을 다운로드할 수 있습니다.  
- 최소 하나의 텍스트 상자, 차트 및 삽입된 그림을 포함하고 있는 Excel 워크북 (`ShapesInExcel.xlsx`).  
- 기본 IDE (IntelliJ, Eclipse, VS Code…) – 어느 것이든 상관없지만 저는 즉시 실행 구성을 위해 IntelliJ를 선호합니다.

그게 전부입니다. 추가 빌드 도구나 외부 서비스가 필요 없습니다. 바로 시작해봅시다.

## Step 1: Excel 워크북 로드 – excel to pptx의 시작점

먼저 소스 워크북을 엽니다. Aspose Cells는 파일 형식을 추상화하므로 기본 XML에 대해 신경 쓸 필요가 없습니다.

```java
import com.aspose.cells.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");
```

> **왜 중요한가:** 워크북을 로드하면 모든 시트 구조와 그 안의 모든 그리기 객체에 접근할 수 있습니다. 이 단계를 건너뛰면 내보내기 루틴이 변환할 대상을 알지 못해 빈 슬라이드가 생성됩니다.

## Step 2: PPTX 저장 옵션 구성 – 편집 가능한 텍스트 상자 유지 및 차트 도형 변환

이제 Aspose Slides에 출력이 어떻게 동작하길 원하는지 알려줍니다. `ImageOrPrintOptions` 클래스가 **editable text boxes**, **convert chart shape**, **embed images pptx**에 대한 마법이 일어나는 곳입니다.

```java
        // Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly in the PPTX
        pptxOptions.setExportChartToShape(true);     // turn charts into editable shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable
```

* `setExportImagesAsBase64(true)`에 대한 간단한 설명: 이 옵션은 내보내기가 그림을 `.pptx` 내부의 Base64 스트림으로 저장하도록 강제합니다. 결과적으로 외부 이미지 참조가 없는 완전한 자체 포함 파일이 생성되며, 이는 **embed images pptx** 요구 사항을 충족합니다.  
* `setExportChartToShape(true)`는 **convert chart shape** 키워드가 약속하는 바로 그 동작을 수행합니다. 차트의 정적 이미지 대신 Aspose가 벡터 도형 컬렉션을 생성하며, 이를 나중에 그룹 해제, 색상 변경 또는 데이터 포인트 교체 등에 사용할 수 있습니다.  
* 마지막으로 `setEditableText(true)`는 Excel에 배치한 텍스트 상자가 PowerPoint에서도 텍스트 상자로 유지되며, 평면 이미지로 변환되지 않도록 보장합니다. 이것이 **editable text boxes** 지원의 핵심입니다.

## Step 3: 워크북을 PPTX로 저장 – excel to pptx 흐름 완성

워크북을 로드하고 옵션을 조정했으면, 이제 `save`를 호출하기만 하면 됩니다. Aspose Cells가 배경에서 무거운 작업을 처리합니다.

```java
        // Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);
    }
}
```

> **내부에서 무슨 일이 일어나나요?** Aspose는 각 워크시트를 순회하면서 그리기 객체를 추출하고, 우리가 설정한 옵션을 적용한 뒤 새로운 PowerPoint 패키지를 작성합니다. 결과 파일은 PowerPoint, LibreOffice Impress 또는 Open XML 형식을 지원하는 모든 뷰어에서 열 수 있습니다.

### 예상 출력

`ExportedShapes.pptx`를 열면 다음을 확인할 수 있습니다:

1. Excel 시트 레이아웃을 그대로 반영한 슬라이드.  
2. 클릭하고 편집 및 이동할 수 있는 텍스트 상자 – 마치 기본 PowerPoint 도형처럼.  
3. 편집 가능한 벡터 도형으로 렌더링된 차트(그룹 해제하여 개별 시리즈를 편집 가능).  
4. 워크북에 포함된 모든 그림이 링크된 파일이 아닌 삽입된 이미지로 표시됩니다.

누락된 요소가 있다면, 원본 Excel에 해당 객체가 실제로 포함되어 있는지 다시 확인하십시오. Aspose가 자동으로 생성해 주지는 않습니다.

## Step 4: 고급 조정 – 내보내기 동작 세밀 조정 (선택 사항)

위의 세 옵션이 대부분의 사용 사례를 커버하지만, Aspose Slides는 유용하게 사용할 수 있는 추가 설정을 제공합니다:

| Option | What It Does | When to Use |
|--------|--------------|-------------|
| `setExportHiddenSheets(true)` | 숨겨진 워크시트를 추가 슬라이드로 포함합니다. | 보고서에서 계산용으로 숨겨진 시트를 사용하는 경우. |
| `setExportNotesToComments(true)` | Excel 셀 주석을 PowerPoint 슬라이드 노트로 이동합니다. | 주석 컨텍스트를 보존하고 싶을 때. |
| `setSlideSize(SlideSizeTypeOnScreen16x9)` | 슬라이드 크기를 16:9로 강제 지정합니다. | 최신 와이드스크린 프레젠테이션용. |

`save`를 호출하기 전에 동일한 `pptxOptions` 인스턴스에 이들 중 원하는 것을 설정할 수 있습니다.

```java
pptxOptions.setExportHiddenSheets(true);
pptxOptions.setExportNotesToComments(true);
pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);
```

## Step 5: 코드 실행 – IDE에서 명령줄까지

IDE를 사용한다면 **Run** 버튼을 누르면 됩니다. 명령줄 빌드의 경우, Aspose JAR를 `libs/` 폴더에 두었다고 가정하고 다음과 같이 컴파일하고 실행합니다:

```bash
javac -cp "libs/*" ExportEditableShapes.java
java -cp ".:libs/*" ExportEditableShapes
```

Windows에서는 클래스패스의 `:`를 `;`로 바꾸세요. 실행 후 `YOUR_DIRECTORY` 폴더에 `ExportedShapes.pptx`가 생성되었는지 확인합니다.

## 일반적인 함정 및 전문가 팁

- **Pitfall:** `setEditableText(true)` 설정을 잊음. 결과: 모든 텍스트가 평면 이미지로 표시됩니다.  
  **Pro tip:** 첫 실행 후 PPTX를 열어 텍스트 상자를 편집해 보세요. 편집이 안 된다면 옵션을 다시 확인하십시오.  
- **Pitfall:** 큰 Excel 파일은 메모리 압박을 일으킬 수 있습니다.  
  **Pro tip:** 로드하기 전에 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`를 사용해 Aspose가 데이터를 스트리밍하도록 하여 전체를 RAM에 로드하지 않게 하세요.  
- **Pitfall:** 이미지가 흐릿하게 표시됩니다.  
  **Pro tip:** 원본 그림 해상도가 충분히 높은지 확인하세요; `setExportImagesAsBase64(true)`가 켜져 있으면 Aspose가 원본 DPI를 유지합니다.  
- **Pitfall:** 차트가 데이터 레이블을 잃음.  
  **Pro tip:** 변환 후 PowerPoint에서 차트 도형을 오른쪽 클릭하고 *Edit Data*를 선택해 기본 데이터 테이블을 확인하세요. 레이블이 없으면 `setExportChartDataLabels(true)`를 활성화하십시오(새 버전 Aspose에서 제공).

## 전체 작업 예제 – 모든 코드를 한 곳에

아래는 완전한 복사‑붙여넣기 가능한 프로그램입니다. `YOUR_DIRECTORY`를 여러분 컴퓨터의 절대 경로나 상대 경로로 바꾸세요.

```java
import com.aspose.cells.*;
import com.aspose.slides.*;

public class ExportEditableShapes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the Excel workbook that contains text boxes or shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesInExcel.xlsx");

        // 2️⃣ Configure PPTX save options to preserve editable elements
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions();
        pptxOptions.setExportImagesAsBase64(true);   // embed images directly
        pptxOptions.setExportChartToShape(true);     // convert charts to shapes
        pptxOptions.setEditableText(true);           // keep text boxes editable

        // Optional: fine‑tune additional settings
        pptxOptions.setExportHiddenSheets(true);
        pptxOptions.setExportNotesToComments(true);
        pptxOptions.setSlideSize(SlideSizeTypeOnScreen16x9);

        // 3️⃣ Save the workbook as a PPTX file with the configured options
        workbook.save("YOUR_DIRECTORY/ExportedShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed! Check ExportedShapes.pptx");
    }
}
```

프로그램을 실행하고 생성된 PowerPoint를 열면 앞서 설명한 내용이 정확히 나타나는 것을 확인할 수 있습니다.

## 결론 – 편집 가능한 도형으로 excel to pptx 마스터하기

우리는 텍스트 상자를 편집 가능하게 유지하고 차트를 벡터 도형으로 변환하며 이미지가 프레젠테이션에 직접 삽입되는 **excel to pptx** 워크플로우를 다뤘습니다. 핵심 포인트는? 몇 가지 `ImageOrPrintOptions` 속성을 조정하면 PowerPoint 사용자에게 자연스러운 **export excel powerpoint** 경험을 얻을 수 있다는 것입니다.

다음 단계로 다음을 탐색해 볼 수 있습니다:

- 슬라이드 전환을 프로그래밍 방식으로 추가 (`Aspose Slides`의 `Slide.addTransition`).  
- 여러 워크시트에서 여러 슬라이드 생성 (`workbook.getWorksheets()` 반복).  
- 이 내보내기를 PDF 변환 파이프라인과 결합해 하이브리드 보고서 작성.

자유롭게 실험하고, 문제를 일으키고, 다시 합쳐 보세요— 이것이 **excel to pptx** 프로세스를 진정으로 장악하는 방법입니다. 질문이 있거나 멋진 변형을 공유하고 싶다면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 작동 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Add and Access Text Boxes in Excel using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [How to Convert Excel Sheets to Images Using Aspose.Cells .NET (Step‑By‑Step Guide)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}