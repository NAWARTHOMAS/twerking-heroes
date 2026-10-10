# Twerking Heroes

Jeu de rythme : on glisse son téléphone dans sa poche arrière et on twerke sur chaque BOUM de la basse 808. L'accéléromètre du téléphone détecte chaque coup de hanche et note le timing (Parfait / Bien / Limite / Raté).

Tout tient dans `index.html` : la musique est synthétisée en direct. Trois bibliothèques sont chargées depuis jsDelivr : Three.js pour la scène 3D, PeerJS pour la connexion télé ↔ téléphones et qrcode-generator pour le QR code.

La partie se joue en 3D : des pontons en bois partent vers un coucher de soleil, avec des îlots à palmiers. Une case « Graphismes 3D » sur l’accueil permet de revenir à la version 2D si l’appareil est trop lent ; le jeu repasse aussi en 2D tout seul si la 3D est indisponible.

## Les mouvements

Le téléphone se met dans la poche arrière, **écran vers l'extérieur et à l'endroit** (le haut du téléphone vers le haut). Chaque note a son son, pour jouer sans regarder l'écran :

- **BOUM** (la basse) : twerk ;
- **tom grave**, à gauche dans les enceintes : hanche à gauche ;
- **tchak aigu**, à droite : hanche à droite.

Dans cette position, l'axe horizontal du téléphone pointe vers la droite du joueur. Le jeu lit la gravité pour corriger tout seul un téléphone rangé à l'envers et la convention inversée des iPhone. Une note gauche ou droite faite du mauvais côté compte « Limite ». La case « Mouvements gauche / droite » permet de ne garder que les BOUM (mode débutant), et « Inverser gauche et droite » sert de secours si un téléphone se trompe de côté.

## Les trois modes

- **Sur la télé du salon** : la télé (ou l'ordi branché dessus) affiche les pistes et joue la musique. Jusqu'à 4 téléphones la rejoignent avec un code à 4 chiffres ou en scannant le QR code, puis partent dans les poches. Les scores s'affichent sur la télé, et chaque téléphone reçoit son classement.
- **Manette** : le téléphone rejoint la télé.
- **Solo** : tout se passe sur un seul téléphone, sans télé.

## Mettre le jeu en ligne (obligatoire pour jouer)

Les téléphones n'ont accès au capteur de mouvement que sur une page en **HTTPS**. Ce dossier est prêt à être publié tel quel avec **GitHub Pages** (gratuit pour un dépôt public) :

1. Sur GitHub, crée un dépôt **public** vide nommé `twerking-heroes` (sans README).
2. Mets-y le contenu de ce dossier, à la racine (`index.html`, les icônes, `manifest.webmanifest`, `.nojekyll`).
3. Dans le dépôt : **Settings → Pages → Build and deployment → Source : Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**.
4. Une à deux minutes plus tard, le jeu est en ligne sur `https://<ton-pseudo>.github.io/twerking-heroes/`. Chaque modification poussée sur `main` le republie.

Ensuite, ouvre cette adresse sur la télé (navigateur de la télé, ordi branché en HDMI, ou onglet Chrome « caster » vers la télé) et sur chaque téléphone. Sur le téléphone, « Ajouter à l'écran d'accueil » installe le jeu avec son icône, comme une appli.

## Comment ça marche

- La télé et les téléphones se parlent en direct (WebRTC). Le serveur public de PeerJS sert seulement à les mettre en relation au départ.
- Chaque téléphone synchronise son horloge avec celle de la télé (échanges ping/pong). Un twerk est donc noté au moment où il a eu lieu, et non au moment où il arrive par le réseau.
- Sur iPhone, le bouton « Rejoindre » demande l'accès « Mouvement et orientation ».
- Pour tester en local sans Internet : `?broker=hote:port` pointe vers un serveur PeerJS local.
