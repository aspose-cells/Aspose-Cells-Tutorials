---
title: .NET에서 문서 변환 진행 상황을 프로그래밍 방식으로 추적
linktitle: .NET에서 문서 변환 진행 상황을 프로그래밍 방식으로 추적
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 문서 변환 진행 상황을 프로그래밍 방식으로 추적하는 방법을 알아봅니다.
weight: 20
url: /ko/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 문서 변환 진행 상황을 프로그래밍 방식으로 추적

## 소개
Aspose.Cells for .NET을 사용하여 문서 변환 프로세스를 개선하고 싶으신가요? 그렇다면 올바른 곳에 오셨습니다! 이 튜토리얼에서는 Excel 문서가 PDF 형식으로 변환되는 동안 변환 진행 상황을 추적하는 방법을 자세히 알아보겠습니다. 이를 달성하기 위한 필수 단계를 안내해 드릴 뿐만 아니라, 그 과정에서 유용한 통찰력도 곁들여 드리겠습니다. 그럼 시작해 볼까요!
## 필수 조건
문서 변환 추적의 세부적인 내용을 살펴보기 전에 몇 가지 전제 조건이 필요합니다.
1. C#에 대한 기본 지식: C#를 사용하여 코딩할 것이므로 이 프로그래밍 언어에 대한 기본적인 이해가 필요합니다.
2. Visual Studio 설치됨: 이것은 우리의 개발 환경으로 사용될 것입니다. 원하는 버전을 사용할 수 있지만, 최신 버전이 항상 좋은 선택입니다.
3.  .NET용 Aspose.Cells: Aspose.Cells가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
4.  Excel 파일: 변환을 위해 샘플 Excel 파일을 준비하세요. 간단한`.xlsx` 파일을 따라가세요.
## 패키지 가져오기
이제 필수 구성 요소를 다루었으므로 필요한 패키지를 C# 프로젝트로 가져올 차례입니다. 방법은 다음과 같습니다.
### 새 프로젝트 만들기
1. Visual Studio를 열고 새 프로젝트를 만듭니다. 단순성을 위해 Console App 템플릿을 선택합니다.
### Aspose.Cells에 참조 추가
2. 솔루션 탐색기에서 참조를 마우스 오른쪽 버튼으로 클릭하고 참조 추가를 선택한 다음 Aspose.Cells 어셈블리로 이동합니다(자동으로 추가되지 않은 경우). 패키지 관리자 콘솔에서 다음 명령을 실행하여 NuGet 패키지 관리자를 사용할 수도 있습니다.
```bash
Install-Package Aspose.Cells
```
### 네임스페이스 가져오기
3.  당신의 맨 위에`Program.cs` 파일에 다음 using 지시문을 추가합니다.
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
이제 프로젝트 설정이 모두 끝났습니다!

기초가 마련되었으니, 문서 변환 추적의 실제 프로세스를 이해하기 쉬운 단계로 나누어 보겠습니다. 
## 1단계: 디렉토리 정의
소스 및 출력 파일이 상주할 디렉토리를 지정하여 시작합니다. 방법은 다음과 같습니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
 교체를 꼭 해주세요`"Your Document Directory"` 시스템의 실제 경로와 함께. 이렇게 하면 파일을 쉽게 찾는 데 도움이 됩니다.
## 2단계: 통합 문서 로드
 다음으로, 다음을 사용하여 Excel 통합 문서를 로드해야 합니다.`Workbook` 수업. 방법은 다음과 같습니다.
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
 이 코드 줄은 다음을 생성합니다.`Workbook` 지정한 Excel 파일과 상호작용할 수 있게 해주는 객체입니다.
## 3단계: PDF 저장 옵션 설정
이제 PDF 저장 옵션을 설정해 보겠습니다. 여기서 진행 상황 추적의 마법이 시작됩니다. 인스턴스를 만듭니다.`PdfSaveOptions` 그리고 콜백을 할당합니다.
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
사용자 정의 콜백을 할당하여 (`TestPageSavingCallback`), 페이지 전환 진행 상황을 추적하기 위한 자체 로직을 구현할 수 있습니다.
## 4단계: 통합 문서를 PDF로 저장
 모든 것이 설정되었으므로 이제 통합 문서를 PDF로 저장할 시간입니다.`Save` 의 방법`Workbook` 클래스는 다음과 같습니다:
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
이 줄은 변환 프로세스를 트리거하고 페이지가 처리되는 동안 콜백 메서드를 호출합니다.
## 5단계: 콜백 클래스 구현
 이제 만들어 보겠습니다`TestPageSavingCallback` 클래스. 여기서 각 페이지를 저장할 때 시작과 끝에서 무슨 일이 일어나는지 정의합니다.
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // 페이지 인덱스 2 앞의 페이지를 출력하지 않습니다.
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // 페이지 인덱스 8 이후에는 페이지를 출력하지 않습니다.
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`이 메서드는 페이지가 저장을 시작하기 직전에 호출됩니다. 여기서는 각 페이지에 대한 저장 프로세스의 시작을 기록합니다. 또한 페이지를 출력할지 여부를 제어할 수 있습니다. 이 경우 인덱스 2 이전의 페이지는 건너뜁니다.
- `PageEndSaving`: 이 메서드는 페이지가 저장된 후에 호출됩니다. 각 페이지에 대한 저장이 종료되는 시점을 기록하고 추가 페이지를 처리할지 여부를 제어할 수 있습니다. 이 예에서는 페이지 인덱스 8 이후에 멈춥니다.
## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 문서 변환 진행 상황을 추적하는 시스템을 성공적으로 구현했습니다. 이 접근 방식을 사용하면 변환 프로세스를 모니터링할 수 있을 뿐만 아니라 포함하거나 제외할 페이지를 제어할 수 있어 문서 관리가 훨씬 더 효율적입니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Excel 파일을 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 강력한 .NET 라이브러리입니다.
### Aspose.Cells 무료 체험판을 어떻게 받을 수 있나요?
 무료 평가판을 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/).
### 변환 과정을 사용자 정의하는 것이 가능합니까?
네, 콜백을 사용하면 변환 중에 페이지가 처리되는 방식을 사용자 정의할 수 있습니다.
### 출력 파일 이름을 제어할 수 있나요?
물론입니다! 통합 문서를 저장할 때 출력 파일에 대한 이름을 지정할 수 있습니다.
### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 방문하면 지원을 받을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
