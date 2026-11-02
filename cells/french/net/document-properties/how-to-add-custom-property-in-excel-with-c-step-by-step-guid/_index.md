---
category: general
date: 2026-02-28
description: Apprenez à ajouter une propriété personnalisée à un classeur Excel en
  C# et à écrire rapidement la sortie console. Inclut le chargement d’un classeur
  Excel en C# et l’accès aux propriétés personnalisées en C#.
draft: false
keywords:
- how to add custom property
- load excel workbook c#
- write console output c#
- access custom properties c#
- get first worksheet c#
language: fr
og_description: Comment ajouter une propriété personnalisée dans Excel avec C# expliqué
  en détail. Charger le classeur, accéder aux propriétés personnalisées et afficher
  la sortie console.
og_title: Comment ajouter une propriété personnalisée dans Excel avec C# – Guide complet
tags:
- C#
- Excel
- Aspose.Cells
- CustomProperties
title: Comment ajouter une propriété personnalisée dans Excel avec C# – Guide étape
  par étape
url: /fr/net/document-properties/how-to-add-custom-property-in-excel-with-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter une propriété personnalisée dans Excel avec C# – Guide étape par étape

Vous vous êtes déjà demandé **comment ajouter une propriété personnalisée** à un fichier Excel en utilisant C# ? Dans ce tutoriel, nous allons parcourir le chargement d’un classeur Excel, l’accès aux propriétés personnalisées et l’affichage du résultat dans la console. C’est un scénario assez courant lorsque vous devez étiqueter une feuille avec des métadonnées comme « Department » ou « Budget » sans modifier les données visibles.

Ce que vous obtiendrez de ce guide, c’est une solution complète, prête à copier‑coller, qui vous montre comment **load excel workbook c#**, récupérer la **first worksheet c#**, ajouter et lire les **custom properties c#**, et enfin **write console output c#**. Aucun renvoi vague à des documents externes — tout ce dont vous avez besoin se trouve ici, ainsi que quelques astuces de pro pour éviter les pièges habituels.

---

## Prérequis

- **.NET 6.0** ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+).  
- **Aspose.Cells for .NET** (version d’essai gratuite ou version sous licence). Si vous préférez une alternative open‑source, EPPlus fonctionne de manière similaire ; il suffit d’échanger le namespace et les noms de classe.  
- Un environnement de développement C# de base (Visual Studio, VS Code, Rider — tout convient).  
- Un fichier Excel nommé `input.xlsx` placé dans un dossier que vous pouvez référencer, par exemple `C:\Data\input.xlsx`.

> **Astuce pro :** Lorsque vous installez Aspose.Cells via NuGet, le package ajoute automatiquement la directive `using Aspose.Cells;` nécessaire, vous n’aurez donc pas à rechercher manuellement les DLL.

## Étape 1 – Charger le classeur Excel C# (Point de départ)

Avant de pouvoir manipuler les propriétés personnalisées, vous avez besoin de l’objet classeur en mémoire.

```csharp
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

// Define the path to your Excel file
string workbookPath = @"C:\Data\input.xlsx";

// Load the workbook – this is the classic way to load excel workbook c#
Workbook wb = new Workbook(workbookPath);
```

**Pourquoi c’est important :** Charger le classeur crée une instance `Workbook` complète qui vous donne accès aux feuilles de calcul, aux cellules et à la collection cachée `CustomProperties`. Ignorer cette étape ou utiliser un chemin incorrect déclenchera une `FileNotFoundException`, c’est pourquoi nous définissons explicitement le chemin dès le départ.

## Étape 2 – Obtenir la première feuille de calcul C# (Là où la magie opère)

La plupart des classeurs ont une feuille par défaut avec laquelle vous voulez travailler. Aspose.Cells stocke les feuilles de calcul dans une collection indexée à partir de zéro, donc la première a l’indice `0`.

