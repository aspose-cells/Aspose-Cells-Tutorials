---
category: general
date: 2026-10-01
description: Java에서 ShapeExportOptions를 사용하여 도형을 내보내는 방법을 배우고, Aspose.Cells를 사용해 PPTX로
  변환할 때 도형을 편집 가능하게 유지하세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: ko
lastmod: 2026-10-01
og_description: Java에서 ShapeExportOptions를 사용하여 도형을 내보내 편집 가능한 PPTX 파일을 생성합니다. 이 튜토리얼은
  Aspose.Cells를 활용한 전체 과정을 단계별로 안내합니다.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Java에서 ShapeExportOptions를 사용한 도형 내보내기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Java에서 ShapeExportOptions를 사용하여 도형 내보내는 방법
url: /ko/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 ShapeExportOptions를 사용하여 도형 내보내기

Excel 워크북에서 **ShapeExportOptions를 사용하여 도형을 내보내야** 할 경우, 이 가이드는 정확한 단계들을 보여줍니다. PPTX 파일로 변환할 때 도형을 편집 가능하게 유지하는 방법을 확인할 수 있으며, 이는 PowerPoint에서의 후속 편집에 필수적입니다.

스프레드시트에서 슬라이드 덱을 생성할 때 도형을 내보내는 작업은 흔히 발생합니다—예를 들어 영업 프레젠테이션, 보고서 대시보드, 자동화된 프레젠테이션을 만들 때 말이죠. 이 튜토리얼은 프로젝트 설정부터 내보낸 파일 확인까지 필요한 모든 내용을 다루며, **Aspose.Cells for Java** 라이브러리를 사용합니다.

## 준비 사항

시작하기 전에 다음을 준비하세요:

- Java 17 이상 (코드는 최신 JDK와 호환됩니다)
- Maven 또는 Gradle (의존성 관리용)
- 최소 하나의 텍스트 상자 또는 기타 도형이 포함된 Excel 파일 (`Shapes.xlsx`)
- Aspose.Cells API에 대한 기본적인 이해

## 1단계: 프로젝트에 Aspose.Cells 추가하기 (Aspose Cells export shape)

Maven을 사용하는 경우 `pom.xml`에 다음 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Gradle을 사용하는 경우 `build.gradle`에 다음을 넣으세요:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** 라이선스를 미리 등록해 두면 평가판 워터마크를 피할 수 있습니다.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## 2단계: 도형이 포함된 워크북 로드하기

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

`Workbook` 객체는 전체 Excel 파일을 나타냅니다. 이를 로드하는 것이 모든 도형 조작의 첫 번째 전제 조건입니다.

## 3단계: 워크시트를 접근하고 원하는 도형 가져오기 (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Why this matters:** 도형은 워크시트별로 저장되므로, 특정 도형을 내보내려면 먼저 올바른 시트로 이동해야 합니다.

## 4단계: **ShapeExportOptions** 설정하여 도형을 편집 가능하게 유지하기 (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

`ExportAsEditable`을 `true`로 설정하면 Aspose.Cells가 도형의 벡터 데이터를 보존하므로, PowerPoint 사용자가 가져온 후에도 도형을 수정할 수 있습니다.

## 5단계: 도형을 PPTX 파일로 직접 내보내기 (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

`exportToImage` 메서드는 여러 이미지 형식을 지원합니다; 대상 파일 이름이 `.pptx`로 끝나면 Aspose.Cells는 해당 도형을 포함한 PowerPoint 슬라이드를 작성합니다.

### 예상 결과

- 지정한 디렉터리에 `textbox.pptx` 파일이 생성됩니다.
- PowerPoint에서 파일을 열면 원본 텍스트 상자가 포함된 단일 슬라이드가 표시됩니다.
- 텍스트 상자는 완전히 편집 가능하며(텍스트, 글꼴, 크기 등을 변경 가능) 확인할 수 있습니다.

## 6단계: 출력 확인 및 일반적인 엣지 케이스 처리

### 프로그래밍 방식으로 확인하기

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

`slideCount`가 `1`이면 내보내기가 성공한 것입니다.

### 엣지 케이스: 여러 도형이 있는 경우

워크시트에 여러 도형이 있고 특정 도형만 내보내고 싶다면 이름으로 찾아야 합니다:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### 엣지 케이스: 도형을 찾을 수 없는 경우

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### 엣지 케이스: 다른 형식으로 내보내기

`ShapeExportOptions`는 PNG, JPEG, SVG, EMF도 지원합니다. 파일 확장자를 변경하고 필요에 따라 `exportOptions.setImageFormat(ImageFormat.PNG)`를 설정하세요.

## 전체 실행 가능한 예제

모든 코드를 합치면 IDE에 복사‑붙여넣기 할 수 있는 독립 실행형 프로그램이 됩니다:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

프로그램을 실행하면 `textbox.pptx`가 생성됩니다. PowerPoint에서 파일을 열고 텍스트 상자를 오른쪽 클릭하면 일반적인 편집 핸들이 표시됩니다—즉 **ShapeExportOptions를 사용한 도형 내보내기**가 편집 가능성을 유지했음을 확인할 수 있습니다.

## 자주 묻는 질문

| Question | Answer |
|----------|--------|
| *Can I export a chart shape?* | Yes. The same `exportToImage` call works for charts, images, and SmartArt. |
| *What if I need a higher resolution PNG?* | Set `options.setImageFormat(ImageFormat.PNG)` and adjust `options.setResolution(300)` before exporting. |
| *Is the exported PPTX compatible with older PowerPoint versions?* | The library writes Office Open XML (PPTX) which is supported by PowerPoint 2007 and later. |
| *Do I need a license for this to work?* | A free evaluation works but adds a watermark. Register a license to remove it. |

## 다음 단계

- 여러 내보낸 도형을 하나의 슬라이드 덱으로 결합해야 한다면 **Aspose.Slides for Java**를 살펴보세요.
- 래스터 이미지(PNG/JPEG)로 빠른 렌더링이 필요할 경우 `ShapeExportOptions.setExportAsEditable(false)`를 사용하세요.
- 배치 처리 자동화: 모든 워크시트를 순회하면서 각 도형을 별도의 PPTX 파일로 내보내는 루프를 구현하세요.

---

### 결론

이제 Java에서 **ShapeExportOptions를 사용하여 도형을 내보내는** 방법을 알게 되었으며, 텍스트 상자(또는 기타 도형)를 PPTX 파일로 변환할 때 편집 가능성을 유지할 수 있습니다. 위 단계—라이브러리 설정, 워크북 로드, `ShapeExportOptions` 구성, `exportToImage` 호출—를 따라 하면 자동화된 보고 파이프라인에 도형 내보내기를 손쉽게 통합할 수 있습니다.

다양한 도형, 출력 형식, 해상도 설정을 실험해 보세요. 이 가이드가 도움이 되었다면 팀원과 공유하거나 나중에 참고할 수 있도록 즐겨찾기에 추가하세요. Happy coding!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 코드 예제와 자세한 설명을 제공해 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색할 수 있도록 도와줍니다.

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}