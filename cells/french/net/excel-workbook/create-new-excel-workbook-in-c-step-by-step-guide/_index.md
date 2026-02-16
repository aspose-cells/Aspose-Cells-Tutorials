---
category: general
date: 2026-02-15
description: Créer un nouveau classeur Excel et apprendre à utiliser EXPAND, développer
  une séquence et calculer la cotangente. Voir également comment enregistrer le classeur
  dans un fichier.
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: fr
og_description: Créer un nouveau classeur Excel avec C#. Apprenez à utiliser EXPAND,
  à développer une séquence, à calculer la cotangente et à enregistrer le classeur
  dans un fichier.
og_title: Créer un nouveau classeur Excel en C# – Guide complet de programmation
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un nouveau classeur Excel en C# – Guide étape par étape
url: /fr/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un nouveau classeur Excel en C# – Guide complet de programmation

Vous avez déjà eu besoin de **créer un nouveau classeur Excel** depuis le code et vous ne saviez pas par où commencer ? Vous n'êtes pas seul ; de nombreux développeurs rencontrent ce problème lorsqu'ils automatisent des rapports ou construisent des pipelines de données. Dans ce tutoriel, nous vous montrerons exactement comment créer un nouveau classeur Excel, écrire quelques formules intéressantes, puis **enregistrer le classeur dans un fichier** pour une inspection ultérieure.  

Nous plongerons également dans les détails de la fonction `EXPAND`, démontrerons **how to use expand** pour transformer une petite séquence en un grand bloc, expliquerons **how to expand sequence** en pratique, et enfin révélerons **how to calculate cotangent** directement dans Excel. À la fin, vous disposerez d'un programme C# exécutable que vous pourrez intégrer à n'importe quel projet .NET.

## Ce dont vous avez besoin

