---
category: general
date: 2026-06-21
description: Activez la vérification orthographique lors de l'exportation du JSON
  Excel avec GridJs. Apprenez à convertir xlsx en JSON, à configurer le chargement
  différé et à charger efficacement le classeur Excel.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: fr
og_description: Activer la vérification orthographique lors de l'exportation d'Excel
  JSON avec GridJs. Ce guide montre comment convertir un fichier xlsx en JSON, configurer
  le chargement paresseux et charger un classeur Excel.
og_title: Activer la vérification orthographique et l’exportation Excel JSON avec
  GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Activer la vérification orthographique et l’exportation Excel JSON avec GridJs
url: /fr/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Activer la vérification orthographique et exporter le JSON Excel avec GridJs

Vous avez déjà eu besoin d'**activer la vérification orthographique** dans une interface de feuille de calcul web et vous vous êtes demandé comment obtenir les données au format JSON en même temps ? Vous n'êtes pas seul. De nombreux développeurs rencontrent le même problème lorsqu'ils essaient d'**exporter le JSON Excel** depuis un classeur tout en conservant des fonctionnalités avancées comme la validation des formules.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **charger un classeur Excel**, le transformer en charge utile JSON avec GridJs, **configurer le chargement paresseux**, et bien sûr **activer la vérification orthographique**. À la fin, vous serez capable de **convertir xlsx en JSON** en quelques lignes seulement — aucune énigme, aucune pièce manquante.

> **Ce que vous en retirerez**  
> * Un script Python qui lit un fichier `.xlsx`, crée un objet serveur GridJs et écrit `grid_data.json`.  
> * Une compréhension des raisons pour lesquelles chaque option est importante (vérification orthographique, vérification des formules, chargement paresseux).  
> * Des astuces pour faire évoluer la solution vers des classeurs plus volumineux.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants sur votre machine :

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.9+ | Nécessaire pour le package `cells` utilisé ci‑dessous. |
| `cells` library (`pip install cells`) | Fournit les classes `Workbook` et `GridJs`. |
| Un fichier Excel d'exemple (`sample.xlsx`) | C’est la source à partir de laquelle nous **chargerons le classeur Excel**. |
| Permission d'écriture sur le dossier de sortie | Nécessaire pour l'étape `grid.save()`. |

Si l'un de ces éléments vous est inconnu, faites une pause et installez‑les d'abord — sinon le script lèvera une erreur d'importation.

## Étape 1 : Charger le classeur Excel

La toute première chose à faire lorsque vous voulez **convertir xlsx en json** est d'ouvrir le classeur. Considérez cela comme déverrouiller la porte avant de pouvoir décorer la pièce.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Conseil pro :** Si votre fichier est volumineux, envisagez d'utiliser `cells.Workbook(..., read_only=True)` pour réduire la consommation de mémoire.

## Étape 2 : Créer un objet serveur GridJs

Maintenant que le classeur est en mémoire, nous avons besoin d'un objet **GridJs** qui traduira les feuilles en JSON que l'interface client pourra consommer.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

La variable `grid` est essentiellement un léger wrapper autour du classeur qui sait comment sérialiser les cellules, les formules et même les informations de style.

## Étape 3 : Activer la vérification orthographique (et le vérificateur de formules)

C’est ici que le mot‑clé principal brille. En basculant le drapeau `enableSpellCheck`, vous offrez aux utilisateurs finaux un filet de sécurité contre les fautes de frappe — tout comme dans Excel sur le bureau.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Pourquoi activer les deux ? La vérification orthographique détecte les erreurs textuelles, tandis que le vérificateur de formules protège contre les calculs défectueux. Ensemble, ils rendent l'interface web aussi soignée que l'expérience native d'Excel.

## Étape 4 : Configurer le chargement paresseux

Si vous traitez des milliers de lignes, envoyer l'ensemble du jeu de données en une seule charge étouffera le navigateur. **Configurez le chargement paresseux** pour envoyer les données par morceaux (500 lignes par requête dans notre exemple).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Vous pouvez ajuster `pageSize` en fonction de vos conditions réseau. Des pages plus petites signifient plus d'aller‑retour mais une interface plus fluide ; des pages plus grandes réduisent les appels mais peuvent entraîner du retard.

