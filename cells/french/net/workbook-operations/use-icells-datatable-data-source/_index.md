---
title: Utiliser ICellsDataTableDataSource pour Workbook Designer
linktitle: Utiliser ICellsDataTableDataSource pour Workbook Designer
second_title: API de traitement Excel Aspose.Cells .NET
description: Apprenez à utiliser ICellsDataTableDataSource avec Aspose.Cells pour .NET pour remplir dynamiquement des feuilles Excel. Idéal pour automatiser les données client dans les classeurs.
weight: 21
url: /fr/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utiliser ICellsDataTableDataSource pour Workbook Designer

## Introduction
 La création de feuilles de calcul avancées avec intégration automatisée des données peut changer la donne, en particulier dans les applications professionnelles. Dans ce tutoriel, nous verrons comment utiliser`ICellsDataTableDataSource`pour un concepteur de classeur dans Aspose.Cells pour .NET. Nous vous guiderons dans la création d'une solution simple et lisible par l'homme pour charger des données personnalisées dans un fichier Excel de manière dynamique. Donc, si vous travaillez avec des listes de clients, des données de vente ou tout autre élément similaire, ce guide est fait pour vous !
## Prérequis
Pour commencer, assurez-vous de disposer des éléments suivants :
-  Bibliothèque Aspose.Cells pour .NET – Vous pouvez la télécharger à partir de[ici](https://releases.aspose.com/cells/net/) ou obtenez une version d'essai gratuite.
- Environnement de développement .NET – Visual Studio est un excellent choix.
- Compréhension de base de C# – La familiarité avec les classes et la gestion des données vous aidera à suivre.
Avant de continuer, assurez-vous que votre environnement de développement est configuré avec les packages nécessaires.
## Paquets d'importation
Pour utiliser efficacement Aspose.Cells, vous devez importer les packages essentiels. Vous trouverez ci-dessous une référence rapide pour les espaces de noms requis :
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Étape 1 : définir une classe de données client
 Pour commencer, créez un simple`Customer` classe. Cette classe contiendra des informations de base sur les clients, telles que`FullName` et`Address`Considérez-le comme un moyen de définir la « forme » de vos données.
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
## Étape 2 : Configurer la classe de liste de clients
 Ensuite, définissez un`CustomerList` classe qui étend`ArrayList` . Cette liste personnalisée contiendra des instances de`Customer` et permettre un accès indexé à chaque entrée.
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
Dans cette étape, nous enveloppons nos données dans un format qu'Aspose.Cells peut reconnaître et traiter.
## Étape 3 : créer la classe source de données client
 C'est là que les choses deviennent intéressantes. Nous allons créer un`CustomerDataSource` classe implémentant`ICellsDataTable` pour rendre nos données compatibles avec le concepteur de classeur Aspose.Cells.
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
 Cette coutume`CustomerDataSource` classe permet à Aspose.Cells d'interpréter chaque`Customer` objet sous forme de ligne dans le fichier Excel.
## Étape 4 : Initialiser les données client
Ajoutons maintenant quelques clients à notre liste. C'est ici que nous chargeons les données à écrire dans le classeur. N'hésitez pas à ajouter d'autres entrées si nécessaire.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Dans cet exemple, nous travaillons avec un petit ensemble de données. Cependant, vous pouvez facilement étendre cette liste en chargeant des données à partir d'une base de données ou d'autres sources.
## Étape 5 : Charger le classeur
Ouvrons maintenant un classeur Excel existant contenant les marqueurs intelligents nécessaires. Ce classeur servira de modèle et Aspose.Cells remplacera dynamiquement les marqueurs intelligents par les données client.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Assurez-vous que`"SmartMarker1.xlsx"` contient des espaces réservés comme`&=Customer.FullName` et`&=Customer.Address` où les données doivent être renseignées.
## Étape 6 : Configurer le concepteur de classeurs
Maintenant, configurons le concepteur de classeur pour lier notre source de données client aux marqueurs intelligents du classeur.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 Le`SetDataSource` méthode lie notre`CustomerDataSource` aux marqueurs intelligents du classeur. Chaque marqueur est étiqueté`&=Customer` dans Excel sera désormais remplacé par les données client correspondantes.
## Étape 7 : Traiter et enregistrer le classeur
Enfin, traitons le classeur pour remplir les données et enregistrer les résultats.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Ce code déclenche le traitement du marqueur intelligent, remplace tous les espaces réservés par des données et enregistre le résultat sous`dest.xlsx`.
## Conclusion
 Félicitations ! Vous avez implémenté avec succès`ICellsDataTableDataSource` pour un concepteur de classeur utilisant Aspose.Cells pour .NET. Cette approche est idéale pour automatiser le remplissage des données dans les feuilles de calcul, en particulier lorsqu'il s'agit de données dynamiques telles que des listes de clients ou des inventaires de produits. Grâce à ces compétences, vous êtes sur la bonne voie pour créer des applications pilotées par les données qui simplifient la création de rapports basés sur Excel !
## FAQ
###  Qu'est-ce que`ICellsDataTable` in Aspose.Cells?  
Il s'agit d'une interface permettant de lier des sources de données personnalisées aux marqueurs intelligents Aspose.Cells pour un remplissage de données dynamique.
### Comment puis-je personnaliser les données dans le modèle de classeur ?  
 Espaces réservés appelés marqueurs intelligents, tels que`&=Customer.FullName`, sont utilisés. Ces marqueurs sont remplacés par des données réelles lors du traitement.
### Aspose.Cells pour .NET est-il gratuit ?  
 Aspose.Cells propose un essai gratuit, mais l'accès complet nécessite une licence payante. Vérifiez leur[essai gratuit](https://releases.aspose.com/) ou[acheter](https://purchase.aspose.com/buy) options.
### Puis-je ajouter davantage de données client de manière dynamique ?  
 Absolument ! Il suffit de remplir le`CustomerList`avec des entrées supplémentaires avant d'exécuter le programme.
### Où puis-je obtenir de l’aide si je suis bloqué ?  
 Aspose a un[Forum de soutien](https://forum.aspose.com/c/cells/9) où les utilisateurs peuvent poser des questions et obtenir de l'aide de la communauté et de l'équipe Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
