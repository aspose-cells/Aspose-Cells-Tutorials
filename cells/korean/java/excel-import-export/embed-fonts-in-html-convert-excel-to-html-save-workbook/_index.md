---
category: general
date: 2026-06-27
description: Excel을 HTML로 변환할 때 HTML에 글꼴을 포함시키세요. 간단한 Java 코드를 사용하여 글꼴이 포함된 HTML로
  워크북을 저장하는 방법을 배워보세요.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: ko
og_description: Excel을 HTML로 변환할 때 HTML에 글꼴을 포함합니다. 이 가이드는 Java를 사용하여 워크북을 글꼴이 포함된
  HTML로 저장하는 방법을 보여줍니다.
og_title: HTML에 글꼴 삽입 – Excel을 HTML로 변환하고 워크북 저장
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: HTML에 글꼴 포함 – Excel을 HTML로 변환하고 워크북 저장
url: /ko/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML에 글꼴 삽입 – Excel을 HTML로 변환하고 워크북 저장

Excel을 HTML로 변환할 때 **HTML에 글꼴을 삽입**해야 했던 적이 있나요? 보고서 포털을 구축 중인데 기본 웹 글꼴로는 부족할 수도 있습니다. 좋은 소식은 평범하고 일반적인 모양에 만족할 필요가 없다는 것입니다—Aspose.Cells를 사용하면 스프레드시트에서 사용한 정확한 글꼴을 생성된 HTML 파일에 바로 포함시킬 수 있습니다.

이 튜토리얼에서는 **워크북을 HTML로 저장**하면서 글꼴을 삽입하는 완전한 실행 가능한 Java 예제를 단계별로 살펴보고, 이렇게 해야 하는 이유를 설명하며, 발생할 수 있는 몇 가지 주의사항을 짚어봅니다. 최종적으로 원본 Excel 시트와 동일하게 보이는 독립형 HTML 페이지를 얻을 수 있습니다. 글리프가 누락되지 않고 외부 CSS 문제도 없습니다.

## What You’ll Learn

- Java에서 기존 Excel 워크북을 로드하거나 새로 만드는 방법.  
- `HtmlSaveOptions`를 구성하여 워크북의 글꼴을 HTML 출력에 직접 삽입하는 방법.  
- `Workbook.save`를 호출하여 **글꼴이 삽입된 HTML** 파일로 저장하는 방법.  
- 큰 글꼴 파일, 사용자 정의 글꼴 디렉터리 처리 및 일반적인 함정 해결 팁.

> **Prerequisite:** 클래스패스에 Aspose.Cells for Java(최신 버전)와 Java 8+ 런타임이 필요합니다. 다른 서드파티 라이브러리는 필요하지 않습니다.

---

## Step 1: Set Up the Project and Import Required Classes

코드에 들어가기 전에 개발 환경이 준비되었는지 확인합니다. Maven을 사용한다면 `pom.xml`에 Aspose.Cells 의존성을 추가하세요:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Gradle을 선호한다면 다음과 같이 추가합니다:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Pro tip:** 라이브러리를 최신 상태로 유지하세요. 새로운 릴리스는 글꼴 처리 기능을 개선하고 삽입된 데이터 크기를 줄이는 경우가 많습니다.

이제 필요한 클래스를 임포트합니다:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

이 임포트문을 통해 워크북 모델, HTML 내보내기 옵션 및 몇 가지 유틸리티 클래스를 사용할 수 있습니다.

---

## Step 2: Load (or Create) the Excel Workbook

기존 `.xlsx` 파일을 로드하거나 즉석에서 워크북을 만들 수 있습니다. 예시로 프로젝트 `resources` 폴더에 `Sample.xlsx` 파일이 있다고 가정해 보겠습니다.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

소스 파일이 없는 경우 빠르게 워크북을 생성할 수도 있습니다:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Why this matters:** 글꼴을 삽입하면 Aspose.Cells가 워크북에 사용된 정확한 글꼴 정의를 추출합니다. 워크북에 사용자 정의 글꼴이 포함되어 있으면 HTML에 함께 포함되어 시각적 충실도를 보장합니다.

---

## Step 3: Configure HtmlSaveOptions to Embed Fonts

이 단계가 튜토리얼의 핵심입니다. 기본적으로 `HtmlSaveOptions`는 시스템 글꼴을 참조하는 CSS를 작성합니다. 이 동작을 바꾸려면 `setEmbedFonts(true)` 플래그를 활성화합니다.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### What the Options Do

| Option | Default | Effect when changed |
|--------|---------|---------------------|
| `setEmbedFonts(true)` | `false` | 전체 글꼴 파일을 (보통 Base64‑인코딩된 data URI 형태로) 생성된 HTML에 삽입합니다. |
| `setSubsetFonts(true)` | `false` | 실제 사용된 문자만 포함하도록 삽입 글꼴을 축소하여 파일 크기를 크게 줄입니다. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | 라이선스 제약이 있는 경우 특정 글꼴만 선택적으로 삽입하도록 설정할 수 있습니다. |