- **Aspose.Cells for .NET** (version d'essai gratuite ou version sous licence) – la bibliothèque qui nous permet de manipuler Excel sans Office installé.  
- **.NET 6+** (ou .NET Framework 4.6+).  
- Un IDE modeste tel que Visual Studio 2022, VS Code ou Rider.  

Aucun package NuGet supplémentaire n'est requis au-delà de `Aspose.Cells`. Si vous ne l'avez pas encore, exécutez :

```bash
dotnet add package Aspose.Cells
```

C’est tout—rien d’autre à configurer.

## Étape 1 : Créer un nouveau classeur Excel

La toute première chose que nous faisons est d'instancier un objet `Workbook`. Considérez-le comme une toile vierge où toutes les feuilles, cellules et formules vivront.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **Pourquoi c'est important :** Créer le classeur en mémoire signifie que nous ne touchons jamais le disque jusqu'à ce que nous décidions explicitement d'**enregistrer le classeur dans un fichier**. Cela maintient l'opération rapide et vous permet d'enchaîner d'autres modifications sans surcharge d'E/S.

## Étape 2 : Comment utiliser EXPAND pour étendre une séquence

`EXPAND` est une fonction Excel plus récente qui prend un tableau plus petit et l'étire à une taille définie. Dans notre exemple, nous commençons avec une séquence verticale de trois lignes et la transformons en un bloc 5 × 5.

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **Explication :** `SEQUENCE(3)` produit `{1;2;3}` (un tableau vertical). `EXPAND(...,5,5)` indique à Excel de répéter ce tableau jusqu'à ce qu'il remplisse un rectangle de 5 lignes par 5 colonnes, en commençant à A1. Le résultat est une matrice où chaque colonne répète les trois nombres d'origine, et les deux dernières lignes sont vides parce que la source ne comporte que trois lignes.

### Résultat attendu

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

Vous verrez le même motif se répéter sur la plage une fois le classeur ouvert dans Excel.

## Étape 3 : Comment calculer la cotangente dans Excel

La plupart des gens connaissent `SIN`, `COS` et `TAN`, mais `COT` est un raccourci pratique pour le réciproque de la tangente. Voici comment obtenir la cotangente de 45° (qui vaut 1) en utilisant les radians.

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Pourquoi utiliser COT ?** Appeler directement `COT` évite la division supplémentaire nécessaire avec `1/TAN(...)`, rendant la formule plus claire et légèrement plus rapide pour les grandes feuilles.

## Étape 4 : Évaluer toutes les formules

Aspose.Cells ne calcule pas automatiquement les formules à moins que vous ne le lui indiquiez. La méthode `CalculateFormula` force une évaluation complète afin que les valeurs résultantes soient stockées dans les cellules.

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **Astuce :** Si vous avez de nombreuses formules coûteuses, vous pouvez passer un objet `CalculationOptions` pour affiner les performances (par ex., activer le multithreading).

## Étape 5 : Enregistrer le classeur dans un fichier

Maintenant que tout est prêt, nous **enregistrons le classeur dans un fichier**. Choisissez un dossier où vous avez les droits d'écriture et donnez au fichier un nom significatif.

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Que se passe-t-il sur le disque ?** L'appel `Save` écrit un package `.xlsx` complet, incluant le tableau étendu provenant de `EXPAND` et la valeur de cotangente calculée. Ouvrez le fichier dans Excel et vous verrez le bloc 5 × 5 commençant à A1 et le nombre `1` en B1.

![Sortie Excel montrant la séquence étendue et la valeur de cotangente](excel-output.png "exemple de sortie de création d'un nouveau classeur Excel")

*Texte alternatif de l'image : exemple de sortie de création d'un nouveau classeur Excel*

### Vérification rapide

1. Ouvrez `output.xlsx`.  
2. Vérifiez que les cellules **A1:E5** contiennent le motif répété 1‑2‑3.  
3. Regardez **B1** – elle doit afficher `1`.  

Si tout correspond, félicitations—vous avez automatisé Excel avec succès !

## Comment étendre une séquence dans d'autres scénarios

Bien que l'exemple ci‑dessus utilise un `SEQUENCE(3)` statique, vous pouvez facilement le remplacer par une plage dynamique ou une autre formule :

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**Quand l'utiliser ?**  
- Générer des tables de substitution pour les modèles.  
- Répliquer rapidement une ligne d'en-tête sur de nombreuses colonnes.  
- Construire des grilles de cartes thermiques sans copier‑coller manuel.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| `#VALUE!` après `EXPAND` | Le tableau source n'est pas une plage correcte (par ex., contient des erreurs) | Nettoyez les données sources ou encapsulez-les dans `IFERROR`. |
| La cotangente renvoie `#DIV/0!` pour 0° | `COT(0)` est mathématiquement infini | Protégez avec `IF(PI()/4=0,0,COT(...))`. |
| Le classeur n'est pas enregistré | Le chemin est invalide ou les permissions d'écriture manquent | Utilisez `Path.GetFullPath` et vérifiez que le dossier existe. |
| Les formules ne sont pas calculées | `CalculateFormula` omis | Appelez toujours cette méthode avant `Save`. |

## Bonus : Ajouter du style (optionnel)

Si vous souhaitez que la sortie soit plus esthétique, vous pouvez appliquer un style simple après les calculs :

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

Cet extrait est optionnel, mais il illustre comment vous pouvez combiner la logique de **create new Excel workbook** avec le formatage en une seule passe.

## Récapitulatif

Nous avons parcouru l'ensemble du processus :

1. **Create new Excel workbook** avec Aspose.Cells.  
2. Utilisez **how to use expand** pour transformer un petit `SEQUENCE` en une matrice 5 × 5.  
3. Montrez **how to calculate cotangent** directement dans une cellule.  
4. Forcez le calcul avec `CalculateFormula`.  
5. **Save workbook to file** et vérifiez le résultat.

Tout cela est autonome, fonctionne sur n'importe quel runtime .NET récent, et ne nécessite qu'un seul package NuGet.

## Et après ?

- **Dynamic data sources** : extraire des données d'une base de données et les injecter dans `EXPAND`.  
- **Multiple worksheets** : parcourir une collection de feuilles pour générer un classeur de rapport complet.  
- **Advanced formulas** : explorer `LET`, `LAMBDA` ou la logique conditionnelle basée sur des tableaux pour des feuilles de calcul plus intelligentes.  

N'hésitez pas à expérimenter—remplacez l'argument `SEQUENCE`, essayez différents angles pour `COT`, ou intégrez la génération de graphiques. Le ciel est la limite lorsque vous pouvez **create new Excel workbook** de façon programmatique.

---

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou contactez‑moi sur Twitter @YourHandle. Je serai ravi d'aider.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}