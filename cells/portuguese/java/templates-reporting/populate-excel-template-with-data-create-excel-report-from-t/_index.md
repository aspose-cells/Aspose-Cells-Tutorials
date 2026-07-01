---
category: general
date: 2026-06-30
description: Preencha o modelo Excel com dados usando SmartMarkerProcessor e aprenda
  como criar um relatório Excel a partir do modelo em Java – guia passo a passo.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: pt
og_description: Preencha o modelo Excel com dados usando SmartMarkerProcessor. Este
  guia mostra como criar um relatório Excel a partir de um modelo em Java, completo
  com código.
og_title: Preencher Modelo de Excel com Dados – Criar Relatório de Excel a partir
  do Modelo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Preencher Modelo de Excel com Dados – Criar Relatório de Excel a partir do
  Modelo
url: /pt/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preencher Modelo Excel com Dados – Criar Relatório Excel a partir do Modelo

Já precisou **preencher um modelo Excel com dados** mas não sabia qual biblioteca poderia fazer o trabalho pesado? Você não está sozinho. Quando você está construindo dashboards mensais, faturas ou qualquer tipo de planilha orientada a dados, fazer isso manualmente rapidamente se torna um pesadelo.  

A boa notícia é que o SmartMarkerProcessor do Aspose.Cells torna tudo simples — basta fornecer um modelo e uma fonte de dados, e você terá um relatório Excel polido em segundos. Neste tutorial também mostraremos **como criar um relatório Excel a partir de um modelo** usando Java puro, para que você possa inserir a solução diretamente no seu projeto.

## Pré‑requisitos (O que você precisará)

- Java 17 ou superior (o código compila com versões mais antigas, mas 17 oferece os recursos mais recentes da linguagem).  
- Aspose.Cells para Java (o artefato Maven `com.aspose:aspose-cells` versão 24.9 ou posterior).  
- Um arquivo Excel que contenha Smart Markers (por exemplo, `input.xlsx`).  
- Uma fonte de dados simples que implemente `IDataSource` (construiremos uma para você).  

Nenhum IDE especial é necessário — qualquer editor que consiga compilar Java serve.  

---

## Preencher Modelo Excel com Dados – Passo a Passo

A seguir dividimos o processo em seis etapas lógicas. Cada etapa inclui **por que** ela importa, não apenas **o que** digitar.

### Etapa 1: Instanciar o SmartMarkerProcessor  

O processador é o motor que varre sua pasta de trabalho, encontra Smart Markers e os substitui por valores reais.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Por que?*  
Criar um processador novo garante que você comece com um estado limpo. Se reutilizar uma instância antiga, configurações residuais podem vazar para a próxima execução — algo que você definitivamente quer evitar em um trabalho de produção.

### Etapa 2 (Opcional): Renomear a Planilha de Detalhe  

Smart Markers costumam gerar uma planilha “detail” oculta que contém dados intermediários. Renomeá‑la torna a pasta de trabalho final mais fácil de navegar.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Dica de especialista:*  
Se o seu modelo já contém uma planilha chamada “Detail”, dê à planilha gerada um sufixo único (por exemplo, `CopyOfDetail_2024`) para evitar colisões de nomes.

### Etapa 3: Carregar a Pasta de Trabalho Modelo  

É aqui que você aponta o processador para o arquivo Excel que contém os marcadores.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Por que?*  
Carregar a pasta de trabalho na memória permite que o Aspose.Cells a manipule sem tocar no arquivo original no disco. Você pode reutilizar com segurança o mesmo arquivo modelo para vários relatórios.

### Etapa 4: Preparar uma Fonte de Dados  

SmartMarkerProcessor espera uma implementação de `IDataSource` que saiba como obter valores para cada marcador. Abaixo está uma fonte de dados **in‑memory** mínima que usa um `Map<String, Object>`.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*Por que essa implementação?*  
É leve, não requer banco de dados externo e é perfeita para demonstrações ou testes unitários. Em um cenário real você substituiria `MapDataSource` por algo que busque em um result set JDBC, uma API REST ou uma entidade ORM.

