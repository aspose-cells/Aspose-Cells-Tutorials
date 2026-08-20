---
category: general
date: 2026-02-14
description: Créez rapidement un modèle de remise et apprenez comment appliquer une
  remise dans une feuille de calcul, injecter des données dans le modèle et définir
  un préfixe variable pour les marqueurs intelligents.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: fr
og_description: Créer un modèle de remise avec C#. Apprenez à appliquer une remise
  dans une feuille de calcul, à injecter des données dans le modèle et à définir un
  préfixe variable pour les marqueurs intelligents.
og_title: Créer un modèle de remise – Tutoriel complet C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Créer un modèle de remise en C# – Guide étape par étape
url: /fr/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un modèle de remise – Guide complet en C#

Vous avez déjà eu besoin de **créer un modèle de remise** pour un rapport de ventes mais vous ne saviez pas comment alimenter automatiquement les chiffres dans une feuille de calcul ? Vous n'êtes pas seul. Dans ce tutoriel, nous vous montrerons exactement comment **créer un modèle de remise**, puis **appliquer la remise dans les cellules de la feuille de calcul**, **injecter des données dans le modèle**, et même **définir le préfixe de variable** pour vos smart markers—le tout avec du code C# propre.

Nous commencerons par exposer le problème, puis nous passerons directement à une solution fonctionnelle que vous pouvez copier‑coller. À la fin, vous disposerez d’un modèle réutilisable qui fonctionne que vous génériez des factures, des listes de prix ou toute feuille de calcul nécessitant des remises dynamiques.

---

## Ce que vous allez apprendre

- Comment concevoir un modèle de feuille de calcul prenant en charge les remises.  
- Comment configurer un `VariablePrefix` / `VariableSuffix` personnalisé afin que les marqueurs soient faciles à repérer.  
- Comment passer un objet anonyme (`discountData`) au `SmartMarkerProcessor`.  
- Comment la formule résultante (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) calcule automatiquement le prix final.  
- Conseils pour gérer les cas limites comme les lignes sans remise ou les niveaux de remise multiples.  

**Prérequis** – un runtime .NET récent (≥ .NET 6), une référence à la bibliothèque `Aspose.Cells` (ou similaire) qui fournit `SmartMarkerProcessor`, et une compréhension de base de la syntaxe C#. Rien d'exotique.

---

## Étape 1 : Créer un modèle de remise dans votre feuille de calcul

Tout d’abord, ouvrez un nouveau classeur (ou utilisez-en un existant) et placez un espace réservé à l’endroit où la remise sera appliquée. Considérez le modèle comme un simple fichier Excel contenant des “smart markers” que le processeur remplacera.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Pourquoi c’est important :** En intégrant `#Discount#` dans la formule, nous indiquons au processeur exactement où la valeur de remise doit être insérée. Le `SmartMarkerProcessor` remplacera `#Discount#` par le nombre que vous fournirez plus tard, en laissant le reste de la formule intact.

---

## Étape 2 : Définir le préfixe de variable pour les Smart Markers

Par défaut, de nombreuses bibliothèques recherchent `${Variable}` ou `{{Variable}}`. Dans notre cas, nous voulons un marqueur propre et lisible, nous **définissons donc explicitement le préfixe et le suffixe de variable**.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Astuce :** Utiliser `#` garde les marqueurs courts et faciles à repérer dans la barre de formule d’Excel. Si vous devez éviter les conflits avec des fonctions Excel existantes, choisissez une paire différente (par ex., `[[` et `]]`).

---

## Étape 3 : Injecter des données dans le modèle avec SmartMarkerProcessor

Nous allons maintenant fournir la valeur réelle de la remise. Le processeur parcourra la feuille, trouvera chaque `#Discount#` et le remplacera par la valeur de l’objet anonyme que nous transmettons.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Après cet appel, la formule en `B2` devient :

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Lorsque le classeur calcule, `B2` affiche **90**, c’est‑à‑dire une remise de 10 % appliquée au prix d’origine de 100.

**Pourquoi cela fonctionne :** `StartSmartMarkerProcessing` parcourt chaque cellule, recherche le jeton `#Discount#` et le substitue par la valeur numérique. Comme le jeton se trouve à l’intérieur d’une instruction `IF`, la feuille de calcul gère toujours les cas où la remise pourrait être nulle.

---

## Étape 4 : Appliquer la remise dans la feuille de calcul – Vérifier le résultat

Déclenchons le calcul et affichons le prix final dans la console. Cette étape prouve que le workflow **appliquer la remise dans la feuille de calcul** a réussi.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Sortie attendue**

```
Original: 100
Discounted (10%): 90
```

Si vous changez `discountData.Discount` à `0.25` et relancez le processeur, la sortie reflétera automatiquement une remise de 25 %—aucun code supplémentaire n’est nécessaire.

---

## Étape 5 : Gestion des cas limites et des remises multiples

### Lignes sans remise

Parfois un produit n’est pas en promotion. Pour que la formule reste robuste, le `IF` que vous avez placé précédemment couvre déjà ce scénario : lorsque `#Discount#` vaut `0`, le prix d’origine passe inchangé.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Colonnes de remise multiples

Si vous avez besoin de remises distinctes par ligne, attribuez à chaque ligne son propre marqueur, par ex., `#Discount1#`, `#Discount2#`, et transmettez une collection :

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Le processeur associe les marqueurs séquentiellement, de sorte que chaque ligne reçoit la bonne valeur.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à être copié, qui intègre toutes les étapes ci‑dessus. Enregistrez‑le sous le nom `Program.cs`, ajoutez une référence à `Aspose.Cells`, puis exécutez‑le.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

L’exécution affiche les nombres attendus et génère un fichier `DiscountedPricing.xlsx` que vous pouvez ouvrir dans Excel pour voir la formule déjà résolue.

---

## Conclusion

Vous savez maintenant comment **créer un modèle de remise**, **appliquer la remise dans la feuille de calcul**, **injecter des données dans le modèle**, et **définir le préfixe de variable** pour les smart markers—le tout avec quelques lignes concises de C#. Le modèle est extensible : il suffit de modifier l’objet anonyme ou de fournir une collection pour des mises à jour en masse, et le même modèle gérera n’importe quel scénario de remise que vous lui présenterez.

Prêt pour le niveau suivant ? Essayez :

- Ajouter des calculs de taxe en plus des remises.  
- Récupérer les pourcentages de remise depuis une base de données au lieu de les coder en dur.  
- Utiliser le formatage conditionnel pour mettre en évidence les lignes avec des remises élevées.  

Ces extensions conservent l’idée de base tout en augmentant l’utilité de votre modèle de remise.

Des questions ou un cas d’utilisation intéressant ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}