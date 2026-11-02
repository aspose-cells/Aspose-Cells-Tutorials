---
category: general
date: 2026-08-11
description: Crie uma nova pasta de trabalho Aspose em Java, adicione uma propriedade
  personalizada ao Excel e, em seguida, salve a pasta de trabalho como XLSB com um
  exemplo completo passo a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: pt
lastmod: 2026-08-11
og_description: Crie uma nova pasta de trabalho Aspose em Java, adicione uma propriedade
  personalizada ao Excel e salve a pasta de trabalho como XLSB com um exemplo completo,
  pronto‑para‑executar.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Criar nova pasta de trabalho Aspose – adicionar propriedade personalizada
  no Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Criar nova pasta de trabalho Aspose – adicionar propriedade personalizada ao
  Excel e salvar como XLSB
url: /pt/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar nova pasta de trabalho Aspose – adicionar propriedade personalizada Excel e salvar como XLSB

Se você precisa **criar nova pasta de trabalho Aspose** em uma aplicação Java, este guia mostra exatamente como fazer isso. Você aprenderá a **adicionar propriedade personalizada Excel**, recuperar o valor e **salvar a pasta de trabalho como XLSB** sem perder nenhum metadado.

O tutorial cobre tudo, desde a configuração do projeto até a verificação do arquivo salvo. Nenhuma documentação externa é necessária; basta seguir os passos e executar o código.

## Pré-requisitos

- Java Development Kit (JDK) 8 ou superior instalado.
- Maven ou Gradle para gerenciar dependências (o exemplo usa Maven).
- Uma licença ativa do Aspose.Cells for Java (ou use o modo de avaliação gratuito para testes).

## Etapa 1: Adicionar Aspose.Cells ao seu projeto

Adicione o artefato Maven do Aspose.Cells ao seu `pom.xml`. Esta dependência fornece as classes necessárias para **criar nova pasta de trabalho Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Dica:** Se preferir Gradle, substitua o trecho Maven pela linha equivalente `implementation "com.aspose:aspose-cells:23.12"`.

## Etapa 2: Criar uma nova pasta de trabalho Aspose

O primeiro passo funcional é instanciar um objeto `Workbook`. Este objeto representa um arquivo Excel na memória e é o ponto de entrada para todas as operações subsequentes.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Criar uma nova pasta de trabalho Aspose fornece uma pasta limpa com uma planilha padrão, pronta para personalizações.

## Etapa 3: Adicionar propriedade personalizada Excel

Propriedades personalizadas permitem armazenar metadados arbitrários dentro de um arquivo Excel. Aqui, nós **adicionamos propriedade personalizada Excel** chamada `ProjectId` com um valor numérico.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

O método `add` aceita um nome de propriedade e um valor de qualquer tipo suportado (string, número, data, etc.). Esses metadados acompanham o arquivo onde quer que você o copie.

## Etapa 4: Recuperar e exibir a propriedade personalizada

Ler novamente a propriedade verifica se ela foi armazenada corretamente. Você também pode usar o valor recuperado na sua lógica de negócios.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Converter para `int` funciona porque armazenamos um valor numérico. Se você armazenar uma string, use `(String)` em vez disso.

## Etapa 5: Salvar a pasta de trabalho como XLSB

Agora você **salva a pasta de trabalho como XLSB**. O formato XLSB armazena a pasta de trabalho em uma representação binária, que é mais rápida de abrir e ocupa menos espaço em disco. Todas as propriedades personalizadas são preservadas automaticamente.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Substitua `"WithCustomProps.xlsb"` por um caminho absoluto se precisar do arquivo em um diretório específico. O enum `SaveFormat.XLSB` indica ao Aspose.Cells que escreva no formato binário.

## Etapa 6: Verificar a saída

Execute o programa a partir da sua IDE ou linha de comando:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Você deverá ver:

```
ProjectId = 12345
```

Abra `WithCustomProps.xlsb` no Excel. Navegue até **Arquivo → Informações → Propriedades → Propriedades avançadas → Personalizado**. A entrada `ProjectId` com o valor `12345` será listada, confirmando que a etapa **add custom property excel** foi bem-sucedida e que a operação **save workbook as xlsb** preservou os metadados.

## Perguntas comuns e casos de borda

### E se eu precisar armazenar uma propriedade string?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Recupere-a com:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Posso adicionar várias propriedades personalizadas de uma vez?

Sim. Chame `add` repetidamente para cada par nome/valor. O Aspose.Cells não limita o número de propriedades personalizadas, mas mantenha o tamanho total razoável para evitar inflar o arquivo.

### Como o formato binário afeta o desempenho?

Arquivos XLSB carregam mais rápido porque evitam a análise XML. Isso é especialmente perceptível em pastas de trabalho com muitas linhas, fórmulas ou imagens incorporadas.

### E se eu precisar trabalhar com um arquivo XLSX existente?

Substitua o construtor `new Workbook()` por `new Workbook("ExistingFile.xlsx")`. O restante das etapas (adição de propriedades, salvar como XLSB) permanece idêntico.

## Código-fonte completo

Abaixo está o exemplo completo, pronto‑para‑executar. Copie-o para um arquivo chamado `CustomPropertiesXlsb.java` dentro da sua pasta `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Executar esta classe produz um arquivo XLSB que contém a propriedade personalizada e pode ser aberto em qualquer versão moderna do Microsoft Excel.

## Conclusão

Agora você sabe como **criar nova pasta de trabalho Aspose**, **adicionar propriedade personalizada Excel** e **salvar a pasta de trabalho como XLSB** usando Java. O exemplo demonstra todo o ciclo de vida: inicialização, injeção de metadados, verificação e serialização binária.

Em seguida, explore tópicos relacionados como **definir propriedades de documento**, **trabalhar com fórmulas Excel** ou **converter entre XLSX e XLSB**. Cada um desses se baseia na mesma API Aspose.Cells que você acabou de usar, permitindo estender a solução sem precisar aprender novas bibliotecas.

Sinta-se à vontade para experimentar diferentes tipos de dados, múltiplas planilhas ou proteção por senha—Aspose.Cells oferece suporte a todos esses cenários prontamente. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar e salvar pasta de trabalho Excel Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Como criar e salvar uma pasta de trabalho Excel como SVG usando Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Criar pasta de trabalho Excel e adicionar rótulos com Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}