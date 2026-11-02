---
category: general
date: 2026-06-21
description: Copie programaticamente um intervalo de planilha em Java usando Aspose.Cells.
  Aprenda como copiar um intervalo do Excel para outra pasta de trabalho de forma
  eficiente.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: pt
og_description: Copie programaticamente um intervalo de planilha em Java. Este guia
  mostra como copiar um intervalo do Excel para outra pasta de trabalho, com código
  completo e dicas.
og_title: Copiar Intervalo de Planilha Programaticamente – Java Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Copiar Intervalo de Planilha Programaticamente – Guia Completo de Java
url: /pt/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Intervalo de Planilha Programaticamente – Guia Completo em Java

Já se perguntou como **copiar programaticamente um intervalo de planilha** sem abrir o Excel manualmente? Você não está sozinho. Seja para duplicar um relatório, clonar um painel baseado em tabela dinâmica ou simplesmente mover dados entre arquivos, fazer isso por código economiza tempo e elimina erros humanos.

Neste tutorial vamos percorrer uma solução limpa, de ponta a ponta, que mostra **como copiar um intervalo do Excel para outra pasta de trabalho** usando Java e a biblioteca Aspose.Cells. Ao final você terá um programa pronto para executar, entenderá o porquê de cada passo e conhecerá as armadilhas a observar.

---

## O Que Você Precisa

- **Java Development Kit (JDK) 11+** – o código compila com qualquer JDK recente.  
- **Aspose.Cells for Java** (versão de avaliação ou licenciada). Adicione a dependência Maven ou faça o download do JAR.  
- Dois arquivos Excel: um `input.xlsx` que contém o intervalo de origem (incluindo uma tabela dinâmica) e um `output.xlsx` vazio onde o intervalo será colocado.  
- Qualquer IDE de sua preferência – IntelliJ IDEA, Eclipse ou até mesmo um editor de texto simples.

É só isso. Sem serviços extras, sem interop COM, apenas Java puro.

---

![Diagrama ilustrando a cópia programática de intervalo de planilha entre duas pastas de trabalho](image.png)

*Texto alternativo da imagem: ilustração da cópia programática de intervalo de planilha*

---

## Etapa 1: Configurar o Projeto e Importar Aspose.Cells

Primeiro de tudo, precisamos da biblioteca no classpath. Se você usa Maven, adicione:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Se preferir um JAR manual, coloque-o na pasta `libs` e adicione ao caminho de compilação.

Por que isso importa: Aspose.Cells nos fornece um modelo de objetos rico (`Workbook`, `Worksheet`, `Range`) que permite copiar dados **incluindo tabelas dinâmicas, fórmulas e formatação** em uma única chamada — algo que a biblioteca Apache POI não faz de forma tão limpa.

---

## Etapa 2: Carregar a Pasta de Trabalho de Origem

Vamos abrir a pasta de trabalho que contém os dados que queremos clonar. O construtor `Workbook` recebe um caminho de arquivo, e o Aspose lerá todo o arquivo na memória.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Dica profissional:* Envolva o carregamento em um bloco try‑catch caso o arquivo possa estar ausente; caso contrário o programa terminará com um erro claro.

---

## Etapa 3: Criar uma Pasta de Trabalho de Destino Vazia

Uma pasta de trabalho nova nos dá uma tela limpa. Não precisamos pré‑popular nenhuma planilha; o Aspose adicionará uma para nós.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Por que não reutilizar a origem? Mantê‑las separadas evita sobrescritas acidentais e torna o código reutilizável para operações em lote.

---

## Etapa 4: Definir o Intervalo Exato a Copiar

É aqui que a mágica de **copiar programaticamente um intervalo de planilha** começa. Selecionamos as células `A1:D20` da primeira planilha do arquivo de origem. O método `createRange` devolve um objeto `Range` que representa exatamente essas células, incluindo tabelas dinâmicas.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Se precisar de um intervalo dinâmico (por exemplo, “última linha usada”), você pode substituir o endereço fixo por `Cells.maxDisplayRange` ou calculá‑lo com `Cells.getMaxDataColumn()` e `Cells.getMaxDataRow()`.

---

## Etapa 5: Adicionar uma Planilha de Destino na Pasta de Trabalho

O Aspose cria uma planilha padrão chamada “Sheet1” ao instanciar `Workbook`. Vamos adicionar uma nova para manter as coisas organizadas, especialmente se você pretende copiar vários intervalos depois.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Você pode dar à planilha um nome amigável:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Etapa 6: Executar a Cópia – Incluindo Tabelas Dinâmicas

