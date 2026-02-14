---
category: general
date: 2026-02-14
description: 'Automatisez la génération de factures avec SmartMarker : apprenez à
  dupliquer les feuilles de calcul, à les nommer dynamiquement et à maîtriser la nomination
  dynamique des feuilles en quelques minutes.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: fr
og_description: Automatisez la génération de factures avec SmartMarker. Ce guide montre
  comment répéter les feuilles de calcul, les nommer dynamiquement et maîtriser la
  nomination dynamique des feuilles.
og_title: Automatiser la génération de factures – Nommage dynamique des feuilles de
  calcul et répétition
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatiser la génération de factures – Nommage dynamique des feuilles de calcul
  et répétition en C#
url: /fr/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatiser la génération de factures – Nomination dynamique des feuilles de calcul et répétition en C#

Vous êtes‑vous déjà demandé comment **automatiser la génération de factures** sans copier manuellement les feuilles pour chaque commande ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un obstacle lorsqu'ils ont besoin d'une feuille de calcul distincte par facture tout en souhaitant que le nom de la feuille reflète le numéro de commande. Dans ce tutoriel, nous résoudrons ce problème en utilisant le `SmartMarkerProcessor` de SmartMarker et nous vous montrerons **comment nommer les feuilles de calcul** dynamiquement tout en couvrant **comment répéter une feuille de calcul** pour chaque enregistrement. À la fin, vous disposerez d'un exemple C# prêt à l'emploi qui produit un classeur où chaque facture se trouve sur son propre onglet, correctement nommé.

Nous parcourrons chaque étape — depuis la récupération des commandes depuis une source de données jusqu'à la configuration de `SmartMarkerOptions` pour la nomination dynamique des feuilles de calcul. Aucun document externe n'est requis ; tout ce dont vous avez besoin se trouve ici. Un petit bagage préalable en C# et une référence à la bibliothèque Aspose.Cells (ou à tout moteur compatible SmartMarker) suffiront.

---

## Ce que vous allez créer

- Récupérer une collection d'objets commande.
- Configurer SmartMarker pour **répéter une feuille de calcul** pour chaque commande.
- Appliquer **la nomination dynamique des feuilles de calcul** en utilisant le placeholder `{OrderId}`.
- Générer un fichier Excel où chaque onglet porte le nom `Invoice_12345`, `Invoice_67890`, etc.
- Vérifier le résultat en ouvrant le classeur.

---

## Prérequis

- .NET 6.0 ou version ultérieure (le code se compile également avec .NET 5+).
- Aspose.Cells pour .NET (ou toute bibliothèque implémentant SmartMarker). Installez via NuGet :

```bash
dotnet add package Aspose.Cells
```

- Une classe `Order` basique (vous pouvez la remplacer par votre propre DTO).

---

## Étape 1 : Configurer le projet et le modèle

Tout d'abord, créez une nouvelle application console et définissez le modèle de données qui représente une commande.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Astuce :** Gardez le modèle léger pour la démonstration ; vous pourrez toujours l'enrichir plus tard avec des lignes d'articles, des détails fiscaux, etc.

---

## Étape 2 : Préparer le modèle Excel

SmartMarker fonctionne sur un classeur modèle. Créez un fichier nommé `InvoiceTemplate.xlsx` contenant une seule feuille de calcul nommée `InvoiceTemplate`. Dans la cellule **A1**, placez un placeholder SmartMarker tel que :

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Vous pouvez formater les cellules comme vous le souhaitez — en‑têtes en gras, format monétaire, etc. Enregistrez le fichier dans le répertoire racine du projet.

> **Pourquoi un modèle ?** Il sépare la mise en page du code, permettant aux designers d'ajuster l'apparence sans toucher à la logique.

---

## Étape 3 : Configurer les options SmartMarker – Répéter et nommer les feuilles de calcul

Nous allons maintenant indiquer à SmartMarker de *répéter* la feuille de modèle pour chaque commande et d'attribuer à chaque copie un nom incluant l'ID de la commande. C’est le cœur de la **nomination dynamique des feuilles de calcul**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Comment cela fonctionne

