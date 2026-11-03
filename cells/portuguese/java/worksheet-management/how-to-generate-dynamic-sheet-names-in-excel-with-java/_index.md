---
category: general
date: 2026-09-27
description: Aprenda como gerar nomes de planilhas dinâmicos no Excel com Java enquanto
  preenche um modelo do Excel e cria planilhas a partir dos dados para relatórios
  robustos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: pt
lastmod: 2026-09-27
og_description: Nomes de planilhas dinâmicos permitem gerar várias planilhas a partir
  de um conjunto de dados. Este tutorial mostra como preencher um modelo do Excel
  em Java e criar planilhas a partir dos dados usando o Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Gerar nomes de planilhas dinâmicos no Excel com Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como gerar nomes de planilhas dinâmicos no Excel com Java
url: /pt/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como gerar nomes de planilhas dinâmicos no Excel com Java

Se você precisa de **nomes de planilhas dinâmicos** ao preencher um modelo do Excel em Java, este guia o conduzirá por todo o processo. Você verá como *gerar múltiplas planilhas* a partir de uma coleção de dados e como cada planilha recebe um nome exclusivo automaticamente. Ao final, você terá um exemplo executável que cria planilhas a partir dos dados e salva o resultado com a convenção de nomenclatura desejada.

Gerar planilhas sob demanda é uma necessidade comum para dashboards de relatórios, lotes de faturas ou qualquer cenário em que o número de seções detalhadas não seja conhecido previamente. O motor Smart Marker do Aspose.Cells torna essa tarefa concisa e confiável, e o código abaixo demonstra a abordagem recomendada.

## Usando nomes de planilhas dinâmicos com Aspose.Cells

Aspose.Cells for Java fornece um processador **Smart Marker** que pode ler marcadores de posição em uma pasta de trabalho modelo e expandi‑los em linhas, colunas ou até novas planilhas. Ao configurar `SmartMarkerOptions.DetailSheetNewName` você controla o nome de cada planilha gerada. O marcador `{0}` é substituído pelo índice baseado em zero da linha de dados atual, fornecendo nomes de planilha totalmente **dinâmicos** como `Detail_0`, `Detail_1`, …​.

> **Dica profissional:** Mantenha a pasta de trabalho modelo em uma pasta de recursos dedicada e use um caminho relativo sempre que possível. Isso evita codificar caminhos absolutos que quebram em ambientes diferentes.

## Etapa 1: Carregar o modelo Excel (populate excel template java)

Primeiro, carregue a pasta de trabalho que contém as tags Smart Marker. O modelo deve ter uma planilha chamada, por exemplo, `Detail` com um marcador como `&=Orders!A1` que indica ao processador onde começar a inserir linhas.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Por que esta etapa importa:* O modelo define o layout (cabeçalhos, fórmulas, formatação) que será copiado para cada planilha gerada. Sem um modelo adequado, a saída perderia estilos e fórmulas.

## Etapa 2: Preparar a fonte de dados para criar planilhas a partir dos dados

Em seguida, construa uma fonte de dados que o processador Smart Marker possa iterar. Neste exemplo usamos um `Map<String, Object>` onde a chave `"Orders"` corresponde ao nome do marcador no modelo.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Por que esta etapa importa:* O motor Smart Marker lê o array, cria uma linha para cada `Object[]` interno e—como pediremos que ele gere novas planilhas—cria uma planilha separada para cada linha. Esse é o núcleo de **criar planilhas a partir de dados**.

## Etapa 3: Configurar SmartMarkerOptions para gerar múltiplas planilhas com nomes exclusivos

Agora informe ao Aspose.Cells como nomear cada nova planilha. O marcador `{0}` será substituído pelo índice da linha atual.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Por que esta etapa importa:* Sem definir `DetailSheetNewName`, o processador reutilizaria o nome da planilha original para cada linha, sobrescrevendo os dados. Esta opção habilita **nomes de planilhas dinâmicos**.

## Etapa 4: Processar os SmartMarkers e gerar a pasta de trabalho

