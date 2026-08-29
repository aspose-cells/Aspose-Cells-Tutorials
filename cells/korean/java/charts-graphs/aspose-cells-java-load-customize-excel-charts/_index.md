---
date: '2026-06-12'
description: Aspose.Cells Java를 사용하여 차트를 PNG로 내보내는 방법을 배우고, 차트 이미지를 생성하고, Excel 차트를
  PNG로 렌더링하며, 시각화를 효율적으로 맞춤 설정하는 방법을 알아보세요.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: Aspose.Cells Java를 사용하여 차트를 PNG로 내보내기
url: /ko/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java를 사용하여 차트를 PNG로 내보내기

## 소개

차트를 PNG로 내보내는 것은 보고서, 프레젠테이션 또는 웹 페이지에 시각 데이터를 삽입해야 할 때 흔히 요구되는 작업입니다. **Aspose.Cells for Java**를 사용하면 기존 Excel 워크북을 로드하고, 차트 데이터를 새로 고치며, 글로벌화 설정을 적용하고, 차트를 고품질 PNG 이미지로 직접 렌더링할 수 있습니다—Microsoft Excel이 설치되어 있지 않아도 됩니다. 이 튜토리얼에서는 **차트를 PNG로 내보내는** 방법, 차트 이미지를 프로그래밍 방식으로 생성하는 방법, 그리고 전 세계 사용자를 위한 출력 맞춤 방법을 알아봅니다.

## 빠른 답변
- **차트를 PNG로 내보내려면 어떻게 해야 하나요?** 워크북을 로드하고 차트에 접근한 뒤, `ImageOrPrintOptions`를 PNG로 설정하고 `chart.toImage()`를 호출합니다.  
- **Java 차트 이미지 생성을 지원하는 라이브러리는 무엇인가요?** Aspose.Cells for Java는 Excel 차트를 이미지로 렌더링하기 위한 완전한 API를 제공합니다.  
- **PNG 내보내기에 라이선스가 필요합니까?** 무료 체험으로도 가능하지만, 상용 라이선스를 사용하면 평가 제한이 해제됩니다.  
- **숫자 형식을 전역적으로 사용자 정의할 수 있나요?** 예, 렌더링 전에 `Workbook.getSettings().setGlobalizationSettings()`를 사용하면 됩니다.  
- **PNG만 지원하나요?** 아니요, 이미지 형식 옵션을 변경하면 JPEG, BMP, TIFF 등으로도 렌더링할 수 있습니다.

## Aspose.Cells for Java란?
`Aspose.Cells for Java`는 **Java 기반 스프레드시트 처리 라이브러리**로, 개발자가 Microsoft Office 없이도 Excel 파일을 생성, 수정, 변환 및 렌더링할 수 있게 해줍니다. 50개 이상의 파일 형식을 지원하고, 수천 행의 워크북을 처리하며, 일반 서버 하드웨어에서 1초 미만으로 차트를 이미지로 렌더링할 수 있습니다.

## Aspose.Cells로 차트를 PNG로 내보내는 이유
Aspose.Cells를 사용해 차트를 PNG로 내보내면 높은 성능, 낮은 메모리 사용량, 다양한 포맷 지원을 제공하면서 Microsoft Excel이 필요 없게 됩니다. 이 라이브러리는 차트를 1초 미만에 렌더링하고 힙 사용량을 적게 유지하며, PNG, JPEG, BMP, TIFF를 지원해 웹, 인쇄, 크로스‑플랫폼 배포에 이상적입니다.

## 전제 조건

- **Aspose.Cells for Java** v25.3 (이상).  
- **JDK 8+**가 개발 머신에 설치되어 있어야 합니다.  
- **IDE**(IntelliJ IDEA 또는 Eclipse 등).  
- **Maven 또는 Gradle**을 사용한 종속성 관리.  

### 필요한 라이브러리 및 종속성

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### 환경 설정

1. **JDK 8** 이상이 `PATH`에 있는지 확인합니다.  
2. 선호하는 IDE를 열고 새로운 Maven/Gradle Java 프로젝트를 생성합니다.  
3. 위의 스니펫을 사용해 Aspose.Cells 종속성을 추가합니다.  

### 라이선스 획득

Aspose.Cells는 기능을 평가할 수 있는 무료 체험을 제공합니다:

