---
category: general
date: 2026-03-22
description: Comment générer un rapport Excel en C# avec un modèle maître‑détail.
  Apprenez à remplir rapidement un modèle Excel en C# en utilisant SmartMarker pour
  des feuilles répétables.
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: fr
og_description: Comment générer un rapport Excel en C# à l'aide d'un modèle réutilisable.
  Ce guide étape par étape vous montre comment remplir un modèle Excel en C# avec
  des données maître‑détail.
og_title: Comment générer un rapport Excel en C# – Tutoriel complet sur SmartMarker
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: Comment générer un rapport Excel en C# – Guide complet avec SmartMarker
url: /fr/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment générer un rapport Excel en C# – Guide complet avec SmartMarker

Vous vous êtes déjà demandé **comment générer un rapport Excel** en C# sans écrire du code cellule par cellule à l’infini ? Vous n’êtes pas seul. La plupart des développeurs se heurtent à un mur lorsqu’ils ont besoin d’un rapport poli, multi‑feuilles, reflétant des relations maître‑détail—pensez aux commandes et aux lignes de commande—sans vouloir réinventer la roue à chaque fois.

Bonne nouvelle ? Avec un modèle Excel prêt à l’emploi et le moteur **SmartMarker** d’Aspose.Cells, vous pouvez **populate Excel template C#** en quelques lignes seulement. Dans ce tutoriel, nous parcourrons un scénario réel, expliquerons pourquoi chaque étape est importante, et vous fournirons un exemple complet et exécutable que vous pouvez copier‑coller dès aujourd’hui.

> **Ce que vous obtiendrez :** un rapport Excel maître‑détail où chaque commande génère sa propre feuille de calcul, le tout piloté par de simples objets C#. Aucun bouclage manuel sur les cellules, aucune formule fragile—juste du code propre et maintenable.

---

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **.NET 6.0** (ou supérieur) installé – le code cible .NET 6 mais fonctionne également avec .NET Framework 4.7+.
- **Aspose.Cells for .NET** package NuGet (`Install-Package Aspose.Cells`) – il fournit les classes `Workbook`, `SmartMarkerProcessor` et les classes associées.
- Un fichier Excel nommé **MasterDetailTemplate.xlsx** placé dans `YOUR_DIRECTORY`. Il doit contenir un bloc SmartMarker tel que `{{Orders.OrderId}}` dans la première feuille et un bloc imbriqué `{{Orders.Items.Prod}}` pour les lignes de détail.
- Une compréhension de base des types anonymes C# – nous les utiliserons pour modéliser les commandes et les articles.

Si l’un de ces points vous semble inconnu, pas d’inquiétude. Nous mentionnerons des alternatives (par ex., EPPlus) plus loin, mais le concept central reste le même.

---

## Étape 1 : Charger le modèle Excel contenant les blocs SmartMarker

