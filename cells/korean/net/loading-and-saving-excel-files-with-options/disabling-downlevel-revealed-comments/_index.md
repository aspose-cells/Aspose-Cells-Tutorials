---
title: HTML로 저장하는 동안 하위 레벨 공개 주석 비활성화
linktitle: HTML로 저장하는 동안 하위 레벨 공개 주석 비활성화
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel 통합 문서를 HTML로 저장할 때 하위 수준의 표시된 주석을 비활성화하는 방법을 알아보세요.
weight: 11
url: /ko/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML로 저장하는 동안 하위 레벨 공개 주석 비활성화

## 소개
Excel 통합 문서를 HTML로 변환해야 했고 프로세스 중에 불필요한 주석이나 숨겨진 내용이 드러나지 않도록 하려고 했던 적이 있나요? 바로 이때 하위 공개 주석을 비활성화하는 것이 유용합니다. Aspose.Cells for .NET을 사용하는 경우 Excel 통합 문서가 HTML 파일로 렌더링되는 방식을 완벽하게 제어할 수 있습니다. 이 자습서에서는 통합 문서를 HTML로 저장하는 동안 하위 공개 주석을 비활성화하는 데 도움이 되는 간단한 단계별 가이드를 안내합니다. 
이 글을 끝까지 읽으면 이 기능을 사용하는 방법을 명확하게 이해하고 HTML 출력물이 깔끔하고 주석이 없는지 확인할 수 있습니다.
## 필수 조건
단계별 가이드를 살펴보기에 앞서, 원활하게 따라갈 수 있도록 꼭 준비해야 할 몇 가지 사항을 살펴보겠습니다.
1. .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 설치해야 합니다. 아직 설치하지 않았다면 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
2. IDE: C# 코드를 작성하고 실행하기 위한 Visual Studio와 같은 개발 환경입니다.
3. C#에 대한 기본 지식: C# 구문과 객체 지향 프로그래밍에 익숙하면 코드를 따라가는 데 도움이 됩니다.
4.  임시 또는 라이센스 버전: 무료 평가판을 사용하거나 다음에서 임시 라이센스를 신청할 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/). 이렇게 하면 라이브러리가 아무런 제한 없이 작동합니다.
이제 준비가 되었으니 바로 시작해볼까요!
## 네임스페이스 가져오기
코드 예제를 살펴보기 전에 Aspose.Cells에 필요한 네임스페이스를 포함하는 것이 필수적입니다. 이것이 없으면 코드는 Excel 파일을 조작하는 데 필요한 메서드와 속성에 액세스할 수 없습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Aspose.Cells 네임스페이스를 가져오려면 C# 파일의 맨 위에 이 줄을 추가하세요.
## 1단계: 디렉토리 경로 설정
무엇보다도 먼저 소스 디렉토리(Excel 파일이 저장되는 곳)와 출력 디렉토리(HTML 파일이 저장되는 곳)를 설정해야 합니다. 이는 Aspose.Cells가 파일에 액세스하고 저장하기 위해 정확한 파일 경로가 필요하기 때문에 중요합니다.
```csharp
// Excel 파일이 있는 소스 디렉토리
string sourceDir = "Your Document Directory";
// 결과 HTML 파일이 저장될 출력 디렉토리
string outputDir = "Your Document Directory";
```
 이 단계에서는 다음을 교체합니다.`"Your Document Directory"` 시스템의 실제 파일 경로와 함께. 사용자 정의 디렉토리를 만들어 입력 및 출력 파일을 더 잘 구성할 수도 있습니다.
## 2단계: Excel 통합 문서 로드
 이 단계에서는 Excel 통합 문서를 메모리에 로드하여 조작할 수 있습니다. 데모 목적으로 샘플 파일인`"sampleDisableDownlevelRevealedComments.xlsx"`원하는 워크북을 사용할 수 있습니다.
