---
category: general
date: 2026-08-17
description: Exportar Excel para TXT limitando os dígitos significativos – aprenda
  como definir os dígitos e converter Excel para texto em Java com um exemplo completo
  do Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: pt
lastmod: 2026-08-17
og_description: Exportar Excel para TXT limitando os dígitos significativos. Este
  tutorial mostra como definir os dígitos e converter Excel para texto usando Aspose.Cells
  para Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Exportar Excel para TXT com dígitos significativos limitados – Guia Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Como exportar Excel para TXT com dígitos significativos limitados usando Java
url: /pt/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel para TXT com dígitos significativos limitados usando Java

Se você precisar **exportar Excel para TXT** controlando o número de dígitos significativos, este guia fornece uma solução pronta‑para‑executar. Você verá como definir os dígitos, converter Excel para texto e manter a saída organizada com uma única alteração de configuração.

O exemplo usa Aspose.Cells para Java 25.10, que introduz a opção `setSignificantDigits`. Ao final do tutorial você poderá gerar um arquivo TXT que contém apenas os dígitos desejados, sem código extra de arredondamento.

## O que você vai alcançar

- Criar uma pasta de trabalho programaticamente.  
- Inserir um valor numérico em uma célula.  
- Configurar as opções de salvamento TXT para limitar dígitos significativos.  
- Salvar a pasta de trabalho como um arquivo de texto simples.  
- Entender como funciona a configuração `significantDigits` e como adaptá‑la para outros cenários.

### Pré‑requisitos

- Java 17 ou posterior (o código também compila com Java 8).  
- Aspose.Cells para Java 25.10 ou mais recente. Baixe o JAR no [site da Aspose](https://products.aspose.com/cells/java) e adicione‑o ao classpath do seu projeto.  
- Uma IDE ou um editor de texto simples e uma ferramenta de build de linha de comando (Maven/Gradle).

## Etapa 1: Configurar o projeto e importar Aspose.Cells

Crie um novo projeto Java e adicione o JAR do Aspose.Cells ao caminho de compilação. Se você usar Maven, adicione a dependência a seguir ao `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Dica profissional:** Use o classificador `jdk17` para a runtime Java mais recente; isso reduz o risco de avisos de compatibilidade.

## Etapa 2: Criar uma pasta de trabalho e escrever um valor

A pasta de trabalho representa um arquivo Excel na memória. Você pode adicionar dados a qualquer célula usando o método `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

O número `123.456789` será a fonte para a exportação TXT. Por padrão, o Aspose.Cells escreveria todas as casas decimais, o que frequentemente gera arquivos de texto ruidosos.

## Etapa 3: Configurar as opções de salvamento TXT para limitar dígitos significativos

O Aspose.Cells fornece `TxtSaveOptions` para controle detalhado da saída em texto puro. O método `setSignificantDigits` indica ao exportador quantos dígitos manter **no total**, não apenas após o ponto decimal.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Quando `significantDigits` é definido como `4`, o exportador arredonda o valor `123.456789` para `123.5`. Esse comportamento corresponde à definição matemática de algarismos significativos: os quatro primeiros dígitos diferentes de zero são retidos.

### Como a configuração difere de “limitar decimais”

- **limitar decimais** (`setDecimalPlaces`) corta dígitos *após* o ponto decimal, independentemente da parte inteira.  
- **dígitos significativos** (`setSignificantDigits`) conta dígitos a partir do primeiro dígito não‑zero, o que é útil quando os números variam em magnitude.

Se precisar de um número fixo de casas decimais, substitua a linha acima por:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Etapa 4: Salvar a pasta de trabalho como um arquivo TXT

Agora escreva a pasta de trabalho no disco usando as opções configuradas.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Executar o programa cria `significant_digits.txt` no diretório de trabalho. O arquivo contém uma única linha:

```
123.5
```

### Saída esperada

| Célula | Valor original | Exportado (4 dígitos significativos) |
|--------|----------------|---------------------------------------|
| A1     | 123.456789     | 123.5                                 |

Se você mudar `setSignificantDigits(4)` para `6`, a saída passa a ser `123.457`. Experimente valores diferentes para ver como o arredondamento se adapta.

## Etapa 5: Variações comuns e casos de borda

### Exportando um intervalo inteiro

Se quiser exportar mais de uma célula, basta preencher o intervalo antes de salvar:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

A mesma configuração `significantDigits` se aplica a cada célula numérica, garantindo precisão consistente em todo o arquivo.

### Manipulando separadores decimais específicos de localidade

O Aspose.Cells respeita a localidade do sistema ao escrever texto. Para forçar um ponto (`.`) como separador decimal, defina a cultura nas `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Isso é útil quando a aplicação de destino espera um formato específico, como analisadores CSV que aceitam apenas `.`.

### Sobrescrevendo arquivos existentes

O método `save` sobrescreve o arquivo de destino por padrão. Se precisar evitar perda acidental de dados, verifique a existência do arquivo primeiro:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Grandes pastas de trabalho e uso de memória

Ao exportar planilhas muito grandes, considere transmitir a saída:

```java
saveOptions.setEnableMemorySaving(true);
```

Essa opção reduz o consumo de heap ao escrever linhas incrementalmente.

## Exemplo completo em funcionamento

Abaixo está o programa completo que você pode copiar, colar e executar imediatamente:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Executar este código produz `significant_digits.txt` com o seguinte conteúdo (colunas separadas por tabulação):

```
123.5	0.001235	98770
```

Cada número respeita a regra de **4 dígitos significativos**, demonstrando que a configuração funciona em diferentes magnitudes.

## Conclusão

Agora você sabe como **exportar Excel para TXT** controlando o número de dígitos significativos. Usando `TxtSaveOptions.setSignificantDigits`, você pode **definir dígitos**, **limitar decimais** e **limitar dígitos significativos** em uma única linha de código fácil de manter. A abordagem funciona para células individuais, intervalos completos e grandes pastas de trabalho.

### Próximos passos

- Explore outras propriedades de `TxtSaveOptions` como `setDelimiter('\t')` para personalizar os separadores de coluna.  
- Combine o exportador com `CsvSaveOptions` se precisar de valores separados por vírgula em vez de texto puro.  
- Integre a rotina em um serviço web que aceita arquivos Excel enviados e devolve a saída TXT recortada em tempo real.

Sinta‑se à vontade para experimentar diferentes limites de dígitos e localidades. Se encontrar um cenário em que as opções embutidas não atendam a um requisito especial, você pode sempre pós‑processar o arquivo TXT gerado com as utilidades padrão de I/O do Java.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Convert Text to Numbers in Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}