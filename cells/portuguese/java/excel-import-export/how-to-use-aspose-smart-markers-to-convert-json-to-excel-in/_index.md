---
category: general
date: 2026-08-20
description: Aprenda a escrever JSON para Excel e a preencher uma pasta de trabalho
  Excel a partir de JSON usando marcadores inteligentes da Aspose e Java – guia passo
  a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose smart markers
- convert json to excel
- write json to excel
- populate excel from json
- create excel workbook java
language: pt
lastmod: 2026-08-20
og_description: Os marcadores inteligentes do Aspose permitem escrever JSON no Excel
  e criar um exemplo de código Java para uma pasta de trabalho do Excel. Siga este
  tutorial para preencher o Excel a partir de JSON rapidamente.
og_image_alt: Screenshot of an Excel file generated from a JSON array using Aspose.Cells
og_title: 'aspose smart markers: converter JSON para Excel em Java – guia completo'
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  headline: How to use aspose smart markers to convert JSON to Excel in Java
  type: TechArticle
- description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  name: How to use aspose smart markers to convert JSON to Excel in Java
  steps:
  - name: Expected output
    text: 'When you open `JsonArraySingleCell.xlsx`, cell **A1** contains:'
  - name: 1. Populating multiple cells with different JSON objects
    text: 'If you need to fill a table rather than a single cell, omit `ArrayAsSingle`
      and use the default array handling:'
  - name: 2. Using a JSON file instead of a hard‑coded string
    text: '```java String jsonPath = "data/people.json"; String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)),
      StandardCharsets.UTF_8); ```'
  - name: 3. Handling nested JSON structures
    text: 'For nested objects, reference sub‑properties in the smart marker:'
  - name: 4. License activation
    text: 'To avoid the evaluation watermark, activate your license before creating
      the workbook:'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- JSON
title: Como usar marcadores inteligentes do Aspose para converter JSON em Excel em
  Java
url: /pt/java/excel-import-export/how-to-use-aspose-smart-markers-to-convert-json-to-excel-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar aspose smart markers para converter JSON em Excel em Java

Se você precisar de **aspose smart markers** para converter JSON em Excel, este tutorial mostra uma solução pronta‑para‑executar. Você verá como escrever JSON em Excel, preencher uma pasta de trabalho Excel a partir de JSON e gerar um arquivo com uma única linha de código.

O exemplo usa Aspose.Cells for Java, uma biblioteca que elimina a necessidade do Microsoft Office no servidor. Ao final do guia, você terá um programa Java completo que cria uma pasta de trabalho Excel, insere um array JSON em uma única célula e salva o resultado como `JsonArraySingleCell.xlsx`.

## Pré-requisitos

* Java Development Kit 17 ou mais recente instalado.
* Maven ou Gradle para gerenciar dependências (o exemplo usa Maven).
* Uma licença Aspose.Cells for Java (a avaliação gratuita funciona para testes).
* Familiaridade básica com a sintaxe Java e o formato JSON.

> **Dica profissional:** Se você executar o código sem uma licença, a pasta de trabalho gerada conterá uma pequena marca d'água de avaliação na primeira planilha.

## Adicionar Aspose.Cells ao seu projeto

Adicione a dependência a seguir ao seu `pom.xml` (Maven) ou o equivalente no Gradle:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

A biblioteca fornece as classes `Workbook`, `Worksheet`, `JsonDataSource` e `SmartMarker` usadas ao longo deste tutorial.

## Etapa 1: Criar uma pasta de trabalho Excel em Java

Primeiro, instancie um novo objeto `Workbook`. Ele representa um arquivo Excel vazio na memória.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // Creates a blank .xlsx file
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();
```

`Workbook` é o ponto de entrada para todas as operações do Excel. Por padrão, ele contém uma planilha, que recuperamos para manipulação adicional.

## Etapa 2: Preparar o array JSON que você deseja escrever no Excel

A string JSON pode vir de um arquivo, de um serviço web ou ser construída programaticamente. Para este tutorial, usamos um array simples embutido:

```java
// Step 2: Define the JSON array that will be used as the data source
String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";
```

A estrutura JSON corresponde ao formato esperado pelos smart markers do Aspose.Cells: um array de objetos onde cada objeto contém a propriedade `Name`.

## Etapa 3: Inserir um smart marker que trata o array como uma única célula

Os smart markers da Aspose permitem que você incorpore marcadores de posição diretamente nas células. A opção `ArrayAsSingle` indica ao mecanismo que coloque todo o array JSON em uma única célula, em vez de expandi‑lo em uma tabela.

```java
// Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
cells.putValue("A1", "${jsonArray,ArrayAsSingle}");
```

Quando a pasta de trabalho for processada, `${jsonArray,ArrayAsSingle}` será substituído pelo texto JSON bruto.

## Etapa 4: Registrar a fonte de dados JSON com o nome do smart marker

Vincule o nome do marcador de posição (`jsonArray`) a uma instância `JsonDataSource`. Esta etapa associa a string JSON ao marcador.

