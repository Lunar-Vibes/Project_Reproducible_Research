
# Project: Predicting Rocket League Outcomes using Random Forest

## Team Members

- Kacper Geisshirt (443171)  
- Shagufta Shaheen (477654)  
- Zahra Eshtiaghi (476679)
- Celia Mlambo (476670)  
  
## Overview
This project aims to reproduce the research by Smithies et al. (2021), which applies Random Forest models to identify key metrics that predict match outcomes and player rankings in the esport *Rocket League*. The dataset and methodology are provided in the original study, and our main focus will be on implementing and properly tuning the models.

## Abstract
Notational analysis is widely used in traditional sports but is less explored in esports. This study analyzes over 21,000 Rocket League matches using Random Forest models to identify important performance indicators (PIs) and rank indicators (RIs).

Key findings include:
- **Performance indicators (PIs):** shots taken, shots conceded, saves made, and time spent goalside of the ball  
- **Rank indicators (RIs):** time at supersonic speed, time on the ground, shots conceded, and time goalside  

This project will reproduce these results and evaluate the effectiveness of Random Forest models, with particular focus on hyperparameter tuning and feature importance analysis.

## Instructions for reproduction

For notebooks folder:
1. Download or clone the repository locally.
2. Open the RR folder as the project root in your code editor of choice.
3. In a terminal opened at RR, run uv sync. This should install project dependencies.
4. Pick the interpreter from .venv
5. Run notebooks in which ever order, they are all independent. Warning - computation will take a LONG time.

The instructions for the analyst part are included in the Analyst Part- Zahra Eshtiaghi folder.
## Reference
Smithies, T.D., Campbell, M.J., Ramsbottom, N. et al. (2021)  
https://www.nature.com/articles/s41598-021-98879-9
