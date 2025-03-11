---
title: Registrando e chamando função do Add-In no Excel
linktitle: Registrando e chamando função do Add-In no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Descubra como registrar e chamar funções de suplementos no Excel usando o Aspose.Cells para .NET com nosso tutorial passo a passo fácil.
weight: 20
url: /pt/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Registrando e chamando função do Add-In no Excel

## Introdução
Você quer melhorar sua experiência no Excel chamando funções de um add-in? Se sim, você está no lugar certo! Os add-ins do Excel são como as fadas madrinhas das planilhas; eles expandem magicamente a funcionalidade, dando a você um monte de novas ferramentas na ponta dos dedos. E com o Aspose.Cells para .NET, é mais fácil do que nunca registrar e usar essas funções de add-in. 
Neste guia, vou orientá-lo no processo de registrar e chamar uma função de um suplemento do Excel usando o Aspose.Cells para .NET. Vamos detalhar tudo passo a passo, para que você se sinta um profissional em pouco tempo!
## Pré-requisitos
Antes de mergulharmos na magia da codificação, vamos abordar o que você precisa ter em mãos:
1. Visual Studio: Certifique-se de ter o Visual Studio instalado em sua máquina. É aqui que escreveremos e executaremos nosso código.
2.  Biblioteca Aspose.Cells: Você precisará da biblioteca Aspose.Cells instalada. Você pode obtê-la de seu[página de download](https://releases.aspose.com/cells/net/).
3. Conhecimento básico de C#: Um pouco de conhecimento de C# será muito útil; ajudará você a acompanhar o processo sem problemas.
4.  Suplementos do Excel: Você deve ter um arquivo de suplemento (como`.xlam`) que contém as funções que você deseja registrar e usar.
5.  Um suplemento de exemplo do Excel: para este tutorial, usaremos um suplemento do Excel chamado`TESTUDF.xlam`. Então certifique-se de ter isso à sua disposição!
Agora que você está pronto, vamos arregaçar as mangas e começar a programar!
## Importando Pacotes
Para começar, você precisará importar alguns namespaces essenciais no topo do seu arquivo C#. Aqui está o que você precisa incluir:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Esses namespaces permitirão que você acesse as classes e métodos que usaremos neste tutorial.
Vamos dividir isso em etapas gerenciáveis. Ao final deste guia, você terá um entendimento sólido de como registrar funções de suplemento e usá-las em suas pastas de trabalho do Excel.
## Etapa 1: configure seus diretórios de origem e saída
Antes de registrar seu complemento, você precisa definir onde ele e os arquivos de saída ficarão.
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
// Diretório de saída
string outputDir = "Your Document Directory";
```
 Substituir`"Your Document Directory"` com o caminho real onde seu`.xlam` arquivo e os arquivos de saída serão salvos. Isso é como preparar o cenário antes do show começar.
## Etapa 2: Crie uma pasta de trabalho vazia
Em seguida, você vai querer criar uma pasta de trabalho em branco onde podemos brincar com funções de complemento.
```csharp
// Criar pasta de trabalho vazia
Workbook workbook = new Workbook();
```
Esta linha de código cria uma nova pasta de trabalho que servirá como nosso playground. Pense nela como uma tela nova, pronta para seus traços criativos.
## Etapa 3: Registre a função Add-In
Agora, vamos ao cerne da questão! É hora de registrar sua função add-in. Veja como fazer isso:
```csharp
// Registre o complemento habilitado para macro junto com o nome da função
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Esta linha registra a função de suplemento chamada`TEST_UDF` encontrado no`TESTUDF.xlam` arquivo add-in. O`false`parâmetro significa que o complemento não é carregado em um modo 'isolado'. 
## Etapa 4: Registre funções adicionais (se houver)
Se você tiver mais funções registradas no mesmo arquivo de complemento, você também pode registrá-las!
```csharp
// Registre mais funções no arquivo (se houver)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Aqui, você pode ver como é fácil adicionar mais funções do mesmo add-in. Basta continuar empilhando-as como blocos de construção!
## Etapa 5: Acesse a planilha
Vamos prosseguir e acessar a planilha onde usaremos nossa função. 
```csharp
// Acesse a primeira planilha
Worksheet worksheet = workbook.Worksheets[0];
```
Estamos acessando a primeira planilha na pasta de trabalho para colocar nossa fórmula. É como abrir a porta da sala onde a diversão acontece.
## Etapa 6: Acesse uma célula específica
Em seguida, precisamos escolher qual célula queremos usar para nossa fórmula. 
```csharp
// Acesse a primeira célula
var cell = worksheet.Cells["A1"];
```
Aqui estamos apontando para a célula A1. É aqui que vamos soltar nossa fórmula mágica. Você pode pensar nisso como fixar um alvo em seu mapa do tesouro!
## Etapa 7: Defina a fórmula
Agora é hora da grande revelação! Vamos definir a fórmula que chama nossa função registrada.
```csharp
// Definir nome da fórmula presente no suplemento
cell.Formula = "=TEST_UDF()";
```
Com esta linha, estamos dizendo ao Excel para usar nossa função dentro da célula A1. É como dar um comando ao Excel e dizer: “Ei, faça isso!”
## Etapa 8: Salve a pasta de trabalho
Por último, mas não menos importante, é hora de salvar nossa obra-prima.
```csharp
// Salvar a pasta de trabalho no formato de saída XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Aqui, estamos salvando nossa pasta de trabalho como um arquivo XLSX. Este passo final é como colocar sua pintura em uma moldura e se preparar para exibi-la!
## Etapa 9: Confirmar execução
Por fim, vamos finalizar tudo imprimindo uma mensagem de sucesso no console.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Esta linha atua como nossa bandeira da vitória. É um pequeno toque legal para confirmar que tudo correu bem.
## Conclusão 
aí está! Você não só aprendeu como registrar e chamar funções de suplementos do Excel usando o Aspose.Cells para .NET, mas também ganhou uma compreensão mais profunda de cada etapa envolvida. A vida está um pouco mais fácil agora, não é? Então por que não experimentar você mesmo? Mergulhe nesses suplementos do Excel e dê às suas planilhas um novo nível de interatividade e funcionalidade.
## Perguntas frequentes
### O que é um suplemento do Excel?  
Um suplemento do Excel é um programa que adiciona recursos, funções ou comandos personalizados ao Excel, permitindo que os usuários estendam seus recursos.
### Posso usar o Aspose.Cells sem instalá-lo localmente?  
Não, você precisa instalar a biblioteca Aspose.Cells para usá-la em seus aplicativos .NET.
### Como obtenho uma licença temporária para o Aspose.Cells?  
 Você pode visitar o site deles[página de licença temporária](https://purchase.aspose.com/temporary-license/) para maiores informações.
### É possível chamar várias funções de um único complemento?  
 Sim! Você pode registrar várias funções do mesmo arquivo de complemento usando o`RegisterAddInFunction` método.
### Onde posso encontrar mais documentação sobre o Aspose.Cells?  
 Você pode explorar a documentação abrangente no site[aqui](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
