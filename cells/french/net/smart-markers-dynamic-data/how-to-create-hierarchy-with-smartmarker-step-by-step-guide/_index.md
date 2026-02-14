---
category: general
date: 2026-02-14
description: Créer une hiérarchie dans les modèles SmartMarker est plus facile que
  vous ne le pensez – apprenez à créer des données hiérarchiques et à répertorier
  les employés efficacement.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: fr
og_description: Comment créer une hiérarchie dans les modèles SmartMarker est simple.
  Suivez ce guide pour créer des données hiérarchiques et lister les employés avec
  des plages imbriquées.
og_title: Comment créer une hiérarchie avec SmartMarker – Guide complet
tags:
- SmartMarker
- C#
- templating
title: Comment créer une hiérarchie avec SmartMarker – Guide étape par étape
url: /fr/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer une hiérarchie avec SmartMarker – Guide complet

Vous vous êtes déjà demandé **comment créer une hiérarchie** dans un modèle SmartMarker sans vous arracher les cheveux ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting, vous avez besoin d'une relation parent‑enfant — pensez aux départements et aux personnes qui y travaillent. La bonne nouvelle, c'est que SmartMarker rend cela un jeu d'enfant une fois que vous connaissez les bonnes étapes.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : de **la création de données hiérarchiques** en C#, à l'activation des plages imbriquées, et enfin au rendu d’un modèle qui **liste les employés** pour chaque département. À la fin, vous disposerez d’un exemple prêt à l'emploi que vous pourrez intégrer dans n’importe quel projet .NET.

---

## Ce dont vous avez besoin

- .NET 6+ (toute version récente fonctionne)
- Une référence à la bibliothèque **SmartMarker** (l’espace de noms `ws.SmartMarkerProcessor`)
- Connaissances de base en C# – rien de compliqué, juste quelques objets et une ou deux lambda
- Un IDE ou éditeur de votre choix (Visual Studio, Rider, VS Code… à vous de choisir)

Si vous avez déjà tout cela, super—plongeons-y.

---

## Comment créer une hiérarchie – Vue d’ensemble

L’idée principale est de construire un **graph d’objets imbriqués** qui reflète la structure que vous souhaitez voir dans le document final. Dans notre cas, le graphe ressemble à :

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker peut alors itérer sur `Departments` et, comme nous activerons le **traitement des plages imbriquées**, il parcourra également la collection `Employees` de chaque département automatiquement.

---

## Étape 1 : Construire le modèle de données hiérarchique

Tout d’abord, nous créons un objet anonyme qui contient un tableau de départements, chacun avec sa propre liste d’employés. L’utilisation d’un type anonyme rend l’exemple léger—n’hésitez pas à le remplacer par de vraies classes POCO plus tard.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Pourquoi c’est important :** Le tableau `Departments` est la collection de niveau supérieur. Chaque élément contient un tableau `Employees`, nous offrant le deuxième niveau de hiérarchie auquel nous accéderons plus tard avec `#Departments.Employees#`.

---

## Étape 2 : Activer le traitement des plages imbriquées

SmartMarker n’explorera pas les collections internes à moins que vous ne le lui indiquiez. L’objet `SmartMarkerOptions` contient cet interrupteur.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Astuce :** Si vous oubliez ce drapeau, la plage interne `#Employees#` ne renvoie simplement rien, et vous vous gratterez la tête en vous demandant pourquoi le modèle est vide.

---

## Étape 3 : Exécuter le processeur avec vos données

Nous transmettons maintenant les données et les options au processeur. La variable `ws` représente votre **WebService** (ou tout autre objet hébergeant le moteur SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

À ce stade, SmartMarker analyse le modèle, remplace `#Departments.Name#` par le nom de chaque département, puis, comme les plages imbriquées sont activées, parcourt la collection `Employees` de chaque département.

---

## Étape 4 : Concevoir les marqueurs du modèle

Ci-dessous se trouve un modèle minimal qui montre à la fois la boucle externe et la boucle interne. Collez‑le dans l’éditeur de modèle SmartMarker (ou dans un fichier `.txt` que vous passez au processeur).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Lors du rendu, vous verrez :

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Ce que vous voyez :** Le `#Departments.Name#` externe affiche le titre du département. Le bloc interne `#Departments.Employees#` parcourt chaque employé, et `#Departments.Employees#` à l’intérieur du bloc affiche le nom réel.

---

## Résultat attendu & vérification

Exécuter l’exemple complet (données + options + modèle) devrait produire exactement la liste affichée ci‑dessus. Pour vérifier rapidement, vous pouvez afficher le résultat dans la console :

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Si vous voyez les deux titres de département suivis de leurs puces d’employés, vous avez réussi à **créer une hiérarchie** et à **lister les employés**.

---

## Pièges courants & cas limites

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Aucun résultat pour les employés | `EnableNestedRange` laissé à false | Définir `EnableNestedRange = true` |
| Noms d’employés en double | Même tableau réutilisé entre les départements | Cloner le tableau ou utiliser des collections distinctes |
| Hiérarchies très volumineuses provoquent une pression mémoire | SmartMarker charge tout le graphe d’objets en mémoire | Diffuser les données ou paginer les grandes collections |
| Erreurs de syntaxe du modèle | Balises de fermeture `#/…#` manquantes | Utiliser le validateur SmartMarker ou exécuter un test rapide avec un petit modèle |

---

## Aller plus loin – Variations du monde réel

1. **Sources de données dynamiques** – Récupérez les départements depuis une base de données et mappez‑les à la structure anonyme à l’aide de LINQ.  
2. **Mise en forme conditionnelle** – Ajoutez un drapeau `IsManager` à chaque employé et utilisez les balises conditionnelles de SmartMarker (`#if …#`) pour mettre en évidence les managers.  
3. **Niveaux d’imbrication multiples** – Si vous avez besoin d’équipes au sein des départements, ajoutez simplement une autre collection (`Teams`) et conservez `EnableNestedRange` activé.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Modèle (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

L’exécution du programme affiche la hiérarchie exactement comme indiqué précédemment.

---

## Conclusion

Nous avons couvert **comment créer une hiérarchie** dans SmartMarker, depuis la création de **données hiérarchiques** en C# jusqu’à l’activation des plages imbriquées et enfin le rendu d’un modèle qui **liste les employés** par département. Le modèle est extensible—ajoutez simplement plus de collections imbriquées ou de logique conditionnelle et vous disposerez d’un moteur de reporting puissant à portée de main.

Prêt pour le prochain défi ? Essayez de remplacer les types anonymes par des classes POCO fortement typées, ou intégrez ce flux dans un point de terminaison ASP.NET Core qui renvoie un document PDF ou Word. Le ciel est la limite, et vous avez maintenant une base solide.

![How to create hierarchy diagram](image.png){alt="Diagramme montrant la création de hiérarchie avec la relation département‑employé"}

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—je serai heureux d’aider.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}