---
"description": "Aspose.Cells for .NET을 사용하여 Excel 워크시트의 셀과 범위를 보호하는 방법을 알아보세요. 이 단계별 가이드를 따라 스프레드시트를 보호하세요."
"linktitle": "Aspose.Cells를 사용하여 워크시트의 셀과 범위 보호"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Aspose.Cells를 사용하여 워크시트의 셀과 범위 보호"
"url": "/ko/net/worksheet-security/protect-cells-and-ranges/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 워크시트의 셀과 범위 보호

## 소개
스프레드시트 작업에는 특히 협업 환경에서 시트의 특정 부분을 원치 않는 수정으로부터 보호하는 작업이 포함되는 경우가 많습니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 워크시트의 특정 셀과 범위를 보호하는 방법을 살펴보겠습니다. 보호된 시트를 설정하고, 편집 가능한 범위를 지정하고, 파일을 저장하는 과정을 안내해 드립니다. 이 기능은 민감한 데이터에 대한 액세스를 제한하면서 특정 섹션은 다른 사용자가 수정할 수 있도록 허용하려는 경우 매우 유용합니다.
## 필수 조건
튜토리얼을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.
1. Aspose.Cells for .NET: 프로젝트에 Aspose.Cells 라이브러리가 설치되어 있어야 합니다. 아직 설치되어 있지 않다면 다음에서 다운로드할 수 있습니다. [Aspose 웹사이트](https://releases.aspose.com/cells/net/).
2. Visual Studio: 이 가이드에서는 C# 개발을 지원하는 Visual Studio나 이와 유사한 IDE를 사용한다고 가정합니다.
3. C#에 대한 기본 지식: C# 프로그래밍의 기본 사항과 Visual Studio에서 프로젝트를 설정하는 방법을 알아야 합니다.
4. Aspose.Cells 라이선스: Aspose는 무료 평가판을 제공하지만, 유효한 라이선스를 사용하면 라이브러리의 모든 기능을 사용할 수 있습니다. 라이선스가 없는 경우, [여기 임시 면허증](https://purchase.aspose.com/temporary-license/).
위에 나열한 모든 것을 준비했다면 이제 코딩 단계로 넘어가겠습니다.
## 패키지 가져오기
Aspose.Cells를 사용하려면 먼저 필요한 네임스페이스를 C# 파일로 가져와야 합니다. 가져오는 방법은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
```
그만큼 `Aspose.Cells` 네임스페이스를 사용하면 Excel 파일을 조작하기 위한 핵심 기능에 액세스할 수 있습니다. `System.IO` 통합 문서 저장과 같은 파일 작업에 사용됩니다.
이제 Aspose.Cells를 사용하여 워크시트 내의 셀과 범위를 보호하는 단계를 살펴보겠습니다.
## 1단계: 환경 설정
먼저 Excel 파일을 저장할 디렉터리를 만드세요. 디렉터리가 없으면 새로 만들겠습니다. 이렇게 하면 출력 파일을 저장할 공간이 확보됩니다.
```csharp
// 문서 디렉토리 경로를 정의하세요
string dataDir = "Your Document Directory";
// 디렉토리가 존재하는지 확인하고, 존재하지 않으면 디렉토리를 생성합니다.
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
여기서 우리는 사용하고 있습니다 `System.IO.Directory.Exists()` 폴더가 존재하는지 확인하고, 존재하지 않으면 다음을 사용하여 폴더를 생성합니다. `Directory.CreateDirectory()`.
## 2단계: 새 통합 문서 만들기
이제 새 Workbook 객체를 인스턴스화해 보겠습니다. 이 객체는 셀과 범위를 정의하는 Excel 파일로 사용됩니다.
```csharp
// 새 Workbook 개체 인스턴스화
Workbook book = new Workbook();
```
그만큼 `Workbook` 클래스는 Aspose.Cells에서 Excel 파일을 작업하기 위한 진입점입니다. Excel 문서를 나타냅니다.
## 3단계: 기본 워크시트에 액세스
새로 만든 모든 통합 문서에는 기본 워크시트가 있습니다. 이 워크시트를 가져와서 내용을 작업해 보겠습니다.
```csharp
// 통합 문서의 첫 번째(기본) 워크시트 가져오기
Worksheet sheet = book.Worksheets[0];
```
여기, `Worksheets[0]` 통합 문서의 첫 번째 시트가 제공됩니다(인덱싱은 0부터 시작).
## 4단계: 편집 가능한 범위 정의
사용자가 특정 셀을 편집할 수 있도록 하면서 워크시트의 특정 부분을 보호하려면 편집 가능한 범위를 정의해야 합니다. 편집 가능한 범위를 만들어 워크시트의 AllowEditRanges 컬렉션에 추가하겠습니다.
```csharp
// AllowEditRanges 컬렉션 가져오기
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// ProtectedRange를 정의하고 컬렉션에 추가합니다.
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
위의 코드에서:
- `"r2"` 편집 가능한 범위의 이름입니다.
- 숫자 `1, 1, 3, 3` 범위에 대한 시작 및 끝 행과 열 인덱스를 나타냅니다(예: 셀 B2부터 D4까지).
## 5단계: 보호된 범위에 대한 암호 설정
이제 편집 가능 범위를 정의했으니, 비밀번호를 추가하여 보호해 보겠습니다. 즉, 사용자가 이 특정 범위를 편집하려면 비밀번호가 필요합니다.
```csharp
// 편집 가능한 범위에 대한 비밀번호를 지정하세요
protectedRange.Password = "123";
```
여기서는 비밀번호를 다음과 같이 설정했습니다. `"123"`하지만 안전한 비밀번호를 선택하실 수 있습니다. 이 단계는 편집 가능한 영역에 대한 접근을 제어하는 데 필수적입니다.
## 6단계: 시트 전체 보호
이 단계에서는 전체 워크시트를 보호합니다. 워크시트를 보호하면 허용된 범위를 제외한 시트의 다른 부분은 편집할 수 없습니다.
```csharp
// 지정된 보호 유형(전체)으로 시트를 보호합니다.
sheet.Protect(ProtectionType.All);
```
이렇게 하면 편집 가능한 범위에 있는 셀을 제외하고 시트의 모든 셀이 잠깁니다.
## 7단계: 통합 문서 저장
마지막으로 통합 문서를 파일로 저장합니다. 보호된 시트는 지정한 이름으로 저장됩니다.
```csharp
// 지정된 디렉토리에 Excel 파일을 저장합니다.
book.Save(dataDir + "protectedrange.out.xls");
```
여기서 Excel 파일은 다음과 같이 저장됩니다. `protectedrange.out.xls` 이전에 정의한 디렉터리에 저장합니다. 다른 이름이나 형식으로 저장하려면 파일 이름과 확장자를 수정하면 됩니다.
## 결론
이 튜토리얼을 따라 Aspose.Cells for .NET을 사용하여 Excel 워크시트의 셀과 범위를 보호하는 방법을 알아보았습니다. 이 방법을 사용하면 스프레드시트에서 편집 가능한 영역과 편집 불가능한 영역을 유연하게 제어할 수 있습니다. 이제 이러한 기술을 직접 프로젝트에 적용하여 민감한 데이터를 안전하게 보호하면서 사용자에게 편집 가능한 영역을 제공할 수 있습니다.
Aspose.Cells는 Excel 파일을 작업하는 데 필요한 강력한 도구 세트를 제공하며, 이는 Aspose.Cells를 사용하여 할 수 있는 많은 작업 중 하나일 뿐입니다. 
## 자주 묻는 질문
### 워크시트에서 특정 셀만 보호할 수 있나요?
네, 다음을 사용하여 `AllowEditRanges` 속성을 사용하면 워크시트의 나머지 부분은 보호된 채로 어떤 셀이나 범위만 편집할 수 있는지 지정할 수 있습니다.
### 나중에 보호를 해제할 수 있나요?
예, 다음을 사용하여 워크시트의 보호를 해제할 수 있습니다. `Unprotect()` 방법이고, 비밀번호가 설정된 경우 비밀번호를 제공해야 합니다.
### 비밀번호로 시트 전체를 보호하려면 어떻게 해야 하나요?
시트 전체를 보호하려면 다음을 사용하면 됩니다. `Protect()` 비밀번호가 있거나 없는 방식입니다. 예를 들어, `sheet.Protect("password")`.
### 편집 가능한 범위를 여러 개 추가할 수 있나요?
물론입니다! 필요한 만큼 편집 가능한 범위를 추가하려면 다음을 호출하세요. `allowRanges.Add()` 여러 번.
### Aspose.Cells는 어떤 다른 보안 기능을 제공하나요?
Aspose.Cells는 통합 문서 암호화, 파일 암호 설정, 셀 및 시트 보호 등 다양한 보안 기능을 지원합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}