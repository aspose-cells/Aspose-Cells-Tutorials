---
"description": "Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 편집 가능한 범위를 만드는 방법을 배우고, 워크시트 보호 기능으로 나머지 셀을 보호하면서 특정 셀만 편집 가능하도록 설정합니다."
"linktitle": "Aspose.Cells를 사용하여 사용자가 워크시트의 범위를 편집하도록 허용"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Aspose.Cells를 사용하여 사용자가 워크시트의 범위를 편집하도록 허용"
"url": "/ko/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 사용자가 워크시트의 범위를 편집하도록 허용

## 소개
Excel 문서에는 원치 않는 편집으로부터 보호해야 할 민감한 데이터나 구조화된 콘텐츠가 포함된 경우가 많습니다. 하지만 특정 사용자가 편집할 수 있도록 특정 셀이나 범위를 설정해야 할 수도 있습니다. Aspose.Cells for .NET은 지정된 범위에 대한 편집 권한을 부여하면서도 전체 워크시트를 보호할 수 있는 강력한 도구입니다. 특정 셀만 편집 가능하고 다른 셀은 안전하게 보호되는 예산 스프레드시트를 공유한다고 생각해 보세요. Aspose.Cells는 이러한 작업을 쉽고 효율적으로 처리해 줍니다.
## 필수 조건
코딩 부분으로 들어가기 전에 필요한 모든 것이 있는지 확인해 보겠습니다.
- Aspose.Cells for .NET: Aspose.Cells for .NET 라이브러리가 설치되어 있는지 확인하세요. 다운로드할 수 있습니다. [여기](https://releases.aspose.com/cells/net/).
- 개발 환경: Visual Studio 또는 C# 호환 IDE.
- .NET Framework: 버전 4.0 이상.
- 면허: 재판 제한을 피하려면 면허 취득을 고려하세요. [여기 임시 면허증](https://purchase.aspose.com/temporary-license/).
## 패키지 가져오기
코드 시작 부분에 필요한 Aspose.Cells 네임스페이스를 포함해야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이렇게 하면 Excel 파일에서 보호된 범위를 설정하는 데 필요한 모든 클래스와 메서드에 액세스할 수 있습니다.
이제 기초가 마련되었으니, 코드를 한 단계씩 자세히 살펴보겠습니다.
## 1단계: 디렉토리 설정
파일 작업을 시작하기 전에 Excel 파일을 저장할 디렉터리를 설정해야 합니다. 이렇게 하면 파일이 체계적으로 정리되고 안전하게 저장됩니다.
```csharp
// 문서 디렉토리 경로를 정의하세요
string dataDir = "Your Document Directory";
// 디렉토리가 존재하는지 확인하고, 존재하지 않으면 디렉토리를 생성합니다.
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
이 코드 부분은 디렉터리가 파일 작업을 수행할 준비가 되었는지 확인합니다. 이후의 모든 작업의 기반을 마련하는 것이라고 생각하면 됩니다.
## 2단계: 통합 문서 및 워크시트 초기화
이제 새로운 통합 문서를 만들고 기본 워크시트에 액세스하여 계속 진행해 보겠습니다.
```csharp
// 새 통합 문서 초기화
Workbook book = new Workbook();
// 통합 문서의 첫 번째 워크시트에 액세스합니다.
Worksheet sheet = book.Worksheets[0];
```
여기서는 Excel 통합 문서를 초기화하고 그 안의 첫 번째 워크시트를 선택합니다. 이 워크시트는 보호 설정을 적용하고 편집 가능한 범위를 정의하는 캔버스 역할을 합니다.
## 3단계: 편집 범위 허용 컬렉션에 액세스
Aspose.Cells에는 다음과 같은 기능이 있습니다. `AllowEditRanges`이는 워크시트가 보호되어 있어도 편집할 수 있는 범위의 모음입니다.
```csharp
// 편집 범위 허용 컬렉션에 액세스
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
이 줄은 편집 가능한 특정 범위 모음에 대한 액세스를 설정합니다. 워크시트의 "VIP" 영역이라고 생각하면 되는데, 특정 범위만 보호를 우회할 수 있습니다.
## 4단계: 보호 범위 정의 및 생성
이제 워크시트에 보호된 범위를 정의하고 만들어 보겠습니다. 이 범위의 시작 셀과 끝 셀을 지정합니다.
```csharp
// ProtectedRange 변수 정의
ProtectedRange protectedRange;
// 특정 이름과 셀 위치를 사용하여 컬렉션에 새 범위를 추가합니다.
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
이 코드 블록에서:
- `EditableRange` 범위에 지정된 이름입니다.
- 숫자 (1, 1, 3, 3)은 범위 좌표를 정의합니다. 즉, 셀 B2(행 1, 열 1)에서 셀 D4(행 3, 열 3)까지입니다.
## 5단계: 보호된 범위에 대한 암호 설정
보안을 강화하려면 보호된 범위에 비밀번호를 설정할 수 있습니다. 이 단계를 통해 권한이 있는 사용자만 범위를 편집할 수 있도록 보안을 강화할 수 있습니다.
```csharp
// 편집 가능한 범위에 대한 암호를 설정하세요
protectedRange.Password = "123";
```
여기서 우리는 비밀번호를 추가했습니다 (`"123"`)을 보호된 범위로 설정합니다. 이 암호 요구 사항은 누가 변경할 수 있는지에 대한 추가적인 제어 수준을 제공합니다.
## 6단계: 워크시트 보호
편집 가능 범위가 설정되었으므로 다음 단계는 전체 워크시트를 보호하는 것입니다. 이 보호 설정을 사용하면 정의된 범위 밖의 모든 셀이 잠기고 편집할 수 없게 됩니다.
```csharp
// 워크시트에 보호를 적용하여 다른 모든 셀을 편집할 수 없게 합니다.
sheet.Protect(ProtectionType.All);
```
그만큼 `Protect` 이 메서드는 편집 가능으로 정의한 범위를 제외한 전체 워크시트를 잠급니다. 이 단계는 기본적으로 필요에 따라 특정 셀에 접근할 수 있는 안전한 "읽기 전용" 환경을 만듭니다.
## 7단계: 통합 문서 저장
마지막 단계는 통합 문서를 저장하는 것입니다. 이렇게 하면 설정이 적용되고 저장됩니다.
```csharp
// 지정된 디렉토리에 Excel 파일을 저장합니다.
book.Save(dataDir + "protectedrange.out.xls");
```
이 단계에서는 1단계에서 설정한 디렉터리에 통합 문서를 "protectedrange.out.xls"라는 이름으로 저장합니다. 이제 특정 범위만 편집할 수 있는 완벽한 기능과 보안을 갖춘 Excel 파일이 생겼습니다!
## 결론
Aspose.Cells for .NET은 Excel 파일 내에서 보호 및 권한을 관리하는 탁월한 방법을 제공합니다. 편집 가능한 범위를 생성하면 특정 영역에 대한 접근 권한을 유지하면서도 워크시트를 보호할 수 있습니다. 이 기능은 특히 일부 셀만 편집을 위해 열어두고 다른 셀은 잠가두어야 하는 공동 작업 문서에 유용합니다.
## 자주 묻는 질문
### 워크시트에 여러 개의 편집 가능한 범위를 추가할 수 있나요?
예, 간단히 반복하여 여러 범위를 추가할 수 있습니다. `allowRanges.Add()` 새로운 범위마다 다른 방법을 사용합니다.
### 나중에 보호된 범위를 제거하려면 어떻게 해야 하나요?
사용하세요 `allowRanges.RemoveAt()` 제거하려는 범위의 인덱스를 사용하는 방법입니다.
### 각 범위마다 다른 비밀번호를 설정할 수 있나요?
물론입니다. 각각 `ProtectedRange` 고유한 비밀번호를 사용하여 세부적인 제어가 가능합니다.
### 편집 가능한 범위 없이 워크시트를 보호하면 어떻게 되나요?
편집 가능한 범위를 정의하지 않으면 보호된 워크시트 전체를 편집할 수 없습니다.
### 보호된 범위는 다른 사용자에게도 표시됩니까?
아니요, 보호는 내부적으로 적용됩니다. 사용자가 보호된 영역을 편집하려고 할 때만 비밀번호를 입력하라는 메시지가 표시됩니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}