```csharp
// Retrieve the first worksheet – get first worksheet c# is as simple as this
Worksheet worksheet = wb.Worksheets[0];
```

**Quel est l’avantage ?** En ciblant directement la première feuille, vous évitez de parcourir la collection alors que vous n’avez besoin que d’une seule feuille. Si votre fichier possède plusieurs feuilles et que vous avez besoin d’une autre, il suffit de changer l’indice ou d’utiliser `Worksheets["SheetName"]`.

## Étape 3 – Ajouter une propriété personnalisée (Le cœur de la façon d’ajouter une propriété personnalisée)

Nous répondons enfin à la question principale : **comment ajouter une propriété personnalisée** à une feuille de calcul.

```csharp
// Add a custom property named "Department" with value "Finance"
worksheet.CustomProperties.Add("Department", "Finance");

// Add a numeric custom property named "Budget" with value 1,250,000
worksheet.CustomProperties.Add("Budget", 1250000);
```

### En coulisses

- `CustomProperties` est une collection qui appartient à l’objet `Worksheet`, pas au classeur.  
- La méthode `Add` accepte une clé de type chaîne et une valeur d’objet, vous pouvez donc stocker du texte, des nombres, des dates ou même des indicateurs booléens.  
- Aspose.Cells persiste automatiquement ces propriétés dans le fichier Excel sous‑jacent lorsque vous l’enregistrez plus tard.

> **Attention :** Si vous essayez d’ajouter une propriété avec un nom déjà existant, Aspose déclenchera une `ArgumentException`. Pour mettre à jour une propriété existante, utilisez `worksheet.CustomProperties["Budget"].Value = newValue;`.

## Étape 4 – Récupérer et utiliser la propriété personnalisée (Access Custom Properties C#)

Lire une propriété est tout aussi simple que de l’écrire. Cette étape montre **access custom properties c#** et indique également comment **write console output c#**.

```csharp
// Retrieve the "Budget" value from the custom properties collection
var budget = worksheet.CustomProperties["Budget"].Value;

// Optional: Cast to the expected type if you need numeric operations
decimal budgetAmount = Convert.ToDecimal(budget);
```

**Pourquoi caster ?** La propriété `Value` renvoie un `object`. La convertir en type numérique vous permet d’effectuer des calculs — par exemple, ajouter la TVA ou comparer les budgets — sans surcharge supplémentaire de boxing/unboxing.

## Étape 5 – Écrire la sortie console C# (Voir le résultat)

Enfin, nous affichons le budget récupéré dans la console. Cela satisfait l’exigence **write console output c#**.

```csharp
// Display the budget amount in the console
Console.WriteLine($"Budget: {budgetAmount:C0}");
```

Le spécificateur de format `:C0` affiche le nombre en devise sans décimales, par ex., `Budget: $1,250,000`. N’hésitez pas à ajuster la chaîne de format pour correspondre à votre paramètre régional.

## Étape 6 – Enregistrer le classeur (Persistance des modifications)

Si vous souhaitez que les propriétés personnalisées persistent au‑delà de la session actuelle, vous devez enregistrer le classeur.

