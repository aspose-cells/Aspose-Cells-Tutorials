---
title: PDF 저장 옵션에 대한 기본 글꼴 설정
linktitle: PDF 저장 옵션에 대한 기본 글꼴 설정
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 PDF 저장 옵션에 대한 기본 글꼴을 설정하는 방법을 알아보고, 항상 문서가 완벽하게 보이도록 하세요.
weight: 11
url: /ko/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF 저장 옵션에 대한 기본 글꼴 설정

## 소개
PDF 형식으로 보고서, 송장 또는 기타 문서를 생성할 때 콘텐츠가 적절하게 보이도록 하는 것이 가장 중요합니다. 글꼴은 문서의 시각적 매력과 가독성을 유지하는 데 중요한 역할을 합니다. 그러나 Excel 파일에서 사용한 글꼴을 PDF를 생성하는 시스템에서 사용할 수 없는 경우 어떻게 해야 할까요? 바로 Aspose.Cells for .NET이 유용합니다. 이 강력한 라이브러리를 사용하면 PDF 저장 옵션에 대한 기본 글꼴을 설정하여 어디에서 열든 문서가 전문적이고 일관되게 보이도록 할 수 있습니다.
## 필수 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1. Visual Studio: 코드를 작성하고 실행하려면 Visual Studio와 같은 개발 환경이 필요합니다.
2.  .NET용 Aspose.Cells: 최신 버전은 다음에서 다운로드할 수 있습니다.[이 링크](https://releases.aspose.com/cells/net/). 혹은, Visual Studio의 NuGet 패키지 관리자를 통해 설치할 수도 있습니다.
3. C#에 대한 기본 지식: C#의 기본을 이해하면 코드 예제를 따라가는 데 도움이 됩니다.
4. 샘플 Excel 파일: 테스트를 위해 샘플 Excel 파일을 준비하세요. 다양한 글꼴과 스타일로 하나를 만들어 Aspose.Cells가 누락된 글꼴을 어떻게 처리하는지 확인할 수 있습니다.
## 패키지 가져오기
프로젝트에서 Aspose.Cells를 사용하려면 먼저 필요한 패키지를 가져와야 합니다. 방법은 다음과 같습니다.
1. 프로젝트 열기: Visual Studio를 실행하고 기존 프로젝트를 열거나 새 프로젝트를 만듭니다.
2. 참조 추가: 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 "NuGet 패키지 관리"를 선택합니다.
3. Aspose.Cells 설치: "Aspose.Cells"를 검색하고 "설치" 버튼을 클릭하세요.
4. 사용 지침 추가: C# 파일의 맨 위에 다음 네임스페이스를 포함합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## 1단계: 디렉토리 설정
파일을 작업하기 전에 소스 및 출력 디렉토리를 정의하는 것이 중요합니다. 이렇게 하면 입력 Excel 파일을 쉽게 찾고 생성된 출력 파일을 저장할 수 있습니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` 디렉토리의 실제 경로를 포함합니다.
## 2단계: Excel 파일 열기
 이제 디렉토리가 설정되었으므로 작업하려는 Excel 파일을 열어 보겠습니다.`Workbook` Aspose.Cells의 클래스는 Excel 문서를 로드하는 데 사용됩니다.
```csharp
// Excel 파일을 엽니다
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
파일 이름을 실제 파일 이름으로 바꿔야 합니다.
## 3단계: 이미지 렌더링 옵션 설정
다음으로 Excel 시트를 이미지 형식으로 변환하기 위한 렌더링 옵션을 구성해야 합니다. 인스턴스를 만듭니다.`ImageOrPrintOptions`이미지 유형과 기본 글꼴을 지정합니다.
```csharp
// PNG 파일 형식으로 렌더링
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 이 코드 조각에서 우리는 다음을 설정합니다.`CheckWorkbookDefaultFont` 재산에`false`즉, 글꼴이 누락된 경우 지정된 기본 글꼴("Times New Roman")이 대신 사용됩니다.
## 4단계: 시트를 이미지로 렌더링
 이제 워크북의 첫 번째 시트를 PNG 이미지로 렌더링해 보겠습니다.`SheetRender` 이를 달성하려면 클래스를 사용해야 합니다.
```csharp
// 첫 번째 워크시트를 이미지로 렌더링합니다.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## 5단계: 이미지 유형 변경 및 TIFF로 렌더링
 TIFF와 같이 동일한 시트를 다른 이미지 형식으로 렌더링하려면 간단히 다음을 변경하면 됩니다.`ImageType` 속성을 확인하고 렌더링 과정을 반복합니다.
```csharp
// TIFF 형식으로 설정
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## 6단계: PDF 저장 옵션 구성
 다음으로 PDF 저장 옵션을 설정해 보겠습니다. 우리는 인스턴스를 생성할 것입니다.`PdfSaveOptions`기본 글꼴을 설정하고, 누락된 글꼴을 확인하도록 지정합니다.
```csharp
// PDF 저장 옵션 구성
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## 7단계: 통합 문서를 PDF로 저장
저장 옵션이 구성되었으니, 이제 Excel 통합 문서를 PDF 파일로 저장할 차례입니다. 
```csharp
// 통합 문서를 PDF로 저장
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## 8단계: 실행 확인
마지막으로, 사용자에게 프로세스가 성공적으로 완료되었음을 알리는 것이 좋습니다. 간단한 콘솔 메시지를 사용하여 이를 달성할 수 있습니다.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## 결론
Aspose.Cells는 Excel 파일 조작을 처리하는 유연하고 강력한 방법을 제공하여 개발자가 서식을 유지하는 시각적으로 매력적인 문서를 더 쉽게 만들 수 있도록 합니다. 보고서, 재무 문서 또는 기타 형태의 데이터 프레젠테이션을 작업하든 글꼴 렌더링을 제어하면 출력 품질을 크게 향상시킬 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Microsoft Excel을 설치하지 않고도 Excel 파일을 조작할 수 있는 강력한 .NET 라이브러리입니다. 다양한 파일 형식을 지원하고 스프레드시트 작업을 위한 풍부한 기능을 제공합니다.
### Excel 파일에 기본 글꼴을 어떻게 설정할 수 있나요?
 기본 글꼴은 다음을 사용하여 설정할 수 있습니다.`PdfSaveOptions` 클래스를 지정하고 원하는 글꼴 이름을 지정합니다. 이렇게 하면 글꼴이 없어도 문서에서 지정한 기본 글꼴을 사용합니다.
### Excel 파일을 PDF 이외의 다른 형식으로 변환할 수 있나요?
물론입니다! Aspose.Cells를 사용하면 Excel 파일을 이미지(PNG, TIFF), HTML, CSV 등 다양한 형식으로 변환할 수 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 상업용 제품이지만, 제한된 체험판으로 무료로 사용해 볼 수 있습니다. 모든 기능을 사용하려면 라이선스를 구매해야 합니다.
### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 Aspose.Cells에 대한 지원은 다음 사이트를 방문하여 찾을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9), 다른 사용자 및 개발자에게 질문을 하고 통찰력을 공유할 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
