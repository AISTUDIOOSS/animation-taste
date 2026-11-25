# Le goût

Deux styles, tirés de vraies animations validées après plusieurs tours de retours. Si la personne a donné sa propre référence, sa référence passe avant : prends ici seulement le rendu, le grain et le mouvement qui ne la contredisent pas.

Les règles « Toujours » valent pour les deux styles.

---

## Toujours

### Rendu
- **Dessiné image par image, pas lisse.** L'animation tourne à 12 images par seconde (8 pour une vidéo insérée dans une animation), pas à 60. Calcule l'image à partir de son numéro : `fi = floor(temps × FPS)`, puis `t = fi / FPS`. Ça donne le côté fait main. Le 60 i/s lisse, c'est le look « SaaS ».
- **Une boucle parfaite.** Tout ce qui bouge fait un nombre entier de tours sur la durée de la boucle (par exemple 6 s) : `phase = 2π × k × t / T`, avec `k` entier. La dernière image raccorde avec la première, sans saut.
- **Le hasard est fixé.** Un générateur à graine (même graine = mêmes valeurs), jamais `Math.random()` à chaque image : la boucle est identique à chaque passage, et ce qui doit trembler tremble parce que tu changes la graine, pas par accident.
- **Pas de zoom, pas de pulsation, pas de fondu.** Rien ne grossit puis rétrécit en battant, aucun élément n'apparaît en fondu : il est là dès sa première image. La caméra ne zoome pas.
- **Rien sur les bords.** Ce qui compte est centré, loin des bords de l'image (Instagram coupe en haut, en bas et sur la grille du profil).

### Couleur
- **Palette courte** : 5 à 7 couleurs, écrites en hex en haut du fichier, une seule couleur d'accent qui claque.
- **Des aplats, pas des dégradés.** Un objet = une couleur pleine. La lumière et l'ombre se font avec du grain (voir plus bas), jamais avec un dégradé lisse. Seule exception : un vignettage très léger dans les coins.
- **Pas de blanc pur, pas de noir pur** dans le dessin : crème (`#f6e7c4`) au lieu du blanc, violet très sombre (`#0c0520`) au lieu du noir.

### Grain
Le grain, c'est ce qui fait « imprimé », « vrai ». Trois couches :
1. **Grain de matière**, dans les formes : des petits carrés de 2 à 5 px, posés en nombre dans l'objet (sable, tronc, bûche), d'une teinte un peu plus claire ou plus sombre que l'aplat.
2. **Grain de lumière**, à la place des dégradés : pour éclairer le côté d'un objet, découpe l'objet et sème des carrés de la couleur de la lumière, plus serrés près de la source et de plus en plus rares en s'éloignant (densité qui suit une courbe en puissance, par exemple `u = hasard^2`).
3. **Grain d'impression**, sur toute l'image, retiré à chaque image : environ 2 600 carrés blancs de 3 px à 5 % d'opacité et 2 600 carrés noirs à 9 %, nouvelle graine à chaque image. L'image vit même quand rien ne bouge.

### Lumière
- **Une source qui éclaire vraiment.** Le feu (ou la lampe, l'écran…) éclaire le côté des objets tourné vers lui : pierres, tronc, herbes, avec un liseré chaud sur le bord côté source, et un reflet sur l'eau ou le sol.
- **Deux lumières maximum** (par exemple la lune froide au-dessus, le feu chaud en dessous), et chacune reste de son côté.
- **Ramener l'œil** : un seul point focal, les coins un peu assombris.

### Formes de la nature
- **Jamais de bord droit.** Une mer, une vague, un nuage, une colline : bords irréguliers, en lobes, qui bougent un peu.
- **Les choses en couches** : l'écume = pellicule d'eau devant, bande d'écume, voile plus pâle derrière, dentelle qui traîne. Une seule couche fait plat.
- **Les petits détails qui bougent** : herbes qui se balancent, étoiles qui scintillent à des rythmes différents, houle en petits traits courbes.

---

## Style 1 : le feu de camp (dessin plat et granuleux)

Exemple complet : `exemples/feu-dirige.html`. Lis son code avant d'écrire une flamme, une eau ou une lumière.

### La flamme
C'est ce que tout le monde rate. Une flamme ratée **gonfle** (un ovale qui grossit et rétrécit). Une flamme réussie **se tord**.
- Trace d'abord une **ligne centrale** qui ondule de bas en haut : l'onde monte, et plus on va vers le haut, plus elle s'écarte (la pointe fouette).
- Pose ensuite **l'épaisseur de chaque côté** de cette ligne : large à la base, fine à la pointe, avec une petite respiration.
- **Trois couches** emboîtées : extérieure orange (`#ff7a1f`), milieu jaune (`#ffd23f`), cœur rouge (`#ff3f4a`) découpé dans le jaune, chacune avec sa phase et son inclinaison. Plusieurs langues de flamme qui ne bougent pas ensemble.
- Une petite **rafale** : toutes les flammes penchent un peu du même côté, de temps en temps.
- **Flammèches** : une pointe se détache, monte en tournant et rapetisse.
- **Braises** : petits losanges jaunes puis orange, qui montent en se balançant et disparaissent en haut.
- La hauteur varie d'à peine 7 %. Jamais de « pouf ».

### Le décor
- Décor fixe peint une seule fois dans une image à part (ciel, lune, sable), puis seulement ce qui bouge par-dessus à chaque image.
- Nuit en violets (`#1b0e40` ciel, `#22176a` mer, `#2a1540` sable), lune crème avec cratères en grain, étoiles en petits carrés + quelques grandes étoiles à 4 branches.
- Reflet de la lune sur l'eau : des taches irrégulières qui s'élargissent vers le rivage, pas une bande droite.

### Ce qui distingue le premier jet de la version dirigée
| Premier jet (moche) | Dirigé (studio) |
|---|---|
| Scène figée, seul le feu respire | Tout vit un peu : eau, herbes, étoiles, braises |
| Flamme en ovale qui gonfle | Flamme qui se tord, pointe qui fouette |
| Dégradés lisses | Aplats + grain de lumière |
| Mer à bord droit, écume blanche | Bords en lobes, écume crème en couches |
| Image propre, numérique | Grain d'impression sur toute l'image |
| 60 images par seconde | 12 images par seconde, dessiné image par image |

---

## Style 2 : collage papier (pour les animations d'un Reel face caméra)

Pour les petites animations qui illustrent ce que dit la personne à l'écran.
- **Fond blanc** (ou l'animation posée au-dessus de la tête de la personne). Pas d'écran coupé en deux, pas de « petite fenêtre » d'appli façon SaaS.
- **Objets découpés** comme du papier : une vraie photo ou image de l'objet, détourée, avec une **bordure blanche de papier** et un **vrai morceau de scotch** pour la tenir. Objets **de face**, bien droits : rien n'est penché.
- **Une étoile orange** (`#FD5700`, une vingtaine à trente pointes) derrière le mot ou l'objet important : elle part de 0, grandit plus grande que sa boîte en ralentissant, et tourne doucement. Une seule par animation.
- **Un curseur vintage blanc** quand il faut montrer un clic.
- **Aucun texte écrit dans l'animation** : les sous-titres s'en chargent. Pas d'étiquettes, pas de pastilles.
- Une **vidéo insérée** dans une animation est passée à **8 images par seconde** et apparaît pleine dès sa première image.
- Quand une animation reprend une vraie interface (Claude, un logiciel), elle est **identique à la vraie**, avec un vrai texte, pas du faux texte.
- Centré, gros (65 à 80 % de la largeur), rien qui se touche.
