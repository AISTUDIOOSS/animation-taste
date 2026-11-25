---
name: animation-taste
description: À utiliser quand quelqu'un demande à Claude une animation (HTML, canvas, motion design, animation pour un Reel ou une vidéo) et veut qu'elle ait l'air de sortir d'un vrai studio, pas d'être une animation Claude de plus. Dirige l'animation comme un directeur artistique dirige une personne : image de référence d'abord, premier jet assumé, retours précis sur ce qui ne va pas, et des tours jusqu'à ce que ce soit bon. Contient un guide de goût pour le rendu, le grain et le mouvement (le style « feu de camp ») et un style collage papier pour les Reels.
argument-hint: "[ce qu'il faut animer] + [une image de référence]"
---

# Animation Taste

Claude sait animer. Ce qu'il ne sait pas, c'est ce qui est beau et ce qui est moche. Laissé seul, il sort la même chose à tout le monde : les mêmes couleurs, les mêmes dégradés lisses, les mêmes cartes qui flottent, les mêmes mouvements. C'est chiant et ça se repère direct.

Ce skill fait de la personne le directeur artistique. On n'écrit pas « un meilleur prompt ». On dirige, comme on dirigerait quelqu'un : on montre, on regarde, on dit précisément ce qui ne va pas, on recommence.

Tous les fichiers cités sont dans le dossier de ce skill.

- `gout.md` : le goût. À lire avant de dessiner quoi que ce soit, à chaque fois.
- `critique.md` : la grille pour juger chaque jet, et comment transformer une impression floue en consigne précise.
- `exemples/feu-premier-jet.html` et `exemples/feu-dirige.html` : le même feu de camp sur la plage, premier jet brut et version dirigée. `exemples/comparaison.html` les montre côte à côte. C'est la barre à atteindre.

## La méthode, en 4 étapes

### 1. Une image de référence, jamais une description

Demande une image d'un style que la personne aime (une image de film, une illustration, une affiche, une capture). Une description comme « moderne, propre, cinématique » ne veut rien dire : tout le monde l'écrit, et Claude y répond avec le même look moyen.

- Si la personne donne une image : regarde-la et écris, en 6 lignes maximum, ce que tu vois vraiment : la palette (5 à 7 couleurs avec leur code hex), comment sont faites la lumière et l'ombre (aplats ? grain ? dégradé ?), le trait (aucun, fin, brut), la texture, le rythme du mouvement si c'est une vidéo, et la chose qui fait que c'est ce style-là et pas un autre.
- Si elle n'en a pas : montre-lui les deux feux de camp et demande « plutôt celui de gauche ou celui de droite ? », ou propose de partir du style feu de camp de `gout.md`. N'invente jamais un style à partir de mots.

Garde la même composition que la référence ou que le premier jet. Si on change la composition et le style en même temps, personne ne voit ce qui s'est amélioré.

### 2. Le premier jet, et le regarder

Fais un premier jet vite, dans un seul fichier HTML autonome (1080×1920 pour un Reel, 1920×1080 pour une vidéo, sauf demande contraire). Il sera moyen, voire pas ouf. C'est normal, dis-le franchement : « premier jet, il va être moyen, on corrige juste après ».

Puis regarde-le toi-même avant de le montrer. Fige des images en ajoutant `#t=<secondes>` à la fin de l'adresse (les exemples le gèrent ; donne la même chose à chaque fichier que tu écris) et fais des captures à 3 ou 4 moments de la boucle. Juge-les avec `critique.md`, pas de mémoire de ton code.

### 3. Dire précisément ce qui ne va pas

Jamais « rends-le plus beau », « plus pro », « plus dynamique ». Chaque consigne nomme une chose, où elle est, et ce qu'elle doit devenir :

- « les bords de la mer sont trop droits : rends-les irréguliers, en lobes »
- « l'écume est blanc pur : passe-la en crème, en 3 couches »
- « la lune est trop petite : 10 % plus grande »
- « la flamme gonfle comme un ballon : elle doit se tordre, la pointe doit fouetter »
- « l'ombre est un dégradé : fais-la avec des points de grain »

Est-ce que c'est l'angle ? Les textures ? Les couleurs ? La vitesse ? La lumière ? Le cadrage ? Choisis, nomme-le, donne un chiffre quand tu peux. `critique.md` liste les défauts habituels et la phrase qui corrige chacun.

Quand la personne fait un retour, reformule-le en liste numérotée de consignes précises comme celles-ci, applique-les toutes, et vérifie chacune sur une image avant de dire que c'est fait.

### 4. Recommencer jusqu'à ce que ça plaise

À chaque tour : appliquer, regarder les images, montrer. Garde toutes les versions (`v1`, `v2`…), n'écrase jamais la précédente, pour pouvoir revenir en arrière. Ne change que ce qui a été demandé dans ce tour : aucune nouvelle idée glissée en douce.

Il faut souvent 3 à 5 tours. L'œil, ça s'apprend : au bout de quelques animations, la personne verra les défauts toute seule.

## Ce que tu livres

- Un fichier HTML par animation, autonome, sans librairie, qui boucle proprement et s'ouvre d'un double-clic.
- Les images que tu as vérifiées, si la personne les veut.
- Une ligne : ce qui a changé dans ce tour.

Si l'animation doit aller dans un logiciel de montage, enregistre-la image par image depuis l'adresse `#t=` (une capture par image, à la cadence de l'animation) plutôt que de filmer l'écran : rien ne saccade, aucune image ne saute.
