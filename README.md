# POC
Dataset :
Mes données ont été généré par moi-même, j’ai essayé de générer une série temporelle sans bruit ni outliers ensuite j’ai ajouté ces derniers pour évaluer leurs impacts dans les analyses. Quant aux valeurs aberrantes, je les ai fixés pour une amplitude importante de 20 pour qu’ils apparaissent comme des points de changements pour évaluer mon algorithme d’une façon robuste. Ainsi, j’ai ajouté du bruit à mon signal de base en jouant avec des moyennes et des écart-types. Expliquons la méthode de génération :
    •	Nombre de Segments (n_segments) : Chaque segment représente une période distincte.
    •	Longueur de chaque Segment (segment_length) : Cela détermine combien de points de données composent chaque segment.
    •	Moyennes et Écarts Types (means, std_dev) : Pour chaque segment, j’ai défini des moyennes et des écarts types différents pour simuler le bruit dans le signal.
    •	Nombre et Magnitude des Valeurs Aberrantes (n_outliers, outlier_magnitude) : Ces valeurs aberrantes sont essentielles pour tester la robustesse des algorithmes 
      d'analyse de séries temporelle comme j’avais mentionné au-dessus.
En utilisant np.random.normal, j’ai généré des données pour chaque segment. Ce choix est motivé par le fait que beaucoup de phénomènes naturels et économiques suivent une distribution normale.
Insertion Aléatoire des outliers : J'ai inséré ces outliers à des positions aléatoires pour imiter les anomalies réelles dans les données.
   •	DataFrame : Pour une manipulation facile, j’ai converti les données générées en DataFrame.
   •	Enregistrement : Enregistrer les données en format CSV pour une utilisation ultérieure.
J’ai tracé mes data pour comprendre les données générées pour avoir un aperçu visuel de leurs structures, y compris les valeurs aberrantes.

Métrique : 

Ces métriques sont pour but de créer un environnement de test contrôlé et complexe, qui me permet d'évaluer les capacités de mon approche d'analyse de séries temporelle et de modéliser des situations réalistes. Cela va m’aider à déduire que les méthodes développées sont non seulement théoriquement solides mais aussi pratiquement efficaces et robustes face aux défis des données réelles.
J’ai considéré le nombre de segments, les points de changement, La fréquence et l'amplitude des outliers pour évaluer la robustesse de l’algorithme au traitement des séries temporelles.
J’ai incorporé le bruit (mean bruit, écart types) pour Simuler dans des Conditions Réalistes.

L’algorithme de détéction de points de changements : R-FPOP:

Pour appliquer l’algorithme sur la série temporelle, il faut prendre des précautions comme le choix de certains paramètres qui peuvent le pénaliser ou bien réduire de sa robustesse notamment le paramètre de pénalité beta, son choix doit être approprié aux cas étudiés comme mentionné dans l’article, il faut que beta soit proportionnelle à log(n) même cette condition ne suffit pas, il faut jouer sur un coefficient C1, 

Le paramètre beta:

Une beta plus élevée impose une pénalité plus forte pour l'ajout de points de changement, ce qui conduit à un modèle plus simple avec moins de points de changement. Une beta plus faible permet plus facilement l'ajout de points de changement, ce qui peut conduire à un surajustement où le modèle capte trop de « bruit » en tant que changements structurels
Un choix inapproprié de beta peut soit masquer de véritables points de changement (si la pénalité est trop élevée), soit produire trop de fausses détections (si la pénalité est trop basse). Ainsi, le réglage de beta est essentiel pour obtenir des résultats fiables de l'algorithme.

Le paramètre K :

 K est défini comme un multiple de la MAD (Médiane Absolue de la Déviation) qui est souvent utilisée pour estimer la variance dans des données avec des valeurs aberrantes car elle est plus robuste que l'écart-type.
Un K bien choisi permet de trouver un équilibre entre détecter de véritables points de changement (sensibilité) et ignorer les outliers.

Cas d'Utilisation de l'algorithme :

Diagraphie de Puits et Forage : La méthode est utilisée dans la diagraphie de puits pour la détection des changements de strates rocheuses. Cela est crucial dans le forage, où une identification précise des différentes couches géologiques peut influencer les décisions de forage.

Domaine Clinique : En médecine, l'algorithme peut être appliqué pour la détection précoce de tumeurs cancéreuses. Cela pourrait permettre une identification plus rapide des changements anormaux dans les images médicales, ce qui est essentiel pour le diagnostic et le traitement du cancer.

Sécurité des Connexions Sans Fil : Dans le domaine de la sécurité informatique, la méthode trouve son application dans la détection de falsifications dans les réseaux sans fil. Elle peut être utilisée pour identifier les anomalies dans les signaux de transmission, ce qui est un aspect important de la sécurisation des connexions sans fil


