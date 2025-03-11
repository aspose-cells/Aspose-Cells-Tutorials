---
title: Adicionar botão de opção à planilha no Excel
linktitle: Adicionar botão de opção à planilha no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda como adicionar botões de opção a uma planilha do Excel usando Aspose.Cells para .NET com este guia passo a passo fácil. Perfeito para criar formulários interativos do Excel.
weight: 19
url: /pt/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar botão de opção à planilha no Excel

## Introdução
Já se perguntou como apimentar suas planilhas do Excel com elementos interativos como botões de opção? Não importa se você está criando uma pesquisa, um formulário ou uma ferramenta de análise, adicionar botões de opção pode realmente melhorar a interação do usuário. Neste tutorial, vamos orientá-lo no processo de adicionar botões de opção às suas planilhas do Excel usando o Aspose.Cells para .NET. Vamos dividir tudo em etapas fáceis de seguir, garantindo que você seja um profissional até o final deste artigo. Pronto para mergulhar? Vamos começar!
## Pré-requisitos
Antes de começarmos a parte divertida de adicionar botões de opção, vamos garantir que você tenha tudo configurado para começar.
1.  Aspose.Cells para .NET: Primeiro, certifique-se de ter baixado e instalado o[Aspose.Cells para .NET](https://releases.aspose.com/cells/net/) biblioteca. Você pode obtê-lo via NuGet no Visual Studio ou na página de download.
2. IDE (Ambiente de Desenvolvimento Integrado): Você precisará de um IDE como o Visual Studio para escrever e executar seu código C#.
3. .NET Framework: Certifique-se de ter o .NET Framework 4.0 ou superior instalado em sua máquina. O Aspose.Cells requer isso para funcionar.
4. Noções básicas de C#: a familiaridade com a sintaxe C# e a programação .NET tornará as coisas mais fáceis à medida que você acompanha o tutorial.
Depois que tudo estiver pronto, estamos prontos para começar!
## Pacotes de importação
Antes de codificar, é essencial importar os namespaces necessários para evitar erros mais tarde. Adicione o seguinte ao seu código:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Essas importações são essenciais para acessar funcionalidades da pasta de trabalho, adicionar botões de opção e manipular operações de arquivo.
## Etapa 1: Configurando a pasta de trabalho
Primeiramente, vamos criar uma nova pasta de trabalho do Excel.
 Para começar, você precisará instanciar um novo`Workbook` objeto. Isso representará seu arquivo Excel em código.
```csharp
// Instanciar uma nova pasta de trabalho.
Workbook excelbook = new Workbook();
```
Nesta etapa, você está criando uma pasta de trabalho em branco. Imagine-a como sua tela em branco onde você adicionará botões de opção em etapas subsequentes.
## Etapa 2: Adicionar e formatar um valor de célula
Em seguida, vamos adicionar um título à planilha. Adicionaremos algum texto à célula`C2` e formate-o para deixá-lo em negrito. Esta etapa adiciona contexto aos seus botões de opção.
### Inserir texto na célula
```csharp
// Insira um valor na célula C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Deixe o texto em negrito
```csharp
// Defina o texto da fonte na célula C2 como negrito.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
 Aqui, adicionamos um título simples, “Faixas etárias”, na célula`C2`, e o deixou em negrito para que se destacasse. Fácil, certo?
## Etapa 3: Adicionando o primeiro botão de opção
Agora vem a parte mais emocionante: adicionar seu primeiro botão de opção à planilha!
### Adicionar um botão de opção
```csharp
// Adicione um botão de opção à primeira planilha.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Esta linha adiciona o botão de opção a uma posição específica na sua planilha. Os números representam seu posicionamento e tamanho. Pense nisso como definir as coordenadas X e Y do botão.
### Definir texto do botão de opção
```csharp
// Defina sua sequência de texto.
radio1.Text = "20-29";
```
Aqui, demos ao botão de opção um rótulo, “20-29”, representando uma faixa etária.
### Vincular o botão de opção a uma célula
```csharp
// Defina a célula A1 como uma célula vinculada para o botão de opção.
radio1.LinkedCell = "A1";
```
 Isso vincula o botão de opção à célula`A1`o que significa que o resultado da seleção do botão será armazenado nessa célula.
### Adicionar efeito 3D
```csharp
// Torne o botão de opção 3D.
radio1.Shadow = true;
```
Como queremos que esse botão de opção se destaque, adicionamos um efeito 3D.
### Personalize a linha do botão de opção
```csharp
// Defina o peso da linha do botão de opção.
radio1.Line.Weight = 4;
// Defina o estilo do traço da linha do botão de opção.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Essas linhas de código ajustam a espessura e o estilo do traço da borda do botão de opção para torná-lo mais atraente visualmente.
## Etapa 4: Adicionando botões de opção adicionais
Vamos adicionar mais dois botões de opção para as faixas etárias restantes: "30-39" e "40-49". As etapas são as mesmas, apenas com pequenas variações nas coordenadas e rótulos.
### Adicione o segundo botão de opção
```csharp
// Adicione outro botão de opção à primeira planilha.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Defina sua sequência de texto.
radio2.Text = "30-39";
// Defina a célula A1 como uma célula vinculada para o botão de opção.
radio2.LinkedCell = "A1";
// Torne o botão de opção 3D.
radio2.Shadow = true;
// Defina o peso do botão de opção.
radio2.Line.Weight = 4;
// Defina o estilo do traço do botão de opção.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Adicione o terceiro botão de opção
```csharp
// Adicione outro botão de opção à primeira planilha.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Defina sua sequência de texto.
radio3.Text = "40-49";
// Defina a célula A1 como uma célula vinculada para o botão de opção.
radio3.LinkedCell = "A1";
// Torne o botão de opção 3D.
radio3.Shadow = true;
// Defina o peso do botão de opção.
radio3.Line.Weight = 4;
// Defina o estilo do traço do botão de opção.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Etapa 5: salvando o arquivo Excel
Depois que todos os seus botões de opção forem adicionados e formatados, é hora de salvar o arquivo.
```csharp
// Salve o arquivo Excel.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
Nesta etapa, a pasta de trabalho é salva no diretório especificado. É simples assim — sua planilha interativa agora está pronta!
## Conclusão
Pronto! Você acabou de adicionar botões de opção a uma planilha do Excel usando o Aspose.Cells para .NET. Este tutorial abordou tudo, desde a configuração da pasta de trabalho, inserção e formatação de um valor, adição de vários botões de opção e vinculação deles a uma célula. Agora, você está pronto para criar planilhas interativas do Excel que não só têm uma ótima aparência, mas também fornecem uma experiência de usuário aprimorada. Divirta-se explorando mais possibilidades com o Aspose.Cells!
## Perguntas frequentes
### Posso adicionar mais botões de opção a planilhas diferentes?  
Absolutamente! Você pode repetir o processo em qualquer planilha dentro da pasta de trabalho especificando o índice correto da planilha.
### Posso personalizar ainda mais a aparência dos botões de opção?  
Sim, o Aspose.Cells oferece uma variedade de opções de personalização, incluindo alteração de cores, tamanhos e outros atributos de formatação.
### Como posso detectar qual botão de opção está selecionado?  
célula vinculada (por exemplo, A1) mostrará o índice do botão de opção selecionado. Você pode verificar o valor da célula vinculada para descobrir qual está selecionada.
### Existe um limite para o número de botões de opção que posso adicionar?  
Não, não há um limite rígido para o número de botões de rádio que você pode adicionar. No entanto, é bom manter a interface amigável ao usuário.
### Posso usar o Aspose.Cells com outras linguagens de programação?  
Sim, o Aspose.Cells suporta múltiplas linguagens de programação, incluindo Java. Mas este tutorial foca especificamente em .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
