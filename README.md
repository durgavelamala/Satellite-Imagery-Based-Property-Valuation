# Satellite-Based Property Price Prediction

## Overview
This project focuses on predicting property prices by combining traditional
tabular real estate data with satellite imagery. The objective is to evaluate
whether visual context extracted from satellite images can enhance property
price prediction compared to tabular-only models.

---

## Repository Contents
├── 22323041_Code.ipynb
├── README.md
├── report.pdf
├── outputs/
│ └── 22323041_final.csv


---

## Dataset Description

### Tabular Data
The tabular dataset contains structured property information such as:
- Location (latitude, longitude, zipcode)
- Structural attributes (bedrooms, bathrooms, living area, grade, condition)
- Neighborhood characteristics

The target variable is property price. A log transformation is applied during
modeling to improve regression performance.

### Satellite Images
Satellite images were programmatically acquired using the Mapbox Static Images
API based on latitude and longitude coordinates. Due to API rate limits and time
constraints, images were collected for a representative random subset of 500
properties. These images capture neighborhood-level visual context such as
buildings, roads, greenery, and water bodies.

Note: The Mapbox access token used for satellite image retrieval has been
removed from the code for security reasons.

---

## Methodology

### Models Implemented
- **Baseline Model (Ridge Regression)**  
  Provides a simple reference for performance comparison.

- **XGBoost (Tabular Only)**  
  A tree-based ensemble model trained on tabular features. Hyperparameter tuning
  was performed to optimize performance.

- **Multimodal Model (Tabular + Satellite Images)**  
  Combines tabular features with satellite image embeddings extracted using a
  CNN (ResNet50). Grad-CAM is used for visual explainability.

---

## Explainability
Grad-CAM visualizations are generated for selected satellite images to highlight
regions that contribute most to price predictions. These visualizations provide
insight into how neighborhood characteristics influence the model’s decisions.

---

## Results Summary

| Model | RMSE (log-price) | R² |
|------|------------------|----|
| Baseline (Ridge) | 0.183 | 0.879 |
| XGBoost (Default) | 0.190 | 0.870 |
| XGBoost (Tuned) | **0.178** | **0.885** |
| Multimodal (Tabular + Images) | 0.369 | 0.478 |

---

## Final Predictions
Final predictions were generated using the tuned XGBoost model and saved in the
required CSV format:

outputs/price_predictions.csv

yaml
Copy code

Duplicate property IDs in the test dataset were handled by retaining the first
occurrence to ensure one prediction per property.

---

## How to Run
1. Open the Jupyter notebook:
```bash
jupyter notebook notebook.ipynb
Run all cells from top to bottom.

Environment & Dependencies
The project was developed using Anaconda with a TensorFlow-enabled environment
(tf_env).

Required libraries:

Python 3.x

pandas, numpy

scikit-learn

xgboost

tensorflow / keras

matplotlib, seaborn

pillow, opencv-python

Conclusion
This project demonstrates that tuned tree-based models perform strongly on
structured real estate data, while multimodal learning with satellite imagery
adds interpretability and future potential when larger image datasets are
available.

Author
Velamala Pujitha
