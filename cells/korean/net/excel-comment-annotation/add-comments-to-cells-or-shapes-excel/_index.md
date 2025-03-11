---
title: Excel에서 셀이나 도형에 주석 추가
linktitle: Excel에서 셀이나 도형에 주석 추가
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 셀에 주석을 추가하는 방법을 알아보세요. 초보자를 위한 Excel 기능 향상을 위한 단계별 가이드입니다.
weight: 11
url: /ko/net/excel-comment-annotation/add-comments-to-cells-or-shapes-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 셀이나 도형에 주석 추가

## 소개
셀이나 도형에 주석을 추가하여 Excel 문서를 개선하고 싶으신가요? 글쎄요, 당신은 올바른 곳에 있습니다! 이 문서에서는 Aspose.Cells for .NET을 사용하여 Excel 파일에 효율적으로 주석을 추가하는 방법을 안내합니다. 피드백, 주석 또는 친절한 메모를 제공하든, 단계별로 나누어서 매끄럽게 따라갈 수 있도록 도와드리겠습니다. 그러니 가상 도구 상자를 들고 시작해 볼까요!
## 필수 조건
Excel 시트에 주석을 추가하는 여정을 시작하기 전에 필요한 모든 것이 있는지 확인해 보겠습니다. 다음은 준비해야 할 사항입니다.
- Visual Studio 설치됨: .NET 애플리케이션을 작성하고 컴파일할 수 있는 IDE가 필요합니다. Visual Studio는 많은 개발자에게 인기 있는 선택입니다.
-  Aspose.Cells 패키지: Aspose.Cells 라이브러리가 설치되어 있는지 확인하세요. Excel 파일을 조작하는 강력한 도구입니다. 다음에서 다운로드할 수 있습니다.[릴리스 페이지](https://releases.aspose.com/cells/net/).
- C#에 대한 기본 지식: 모든 예제가 이 프로그래밍 언어를 사용하므로 C# 프로그래밍에 대한 기본적인 이해가 유익합니다.
-  Aspose.Cells 라이센스: 확장된 기능을 사용하려면 라이센스 구매를 고려하세요. 그러나 다음과 같이 시작할 수도 있습니다.[무료 체험](https://releases.aspose.com/), 제한이 따릅니다.
## 패키지 가져오기
Aspose.Cells 작업을 시작하려면 먼저 C# 프로젝트에서 필요한 패키지를 가져와야 합니다. 방법은 다음과 같습니다.
### 프로젝트 열기
Visual Studio에서 기존 프로젝트를 열거나, 처음부터 시작하는 경우 새 프로젝트를 만듭니다.
### Aspose.Cells 설치
NuGet에서 Aspose.Cells 패키지를 쉽게 설치할 수 있습니다. 방법은 다음과 같습니다.
1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
2. "NuGet 패키지 관리"를 선택합니다.
3. "Aspose.Cells"를 검색하여 최신 버전을 설치하세요.
### 사용 문장 추가
코드 파일의 맨 위에 다음 using 지시문을 포함합니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이제 Aspose.Cells를 사용하여 Excel 파일을 조작할 준비가 되었습니다. 

전제 조건을 정리했으니 가이드의 핵심으로 넘어가겠습니다. Excel 파일의 셀이나 모양에 주석을 추가하는 것입니다. 단계별로 살펴보겠습니다.
## 1단계: 문서 디렉토리 설정
Workbook을 조작하기 전에 문서를 저장할 위치를 정의해야 합니다. 문서 디렉토리를 설정하는 방법은 다음과 같습니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
여기서는 디렉토리가 있는지 확인합니다. 없으면 만듭니다. 가구를 정리하기 전에 집이 있는지 확인하는 것과 같습니다!
## 2단계: 통합 문서 개체 인스턴스화
이제 모든 작업을 수행할 새로운 Workbook 인스턴스를 만들어야 합니다.
```csharp
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
```
통합 문서를 Excel 걸작을 그릴 수 있는 빈 캔버스로 생각해 보세요. 
## 3단계: 새 워크시트 추가
Excel 파일에는 여러 개의 시트가 포함될 수 있습니다. 통합 문서에 새 워크시트를 추가해 보겠습니다.
```csharp
// Workbook 개체에 새 워크시트 추가
int sheetIndex = workbook.Worksheets.Add();
```
모든 위대한 예술가에게는 빈 캔버스가 필요합니다. 여기서, 우리는 하나를 더합니다!
## 4단계: 새 워크시트 액세스
다음으로, 새 워크시트를 참조하여 변경 작업을 시작하세요.
```csharp
// 새로 추가된 워크시트의 시트 인덱스를 전달하여 해당 워크시트의 참조를 얻습니다.
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
이 단계는 방금 추가한 새 시트에서 직접 작업할 수 있게 해주고 워크벤치에 접근하는 것과 같은 효과를 주기 때문에 매우 중요합니다.
## 5단계: 셀 F5에 주석 추가
이제 흥미로운 부분으로 넘어가겠습니다. 특정 셀에 주석을 추가하는 것입니다. 이 경우, 셀 "F5"에 주석을 달 것입니다.
```csharp
// "F5" 셀에 주석 추가
int commentIndex = worksheet.Comments.Add("F5");
```
이것을 작업의 특정 부분에 스티커 노트를 붙이는 것으로 생각해보세요. 생각을 기억하는 데 도움이 됩니다!
## 6단계: 새로 추가된 댓글에 접근하기
댓글을 사용자 지정하려면 댓글을 추가한 직후에 댓글에 접근해야 합니다.
```csharp
// 새로 추가된 댓글에 접근하기
Comment comment = worksheet.Comments[commentIndex];
```
이 단계에서는 스티커 노트를 꺼내서 거기에 우리의 생각을 적어봅니다.
## 7단계: 주석 메모 설정
이제 메모를 적어둘 시간입니다. 댓글에 텍스트를 추가해 보겠습니다.
```csharp
// 댓글 메모 설정하기
comment.Note = "Hello Aspose!";
```
이것을 당신의 스티커 노트에 쓰는 것으로 상상해보세요. 당신은 당신의 생각을 말로 표현하고 있는 거예요!
## 8단계: Excel 파일 저장
마지막으로, 우리는 우리의 노고를 저장해야 합니다. 이렇게 하면 우리의 코멘트가 포함된 워크북이 저장될 것입니다!
```csharp
// Excel 파일 저장하기
workbook.Save(dataDir + "book1.out.xls");
```
이 단계는 환상적인 이야기를 쓴 후 책을 닫는 것과 같습니다. 책이 저장되도록 해야 합니다!
## 결론
이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel 파일의 셀에 주석을 성공적으로 추가했습니다. 주석은 협업 프로젝트에 유용할 수도 있고, 단순히 자신에게 알림을 남기는 데도 유용합니다. 이제 전체 과정을 거쳤으니 Excel 기술을 다음 단계로 끌어올릴 준비가 되었습니다.
## 자주 묻는 질문
### Aspose.Cells를 사용하여 도형에 주석을 추가할 수 있나요?
네! 셀에 하는 것과 비슷한 방식으로 도형에 주석을 추가할 수 있습니다.
### Aspose.Cells는 어떤 파일 형식을 지원하나요?
Aspose.Cells는 XLS, XLSX, CSV 등 다양한 형식을 지원합니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 무료 체험판을 제공하지만, 모든 기능을 사용하려면 라이선스를 구매해야 할 수도 있습니다.
### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?
 방문하면 지원을 받을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9).
### Aspose.Cells에 대한 임시 라이선스를 어떻게 얻을 수 있나요?
 임시 면허는 다음에서 얻을 수 있습니다.[Aspose 라이센스 페이지](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