- **`RepeatWorksheet = true`** indique au moteur de dupliquer la feuille source pour chaque élément de la collection `orders`. Cela répond à l'exigence **comment répéter une feuille de calcul**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** est une chaîne modèle où `{OrderId}` est un placeholder que SmartMarker remplace par l'ID de la commande en cours. C’est la réponse à **comment nommer les feuilles de calcul** et à la **nomination dynamique des feuilles de calcul**.
- Le processeur fusionne les champs de chaque commande (`{{OrderId}}`, `{{Customer}}`, etc.) dans la feuille dupliquée, produisant une facture entièrement remplie.

---

## Étape 4 : Exécuter l'application et vérifier la sortie

Compilez et exécutez l'application console :

```bash
dotnet run
```

Vous devriez voir le message de succès dans la console. Ouvrez `GeneratedInvoices.xlsx` et vous trouverez trois onglets :

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Chaque feuille contient les données de la commande substituées aux placeholders. La mise en page que vous avez conçue dans le modèle est conservée, prouvant que **automatiser la génération de factures** fonctionne de bout en bout.

### Capture d'écran attendue (texte alternatif pour le SEO)

![exemple d'automatisation de génération de factures montrant trois feuilles nommées dynamiquement](/images/invoice-automation.png)

> *Le texte alternatif de l'image inclut le mot‑clé principal pour satisfaire le SEO.*

---

## Étape 5 : Cas limites et variations courantes

### Que faire si un OrderId contient des caractères illégaux ?

Les noms de feuilles Excel ne peuvent pas contenir `\ / ? * [ ] :`. Si vos ID peuvent inclure ces caractères, nettoyez‑les :

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Ajoutez une propriété calculée à `Order` :

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Besoin de conserver la feuille modèle originale ?

Définissez `smartMarkerOptions.RemoveTemplate = false;` (la valeur par défaut est `true`). Cela laisse la `InvoiceTemplate` originale intacte comme référence.

### Vous souhaitez regrouper les factures par client ?

Vous pouvez imbriquer des **groupes de répétition**. D'abord répéter par client, puis par commandes à l'intérieur de chaque feuille de client. La syntaxe devient un peu plus complexe, mais le principe reste le même — utilisez `RepeatWorksheet` et un modèle de nommage qui reflète la hiérarchie.

---

## Exemple complet fonctionnel (tout le code en un seul endroit)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copiez‑collez ceci dans `Program.cs`, placez `InvoiceTemplate.xlsx` à côté, et vous êtes prêt à partir.

---

## Questions fréquentes

**Q : Cette approche fonctionne‑t‑elle avec de grands ensembles de données (des milliers de factures) ?**  
R : Oui. SmartMarker diffuse les données efficacement, mais surveillez l’utilisation de la mémoire. Si vous atteignez des limites, envisagez de traiter par lots et d’écrire chaque lot dans un classeur séparé.

**Q : Puis‑je ajouter automatiquement un logo à chaque facture ?**  
R : Absolument. Placez l’image du logo sur la feuille modèle. Comme la feuille est dupliquée, le logo apparaît sur chaque facture générée sans code supplémentaire.

**Q : Que faire si je dois protéger les feuilles de calcul ?**  
R : Après le traitement, parcourez `wb.Worksheets` et appelez `ws.Protect(Password, ProtectionType.All)`.

---

## Conclusion

Nous venons d'**automatiser la génération de factures** en exploitant la fonctionnalité de répétition de feuille de SmartMarker et un modèle de nommage astucieux. Le tutoriel a couvert **comment nommer les feuilles de calcul**, démontré **comment répéter une feuille de calcul** pour chaque commande, et présenté la **nomination dynamique des feuilles de calcul** qui maintient votre classeur ordonné et facilement recherchable.  

De la récupération des données, à la mise en place d'un modèle, la configuration de `SmartMarkerOptions`, jusqu'à la gestion des cas limites, vous disposez maintenant d'une solution complète et exécutable. Ensuite, essayez d'ajouter des tableaux d'articles, d'appliquer un formatage conditionnel, ou d'exporter les mêmes données en PDF pour une chaîne de facturation entièrement automatisée.

Prêt à passer au niveau supérieur ? Explorez des sujets connexes tels que « exportation massive d'Excel avec Aspose.Cells », « conversion PDF des feuilles de calcul », ou « envoi des factures générées directement depuis C# ». Le ciel est la limite — bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}