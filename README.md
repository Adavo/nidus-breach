# Nidus Breach

Jeu d'action coopératif en vue de dessus, dans le navigateur. Vous incarnez un soldat, vos frères d'armes sont
contrôlés par l'IA, et en face il y a des araignées extraterrestres. Brisez le nid, ou tenez la forteresse.

Tout le jeu tient dans un seul fichier, [`index.html`](index.html) : pas de build, pas de dépendance à installer.
Les graphismes sont dessinés en code.

## Jouer

Ouvrir `index.html` dans un navigateur récent (ou le servir en HTTPS, voir plus bas).

| Action | Commande |
|---|---|
| Se déplacer | `Z` `Q` `S` `D` |
| Viser | souris |
| Tirer | clic gauche |
| Grenade (zone) ; roquette si on est dans le mécha | clic droit |
| Ouvrir/fermer une porte, ordre aux alliés à moins de 3 cases, monter/descendre du mécha | `E` |
| Recommencer / changer de mode (hôte ou solo) | `Entrée` / `M` |
| Pause (volumes, quitter la partie) | `Échap` |
| Couper / remettre le son | `N` (ou le bouton « Son » du menu) |

### Son
Musique et bruitages sont synthétisés en direct (WebAudio), sans aucun fichier audio : un morceau pour le menu et un par monde,
qui devient plus intense quand les aliens approchent. Le son démarre au premier clic ou à la première touche (règle des navigateurs).
En coop, l'invité entend les bruitages de l'hôte.

### Sur mobile
Les commandes tactiles apparaissent automatiquement (écran tactile) : joysticks flottants (le socle apparaît sous le doigt) : à gauche pour se déplacer, à droite pour
orienter, boutons **TIRER**, **GREN.** (grenade) et **E** (porte / ordres aux alliés), et **☰** pour ouvrir le menu pause.
Mieux vaut jouer en mode paysage. Ajouter `?touch=1` à l'adresse force l'affichage des commandes tactiles.

### Modes
- **Chasse à la reine** : tuer la reine des aliens dans son nid avant la fin du temps imparti (7 minutes). On réapparaît à la base à l'infini : seul le temps joue contre nous.
- **Survie** : tenir la forteresse 3 minutes. Le **réacteur** de la base nous fait réapparaître (6 s après la mort) ; s'il est détruit, plus de retour : quand tous les joueurs sont tombés, c'est perdu.

Dans les deux modes, des **nids** (petits dômes bruns répartis sur la carte, visibles sur la mini-carte) pondent des aliens en continu ; on peut les détruire (balles, flammes, explosions).
Un tir suffit à tuer un alien ordinaire ou un allié ; les brutes et la reine sont plus résistantes. Les aliens et les alliés visent et se déplacent de façon un peu approximative.

### Jour / nuit
À la création d'une partie : **Nuit** (obscurité, vue courte) ou **Jour** (pas d'obscurité). L'hôte choisit pour les deux joueurs. Le zoom du jour se règle avec la constante `DAY_ZOOM` dans `index.html` (1 = normal, 0,8 = vue plus large).

### Pause
`Échap` (ou ☰ sur mobile) ouvre le menu pause : volume de la musique et des effets (mémorisés), son coupé/activé, reprendre ou quitter la partie.
En solo le jeu est figé ; en multijoueur la partie **continue** pendant que le menu est ouvert (votre soldat reste immobile).

### Mondes
Avant-poste Kappa, Marais de Vesper, Canyon Rouge, Ruines du Givre.

