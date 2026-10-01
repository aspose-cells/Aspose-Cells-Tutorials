---
category: general
date: 2026-10-01
description: Convertir une date d’ère japonaise en DateTime grégorien avec Aspose.Cells
  en C#. Apprenez à convertir rapidement le calendrier japonais.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: fr
lastmod: 2026-10-01
og_description: Convertir une date d’ère japonaise en DateTime grégorien en C#. Ce
  tutoriel explique comment convertir le calendrier japonais avec précision à l’aide
  d’Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Convertir une date de l’ère japonaise en calendrier grégorien en C# – guide
  étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Comment convertir une date de l’ère japonaise en calendrier grégorien en C#
url: /fr/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir une date d'ère japonaise en calendrier grégorien en C#

Si vous devez **convertir des dates d'ère japonaise** en dates grégoriennes en C#, ce guide vous montre exactement comment faire. Que vous traitiez des données héritées, lisiez des entrées utilisateur ou génériez des rapports, la bibliothèque Aspose.Cells rend la conversion simple. De plus, vous découvrirez la meilleure façon de **convertir le calendrier japonais** lors du travail avec des feuilles de calcul.

Le tutoriel couvre chaque étape — de la création d'un classeur à la récupération d'une valeur `DateTime` — afin que vous puissiez copier‑coller un programme complet et exécutable. Aucune documentation externe n'est requise ; suivez simplement le code et les explications ci‑dessous.

## Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.6+)
* Une licence pour **Aspose.Cells** (l'essai gratuit fonctionne pour les tests)
* Un environnement de développement tel que Visual Studio 2022 ou VS Code
* Une connaissance de base des applications console C#

## Convertir une date d'ère japonaise avec Aspose.Cells

Le cœur de la conversion repose sur quelques appels d'API simples. Aspose.Cells interprète automatiquement les chaînes d'ère japonaise (par ex., « Reiwa 2/04/01 ») et expose le résultat sous forme d'objet `DateTime` une fois la feuille de calcul recalculée.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Pourquoi chaque étape est importante

| Étape | Objectif | Comment cela aide la conversion |
|------|----------|---------------------------------|
| **Créer un classeur** | Fournit un conteneur qui comprend les formules Excel et les systèmes de dates. | Le moteur de dates interne de la bibliothèque n'est activé que dans un classeur. |
| **Insérer la chaîne d'ère** | Fournit le texte brut du calendrier japonais que vous souhaitez traduire. | Aspose.Cells reconnaît les noms d'ères comme *Reiwa*, *Heisei*, *Showa*, etc. |
| **Définir le style** | Force la cellule à être traitée comme une cellule de valeur plutôt que comme une chaîne littérale. | Sans style, la méthode `Calculate` peut ignorer la cellule, laissant le texte inchangé. |
| **Calculer** | Déclenche l'analyse de la chaîne d'ère et la conversion en nombre de série interne. | La bibliothèque convertit « Reiwa 2/04/01 » → nombre de série → `DateTime` grégorien. |
| **Lire `DateTimeValue`** | Renvoie l'objet .NET `DateTime` converti. | Vous disposez maintenant d'un `DateTime` standard que vous pouvez utiliser dans n'importe quelle API .NET. |

## Comment convertir le calendrier japonais dans d'autres scénarios

La même approche fonctionne pour tout nom d'ère japonaise pris en charge par Aspose.Cells :

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Gestion des chaînes invalides ou ambiguës

* **Invalid era name** – Aspose.Cells lance une `FormatException`. Enveloppez la conversion dans un `try/catch` pour fournir un message d'erreur convivial.
* **Missing year/month/day** – La bibliothèque attend un motif complet « Era Year/Month/Day ». Si vous recevez des données partielles, préfixez les parties manquantes ou rejetez l'entrée dès le départ.
* **Different locale settings** – La conversion ne dépend **pas** de la culture du thread actuel ; elle utilise toujours la carte des ères japonaises intégrée à Aspose.Cells. Cela rend la méthode sûre pour le traitement côté serveur.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Conseils pratiques et pièges courants

* **Always call `SetStyle`** avant `Calculate`. Ignorer cette étape est une source fréquente de bugs car la cellule reste un simple conteneur de texte.
* **Reuse the same workbook** si vous devez convertir de nombreuses dates. Créer un nouveau classeur pour chaque conversion ajoute une surcharge inutile.
* **Batch conversion** – Remplissez une colonne avec des chaînes d'ère, appelez `worksheet.Calculate()` une fois, puis lisez toute la colonne de `DateTimeValue`. C’est bien plus efficace que de recalculer cellule par cellule.
* **Version compatibility** – La logique de conversion d'ère a été introduite dans Aspose.Cells 22.9. Assurez‑vous d’utiliser cette version ou une version ultérieure ; les versions antérieures traitent la chaîne comme du texte brut.

## Exemple complet fonctionnel (application console)

Voici un programme autonome que vous pouvez compiler et exécuter immédiatement. Il montre à la fois une conversion Reiwa et Heisei, en gérant les erreurs de manière élégante.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Sortie console attendue**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

L'exécution de ce programme confirme que la bibliothèque convertit correctement les chaînes **de dates d'ère japonaise** et signale élégamment les valeurs non prises en charge.

## Conclusion

Vous savez maintenant comment **convertir des dates d'ère japonaise** en objets `DateTime` grégoriens standard en utilisant Aspose.Cells en C#. Le processus se résume à insérer le texte d'ère, appliquer un style, recalculer la feuille de calcul et lire `DateTimeValue`. En suivant les étapes ci‑dessus, vous pouvez également répondre à la question plus large de **comment convertir le calendrier japonais** en masse, gérer les erreurs et optimiser les performances.

### Prochaines étapes

* Explorez les **options de formatage** pour écrire la date grégorienne dans la feuille de calcul avec un format numérique personnalisé.
* Combinez cette conversion avec les **pipelines d'importation de données** (par ex., lecture de fichiers CSV contenant des dates d'ère).
* Examinez d'autres fonctionnalités d'Aspose.Cells telles que **l'arithmétique des dates** et les **paramètres régionaux** pour des scénarios de calendrier plus complexes.

Bonne programmation, et n'hésitez pas à adapter l'exemple à vos propres flux de traitement de données !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Analyser les dates d'ère japonaise en C# avec Aspose.Cells – Guide complet](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Activer l'analyse d'ère japonaise en C# avec Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Comment créer un classeur et convertir une chaîne en date en C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}