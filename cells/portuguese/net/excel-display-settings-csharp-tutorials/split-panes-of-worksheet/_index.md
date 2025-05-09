---
"description": "Aprenda a dividir painéis de planilhas no Aspose.Cells para .NET com nosso guia passo a passo. Melhore a navegação em arquivos do Excel com este tutorial fácil."
"linktitle": "Dividir painéis da planilha"
"second_title": "Referência da API Aspose.Cells para .NET"
"title": "Dividir painéis da planilha"
"url": "/pt/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dividir painéis da planilha

## Introdução

Pronto para dividir os painéis de uma planilha do Excel usando o Aspose.Cells para .NET? Imagine a seguinte situação: você tem uma planilha gigante do Excel e está cansado de ficar rolando os cabeçalhos para lembrar em qual coluna está trabalhando. Eis que surge a "Dividir Painéis". Esse recurso prático permite congelar uma parte da planilha, facilitando muito a navegação. Seja trabalhando com dados financeiros, gerenciamento de estoque ou conjuntos de dados enormes, dividir painéis pode aumentar sua produtividade em dez vezes. 

## Pré-requisitos

Antes de começarmos a dividir os painéis como um assistente de planilha, vamos configurar corretamente. Aqui está o que você precisa:

- Aspose.Cells para .NET: Certifique-se de ter baixado e instalado. Se ainda não o fez, baixe-o [aqui](https://releases.aspose.com/cells/net/).
- .NET Framework: Este guia pressupõe que você esteja trabalhando em um ambiente .NET.
- Uma pasta de trabalho do Excel: usaremos um arquivo de exemplo do Excel para mostrar como esse recurso funciona.
- Uma licença temporária ou completa: Aspose.Cells requer uma licença. Se você está apenas experimentando, obtenha uma [licença temporária gratuita](https://purchase.aspose.com/temporary-license/) para evitar limitações de avaliação.

## Pacotes de importação

Antes de começarmos a trabalhar no código, vamos importar os namespaces necessários. Não é possível fazer nada em Aspose.Cells sem incluí-los.

```csharp
using System.IO;
using Aspose.Cells;
```

Agora que abordamos o essencial, vamos para a parte mais interessante: dividir os painéis!

## Etapa 1: Instanciar uma pasta de trabalho

O primeiro passo neste processo é criar uma `Workbook` objeto, que representará o arquivo do Excel que você deseja modificar. Neste caso, carregaremos um arquivo de um diretório. Esta é a sua tela, a planilha do Excel na qual você fará sua mágica.

Antes de podermos dividir painéis, precisamos de uma pasta de trabalho para trabalhar! Esta etapa é tão essencial quanto abrir um livro antes de começar a lê-lo.

```csharp
// O caminho para o diretório de documentos
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instanciar uma nova pasta de trabalho e abrir um arquivo de modelo
Workbook book = new Workbook(dataDir + "Book1.xls");
```

No código acima, substitua `"YOUR DOCUMENT DIRECTORY"` com o caminho real onde seu arquivo Excel está localizado. O `Workbook` a classe carrega o arquivo Excel na memória.

## Etapa 2: Defina a célula ativa

Após carregar a pasta de trabalho, é hora de definir a célula ativa. Em termos do Excel, a célula ativa é aquela que está selecionada ou em foco. Neste tutorial, selecionaremos a célula `A20` na primeira planilha.

Definir a célula ativa é crucial porque a divisão do painel começa a partir dela. É como escolher onde fazer o primeiro corte em uma pizza — escolha sua fatia!

```csharp
// Defina a célula ativa
book.Worksheets[0].ActiveCell = "A20";
```

Este pedaço de código faz `A20` a célula ativa. Isso é importante porque a divisão acontece em torno deste ponto, assim como a navegação no Excel costuma se concentrar em uma célula específica.

## Etapa 3: Divida a planilha

Agora que a célula ativa está definida, vamos para a parte divertida: dividir a planilha! É aqui que a mágica acontece. Você poderá dividir a planilha em vários painéis para facilitar a visualização e a navegação.

Este é o cerne de todo o tutorial. Ao dividir a planilha, você cria painéis separados que permitem navegar por diferentes seções da planilha do Excel sem perder de vista os cabeçalhos ou outras áreas importantes.

```csharp
// Dividir a janela da planilha
book.Worksheets[0].Split();
```

Com o `Split()` método, você está dizendo ao Aspose.Cells para dividir a planilha na célula ativa (`A20` neste caso). A partir deste ponto, o Excel cria uma divisão na planilha que separa os painéis para você navegar de forma independente.

## Etapa 4: Salve a pasta de trabalho

Após dividir os painéis, resta apenas salvar seu trabalho. Esta etapa final garantirá que suas alterações sejam salvas no arquivo de saída especificado.

De que adianta todo o seu trabalho duro se você não o salvar? Salvar garante que seus lindos painéis divididos permaneçam intactos para uso futuro.

```csharp
// Salvar o arquivo Excel
book.Save(dataDir + "output.xls");
```

Aqui, o `Save()` O método salva a pasta de trabalho com os painéis recém-divididos em um arquivo de saída do Excel. As alterações feitas agora estão prontas para você — ou qualquer outra pessoa — usar.

## Conclusão

E pronto! Você acabou de aprender a dividir painéis em uma planilha do Excel usando o Aspose.Cells para .NET. Chega de rolar a tela sem parar ou perder o controle dos seus dados. Este método torna o processamento de arquivos grandes do Excel muito menos trabalhoso e muito mais eficiente. Com a capacidade de dividir painéis, agora você pode acompanhar pontos de dados críticos enquanto trabalha com planilhas complexas.

## Perguntas frequentes

### Posso dividir mais de dois painéis?  
Sim, você pode dividir a planilha em vários painéis especificando diferentes células ativas e chamando o `Split()` método.

### Qual é a diferença entre dividir painéis e congelá-los?  
Dividir painéis permite rolar em ambos os painéis independentemente. Congelar painéis bloqueia os cabeçalhos ou linhas/colunas específicas para que permaneçam visíveis durante a rolagem.

### Posso remover a divisão depois de aplicá-la?  
Sim, você pode remover a divisão fechando e reabrindo a pasta de trabalho ou redefinindo-a programaticamente.

### A divisão de painéis funciona da mesma forma para diferentes formatos de arquivo do Excel (XLS, XLSX)?  
Sim, o `Split()` O método funciona para os formatos XLS e XLSX.

### Posso usar o Aspose.Cells sem uma licença?  
Sim, mas tem limitações. Para uma experiência completa, é melhor usar um [temporário](https://purchase.aspose.com/tempouary-license/) or [licença paga](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}