Agora a operação central: `copyRange`. Este método copia **valores, fórmulas, formatação e objetos incorporados** (como tabelas dinâmicas) do intervalo de origem para uma célula de destino (`A1` em nossa nova planilha). É a maneira mais simples de alcançar **como copiar intervalo do Excel para outra pasta de trabalho** sem mexer em loops de célula de baixo nível.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Nos bastidores, o Aspose serializa o intervalo de origem em um formato intermediário e depois o desserializa na planilha de destino — assim tudo permanece intacto.

---

## Etapa 7: Salvar a Pasta de Trabalho de Destino e Verificar

Por fim, gravamos a pasta de trabalho de destino no disco. Abra `output.xlsx` no Excel para ver o intervalo copiado, a tabela dinâmica e toda a formatação preservada.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Ao abrir `output.xlsx`, você deverá ver uma planilha chamada “CopiedData” com o mesmo layout de `A1:D20` da origem, incluindo a tabela dinâmica que agora aponta para os dados copiados.

---

## Tratamento de Casos de Borda Comuns

### 1. Copiando Entre Diferentes Versões do Excel
Aspose.Cells funciona com `.xls`, `.xlsx`, `.xlsb` e até `.csv`. Se a origem e o destino usarem formatos diferentes, a biblioteca converte‑os automaticamente. Apenas certifique‑se de que as extensões de arquivo correspondam ao resultado desejado.

### 2. Preservando Fontes de Dados Externas em Tabelas Dinâmicas
Se a tabela dinâmica na origem referencia uma fonte externa (por exemplo, uma conexão de banco de dados), a cópia manterá a string de conexão, mas **não será atualizada automaticamente**. Chame `pivotTable.refreshData()` após a cópia se precisar de resultados atualizados.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Grandes Intervalos e Consumo de Memória
Copiar intervalos massivos (centenas de milhares de linhas) pode elevar o uso de memória. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` antes de carregar arquivos grandes para manter a pegada baixa.

### 4. Múltiplas Planilhas ou Intervalos
Se precisar copiar vários intervalos não contíguos, repita as etapas 4‑6 para cada intervalo, ou use `copyRange` com um intervalo de união (`Cells.createRange("A1:B10,C1:D10")`).

---

## Dicas Profissionais para Automação Robusta

- **Valide o intervalo de origem** antes de copiar. Use `sourceRange.isValid()` para evitar erros em tempo de execução.  
- **Desbloqueie o arquivo de destino** com `FileInfo.setReadOnly(false)` se estiver sobrescrevendo uma pasta de trabalho existente.  
- **Registre as ações** com um logger leve (SLF4J) – especialmente útil ao processar lotes.  
- **Dispose das pastas de trabalho** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) em serviços de longa execução para liberar recursos nativos.

---

## Recapitulação do Exemplo Completo

Abaixo está a classe Java completa, autocontida, que você pode colar no seu IDE e executar. Lembre‑se de substituir `YOUR_DIRECTORY` pelo caminho real da sua máquina.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Saída esperada:** Um arquivo `output.xlsx` com uma planilha chamada “CopiedData”. As células `A1:D20` refletirão a origem, e qualquer tabela dinâmica dentro desse bloco funcionará plenamente, apontando para os dados copiados.

---

## Conclusão

Acabamos de demonstrar uma solução limpa e **programaticamente copiar intervalo de planilha** em Java, respondendo à pergunta comum **como copiar intervalo do Excel para outra pasta de trabalho**. Ao aproveitar a API de alto nível do Aspose.Cells evitamos loops de célula de baixo nível, preservamos tabelas dinâmicas e mantemos o código legível.

O que vem a seguir? Experimente estender esse padrão para:

- Copiar planilhas inteiras em vez de um único intervalo.  
- Processar em lote dezenas de pastas de trabalho em uma pasta.  
- Exportar o intervalo copiado para CSV ou PDF para pipelines de relatórios.

Sinta‑se à vontade para experimentar e, se encontrar algum obstáculo, deixe um comentário. Boa codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como Copiar Múltiplas Colunas no Excel Usando Aspose.Cells Java: Um Guia Completo](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copiar Colunas do Excel de Forma Eficiente Usando Aspose.Cells for Java: Um Guia Abrangente](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Copiar Imagens Entre Planilhas no Excel Usando Aspose.Cells for Java: Um Guia Abrangente](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}