- [Download Free Trial](https://releases.aspose.com/cells/java/)  
- 프로덕션 사용을 위해서는 [Purchase Aspose.Cells](https://purchase.aspose.com/buy)에서 라이선스를 구매하십시오.  
- 장기 테스트를 위해 임시 라이선스를 요청할 수 있습니다.

## Aspose.Cells for Java 설정

환경이 준비되면 프로젝트에서 Aspose.Cells를 초기화합니다:

1. 앞서 보여준 대로 Maven 또는 Gradle 종속성을 추가합니다.  
2. 라이선스 파일(`Aspose.Cells.lic`)을 프로젝트의 resources 폴더에 배치합니다.  
3. 런타임에 라이선스를 로드합니다:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## 구현 가이드

세 가지 핵심 시나리오인 차트 로드 및 새로 고침, 글로벌화 설정 사용자 정의, 차트를 PNG로 렌더링하는 과정을 단계별로 살펴보겠습니다.

### Aspose.Cells Java로 차트를 PNG로 내보내는 방법?

Aspose.Cells for Java로 차트를 PNG로 내보내려면 먼저 `Workbook` 클래스를 사용해 워크북을 로드하고, 해당 워크시트에서 원하는 `Chart` 객체를 가져옵니다. `ImageOrPrintOptions`를 설정해 이미지 형식을 PNG로 지정한 뒤, 최종적으로 `chart.toImage(outputStream, options)`를 호출합니다. 이렇게 생성된 스트림은 고품질 PNG를 포함하며, 이를 저장하거나 클라이언트에 직접 전송할 수 있습니다.

### Excel 파일에서 차트 로드 및 새로 고침

**Overview**: 기존 워크북을 로드하고 차트가 최신 데이터를 반영하도록 하며, 렌더링을 위해 준비합니다.

#### 1. 워크북 로드  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*Definition anchor*: `Workbook` 클래스는 메모리 내 전체 Excel 파일을 나타내며, 워크시트, 차트 및 셀에 대한 접근을 제공합니다.

#### 2. 워크시트 및 차트 접근  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*Definition anchor*: `Worksheet` 객체는 행/열 접근을 제공하고, `Chart` 객체는 차트와 관련된 모든 속성을 캡슐화합니다.

#### 3. 차트 새로 고침  
```java
chart.calculate();
```  
`calculate()`를 호출하면 차트가 변경된 원본 데이터를 기반으로 시리즈를 다시 계산하도록 강제하여 시각적 정확성을 보장합니다.

### 차트에 대한 글로벌화 설정 사용자 정의

**Overview**: 렌더링 전에 날짜, 시간 및 숫자 형식을 지역 관습에 맞게 조정합니다.

#### 1. 워크북 로드  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. 사용자 정의 글로벌화 설정 적용  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
날짜에 대해 `"dd-MMM-yyyy"`와 같이 지역별 패턴을, 숫자에 대해 `"#,##0.00"`와 같이 지정할 수 있으며, 이를 통해 내보낸 PNG가 로컬 표준을 따르도록 할 수 있습니다.

### 차트를 이미지로 렌더링

**Overview**: 새로 고친 차트를 프레젠테이션, PDF 또는 웹 페이지에 사용할 수 있는 PNG 파일로 변환합니다.

#### 1. 워크북 로드 및 차트 접근  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. 이미지로 렌더링  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
`toImage()` 메서드는 차트를 `java.io.OutputStream`에 기록합니다. `ImageOrPrintOptions.setImageFormat(ImageFormat.png)`를 설정하면 선명한 PNG 파일을 얻을 수 있습니다.

## 실용적인 적용 사례

- **비즈니스 보고서** – 이해관계자 배포를 위해 PDF 또는 Word 문서에 PNG 차트를 삽입합니다.  
- **데이터 대시보드** – 새로운 데이터가 도착하면 차트를 즉시 새로 고치고, PNG로 렌더링해 빠른 웹 전달을 수행합니다.  
- **글로벌 컴플라이언스** – 지역 규제 요구사항을 충족하도록 로케일별 숫자 및 날짜 형식을 적용합니다.

## 성능 고려 사항

- **메모리 관리**: 대용량 파일의 경우 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`를 사용합니다.  
- **선택적 새로 고침**: 원본 데이터가 변경된 차트에만 `chart.calculate()`를 호출합니다.  
- **스레드 안전성**: 동시성 문제를 피하기 위해 스레드당 별도의 `Workbook` 인스턴스를 생성합니다.

## 일반적인 문제 및 해결책

| 문제 | 해결책 |
|-------|----------|
| 라이선스를 찾을 수 없음 | `Aspose.Cells.lic` 경로를 확인하고 클래스패스에 포함되어 있는지 확인합니다. |
| PNG 출력이 비어 있음 | 차트가 숨겨져 있지 않은지 확인하고 렌더링 전에 `calculate()`가 호출되었는지 확인합니다. |
| 대용량 파일에서 렌더링이 느림 | `MemorySetting.MEMORY_PREFERENCE`를 활성화하고 필요한 워크시트만 렌더링합니다. |

## 자주 묻는 질문

**Q: 라이선스 활성화 문제를 어떻게 해결하나요?**  
A: `Aspose.Cells.lic` 파일을 resources 폴더에 배치하고 `License license = new License(); license.setLicense("Aspose.Cells.lic");`를 사용해 로드합니다.

**Q: Aspose.Cells for Java를 웹 애플리케이션에서 사용할 수 있나요?**  
A: 예, Spring Boot, Jakarta EE 또는 모든 서블릿 컨테이너와 원활하게 통합됩니다.

**Q: 차트를 새로 고칠 때 흔히 발생하는 실수는 무엇인가요?**  
A: `calculate()`를 호출하기 전에 원본 데이터를 업데이트하지 않으면 오래된 시각적 결과가 나타납니다.

**Q: 대용량 Excel 파일을 효율적으로 처리하려면 어떻게 해야 하나요?**  
A: `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`를 사용하고 워크시트를 스트림으로 처리합니다.

**Q: 차트 렌더링에 지원되는 이미지 포맷은 무엇인가요?**  
A: PNG, JPEG, BMP, TIFF를 모두 지원하며, 무손실 품질을 위해 PNG를 선택합니다.

## 리소스

- **문서**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **다운로드**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **구매 및 라이선스**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **무료 체험**: [Get a Free Trial of Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **임시 라이선스**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **지원 및 포럼**: [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

이 단계들을 숙달하면 **차트를 PNG로 내보내는** 작업을 안정적으로 수행할 수 있으며, 고품질 시각화를 모든 Java 기반 솔루션에 통합할 수 있습니다.

---

**마지막 업데이트:** 2026-06-12  
**테스트 환경:** Aspose.Cells 25.3 for Java  
**작성자:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 관련 튜토리얼

- [Aspose.Cells Java를 사용하여 Excel 차트를 SVG(확장 벡터 그래픽)로 내보내는 방법](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 차트를 PDF로 내보내기: 맞춤 페이지 크기 가이드](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Aspose.Cells Java를 사용하여 테마 색상으로 Excel 차트 맞춤 설정하는 방법](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```