```csharp
// Save the workbook to a new file so you don't overwrite the original
string outputPath = @"C:\Data\output_with_properties.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

**Note :** Bien que les propriétés personnalisées soient attachées à la feuille de calcul, elles sont stockées à l’intérieur du package `.xlsx`, de sorte que la taille du fichier n’augmente que marginalement.

## Exemple complet fonctionnel (Prêt à copier‑coller)

Ci‑dessous se trouve le programme complet qui regroupe toutes les étapes. Collez‑le dans un nouveau projet console et appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook – how to add custom property starts here
            string workbookPath = @"C:\Data\input.xlsx";
            Workbook wb = new Workbook(workbookPath);

            // 2️⃣ Get the first worksheet – get first worksheet c#
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Add custom properties – this is the core of how to add custom property
            worksheet.CustomProperties.Add("Department", "Finance");
            worksheet.CustomProperties.Add("Budget", 1250000);

            // 4️⃣ Retrieve the budget – access custom properties c#
            var budget = worksheet.CustomProperties["Budget"].Value;
            decimal budgetAmount = Convert.ToDecimal(budget);

            // 5️⃣ Write console output – write console output c#
            Console.WriteLine($"Budget: {budgetAmount:C0}");

            // 6️⃣ Save the workbook so the properties persist
            string outputPath = @"C:\Data\output_with_properties.xlsx";
            wb.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");

            // Keep console window open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Sortie console attendue**

```
Budget: $1,250,000
Workbook saved to C:\Data\output_with_properties.xlsx
Press any key to exit...
```

Exécutez le programme, ouvrez `output_with_properties.xlsx` dans Excel, puis allez dans **File → Info → Properties → Advanced Properties → Custom**. Vous verrez « Department » = « Finance » et « Budget » = 1250000 listés là.

## Questions fréquentes & cas limites

### Que faire si le classeur est protégé par mot de passe ?

Aspose.Cells vous permet d’ouvrir un fichier protégé en passant un objet `LoadOptions` contenant le mot de passe :

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx) { Password = "mySecret" };
Workbook wb = new Workbook(workbookPath, loadOptions);
```

### Puis‑je ajouter des propriétés personnalisées au classeur lui‑même au lieu d’une seule feuille ?

Oui — utilisez `wb.CustomProperties` au lieu de `worksheet.CustomProperties`. L’API est identique, mais la portée passe de par‑feuille à l’ensemble du fichier.

### Cela fonctionne‑t‑il avec les fichiers .xls (Excel 97‑2003) ?

Absolument. Aspose.Cells abstrait le format, de sorte que le même code fonctionne avec les fichiers `.xls`, `.xlsx`, `.xlsm`, etc. Assurez‑vous simplement que l’extension du fichier correspond au format réel.

### Comment supprimer une propriété personnalisée ?

```csharp
worksheet.CustomProperties.Remove("Department");
```

Supprimer une propriété est sûr ; si la clé n’existe pas, rien ne se passe.

## Astuces pro & pièges

- **Évitez de coder en dur les chemins** dans le code de production. Utilisez `Path.Combine` et des fichiers de configuration pour garder de la flexibilité.  
- **Libérez le classeur** si vous traitez de nombreux fichiers dans une boucle. Encapsulez‑le dans un bloc `using` ou appelez `wb.Dispose()` manuellement.  
- **Attention aux formats numériques spécifiques à la culture** lors de la conversion de la valeur `object`. `Convert.ToDecimal` respecte la culture du thread actuel, donc définissez `CultureInfo.InvariantCulture` si vous avez besoin d’une analyse cohérente.  
- **Ajoutez les propriétés par lots** : si vous avez des dizaines d’éléments de métadonnées, envisagez de parcourir un dictionnaire pour garder le code DRY.

## Conclusion

Nous venons de couvrir **comment ajouter une propriété personnalisée** à une feuille Excel en utilisant C#. Du chargement du classeur, à l’obtention de la première feuille, en passant par l’ajout et la lecture des propriétés personnalisées, jusqu’à l’écriture du résultat dans la console et la persistance du fichier — vous disposez maintenant d’une solution complète, prête à copier.

Ensuite, vous pourriez explorer **access custom properties c#** au niveau du classeur, ou expérimenter avec des types de données plus complexes comme les dates et les booléens. Si vous êtes curieux d’automatiser la génération de rapports, consultez notre guide sur **write console output c#** pour la journalisation de grands ensembles de données, ou plongez dans la série **load excel workbook c#** pour une manipulation avancée des feuilles.

N’hésitez pas à ajuster les noms des propriétés, ajouter vos propres métadonnées, et intégrer ce modèle dans des pipelines de traitement de données plus importants. Bon codage, et que vos feuilles de calcul restent richement annotées !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}