La première chose que nous faisons est d’ouvrir le fichier modèle. Pensez au modèle comme à un squelette ; SmartMarker le remplira ensuite avec les données réelles.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Pourquoi c’est important :** En séparant la mise en page (le modèle) des données (les objets C#), vous gardez les designers heureux et les développeurs satisfaits. Les designers peuvent ajuster polices, couleurs ou formules sans toucher au code.

---

## Étape 2 : Construire la source de données maître‑détail

Ensuite, nous créons les données qui alimenteront le modèle. Pour un rapport de commandes typique, vous avez une collection de commandes, chacune contenant sa propre collection d’articles.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **Astuce :** Utilisez des classes fortement typées au lieu de types anonymes si vous devez réutiliser le modèle sur plusieurs rapports. L’approche anonyme garde l’exemple concis.

**Pourquoi c’est important :** SmartMarker fonctionne en faisant correspondre les noms de propriétés (`Orders`, `OrderId`, `Items`, `Prod`, `Qty`) avec les espaces réservés du modèle. La hiérarchie doit correspondre exactement, sinon le moteur ignorera ces sections.

---

## Étape 3 : Dire à SmartMarker de créer une nouvelle feuille pour chaque enregistrement maître

Par défaut, SmartMarker écrit toutes les lignes dans une seule feuille. Nous voulons chaque commande sur sa propre feuille de calcul, ce qui est idéal pour l’impression ou l’envoi de PDF par commande plus tard.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**Pourquoi c’est important :** `EnableRepeatingSheet` élimine le besoin de cloner manuellement les feuilles. Le moteur copie la feuille d’origine, injecte les données de la commande, et renomme la feuille automatiquement (généralement en utilisant la valeur de la première colonne).

---

## Étape 4 : Traiter le modèle avec vos données

Maintenant, nous relions le tout. Le `SmartMarkerProcessor` parcourt le classeur, remplace les balises et crée de nouvelles feuilles selon les instructions.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**Pourquoi c’est important :** Cette ligne unique fait le gros du travail—analyse du modèle, itération sur les collections, et gestion des tables imbriquées. C’est le cœur du **populate Excel template C#** sans aucune boucle manuelle.

---

## Étape 5 : Enregistrer le rapport final

Enfin, écrivez le classeur rempli sur le disque. Vous pouvez également le diffuser directement dans une réponse HTTP pour les applications web.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**Pourquoi c’est important :** Sauvegarder dans un fichier vous donne un artefact tangible que vous pouvez ouvrir dans Excel, partager avec les parties prenantes, ou acheminer vers des processus en aval comme la conversion PDF.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, incluant les directives `using` et une méthode `Main`. Déposez‑le dans une application console, ajustez les chemins de fichiers, et exécutez.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `MasterDetailResult.xlsx`, vous verrez :

- **Feuille “Order_1”** – contient l’en‑tête de la Commande 1 et deux lignes pour les produits A et B.
- **Feuille “Order_2”** – contient l’en‑tête de la Commande 2 et une seule ligne pour le produit C.
- Toutes les formules, le formatage et les graphiques du modèle original sont conservés.

![Rapport Excel avec des feuilles séparées pour chaque commande – exemple de classeur rempli](/images/excel-report-example.png "Rapport Excel généré avec des données maître‑détail")

*Texte alternatif de l’image : rapport Excel généré avec des feuilles séparées pour chaque commande, montrant comment générer un rapport Excel en C# avec SmartMarker.*

---

## Questions fréquentes & cas particuliers

### Et si j’ai besoin d’une feuille statique (par ex., un résumé) en plus des feuilles répétées ?

Définissez `EnableRepeatingSheet = true` **uniquement** sur la feuille qui contient le bloc maître. Les autres feuilles resteront intactes, vous pouvez donc garder une page de résumé dans le modèle d’origine.

### Puis‑je utiliser un DataTable au lieu d’objets anonymes ?

Absolument. SmartMarker fonctionne avec tout objet implémentant `IEnumerable`. Remplacez simplement le type anonyme par un `DataTable` et assurez‑vous que les noms de colonnes correspondent aux balises.

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### Comment modifier la convention de nommage des feuilles générées ?

Implémentez une interface personnalisée `ISmartMarkerSheetNaming` (ou manipulez `workbook.Worksheets` après le traitement). La plupart des développeurs renomme simplement les feuilles en fonction d’une valeur de cellule :

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### Et si mon modèle utilise une syntaxe de placeholder différente ?

SmartMarker autorise des délimiteurs personnalisés via `SmartMarkerOptions`. Par exemple, pour utiliser `<< >>` au lieu de `{{ }}` :

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

---

## Conseils pour faire évoluer cette approche

- **Mettez en cache le modèle** en mémoire si vous générez de nombreux rapports par requête ; le chargement depuis le disque à chaque fois ajoute de la latence.
- **Combinez avec la conversion PDF** (`workbook.Save("report.pdf", SaveFormat.Pdf)`) pour des sorties prêtes à l’envoi par e‑mail.
- **Paramétrez les chemins de fichiers** à l’aide de fichiers de configuration ou de variables d’environnement afin de rendre la solution portable entre dev, test et prod.
- **Testez unitaires la couche de données** séparément ; SmartMarker est déterministe, vous n’avez donc besoin que de vérifier que les données fournies correspondent au schéma attendu.

---

## Conclusion

Nous avons couvert **comment générer un rapport Excel** en C# de bout en bout, du chargement d’un modèle compatible SmartMarker à l’enregistrement d’un classeur multi‑feuilles reflétant des relations maître‑détail. En **populate Excel template C#** avec seulement quelques lignes de code, vous évitez la logique fragile cellule par cellule et offrez aux designers la liberté de façonner le rendu final.

Ensuite, vous pourriez explorer :

- Utiliser **populate Excel template C#** avec des graphiques qui se mettent à jour automatiquement par feuille.
- Intégrer **excel smartmarker c#** avec ASP.NET Core pour diffuser les rapports directement aux navigateurs.
- Automatiser des pipelines **c# excel automation** qui récupèrent les données depuis des API ou des bases de données.

Essayez, ajustez le modèle, et voyez à quel point il est rapide de transformer des données brutes en un rapport Excel soigné. Des questions ou un cas d’usage intéressant ? Laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}