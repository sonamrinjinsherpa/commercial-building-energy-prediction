# commercial-building-energy-prediction

Machine learning and data analytics project for predicting peak energy demand in commercial buildings using the ASHRAE Great Energy Predictor III dataset.

## Project Objective

The project estimates when commercial buildings are most likely to reach their daily peak electricity demand. It combines historical hourly readings, building characteristics, time patterns, and weather conditions to provide building managers with a practical readiness window.

## Final Result

On the final chronological test period, the building-specific approach identified:

- 18.7% of daily peaks at the exact hour;
- 42.6% within one hour; and
- 57.6% within two hours.

Always assuming a 2:00 PM peak identified 34.3% within two hours. The building-specific approach improved the two-hour result by 23.3 percentage points.

## Notebook Organization

Run the main notebooks in this order:

1. `01_data_inspection.ipynb` - inspect the raw ASHRAE files.
2. `02_preprocessing.ipynb` - integrate and clean electricity, building, and weather data.
3. `03_eda.ipynb` - examine consumption, building types, weather, peak timing, and data quality.
4. `04_modeling_data_split.ipynb` - create chronological training, validation, and test periods.
5. `05_basic_tabular_models.ipynb` - establish hourly-consumption baselines.
6. `07_tabular_model_tuning.ipynb` - compare tuned hourly-consumption approaches.
7. `08_peak_hour_prediction.ipynb` - compare direct peak-hour approaches.
8. `09_indirect_peak_from_meter_reading.ipynb` - compare direct and indirect peak estimates.
9. `11_professor_feedback_validation.ipynb` - apply the locked quality policy and rolling validation.
10. `12_final_heldout_test_evaluation.ipynb` - perform the final chronological test evaluation.

The `notebooks/experiments/` directory contains approaches that were investigated but were not used in the final peak-hour solution. Notebook numbers are preserved to show the order in which the project developed.

- `06_lstm_forecasting.ipynb` evaluates LSTM forecasting as a separate sequential experiment.
- `10_improved_peak_hour_model.ipynb` contains an unexecuted model iteration that was superseded by Notebooks 11 and 12.

## Setup

Create a Python 3.12 environment and install the project dependencies:

```bash
python -m pip install -r requirements.txt
```

Place the ASHRAE Great Energy Predictor III CSV files in `data/raw/` before running the notebooks. Datasets, generated reports, figures, and trained model artifacts are intentionally excluded from Git.

## Final Data-Quality Policy

Complete building-days with changing readings are included in peak-hour evaluation. Flat-zero, flat-nonzero, and incomplete days remain available for review but are excluded from peak scoring because they do not provide a reliable daily maximum.

## Limitations

The final results are based on 2016 ASHRAE buildings and may change as building operations, occupancy, equipment, and weather patterns change. The current weather features use same-day summaries; an operational day-ahead implementation should replace them with weather forecasts available at prediction time.
