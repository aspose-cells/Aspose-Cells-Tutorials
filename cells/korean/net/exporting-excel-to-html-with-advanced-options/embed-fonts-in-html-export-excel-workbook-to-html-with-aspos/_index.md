---
category: general
date: 2026-06-17
description: 통합 문서를 HTML로 저장할 때 HTML에 글꼴을 포함합니다. 몇 단계만으로 통합 문서를 HTML로 변환하고 글꼴이 포함된
  Excel HTML을 내보내는 방법을 알아보세요.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: ko
og_description: 통합 문서를 HTML로 저장할 때 HTML에 글꼴을 포함합니다. 이 가이드를 따라 통합 문서를 HTML로 변환하고 전체
  글꼴 지원이 포함된 Excel HTML을 내보내는 방법을 알아보세요.
og_title: HTML에 글꼴 포함 – Excel 워크북을 HTML로 내보내기
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: HTML에 글꼴 삽입 – Aspose.Cells를 사용하여 Excel 워크북을 HTML로 내보내기
url: /ko/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML에 폰트 삽입 – Aspose.Cells로 Excel 워크북을 HTML로 내보내기

Excel 시트를 내보낼 때 **HTML에 폰트를 삽입**하는 방법이 궁금하셨나요? 여러분만 그런 것이 아닙니다. 많은 개발자들이 생성된 HTML이 원본 Excel 스타일 대신 일반적인 sans‑serif 폰트를 표시하면서 난관에 봉착합니다. 좋은 소식은? 몇 줄의 코드만으로 **워크북을 HTML로 저장**하고 모든 폰트를 그대로 유지할 수 있다는 것입니다.

이 튜토리얼에서는 Aspose.Cells for .NET을 사용해 **워크북을 HTML로 변환**하는 전체 과정을 살펴보고, 폰트 삽입이 왜 중요한지 설명하며, **Excel HTML을 내보내는 방법**을 정확히 보여드립니다. 외부 도구나 수동 후처리 없이 깔끔하고 실행 가능한 C# 코드만으로 가능합니다.

## 사전 요구 사항

- .NET 6.0 이상 (예제는 .NET Core, .NET Framework, .NET 5+에서도 동작)
- Aspose.Cells for .NET NuGet 패키지 (`Install-Package Aspose.Cells`)
- C# 및 Excel 파일 처리에 대한 기본 지식
- 선택 사항: 삽입하려는 사용자 정의 TrueType 폰트 파일 (예: `MyFont.ttf`)

모두 준비되셨나요? 좋습니다—시작해봅시다.

## 1단계: 프로젝트 설정 및 Excel 워크북 로드

먼저 워크북 객체가 필요합니다. 새로 만들거나 기존 `.xlsx` 파일을 로드할 수 있습니다. 아래 예제는 최소 설정에 사용자 정의 폰트를 워크북 스타일 컬렉션에 추가하는 방법을 보여줍니다.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*왜 이 단계인가요?* 워크북을 먼저 로드하면 Aspose.Cells가 모든 셀 스타일을 검사할 수 있습니다. 사용자 정의 폰트를 등록하면 나중에 HTML에 삽입할 때 해당 폰트를 찾을 수 있게 보장됩니다.

## 2단계: **HTML에 폰트 삽입**을 위한 HtmlSaveOptions 구성

마법은 `HtmlSaveOptions`에 있습니다. `EmbedFonts = true`로 설정하면 라이브러리가 사용된 모든 폰트를 Base64‑인코딩된 `@font-face` 규칙으로 HTML 파일 안에 삽입합니다.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*왜 `EmbedFonts`를 활성화하나요?* 이를 비활성화하면 출력 HTML이 시스템 폰트를 참조하게 되고, 해당 폰트가 없는 컴퓨터에서는 대체 폰트가 표시됩니다. 삽입을 하면 브라우저와 장치에 관계없이 시각적 일관성을 보장합니다.

## 3단계: 구성된 옵션으로 **워크북을 HTML로 저장**

이제 파일을 실제로 씁니다. `Save` 메서드는 세 개의 인수를 받습니다: 대상 경로, 포맷(`SaveFormat.Html`), 그리고 방금 구성한 옵션입니다.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

문제가 없으면 전체 스프레드시트 레이아웃 *및* 폰트 데이터가 마크업에 직접 인코딩된 단일 `with-fonts.html` 파일이 생성됩니다.

