---
"date": "2025-04-08"
"description": "Aprenda a usar o Aspose.Cells para Java para adicionar caixas de texto e definir espaçamento entre linhas em pastas de trabalho do Excel. Aprimore suas apresentações de pastas de trabalho com formas de texto estilizadas."
"title": "Adicionar caixa de texto e definir espaçamento de linha no Excel usando Aspose.Cells para Java"
"url": "/pt/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Adicionar uma caixa de texto e definir o espaçamento entre linhas no Excel usando Aspose.Cells para Java

## Introdução

A criação de relatórios dinâmicos no Excel geralmente requer formatação de texto personalizada, como adicionar caixas de texto com espaçamento de linha específico. Com o Aspose.Cells para Java, isso se torna simples e eficiente. Este tutorial guiará você pelo aprimoramento das apresentações da sua pasta de trabalho usando o Aspose.Cells para Java para adicionar formas de texto estilizadas.

Ao final deste guia, você aprenderá como:
- Crie uma nova pasta de trabalho do Excel e acesse suas planilhas
- Adicionar uma forma de caixa de texto a uma planilha
- Definir espaçamento de linha personalizado dentro de uma forma de texto
- Salve sua pasta de trabalho formatada no formato XLSX

Vamos começar configurando seu ambiente.

### Pré-requisitos

Antes de começar, certifique-se de ter o seguinte:
- Java Development Kit (JDK) instalado em sua máquina
- Um IDE ou editor para escrever código Java
- Sistema de construção Maven ou Gradle configurado para gerenciar dependências

Um conhecimento básico de programação Java e familiaridade com estruturas de arquivos do Excel serão benéficos.

## Configurando Aspose.Cells para Java

Inclua Aspose.Cells no gerenciamento de dependências do seu projeto usando Maven ou Gradle:

**Especialista**

Adicione o seguinte bloco de dependência ao seu `pom.xml` arquivo:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Inclua isso em seu `build.gradle` arquivo:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Em seguida, adquira uma licença para o Aspose.Cells optando por um teste gratuito, solicitando uma licença temporária ou comprando uma licença completa.

### Inicializando Aspose.Cells

Depois que a biblioteca estiver incluída no seu projeto, inicialize-a no seu aplicativo Java:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Inicializar uma instância de Workbook (representa um arquivo Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Guia de Implementação

### Crie uma pasta de trabalho e uma planilha do Access

Comece criando uma nova pasta de trabalho do Excel e acessando a primeira planilha. É aqui que você adicionará sua caixa de texto.

#### Visão geral

A criação de uma nova pasta de trabalho fornece uma tela em branco para acrescentar dados, formas e formatação conforme necessário.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Adicionar caixa de texto à planilha

Em seguida, adicione uma caixa de texto à planilha selecionada. Essa caixa pode conter qualquer conteúdo textual que você precisar.

#### Visão geral

Caixas de texto são ferramentas versáteis para incluir textos personalizados, como notas ou instruções, diretamente em uma planilha do Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Adicionar uma forma de caixa de texto à planilha
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Definir texto em forma

Quando sua caixa de texto estiver pronta, defina seu conteúdo e formate o texto dentro dela.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Adicionar uma forma de caixa de texto à planilha
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Definir conteúdo de texto dentro da forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Acesse parágrafos de texto em forma

Você pode acessar parágrafos individuais dentro de uma caixa de texto para aplicar formatação específica.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Adicionar uma forma de caixa de texto à planilha
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Definir conteúdo de texto dentro da forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Acesse o segundo parágrafo no formato
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Definir espaçamento entre linhas do parágrafo

Personalizar o espaçamento entre linhas pode melhorar a legibilidade. Veja como configurá-lo:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Adicionar uma forma de caixa de texto à planilha
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Definir conteúdo de texto dentro da forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Acesse o segundo parágrafo no formato
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Defina o espaçamento entre linhas para 20 pontos
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurar espaço antes e depois do parágrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Salvar pasta de trabalho

Por fim, salve sua pasta de trabalho com a caixa de texto recém-adicionada e formatada.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Criar uma nova pasta de trabalho (arquivo Excel)
        Workbook workbook = new Workbook();
        
        // Acesse a primeira planilha
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Adicionar uma forma de caixa de texto à planilha
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Definir conteúdo de texto dentro da forma
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Acesse o segundo parágrafo no formato
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Defina o espaçamento entre linhas para 20 pontos
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configurar espaço antes e depois do parágrafo
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Salvar a pasta de trabalho
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusão

Você aprendeu com sucesso a adicionar uma caixa de texto e definir o espaçamento entre linhas em uma pasta de trabalho do Excel usando o Aspose.Cells para Java. Isso aprimora sua capacidade de criar relatórios dinâmicos e visualmente atraentes.

## Recomendações de palavras-chave
- "Aspose.Cells para Java"
- "Adicionar caixa de texto no Excel"
- "Definir espaçamento de linha no Excel"
- "Pasta de trabalho do Excel com texto estilizado"
- "Java e Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}