### Campagne (missions 1 et 2 jouables, la suite arrive)
Le scénario complet est dans [`SCENARIO.txt`](SCENARIO.txt). Menu **Solo** (ou **Multi → Créer une partie**) → **Campagne**.
- **Introduction** : cinématique d'un vaisseau qui arrive sur la planète (dessinée en code, passable ; « Revoir l'introduction » dans l'écran des missions).
- **Briefing / débriefing** façon *Metal Gear Solid* : écran de codec plein écran, deux portraits face à face, texte qui s'écrit (clic, `Entrée` ou `Espace` pour continuer, `Échap` pour passer). En mission, des répliques radio s'affichent dans une bande discrète, sans pause.
- **Mission 1 – Atterrissage** : détruire les 3 nids autour de la colonie. **Mission 2 – Relais radio** : tenir 4 minutes dans la zone du relais pendant qu'il émet (la transmission s'arrête si plus personne n'est dans la zone ; le relais détruit = échec).
- **Rangs** : **or** si aucune mort, **argent** jusqu'à 3 morts (les deux joueurs cumulés), **bronze** au-delà. Le meilleur rang de chaque mission est mémorisé (navigateur) et chaque mission terminée peut être rejouée depuis l'écran de sélection. Une mission s'ouvre quand la précédente est réussie (`?unlock=1` dans l'adresse ouvre tout, pour tester).
- En ligne, l'hôte choisit la mission ; les deux joueurs voient l'intro et le briefing, la mission démarre quand les deux sont prêts.

### Soldats : homme ou femme
Dans les menus Solo et Créer une partie, le **joueur 1** choisit son design (homme ou femme). Le **joueur 2 prend toujours l'autre** : il n'y a jamais deux femmes (ni deux hommes), c'est le joueur 1 qui décide. Les portraits de Rook et Lyra suivent ce choix.

### Langues
Français et anglais : bouton **FR / EN** en haut à gauche du menu (le choix est mémorisé, la langue du navigateur sert de valeur par défaut). Les textes sont dans l'objet `STR` de `index.html` ; chaque joueur voit le jeu dans sa propre langue, même en ligne.

### Armes
Pistolet (munitions infinies, arme par défaut), mitraillette, fusil à pompe, lance-flammes, lance-roquettes.
On équipe une arme en la ramassant ; l'ancienne tombe au sol. Sans munitions, on retombe sur le pistolet.

### Bonus
Munitions, armes, grenades, soins, bombardement, et trois bonus de rang qui sont activés au ramassage :
- **Bronze (convoi)** : 5 soldats arrivent à la base.
- **Argent (hélico)** : un hélicoptère traverse l'écran en tirant sur les aliens et largue 3 soldats en parachute.
- **Or (mécha)** : un mécha est livré à la base. `E` à côté pour y monter : deux fois plus résistant qu'un soldat, canons jumelés (clic gauche) et 5 roquettes, sans recharge (clic droit). `E` pour en descendre (il reste sur place) ; s'il est détruit, le pilote survit. Le mécha est rare (au moins 2 min 30 entre deux).

Les renforts (alliés) n'arrivent plus que par ces bonus bronze et argent. Les caisses de munitions et les armes au sol sont plafonnées.

### Alliés
`E` près d'eux fait défiler leurs ordres : par défaut (avancer prudemment, ou garder la forteresse en survie),
nous suivre, tenir la position.

## Multijoueur (2 joueurs)

Menu **Multi** → *Créer une partie* (code à 5 caractères) ou *Rejoindre une partie* (saisir le code).

- Connexion navigateur à navigateur (WebRTC) via [PeerJS](https://peerjs.com/) ; le service public de PeerJS
  ne sert qu'à la mise en relation. **Internet est nécessaire** pour le multi.
- Sur l'écran d'attente, **toucher ou cliquer le code le copie** dans le presse-papiers pour l'envoyer à l'autre joueur.
- L'hôte fait tourner toute la simulation ; l'invité envoie ses touches et reçoit l'état du jeu.
- Pour jouer à distance, la page doit être servie en **HTTPS** (GitHub Pages, Netlify, Cloudflare Pages…).
- Certains réseaux (Wi-Fi d'entreprise, certaines 4G) bloquent la connexion directe : il faudrait alors un relais TURN.

## Mises à jour et cache
Pour que les joueurs chargent toujours la dernière version : la page demande au navigateur de ne pas la mettre en cache, et au chargement
elle compare son code avec la version en ligne (récupérée sans cache) ; si elles diffèrent, elle se recharge une fois avec une adresse neuve.
Le fichier `_headers` demande en plus `Cache-Control: no-cache` sur Netlify et Cloudflare Pages (GitHub Pages l'ignore : c'est la vérification
au chargement qui garantit la mise à jour, avec au pire un rechargement automatique).

## État du projet

Prototype. La campagne compte 10 missions au scénario, dont les 2 premières sont jouables ; les suivantes s'affichent « Bientôt ».
