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
| Grenade (zone) | clic droit |
| Ouvrir/fermer une porte, ordre aux alliés à moins de 3 cases | `E` |
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
- **Chasse à la reine** : tuer la reine des aliens dans son nid.
- **Survie** : tenir la forteresse 150 secondes.

### Pause
`Échap` (ou ☰ sur mobile) ouvre le menu pause : volume de la musique et des effets (mémorisés), son coupé/activé, reprendre ou quitter la partie.
En solo le jeu est figé ; en multijoueur la partie **continue** pendant que le menu est ouvert (votre soldat reste immobile).

### Mondes
Avant-poste Kappa, Marais de Vesper, Canyon Rouge, Ruines du Givre.

### Armes
Pistolet (munitions infinies, arme par défaut), mitraillette, fusil à pompe, lance-flammes, lance-roquettes.
On équipe une arme en la ramassant ; l'ancienne tombe au sol. Sans munitions, on retombe sur le pistolet.

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

Prototype. La campagne n'est pas encore implémentée (bouton grisé).
