---
category: general
date: 2026-09-27
description: Converter JSON para Excel com Aspose.Cells – aprenda como preencher o
  Excel a partir de JSON e como processar JSON no Excel de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to excel
- populate excel from json
- how to process json in excel
- Aspose.Cells Java
- smart marker JSON
- excel automation Java
language: pt
lastmod: 2026-09-27
og_description: Converter JSON para Excel usando Aspose.Cells. Este tutorial mostra
  como preencher o Excel a partir de JSON e explica como processar JSON no Excel com
  marcadores inteligentes.
og_image_alt: Excel sheet after JSON data is merged into a single cell using Aspose.Cells
  Smart Marker
og_title: Converter JSON para Excel com Aspose.Cells – guia completo
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  headline: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  type: TechArticle
- description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  name: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  steps:
  - name: Why each step matters
    text: '* **Step 1** – The JSON string is the source data. Because we set `ArrayAsSingle`,
      the processor will not try to create rows for each object; instead it will write
      the raw JSON text into the cell. * **Step 2** – Loading the template separates
      presentation (the Excel layout) from data (the JSON). Thi'
  - name: 4.1 Converting a large JSON payload
    text: 'If the JSON text exceeds the default cell length limit, increase the column
      width or set the cell’s `Style` to wrap text:'
  - name: 4.2 Using a named range instead of a fixed cell
    text: You can place the smart‑marker inside a named range (e.g., `JsonCell`) and
      refer to it by name in the template. The processing code remains unchanged;
      Aspose.Cells resolves the marker wherever it appears.
  - name: 4.3 Merging multiple JSON objects into separate cells
    text: If you later decide to expand the array into rows, simply remove `options.setArrayAsSingle(true)`.
      The processor will generate a table where each object occupies a row, and you
      can customize column headings with additional markers.
  - name: 4.4 Handling nested JSON structures
    text: For nested objects, use dot notation in the marker, e.g., `${person.name}`.
      The processor will traverse the hierarchy automatically, allowing you to **populate
      Excel from JSON** with complex data models.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como converter JSON para Excel e preencher o Excel a partir de JSON usando
  Aspose.Cells
url: /pt/java/excel-import-export/how-to-convert-json-to-excel-and-populate-excel-from-json-us/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter JSON para Excel e preencher Excel a partir de JSON usando Aspose.Cells

Se você precisa **converter JSON para Excel**, este guia mostra uma solução completa, pronta‑para‑executar. Ao final das duas primeiras frases, você entenderá como **preencher Excel a partir de JSON** com uma única expressão smart‑marker e por que a chamada `SmartMarkerOptions.setArrayAsSingle(true)` é essencial para o layout desejado.

Percorreremos cada passo necessário para **processar JSON no Excel**: carregar um modelo, configurar o motor de smart‑marker, mesclar os dados e salvar o resultado. O tutorial assume que você tem conhecimento básico de Java e uma licença válida do Aspose.Cells. Nenhuma ferramenta externa é necessária, e o código compila e executa no Java 8+.

## Pré-requisitos

* Java Development Kit (JDK) 8 ou mais recente instalado.
* Aspose.Cells for Java (a versão mais recente no momento da escrita, 23.9) adicionada ao classpath do seu projeto.
* Um modelo Excel chamado `SmartMarkerTemplate.xlsx` que contém o smart‑marker `${jsonArray:ArrayAsSingle}` na célula onde você deseja que os dados JSON apareçam.
* Um diretório onde você possa gravar o arquivo de saída `JsonSingleCell.xlsx`.

Se algum desses itens estiver ausente, instale o JDK, faça o download do JAR do Aspose.Cells e crie o modelo conforme descrito na próxima seção.

## Etapa 1: Criar um modelo Excel com um smart‑marker

Um smart‑marker indica ao Aspose.Cells onde inserir os dados. Neste caso, queremos que todo o array JSON seja tratado como um único valor, então colocamos o marcador a seguir na célula de destino (por exemplo, **A1**):

```
${jsonArray:ArrayAsSingle}
```

> **Dica profissional:** O modificador `ArrayAsSingle` instrui o processador a renderizar todo o array em uma única célula ao invés de expandi‑lo em uma tabela. Esta é a opção chave para o cenário de **converter JSON para Excel** demonstrado mais adiante.

Salve a pasta de trabalho como `SmartMarkerTemplate.xlsx` em uma pasta que você referenciará a partir do seu código Java.

## Etapa 2: Escrever o programa Java que **converte JSON para Excel**

Abaixo está o arquivo fonte completo `JsonSmartMarker.java`. Cada linha está comentada para que você possa ver como o programa **preenche Excel a partir de JSON** e **processa JSON no Excel**.

