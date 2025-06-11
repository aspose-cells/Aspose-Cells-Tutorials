---
"description": "Aspose.Cells for .NET을 사용하여 Excel에서 이미지를 비례적으로 배치하는 방법을 알아보세요. 스프레드시트를 더욱 시각적으로 멋지게 만들어 보세요."
"linktitle": "Excel에서 그림 위치(비례)"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Excel에서 그림 위치(비례)"
"url": "/ko/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 그림 위치(비례)

## 소개
Excel 스프레드시트에 딱 맞지 않는 픽셀화된 이미지에 지치셨나요? 다음과 같은 상황을 상상해 보세요. Excel 시트에 눈에 띄게 표시해야 할 아름다운 로고가 있는데, 결국 찌그러지거나 늘어나거나 제대로 배치되지 않은 경우가 있습니다. 누구도 이런 상황을 원하지 않죠! 자, 그럼 자리를 잡으세요. 오늘은 .NET용 Aspose.Cells 라이브러리를 사용하여 Excel에서 이미지를 비례적으로 배치하는 방법을 배우게 될 겁니다. 이 강력한 라이브러리를 사용하면 보고서 작성, 데이터 분석 또는 프레젠테이션을 더욱 돋보이게 하는 등 Excel 파일을 손쉽게 조작할 수 있습니다. 이제 사진을 완벽하게 정렬하는 방법을 자세히 알아보겠습니다!
## 필수 조건
실제 코딩에 들어가기 전에 컴퓨터에 설정해야 할 몇 가지 사항이 있습니다.
1. Visual Studio: .NET 프로젝트에 편리한 환경을 제공하므로 Visual Studio가 설치되어 있는지 확인하세요.
2. Aspose.Cells 라이브러리: Aspose.Cells 라이브러리가 필요합니다. 무료 체험판을 이용하거나 다음에서 구매할 수 있습니다. [Aspose 웹사이트](https://purchase.aspose.com/buy).
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 약간의 지식은 우리가 논의할 예제를 이해하는 데 큰 도움이 될 것입니다.
4. 이미지 파일: Excel 시트에 삽입할 이미지(로고 등)를 준비하세요.
이제 모든 것을 준비했으니 코딩을 시작해 보겠습니다!
## 패키지 가져오기
프로젝트에서 Aspose.Cells를 사용하려면 특정 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.
### 새 프로젝트 만들기
Visual Studio에서 새 프로젝트를 만듭니다.
- Visual Studio를 엽니다.
- "새 프로젝트 만들기"를 클릭하세요.
- 기본 설정에 따라 "클래스 라이브러리(.NET Framework)" 또는 "콘솔 응용 프로그램"을 선택하세요.
### Aspose.Cells 설치
NuGet을 통해 프로젝트에 Aspose.Cells 패키지를 추가할 수 있습니다. 방법은 다음과 같습니다.
- 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
- "NuGet 패키지 관리"를 선택하세요.
- "Aspose.Cells"를 검색하고 "설치"를 클릭합니다.
### 지시어를 사용하여 추가
코드 파일의 맨 위에 다음 지침을 포함하세요.
```csharp
using System.IO;
using Aspose.Cells;
```
이러한 지침을 사용하면 Excel 파일을 조작하는 데 필요한 클래스에 액세스할 수 있습니다.
이제 Excel에서 이미지를 비율에 맞게 성공적으로 배치하기 위한 자세한 단계를 살펴보겠습니다.
## 1단계: 디렉토리 설정
먼저, 문서를 보관할 폴더를 지정하세요. 폴더가 없는 경우, 다음과 같이 폴더를 만드세요.
```csharp
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 새로 만듭니다.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 스니펫은 Excel 파일을 저장할 새 디렉터리(존재하지 않는 경우)를 만듭니다. 다음 내용을 바꾸세요. `"Your Document Directory"` 파일을 저장하려는 실제 경로를 입력합니다.
## 2단계: 통합 문서 인스턴스화
다음으로, 새로운 통합 문서를 만들어 보겠습니다.
```csharp
Workbook workbook = new Workbook();
```
이 줄은 새 통합 문서 개체를 초기화하여 작업할 수 있는 빈 캔버스를 제공합니다.
## 3단계: 새 워크시트 추가
이제 통합 문서를 설정했으니 여기에 새 워크시트를 추가해 보겠습니다.
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
이렇게 하면 새 워크시트가 추가되고 해당 시트의 인덱스가 반환됩니다. 이 인덱스를 사용하여 나중에 조작할 수 있습니다.
## 4단계: 새 워크시트에 액세스
새로 추가된 워크시트를 조작하려면 워크시트에 액세스해야 합니다.
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
지금, `worksheet` 해당 시트에 콘텐츠와 이미지를 추가할 수 있습니다.
## 5단계: 그림 삽입
이제 신나는 순간입니다! 아름다운 이미지를 추가해 보세요. `"logo.jpg"` 이미지 파일 이름으로:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
이 줄은 셀 F6에 이미지를 추가합니다(행과 열은 0부터 인덱싱되므로) `5` (여섯 번째 셀을 가리킴)
## 6단계: 추가된 사진에 액세스
이미지를 삽입하면 다음과 같이 액세스할 수 있습니다.
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
이를 통해 그림 속성을 조작할 수 있습니다.
## 7단계: 그림을 비율에 맞게 배치
이제 그림을 비율에 맞게 배치해 보겠습니다.
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
여기, `UpperDeltaX` 그리고 `UpperDeltaY` 셀 크기에 따라 이미지의 위치를 조정하세요. 이 값을 조정하여 원하는 이미지를 얻을 수 있습니다.
## 8단계: 변경 사항 저장
마지막으로, 모든 변경 사항을 보존하려면 통합 문서를 저장하세요.
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
이 줄은 통합 문서를 다음과 같이 저장합니다. `book1.out.xls` 지정된 디렉토리에 보관하세요.
## 결론
자, 이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel에서 그림을 비례적으로 배치하는 방법을 방금 배웠습니다. 단순히 이미지를 삽입하는 것이 아니라, 스프레드시트에서 이미지를 완벽하게 보이게 하는 것입니다. 잘 배치된 그림은 데이터 프레젠테이션의 완성도를 크게 높여준다는 점을 기억하세요.
다양한 이미지와 배치를 실험해 보세요. Aspose.Cells의 풍부한 기능을 더욱 깊이 있게 살펴보는 것도 좋습니다. Excel 시트가 완전히 새롭게 바뀔 거예요!
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 사용자가 Microsoft Excel을 설치하지 않고도 Excel 파일을 만들고, 조작하고, 변환할 수 있는 강력한 .NET용 라이브러리입니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
예, Aspose.Cells에서는 무료 평가판을 제공하며 이를 다운로드할 수 있습니다. [여기](https://releases.aspose.com/).
### 문서는 어디서 찾을 수 있나요?
포괄적인 정보에 접근할 수 있습니다. [선적 서류 비치](https://reference.aspose.com/cells/net/) Aspose.Cells용.
### Aspose.Cells는 모든 이미지 형식을 지원합니까?
Aspose.Cells는 JPEG, PNG, BMP, GIF, TIFF 등 다양한 형식을 지원합니다.
### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
문의사항이 있으시면 언제든지 방문해 주세요. [지원 포럼](https://forum.aspose.com/c/cells/9) 질문을 할 수 있는 곳입니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}