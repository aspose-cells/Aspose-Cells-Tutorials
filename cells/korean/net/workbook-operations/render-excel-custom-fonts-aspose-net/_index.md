---
"date": "2025-04-05"
"description": "Aspose.Cells for .NET을 사용하여 사용자 지정 글꼴을 사용하면서 Excel 파일을 PNG, TIFF, PDF 형식으로 렌더링하는 방법을 알아보세요. 모든 문서 변환에서 일관된 타이포그래피를 유지하세요."
"title": "Aspose.Cells를 사용하여 .NET에서 사용자 지정 글꼴을 사용하여 Excel을 PNG, TIFF, PDF로 렌더링"
"url": "/ko/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for .NET을 사용하여 사용자 지정 글꼴을 사용하여 Excel 파일을 PNG, TIFF 및 PDF로 렌더링합니다.

## 소개

Excel 파일을 이미지나 PDF로 변환할 때 글꼴 무결성을 유지하는 것은 브랜드 일관성에 매우 중요합니다. Aspose.Cells for .NET은 문서 변환 과정에서 사용자 지정 기본 글꼴을 지정할 수 있도록 하여 강력한 솔루션을 제공합니다.

이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 파일을 지정된 사용자 지정 기본 글꼴을 사용하여 PNG, TIFF, PDF 형식으로 렌더링하는 방법을 안내합니다. 다음과 같은 경우에 적합합니다.
- 렌더링된 문서에서는 일관된 인쇄체를 사용하세요.
- 변환하는 동안 글꼴 설정을 사용자 정의해야 합니다.
- .NET용 Aspose.Cells의 구성 옵션을 살펴보고 싶습니다.

귀하의 환경을 설정하고 이러한 기능을 원활하게 구현해 보겠습니다.

### 필수 조건

시작하기 전에 다음 사항이 있는지 확인하세요.
- **.NET 환경**: 컴퓨터에 설치합니다(가급적 .NET Core 또는 .NET Framework).
- **.NET용 Aspose.Cells 라이브러리**: 프로젝트에 설치되었습니다.
- **엑셀 파일**: 변환할 데이터가 있는 Excel 통합 문서입니다.

### .NET용 Aspose.Cells 설정

시작하려면 프로젝트에 Aspose.Cells 라이브러리를 추가하세요.

**.NET CLI 사용:**
```bash
dotnet add package Aspose.Cells
```

**패키지 관리자 사용:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

