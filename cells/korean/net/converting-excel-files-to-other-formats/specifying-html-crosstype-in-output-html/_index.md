---
title: .NET에서 프로그래밍 방식으로 출력 HTML에 HTML CrossType 지정
linktitle: .NET에서 프로그래밍 방식으로 출력 HTML에 HTML CrossType 지정
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET에서 HTML CrossType을 지정하는 방법을 알아보세요. 단계별 튜토리얼을 따라 Excel 파일을 정밀하게 HTML로 변환하세요.
weight: 17
url: /ko/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 프로그래밍 방식으로 출력 HTML에 HTML CrossType 지정

## 소개
.NET 애플리케이션에서 Excel 파일을 HTML로 변환할 때 출력에서 교차 참조를 처리하는 방법을 지정해야 할 수도 있습니다. .NET용 Aspose.Cells의 HtmlSaveOptions 클래스는 변환 프로세스를 제어하는 다양한 설정을 제공하며, 이러한 옵션 중 하나는 HtmlCrossType입니다. 이 튜토리얼에서는 Excel 파일을 HTML 형식으로 내보낼 때 HTML 교차 유형을 프로그래밍 방식으로 지정하는 방법을 살펴보겠습니다. 
## 필수 조건
코드를 살펴보기 전에 다음 사항이 있는지 확인하세요.
-  .NET용 Aspose.Cells: 프로젝트에 Aspose.Cells 라이브러리가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
- Visual Studio: Visual Studio나 다른 .NET 개발 환경의 작업 설치입니다.
- C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 예제를 더 잘 이해하는 데 도움이 됩니다.
-  샘플 Excel 파일: 작업할 샘플 Excel 파일을 준비하세요. 이 예에서는 다음을 사용합니다.`sampleHtmlCrossStringType.xlsx`.
## 패키지 가져오기
시작하려면 필요한 Aspose.Cells 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
단계별로 나누어 설명하면, 여러분이 쉽게 따라할 수 있고 여러분의 프로젝트에 이 기능을 구현할 수 있을 것입니다.
## 1단계: 소스 및 출력 디렉토리 정의
먼저, 원본 Excel 파일의 디렉토리와 출력 HTML 파일을 저장할 디렉토리를 설정해야 합니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
## 2단계: 샘플 Excel 파일 로드
 다음으로 샘플 Excel 파일을 로드합니다.`Workbook` 객체. 여기서 모든 마법이 시작됩니다.
```csharp
// 샘플 Excel 파일을 로드합니다
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 여기서 교체하세요`"Your Document Directory"` Excel 파일이 있는 실제 경로와 함께. 이 줄은 Excel 파일을 메모리로 읽어서 조작할 수 있습니다.
## 3단계: HTML 저장 옵션 지정
 이제 우리는 인스턴스를 생성하겠습니다.`HtmlSaveOptions`이를 통해 Excel 파일을 HTML로 변환하는 방식을 구성할 수 있습니다.
```csharp
// HTML 교차 유형 지정
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 이 단계에서는 다음을 설정했습니다.`HtmlCrossStringType` 에게`HtmlCrossType.Default`이는 출력 HTML에서 교차 참조를 처리하는 데 사용할 수 있는 옵션 중 하나입니다.
## 4단계: 필요에 따라 십자가 유형 변경
 다양한 유형을 지정할 수 있습니다.`HtmlCrossStringType` 귀하의 요구 사항에 따라. 사용할 수 있는 다양한 옵션은 다음과 같습니다.
- `HtmlCrossType.Default`: 기본 십자가 유형입니다.
- `HtmlCrossType.MSExport`: MS Excel과 같은 동작으로 HTML을 내보냅니다.
- `HtmlCrossType.Cross`: 교차 참조를 생성합니다.
- `HtmlCrossType.FitToCell`: 교차 참조를 셀 크기에 맞춥니다.
 수정할 수 있습니다`HtmlCrossStringType` 이와 같이:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// 또는
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// 또는
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## 5단계: 출력 HTML 파일 저장
 옵션을 구성했으면 변환된 HTML 파일을 저장할 차례입니다. 다음을 사용하세요.`Save` 당신의 방법`Workbook` 물체:
```csharp
// 출력 HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 여기서 우리는 출력 파일의 이름을 다음을 기준으로 지정합니다.`HtmlCrossStringType` 우리는 설정했습니다. 이렇게 하면 변환에 사용된 교차 유형을 쉽게 식별할 수 있습니다.
## 6단계: 성공적인 실행 확인
마지막으로, 작업이 성공했는지 확인하는 것이 항상 좋은 방법입니다. 콘솔에 메시지를 인쇄할 수 있습니다.
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
이를 통해 오류 없이 프로세스가 완료되었음을 알 수 있습니다.
## 결론
이제 Aspose.Cells를 사용하여 .NET에서 Excel 내보내기에 대한 HTML 교차 유형을 성공적으로 지정했습니다. 이 기능은 HTML 출력에서 특정 서식이나 참조를 유지해야 할 때 특히 유용하며, 변환된 문서가 요구 사항을 충족하는지 확인합니다.
## 자주 묻는 질문
### Aspose.Cells의 HtmlCrossType은 무엇입니까?  
HtmlCrossType은 HTML 변환 중에 Excel 파일의 교차 참조가 처리되는 방식을 정의합니다. Default, MSExport, Cross, FitToCell과 같은 옵션을 선택할 수 있습니다.
### Aspose.Cells를 무료로 사용할 수 있나요?  
 Aspose.Cells는 무료 체험판을 제공합니다. 여기에서 다운로드할 수 있습니다.[웹사이트](https://releases.aspose.com/).
### .NET 프로젝트에 Aspose.Cells를 어떻게 설치합니까?  
 Visual Studio에서 NuGet 패키지 관리자를 통해 다음 명령을 실행하여 Aspose.Cells를 설치할 수 있습니다.`Install-Package Aspose.Cells`.
### Aspose.Cells에 대한 설명서는 어디서 찾을 수 있나요?  
 Aspose.Cells에서 포괄적인 문서를 찾을 수 있습니다.[여기](https://reference.aspose.com/cells/net/).
### HTML 파일을 저장하는 동안 오류가 발생하면 어떻게 해야 하나요?  
디렉토리 경로가 올바른지, 출력 디렉토리에 대한 쓰기 권한이 있는지 확인하세요. 문제가 지속되면 Aspose 지원 포럼에서 도움을 받으세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
