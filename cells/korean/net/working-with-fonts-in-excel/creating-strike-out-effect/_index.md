---
title: Excel에서 텍스트에 취소선 효과 만들기
linktitle: Excel에서 텍스트에 취소선 효과 만들기
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 단계별 자습서를 통해 Aspose.Cells for .NET을 사용하여 Excel에서 텍스트에 취소선 효과를 적용하는 방법을 알아보세요.
weight: 15
url: /ko/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 텍스트에 취소선 효과 만들기

## 소개
Excel에서 시각적 요소는 데이터 자체만큼 중요합니다. 중요한 변경 사항을 강조 표시하든 더 이상 관련성이 없는 항목을 표시하든 텍스트의 취소선 효과는 스프레드시트에서 시각적 표현을 관리하는 고전적인 방법입니다. 이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel에서 텍스트에 취소선 효과를 구현하는 과정을 안내합니다. 이 자습서에서는 필요한 전제 조건을 다룰 뿐만 아니라 이 효과를 쉽게 복제할 수 있도록 단계별 접근 방식도 제공합니다.
## 필수 조건
튜토리얼을 시작하기 전에 다음 전제 조건을 충족하는지 확인하세요.
1. 개발 환경: .NET 개발 환경을 설정해야 합니다. 이는 Visual Studio 또는 .NET 개발을 지원하는 다른 IDE가 될 수 있습니다.
2. .NET용 Aspose.Cells: 프로젝트에 Aspose.Cells가 설치되어 있는지 확인하세요. 다음 링크에서 다운로드할 수 있습니다.[Aspose.Cells 다운로드](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: 예제가 C#로 코딩되므로 C# 프로그래밍에 대한 기본적인 이해가 도움이 됩니다.
4. .NET Framework: 프로젝트가 호환되는 .NET Framework 버전(일반적으로 .NET Core 또는 .NET Framework 4.5 이상)을 대상으로 하는지 확인하세요.
## 패키지 가져오기
코드를 작성하기 전에 Aspose.Cells에서 필요한 네임스페이스를 가져와야 합니다. 이는 라이브러리에서 제공하는 다양한 기능에 액세스하는 데 중요합니다. 필요한 네임스페이스를 가져오는 방법은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이러한 가져오기를 사용하면 이 튜토리얼 전체에서 사용되는 Workbook, Worksheet 및 Style 클래스에 액세스할 수 있습니다.
이제 무대를 마련했으니, 프로세스를 관리 가능한 단계로 나누어 보겠습니다. 각 단계에는 Excel에서 텍스트에 취소선 효과를 만드는 방법을 안내하는 명확한 지침이 함께 제공됩니다.
## 1단계: 문서 디렉토리 정의
Excel 문서가 저장될 경로를 정의하는 것으로 시작합니다. 이는 출력 파일을 저장할 위치입니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` Excel 파일을 저장할 실제 디렉토리 경로와 함께. 이렇게 하면 출력에 대한 디렉토리가 설정됩니다.
## 2단계: 디렉토리 생성
다음으로, 이전 단계에서 지정한 디렉토리가 존재하는지 확인해야 합니다. 존재하지 않는 경우 프로그래밍 방식으로 생성할 수 있습니다.
```csharp
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 코드는 디렉토리가 존재하는지 확인하고 존재하지 않으면 생성합니다. 이는 나중에 파일을 저장하려고 할 때 오류를 방지하는 데 도움이 됩니다.
## 3단계: 통합 문서 개체 인스턴스화
이제 새 Workbook 개체를 만들 시간입니다. 이는 데이터를 추가하고 형식을 적용할 Excel 파일의 기초입니다.
```csharp
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
```
 그만큼`Workbook` 클래스는 Excel 파일을 나타냅니다. 이 클래스의 인스턴스를 만들면 본질적으로 새 Excel 문서를 만드는 것입니다.
## 4단계: 새 워크시트 추가
각 워크북에는 여러 워크시트가 포함될 수 있습니다. 워크북에 새 워크시트를 만들어 보겠습니다.
```csharp
// Excel 개체에 새 워크시트 추가
int i = workbook.Worksheets.Add();
```
 그만큼`Add` 의 방법`Worksheets` 컬렉션은 통합 문서에 새 워크시트를 추가하고 해당 인덱스를 반환합니다. 
## 5단계: 새 워크시트 참조 얻기
워크시트를 만든 후에는 향후 작업을 위해 이를 참조해야 합니다.
```csharp
// 새로 추가된 워크시트의 시트 인덱스를 전달하여 해당 워크시트의 참조를 얻습니다.
Worksheet worksheet = workbook.Worksheets[i];
```
여기서 인덱스를 사용하여 새로 생성된 워크시트를 가져옵니다.`i`). 이를 통해 워크시트를 조작할 수 있습니다.
## 6단계: 셀에 액세스
 워크시트에서 취소선 형식을 적용할 특정 셀에 액세스하고 싶을 것입니다. 이 예에서는 셀을 사용합니다.`A1`.
