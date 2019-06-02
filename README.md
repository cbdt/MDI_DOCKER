Nous avions une version fonctionnelle du TP opencv mais celle-ci était sur un seul dockerfile.
Nous avons donc decider de decouper le dockerfile en deux parties, une pour la compilation d'opencv et l'autre pour l'éxécution de l'application. 
Seulement nous avons rencontré un probème lors de l'étape build de la seconde image. En effet celle-ci a besoin des fichiers compilés lors du build d'opencv pour se créer. Il a donc fallu créer un volume dans lequel on enregistre l'ensemble des données de build d'openCV. Cependant, vu que nous ne pouvons pas utiliser ce volume lors du build de la seconde image nous sommes obligé de passer par un container intermédiaire pour copier le contenu du volume sur la machine locale.
Toute ces lignes de commandes sont précisés dans le dockerfile à la racine du TP_opencv (celui du build).

La partie du TP sur OPENCV ne fonctionne pas à cause des dépendances d'OpenCV, notamment libjpeg, il y en effet un problème lors de l'éxécution du jar de l'application.