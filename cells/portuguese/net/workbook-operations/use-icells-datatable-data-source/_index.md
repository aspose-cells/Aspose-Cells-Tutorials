---
"description": "Aprenda a usar ICellsDataTableDataSource com Aspose.Cells para .NET para preencher planilhas do Excel dinamicamente. Perfeito para automatizar dados de clientes em pastas de trabalho."
"linktitle": "Use ICellsDataTableDataSource para o Designer de Pasta de Trabalho"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Use ICellsDataTableDataSource para o Designer de Pasta de Trabalho"
"url": "/pt/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Use ICellsDataTableDataSource para o Designer de Pasta de Trabalho

## Introdução
Criar planilhas avançadas com integração automatizada de dados pode ser uma grande mudança, especialmente em aplicações empresariais. Neste tutorial, vamos nos aprofundar em como usar `ICellsDataTableDataSource` para um designer de pasta de trabalho no Aspose.Cells para .NET. Vamos orientá-lo na criação de uma solução simples e legível para carregar dados personalizados em um arquivo Excel dinamicamente. Portanto, se você trabalha com listas de clientes, dados de vendas ou algo semelhante, este guia é para você!
## Pré-requisitos
Para começar, certifique-se de ter o seguinte:
- Biblioteca Aspose.Cells para .NET – Você pode baixá-la em [aqui](https://releases.aspose.com/cells/net/) ou obtenha uma versão de teste gratuita.
- Ambiente de desenvolvimento .NET – O Visual Studio é uma ótima escolha.
- Noções básicas de C# – Familiaridade com classes e tratamento de dados ajudará você a acompanhar.
Antes de prosseguir, certifique-se de que seu ambiente de desenvolvimento esteja configurado com os pacotes necessários.
## Pacotes de importação
Para usar o Aspose.Cells com eficiência, você precisa importar os pacotes essenciais. Abaixo, uma referência rápida para os namespaces necessários:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Etapa 1: definir uma classe de dados do cliente
Para começar, crie um simples `Customer` classe. Esta classe conterá detalhes básicos do cliente, como `FullName` e `Address`Pense nisso como uma maneira de definir o "formato" dos seus dados.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Etapa 2: Configurar a classe Lista de clientes
Em seguida, defina um `CustomerList` classe que se estende `ArrayList`. Esta lista personalizada conterá instâncias de `Customer` e permitir acesso indexado a cada entrada.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
Nesta etapa, estamos encapsulando nossos dados em um formato que o Aspose.Cells pode reconhecer e processar.
## Etapa 3: Criar a classe de fonte de dados do cliente
É aqui que as coisas ficam interessantes. Vamos criar um `CustomerDataSource` implementação de classe `ICellsDataTable` para tornar nossos dados compatíveis com o designer de pastas de trabalho do Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
Este costume `CustomerDataSource` A classe torna possível que Aspose.Cells interprete cada `Customer` objeto como uma linha no arquivo Excel.
## Etapa 4: Inicializar os dados do cliente
Agora, vamos adicionar alguns clientes à nossa lista. É aqui que carregamos os dados a serem gravados na pasta de trabalho. Sinta-se à vontade para adicionar mais entradas, se necessário.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Neste exemplo, estamos trabalhando com um pequeno conjunto de dados. No entanto, você pode facilmente expandir essa lista carregando dados de um banco de dados ou de outras fontes.
## Etapa 5: Carregar a pasta de trabalho
Agora, vamos abrir uma pasta de trabalho existente do Excel que contém os Marcadores Inteligentes necessários. Essa pasta de trabalho servirá como nosso modelo, e o Aspose.Cells substituirá dinamicamente os Marcadores Inteligentes pelos dados do cliente.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Garantir que `"SmartMarker1.xlsx"` contém marcadores de posição como `&=Customer.FullName` e `&=Customer.Address` onde os dados devem ser preenchidos.
## Etapa 6: Configurar o Designer de Pasta de Trabalho
Agora, vamos configurar o designer da pasta de trabalho para vincular nossa fonte de dados do cliente aos marcadores inteligentes da pasta de trabalho.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
O `SetDataSource` método vincula nosso `CustomerDataSource` aos marcadores inteligentes na pasta de trabalho. Cada marcador rotulado `&=Customer` no Excel agora serão substituídos pelos dados correspondentes do cliente.
## Etapa 7: Processar e salvar a pasta de trabalho
Por fim, vamos processar a pasta de trabalho para preencher os dados e salvar os resultados.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Este código aciona o processamento do Smart Marker, substitui todos os espaços reservados por dados e salva o resultado como `dest.xlsx`.
## Conclusão
Parabéns! Você implementou com sucesso `ICellsDataTableDataSource` Para um designer de pasta de trabalho que usa Aspose.Cells para .NET. Essa abordagem é ideal para automatizar o preenchimento de dados em planilhas, especialmente ao lidar com dados dinâmicos, como listas de clientes ou estoques de produtos. Com essas habilidades, você está no caminho certo para criar aplicativos baseados em dados que facilitam a geração de relatórios baseados em Excel!
## Perguntas frequentes
### O que é `ICellsDataTable` em Aspose.Cells?  
É uma interface que permite que fontes de dados personalizadas sejam vinculadas aos marcadores inteligentes do Aspose.Cells para preenchimento dinâmico de dados.
### Como posso personalizar dados no modelo de pasta de trabalho?  
Espaços reservados chamados marcadores inteligentes, como `&=Customer.FullName`, são utilizados. Esses marcadores são substituídos por dados reais durante o processamento.
### O Aspose.Cells para .NET é gratuito?  
Aspose.Cells oferece um teste gratuito, mas o acesso completo requer uma licença paga. Confira [teste gratuito](https://releases.aspose.com/) ou [comprar](https://purchase.aspose.com/buy) opções.
### Posso adicionar mais dados de clientes dinamicamente?  
Com certeza! Basta preencher o `CustomerList` com entradas adicionais antes de executar o programa.
### Onde posso obter ajuda se estiver preso?  
Aspose tem um [fórum de suporte](https://forum.aspose.com/c/cells/9) onde os usuários podem fazer perguntas e obter assistência da comunidade e da equipe do Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}