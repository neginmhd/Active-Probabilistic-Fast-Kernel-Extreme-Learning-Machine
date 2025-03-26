README - Active Probabilistic Fast Kernel Extreme Learning Machine

=========================
Project Overview
=========================

This project implements an ultra-efficient forecasting model to predict bridge deterioration conditions using historical data from the National Bridge Inventory (NBI). The model, based on an Active Probabilistic Fast Kernel Extreme Learning Machine, is designed to work with a small training dataset and deliver high predictive performance through an active learning strategy.

=========================
Feature Descriptions
=========================

This section documents the explanatory variables used in the model to predict bridge condition for the following year.
The response variable/target is `NEXT_LOWEST_RATING`, which indicates the condition rating for the next year.

Explanatory Variables:

- Installation_Year              : Year the bridge was built or installed
- ADT_029                        : Average daily traffic
- MAX_SPAN_LEN_MT_048           : Maximum span length (in meters)
- IMP_LEN_MT_076                : Length of structure improvement (in meters)
- DECK_AREA                     : Deck area (in square meters)
- TIC (Time in condition rating): Years in current condition rating
- STRUCTURE_KIND_043A           : Structural material (e.g., concrete, steel)
- STRUCTURE_TYPE_043B           : Structural system (e.g., girder, slab, truss)
- DECK_STRUCTURE_TYPE_107       : Deck system type
- LOWEST_RATING                 : Current condition rating of the bridge

Target Variable:

- NEXT_LOWEST_RATING            : Bridge condition rating in the following year

For additional variables and full descriptions, refer to the NBI Coding Guide:
https://www.fhwa.dot.gov/bridge/mtguide.pdf

=========================
Auxiliary Variables
=========================

These variables are not used as model predictors but serve as auxiliary features to guide sample selection and clustering:

- STRUCTURE_NUMBER_008          : A unique ID for each bridge, defined by state agencies and consistent across records
- hierarchical_cluster          : Cluster label assigned to each bridge for diversity sampling
- CollectionYear                : The year the record was collected

=========================
Model Highlights
=========================

- Combines a Fast Kernel Extreme Learning Machine (ELM) with an active learning mechanism
- Uses entropy-based sampling and hierarchical clustering to select the most informative and diverse samples
- Provides accurate, probabilistic ordinal predictions
- Achieves high performance (RPS = 0.01) using data from only 70 bridges