```csharp
// 워크시트에서 "A1" 셀에 액세스하기
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
 Excel에서 셀은 열 및 행 식별자(예: "A1")로 참조됩니다. 우리는 셀에 대한 참조를 얻고 있습니다.`A1` 추가 조작을 위해서.
## 7단계: 셀에 값 추가
 다음으로 셀에 텍스트를 삽입해 보겠습니다. 셀에 "Hello Aspose!"라고 씁니다.`A1`.
```csharp
// "A1" 셀에 값 추가
cell.PutValue("Hello Aspose!");
```
 그만큼`PutValue` 방법은 셀에 문자열 값을 할당하는 데 사용됩니다. 이 문자열을 표시하려는 내용으로 수정할 수 있습니다.
## 8단계: 셀의 스타일 얻기
이제 셀에 텍스트가 들어갔으므로, 원하는 서식을 적용하기 위해 셀의 스타일에 접근하여 취소선 효과를 포함한 설정을 할 차례입니다.
```csharp
// 셀의 스타일 얻기
Style style = cell.GetStyle();
```
 그만큼`GetStyle` 이 메서드는 셀의 현재 스타일을 검색하여 글꼴 유형, 크기, 효과 등의 속성을 수정할 수 있습니다.
## 9단계: 취소선 효과 설정
셀의 텍스트에 취소선 효과를 적용해 보겠습니다. 셀의 글꼴 스타일을 수정하겠습니다.
```csharp
// ExStart:SetStrikeout
// 글꼴에 취소선 효과 설정하기
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
 설정하여`IsStrikeout` true로 설정하면 Excel에서 선택한 셀의 취소선에 있는 텍스트를 시각적으로 취소선으로 지우도록 지시하는 것입니다. 이는 목록에서 시각적으로 항목을 표시하는 것과 비슷합니다.
## 10단계: 셀에 스타일 적용
스타일을 수정한 후에는 셀에 다시 적용하여 변경 사항을 반영해야 합니다.
```csharp
// 셀에 스타일 적용하기
cell.SetStyle(style);
```
 그만큼`SetStyle` 이 방법은 셀을 새 스타일로 업데이트하며, 이제 취소선 서식도 포함됩니다.
## 11단계: Excel 파일 저장
 마지막으로, 통합 문서를 지정된 디렉토리에 저장할 시간입니다. 이 예에서는 다음 이름으로 파일을 저장합니다.`book1.out.xls`.
```csharp
// Excel 파일 저장하기
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 그만큼`Save`방법은 97-2003 Excel 형식으로 통합 문서를 디스크에 씁니다. 필요한 경우 다른 형식을 지정할 수 있습니다.
## 결론
Aspose.Cells for .NET을 사용하여 Excel에서 텍스트에 취소선 효과를 만드는 것은 단계별로 나누어 보면 간단한 과정입니다. 이 가이드를 따르면 이제 시각적 단서로 스프레드시트를 향상시키고 데이터를 유익할 뿐만 아니라 시각적으로 매력적으로 만드는 기술을 갖추게 됩니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 .NET 애플리케이션에서 Excel 파일을 관리하기 위한 강력한 라이브러리로, 이를 통해 Excel 문서를 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있습니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
 네, 체험 기간 동안 무료로 사용할 수 있습니다. 무료 체험은 다음에서 가능합니다.[Aspose.Cells 무료 체험판](https://releases.aspose.com/).
### Aspose.Cells를 어떻게 구매하나요?
 Aspose.Cells에 대한 라이센스는 해당 웹사이트를 통해 구매할 수 있습니다.[Aspose.Cells 구매](https://purchase.aspose.com/buy).
### Aspose.Cells 사용에 대한 예가 있나요?
 네, 다음에서 많은 예제와 코드 스니펫을 찾을 수 있습니다.[Aspose.Cells 문서](https://reference.aspose.com/cells/net/).
### Aspose.Cells에 대한 지원은 어디서 받을 수 있나요?
 커뮤니티 지원 및 도움을 받을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
