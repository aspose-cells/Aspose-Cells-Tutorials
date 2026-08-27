---
date: 2026-02-14
description: Aprenda a exportar o gráfico para PNG, adicionar séries de dados, combinar
  gráfico de linhas e colunas, salvar a pasta de trabalho como XLSX e adicionar legenda
  ao gráfico usando Aspose.Cells para Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Exportar gráfico para PNG e adicionar série de dados para gráfico combinado
url: /pt/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico para PNG e adicionar séries de dados para gráfico combinado

Neste tutorial você **adicionará séries de dados** a uma pasta de trabalho Excel, **combinará elementos de gráfico de linha e coluna**, e aprenderá como **exportar o gráfico para PNG** usando Aspose.Cells for Java. Percorreremos cada passo — desde a configuração da pasta de trabalho, a adição do gráfico a uma planilha, a personalização da legenda, até **salvar a pasta de trabalho como xlsx** e gerar uma imagem PNG do gráfico. Ao final, você terá um gráfico combinado pronto‑para‑uso que pode ser incorporado em relatórios ou dashboards.

## Respostas rápidas
- **Qual biblioteca cria gráficos combinados?** Aspose.Cells for Java  
- **Como adiciono uma série de dados?** Use `chart.getNSeries().add(...)`  
- **Como exportar o gráfico para png?** Chame `chart.toImage("file.png", ImageFormat.getPng())`  
- **Em que formato de arquivo posso salvar a pasta de trabalho?** `.xlsx` padrão (salvar pasta de trabalho como xlsx)  
- **Preciso de licença para produção?** É necessária uma licença válida do Aspose.Cells  

## O que é **exportar gráfico para PNG** no Aspose.Cells?
Exportar um gráfico para PNG cria uma imagem raster do gráfico Excel que pode ser exibida em páginas web, relatórios ou e‑mails sem exigir o aplicativo Excel.

## Por que criar um **gráfico combinado de linha e coluna**?
Um gráfico combinado permite exibir diferentes conjuntos de dados com representações visuais distintas (por exemplo, uma série de linha sobre uma série de coluna) em uma única visualização. Isso é ideal para comparar tendências com totais, destacar correlações ou oferecer insights mais ricos em um formato compacto.

## Pré‑requisitos
- Java Development Kit (JDK) 8 ou superior  
- Biblioteca Aspose.Cells for Java (download no link abaixo)  
- Familiaridade básica com sintaxe Java e conceitos de Excel  

## Começando

Primeiro, faça o download da biblioteca Aspose.Cells for Java no site oficial:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Depois que o JAR for adicionado ao classpath do seu projeto, você pode começar a construir o gráfico.

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

### Etapa 4: Adicionar um objeto de gráfico combinado à planilha  
Começaremos com um gráfico de linha e, posteriormente, adicionaremos uma série de coluna para obter o efeito de **gráfico combinado de linha e coluna**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adicionando Dados ao Gráfico

Agora que o contêiner do gráfico existe, precisamos alimentá‑lo com dados.

### Etapa 5: Definir os intervalos de dados e **adicionar séries de dados**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Dica profissional:** O primeiro parâmetro (`"A1:A5"`) é o intervalo para a primeira série, e o segundo (`"B1:B5"`) cria uma segunda série que será combinada com a primeira.

### Etapa 6: Definir os dados de categoria (eixo X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizando o Gráfico

Um bom gráfico conta uma história. Vamos dar títulos, rótulos de eixos e uma legenda clara.

### Etapa 7: **Definir rótulos dos eixos do gráfico** e título
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Etapa 8: **Adicionar legenda ao gráfico** e ajustar sua posição
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvando e Exportando o Gráfico

Após a personalização, você desejará **salvar a pasta de trabalho como xlsx** e também gerar uma imagem.

### Etapa 9: Salvar a pasta de trabalho como arquivo Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Etapa 10: **Exportar gráfico para PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> O método `chart.toImage` **gera imagens do gráfico Excel** que podem ser usadas em páginas web, relatórios ou e‑mails.

## Problemas Comuns & Solução de Problemas

| Problema | Solução |
|----------|---------|
| **Nenhum dado aparece** | Verifique se os intervalos de células (`A1:A5`, `B1:B5`, `C1:C5`) realmente contêm dados antes de criar o gráfico. |
| **Legenda sobrepõe o gráfico** | Defina `chart.getLegend().setOverlay(false)` ou mova a legenda para outra posição (por exemplo, `RIGHT`). |
| **Arquivo de imagem está em branco** | Certifique‑se de que o gráfico tem ao menos uma série e que `chart.toImage` é chamado após todas as personalizações. |
| **Salvar gera exceção** | Verifique se você tem permissão de escrita no diretório de destino e se o arquivo não está aberto no Excel. |

## Perguntas Frequentes

**P: Como instalo o Aspose.Cells for Java?**  
R: Baixe o JAR no site oficial e adicione‑o ao classpath do seu projeto. O link de download é: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**P: Posso criar outros tipos de gráfico além de linha e coluna?**  
R: Sim, o Aspose.Cells suporta barra, pizza, dispersão, área e muitos outros tipos de gráfico. Consulte a documentação da API para a lista completa.

**P: É necessária uma licença para uso em produção?**  
R: Uma licença válida do Aspose.Cells é necessária para implantações em produção. Uma avaliação gratuita está disponível.

**P: Como altero as cores de cada série?**  
R: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (ou similar) após adicionar as séries.

**P: Onde encontro mais exemplos de código?**  
R: Documentação completa e exemplos adicionais estão disponíveis no site de referência da Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Última atualização:** 2026-02-14  
**Testado com:** Aspose.Cells for Java versão mais recente  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}