## 예상 출력

`with-fonts.html`을 최신 브라우저(Chrome, Edge, Firefox)에서 열면 다음과 같이 표시됩니다:

- 원본 Excel 파일과 동일한 셀 값, 색상, 테두리
- Excel에서 사용한 정확한 폰트로 텍스트가 렌더링(컴퓨터에 해당 폰트가 설치되지 않아도)
- 외부 `.css` 또는 이미지 파일이 없음—모든 것이 HTML 파일 내부에 포함

아래는 생성된 `<style>` 블록의 작은 예시이며, Base64 문자열은 가독성을 위해 잘라두었습니다:

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## 4단계: 흔히 발생하는 문제와 해결 방법

| Issue | Why It Happens | Fix |
|------|----------------|-----|
| **Missing font in the HTML** | 폰트 파일이 `FontConfigs`에 저장되지 않은 상태에서 저장을 수행함. | `HtmlSaveOptions`를 만들기 **전** `FontConfigs.AddFontFile`을 호출합니다. |
| **Huge HTML file size** | 많은 대용량 폰트를 삽입하면 파일 크기가 급증. | 실제로 필요한 폰트만 삽입하고, 최신 Aspose 버전에서는 `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`을 사용해 사용된 글리프만 포함시킵니다. |
| **Incorrect characters (e.g., Asian glyphs)** | 폰트에 필요한 유니코드 범위가 포함되지 않음. | 해당 문자들을 지원하는 폰트를 사용하거나 추가 폰트를 폰트 폴백으로 삽입합니다. |
| **Performance slowdown on large workbooks** | 폰트 삽입 과정에서 추가 처리 비용 발생. | `ExportActiveWorksheetOnly = true`로 활성 워크시트만 내보내거나 워크북을 작은 단위로 나눕니다. |

## 5단계: 솔루션 확장 – 여러 워크시트 내보내기

모든 시트를 **HTML로 변환**하려면 `ExportActiveWorksheetOnly`를 끄기만 하면 됩니다:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

각 워크시트는 동일 HTML 파일 내에서 별도의 `<div>`로 표시되며, 폰트 삽입은 그대로 유지됩니다.

## 팁: CSS 커스터마이징과 결합

생성된 마크업을 더 세밀하게 제어하고 싶다면 `HtmlSaveOptions`의 `CssClassPrefix` 속성을 활용해 클래스 이름 충돌을 방지할 수 있습니다:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

이제 모든 생성된 CSS 클래스가 `myExcel_`으로 시작하므로, 나중에 자체 스타일시트를 적용하기가 쉬워집니다.

## 정리

- `HtmlSaveOptions.EmbedFonts = true` 로 **HTML에 폰트 삽입**을 활성화
- `wb.Save(..., SaveFormat.Html, ...)` 로 **워크북을 HTML로 저장**하여 단일, 자체 포함 파일 생성
- 이 방법은 **워크북을 HTML로 변환**하면서 모든 시각적 요소를 보존, 즉 **Excel HTML을 내보내는 방법**에 대한 고전적인 질문에 답변
- `FontConfigs.AddFontFile` 로 사용자 정의 폰트를 등록해 삽입 가능하도록 보장
- `ExportImagesAsBase64`, `ExportActiveWorksheetOnly` 등 옵션을 조정해 프로젝트 요구에 맞춤

## 다음 단계는?

- 더 휴대성이 높은 패키지를 원한다면 **MHTML**(`SaveFormat.Mhtml`) 로 내보내기
- 인쇄용 포맷이 필요하면 **PDF 변환**(`SaveFormat.Pdf`) 탐색
- HTML 내보내기를 웹 API에 통합해 사용자가 실시간으로 스타일링된 스프레드시트를 다운로드하도록 구현

폰트를 바꾸고, 워크시트 선택을 변경하고, 여러 내보내기 포맷을 조합해 보세요. Aspose.Cells의 유연성을 활용하면 자동화된 보고 대시보드부터 이메일용 HTML 스니펫까지 어떤 시나리오에도 맞춤형 출력을 만들 수 있습니다.

코딩 즐겁게, 그리고 HTML이 언제나 원본 Excel 시트와 똑같이 보이길 바랍니다!


## 다음에 배워야 할 내용은?


다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 제공해 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Set Default Font in Excel-to-HTML Conversion with Aspose.Cells for .NET | Workbook Operations Guide](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}