> **Edge case:** 워크북이 서버에 설치되지 않은 글꼴을 사용하면 Aspose.Cells는 기본 시스템 글꼴로 대체합니다. 예기치 않은 상황을 방지하려면 모든 사용자 정의 글꼴이 Java 런타임의 글꼴 디렉터리에 있거나 `FontConfig`를 통해 수동으로 등록되어 있는지 확인하세요.

---

## Step 4: Save the Workbook as HTML with Embedded Fonts

옵션 설정이 완료되었으니 `save`를 호출하면 됩니다. 출력은 워크북 데이터 **와** 글꼴 파일이 마크업에 직접 인코딩된 단일 `.html` 파일이 됩니다.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

`page.html`을 최신 브라우저(Chrome, Firefox, Edge 등)에서 열면 Excel에서 보던 정확한 타이포그래피가 그대로 렌더링됩니다. 외부 글꼴 파일이나 누락된 문자가 없습니다.

---

## Step 5: Verify the Result and Understand the Output

생성된 HTML 파일을 브라우저에서 열어보세요(Chrome, Firefox, Edge 등). 워크시트가 충실히 렌더링되는 것을 확인할 수 있습니다. 글꼴이 실제로 삽입됐는지 다시 확인하려면:

1. 페이지를 오른쪽 클릭 → “View Page Source”(페이지 소스 보기).  
2. `@font-face`를 검색합니다. `src: url(data:font/ttf;base64,…)` 형태의 CSS 규칙을 찾을 수 있는데, 이것이 Base64‑인코딩된 글꼴 데이터입니다.  

이와 같이 보이면 **HTML에 글꼴 삽입** 단계가 성공한 것입니다.

### Common Questions

- **“HTML 파일이 예상보다 큰 이유는?”**  
  전체 글꼴 파일을 삽입하면 수백 KB가 추가될 수 있습니다. `setSubsetFonts(true)`를 사용해 크기를 줄이거나 필요한 시트만 변환하는 방안을 고려하세요.

- **“특정 글꼴만 삽입할 수 있나요?”**  
  가능합니다. `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)`를 설정하고 `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`와 같이 글꼴 이름을 지정하면 됩니다.

- **“글꼴에 라이선스가 있어 삽입할 수 없는 경우는?”**  
  플래그를 끄고(`setEmbedFonts(false)`) CSS에서 웹 안전 폰트 대체를 제공하거나, 권한이 있는 CDN에 호스팅된 글꼴을 사용하세요.

---

## Step 6: Handling Large Workbooks and Performance Tips

글꼴 삽입은 보통 규모의 스프레드시트에 적합하지만, 수십 개의 사용자 정의 글꼴이 포함된 워크북은 HTML 크기를 급격히 증가시킬 수 있습니다. 다음과 같은 성능 중심 권장 사항을 참고하세요:

- **Subset fonts**(이미 소개)로 실제 사용된 글리프만 포함하도록 합니다.  
- **필요한 워크시트만 내보내기** `htmlOpts.setExportActiveWorksheetOnly(true)` 사용.  
- **HTML 압축**(예: 서버에서 gzip)으로 네트워크 지연을 줄입니다.  
- **생성된 HTML 캐시**를 활용해 동일한 Excel 파일에 대한 반복 요청을 빠르게 처리합니다.

---

## Step 7: Next Steps – Going Beyond Basic Export

이제 **HTML에 글꼴 삽입**을 마스터했으니 관련 기능을 탐색해 볼 수 있습니다:

- **이미지를 포함한 Excel → HTML 변환** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **HTML 대신 PDF 생성** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **반응형 HTML 만들기** `htmlOpts.setExportActiveWorksheetOnly`와 `htmlOpts.setExportGridLines`를 조정.  

모든 기능은 동일한 패턴을 따릅니다: `*SaveOptions` 객체를 구성하고, 적절한 플래그를 전환한 뒤 `Workbook.save`를 호출합니다.

---

## Conclusion

Aspose.Cells for Java를 사용해 **Excel을 HTML로 변환**하고 **워크북을 HTML로 저장**하면서 **글꼴을 HTML에 삽입**하는 방법을 배웠습니다. 핵심 단계는 다음과 같습니다:

1. 워크북을 로드하거나 생성합니다.  
2. `HtmlSaveOptions`를 만들고 `setEmbedFonts(true)`를 활성화합니다.  
3. 해당 옵션으로 `Workbook.save`를 호출합니다.

그 결과 원본 스프레드시트와 동일하게 보이는 단일 포터블 HTML 파일을 얻을 수 있습니다—글꼴이 누락되지 않고, 추가 CSS 파일도 없으며, 클라이언트에 설치된 글꼴에 의존하지 않습니다.

글꼴 서브세팅, 선택적 삽입, 서버‑사이드 캐싱 등을 실험해 보세요. 파일이 예상보다 크거나 글리프가 누락되는 등 문제가 발생하면 앞서 다룬 옵션을 다시 검토하고 조정하면 됩니다.

즐거운 코딩 되시고, 이제 Java 애플리케이션에서 바로 제공할 수 있는 픽셀‑완벽 HTML을 마음껏 활용하세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Convert Excel to HTML in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Export Excel to HTML Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Export Excel to HTML using IStreamProvider & Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}