Execute o processador com a fonte de dados e as opções que acabamos de configurar.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Por que esta etapa importa:* O processador expande os marcadores, cria o número necessário de planilhas, copia o layout do modelo e preenche cada planilha com os dados da linha correspondente.

## Etapa 5: Salvar e verificar o resultado

Por fim, grave a pasta de trabalho no disco. Abra o arquivo no Excel para ver as planilhas criadas automaticamente.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Saída esperada**

Ao abrir `MasterDetailResult.xlsx` você deverá ver três novas planilhas:

* `Detail_0` – contém o pedido 101 (Alice, 250.00)  
* `Detail_1` – contém o pedido 102 (Bob, 175.50)  
* `Detail_2` – contém o pedido 103 (Carol, 320.75)

Cada planilha mantém a formatação, larguras de coluna e quaisquer fórmulas que existiam na planilha modelo original `Detail`.

## Exemplo completo executável

Juntando todas as seções, você obtém um programa autocontido que pode ser compilado e executado:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Como executar

1. Adicione o JAR do Aspose.Cells for Java ao classpath do seu projeto (disponível no Maven Central ou no site da Aspose).  
2. Coloque `MasterDetailTemplate.xlsx` em `templates/` relativo à raiz do projeto.  
3. Execute o método `main`. A pasta `output/` conterá o arquivo gerado.

## Variações comuns e casos de borda

| Situação | O que mudar |
|-----------|----------------|
| **Padrão de nomenclatura diferente** | Use `"OrderSheet_{0}_v{1}"` e inclua marcadores adicionais como `{1}` para um segundo índice (por exemplo, número da página). |
| **Conjuntos de dados grandes** | Aumente o heap da JVM (`-Xmx2g`) para evitar `OutOfMemoryError` ao gerar centenas de planilhas. |
| **Criação condicional de planilhas** | Antes de chamar `process`, filtre o array de dados para que linhas que não atendam a um critério sejam omitidas, evitando planilhas desnecessárias. |
| **Preservar fórmulas que referenciam outras planilhas** | Mantenha o nome original da planilha como um marcador oculto (ex.: `DetailTemplate`) e use `SmartMarkerOptions.setDetailSheetNewName` apenas para o nome visível; as fórmulas que referenciam o nome oculto ainda serão resolvidas corretamente. |

## Dicas para automação robusta do Excel

* **Validar a fonte de dados** – Garanta que cada array interno tenha o mesmo número de elementos das colunas definidas no modelo; comprimentos incompatíveis causam erros em tempo de execução.  
* **Usar intervalos nomeados** no modelo para uma sintaxe Smart Marker mais clara (`&=Orders!A1`).  
* **Fechar recursos** – Embora o Aspose.Cells gerencie streams internamente, chamar explicitamente `templateWorkbook.dispose()` em um bloco `finally` pode liberar memória nativa mais rapidamente.  
* **Testar com valores de borda** – Zero linhas devem produzir uma pasta de trabalho contendo apenas a planilha modelo original; uma fonte de dados vazia verifica se seu código lida com “nenhum dado” de forma elegante.

## Conclusão

Agora você sabe como **gerar nomes de planilhas dinâmicos** no Excel usando Java, como **preencher um modelo Excel** e **criar planilhas a partir de dados**, e como **gerar múltiplas planilhas** automaticamente com Smart Markers do Aspose.Cells. Seguindo os passos acima, você pode adaptar o padrão a qualquer cenário de relatório—seja precisando de dezenas de planilhas detalhadas, convenções de nomenclatura personalizadas ou criação condicional de planilhas.

Pronto para expandir esta solução? Experimente adicionar gráficos a cada planilha gerada ou exportar a pasta de trabalho para PDF usando `Workbook.save("result.pdf", SaveFormat.PDF)`. Ambas as técnicas se baseiam na mesma fundação de planilhas dinâmicas que você acabou de dominar. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Master Dynamic Excel Sheets in Java with Aspose.Cells: A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}