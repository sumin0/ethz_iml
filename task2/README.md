## Task 2.

#### Dataset description

The data of each patient is identified through a unique patient id (*pid*). In `train_features.csv`, medical data for each patient is arranged in 12 consecutive rows representing the information about the first 12 recorded hours of their hospital stay. The column Time provides the time after hospital admission (as an offset in hours) at which the vital sign / medical test measurements were observed. The column *Age* contains the age of the patient, and it is unique for a single *pid*. The columns *Heartrate*, *SpO2*, *ABPs*, *ABPm*, *ABPd*, *RRate*, *Temp* are vital signs. and the remaining columns without a 'LABEL' prefix are medical test observations. All of these columns can contain missing values, which are indicated by 'nan'.

While `train_features.csv` contains 12 entries for a patient (corresponding to the first 12 recorded hours of their stay), `train_labels.csv` contains 1 entry per patient, since these refer to the events during the remaining hours of the patient's stay.

**Note** Both `train_features.csv` and `test_features.csv` contain missing values ('nan' entries). An important part of this project is how to deal with such missing data (known as 'data imputation' in the ML literature) and feature engineering (what features can you extract from measurements taken in consecutive hours, etc.)

#### Subtask 1

Predict whether medical tests are ordered by a clinician in the remainder of the hospital stay: 0 means that there will be no further tests of this kind ordered, 1 means that at least one of a test of that kind will be ordered. In the submission file, you are asked to submit predictions in the interval [0, 1], i.e., the predictions are not restricted to binary. 0.0 indicates you are certain this test will not be ordered, 1.0 indicates you are sure it will be ordered. The corresponding columns containing the binary groundtruth in `train_labels.csv` are: *LABEL_BaseExcess, LABEL_Fibrinogen, LABEL_AST, LABEL_Alkalinephos, LABEL_Bilirubin_total, LABEL_Lactate, LABEL_TroponinI, LABEL_SaO2, LABEL_Bilirubin_direct, LABEL_EtCO2.*

#### Subtask 2

Predict whether sepsis will occur in the remaining stay: 0 means that no sepsis will occur, 1 otherwise. Similar to Subtask 1, you are asked to produce predictions in the interval [0, 1] for this task. The corresponding column containing the binary groundtruth in `train_labels.csv` is *LABEL_Sepsis*.

#### Subtask 3

Predict future mean values of key vital signs. The corresponding columns containing the real-valued groundtruth in `train_labels.csv` are *LABEL_RRate, LABEL_ABPm, LABEL_SpO2, LABEL_Heartrate.*

#### Evaluation

For subtasks 1 and 2 we calculate the Areas Under the Receiver Operating Characteristic Curve, aka ROC_AUC scores. For the regression subtask 3, we measure the $R^2$ score, threshold it below at 0 and normalize it to the range [0.5, 1]. Your final score is the average of these 3 scores. For your convenience, in the handout we provide you with the `get_score` function in score_submission.py, which shows how to calculate this score in Python.

