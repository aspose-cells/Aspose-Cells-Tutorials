---
category: general
date: 2026-08-14
description: Aspose.Cells를 사용하여 Excel을 SVG로 내보낼 때 SVG에 글꼴을 포함합니다. 인쇄 영역 설정, 인쇄 옵션
  설정 및 WRAPCOLS 함수 사용 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: ko
lastmod: 2026-08-14
og_description: Aspose.Cells를 사용하여 Excel을 SVG로 내보낼 때 SVG에 글꼴을 포함합니다. 이 가이드는 인쇄 영역을
  설정하고, 인쇄 옵션을 구성하며, WRAPCOLS 함수를 적용하는 방법을 보여줍니다.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Excel을 SVG로 내보낼 때 SVG에 글꼴 삽입 – 단계별
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Excel을 SVG로 내보낼 때 SVG에 글꼴 포함
url: /ko/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 SVG로 내보내면서 SVG에 폰트 포함하기

Excel을 SVG로 내보낼 때 **SVG에 폰트를 포함**해야 하는 경우, 이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 정확히 수행하는 방법을 보여줍니다. 또한 **인쇄 영역 설정**, **인쇄 옵션 설정**, **WRAPCOLS 함수 사용**을 통해 레이아웃을 잃지 않고 데이터를 포맷하는 방법도 다룹니다.

전체 실행 가능한 예제를 따라가며 기존 워크북을 로드하고, `WRAPCOLS` 수식을 적용하고, SVG 전용 이미지 옵션을 구성하고, 인쇄 영역을 정의한 뒤, 폰트가 포함된 SVG 파일로 저장합니다. 별도의 외부 문서는 필요 없습니다—코드를 복사해서 실행하고 결과 SVG를 확인하면 됩니다.

## Embed fonts in SVG – configuring ImageOrPrintOptions

폰트를 포함하면 원본 Excel과 동일하게 SVG가 렌더링되며, 원본 폰트가 설치되지 않은 컴퓨터에서도 동일하게 보입니다.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*이 점이 중요한 이유*: `setEmbedFonts(true)`를 활성화하면 Aspose.Cells가 폰트 데이터를 SVG의 `<defs>` 섹션에 직접 기록합니다. 그 결과 브라우저와 플랫폼에 관계없이 동일하게 보이는 독립형 파일이 생성됩니다.

## Export Excel to SVG – full workflow

다음 단계는 워크북을 로드하고 SVG 파일로 저장하기까지의 전체 흐름을 보여줍니다.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**예상 출력**: `output.svg`가 `YOUR_DIRECTORY`에 생성됩니다. 브라우저에서 열면 모든 폰트가 포함된 워크시트와 `WRAPCOLS` 덕분에 3열로 래핑된 데이터, 그리고 `A1:H30` 영역 내부 셀만 렌더링된 것을 확인할 수 있습니다.

## Set print area for the worksheet

인쇄 영역을 정의하면 내보낸 SVG가 특정 범위로 제한되어 파일 크기가 줄어들고, 사용자는 관련 데이터에만 집중할 수 있습니다.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*팁*: 범위는 Excel의 A1 표기법을 따릅니다. 동적 범위가 필요하면 `ws.getCells().getMaxDisplayRange()`를 사용해 프로그래밍적으로 계산할 수 있습니다.

## Set print options for SVG output

인쇄 옵션은 Aspose.Cells가 워크시트를 이미지로 변환하는 방식을 제어합니다. 폰트 포함 외에도 해상도, 스케일링, 페이지 레이아웃 등을 조정할 수 있습니다.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*인쇄 옵션을 설정해야 하는 이유*: 옵션을 명시하지 않으면 Aspose.Cells가 기본값을 사용하게 되며, 이 경우 폰트가 포함되지 않거나 원하지 않는 스케일링이 적용돼 SVG가 흐리게 보이거나 스타일이 잘못될 수 있습니다.

## Use WRAPCOLS function to wrap column data

`WRAPCOLS`는 세로 범위를 지정된 열 수로 분배하는 Excel 수식입니다. 긴 목록을 컴팩트한 그리드 형태로 표시하고 싶을 때 유용합니다.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

워크북을 저장하면 Aspose.Cells가 수식을 평가해 정의된 인쇄 영역 안에 3열 레이아웃을 생성합니다. 이 기법은 범위 크기에 관계없이 적용 가능하니 두 번째 인수를 원하는 열 개수로 조정하면 됩니다.

## Complete runnable example

아래는 어떤 IDE에든 붙여넣을 수 있는 전체 Java 프로그램입니다. 클래스패스에 Aspose.Cells for Java 라이브러리가 포함되어 있는지 확인하세요.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**검증 단계**

1. 프로그램을 실행합니다.  
2. `output.svg`를 웹 브라우저에서 엽니다.  
3. 텍스트가 원본 Excel 파일과 동일한 서체로 표시되는지 확인합니다(폰트가 포함됨).  
4. `A1:H30` 영역 내 셀만 표시되고 `A2:A10` 데이터가 3열로 나타나는지 확인합니다.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| SVG에서 폰트가 누락됨 | `setEmbedFonts(false)`이 설정됐거나 폰트 파일에 접근할 수 없음 | `setEmbedFonts(true)`로 설정하고, 코드가 실행되는 머신에 폰트가 설치되어 있는지 확인 |
| WRAPCOLS가 평가되지 않음 | 계산 엔진이 비활성화됨 | 내보내기 전에 `workbook.calculateFormula()`를 호출하거나 저장 시 Aspose.Cells가 자동으로 평가하도록 함 |
| 내보낸 SVG가 빈 화면임 | 인쇄 영역에 데이터가 포함되지 않음 | `setPrintArea`에 전달하는 범위를 다시 확인 |
| SVG 파일이 너무 큼 | 스케일링이 적용되지 않아 해상도가 높음 | `imgOptions.setResolution(96)` 등으로 DPI를 조정 |

## Pro tip: reuse ImageOrPrintOptions for multiple worksheets

워크북에 여러 시트가 있고 동일한 SVG 설정이 필요할 경우, 하나의 `ImageOrPrintOptions` 인스턴스를 생성해 각 시트의 `PageSetup`에 할당하세요. 이렇게 하면 메모리 사용량이 감소하고 모든 내보낸 파일에서 폰트 포함이 일관되게 적용됩니다.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Next steps

* **다른 벡터 포맷으로 내보내기** – `ImageFormat.SVG`를 `ImageFormat.PDF`로 바꾸면 고품질 PDF를 생성합니다.  
* **배치 처리** – 폴더에 있는 `.xlsx` 파일을 순회하면서 자동으로 SVG를 생성합니다.  
* **맞춤형 폰트 처리** – 시스템 폰트가 부족할 때 `FontSettings`를 사용해 특정 디렉터리에서 폰트를 로드합니다.  

**embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, **use WRAPCOLS function**을 마스터하면 Excel 데이터를 직접 활용해 보고서, 대시보드, 웹 시각화용 고품질 SVG를 자동으로 생성할 수 있습니다. 즐거운 코딩 되세요!

## What Should You Learn Next?

다음 튜토리얼에서는 이 가이드에서 다룬 기술을 확장하는 관련 주제를 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [Aspose.Cells for .NET를 사용하여 Excel에서 인쇄 영역 설정 방법](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Aspose.Cells for .NET를 사용한 Excel 인쇄 영역 설정 (독일어)](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Aspose.Cells for .NET를 사용한 Excel 인쇄 영역 설정 (프랑스어)](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}