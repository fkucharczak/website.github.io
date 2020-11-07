---
layout: post
title: Notes Matlab modèles cinématiques TEP
tags: [Médecine nucléaire, Recherche]
---

## Documentation

- [Article Fayçal](/assets/docs/articles/KineticModeling/FBB_19.pdf) sur la comparaison LLS, NLS, Patlak pour la modélisation cinématique cérébrale
- [Documentation](http://www.turkupetcentre.net/petanalysis/model_compartmental_ref.html) du Turku PET Centre sur la TEP dynamique
- [Extraction de TAC à partir des données dynamiques](http://www.turkupetcentre.net/petanalysis/input_idif.html)
- **[AUC en PET](http://www.turkupetcentre.net/petanalysis/tac_auc.html)** -> voir spécifiquement la section *"AUC from time frame data"*
     - Blood time-activity curves (BTACs) are collected as mean concentrations during specified time frames.
     - The events (counts) have to be collected over the certain time “frame” to achieve acceptable count statistics, and the number of measured events are then divided by the time frame length to obtain the count rates (counts/s), which are further calibrated to radioactivity concentrations (Bq/mL) based on the measured volume and calibration coefficients.
     - If time frames are sufficiently short, we can assume that the average tracer concentration during the time frame represents the instantaneous concentration at frame middle time point
     - If concentration changes markedly during the time frame, then the midframe approximation is not valid
- [Méthode graphique de Patlak](http://www.turkupetcentre.net/petanalysis/model_mtga.html#patlak)
- [Slides PPT - modèle NLS](/assets/docs/articles/KineticModeling/DMG_DIAPOS.pdf)
- [Templates vasculaires](https://www.ucalgary.ca/miplab/downloads)
- [Occiput.io](https://github.com/spedemon/occiput)
- [APPIAN](https://www.frontiersin.org/articles/10.3389/fninf.2018.00064/full). [GitHub](https://github.com/APPIAN-PET/APPIAN)


- **Articles intéressants** :
  - [Estimation of an image derived input function with MR-defined carotid arteries in FDG-PET human studies using a novel partial volume correction method](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5453460/#!po=53.4483)

### Informations sur l'estimation de TAC avec l'activité carotidienne

- In brain PET studies the blood curve is estimated from carotid arteries or other intra-cranial blood vessels, but because of large partial volume effect and proximity of large veins the results may be poor and require a few blood samples for calibration. Different approaches like factor analysis, non-negative matrix factorization, independent component analysis (ICA), cluster analysis, and applying MRI have been used to overcome these problems.
- Mean diameters of internal carotid artery and common carotid artery are 5.11±0.87 mm and 6.52±0.98 mm in men, and 4.66±0.78 mm and 6.10±0.80 mm in women (Krejza et al., 2006).

## Divers points débattus

- Les valeurs des pixels enregistrées dans les données DICOM semblent bien être en Bq/voxel = coups/(secondes.voxel) (le temps d’acquisition par volume est donc déjà pris en compte). Par exemple, sur la série échantillonnée toutes les minutes, un voxel dans le striatum G est autour de 6500 entre la 4° et 5° minute, et dans celle échantillonnée toutes les 5’, dans le premier volume, on trouve 5000 dans les 5 premières minutes (un peu moins car la 1° partie de l’acquisition, avant la 4° minute, a moins d’activité).
Il ne faut donc pas pondérer par la durée d’acquisition et garder le signal DICOM tel quel en Bq/voxel.

## Tests

<p align="center">
  <img src="/assets/img/recherche/activity_vs_time.png" style="width:70%"/>
  <br>
    <em>Activité moyenne par volume 3D en fonction du temps d'acquisition en minutes</em>
</p>

<p align="center">
  <img src="/assets/img/recherche/activity_vs_time_normalise.png" style="width:70%"/>
  <br>
    <em>Activité moyenne par volume 3D en fonction du temps d'acquisition en minutes si on normalise l'activité par la durée d'acquisition de la séquence</em>
</p>


## Time-activity curve (TAC) input

<p align="center">
  <img src="/assets/img/recherche/T2_tac.png" style="width:70%"/>
  <br>
    <em>Coupes de T2 avec entrées carotidiennes</em>
</p>

Coordonnées d'une portion coronale de carotide interne.<br>
- **CI gauche centrée en (84,139,43)**
- **CI droite centrée en (104,139,43)**

### Essais de tracé de TAC

Si on prend une ROI centrée sur la carotide gauche par exemple, avec une ROI de +/- 2 dans toutes les dimensions on obtient une TAC comme celle présentée à gauche dans la figure suivante.

<div>
    <img src="/assets/img/recherche/TAC_ss_norm.png" style="width:49%">
    <img src="/assets/img/recherche/AUC_nn_norm.png" style="width:49%">
</div>
<p align="center">
    <br>
    <em>Série 10 en vue coronale avec ROI en noir (G).<br> TAC associée sans normalisation de la durée d'acquisition (C). AUC = intégration de 0 à t sur la même ROI (D) </em>
</p>
^
<div>
    <img src="/assets/img/recherche/AN.png" style="width:49%">
    <img src="/assets/img/recherche/AUC.png" style="width:49%">
</div>
<p align="center">
    <br>
    <em>TAC normalisée par durée de la série à (G). AUC = intégration de 0 à t sur la même ROI (D). </em>
</p>



Ci-dessous, une vue de la même coupe coronale pour trois différentes séries temporelles. Le carré noir correspond à une coupe du volume utilisé pour le calcul de la TAC.

<div>
    <img src="/assets/img/recherche/8.png" style="width:33%">
    <img src="/assets/img/recherche/15.png" style="width:33%">
    <img src="/assets/img/recherche/29.png" style="width:33%">
</div>
<p align="center">
    <br>
    <em>Série 8, 15 et 29 avec la même échelle de couleur [0, 10k]. </em>
</p>

## Logiciel développé

### Première version : données normalisées par la durée d'acquisition

<p align="center">
  <img src="/assets/img/recherche/logiciel_print1.png" style="width:100%"/>
  <br>
    <em>Exemple du logiciel DynaPET développé sous Matlab</em>
</p>

### Seconde version

<p align="center">
  <img src="/assets/img/recherche/logiciel_print2.png" style="width:100%"/>
  <br>
    <em>Nouvelle version avec gestion des données d'entrée brutes et du recalage</em>
</p>

## Templates

- Lien sur site de [McGill](http://www.bic.mni.mcgill.ca/ServicesAtlases/ICBM152NLin2009)

## Analyse compartimentale Yale

- [Lien](https://tauruspet.med.yale.edu/staff/edm42/chapters/kinetic-modeling-chapter-23-wernick-book.pdf)
^
- $$C_a$$ : measurement of blood samples drawn during a PET scan
- $$C_t$$ : radioactivity concen- tration that is measured in a given tissue region
  - $$C (t) = K_1 \int_0^{t} C_a(x) exp[–k_2(t – x)]dx$$
^
- $$Cp*(t)$$ (in nCi/ml plasma) represents the concentration of [18F]FDG measured in the arterial plasma t minutes after its injection into the venous blood
- $$Cm*(t)$$ concentration of products of [18F]FDG metabolism in the tissue
- $$Ci*(t)$$ total concentration of activity in the tissue

## Analyse compartimentale FBB

- $$\Delta_n = [10,10,10,10,10,10,10,10,10,10,10,10,30,30,30,30,30,30,60,60,60,60,60,300,300,300,300,300,300]$$
- $$t_n = [5,15,25,35,45,55,65,75,85,95,105,115,135,165,195,225,255,285,330,390,450,510,570,750,1050,1350,1650,1950,2250]$$
- $$\overline{C_p}(t_n) = \frac{\int_{t_n -\Delta_n/2}^{t_n +\Delta_n/2}C_p(t)dt}{\Delta_n}$$ correspondant à la concentration plasmatique artérielle de $$^{18}$$F-FDG.
- $$\overline{C_c}(t_n) = \frac{\int_{t_n -\Delta_n/2}^{t_n +\Delta_n/2}C_c(t)dt}{\Delta_n}$$ correspondant à la concentration de tissus cérébral de $$^{18}$$F-FDG.

### Expression graphique de Patlak

- $$\frac{C_c(t)}{C_p(t)} = K_i\frac{\int_{0}^{t}C_p(\tau)d\tau}{C_p(t)} + \frac{K_1k_2}{(k_2 + k_3)^2}$$
- On trace le rapport $$\frac{C_c(t)}{C_p(t)}$$ en fonction de $$\frac{\int_{0}^{t}C_p(\tau)d\tau}{C_p(t)}$$

### Illustration : Pat_001_DESY68

<p align="center">
  <img src="/assets/img/recherche/TAC.png" style="width:70%">
  <br>
    <em>TAC brute obtenue en moyennant les TAC D et G issues de la partie pétreuse de la carotide interne</em>
</p>

^
<div>
    <img src="/assets/img/recherche/Coupe.png" style="width:49%">
    <img src="/assets/img/recherche/Ki_patlak.png" style="width:49%">
</div>
<p align="center">
    <br>
    <em> Illustration de la méthode de Patlak pour le voxel (47,83,64) correspondant à celui pointé sur l'image de gauche. </em>
</p>
^
<p align="center">
  <img src="/assets/img/recherche/coupe_Ki.png" style="width:70%">
  <br>
    <em>Coupe de Ki correspondante</em>
</p>