모든 기능에 대한 라이선스를 취득하세요:
- **무료 체험**: 방문하다 [Aspose 무료 체험판](https://releases.aspose.com/cells/net/) 최초 접근을 위해.
- **임시 면허**: 에서 얻으세요 [Aspose 임시 면허](https://purchase.aspose.com/temporary-license/).
- **구입**: 영구 라이센스를 받으려면 다음으로 이동하세요. [Aspose 구매](https://purchase.aspose.com/buy).

라이센스를 취득한 후 애플리케이션에서 Aspose.Cells를 초기화합니다.
```csharp
// Aspose.Cells에 대한 라이선스를 설정합니다.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## 구현 가이드

### 사용자 정의 기본 글꼴을 사용하여 PNG로 렌더링

사용자 지정 기본 글꼴을 설정하면서 Excel 워크시트를 PNG 형식으로 렌더링하면 시각적 일관성을 유지할 수 있습니다. 방법은 다음과 같습니다.

#### 1단계: 이미지 옵션 구성

이미지 출력에 대한 렌더링 옵션을 구성합니다.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// 디렉토리를 지정하세요.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Excel 파일을 엽니다.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 이미지 렌더링 옵션을 설정합니다.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // 통합 문서에서 누락된 글꼴에 사용자 지정 글꼴을 사용합니다.
imgOpt.DefaultFont = "Times New Roman";
```

#### 2단계: 렌더링 및 저장

이러한 설정을 사용하여 워크시트를 이미지 파일로 렌더링합니다.
```csharp
// 첫 번째 워크시트를 PNG 이미지로 렌더링합니다.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### 사용자 정의 기본 글꼴을 사용하여 TIFF로 렌더링

TIFF 형식은 고품질 이미지에 적합합니다. 전체 통합 문서를 TIFF 파일로 렌더링하는 방법은 다음과 같습니다.

#### 3단계: TIFF에 대한 이미지 옵션 설정

TIFF 출력에 맞게 렌더링 옵션을 구성합니다.
```csharp
// 이전에 정의한 디렉토리를 재사용하고 Excel 파일을 엽니다.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// TIFF에 대한 이미지 렌더링 옵션을 구성합니다.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### 4단계: 전체 통합 문서를 TIFF로 렌더링

전체 통합 문서를 단일 TIFF 파일로 변환합니다.
```csharp
// 통합 문서를 TIFF 이미지로 렌더링합니다.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### 사용자 정의 기본 글꼴을 사용하여 PDF로 렌더링

전문적인 문서 작성 시에는 글꼴의 일관성을 유지하면서 Excel 통합 문서를 PDF로 저장하는 것이 중요합니다.

#### 5단계: PDF 저장 옵션 구성

파일을 PDF로 저장하는 데 필요한 옵션을 설정합니다.
```csharp
using Aspose.Cells;

// 통합 문서를 다시 엽니다.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// PDF 저장 옵션을 설정합니다.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // 통합 문서에서 누락된 글꼴에 사용자 지정 글꼴을 사용합니다.
```

#### 6단계: PDF로 저장

통합 문서를 PDF 문서로 내보냅니다.
```csharp
// 통합 문서를 PDF 파일로 저장합니다.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## 실제 응용 프로그램

- **사업 보고서**: 사용자 정의 글꼴을 사용하여 모든 내보낸 보고서에 일관된 브랜딩을 보장합니다.
- **문서 보관**: 기존 Excel 파일을 균일한 인쇄 체계를 사용하여 쉽게 공유하고 보관할 수 있는 PDF로 변환합니다.
- **그래픽 디자인**: 프레젠테이션이나 디자인 프로젝트를 위해 Excel 데이터의 고해상도 TIFF 이미지를 만듭니다.

CRM 플랫폼이나 문서 관리 솔루션 등 다른 시스템과 통합하면 특정 트리거나 이벤트에 따라 내보내기를 자동화하여 이러한 사용 사례를 더욱 향상시킬 수 있습니다.

## 성능 고려 사항

렌더링 프로세스를 최적화하는 것이 중요합니다.
- **메모리 관리**: 폐기하다 `Workbook`, `SheetRender`, 그리고 `WorkbookRender` 객체를 신속하게 처리하여 리소스를 확보합니다.
- **일괄 처리**여러 파일을 다루는 경우 효율적인 처리를 위해 일괄 처리를 구현합니다.
- **비동기 작업**: 가능한 경우 비동기 방식을 활용하여 애플리케이션의 응답성을 개선합니다.

## 결론

이제 Aspose.Cells for .NET을 사용하여 Excel 통합 문서를 PNG, TIFF, PDF 형식으로 렌더링하고 사용자 지정 기본 글꼴을 설정하는 방법을 완벽하게 익히셨습니다. 이 기능을 사용하면 다양한 플랫폼과 용도에서 문서의 시각적 무결성을 유지할 수 있습니다.

Aspose.Cells에서 제공하는 추가 기능을 살펴보고 문서 처리 기능을 더욱 향상시키세요. 자세한 정보나 지원은 다음 웹사이트를 방문하세요. [Aspose 포럼](https://forum.aspose.com/c/cells/9).

## FAQ 섹션

**1. Aspose.Cells for .NET이란 무엇인가요?**
   — Aspose.Cells for .NET은 Excel 파일을 프로그래밍 방식으로 관리하고 변환하는 강력한 기능을 제공하는 라이브러리입니다.

**2. 웹 애플리케이션에서 Aspose.Cells를 사용할 수 있나요?**
   — 네, Aspose.Cells는 ASP.NET이나 다른 .NET 기반 웹 애플리케이션에 통합될 수 있습니다.

**3. 렌더링 중에 누락된 글꼴을 어떻게 처리합니까?**
   — 설정하여 `CheckWorkbookDefaultFont` 거짓으로 지정하고 `DefaultFont`원본 글꼴을 사용할 수 없더라도 모든 텍스트에 선택한 글꼴이 사용되도록 해야 합니다.

**4. PNG, TIFF, PDF 이외의 다른 형식도 지원되나요?**
   — 네, Aspose.Cells는 JPEG, BMP 등 다양한 이미지 형식을 지원하고 광범위한 문서 변환 기능을 제공합니다.

**5. 대규모 애플리케이션에서 Aspose.Cells를 사용하는 모범 사례는 무엇입니까?**
   — 효율적인 메모리 관리 기술을 활용하고, 여러 파일을 처리하기 위한 일괄 처리를 수행하며, 비동기 작업을 고려하여 애플리케이션 성능을 향상시킵니다.

## 자원
- **선적 서류 비치**: [Aspose.Cells 문서](https://reference.aspose.com/cells/net/)
- **다운로드**: [Aspose.Cells 출시](https://releases.aspose.com/cells/net/)
- **구입**: [Aspose.Cells 구매](https://purchase.aspose.com/buy)
- **무료 체험**: [Aspose.Cells를 무료로 사용해 보세요](https://releases.aspose.com/cells/net/)
- **임시 면허**: [임시 면허증을 받으세요](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}