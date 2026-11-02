---
category: general
date: 2026-03-29
description: Comment substituer des variables dans JSON en utilisant SmartMarker –
  apprenez à utiliser l’expression if, appliquer la logique conditionnelle, multiplier
  les valeurs et générer du JSON sans effort.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: fr
og_description: Comment substituer des variables dans JSON en utilisant SmartMarker.
  Découvrez comment utiliser l’expression if, appliquer une logique conditionnelle,
  multiplier des valeurs et générer du JSON en quelques minutes.
og_title: Comment remplacer des variables dans JSON avec SmartMarker – Étape par étape
tags:
- C#
- SmartMarker
- JSON templating
title: Comment remplacer des variables dans JSON avec SmartMarker – Guide complet
url: /fr/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment substituer des variables dans JSON avec SmartMarker – Guide complet

Vous vous êtes déjà demandé **how to substitute variables** à l'intérieur d'une charge JSON sans écrire un analyseur personnalisé ? Vous n'êtes pas seul. Dans de nombreux scénarios d'intégration — pensez aux factures, aux moteurs de tarification ou aux fichiers de configuration dynamiques — vous devez injecter des valeurs d'exécution, appliquer des conditions simples, et peut‑être même effectuer une multiplication rapide. Ce tutoriel vous montre exactement **how to substitute variables** en utilisant la bibliothèque SmartMarker, tout en gardant le JSON propre et lisible.

Nous allons parcourir un exemple réel qui couvre **use if expression**, **how to apply conditional**, **how to multiply values**, et **how to generate json** à la volée. À la fin, vous disposerez d’un extrait C# prêt à l’emploi que vous pourrez intégrer dans n’importe quel projet .NET.

## Ce que vous allez apprendre

- Configurer `SmartMarkerOptions` pour stocker des variables réutilisables.  
- Écrire un modèle JSON contenant une expression `if` pour la logique conditionnelle.  
- Multiplier une valeur par une variable dans le modèle.  
- Traiter le modèle avec `SmartMarkerProcessor` et obtenir la chaîne JSON finale.  
- Dépanner les problèmes courants tels que les variables manquantes ou les expressions mal formées.

Aucun service externe, aucune dépendance lourde — juste du C# pur et le package NuGet SmartMarker.

---

## Comment substituer des variables – Vue d’ensemble étape par étape

Voici une vue d’ensemble du flux de travail. Pensez à un pipeline où votre modèle JSON brut entre à gauche, le moteur SmartMarker fait sa magie, et le JSON entièrement rendu sort à droite.

