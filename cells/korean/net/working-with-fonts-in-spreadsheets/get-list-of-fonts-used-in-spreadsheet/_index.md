---
title: 스프레드시트에 사용된 글꼴 목록 가져오기
linktitle: 스프레드시트에 사용된 글꼴 목록 가져오기
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 쉬운 튜토리얼을 통해 Aspose.Cells for .NET을 사용하여 Excel 스프레드시트에서 글꼴을 가져오고 나열하는 방법을 알아보세요.
weight: 10
url: /ko/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스프레드시트에 사용된 글꼴 목록 가져오기

## 소개
Excel 스프레드시트를 스크롤하면서 다양한 셀에 사용된 글꼴에 대해 궁금해한 적이 있나요? 오래된 문서를 보고 어떤 타이포그래피가 선택되었는지 알고 싶으신가요? 글쎄요, 운이 좋으시네요! Aspose.Cells for .NET을 사용하면 스프레드시트에 숨겨진 글꼴 비밀을 걸러내고 밝혀낼 수 있는 도구 상자가 있는 것과 같습니다. 이 가이드에서는 Excel 파일에서 사용된 모든 글꼴 목록을 쉽게 검색하는 방법을 안내해 드리겠습니다. 안전띠를 매고 스프레드시트의 세계로 뛰어드세요!
## 필수 조건
코드로 넘어가기 전에, 시작하기 위해 필요한 몇 가지가 있습니다. 걱정하지 마세요, 정말 간단합니다. 필요한 것의 체크리스트는 다음과 같습니다.
1. Visual Studio: 컴퓨터에 Visual Studio 버전이 설치되어 있는지 확인하세요. 여기서 코드를 작성합니다.
2. .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 사용할 수 있어야 합니다. 아직 다운로드하지 않았다면 다음에서 가져올 수 있습니다.[대지](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 약간의 이해는 코드를 쉽게 탐색하는 데 분명 도움이 될 것입니다.
4. 샘플 Excel 파일: 작업하려면 "sampleGetFonts.xlsx"와 같은 샘플 Excel 파일이 필요합니다. 여기서 글꼴 탐색을 적용합니다.
모든 것을 준비했다면 이제 코딩에 들어갈 준비가 된 것입니다!
## 패키지 가져오기
시작하기 위해 필요한 네임스페이스를 임포트해 보겠습니다. .NET에서 패키지를 임포트하는 것은 파티에 적합한 손님을 초대하는 것과 비슷합니다. 손님이 없다면 일이 순조롭게 진행되지 않습니다.
Aspose.Cells를 가져오는 방법은 다음과 같습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
이 간단한 줄로 Aspose.Cells의 핵심 기능을 우리 프로젝트에 초대합니다. 이제 워크북을 로드하는 것으로 넘어가겠습니다.
## 1단계: 문서 디렉토리 설정
우선 먼저—코드를 살펴보기 전에 문서 디렉토리 경로를 설정해야 합니다. 여기에 Excel 파일이 있습니다. 
```csharp
string dataDir = "Your Document Directory";
```
"Your Document Directory"를 Excel 파일이 있는 실제 경로로 바꾸세요. 이것은 프로그램에 "여기에 내 Excel 파일을 숨겨 두었습니다. 가서 확인해 보세요!"라고 말하는 것으로 생각하세요.
## 2단계: 소스 워크북 로드
 Excel 파일을 로드할 시간입니다. 우리는 새로운 인스턴스를 만들 것입니다.`Workbook` 클래스를 사용하여 파일 경로를 전달합니다. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 여기서 무슨 일이 일어나고 있나요? 우리는 기본적으로 스프레드시트의 문을 열고 있습니다.`Workbook` 클래스를 이용하면 Excel 파일의 내용과 상호작용할 수 있습니다. 
## 3단계: 모든 글꼴 가져오기
 이제 마법의 순간이 왔습니다. 실제로 글꼴을 검색해 보겠습니다!`GetFonts()` 이 방법은 우리에게 황금 티켓과도 같습니다.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 여기서 우리는 통합 문서에 그 안에서 사용된 모든 글꼴에 대해 털어놓으라고 요청하고 있습니다.`fnts` 배열은 우리의 보물을 보관할 것이다.
## 4단계: 글꼴 인쇄
마지막으로, 그 글꼴을 가져와서 인쇄해 봅시다. 이렇게 하면 우리가 찾은 것을 확인하는 데 도움이 될 것입니다.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 이 루프는 우리의 각 글꼴을 통과합니다`fnts` 배열을 만들어 콘솔에 하나씩 출력합니다. 마치 Excel 파일에 있는 모든 멋진 타이포그래피 선택을 보여주는 것과 같습니다!
## 결론
이제 다 됐습니다! 몇 줄의 코드만 있으면 Aspose.Cells for .NET을 사용하여 Excel 스프레드시트에서 사용된 글꼴 목록을 성공적으로 검색하여 인쇄할 수 있습니다. 이는 글꼴에 대한 것만이 아닙니다. 문서의 미묘한 차이를 이해하고, 프레젠테이션을 개선하고, 스프레드시트에서 타이포그래피의 기술을 마스터하는 것입니다. 개발자이든 Excel을 만지작거리는 것을 좋아하는 사람이든 이 작은 스니펫이 게임 체인저가 될 수 있습니다. 
## 자주 묻는 질문
### Aspose.Cells를 별도로 설치해야 하나요?
네, 프로젝트에서 라이브러리를 다운로드하여 참조해야 합니다. 
### Aspose.Cells를 다른 포맷에도 사용할 수 있나요?
물론입니다! Aspose.Cells는 XLSX, XLS, CSV와 같은 여러 Excel 형식과 호환됩니다.
### 무료 체험판이 있나요?
 네, 무료 체험판을 받으실 수 있습니다.[다운로드 링크](https://releases.aspose.com/).
### 기술 지원은 어떻게 받을 수 있나요?
 도움이 필요하면[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9) 매우 유용한 자료입니다.
### Aspose.Cells는 .NET Core와 호환됩니까?
네, Aspose.Cells는 .NET Core 프로젝트와도 호환됩니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
