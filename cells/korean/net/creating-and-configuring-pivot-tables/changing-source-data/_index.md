---
"description": "Aspose.Cells for .NET을 사용하여 피벗 테이블 소스 데이터를 프로그래밍 방식으로 변경하는 방법을 단계별로 자세히 안내하는 포괄적인 튜토리얼을 통해 알아보세요."
"linktitle": ".NET에서 피벗 테이블의 소스 데이터를 프로그래밍 방식으로 변경"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": ".NET에서 피벗 테이블의 소스 데이터를 프로그래밍 방식으로 변경"
"url": "/ko/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 피벗 테이블의 소스 데이터를 프로그래밍 방식으로 변경

## 소개
데이터 분석 세계에서 Microsoft Excel만큼 빛나는 도구는 드뭅니다. 매일 수많은 사용자가 데이터를 관리하고 분석하기 위해 Excel을 사용하지만, 그 이면에는 단순한 클릭과 드래그보다 훨씬 더 복잡한 과정이 존재합니다. Excel 파일을 프로그래밍 방식으로 조작하고, 특히 피벗 테이블의 원본 데이터를 변경하고 싶었던 적이 있다면, 바로 여기가 정답입니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 이러한 작업을 수행하는 방법을 살펴보겠습니다. 숙련된 개발자든 프로그래밍 세계에 발을 들여놓은 초보자든, 이 튜토리얼에는 따라 하기 쉬운 유용한 정보가 가득합니다.
## 필수 조건
피벗 테이블의 원본 데이터를 변경하는 과정을 시작하기에 앞서 모든 것이 설정되어 있고 준비가 되었는지 확인해 보겠습니다.
1. Visual Studio: 여기에서 코드를 작성할 것이므로 Microsoft Visual Studio가 설치되어 있는지 확인하세요.
2. Aspose.Cells 라이브러리: Aspose.Cells 라이브러리를 다운로드하여 프로젝트에 참조해야 합니다. 다운로드할 수 있습니다. [여기](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: 이 튜토리얼은 간단하지만 C#에 대한 이해가 있으면 코드를 더 잘 이해하는 데 도움이 됩니다.
4. Excel 파일: 조작할 수 있는 피벗 테이블이 포함된 샘플 Excel 파일(예: "Book1.xlsx")이 있어야 합니다.
좋습니다. 이러한 전제 조건을 확인했으니, 이제 필요한 패키지를 가져와서 코딩을 시작해 보겠습니다!
## 패키지 가져오기
먼저 필요한 패키지를 가져오겠습니다. Visual Studio에서 C# 프로젝트를 열고 코드 파일 맨 위에 다음 using 지시문을 추가합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
이러한 네임스페이스를 사용하면 Aspose.Cells를 사용하여 Excel 파일을 작업하고 해당 내용을 조작하는 데 필요한 필수 클래스에 액세스할 수 있습니다.

이제 이 과정을 관리 가능한 단계로 나누어 보겠습니다. Excel 파일을 열고, 워크시트를 수정하고, 피벗 테이블의 데이터 원본을 변경하고, 결과를 저장하는 과정을 살펴보겠습니다.
## 1단계: 문서 디렉터리 정의
먼저 Excel 파일의 위치를 지정해야 합니다. `dataDir` "Book1.xlsx"가 들어 있는 폴더를 가리키는 변수입니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
이 줄은 Excel 파일이 저장되는 디렉토리를 설정하여 나중에 쉽게 액세스할 수 있도록 합니다.
## 2단계: 입력 경로 지정
다음으로, 입력 Excel 파일의 전체 경로를 지정하는 문자열을 만들어 보겠습니다.
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
이렇게 하면 파일 접근이 간소화되고, 코드 전체에서 같은 경로를 여러 번 입력할 필요가 없습니다.
## 3단계: 파일 스트림 만들기
이제 Excel 파일을 열 차례입니다. `FileStream` Excel 파일의 내용을 읽을 수 있습니다.
```csharp
// 열려는 Excel 파일을 포함하는 파일 스트림 생성
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
이 줄은 파일을 읽기 모드로 열어서 데이터에 접근할 수 있게 해줍니다.
## 4단계: 통합 문서 로드
파일 스트림이 준비되면 다음 단계는 통합 문서를 로드하는 것입니다.
```csharp
// 파일 스트림을 통해 Excel 파일 열기
Workbook workbook = new Workbook(fstream);
```
이 명령은 Excel 파일을 가져와서 로드합니다. `Workbook` 객체입니다. 로드가 완료되면 필요에 따라 파일을 조작할 수 있습니다.
## 5단계: 워크시트에 액세스
이제 세부 사항을 살펴볼 차례입니다. 워크북의 첫 번째 워크시트를 살펴보겠습니다.
```csharp
// Excel 파일의 첫 번째 워크시트에 액세스하기
Worksheet worksheet = workbook.Worksheets[0];
```
이렇게 하면 첫 번째 워크시트의 데이터에 직접 접근하여 쉽게 수정할 수 있습니다.
## 6단계: 새 데이터 채우기
다음으로, 셀에 새 데이터를 삽입해 보겠습니다. 이 예시에서는 몇 가지 샘플 데이터를 추가해 보겠습니다.
```csharp
// 워크시트 셀에 새 데이터 채우기
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
여기서는 "Golf", "Qtr4" 및 `7000` 특정 셀에 값을 입력합니다. 필요에 따라 이 값을 변경할 수 있습니다.
## 7단계: 명명된 범위 변경
이제 피벗 테이블이 참조하는 명명된 범위를 변경해 보겠습니다. 이 작업에는 범위를 만들거나 업데이트하는 작업이 포함됩니다.
```csharp
// 명명된 범위 "DataSource" 변경
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
새로운 범위를 정의하면 피벗 테이블이 새로 고침될 때 이 새로운 데이터를 사용하도록 할 수 있습니다.
## 8단계: 수정된 Excel 파일 저장
모든 변경 사항을 적용한 후에는 반드시 작업 내용을 저장해야 합니다! 수정된 통합 문서를 저장해 보겠습니다.
```csharp
// 수정된 Excel 파일 저장
workbook.Save(dataDir + "output.xls");
```
이 명령을 사용하면 통합 문서가 새 파일에 저장되므로 원하지 않는 한 원본 파일을 덮어쓰지 않아도 됩니다!
## 9단계: 파일 스트림 닫기
마지막으로, 사용 중인 리소스를 해제하려면 파일 스트림을 닫는 것이 필수입니다.
```csharp
// 모든 리소스를 해제하기 위해 파일 스트림을 닫습니다.
fstream.Close();
```
이 단계를 거치면 애플리케이션의 메모리 누수가 발생하지 않고 효율성이 유지됩니다.
## 결론
축하합니다! Aspose.Cells를 사용하여 .NET에서 피벗 테이블의 원본 데이터를 프로그래밍 방식으로 성공적으로 변경했습니다. 이 기능은 Excel 작업을 자동화하고 워크플로를 개선할 수 있는 다양한 가능성을 열어줍니다. 재무 보고서를 업데이트하거나, 판매 데이터를 추적하거나, 단순히 데이터 세트를 조작하는 등 어떤 작업이든 프로그래밍 방식으로 이 작업을 수행할 수 있다면 시간을 크게 절약하고 오류 위험을 줄일 수 있습니다.

## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 Excel 파일을 다루기 위한 강력한 .NET 라이브러리로, 사용자가 Excel 문서를 프로그래밍 방식으로 만들고, 수정하고, 조작할 수 있도록 해줍니다.
### 이 방법을 사용하여 기존 피벗 테이블의 소스 데이터를 변경할 수 있나요?
물론입니다! 이 방법을 사용하면 Excel 통합 문서 내 기존 피벗 테이블의 데이터 소스를 업데이트할 수 있습니다.
### Aspose.Cells를 사용하려면 Office를 설치해야 합니까?
아니요! Aspose.Cells는 독립형 라이브러리이므로 Excel 파일을 사용하는 데 Microsoft Office가 설치되어 있지 않아도 됩니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 무료 체험판을 제공하지만, 모든 기능을 사용하려면 라이선스를 구매해야 합니다. 자세한 내용은 여기에서 확인하세요. [여기](https://purchase.aspose.com/buy).
### 더 많은 예와 지원은 어디에서 찾을 수 있나요?
더 많은 예와 지원을 보려면 다음을 확인하세요. [Aspose.Cells 문서](https://reference.aspose.com/cells/net/) 그리고 그들의 커뮤니티 포럼 [여기](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}