![Diagramme montrant comment substituer des variables dans JSON](https://example.com/images/smartmarker-flow.png "Comment substituer des variables dans JSON")

*Texte alternatif de l’image : Diagramme montrant comment substituer des variables dans JSON.*

---

## Étape 1 : Installer et importer SmartMarker

Avant de commencer, assurez‑vous que le package SmartMarker est référencé dans votre projet. Si vous utilisez le .NET CLI, exécutez :

```bash
dotnet add package SmartMarker
```

Puis, ajoutez les directives `using` nécessaires en haut de votre fichier C# :

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Astuce :** La dernière version (en mars 2026) est la 2.4.1. Elle prend en charge .NET 6 et ultérieur, mais fonctionne également avec .NET Framework 4.7.

---

## Étape 2 : Créer les options SmartMarker et définir les variables

Nous allons maintenant créer une instance de `SmartMarkerOptions` qui contiendra toutes les variables que nous souhaitons réutiliser dans le modèle. C’est ici que nous répondons à la question **how to substitute variables** — les variables agissent comme des espaces réservés que SmartMarker remplacera plus tard.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Pourquoi stocker le taux dans `Variables` plutôt que de l’écrire en dur ? Parce que vous pourriez récupérer ce nombre depuis une base de données, un fichier de configuration ou une saisie utilisateur. Le garder dans les options rend le modèle réutilisable et testable.

---

## Étape 3 : Rédiger le modèle JSON avec une expression `if`

C’est ici que le mot‑clé **use if expression** brille. SmartMarker vous permet d’embarquer une logique conditionnelle directement dans la chaîne JSON. La syntaxe ressemble un peu à un nom de propriété, mais SmartMarker l’interprète comme une directive.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Remarquez la clé `if(Amount>500)`. SmartMarker évalue l’expression `Amount>500` ; si elle est vraie, la valeur correspondante (`${Amount * Rate}`) est insérée dans le résultat. La syntaxe `${...}` est le moteur de *substitution de variables* — ici nous **how to multiply values** (`Amount * Rate`) avant d’injecter le résultat.

---

## Étape 4 : Traiter le modèle et récupérer le JSON final

Avec les options et le modèle prêts, nous transmettons le tout au processeur. La méthode `ProcessJson` analyse le modèle, applique la condition, effectue la multiplication, et renvoie une chaîne JSON propre.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

L’exécution de l’extrait affiche :

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Que s’est‑il passé ?**  
- `Amount` vaut 1000, ce qui satisfait `Amount>500`.  
- SmartMarker évalue `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- La clé conditionnelle d’origine (`if(Amount>500)`) est remplacée par un nom de propriété propre (`Result`). Par défaut SmartMarker utilise `"Result"` mais vous pouvez le personnaliser (voir plus loin).

Si vous changez `Amount` à `400`, la sortie devient :

```json
{
  "Amount": 400
}
```

Le bloc conditionnel disparaît parce que l’expression a évalué à `false`. C’est l’essence de **how to apply conditional** dans JSON.

---

## Étape 5 : Personnaliser le nom de la propriété de sortie (optionnel)

Parfois vous ne voulez pas la clé générique `"Result"`. SmartMarker vous permet de spécifier un nom personnalisé via l’option `RenameIfExpression` :

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Sortie :

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Le résultat conditionnel est maintenant stocké sous un nom de propriété plus significatif — parfait pour les services en aval qui attendent un champ précis.

---

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Variable introuvable | Vous avez référencé une variable qui n’est pas dans `smartMarkerOptions.Variables`. | Vérifiez l’orthographe et assurez‑vous que la variable est ajoutée avant le traitement. |
| Syntaxe `if` invalide | Parenthèses manquantes ou opérateur incorrect (`>`, `<`, `==`). | Respectez exactement le modèle `if(<expression>)` ; SmartMarker ne supporte que les comparaisons numériques simples. |
| JSON mal formé | Virgule finale accidentelle après le bloc conditionnel. | Laissez SmartMarker gérer la suppression ; gardez le modèle d’origine syntaxiquement correct. |
| Format de nombre inattendu | Le résultat apparaît comme une chaîne `"80"` au lieu d’un nombre. | Convertissez ou parsez plus tard, ou utilisez `${(Amount * Rate):N0}` pour un format numérique. |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez compiler et exécuter. Il montre **how to generate json** avec des variables dynamiques, des conditionnels et de l’arithmétique — le tout en moins de 30 lignes.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Sortie console attendue**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

N’hésitez pas à modifier `Amount` pour tester la branche conditionnelle, ou à ajuster `Rate` pour voir différents calculs de remise.

---

## Étendre le modèle – Autres scénarios “How to”

- **How to substitute variables** depuis un fichier de configuration : chargez un `Dictionary<string, object>` depuis `appsettings.json` et injectez‑le dans `smartMarkerOptions.Variables`.  
- **How to use if expression** pour plusieurs conditions : enchaînez‑les comme `"if(Amount>500 && CustomerType=='VIP')"` — SmartMarker prend en charge les opérateurs logiques AND/OR.  
- **How to apply conditional** au formatage : utilisez `${Amount:0.00}` dans l’expression pour contrôler les décimales.  
- **How to multiply values** avec des calculs plus complexes : `${(Amount - Discount) * TaxRate}` fonctionne de la même façon.  
- **How to generate json** pour des objets imbriqués : placez le bloc conditionnel à l’intérieur d’un autre objet JSON, et SmartMarker préservera la hiérarchie.

---

## Conclusion

Nous avons couvert **how to substitute variables** dans JSON avec SmartMarker, démontré **use if expression** pour l’inclusion conditionnelle, expliqué **how to apply conditional**, montré **how to multiply values** dans un modèle, et enfin illustré **how to generate json** prêt à être consommé en aval. L’approche est légère, ne nécessite aucun moteur de templating externe, et s’intègre parfaitement à n’importe quel code C#.

Essayez‑le — ajustez les variables, ajoutez d’autres conditions, ou encapsulez le tout dans une classe d’aide réutilisable dans votre solution. Quand vous devez produire du JSON dynamique rapidement, SmartMarker est une option solide et prête pour la production.

---

**Prochaines étapes**

- Approfondir les fonctionnalités avancées de SmartMarker comme les boucles (`foreach`) et les fonctions personnalisées.  
- Combiner cette technique avec des points de terminaison ASP.NET Core pour servir des API JSON dynamiques.  
- Explorer d’autres bibliothèques de templating (par ex., Handlebars.NET) pour comparer, surtout si vous avez besoin d’une syntaxe plus riche.

Des questions ou un cas d’usage particulier qui vous bloque ? Laissez un commentaire ci‑dessous, et résolvons-le ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}