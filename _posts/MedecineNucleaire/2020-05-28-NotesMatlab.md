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

Si on prend une ROI centrée sur la carotide gauche par exemple, avec une ROI de +/- 2 dans toutes les dimensions comme sur l'image ci-dessous à gauche, on obtient une TAC comme celle présentée à droite.

<div class="row">
  <div class="column">
    <img src="/assets/img/recherche/serie10.png" style="width:90%">
  </div>
  <div class="column">
    <img src="/assets/img/recherche/TAC_ss_norm.png" style="width:100%">
  </div>
</div>
<p align="center">
    <br>
    <em>Série 10 en vue coronale avec ROI en noir (G). TAC associée dans normalisation de la durée d'acquisition (D). </em>
</p>

^
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
