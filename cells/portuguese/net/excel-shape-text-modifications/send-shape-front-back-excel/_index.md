---
"description": "Descubra como enviar formas para a frente ou para trás no Excel usando o Aspose.Cells para .NET. Este guia oferece um tutorial passo a passo com dicas."
"linktitle": "Enviar forma para frente ou para trás no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Enviar forma para frente ou para trás no Excel"
"url": "/pt/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Enviar forma para frente ou para trás no Excel

## Introdução
Ao trabalhar com arquivos do Excel, você pode precisar de mais controle sobre os elementos visuais da sua planilha. Formas, como imagens e gráficos, podem aprimorar a apresentação dos seus dados. Mas o que acontece quando essas formas se sobrepõem ou precisam ser reordenadas? É aqui que o Aspose.Cells para .NET se destaca. Neste tutorial, mostraremos as etapas para manipular formas em uma planilha do Excel, especificamente enviando formas para a frente ou para trás de outras formas. Se você está pronto para aprimorar seu Excel, vamos começar!
## Pré-requisitos
Antes de começar, você precisa ter algumas coisas em mãos:
1. Instalação da Biblioteca Aspose.Cells: Certifique-se de ter a biblioteca Aspose.Cells instalada para .NET. Você pode encontrá-la [aqui](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento configurado com suporte ao .NET, como o Visual Studio.
3. Conhecimento básico de C#: a familiaridade com a programação em C# ajudará você a entender melhor os trechos de código.
Certo, você preencheu todos os pré-requisitos? Ótimo! Vamos para a parte divertida: escrever código!
## Pacotes de importação
Antes de mergulharmos na codificação propriamente dita, vamos importar os pacotes necessários. Basta adicionar a seguinte diretiva "using" no início do seu arquivo C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Esses namespaces são cruciais, pois contêm as classes e os métodos que usaremos para manipular arquivos e formas do Excel.
## Etapa 1: Defina os caminhos dos seus arquivos
Nesta primeira etapa, precisamos definir os diretórios de origem e saída. É aqui que o arquivo do Excel está localizado e onde você deseja salvar o arquivo modificado.
```csharp
//Diretório de origem
string sourceDir = "Your Document Directory";
//Diretório de saída
string outputDir = "Your Document Directory";
```
Substituir `"Your Document Directory"` com o caminho real onde seus arquivos do Excel estão armazenados.
## Etapa 2: Carregar a pasta de trabalho
Agora que definimos nossos diretórios, vamos carregar a pasta de trabalho (o arquivo do Excel) que contém as formas que queremos manipular.
```csharp
//Carregar arquivo Excel de origem
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Esta linha de código inicializa um novo `Workbook` objeto, carregando o arquivo Excel especificado na memória para que possamos trabalhar com ele.
## Etapa 3: Acesse a planilha 
Em seguida, precisamos acessar a planilha específica onde nossas formas estão. Para este exemplo, usaremos a primeira planilha.
```csharp
//Acesse a primeira planilha
Worksheet ws = wb.Worksheets[0];
```
Por referência `Worksheets[0]`, estamos focando na primeira planilha da nossa pasta de trabalho. Se suas formas estiverem em uma planilha diferente, ajuste o índice de acordo.
## Etapa 4: Acesse as Formas
Com o acesso à planilha pronto, vamos pegar as formas nas quais estamos interessados. Neste exemplo, acessaremos a primeira e a quarta formas.
```csharp
//Acesse a primeira e a quarta forma
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Essas linhas obtêm formas específicas da planilha com base em seu índice.
## Etapa 5: Imprimir a posição da ordem Z das formas
Antes de mover qualquer forma, vamos imprimir sua posição atual na Ordem Z. Isso nos ajuda a rastrear seu posicionamento antes de fazermos alterações.
```csharp
//Imprima a posição da forma na ordem Z
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Ligando `ZOrderPosition`, podemos ver onde cada forma se encaixa na ordem do desenho.
## Etapa 6: Envie a primeira forma para a frente
Agora é hora de agir! Vamos enviar a primeira forma para a frente da Ordem Z.
```csharp
//Enviar esta forma para a frente
sh1.ToFrontOrBack(2);
```
Passando `2` para `ToFrontOrBack`, estamos instruindo o Aspose.Cells a trazer essa forma para a frente. 
## Etapa 7: Imprima a posição da ordem Z da segunda forma
Antes de enviar a segunda forma para trás, vamos verificar onde ela está posicionada.
```csharp
//Imprima a posição da forma na ordem Z
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Isso nos dá uma ideia da posição da quarta forma antes de fazermos qualquer alteração.
## Etapa 8: Envie a quarta forma para trás
Por fim, enviaremos a quarta forma para o final da pilha da Ordem Z.
```csharp
//Enviar esta forma para trás
sh4.ToFrontOrBack(-2);
```
Usando `-2` pois o parâmetro envia a forma para o fundo da pilha, garantindo que ela não obstruirá outras formas ou texto.
## Etapa 9: Salve a pasta de trabalho 
O último passo é salvar sua pasta de trabalho com as formas recém-posicionadas.
```csharp
//Salvar o arquivo de saída do Excel
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Este comando salva a pasta de trabalho modificada no diretório de saída especificado.
## Etapa 10: Mensagem de confirmação
Por fim, vamos fornecer uma confirmação simples para nos informar que nossa tarefa foi concluída com sucesso.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
E isso conclui o código do nosso tutorial!
## Conclusão
Manipular formas no Excel usando o Aspose.Cells para .NET não é apenas simples, mas também poderoso. Seguindo este guia, você agora poderá enviar formas para a frente ou para trás com facilidade, permitindo melhor controle sobre suas apresentações do Excel. Com essas ferramentas à sua disposição, você está pronto para aprimorar o apelo visual de suas planilhas.
## Perguntas frequentes
### Qual linguagem de programação preciso para o Aspose.Cells?  
Você precisa usar C# ou qualquer linguagem compatível com .NET para trabalhar com Aspose.Cells.
### Posso testar o Aspose.Cells gratuitamente?  
Sim, você pode começar com um teste gratuito do Aspose.Cells [aqui](https://releases.aspose.com/).
### Que tipos de formas posso manipular no Excel?  
Você pode manipular várias formas, como retângulos, círculos, linhas e imagens.
### Como posso obter suporte para o Aspose.Cells?  
Você pode visitar o fórum da comunidade para obter suporte ou dúvidas [aqui](https://forum.aspose.com/c/cells/9).
### Existe uma licença temporária disponível para o Aspose.Cells?  
Sim, você pode solicitar uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}