## Étape 5 : Exporter le JSON Excel

Tout le travail intensif est maintenant en arrière‑plan. L'acte final consiste à **exporter le json Excel** vers un fichier que votre front‑end peut demander.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Lorsque la méthode `save` se termine, vous disposerez d'un `grid_data.json` propre contenant :

* Noms et ID des feuilles  
* Données des lignes (valeurs, formules et formatage)  
* Métadonnées sur les fonctionnalités activées (vérification orthographique, chargement paresseux, etc.)

Vous pouvez vérifier la sortie en ouvrant le fichier dans un éditeur de texte ou en le chargeant dans la console du navigateur :

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

C’est une **solution complète et autonome** pour transformer un fichier Excel en charge utile JSON tout en conservant la vérification orthographique.

## Script complet – Tout assembler

Ci‑dessus se trouve le programme complet que vous pouvez copier‑coller, ajuster les chemins et exécuter. Aucun pas caché, aucun script externe — juste un seul fichier.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Enregistrez ceci sous le nom `export_gridjs.py` et exécutez :

```bash
python export_gridjs.py
```

Vous devriez voir une série de messages `[✓]` confirmant que chaque étape a réussi.

## Questions fréquentes et cas limites

**Et si mon classeur contient plusieurs feuilles ?**  
GridJs itère automatiquement sur chaque feuille, de sorte que le JSON résultant contiendra un tableau `sheets`. Vous pouvez filtrer côté client si vous n’avez besoin que d’un sous‑ensemble.

**Puis‑je désactiver la vérification orthographique pour une feuille spécifique ?**  
Le dictionnaire `options` s’applique globalement. Pour basculer par feuille, vous devrez créer des objets `GridJs` séparés ou post‑traiter le JSON.

**Mon fichier dépasse 10 Mo—le chargement paresseux sera‑t‑il toujours utile ?**  
Absolument. Le chargement paresseux fonctionne au niveau de l’API ; le serveur ne diffuse que la page demandée. Cependant, envisagez d’augmenter le `pageSize` à 1000 si votre latence réseau est faible.

**Dois‑je me préoccuper des caractères Unicode ?**  
`cells` gère l’UTF‑8 nativement, donc les caractères comme les emojis ou les scripts non latins survivent au aller‑retour.

## Conseils pro pour la production

* **Mettre en cache le JSON** – Si le classeur change rarement, mettez en cache `grid_data.json` dans un CDN pour des chargements ultra‑rapides.  
* **Sécurité** – N’exposez jamais le fichier Excel brut ; servez uniquement le JSON généré.  
* **Gestion des versions** – Incluez un numéro de version dans le nom du fichier JSON (par ex., `grid_data_v2.json`) pour éviter les données obsolètes après les mises à jour.  
* **Tests** – Écrivez un petit test unitaire qui charge le JSON et vérifie que `enableSpellCheck` est `true`. Cela détecte les régressions tôt.

## Conclusion

Vous disposez maintenant d’une recette solide, de bout en bout, pour **activer la vérification orthographique** tout en **exportant le JSON Excel** avec GridJs. De **charger le classeur Excel** à **configurer le chargement paresseux** et enfin **convertir xlsx en json**, le processus est simple et prêt pour la production.

Prochaines étapes ? Essayez d’intégrer le `grid_data.json` généré dans une page HTML simple qui utilise la bibliothèque cliente GridJs, expérimentez avec des rendus de cellules personnalisés, ou ajoutez une authentification autour du point d’accès JSON. Le ciel est la limite lorsque vous combinez vérification orthographique, chargement paresseux et conversion fluide d’Excel en JSON.

Vous avez d’autres questions ou un classeur difficile à gérer ? Laissez un commentaire ci‑dessus, et bon codage !

![Enable spell check in GridJs](/images/enable-spell-check-gridjs.png "Screenshot showing spell check enabled in GridJs UI")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Exporter Excel en JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Importer des données JSON dans Excel avec Aspose.Cells Java : Guide complet](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Comment filtrer efficacement les données lors du chargement de classeurs Excel avec Aspose.Cells en Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}