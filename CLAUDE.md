# CLAUDE.md — Instructions pour Claude Code

## Présentation du projet

Application web de formation destinée aux **référents numériques** pour animer une session de sensibilisation à l'IA auprès des parents d'élèves. Déployée sur Vercel à l'adresse `https://sensibiliser-parents-ia.vercel.app` (mot de passe : marta).

## Architecture

Le projet est un **site statique HTML/CSS/JS monofichier** — pas de framework, pas de bundler, pas de dépendances npm.

- `index.html` — fichier principal déployé, avec protection par mot de passe (sessionStorage)
- `app_formation.html` — même contenu sans login (usage local / développement)

Tout le CSS, le JS et les données pédagogiques sont dans le même fichier HTML.

## Conventions de code

- **Pas de framework** : vanilla JS uniquement
- **Pas de commentaires** sauf si la logique est non-évidente
- **CSS inline via `<style>`** dans le `<head>` — ne pas créer de fichier CSS séparé
- **Données dans `const DATA`** — toute modification de contenu pédagogique se fait dans cet objet JS
- **Persistance** : `localStorage` pour la progression et les notes, `sessionStorage` pour l'accès (login)
- Les deux fichiers (`index.html` et `app_formation.html`) doivent rester synchronisés — toute modification de l'un doit être reportée sur l'autre, à l'exception du bloc login

## Variables CSS

```css
--purple: #8B2FC9       /* couleur principale SOPHIAE */
--purple-light: #f3eafa
--purple-mid: #d4a8f0
--grey: #6b6b6b
--grey-light: #f0f0f0
--dark: #1e1e1e
--border: #e2e2e2
--mod1: #3b82f6         /* bleu — Module 1 */
--mod2: #10b981         /* vert — Module 2 */
--mod3: #f59e0b         /* orange — Module 3 */
--mod4: #ef4444         /* rouge — Module 4 */
--sidebar-w: 280px
--header-h: 64px
--panel-w: 272px        /* panneau animateur */
```

## Typographie

- `Cormorant Garamond` — titres, logo, timer animateur
- `Jost` — texte courant, interface
- `Lora` (italic) — astuces animateur

## Déploiement

```bash
# Le déploiement se fait via Vercel CLI ou push git automatique
# Vérifier que index.html est bien le fichier servi à la racine
```

## Points d'attention

- Le panneau animateur (`.anim-panel`) est fixe à droite — `margin-right: var(--panel-w)` sur `.main`
- Le responsive masque le panneau animateur sur mobile (`@media max-width: 900px`)
- Les timers par séquence sont gérés dans `state.timers` (objet JS en mémoire, pas persisté)
- La météo du groupe n'est pas persistée — elle se remet à zéro au rechargement
- Le total de séquences est calculé dynamiquement : `totalSeqs()` — ne pas hardcoder 15
