# PM10 Air Quality Prediction

## Project Description
This project predicts PM10 air pollution levels in Zurich using historical weather data (temperature, humidity, wind speed). It compares regression and classification models to determine the best approach for forecasting air quality and deploys the final model as a Gradio web app on Hugging Face Spaces.

## Results
Regression using a Random Forest Regressor yielded the most interpretable and accurate results. Classification models had high overall accuracy but failed to predict rare high-pollution events. The final model was deployed with a user-friendly interface that allows users to input weather data and instantly receive a PM10 prediction.

### Name & URL
| Name         | URL |
|--------------|-----|
| Huggingface  | [Huggingface Space](https://huggingface.co/spaces/joyjkl/pm10-predictor) |
| Code         | [GitHub Repository](https://github.com/Jojoyoj/weather) |

## Data Sources and Features Used Per Source
| Data Source | Features |
|-------------|----------|
| [Open-Meteo API](https://open-meteo.com/) | temperature, humidity, wind speed |
| [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api) | PM10 concentration |

## Features Created
| Feature | Description |
|---------|-------------|
| PM10 category | Categorized pollution as Low (< 20 µg/m³), Moderate (20–40 µg/m³), High (> 40 µg/m³) |
| Input normalization | Sliders in Gradio restrict user input to realistic ranges |

## Model Training
### Amount of Data
- Historical hourly weather and PM10 data from Zurich between 2013 and 2024
- After merging and cleaning: ~105,000 records

### Data Splitting Method (Train/Test)
- 80/20 train-test split using `train_test_split` with `random_state=42`

### Performance

| It. Nr | Model | Performance | Description |
|--------|--------|-------------|-------------|
| 1 | Linear Regression | RMSE: 8.42, R²: 0.19 | Baseline model – underfitting |
| 2 | Random Forest Regressor | RMSE: 8.67, R²: 0.14 | Slightly worse R² but more flexible |
| 3 | Logistic Regression | Accuracy: 76%, Poor F1 on “High” | Classification – majority class bias |
| 4 | Random Forest Classifier | Accuracy: 73%, Better moderate recall | Better performance on moderate class, still weak on high pollution |

Final model selected: **Random Forest Regressor**  
Reason: more granular predictions, better continuous fit, deployable as a live estimator of pollution levels.

## Deployment
| Step | Description |
|------|-------------|
| Interface | Built with Gradio using sliders for temperature, humidity, wind speed |
| Output | Continuous prediction of PM10 (µg/m³) |
| Hosted on | Hugging Face Spaces (Gradio SDK, CPU environment) |
| Requirements | `gradio`, `scikit-learn`, `pandas`, `numpy`, `joblib` |
| Status | ✅ Live and tested |

## References
- [Open-Meteo API Docs](https://open-meteo.com/)
- [Gradio Documentation](https://gradio.app)
- [Hugging Face Spaces](https://huggingface.co/spaces)
