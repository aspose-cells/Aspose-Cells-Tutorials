---
title: Criar marcador PDF para planilha de gráfico em Aspose.Cells
linktitle: Criar marcador PDF para planilha de gráfico em Aspose.Cells
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a criar marcadores em PDF para planilhas de gráficos no Aspose.Cells para .NET com este guia passo a passo abrangente.
weight: 13
url: /pt/net/rendering-and-export/create-pdf-bookmark-entry-for-chart-sheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar marcador PDF para planilha de gráfico em Aspose.Cells

## Introdução
O Aspose.Cells para .NET permite que os desenvolvedores manipulem arquivos do Excel programaticamente. Um de seus recursos úteis é a capacidade de criar marcadores de PDF para planilhas de gráficos individuais. Este tutorial o guiará pelo processo passo a passo, facilitando o acompanhamento, independentemente da sua experiência em programação. Pegue seu editor de código e vamos mergulhar!
## Pré-requisitos
Antes de começar, vamos garantir que você tenha tudo o que precisa para seguir adiante:
1.  Aspose.Cells para .NET: Você precisará da biblioteca Aspose.Cells. Se você ainda não a tem, você pode baixá-la em[aqui](https://releases.aspose.com/cells/net/).
2. Visual Studio ou qualquer IDE .NET: você precisará de um ambiente de desenvolvimento onde possa escrever e executar seu código C#.
3. Noções básicas de C#: embora o orientemos em cada etapa, um conhecimento fundamental de codificação em C# será útil.
4. Arquivo Excel de Exemplo: Tenha em mãos um arquivo Excel de exemplo que inclui gráficos. Você pode criar um você mesmo ou usar um arquivo de exemplo para este exercício.
Com esses pré-requisitos verificados, você está pronto para criar marcadores em PDF para planilhas de gráficos com facilidade!
## Pacotes de importação
Agora que estamos todos prontos com os pré-requisitos, vamos pular para o código. Antes de começar a manipular arquivos do Excel, você precisa importar os pacotes necessários. Veja como fazer isso:
### Configure seu ambiente de desenvolvimento
1. Crie um novo projeto: Abra o Visual Studio e crie um novo aplicativo de console C#. Vamos chamá-lo de “AsposePDFBookmarkExample”.
2. Adicionar referência Aspose.Cells: clique com o botão direito do mouse no seu projeto no Solution Explorer, selecione "Manage NuGet Packages" e pesquise por "Aspose.Cells". Instale a versão mais recente.
3. Adicionar diretivas Using:
 Em seu`Program.cs` arquivo, adicione as seguintes linhas no topo:
```csharp
using System;
using System.Collections;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
Esses pacotes permitem que você trabalhe com arquivos do Excel e os renderize em PDFs com marcadores.
Vamos decompor o código para criar marcadores de PDF. Passaremos por cada parte passo a passo.
## Etapa 1: Defina os caminhos do seu diretório
Para organizar seu código, vamos definir onde nossos arquivos estão localizados.
```csharp
string sourceDir = "Your Document Directory"; // por exemplo, @"C:\Documentos\"
string outputDir = "Your Document Directory"; // por exemplo, @"C:\Documentos\Saída\"
```
 Substituir`Your Document Directory` com os caminhos reais onde seu arquivo Excel de amostra está armazenado e onde você deseja que o PDF de saída seja salvo.
## Etapa 2: Carregue a pasta de trabalho do Excel
Em seguida, precisamos carregar a pasta de trabalho do Excel que você deseja manipular.
```csharp
Workbook wb = new Workbook(sourceDir + "sampleCreatePdfBookmarkEntryForChartSheet.xlsx");
```
 Aqui criamos uma instância do`Workbook` class, carregando nosso arquivo Excel de exemplo. Certifique-se de que o nome do arquivo corresponde ao seu arquivo real.
## Etapa 3: Acesse as planilhas
Depois que a pasta de trabalho for carregada, você poderá acessar suas planilhas. 
```csharp
Worksheet sheet1 = wb.Worksheets[0];
Worksheet sheet2 = wb.Worksheets[1];
Worksheet sheet3 = wb.Worksheets[2];
Worksheet sheet4 = wb.Worksheets[3];
```
O código faz referência às quatro planilhas na pasta de trabalho. Certifique-se de que seu arquivo Excel tenha pelo menos quatro planilhas.
## Etapa 4: Criar entradas de marcadores em PDF
É aqui que a mágica acontece! Criaremos entradas de marcadores para cada folha.
```csharp
PdfBookmarkEntry ent1 = new PdfBookmarkEntry {
    Destination = sheet1.Cells["A1"],
    Text = "Bookmark-I"
};
PdfBookmarkEntry ent2 = new PdfBookmarkEntry {
    Destination = sheet2.Cells["A1"],
    Text = "Bookmark-II-Chart1"
};
PdfBookmarkEntry ent3 = new PdfBookmarkEntry {
    Destination = sheet3.Cells["A1"],
    Text = "Bookmark-III"
};
PdfBookmarkEntry ent4 = new PdfBookmarkEntry {
    Destination = sheet4.Cells["A1"],
    Text = "Bookmark-IV-Chart2"
};
```
 Cada`PdfBookmarkEntry`objeto tem uma célula de destino e um rótulo de texto. Esta configuração criará marcadores no PDF que correspondem a áreas nas planilhas do Excel.
## Etapa 5: Organize as entradas dos favoritos
Para criar uma estrutura hierárquica de favoritos, precisamos organizá-los.
```csharp
ArrayList lst = new ArrayList();
ent1.SubEntry = lst;
lst.Add(ent2);
lst.Add(ent3);
lst.Add(ent4);
```
Este código adiciona o segundo, terceiro e quarto marcadores como subentradas sob o primeiro marcador. Agora, quando você clicar em "Bookmark-I" no PDF, ele o levará aos outros marcadores.
## Etapa 6: Crie opções de salvamento de PDF com entradas de favoritos
Agora, vamos preparar as opções de salvamento de PDF com nossos favoritos.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = ent1;
```
 O`PdfSaveOptions` a configuração nos permite incluir marcadores quando o PDF é salvo.
## Etapa 7: Salve o PDF de saída
Finalmente, é hora de salvar seu trabalho!
```csharp
wb.Save(outputDir + "outputCreatePdfBookmarkEntryForChartSheet.pdf", opts);
```
Este comando salva a pasta de trabalho em um arquivo PDF no caminho de saída especificado, completo com seus favoritos úteis.
## Etapa 8: Confirmação de execução
Por fim, vamos imprimir uma mensagem de sucesso para confirmar que tudo ocorreu sem problemas.
```csharp
Console.WriteLine("CreatePdfBookmarkEntryForChartSheet executed successfully.");
```
## Conclusão 
Criar marcadores de PDF para planilhas de gráficos usando o Aspose.Cells for .NET é um processo direto que pode melhorar a usabilidade dos seus documentos Excel. Com apenas algumas linhas de código, você pode navegar facilmente pelo seu PDF, economizando tempo valioso e melhorando seu fluxo de trabalho.
Quer você esteja gerando relatórios ou mantendo conjuntos de dados complexos, esses marcadores tornam o acesso às informações muito mais fácil. Então vá em frente, assuma o controle dos seus documentos e enriqueça-os com esse recurso fantástico!
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma poderosa biblioteca .NET projetada para lidar com manipulações de arquivos do Excel, incluindo leitura, gravação e conversão de planilhas.
### Posso criar marcadores apenas para células específicas?
Sim, você pode definir o destino dos favoritos como qualquer célula da sua planilha.
### Preciso de uma licença para usar o Aspose.Cells?
Embora o Aspose.Cells ofereça um teste gratuito, uma licença paga é necessária para funcionalidade completa para uso em produção.
### Posso criar marcadores para mais de quatro folhas?
Claro! Você pode criar marcadores para quantas folhas quiser seguindo uma estrutura similar no código.
### Onde posso encontrar mais ajuda?
 Você pode conferir o[Fórum de suporte da comunidade Aspose](https://forum.aspose.com/c/cells/9) para quaisquer problemas ou dúvidas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
