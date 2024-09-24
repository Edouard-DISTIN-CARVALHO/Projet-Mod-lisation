# Projet-Mod-lisation
UE Modélisation et Quantification HAB928B

# Sujet 1 en Statistique : La consommation alimentaire de la barge hudsonnienne

On s’intéresse à la consommation alimentaire de barges migrantes (limosa haemastica) sur un chenal de marée (“a tidal channel” en anglais), dans un système de vasières de l’Atlantique Sud en Argentine (Samborombon Bay).

**Design expérimental**
L’expérience a été menée sur 19 jours non consécutifs, divisés en trois périodes non consécutives. En se basant
sur le plumage et la période de l’année, les barges ont été classées en “oiseaux en préparation de migration”
(“fin d’été - automne”) et “oiseaux non en préparation de migration”. Ce deuxième groupe peut être de
nouveau divisé en “printemps - début d’été” et “hiver”. Les mesures ont été faites pendant des périodes de
basses eaux sur au moins deux jours par mois, durant 15 mois consécutifs. Pour chaque jour, entre 7 et 19
observations étaient faites. Les données sont des données de Ieno, non publiées.

**Variables mesurées**
La variable d’intérêt est **IntakeRate** qui est la quantité de matière sèche ingérée par seconde de consommation
(Ash free dried prey weight per second of feeding) en milligrammes. L’instant d’ingestion Time est également
noté (exprimé en heures avant et après la marée basse). Nous avons également le sexe de l’oiseau Sex
(unknown, male ou female), ainsi que la période d’observation Period: septembre à janvier (Summer, on est
dans l’hémisphère sud), février à avril (LSummer.Fall) ou mai à août (Winter). Cette variable correspond à la
classification des oiseaux expliquée précédemment. Enfin, nous disposons de l’identifiant du jour échantillonné
ID.

### Chargement et mise en forme des données
```{r données}
limosa <- read.table(file = "limosa.txt", header = TRUE, sep = "\t")
str(limosa)
limosa$fID <- factor(limosa$ID)
limosa$fPeriod <- factor(limosa$Period, levels=c(0,1,2),

labels=c("Summer","LSummer.Fall","Winter"))
limosa$fSex <- factor(limosa$Sex, levels = c(0,1,2), labels=c("Unk","F","M"))
limosa$fID <- factor(limosa$ID)
```

**Objectifs**
Développer un modèle statistique pour expliquer la consommation alimentaire en fonction de la période de
migration, de l’instant d’ingestion mesuré en fonction de la marée basse, du sexe, et du jour échantillonné.
Toutes ces variables explicatives ne sont peut être pas pertinentes, nous souhaitons donc par la même occasion
répondre à la question suivante: 
**Est ce que la consommation alimentaire dépend de la période de migration, de l’instant d’ingestion mesuré en fonction de la marée basse, du sexe, du jour échantillonné et des éventuelles interactions entre ces variables?** 

**Attendus**
Votre démarche doit être entièrement expliquée et éventuellement illustrée par des figures. Le but n’est pas
de donner un modèle final, mais d’expliquer les réflexions qui ont permit d’y arriver (il n’y a pas forcément
qu’un seul bon modèle final, tout peut être argumenté).
• Commencer par une exploration des données pour les présenter et se les approprier.
• Le raisonnement de l’analyse doit être expliqué.
• Pour chaque modèle étudié: écrire l’équation du modèle et les hypothèses associées.
• Pour chaque test effectué: donner les hypothèses et interpréter le résultat.
• Il ne doit pas y avoir de sortie R non commentée.
• Faire le tri entre ce qui doit être présenté ou pas. Un rapport “catalogue” de modèles et de sorties R
serait indigeste. En effet, certains modèles peuvent être étudiés mais leurs résultats non présentés car
moins intéressants que ceux d’autres modèles, ou moins pertinents. Dans ce cas vous pouvez expliquer
votre réflexion et ce que vous avez obtenu, sans forcément montrer les résultats. Le plus important est
de bien faire comprendre et appuyer votre démarche.
