---
title: "Playlist Classification Machine"
date: 2021-11-24T16:35:35+01:00
draft: false
image: "musicpic.jpeg"
tags: ["projects"]
---

Description: Predicting the genre (class) of a playlist using audio features.

Data: Extracted from the "Spotifyr" package in R. 

**Dependent Variable:** _(Eight Genres)_  
- Rap/HipHop
- Synth
- Jazz
- Anime Openings
- Pop
- Classical Music
- Russian Turbo Polka
- Frenchcore

**Predictors:** _(Independent Variables/Features)_
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Tempo
- Liveness
- Mode
- Danceability
- Energy
- Key
- Valence
- Track Popularity

**Methods and Models employed:**

Linear Discriminant Analysis (LDA) and Leave One Out Cross-Validation (LOOCV)

**Model Evaluation:**

Sensitivity, Specificity, Accuracy, Precision, Negative Predictive Value, and Accuracy 

**Data Summary:**
- 500 songs
- 12 predictors
- 8 genres

**Results:**

Overall Model Accuracy = 76 % 
