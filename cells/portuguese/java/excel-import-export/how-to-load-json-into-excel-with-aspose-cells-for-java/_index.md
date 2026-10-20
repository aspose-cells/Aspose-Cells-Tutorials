---
category: general
date: 2026-10-07
description: Aprenda como carregar JSON no Excel e gerar XLSX a partir de JSON usando
  Aspose.Cells. Este guia passo a passo também mostra como preencher o Excel a partir
  de JSON e salvar a pasta de trabalho como XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: pt
lastmod: 2026-10-07
og_description: Carregue JSON no Excel e gere XLSX a partir de JSON usando Aspose.Cells
  para Java. Siga este guia para preencher o Excel com JSON e salvar a pasta de trabalho
  como XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Carregue JSON no Excel com Aspose.Cells – guia completo em Java
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como carregar JSON no Excel com Aspose.Cells para Java
url: /pt/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carregar JSON no Excel com Aspose.Cells para Java

Se você precisa **carregar JSON no Excel**, este tutorial mostra uma maneira confiável de fazer isso com Aspose.Cells para Java. Você verá como gerar XLSX a partir de JSON, preencher Excel a partir de JSON e, finalmente, **salvar a pasta de trabalho como XLSX** — tudo em um único programa autônomo.

Trabalhar com JSON em planilhas é comum quando você exporta dados de serviços web, APIs ou armazenamentos NoSQL. Ao final deste guia, você terá uma classe Java pronta‑para‑executar que cria uma pasta de trabalho a partir de JSON e grava o resultado em um arquivo no disco.

## Pré-requisitos

* Java 8 ou superior instalado (o código usa recursos padrão do Java).
* Biblioteca Aspose.Cells para Java (versão 23.10 ou posterior). Você pode obtê‑la no [site da Aspose](https://downloads.aspose.com/cells/java) ou via Maven Central.
* Uma IDE ou um editor de texto simples e um terminal para compilar e executar código Java.
* Familiaridade básica com a sintaxe JSON e conceitos de Excel.

> **Dica profissional:** Se você usa Maven, adicione a dependência a seguir ao seu `pom.xml` para evitar o gerenciamento manual de JARs:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Etapa 1: Configurar o projeto e importar as classes necessárias

Crie uma nova classe Java chamada `JsonToExcelDemo`. Importe as classes Aspose.Cells que você precisará para criação de pastas de trabalho, manipulação de planilhas e processamento de Smart Markers.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Por que esta etapa é importante:* Importar as classes corretas garante que o compilador encontre as APIs Aspose.Cells. A classe `Workbook` representa o arquivo Excel, enquanto `SmartMarkerProcessor` executa a conversão de JSON‑para‑Excel.

## Etapa 2: Definir a fonte JSON que será carregada no Excel

Para este exemplo, usamos um pequeno array JSON contendo dois objetos. Em um cenário real, você poderia ler o JSON de um arquivo, de um endpoint REST ou de um banco de dados.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Por que esta etapa é importante:* A string JSON é a fonte de dados para a operação **populate Excel from JSON**. Manter o JSON em uma variável `String` facilita passá‑la para o `SmartMarkerProcessor`.

## Etapa 3: Criar uma nova pasta de trabalho e obter a primeira planilha

Uma pasta de trabalho nova fornece uma tela limpa. A primeira planilha (índice 0) é onde inseriremos o Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Por que esta etapa é importante:* Aspose.Cells trabalha com um objeto `Workbook` que pode ser salvo posteriormente como um arquivo XLSX. Acessar a primeira `Worksheet` nos permite colocar o marcador em um endereço de célula conhecido.

## Etapa 4: Inserir um Smart Marker que indica ao Aspose.Cells como tratar o JSON

Smart Markers são marcadores de posição que o Aspose.Cells substitui por dados de uma fonte. O marcador `&=JSONData.ArrayAsSingle` instrui a biblioteca a tratar todo o array JSON como um único valor de célula.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Por que esta etapa é importante:* Usar `ArrayAsSingle` evita o comportamento padrão de expandir cada elemento do array em linhas separadas. Isso é útil quando você deseja que o texto JSON apareça literalmente em uma célula, ou quando pretende dividi‑lo posteriormente com fórmulas.

## Etapa 5: Configurar o SmartMarkerProcessor com a fonte de dados JSON

Agora vincule a string JSON ao nome lógico `JSONData`. O processador substituirá o marcador pelos dados reais.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Por que esta etapa é importante:* `setDataSource` vincula o nome usado no marcador (`JSONData`) ao payload JSON real. `process()` realiza o trabalho pesado: analisar o JSON, aplicar a lógica do marcador e gravar o resultado na planilha.

## Etapa 6: Salvar a pasta de trabalho resultante como um arquivo XLSX

Finalmente, grave a pasta de trabalho no disco. A constante `SaveFormat.XLSX` garante o formato correto Office Open XML.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Por que esta etapa é importante:* Salvar o arquivo completa o fluxo de trabalho **generate XLSX from JSON**. O arquivo produzido pode ser aberto no Excel, LibreOffice ou qualquer outro programa de planilha que suporte XLSX.

### Código-fonte completo

Juntando todas as peças, aqui está o programa completo e executável que **cria pasta de trabalho a partir de JSON**, **preenche Excel a partir de JSON** e **salva a pasta de trabalho como XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Resultado esperado

Ao abrir `JsonSingleCell.xlsx` você verá o array JSON exibido na célula **A1** exatamente como a string original:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Se preferir cada objeto em uma linha separada, substitua o marcador por `&=JSONData` (sem `.ArrayAsSingle`). O processador então expandirá o array em linhas individuais, demonstrando uma técnica diferente de **populate Excel from JSON**.

## Variações comuns e casos de borda

| Situação | Ajuste |
|-----------|------------|
| **Grande payload JSON ( > 10 MB )** | Aumente o tamanho do heap da JVM (`-Xmx2g`) e considere fazer streaming do JSON para evitar `OutOfMemoryError`. |
| **Objetos aninhados** | Use marcadores hierárquicos como `&=JSONData.Name` e `&=JSONData.Age` dentro de uma tabela para mapear cada propriedade a uma coluna. |
| **Arquivo JSON em vez de uma string** | Leia o arquivo para uma `String` com `java.nio.file.Files.readString(Path.of("data.json"))` e passe‑o para `setDataSource`. |
| **Necessidade de manter o formato JSON original** | Mantenha o sufixo `.ArrayAsSingle`, ou envolva o JSON em CDATA se você planeja usar fórmulas do Excel que analisem JSON posteriormente. |
| **Múltiplas planilhas** | Crie planilhas adicionais (`workbook.getWorksheets().add("Sheet2")`) e repita a inserção do marcador em cada planilha. |

> **Aviso:** Smart Markers diferenciam maiúsculas de minúsculas. Certifique‑se de que o nome lógico (`JSONData`) corresponda exatamente entre o marcador e `setDataSource`.

## Testando a solução

1. Compile o programa:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Execute‑o:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verifique se `JsonSingleCell.xlsx` aparece no diretório de trabalho e abre sem erros.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel a partir de JSON – Guia Completo Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Criar Pasta de Trabalho Excel C# – Inserir JSON e Salvar como XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Salvar Pasta de Trabalho Excel a partir de JSON – Guia Completo](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}