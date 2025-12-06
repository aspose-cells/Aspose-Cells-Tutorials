---
date: 2025-12-06
description: Aprenda como adicionar séries de dados, criar tipos de gráfico combinados,
  salvar a planilha do Excel e exportar o gráfico para PNG com Aspose.Cells para Java.
language: pt
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Adicionar séries de dados para criar gráfico combinado usando Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar séries de dados para criar gráfico combinado usando Aspose.Cells

Neste tutorial você **adicionará séries de dados** a uma pasta de trabalho Excel e aprenderá como **criar tipos de gráfico combinado** com Aspose.Cells para Java. Percorreremos cada passo — desde a configuração da pasta de trabalho, adição de séries, personalização da legenda, até **salvar arquivos Excel** e exportar o **gráfico para PNG**. Ao final, você terá um gráfico combinado pronto para uso que pode ser incorporado em relatórios ou dashboards.

## Respostas rápidas
- **Qual biblioteca cria gráficos combinados?** Aspose.Cells para Java  
- **Como adiciono uma série de dados?** Use `chart.getNSeries().add(...)`  
- **Posso exportar o gráfico como imagem?** Sim, com `chart.toImage(...)` (PNG)  
- **Em que formato posso salvar a pasta de trabalho?** `.xlsx` padrão (Excel)  
- **Preciso de licença para produção?** É necessária uma licença válida do Aspose.Cells  

## O que é **add data series** no Aspose.Cells?
Adicionar uma série de dados indica ao gráfico quais células contêm os valores que você deseja plotar. Cada série pode representar uma linha, coluna ou qualquer outro tipo de gráfico, e você pode misturá‑las para criar um **gráfico combinado**.

## Por que criar um **gráfico combinado**?
Um gráfico combinado permite exibir diferentes conjuntos de dados com representações visuais distintas (por exemplo, uma série de linha sobre uma série de colunas) em uma única visualização. Isso é perfeito para comparar tendências com totais, destacar correlações ou oferecer insights mais ricos em um formato compacto.

## Pré‑requisitos
- Java Development Kit (JDK) 8 ou superior  
- Biblioteca Aspose.Cells para Java (baixe no link abaixo)  
- Familiaridade básica com a sintaxe Java e conceitos do Excel  

## Começando

Primeiro, baixe a biblioteca Aspose.Cells para Java no site oficial:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Depois que o JAR for adicionado ao classpath do seu projeto, você pode começar a criar o gráfico.

### Etapa 1: Importar classes do Aspose.Cells
```java
import com.aspose.cells.*;
```

### Etapa 2: Criar uma nova pasta de trabalho
```java
Workbook workbook = new Workbook();
```

### Etapa 3: Acessar a primeira planilha
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Etapa 4: Adicionar um objeto de gráfico combinado  
Começaremos com um gráfico de linha e depois adicionaremos outras séries para obter o efeito de **gráfico combinado**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adicionando Dados ao Gráfico

Agora que o contêiner do gráfico existe, precisamos alimentá‑lo com dados.

### Etapa 5: Definir os intervalos de dados e **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Dica:** O primeiro parâmetro (`"A1:A5"`) é o intervalo para a primeira série, e o segundo (`"B1:B5"`) cria uma segunda série que será combinada com a primeira.

### Etapa 6: Definir os dados de categoria (eixo X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizando o Gráfico

Um bom gráfico conta uma história. Vamos dar a ele títulos, rótulos de eixo e uma legenda clara.

### Etapa 7: Definir título do gráfico e rótulos dos eixos
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Etapa 8: **Add legend chart** e ajustar sua posição
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvando e Exportando o Gráfico

Depois da personalização, você desejará **salvar a pasta de trabalho Excel** e também gerar uma imagem.

### Etapa 9: Salvar a pasta de trabalho como arquivo Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Etapa 10: Exportar o **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> O método `chart.toImage` **gera imagens de gráficos Excel** que podem ser usadas em páginas web, relatórios ou e‑mails.

## Problemas Comuns & Solução de Problemas

| Problema | Solução |
|----------|---------|
| **Nenhum dado aparece** | Verifique se os intervalos de células (`A1:A5`, `B1:B5`, `C1:C5`) realmente contêm dados antes de criar o gráfico. |
| **Legenda sobrepõe o gráfico** | Defina `chart.getLegend().setOverlay(false)` ou mova a legenda para outra posição (por exemplo, `RIGHT`). |
| **Arquivo de imagem está em branco** | Certifique‑se de que o gráfico tenha ao menos uma série e que `chart.toImage` seja chamado após todas as personalizações. |
| **Salvar gera exceção** | Verifique se você tem permissão de escrita no diretório de destino e se o arquivo não está aberto no Excel. |

## Perguntas Frequentes

**P: Como instalo o Aspose.Cells para Java?**  
R: Baixe o JAR no site oficial e adicione‑o ao classpath do seu projeto. O link de download é: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**P: Posso criar outros tipos de gráfico além de linha e coluna?**  
R: Sim, o Aspose.Cells suporta barra, pizza, dispersão, área e muitos outros tipos de gráfico. Consulte a documentação da API para a lista completa.

**P: É necessária licença para uso em produção?**  
R: Uma licença válida do Aspose.Cells é necessária para implantações em produção. Uma versão de avaliação gratuita está disponível para avaliação.

**P: Como altero as cores de cada série?**  
R: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similar) após adicionar as séries.

**P: Onde encontro mais exemplos de código?**  
R: Documentação abrangente e exemplos adicionais estão disponíveis no site de referência da Aspose: [here](https://reference.aspose.com/cells/java/).

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Última atualização:** 2025-12-06  
**Testado com:** Aspose.Cells para Java 24.12  
**Autor:** Aspose  

---