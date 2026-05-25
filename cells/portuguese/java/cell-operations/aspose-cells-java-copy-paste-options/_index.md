---
date: '2026-02-22'
description: Aprenda a automatizar relatórios em Excel com Aspose.Cells em Java usando
  CopyOptions e PasteOptions para manter as fórmulas precisas e colar apenas os valores
  visíveis.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatize Relatórios em Excel – Dominando CopyOptions e PasteOptions em Java
  com Aspose.Cells
url: /pt/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

 Also keep the "## Quick Answers" etc.

Translate sentences.

Let's do it.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatize Relatórios Excel com Aspose.Cells: CopyOptions & PasteOptions em Java

Você está procurando **automatizar relatórios Excel** usando Java? Com Aspose.Cells você pode copiar, colar e ajustar fórmulas programaticamente, garantindo que seus relatórios permaneçam precisos e que apenas os dados necessários sejam transferidos. Neste tutorial vamos percorrer duas funcionalidades essenciais—**CopyOptions.ReferToDestinationSheet** e **PasteOptions**—que permitem preservar referências de fórmulas e colar valores apenas das células visíveis.

## Respostas Rápidas
- **O que `CopyOptions.ReferToDestinationSheet` faz?** Ajusta as fórmulas para apontarem para a planilha de destino ao copiar dados.  
- **Como colar apenas células visíveis?** Defina `PasteOptions.setOnlyVisibleCells(true)` com `PasteType.VALUES`.  
- **Qual versão da biblioteca é necessária?** Aspose.Cells 25.3 ou superior.  
- **Preciso de licença para produção?** Sim, uma licença permanente ou temporária remove as limitações da avaliação.  
- **Posso usar Maven ou Gradle?** Ambos são suportados; veja os trechos de dependência abaixo.

## O que significa “automatizar relatórios Excel”?
Automatizar relatórios Excel significa gerar, consolidar e formatar pastas de trabalho Excel programaticamente, eliminando etapas manuais de copiar‑colar e reduzindo erros. Aspose.Cells fornece uma API rica que permite a desenvolvedores Java manipular planilhas em escala.

## Por que usar CopyOptions e PasteOptions nos relatórios?
- **Manter a integridade das fórmulas** ao mover dados entre planilhas.  
- **Excluir linhas/colunas ocultas** para manter os relatórios limpos e focados.  
- **Aumentar o desempenho** copiando apenas os dados necessários em vez de intervalos inteiros.

## Pré‑requisitos
- Java 8 ou superior.  
- Maven ou Gradle para gerenciamento de dependências.  
- Aspose.Cells 25.3+ (versão de avaliação, licença temporária ou permanente).  

## Configurando Aspose.Cells para Java

Adicione a biblioteca ao seu projeto com uma das opções a seguir:

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Aquisição de Licença
- **Teste Gratuito** – Conjunto completo de recursos para avaliação.  
- **Licença Temporária** – Remove as limitações de avaliação enquanto você testa.  
- **Licença Permanente** – Recomendada para cargas de trabalho de produção.

Inicialize Aspose.Cells no seu código Java:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guia Passo a Passo

### 1. CopyOptions com ReferToDestinationSheet

#### Visão Geral
Definir `CopyOptions.ReferToDestinationSheet` como `true` reescreve as referências de fórmula para que apontem para a nova planilha após a operação de cópia.

#### Etapa 1: Inicializar Workbook e Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Etapa 2: Configurar CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Etapa 3: Executar Operação de Cópia
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Por que isso importa*: Fórmulas que originalmente referenciavam `Sheet1` agora referenciarão corretamente `DestSheet`, mantendo seus relatórios automatizados confiáveis.

**Dica de Solução de Problemas**: Se as fórmulas ainda referenciam a planilha antiga, certifique‑se de que `setReferToDestinationSheet(true)` seja chamado **antes** da cópia.

### 2. PasteOptions para Valores‑Apenas de Células Visíveis

#### Visão Geral
`PasteOptions` permite definir o que será colado. Usando `PasteType.VALUES` juntamente com `onlyVisibleCells=true` copia apenas os valores exibidos, ignorando linhas/colunas ocultas e formatação.

#### Etapa 1: Inicializar Workbook e Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Etapa 2: Configurar PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Etapa 3: Executar Operação de Colagem
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Por que isso importa*: Ideal para extrair dados filtrados ou gerar relatórios limpos sem linhas ocultas ou ruído de formatação.

**Dica de Solução de Problemas**: Verifique se as linhas/colunas estão realmente ocultas no Excel antes de copiar; caso contrário, elas serão incluídas.

## Aplicações Práticas
1. **Consolidação Financeira** – Mesclar planilhas mensais em uma pasta de trabalho mestre mantendo todas as fórmulas precisas.  
2. **Exportação de Dados Filtrados** – Extrair apenas as linhas visíveis de uma tabela filtrada para uma planilha de resumo.  
3. **Geração Programada de Relatórios** – Automatizar a criação noturna de relatórios Excel com valores de célula precisos e referências corretas.

## Considerações de Desempenho
- **Descarte de Workbooks** ao terminar (`wb.dispose();`) para liberar recursos nativos.  
- **Operações em Lote** – Agrupe múltiplas chamadas de copiar/colar para reduzir overhead.  
- **Monitoramento de Memória** – Workbooks grandes podem exigir aumento de heap (`-Xmx2g`).

## Perguntas Frequentes

**Q1: Para que serve `CopyOptions.ReferToDestinationSheet`?**  
R: Reescreve as referências de fórmula para que apontem para a planilha de destino após a cópia, garantindo que as fórmulas dos relatórios permaneçam corretas.

**Q2: Como colar apenas células visíveis?**  
R: Defina `PasteOptions.setOnlyVisibleCells(true)` e escolha `PasteType.VALUES`.

**Q3: Posso usar Aspose.Cells sem comprar uma licença?**  
R: Sim, há uma versão de teste gratuito ou licença temporária para avaliação, mas uma licença permanente é necessária para produção.

**Q4: Por que algumas referências ainda ficam erradas após a cópia?**  
R: Verifique se `ReferToDestinationSheet` está habilitado **antes** da operação de cópia e se as fórmulas de origem não contêm links para pastas de trabalho externas.

**Q5: Quais boas práticas de gerenciamento de memória devo seguir?**  
R: Descarte objetos `Workbook` quando terminar, processe arquivos grandes em blocos e monitore o uso de heap da JVM.

**Q6: É possível combinar CopyOptions e PasteOptions em uma única operação?**  
R: Sim, você pode encadeá‑los primeiro copiando com `CopyOptions` e depois aplicando `PasteOptions` no intervalo de destino.

## Recursos
- **Documentação**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Compra**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Teste Gratuito**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Licença Temporária**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Fórum de Suporte**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Última atualização:** 2026-02-22  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose