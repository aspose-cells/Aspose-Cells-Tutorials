---
category: general
date: 2026-09-27
description: Copiar tabela dinâmica em Java com Aspose.Cells – um guia passo a passo
  que mostra como copiar o intervalo e preservar as definições da tabela dinâmica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: pt
lastmod: 2026-09-27
og_description: Copie a tabela dinâmica em Java usando Aspose.Cells. Siga este tutorial
  completo para copiar intervalos no Aspose.Cells e manter as definições da tabela
  dinâmica intactas.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Copiar uma tabela dinâmica em Java – Guia rápido do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como copiar uma tabela dinâmica em Java usando Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar uma tabela dinâmica em Java usando Aspose.Cells

Se você precisar **copiar tabela dinâmica** de uma pasta de trabalho para outra, este guia mostra exatamente como fazer isso com Aspose.Cells para Java. A solução funciona para qualquer tabela dinâmica que você tenha criado e preserva a definição da tabela dinâmica sem recriação manual.

Você aprenderá como carregar o arquivo de origem, definir o intervalo que contém a tabela dinâmica, copiar esse intervalo para uma nova pasta de trabalho e, finalmente, salvar o resultado. O tutorial também aborda armadilhas comuns, como preservar fontes de dados e lidar com pastas de trabalho grandes.

## O que você precisará

* Java 17 ou posterior (o código também compila com JDK 8+)
* Aspose.Cells for Java 23.9 ou mais recente – a versão mais recente oferece o suporte mais confiável ao **copy range aspose cells**
* Um arquivo Excel de origem que contém uma tabela dinâmica (por exemplo, `SourceWithPivot.xlsx`)
* Um IDE ou ferramenta de construção (Maven/Gradle) que possa referenciar o JAR do Aspose.Cells

## Etapa 1: Carregar a pasta de trabalho de origem que contém a tabela dinâmica

A primeira ação é abrir a pasta de trabalho que contém a tabela dinâmica que você deseja duplicar. Carregar o arquivo cria uma representação em memória de todas as planilhas, células e caches de tabela dinâmica.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Por que isso importa:**  
Aspose.Cells lê toda a pasta de trabalho, incluindo planilhas de cache de tabela dinâmica ocultas. Se você pular esta etapa, a operação subsequente de **copiar tabela dinâmica** perderá a fonte de dados subjacente.

## Etapa 2: Criar uma pasta de trabalho de destino vazia

Em seguida, instancie uma nova pasta de trabalho que receberá a tabela dinâmica copiada. Começar com uma pasta de trabalho limpa evita sobrescritas acidentais.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Dica:** A pasta de trabalho padrão contém uma planilha vazia, o que é perfeito para uma cópia simples. Se precisar copiar para um nome de planilha específico, renomeie `destWs` com `destWs.setName("TargetSheet")`.

## Etapa 3: Definir o intervalo de origem que inclui a tabela dinâmica

Uma tabela dinâmica ocupa um bloco retangular de células. Você deve especificar o intervalo exato; caso contrário, apenas os dados brutos serão copiados. Neste exemplo, assumimos que a tabela dinâmica ocupa **A1:G20**, mas você pode ajustar o endereço para corresponder ao seu arquivo.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Por que isso funciona:**  
Quando você chama `createRange` na coleção `Cells` da planilha, Aspose.Cells inclui a definição da tabela dinâmica, seu cache e qualquer formatação. Este é o núcleo de **como copiar tabela dinâmica** corretamente.

## Etapa 4: Copiar o intervalo definido para a planilha de destino

Agora use o método `copy` para duplicar o intervalo. O método copia tudo dentro do intervalo, incluindo a definição da tabela dinâmica, fórmulas e estilos.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Nota importante:**  
Se você precisar apenas dos dados sem a tabela dinâmica, pode usar `srcRange.copyData`. No entanto, para um verdadeiro **copiar tabela dinâmica**, você deve copiar todo o intervalo conforme mostrado acima.

## Etapa 5: Salvar a pasta de trabalho de destino

Finalmente, grave a nova pasta de trabalho no disco. O arquivo resultante conterá uma tabela dinâmica totalmente funcional, idêntica à de origem.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Executar o programa produz `CopyPivotResult.xlsx` com o mesmo layout de tabela dinâmica, filtros e cálculos do arquivo original.

## Saída esperada

Ao abrir `CopyPivotResult.xlsx` no Excel:

* A tabela dinâmica aparece em **A1:G20** na primeira planilha.
* Todos os campos de linha/coluna, filtros e campos de valor permanecem intactos.
* Atualizar a tabela dinâmica atualiza a mesma fonte de dados da pasta de trabalho de origem (se os dados de origem estiverem incorporados).

## Casos de borda e dicas práticas

| Situação | Como lidar |
|-----------|------------------|
| **A tabela dinâmica abrange mais colunas do que o esperado** | Use `srcWs.getPivotTables().get(0).getPivotTableArea()` para obter o endereço exato programaticamente. |
| **A pasta de trabalho de origem contém várias tabelas dinâmicas** | Itere através de `srcWs.getPivotTables()` e copie cada intervalo individualmente, ajustando os endereços de destino. |
| **Pastas de trabalho grandes causam pressão de memória** | Habilite `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` antes de carregar a origem. |
| **Você precisa copiar apenas a definição da tabela dinâmica, não os dados** | Após copiar, exclua as linhas de dados de origem no destino com `destWs.getCells().deleteRows(startRow, count)`. |
| **O arquivo de destino deve manter a formatação original** | Defina `CopyOptions` com `options.setPasteType(PasteType.ALL)` para uma cópia de fidelidade total. |

**Dica profissional:** Sempre verifique a tabela dinâmica copiada chamando `destWs.getPivotTables().get(0).refresh()` programaticamente. Isso garante que o cache esteja atualizado, especialmente quando os dados de origem residem em uma conexão externa.

## Exemplo completo executável

Abaixo está o programa completo que você pode copiar‑colar em sua IDE. Substitua `YOUR_DIRECTORY` pelo caminho real em sua máquina.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Executar este código **copiará a tabela dinâmica** exatamente como descrito, e demonstra a maneira mais direta de **copy range aspose cells** enquanto preserva a funcionalidade da tabela dinâmica.

## Conclusão

Agora você sabe como **copiar tabela dinâmica** em Java usando Aspose.Cells, desde o carregamento da pasta de trabalho de origem até a gravação do arquivo de destino. O guia cobriu as etapas essenciais, explicou por que cada etapa importa e abordou casos de borda comuns.

Em seguida, você pode explorar:

* **como copiar tabela dinâmica** entre diferentes planilhas dentro da mesma pasta de trabalho
* Usar **copy range aspose cells** para duplicar gráficos ou formatação condicional
* Automatizar a atualização da tabela dinâmica após a cópia para manter os dados atuais

Sinta-se à vontade para experimentar intervalos maiores, múltiplas tabelas dinâmicas ou integrar esta lógica em um pipeline maior de processamento de Excel. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Copiar Tabela Dinâmica em Java – Preservar, Exportar para PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Como atualizar a fonte da Tabela Dinâmica do Excel com Aspose.Cells para Java: Um Guia Abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulação de Tabela Dinâmica do Excel com Aspose.Cells Java: Um Guia Abrangente](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}