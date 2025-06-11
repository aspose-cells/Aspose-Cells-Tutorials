---
"description": "Aspose.Cells for .NET을 사용하여 Excel에서 PDF로 변환할 때 외부 리소스를 제어하는 방법을 쉽게 따라할 수 있는 가이드를 통해 알아보세요."
"linktitle": "Aspose.Cells에서 Excel의 외부 리소스를 PDF로 제어"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Aspose.Cells에서 Excel의 외부 리소스를 PDF로 제어"
"url": "/ko/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells에서 Excel의 외부 리소스를 PDF로 제어

## 소개
오늘날 디지털 시대에 Excel 스프레드시트를 PDF 문서로 변환하는 것은 흔한 일입니다. 보고서, 재무 데이터, 프레젠테이션 자료 등 어떤 자료를 준비하든 PDF가 의도한 대로 정확하게 표시되도록 해야 합니다. Aspose.Cells for .NET은 특히 Excel 파일에 포함된 이미지와 같은 외부 리소스를 처리할 때 이 변환 과정을 세세한 부분까지 제어할 수 있는 강력한 라이브러리입니다. 이 가이드에서는 Aspose.Cells를 사용하여 Excel을 PDF로 변환하는 과정에서 외부 리소스를 제어하는 방법을 자세히 알아보겠습니다. 자, 좋아하는 음료를 준비하고 시작해 볼까요!
## 필수 조건
본격적으로 시작하기 전에, 시작하는 데 필요한 모든 것을 갖추고 있는지 확인해 볼까요? 간단한 체크리스트는 다음과 같습니다.
1. Visual Studio나 .NET 호환 IDE: 코드를 작성하고 테스트할 수 있는 환경이 필요합니다.
2. .NET용 Aspose.Cells: 아직 설치하지 않았다면 다음으로 이동하세요. [Aspose 다운로드](https://releases.aspose.com/cells/net/) 페이지로 가서 최신 버전을 다운로드하세요.
3. C# 기본 지식: C# 프로그래밍 언어에 대한 지식이 있으면 도움이 됩니다. 모르는 개념이 있으면 언제든지 찾아보세요.
4. 샘플 Excel 파일: 변환하려는 외부 리소스가 포함된 Excel 파일을 준비하세요. 제공된 샘플 파일 "samplePdfSaveOptions_StreamProvider.xlsx"를 사용할 수 있습니다.
5. 테스트용 이미지 파일: 변환 과정에서 외부 리소스로 사용됩니다. "newPdfSaveOptions_StreamProvider.png" 이미지 파일을 사용해 보세요.
## 패키지 가져오기
시작하려면 Aspose.Cells 라이브러리에서 필요한 네임스페이스를 가져와야 합니다. 이는 라이브러리의 기능에 접근하는 데 매우 중요합니다. 파일 맨 위에 다음 using 지시문을 추가하세요.
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
이러한 패키지는 작업을 수행하는 데 필요한 모든 필수 클래스와 메서드를 제공합니다.
## 1단계: 스트림 공급자 클래스 만들기
첫 번째 업무 순서는 다음을 구현하는 스트림 공급자 클래스를 만드는 것입니다. `IStreamProvider` 인터페이스. 이 클래스를 사용하면 외부 리소스가 로드되는 방식을 제어할 수 있습니다.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // 메모리 스트림에서 새 이미지를 읽고 Stream 속성에 할당합니다.
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
이 수업에서는:
- CloseStream: 이 메서드는 스트림이 닫힐 때 호출됩니다. 지금은 추적을 위한 디버그 메시지만 작성합니다.
- InitStream: 마법이 시작되는 곳입니다. 여기서 외부 이미지를 바이트 배열로 읽어 메모리 스트림으로 변환한 후 `options.Stream` 재산.
## 2단계: 소스 및 출력 디렉토리 설정
이제 스트림 제공자가 준비되었으므로 Excel 파일이 있는 위치와 PDF를 저장할 위치를 설정할 차례입니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
간단히 교체하세요 `"Your Document Directory"` 파일이 있는 컴퓨터의 실제 경로를 확인하세요. 파일을 정리하는 것이 중요합니다!
## 3단계: Excel 파일 로드
다음으로, PDF를 만들려는 Excel 파일을 로드합니다.
```csharp
// 외부 이미지가 포함된 원본 Excel 파일 로드
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
우리는 사용하고 있습니다 `Workbook` Excel 파일을 나타내는 Aspose.Cells의 클래스입니다. 이 파일에는 변환 중에 제어하려는 이미지와 같은 다양한 외부 리소스가 포함될 수 있습니다.
## 4단계: PDF 저장 옵션 설정
통합 문서를 PDF로 저장하기 전에 저장 방식을 지정해 보겠습니다. 필요에 따라 이러한 옵션을 조정할 수 있습니다.
```csharp
// PDF 저장 옵션 지정 - 스트림 제공자
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // 각 시트를 새 페이지에 저장하세요
```
여기서 우리는 새로운 인스턴스를 만들고 있습니다. `PdfSaveOptions`PDF 형식을 사용자 지정할 수 있는 기능입니다. `OnePagePerSheet` 이 옵션은 각 Excel 시트가 최종 PDF에서 별도의 페이지를 차지하도록 보장하는 데 유용합니다.
## 5단계: 스트림 공급자 지정
PDF 옵션을 설정한 후에는 Aspose에서 외부 리소스에 대해 사용자 정의 스트림 공급자를 사용하도록 지정해야 합니다.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
이 선은 당신을 연결합니다 `Workbook` 인스턴스와 함께 `MyStreamProvider` 이전에 생성한 클래스입니다. 즉, 변환 중에 외부 리소스가 발생할 때마다 제공자가 지정된 대로 해당 리소스를 처리합니다.
## 6단계: 통합 문서를 PDF로 저장
모든 것이 설정되었으니 마침내 Excel 통합 문서를 PDF로 저장할 차례입니다.
```csharp
// 통합 문서를 PDF로 저장
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
호출하여 `Save` 통합 문서 개체에 메서드를 사용하고 PDF 옵션과 함께 출력 디렉터리를 전달하면 Excel 파일이 아름답게 포맷된 PDF로 변환됩니다.
## 7단계: 성공적인 실행 확인
마무리로, 여러분의 과정이 성공적으로 진행되었는지 확인하는 것이 좋습니다!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
콘솔에 성공 메시지를 출력하면 작업 상태를 파악하는 데 도움이 됩니다. 코드에 이러한 간단한 확인 메시지를 포함하는 것이 좋습니다.
## 결론
자, 이제 끝났습니다! Aspose.Cells를 사용하여 Excel에서 PDF로 변환하는 동안 외부 리소스 처리 방식을 전문적으로 제어할 수 있습니다. 즉, 이제 문서에 이미지 및 기타 외부 요소를 정확하게 포함할 수 있어 항상 세련된 최종 결과물을 얻을 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?  
Aspose.Cells는 다양한 형식의 Excel 파일을 만들고, 조작하고, 변환하고, 렌더링할 수 있는 .NET 개발자를 위한 강력한 라이브러리입니다.
### Aspose.Cells를 어떻게 다운로드하나요?  
Aspose.Cells의 최신 버전을 다음에서 다운로드할 수 있습니다. [다운로드 링크](https://releases.aspose.com/cells/net/).
### Aspose.Cells를 무료로 사용해 볼 수 있나요?  
네! 다음 사이트를 방문하시면 무료 체험판을 받으실 수 있습니다. [무료 체험 페이지](https://releases.aspose.com/).
### Aspose.Cells에 대한 지원은 어디에서 찾을 수 있나요?  
지원 관련 문의사항은 다음 웹사이트를 방문하세요. [Aspose 지원 포럼](https://forum.aspose.com/c/cells/9).
### Aspose.Cells에 대한 임시 라이선스를 어떻게 얻을 수 있나요?  
임시면허를 신청할 수 있습니다 [여기](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}