---
"date": "2025-04-08"
"description": "Aspose.Cells for Java를 사용하여 Excel 통합 문서에 텍스트 상자를 추가하고 줄 간격을 설정하는 방법을 알아보세요. 스타일이 적용된 텍스트 모양으로 통합 문서 프레젠테이션을 더욱 멋지게 만들어 보세요."
"title": "Aspose.Cells for Java를 사용하여 Excel에 텍스트 상자 추가 및 줄 간격 설정"
"url": "/ko/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for Java를 사용하여 Excel에 텍스트 상자 추가 및 줄 간격 설정

## 소개

동적 Excel 보고서를 만들 때는 특정 줄 간격의 텍스트 상자를 추가하는 등 사용자 지정 텍스트 서식이 필요한 경우가 많습니다. Aspose.Cells for Java를 사용하면 이러한 작업이 간편하고 효율적입니다. 이 튜토리얼에서는 Aspose.Cells for Java를 사용하여 스타일이 적용된 텍스트 모양을 추가하여 통합 문서 프레젠테이션을 개선하는 방법을 안내합니다.

이 가이드를 끝내면 다음 방법을 배우게 됩니다.
- 새 Excel 통합 문서를 만들고 해당 워크시트에 액세스합니다.
- 워크시트에 텍스트 상자 모양 추가
- 텍스트 모양 내부에 사용자 지정 줄 간격 설정
- 서식이 지정된 통합 문서를 XLSX 형식으로 저장하세요.

먼저 환경 설정부터 시작해 보겠습니다.

### 필수 조건

시작하기 전에 다음 사항이 있는지 확인하세요.
- 컴퓨터에 Java Development Kit(JDK)가 설치되어 있습니다.
- Java 코드를 작성하기 위한 IDE 또는 편집기
- 종속성을 관리하도록 구성된 Maven 또는 Gradle 빌드 시스템

Java 프로그래밍에 대한 기본적인 이해와 Excel 파일 구조에 대한 친숙함이 도움이 될 것입니다.

## Java용 Aspose.Cells 설정

Maven이나 Gradle을 사용하여 프로젝트의 종속성 관리에 Aspose.Cells를 포함합니다.

**메이븐**

다음 종속성 블록을 추가하세요. `pom.xml` 파일:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**그래들**

이것을 당신의 것에 포함시키세요 `build.gradle` 파일:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

다음으로, 무료 평가판을 선택하거나 임시 라이선스를 요청하거나 전체 라이선스를 구매하여 Aspose.Cells 라이선스를 취득하세요.

### Aspose.Cells 초기화

라이브러리가 프로젝트에 포함되면 Java 애플리케이션 내에서 초기화합니다.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Workbook 인스턴스를 초기화합니다(Excel 파일을 나타냄)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## 구현 가이드

### 통합 문서 만들기 및 워크시트 액세스

먼저 새 Excel 통합 문서를 만들고 첫 번째 워크시트에 액세스하세요. 여기에 텍스트 상자를 추가할 것입니다.

#### 개요

새 통합 문서를 만들면 필요에 따라 데이터, 모양, 서식을 추가할 수 있는 빈 공간이 제공됩니다.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### 워크시트에 텍스트 상자 추가

다음으로, 선택한 워크시트에 텍스트 상자 모양을 추가합니다. 이 모양에는 필요한 모든 텍스트 내용을 담을 수 있습니다.

#### 개요

텍스트 상자는 메모나 지침 등의 사용자 지정 텍스트를 Excel 시트 내에 직접 포함하는 데 유용한 도구입니다.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 워크시트에 텍스트 상자 모양 추가
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### 모양에 텍스트 설정

텍스트 상자가 준비되면 내용을 설정하고 상자 안의 텍스트 서식을 지정합니다.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 워크시트에 텍스트 상자 모양 추가
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 모양 안에 텍스트 내용 설정
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Shape에서 텍스트 단락에 액세스

텍스트 상자 내에서 개별 문단에 접근하여 특정 서식을 적용할 수 있습니다.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 워크시트에 텍스트 상자 모양 추가
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 모양 안에 텍스트 내용 설정
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 도형의 두 번째 문단에 접근합니다.
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### 문단의 줄 간격 설정

줄 간격을 사용자 지정하면 가독성을 높일 수 있습니다. 설정 방법은 다음과 같습니다.

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 워크시트에 텍스트 상자 모양 추가
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 모양 안에 텍스트 내용 설정
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 도형의 두 번째 문단에 접근합니다.
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 줄 간격을 20포인트로 설정하세요
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 문단 앞뒤에 공백을 구성합니다.
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### 통합 문서 저장

마지막으로 새로 추가하고 서식을 지정한 텍스트 상자로 통합 문서를 저장합니다.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 새 통합 문서(Excel 파일) 만들기
        Workbook workbook = new Workbook();
        
        // 첫 번째 워크시트에 접근하세요
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 워크시트에 텍스트 상자 모양 추가
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 모양 안에 텍스트 내용 설정
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 도형의 두 번째 문단에 접근합니다.
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 줄 간격을 20포인트로 설정하세요
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 문단 앞뒤에 공백을 구성합니다.
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // 통합 문서를 저장합니다
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## 결론

Aspose.Cells for Java를 사용하여 Excel 통합 문서에 텍스트 상자를 추가하고 줄 간격을 설정하는 방법을 성공적으로 익혔습니다. 이를 통해 동적이고 시각적으로 매력적인 보고서를 만드는 능력이 향상될 것입니다.

## 키워드 추천
- "자바용 Aspose.Cells"
- "Excel에 텍스트 상자 추가"
- "Excel에서 줄 간격 설정"
- "스타일이 적용된 텍스트가 있는 Excel 통합 문서"
- "자바와 Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}