### Etapa 5: Aplicar os Dados à Pasta de Trabalho  

Agora a mágica acontece — os Smart Markers são substituídos pelos valores do seu `IDataSource`.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*O que está acontecendo nos bastidores?*  
O Aspose.Cells itera sobre cada célula que contém um marcador como `${EmployeeName}`. Para cada marcador, ele chama `IDataSource.getValue("EmployeeName")` e grava o valor retornado na célula. Se você tivesse um marcador de tabela (`${Employees}`), o processador expandiria automaticamente as linhas com base no tamanho do array.

### Etapa 6: Salvar a Pasta de Trabalho Processada  

Por fim, escreva a pasta de trabalho preenchida no disco (ou envie-a diretamente para a resposta HTTP se estiver em uma aplicação web).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Dica:*  
Use a sobrecarga `workbook.save(OutputStream, SaveFormat.XLSX)` quando precisar enviar o arquivo ao cliente sem tocar no sistema de arquivos.

---

## Criar Relatório Excel a partir do Modelo – Dicas Avançadas

Agora que o fluxo básico funciona, vamos explorar algumas melhorias comuns que tornam seu **relatório Excel a partir do modelo** pronto para produção.

### H3: Manipulação de Coleções (Tabelas)

Se o seu modelo contém um bloco repetitivo, como uma tabela de vendas, substitua o marcador por um array na sua fonte de dados.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

No modelo você teria marcadores como `${SalesData.Product}`, `${SalesData.Qty}`, etc., dentro de uma linha que o Aspose replicará para cada entrada.

### H3: Formatação de Datas e Números

Smart Markers respeitam a formatação da célula. Se você pré‑formatar uma célula como *Currency* no modelo, o valor numérico que você inserir será exibido automaticamente com o símbolo correto e casas decimais. Nenhum código extra necessário — apenas certifique‑se de que o tipo de dado que você retorna (`Double`, `BigDecimal`, `LocalDate`) corresponde ao formato esperado.

### H3: Considerações de Desempenho

- **Reutilize o processador** se você gerar dezenas de relatórios em lote; basta chamar `processor.clear()` entre as execuções.  
- **Desative o cálculo** (`workbook.getSettings().setRecalcOnLoad(false)`) quando precisar apenas gravar valores, sem recalcular fórmulas.  
- **Faça streaming da saída** para evitar arquivos temporários grandes ao executar em ambientes com recursos limitados.

---

## Saída Esperada

Após executar o exemplo de seis etapas, `output.xlsx` conterá:

| A               | B          | C            |
|-----------------|------------|--------------|
| EmployeeName    | Jane Doe   |              |
| Department      | Engineering|              |
| Salary          | 95,000     |              |
| ReportDate      | 2026‑06‑30 |              |
| …               | …          | …            |

Se você adicionou o exemplo de tabela, verá uma tabela de vendas totalmente preenchida logo abaixo das linhas de cabeçalho. Toda a formatação que você aplicou em `input.xlsx` (símbolos de moeda, padrões de data, cabeçalhos em negrito) permanece intacta.

---

## Conclusão

Acabamos de percorrer como **preencher um modelo Excel com dados** usando o `SmartMarkerProcessor` do Aspose.Cells, e agora você conhece os passos exatos para **criar um relatório Excel a partir do modelo** em Java. A ideia central é simples: defina Smart Markers em uma pasta de trabalho reutilizável, forneça um `IDataSource` compatível e deixe a biblioteca fazer o trabalho pesado.  

A partir daqui você pode:

- Substituir o `MapDataSource` por um banco de dados real.  
- Adicionar gráficos que reflitam automaticamente os novos dados.  
- Implantar o código como um microserviço que devolve o arquivo Excel gerado sob demanda.  

Teste, ajuste os marcadores e veja seu fluxo de relatórios encolher drasticamente. Tem dúvidas ou um cenário de marcador complicado? Deixe um comentário abaixo — boa codificação!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Populate Excel with Nested Data Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Export XML Data from Excel using Aspose.Cells in Java: Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}