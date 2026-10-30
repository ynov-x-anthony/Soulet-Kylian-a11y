# AUDIT.md : à compléter

## 1. Audits outillés

Lance les 3 audits sur la page (`npm run dev`, puis ouvre-la dans Chrome) et
colle ici un résumé de ce que chacun remonte :

- **Lighthouse** (DevTools → onglet Lighthouse → catégorie Accessibility) :
  Score d'accessibilité abaissé (~81/100). Détecte 4 éléments en échec sur la règle *« Background and foreground colors do not have a sufficient contrast ratio »* (`color-contrast`) ciblant `.subtitle`, `.label`, `.hint` et le bouton `.btn-primary`.

- **axe DevTools** (extension Chrome) :
  Signale 4 violations de sévérité *Serious* sur la règle `color-contrast` (*« Elements must meet minimum color contrast ratio thresholds »*). Les éléments incriminés ne respectent pas le ratio minimum de 4.5:1 pour du texte de corps standard.

- **WAVE** (https://wave.webaim.org/, ou l'extension) :
  Détecte 4 erreurs de contraste (icônes rouges *« Very low contrast »*) sur le sous-titre `.subtitle`, le libellé `.label`, le texte d'astuce `.hint` et le texte blanc du bouton `.btn-primary`.

## 2. Les éléments à corriger

| Élément | Couleur texte | Couleur fond | Ratio mesuré | Ratio AA requis | Conforme ? |
|---------|---------------|--------------|--------------|------------------|------------|
| `.subtitle` | `#aaaaaa` | `#ffffff` | ~2.3:1 | 4.5:1 | Non |
| `.label` | `#999999` | `#ffffff` | ~2.8:1 | 4.5:1 | Non |
| `.hint` | `#bbbbbb` | `#ffffff` | ~1.8:1 | 4.5:1 | Non |
| `.btn-primary` | `#ffffff` | `#6fa8dc` | ~2.5:1 | 4.5:1 (texte) | Non |

> Utilise un vérificateur de contraste (ex. le picker de couleur de Chrome
> DevTools affiche déjà le ratio AA/AAA quand tu modifies une couleur).

## 3. Priorisation

Classe les 4 corrections par ordre d'impact (1 = le plus urgent) et explique pourquoi.

1. **`.btn-primary` (Bouton d'action "Gérer mon abonnement")** :
   C'est l'élément interactif clé (Call to Action principal) de la page. Si un utilisateur malvoyant ne peut pas lire le libellé de l'action ou la repérer nettement, il ne peut pas accomplir sa tâche.

2. **`.hint` (Texte d'astuce/facturation)** :
   Présente le pire ratio de contraste de toute la page (~1.8:1, quasiment invisible). Ce texte contient une consigne essentielle sur la facturation et le renouvellement automatique.

3. **`.label` (Libellé "Statut de l'abonnement")** :
   Donne le contexte indispensable à la valeur affichée en dessous ("Actif jusqu'au..."). Sans libellé lisible, la valeur perd sa signification pour les personnes ayant des déficiences visuelles.

4. **`.subtitle` (Sous-titre général)** :
   Texte d'accompagnement informatif ("Gère ton abonnement et tes préférences."). Moins bloquant d'un point de vue fonctionnel que le bouton d'action et les données d'abonnement, mais indispensable pour une lecture confortable de l'en-tête.