```csharp
// 소스 디렉토리에서 샘플 통합 문서를 로드합니다.
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
이렇게 하면 Excel 파일의 모든 데이터와 구조가 포함된 Workbook 개체가 생성됩니다. 여기에서 이를 수정하고, 설정을 적용하고, 궁극적으로 다른 형식으로 저장할 수 있습니다.
## 3단계: HTML 저장 옵션 설정
이제, 하위 레벨의 공개된 주석을 비활성화하도록 HtmlSaveOptions 객체를 구성해야 합니다. 이 옵션은 주석이나 숨겨진 콘텐츠가 결과 HTML 파일에 공개되지 않도록 보장합니다.
```csharp
// 저장 옵션을 구성하려면 새 HtmlSaveOptions 개체를 만듭니다.
HtmlSaveOptions opts = new HtmlSaveOptions();
// 하위 레벨 공개된 댓글 비활성화
opts.DisableDownlevelRevealedComments = true;
```
 설정하여`DisableDownlevelRevealedComments` 에게`true`통합 문서를 HTML 파일로 저장하면 하위 수준의 주석이 비활성화됩니다.
## 4단계: 통합 문서를 HTML로 저장
HtmlSaveOptions 개체가 구성되면 다음 단계는 지정된 옵션을 사용하여 통합 문서를 HTML로 저장하는 것입니다. 여기서 실제 파일 변환이 발생합니다.
```csharp
// 지정된 저장 옵션을 사용하여 통합 문서를 HTML 파일로 저장합니다.
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
이 코드 줄에서 우리는 이전에 지정한 출력 디렉토리에 통합 문서를 저장하고 DisableDownlevelRevealedComments 설정을 적용합니다. 그 결과는 원치 않는 주석이 없는 깨끗한 HTML 파일이 됩니다.
## 5단계: 확인 및 실행
마지막으로 모든 것이 예상대로 작동하는지 확인하려면 콘솔에 성공 메시지를 출력할 수 있습니다.
```csharp
// 콘솔에 성공 메시지를 출력합니다.
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
이를 통해 작업이 오류 없이 완료되었음을 알 수 있습니다.
## 결론
이제 아시겠죠! Aspose.Cells for .NET을 사용하여 Excel 통합 문서를 HTML로 저장하는 동안 하위 레벨의 공개된 주석을 비활성화하는 방법을 성공적으로 배웠습니다. 이 기능을 사용하면 이제 통합 문서가 HTML로 렌더링되는 방식을 제어하고 불필요한 콘텐츠를 공개하지 않아도 됩니다. 웹 앱을 개발하든 단순히 깔끔한 HTML 출력이 필요하든 이 방법은 통합 문서 변환이 정확하고 안전하도록 보장합니다.
이 튜토리얼이 도움이 되었다면 Aspose.Cells의 다른 기능도 살펴보고 Excel 처리 능력을 더욱 향상시켜 보세요.
## 자주 묻는 질문
### 하위 레벨에서 공개된 댓글은 무엇인가요?
하위 레벨 공개 주석은 일반적으로 웹 개발에서 특정 HTML 기능을 지원하지 않는 이전 브라우저에 추가 정보를 제공하는 데 사용됩니다. Excel에서 HTML로 변환할 때 때때로 숨겨진 콘텐츠나 주석을 공개할 수 있으므로 이를 비활성화하는 것이 유용할 수 있습니다.
### 필요할 경우 하위 레벨의 댓글 기능을 활성화할 수 있나요?
 네, 간단히 설정하세요`DisableDownlevelRevealedComments` 재산에`false` 통합 문서를 HTML로 저장할 때 하위 주석을 활성화하려는 경우
### Aspose.Cells에 대한 임시 라이선스를 얻으려면 어떻게 해야 하나요?
 임시면허 신청은 다음 사이트를 방문하시면 간편하게 신청하실 수 있습니다.[Aspose 웹사이트](https://purchase.aspose.com/temporary-license/).
### 하위 주석을 비활성화하면 HTML 모양에 영향을 미칩니까?
아니요, 하위 레벨 공개된 주석을 비활성화해도 HTML 출력의 시각적 모양에는 영향을 미치지 않습니다. 이전 브라우저를 위한 추가 정보의 노출만 방지합니다.
### HTML 외에 다른 형식으로 통합 문서를 저장할 수 있나요?
 예, Aspose.Cells는 PDF, CSV, TXT와 같은 다양한 출력 형식을 지원합니다. 더 많은 옵션을 탐색할 수 있습니다.[선적 서류 비치](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
