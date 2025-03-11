---
title: Conversão de gráfico para imagem em .NET
linktitle: Conversão de gráfico para imagem em .NET
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como converter gráficos em imagens no .NET usando Aspose.Cells com este guia passo a passo. Converta facilmente gráficos do Excel em imagens de alta qualidade.
weight: 10
url: /pt/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversão de gráfico para imagem em .NET

## Introdução
Converter um gráfico do Excel em uma imagem pode ser um requisito crucial ao criar sistemas de relatórios ou compartilhar representações visuais de dados. Felizmente, com o Aspose.Cells para .NET, esse processo é muito fácil! Quer você esteja gerando relatórios ou simplesmente convertendo gráficos do Excel em imagens para melhor exibição, este guia o guiará pelo processo passo a passo.
## Pré-requisitos
Antes de começar, vamos garantir que você tenha tudo pronto para seguir este tutorial.
### Biblioteca Aspose.Cells para .NET
Primeiro, você precisará baixar e referenciar a biblioteca Aspose.Cells for .NET no seu projeto. Você pode pegar a versão mais recente aqui:
- [Baixe Aspose.Cells para .NET](https://releases.aspose.com/cells/net/)
### Ambiente .NET
Certifique-se de ter o .NET framework instalado no seu sistema. Você pode usar o Visual Studio ou qualquer outro ambiente de desenvolvimento .NET para executar este exemplo.
### Configuração de licença (opcional)
 Embora você possa usar o Aspose.Cells com uma avaliação gratuita, para funcionalidade completa sem limitações, considere solicitar uma[licença temporária](https://purchase.aspose.com/temporary-license/) ou compre um de[aqui](https://purchase.aspose.com/buy).

## Pacotes de importação
Para começar, vamos importar os namespaces necessários para trabalhar com a biblioteca Aspose.Cells. Isso nos permitirá manipular arquivos do Excel e gerar imagens.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Certifique-se de ter esses pacotes prontos antes de iniciar a parte de codificação.

Agora, vamos dividir o processo de conversão de um gráfico em uma imagem em etapas simples.
## Etapa 1: configure seu diretório de projeto
Você precisa de um lugar para salvar suas imagens geradas, certo? Vamos primeiro criar um diretório onde as imagens de saída serão salvas.

Começamos definindo o caminho para nosso diretório de documentos e garantindo que a pasta exista. Se não existir, criaremos uma.
```csharp
// Defina o diretório para salvar as imagens
string dataDir = "Your Document Directory";
//Verifique se o diretório existe
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Com esta etapa, você está pronto para gerar e salvar suas imagens de gráfico neste diretório.
## Etapa 2: Crie uma nova pasta de trabalho
Aqui, instanciaremos um objeto Workbook. Isso representará nosso arquivo Excel onde o gráfico será incorporado.

Uma pasta de trabalho é como um arquivo Excel que contém planilhas. Ao criar uma nova pasta de trabalho, estamos começando do zero com um arquivo Excel vazio.
```csharp
// Criar um novo objeto Workbook
Workbook workbook = new Workbook();
```
## Etapa 3: Adicionar uma nova planilha
Todo arquivo Excel tem planilhas (ou abas). Vamos adicionar uma à nossa pasta de trabalho.

Adicionar uma nova planilha é essencial, pois inseriremos nossos dados e gráficos nessa planilha. Uma vez que a planilha é adicionada, recuperamos sua referência.
```csharp
// Adicionar uma nova planilha à pasta de trabalho
int sheetIndex = workbook.Worksheets.Add();
// Recuperar a planilha recém-adicionada
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Etapa 4: preencher a planilha com dados
Para criar um gráfico significativo, precisamos de alguns dados, certo? Vamos preencher algumas células com valores de amostra.

Adicionaremos dados a células específicas na planilha. Esses dados serão usados para gerar nosso gráfico mais tarde.
```csharp
// Adicionar dados de amostra às células
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Etapa 5: Adicionar um gráfico à planilha
Agora, vamos criar um gráfico de colunas que visualize os dados que acabamos de adicionar.

Especificamos o tipo de gráfico (gráfico de colunas) e definimos seu tamanho e posição dentro da planilha.
```csharp
// Adicionar um gráfico de colunas à planilha
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Etapa 6: Defina a fonte de dados do gráfico
É aqui que a mágica acontece: vinculando o gráfico aos dados na planilha!

Nós vinculamos o gráfico aos dados nas colunas A1 a B3. Isso informa ao gráfico de onde extrair os dados.
```csharp
// Vincule o gráfico aos dados no intervalo A1 a B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Etapa 7: converter o gráfico em uma imagem
O momento da verdade: vamos converter este gráfico em um arquivo de imagem!

 Aqui, usamos o`ToImage` método para converter o gráfico em um formato de imagem de sua escolha. Neste caso, estamos convertendo-o para um formato EMF (Enhanced Metafile).
```csharp
// Converta o gráfico em uma imagem e salve-o no diretório
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
E é isso! Seu gráfico agora foi salvo como uma imagem. Hora de dar um tapinha nas costas.
## Etapa 8: Exibir mensagem de sucesso
Para finalizar, vamos exibir uma mensagem confirmando a geração da imagem.
```csharp
// Exibir uma mensagem para indicar sucesso
System.Console.WriteLine("Image generated successfully.");
```
## Conclusão
Boom! É assim que é fácil converter um gráfico do Excel para uma imagem usando o Aspose.Cells para .NET. Esse processo não só simplifica a apresentação de dados, mas também aumenta a flexibilidade de relatórios ou painéis onde imagens são preferidas em vez de gráficos incorporados.
Seguindo as etapas descritas neste guia, agora você pode converter qualquer gráfico do Excel em uma imagem, permitindo que você integre dados visuais em vários aplicativos perfeitamente.
## Perguntas frequentes
### Posso converter diferentes tipos de gráficos usando este método?
Sim, você pode converter qualquer tipo de gráfico suportado pelo Aspose.Cells, incluindo gráficos de pizza, gráficos de barras, gráficos de linhas e muito mais!
### É possível alterar o formato da imagem?
 Claro! Embora tenhamos usado EMF neste exemplo, você pode alterar o formato da imagem para PNG, JPEG, BMP e outros simplesmente modificando o`ImageFormat` parâmetro.
### O Aspose.Cells suporta imagens de alta resolução?
Sim, o Aspose.Cells permite que você controle as configurações de resolução e qualidade da imagem ao exportar gráficos para imagens.
### Posso converter vários gráficos em imagens de uma só vez?
Sim, você pode percorrer vários gráficos em uma pasta de trabalho e convertê-los em imagens em apenas algumas linhas de código.
### Existe um limite para o número de gráficos que posso converter?
Não há limite inerente imposto pelo Aspose.Cells, mas o processamento de grandes quantidades de dados pode depender da memória e dos recursos de desempenho do seu sistema.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
