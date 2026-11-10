---
category: general
date: 2026-10-01
description: Aspose.Cells를 사용하여 Excel을 HTML로 변환하면서 HTML에 글꼴을 삽입하는 방법을 배워보세요. 몇 단계만으로
  글꼴이 포함된 HTML로 Excel을 내보낼 수 있습니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: ko
lastmod: 2026-10-01
og_description: Excel 파일을 내보낼 때 HTML에 글꼴을 삽입하는 방법. 단계별 가이드를 따라 Excel을 글꼴이 포함된 HTML로
  변환하세요.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Excel에서 HTML에 글꼴을 삽입하는 방법 – Aspose.Cells 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Aspose.Cells를 사용하여 Excel을 HTML로 변환할 때 폰트를 포함하는 방법
url: /ko/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 HTML로 변환할 때 Aspose.Cells로 글꼴을 포함하는 방법

Excel 워크북을 HTML로 변환할 때 글꼴을 포함하는 것은 브라우저 간에 원본 모양을 유지하는 데 필수적입니다. 사용자 지정 글꼴을 그대로 유지하면서 Excel을 HTML로 변환해야 한다면, 이 가이드에서 전체 과정을 보여줍니다. 또한 Excel을 HTML로 내보내는 방법과 일관된 렌더링을 위해 HTML에 글꼴을 포함하는 것이 왜 중요한지도 확인할 수 있습니다.

이 튜토리얼에서는 필요한 라이브러리, 코드 구성, 생성된 HTML 파일 검증까지 알아야 할 모든 것을 다룹니다. 마지막에는 몇 줄의 C# 코드만으로 글꼴이 포함된 HTML로 Excel을 내보낼 수 있게 됩니다.

## 필요 사항

시작하기 전에 다음을 준비하세요:

* **.NET 6.0 이상** – 코드는 .NET 6을 대상으로 하지만 Aspose.Cells를 지원하는 모든 .NET 버전에서 동작합니다.
* **Aspose.Cells for .NET** – 라이선스를 받거나 Aspose 웹사이트에서 무료 평가판을 사용하세요.
* **C# 개발 환경** (Visual Studio, Rider, VS Code 등) – .NET 프로젝트를 컴파일할 수 있는 IDE면 됩니다.
* 사용자 지정 글꼴이 적용된 Excel 워크북 (`Styled.xlsx`) – 보존하려는 글꼴이 포함된 파일입니다.

## 1단계: .NET 프로젝트에 Aspose.Cells 설정하기

먼저 프로젝트에 Aspose.Cells NuGet 패키지를 추가합니다:

```bash
dotnet add package Aspose.Cells
```

그 다음 C# 파일 상단에 네임스페이스를 포함합니다:

```csharp
using Aspose.Cells;
```

패키지를 추가하면 `Workbook`, `HtmlSaveOptions` 및 관련 클래스들을 사용할 수 있게 됩니다.

## 2단계: Excel 워크북 로드하기

워크북을 로드하는 것은 **Excel 데이터를 내보내는 방법**의 첫 번째 구체적인 단계입니다. `Workbook` 생성자는 디스크에서 파일을 읽어들입니다:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*왜 중요한가:* Aspose.Cells는 워크북을 파싱하면서 셀 스타일, 수식, 글꼴 정보를 모두 읽어들입니다. 파일을 찾을 수 없으면 예외가 발생하므로 경로가 정확한지 확인하세요.

## 3단계: HTML 저장 옵션을 구성하여 글꼴 포함하기

**HTML에 글꼴을 포함하는** 핵심은 `HtmlSaveOptions` 클래스입니다. `EmbedFonts`를 `true`로 설정하면 워크북에 사용된 모든 글꼴이 Base64‑인코딩된 `@font-face` 규칙으로 HTML 출력에 포함됩니다.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*왜 중요한가:* 기본적으로 Aspose.Cells는 외부 글꼴 파일을 참조합니다. 클라이언트 컴퓨터에 해당 글꼴이 없으면 표시가 깨질 수 있습니다. `EmbedFonts`를 활성화하면 뷰어에 설치된 글꼴과 관계없이 렌더링된 HTML이 원본 Excel 시트와 동일하게 보장됩니다.

