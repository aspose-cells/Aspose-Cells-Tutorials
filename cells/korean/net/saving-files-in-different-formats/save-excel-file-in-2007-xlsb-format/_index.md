---
title: Excel 파일을 2007 xlsb 형식으로 저장
linktitle: Excel 파일을 2007 xlsb 형식으로 저장
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 파일을 xlsb 형식으로 저장하는 방법을 알아보세요! 실용적인 예제가 담긴 단계별 가이드가 여러분을 기다립니다.
weight: 11
url: /ko/net/saving-files-in-different-formats/save-excel-file-in-2007-xlsb-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 파일을 2007 xlsb 형식으로 저장

## 소개
.NET에서 Excel 파일을 작업할 때, 특히 Aspose.Cells 라이브러리를 사용하면 많은 유연성과 기능을 사용할 수 있습니다. 이 강력한 도구를 사용하면 Excel 파일을 손쉽게 만들고, 수정하고, 저장할 수 있습니다. 오늘은 2007 xlsb 형식으로 Excel 파일을 저장하는 방법을 살펴보겠습니다. 일반적인 오버헤드 없이 Excel 파일을 프로그래밍 방식으로 처리할 방법을 찾고 계셨다면, 여기가 바로 적합한 곳입니다! 
## 필수 조건
시작하기 전에, 원활하게 따라갈 수 있는 모든 것이 있는지 확인해 보겠습니다. 필요한 것은 다음과 같습니다.
1. Visual Studio: 컴퓨터에 Visual Studio 버전이 설치되어 있는지 확인하세요. 여기서 .NET 코드를 작성하게 됩니다. 
2.  Aspose.Cells 라이브러리: .NET용 Aspose.Cells 라이브러리가 필요합니다. 아직 다운로드하지 않았다면 다음으로 이동하세요.[Aspose 다운로드 페이지](https://releases.aspose.com/cells/net/) 그것을 잡아라. 
3. C#에 대한 기본 지식: C#과 .NET에 대한 기본적인 이해는 코드 예제를 보다 편안하게 탐색하는 데 도움이 됩니다.
4. .NET Framework: Aspose.Cells 라이브러리에서 지원하는 적절한 .NET Framework로 프로젝트가 설정되었는지 확인하세요.
5. Excel 문서: 새 통합 문서를 만드는 것도 하나의 방법이지만, 기존 파일을 조작하려는 경우 시작 문서가 있으면 유용할 수 있습니다.
## 패키지 가져오기
프로젝트에서 Aspose.Cells 라이브러리를 사용하려면 필요한 네임스페이스를 가져와야 합니다. 이는 프로젝트를 시작하기 전에 도구 상자를 푸는 것과 비슷합니다.
### 프로젝트 설정
1. Visual Studio를 엽니다. '새 프로젝트 만들기'를 선택하여 새 프로젝트를 시작합니다. 
2. 프로젝트 템플릿 선택: 기본 설정에 따라 콘솔 애플리케이션이나 Windows Forms 애플리케이션을 선택하세요.
3. Aspose.Cells 참조 추가: 프로젝트 탐색기에서 "참조"를 마우스 오른쪽 버튼으로 클릭한 다음 "참조 추가"를 클릭합니다. 다운로드한 Aspose.Cells.dll 파일을 탐색합니다.
### 네임스페이스 가져오기
참조를 추가한 후 다음 단계는 C# 파일 맨 위에 네임스페이스를 포함시키는 것입니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이 코드 줄을 사용하면 Aspose.Cells 라이브러리가 제공하는 모든 클래스와 메서드에 아무런 조건 없이 액세스할 수 있습니다.

이제 2007 xlsb 형식으로 Excel 파일을 저장하는 단계를 살펴보겠습니다.
## 1단계: 저장 디렉토리 설정
먼저, Excel 파일을 어디에 저장할지 설정해야 합니다.

```csharp
// 문서 디렉토리 경로
string dataDir = "Your Document Directory\\";
```
 이 줄은 문서 디렉토리 경로를 정의합니다. 다음을 바꾸십시오.`"Your Document Directory"` 파일을 저장하려는 시스템의 실제 경로를 입력하세요.
## 2단계: 통합 문서 개체 만들기
다음으로 Aspose.Cells 라이브러리를 사용하여 새 통합 문서를 만들어 보겠습니다.

```csharp
Workbook workbook = new Workbook();
```
 여기서 우리는 새로운 인스턴스를 생성하고 있습니다`Workbook` 클래스. 이 새로 만든 워크북은 원하는 경우 데이터로 채우기 시작할 수 있는 빈 워크북입니다.
## 3단계: 통합 문서 저장
이제 재밌는 단계가 시작됩니다. 원하는 형식으로 통합 문서를 저장하세요!
```csharp
// Excel2007 xlsb 형식으로 저장
workbook.Save(dataDir + "output.xlsb", SaveFormat.Xlsb);
```
 이 코드 줄은 통합 문서를 다음과 같이 저장합니다.`output.xlsb` 지정된 디렉토리에서 다음을 사용하여`SaveFormat.Xlsb` 형식.`SaveFormat` 열거형은 다양한 형식을 지정할 수 있다는 점에서 강력합니다.`Xlsx`, `Xls`, 등.
## 결론
그리고 그렇게 해서 Aspose.Cells for .NET을 사용하여 2007 xlsb 형식으로 Excel 파일을 저장하는 방법을 성공적으로 배웠습니다. 이 간단하면서도 효과적인 기능은 .NET 애플리케이션에서 Excel 파일 처리를 자동화해야 하는 개발자에게 게임 체인저가 될 수 있습니다.

## 자주 묻는 질문
### Aspose.Cells 라이브러리란 무엇인가요?
Aspose.Cells는 개발자가 Microsoft Excel을 설치하지 않고도 프로그래밍 방식으로 Excel 파일을 만들고, 수정하고, 조작할 수 있게 해주는 강력한 .NET용 라이브러리입니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
 물론입니다! 다음을 사용할 수 있습니다.[무료 체험](https://releases.aspose.com/) 도서관의 기능을 살펴보세요.
### xls와 xlsb 형식의 차이점은 무엇입니까?
xls 형식은 오래되었고 바이너리 파일 구조를 기반으로 하는 반면, xlsb는 바이너리 저장소를 사용하지만 더 큰 파일 크기와 빠른 처리를 제공하는 새로운 형식입니다.
### Aspose.Cells 라이선스는 어디에서 구매할 수 있나요?
 라이센스는 다음에서 직접 구매할 수 있습니다.[Aspose 구매 페이지](https://purchase.aspose.com/buy).
### Aspose.Cells 문제에 대한 지원을 어떻게 요청할 수 있나요?
 문제가 발생하거나 질문이 있는 경우 언제든지 방문하세요.[지원 포럼](https://forum.aspose.com/c/cells/9)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