```java
import com.aspose.cells.*;

public class JsonSmartMarker {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Define the JSON data that will be merged into the workbook.
        // The array contains two simple objects – you can replace it with any valid JSON.
        String json = "[{\"name\":\"John\",\"age\":30},{\"name\":\"Anna\",\"age\":25}]";

        // 2️⃣ Load the Excel template that already contains the smart‑marker.
        // Adjust the path to match your environment.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 3️⃣ Configure SmartMarker to treat the JSON array as a single value.
        // This option is what makes the **convert JSON to Excel** operation produce one cell.
        SmartMarkerOptions options = new SmartMarkerOptions();
        options.setArrayAsSingle(true);   // key option for single‑cell output

        // 4️⃣ Process the JSON data using the configured options.
        // The SmartMarkerProcessor reads the JSON string, matches the marker,
        // and writes the resulting representation into the workbook.
        workbook.getSmartMarkerProcessor().process(json, options);

        // 5️⃣ Save the resulting workbook. The file now contains the JSON text in the target cell.
        workbook.save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

### Por que cada passo importa

* **Etapa 1** – A string JSON é a fonte de dados. Como definimos `ArrayAsSingle`, o processador não tentará criar linhas para cada objeto; ao invés disso, ele escreverá o texto JSON bruto na célula.
* **Etapa 2** – Carregar o modelo separa a apresentação (o layout do Excel) dos dados (o JSON). Esta prática mantém a lógica de **preencher Excel a partir de JSON** limpa e reutilizável.
* **Etapa 3** – `SmartMarkerOptions.setArrayAsSingle(true)` é a única configuração necessária para mudar o comportamento padrão de expansão de arrays. Sem ela, o processador geraria uma tabela, o que não é o que queremos ao **converter JSON para Excel** em uma única célula.
* **Etapa 4** – O método `process` realiza o trabalho pesado de **como processar JSON no Excel**. Ele analisa o JSON, corresponde ao marcador e grava a saída de acordo com as opções.
* **Etapa 5** – Salvar a pasta de trabalho finaliza a conversão. O arquivo de saída `JsonSingleCell.xlsx` pode ser aberto em qualquer aplicativo de planilha.

## Etapa 3: Verificar o resultado

Abra `JsonSingleCell.xlsx`. A célula **A1** (ou a célula onde você colocou `${jsonArray:ArrayAsSingle}`) deve conter a string JSON exata:

```
[{"name":"John","age":30},{"name":"Anna","age":25}]
```

A pasta de trabalho agora contém os dados JSON em uma única célula, provando que o programa converteu JSON para Excel e **preencheu Excel a partir de JSON** com sucesso.

![Excel sheet after JSON data is merged into a single cell using Aspose.Cells](excel-output.png){: .center-image alt="Planilha Excel após os dados JSON serem mesclados em uma única célula usando Aspose.Cells Smart Marker"}

## Etapa 4: Variações comuns e casos de borda

### 4.1 Convertendo uma carga JSON grande

Se o texto JSON exceder o limite padrão de comprimento da célula, aumente a largura da coluna ou defina o `Style` da célula para envolver o texto:

```java
Cell target = workbook.getWorksheets().get(0).getCells().get("A1");
target.getStyle().setWrapText(true);
workbook.getWorksheets().get(0).autoFitColumns();
```

### 4.2 Usando um intervalo nomeado em vez de uma célula fixa

Você pode colocar o smart‑marker dentro de um intervalo nomeado (por exemplo, `JsonCell`) e referenciá‑lo pelo nome no modelo. O código de processamento permanece inalterado; o Aspose.Cells resolve o marcador onde quer que ele apareça.

### 4.3 Mesclando múltiplos objetos JSON em células separadas

Se mais tarde você decidir expandir o array em linhas, basta remover `options.setArrayAsSingle(true)`. O processador gerará uma tabela onde cada objeto ocupa uma linha, e você pode personalizar os cabeçalhos das colunas com marcadores adicionais.

### 4.4 Lidando com estruturas JSON aninhadas

Para objetos aninhados, use notação de ponto no marcador, por exemplo, `${person.name}`. O processador percorrerá a hierarquia automaticamente, permitindo que você **preencha Excel a partir de JSON** com modelos de dados complexos.

## Etapa 5: Dicas para uso em produção

* **Aplicação de licença:** O Aspose.Cells funciona em modo de avaliação com marca d'água. Aplique sua licença antes de chamar `new Workbook(...)` para evitar a marca d'água em produção.
* **Desempenho:** Para arquivos JSON massivos, faça streaming dos dados ao invés de carregar a string inteira na memória. O Aspose.Cells suporta sobrecargas de `InputStream` do método `process`.
* **Tratamento de erros:** Envolva a chamada `process` em um bloco try‑catch para `Exception`. Registre a mensagem da exceção para ajudar a diagnosticar JSON malformado ou marcadores incompatíveis.
* **Testes:** Inclua testes unitários que comparem o valor da célula gerada com a string JSON esperada. Isso garante que sua lógica de **converter JSON para Excel** permaneça confiável após alterações no código.

## Conclusão

Agora você tem um exemplo completo e executável que **converte JSON para Excel**, demonstra como **preencher Excel a partir de JSON** e explica **como processar JSON no Excel** com smart markers do Aspose.Cells. Ajustando o modelo e o `SmartMarkerOptions`, você pode alternar entre saída de célula única e tabelas expandidas, lidar com estruturas aninhadas e integrar a solução em pipelines maiores de processamento de dados.

**Próximos passos**

* Explore outros modificadores de smart‑marker como `:Repeat` e `:If` para criar relatórios mais dinâmicos.
* Combine esta abordagem com fontes CSV ou de banco de dados para criar fluxos de dados híbridos.
* Revise a documentação do Aspose.Cells sobre [Smart Marker syntax](https://docs.aspose.com/cells/java/smart-markers/) para personalizações mais avançadas.

Feliz codificação, e aproveite a automação dos seus fluxos de trabalho Excel com Java!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Importar JSON para Excel de forma eficiente usando Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Importar Dados JSON para Excel usando Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importar Json para Excel Aspose Cells Java](/cells/spanish/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}