### 예외 상황: 지원되지 않는 글꼴

서버에 설치되지 않은 글꼴을 워크북이 사용하고 있다면 Aspose.Cells는 기본 시스템 글꼴로 대체합니다. 이를 방지하려면 서버에 필요한 글꼴을 설치하거나 내보낸 후 수동으로 포함하세요.

## 4단계: 구성한 옵션으로 워크북을 HTML로 저장하기

이제 HTML 파일을 기록합니다. `Save` 메서드에 출력 경로와 `HtmlSaveOptions` 인스턴스를 전달하면 됩니다:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

실행 후 `Styled.html`에는 스프레드시트 데이터와 각 사용자 지정 글꼴에 대한 Base64‑인코딩된 `@font-face` 정의가 포함된 `<style>` 블록이 들어 있습니다.

## 5단계: 포함된 글꼴 확인하기

브라우저에서 `Styled.html`을 열고 `<head>` 섹션을 검사하세요. 다음과 같은 내용이 보일 것입니다:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

테이블에 글꼴이 올바르게 표시되면 포함이 성공한 것입니다. 글자가 누락된 경우, 변환을 수행한 머신에 원본 글꼴 파일이 설치되어 있는지 다시 확인하세요.

## 일반적인 변형 및 추가 옵션

### 여러 워크시트 변환하기

모든 워크시트를 **Excel을 HTML로 변환**하려면 `ExportActiveWorksheetOnly = false`(기본값)를 설정합니다. Aspose.Cells는 각 시트마다 별도의 HTML 파일을 생성합니다.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### CSS 출력 제어하기

인라인 CSS를 비활성화하면 HTML 크기를 줄일 수 있습니다:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### 파일 대신 스트림 사용하기

웹 API에 통합할 때는 HTML을 `MemoryStream`에 기록하고 바로 반환합니다:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## 전문가 팁: 평가판 워터마크 제거를 위해 라이선스 적용하기

평가판을 사용 중이라면 생성된 HTML에 워터마크 주석이 포함될 수 있습니다. 워크북을 로드하기 전에 Aspose.Cells 라이선스를 적용하면 깨끗한 출력물을 얻을 수 있습니다:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## 전체 작동 예제

아래는 **글꼴을 포함하고**, **Excel을 HTML로 변환하며**, **Excel을 HTML로 내보내는** 전체 흐름을 한 번에 보여주는 완전한 실행 프로그램입니다:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**예상 결과:** 프로그램을 실행하면 `Styled.html`이 `YOUR_DIRECTORY`에 생성됩니다. 최신 브라우저에서 파일을 열면 원본 Excel 파일과 동일한 글꼴이 적용된 스프레드시트를 확인할 수 있습니다. 해당 글꼴이 설치되지 않은 머신에서도 동일하게 표시됩니다.

## 결론

이제 Aspose.Cells를 사용해 **Excel을 HTML로 변환**할 때 **글꼴을 포함**하는 방법을 알게 되었으며, 워크북 로드부터 포함된 글꼴 검증까지 전체 흐름을 확인했습니다. 이 접근 방식은 생성된 HTML에서 Excel 파일의 시각적 충실도를 유지하므로 웹 보고서, 이메일 뉴스레터, 또는 사용자 지정 타이포그래피가 필요한 모든 시나리오에 적합합니다.

다음으로 **Excel을 PDF로 내보내기**, **커스텀 CSS로 HTML 출력 스타일링**, **여러 워크북을 일괄 처리**와 같은 관련 주제를 살펴보세요. 이들 모두 동일한 `HtmlSaveOptions` 패턴을 기반으로 하므로 코드를 최소한으로 수정해 적용할 수 있습니다.

행복한 코딩 되세요!

## 다음에 배울 내용

다음 튜토리얼에서는 이 가이드에서 다룬 기술을 확장하는 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하여 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}