```java
// Step 4: Register the JSON data source with the smart marker name
JsonDataSource dataSource = new JsonDataSource(jsonArray);
worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);
```

`JsonDataSource` analisa o JSON e o disponibiliza para o motor de smart markers. A chamada `setDataSource` o registra sob o nome usado na célula (`jsonArray`).

## Etapa 5: Salvar a pasta de trabalho no disco

Finalmente, grave a pasta de trabalho em um arquivo físico. Você pode escolher qualquer diretório que desejar.

```java
// Step 5: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Executar o programa produz um arquivo Excel que contém o array JSON na célula **A1**. Abra o arquivo com Excel, LibreOffice ou qualquer visualizador que suporte `.xlsx` para verificar o resultado.

![Pasta de trabalho Excel criada com Aspose.Cells mostrando dados JSON](/images/json-to-excel.png)

*Texto alternativo da imagem: Captura de tela de um arquivo Excel gerado a partir de um array JSON usando Aspose.Cells.*

## Código-fonte completo

Juntando todas as peças, aqui está a classe Java completa e executável:

```java
import com.aspose.cells.*;

public class JsonArraySmartMarker {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                       // Empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Define the JSON array that will be used as the data source
        String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";

        // Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
        cells.putValue("A1", "${jsonArray,ArrayAsSingle}");

        // Step 4: Register the JSON data source with the smart marker name
        JsonDataSource dataSource = new JsonDataSource(jsonArray);
        worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);

        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Saída esperada

Ao abrir `JsonArraySingleCell.xlsx`, a célula **A1** contém:

```
[{"Name":"John"},{"Name":"Jane"}]
```

Nenhuma linha ou coluna adicional é adicionada — isso demonstra como **aspose smart markers** permitem **escrever JSON em Excel** mantendo a carga JSON intacta.

## Variações comuns e casos de borda

### 1. Preenchendo várias células com diferentes objetos JSON

Se você precisar preencher uma tabela em vez de uma única célula, omita `ArrayAsSingle` e use o tratamento padrão de arrays:

```java
cells.putValue("A1", "${jsonArray}");
```

Aspose.Cells expandirá o array em linhas, criando uma coluna para cada propriedade (`Name` neste caso). Isso é útil quando você deseja uma visualização tabular tradicional.

### 2. Usando um arquivo JSON em vez de uma string codificada diretamente

```java
String jsonPath = "data/people.json";
String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)), StandardCharsets.UTF_8);
```

Leia o conteúdo do arquivo em uma string, então siga as Etapas 3‑5 sem alterações. Essa abordagem funciona para cargas grandes ou dados recebidos de APIs externas.

### 3. Manipulando estruturas JSON aninhadas

Para objetos aninhados, faça referência a sub‑propriedades no smart marker:

```java
cells.putValue("B2", "${jsonArray.Address.City}");
```

Aspose.Cells percorre a hierarquia automaticamente, permitindo que você preencha relatórios complexos sem análise manual.

### 4. Ativação da licença

Para evitar a marca d'água de avaliação, ative sua licença antes de criar a pasta de trabalho:

```java
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

Coloque este código no início do `main`. O arquivo de licença pode ser incorporado como recurso ou carregado de um local seguro.

## Dicas para uso em produção

* **Reutilize o objeto workbook** – Se você gerar muitos relatórios em uma única execução, crie um `Workbook` e clone as planilhas em vez de instanciar um novo workbook a cada vez.
* **Transmita a saída** – Para arquivos grandes, use `workbook.save(OutputStream, SaveFormat.XLSX)` para gravar diretamente em um fluxo de resposta em aplicações web.
* **Valide o JSON** – Antes de passar os dados para `JsonDataSource`, valide o formato JSON para evitar erros em tempo de execução.
* **Desempenho** – Os smart markers são otimizados para operações em lote; evite misturar gravações célula‑a‑célula com o processamento de smart markers na mesma planilha.

## Conclusão

Agora você sabe como usar **aspose smart markers** para **converter JSON em Excel**, **escrever JSON em Excel** e **preencher Excel a partir de JSON** usando Java. O exemplo completo cria uma pasta de trabalho Excel, insere um array JSON em uma única célula e salva o arquivo — tudo em apenas cinco passos concisos.

Em seguida, você pode explorar:

* Gerar relatórios de várias planilhas a partir de estruturas JSON complexas.
* Combinar smart markers com fórmulas do Excel para cálculos dinâmicos.
* Usar `JsonDataSource` junto com `DataTable` para exportações no estilo CSV.

Sinta-se à vontade para experimentar diferentes cargas JSON, intervalos de células e opções de formatação. Com Aspose.Cells, transformar dados JSON em pastas de trabalho Excel refinadas torna‑se um processo simples e orientado a código. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar uma pasta de trabalho Excel usando Aspose.Cells em Java: Um guia passo a passo](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Criando relatórios Excel dinâmicos usando Aspose.Cells Java e Smart Markers](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java-smart-markers/)
- [Dominando Aspose.Cells Java: Implementar Smart Markers e Fórmulas para automação do Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}